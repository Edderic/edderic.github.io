---
layout: default
---

# Stubbing Multiple CarrierWave Buckets with Fog

At work, I came across the issue of having to deal with having multiple Amazon S3 buckets.
Our file-uploading section of our `rails_helper` originally was like the following:
{% highlight ruby linenos %}
Fog.mock!
Fog.credentials_path = Rails.root.join('config/fog_credentials.yml')
connection = Fog::Storage.new(:provider => 'AWS')
connection.directories.create(:key => CarrierWave::Uploader::Base.fog_directory)
{% endhighlight %}

New requirements dictated that we were going to make new uploaders to S3, and that they
are going to be stored in a different bucket by overriding the fog directory:
{% highlight ruby linenos %}
class ArticleCSVUploader < CarrierWave::Uploader::Base
  storage :fog
  include ::CarrierWave::Backgrounder::Delay

  def store_dir
    "articles/#{model.id}"
  end

  def extension_white_list
    %w(csv)
  end

  def fog_directory
    "news-app-#{Rails.env}"
  end
end
{% endhighlight %}

Our Article model is as follows:

{% highlight ruby linenos %}
class Article < ActiveRecord::Base
  attr_accessible :csv

  mount_uploader :csv, ArticleCSVUploader
end
{% endhighlight %}

We wrote the test for the uploader like so:

{% highlight ruby linenos %}
require 'rails_helper'

describe ArticleCSVUploader do
  after  { uploader.remove! }

  let(:article)    { FactoryGirl.create(:article) }
  let(:uploader) { ArticleCSVUploader.new(article) }

  describe '#store_dir' do
    it 'should just be articles/#{model.id}' do
      expect(uploader.store_dir).to eq "articles/#{article.id}"
    end
  end

  describe "with a valid csv" do
    let(:csv) { File.open(Rails.root.join('spec', 'fixtures', "some.csv")) }
    before do
      ArticleCSVUploader.class_eval { storage :file }
      uploader.store!(csv);
    end

    context 'the uploaded csv' do
      it "is stored in S3" do
        expect(uploader.to_s).to include(article.csv.to_s)
      end
    end
  end

  describe "with a filename ending in foo" do
    let(:csv) { File.open(Rails.root.join('spec', 'fixtures', "myface.foo")) }

    it "won't allow the csv to be uploaded" do
      expect { uploader.store!(csv) }.to raise_error(CarrierWave::IntegrityError)
    end
  end
end
{% endhighlight %}

However, running the test gives us an error:
{% highlight bash %}
ArticleCSVUploader
  #store_dir

  An error occurred in an after hook
    Excon::Errors::NotFound: Expected(200) <=> Actual(404 Not Found)

    occurred at /Users/eddericugaddan/.rvm/gems/ruby-2.2.0/gems/fog-1.26.0/lib/fog/aws/requests/storage/shared_mock_methods.rb:30:in `verify_mock_bucket_exists'

    should just be articles/#{model.id} (FAILED - 1)

Failures:

  1) ArticleCSVUploader#store_dir should just be articles/#{model.id}
     Failure/Error: let(:article)    { FactoryGirl.create(:article) }
     Excon::Errors::NotFound:
       Expected(200) <=> Actual(404 Not Found)
     # ./spec/uploaders/article_csv_uploader_spec.rb:6:in `block (2 levels) in <top (required)>'
     # ./spec/uploaders/article_csv_uploader_spec.rb:7:in `block (2 levels) in <top (required)>'
     # ./spec/uploaders/article_csv_uploader_spec.rb:12:in `block (3 levels) in <top (required)>'

{% endhighlight %}

The error here is not as verbose as I would have liked it to have been. It doesn't say why I was getting the `404` error. However, it does give me an idea which part of the `Fog` gem gave the error. I open up the `/fog/aws/requests/storage/shared_mock_methods` file and look at put a breakpoint before line 30:

{% highlight bash %}
$ rspec spec/uploaders/article_csv_uploader_spec.rb:4
Using Rack::Test
Run options: include {:locations=>{"./spec/uploaders/article_csv_uploader_spec.rb"=>[4]}}

ArticleCSVUploader
  #store_dir

[20, 29] in /Users/eddericugaddan/.rvm/gems/ruby-2.2.0/gems/fog-1.26.0/lib/fog/aws/requests/storage/shared_mock_methods.rb
   20:           data
   21:         end
   22:
   23:         def verify_mock_bucket_exists(bucket_name)
   24:           require 'byebug'; byebug
=> 25:           if (bucket = self.data[:buckets][bucket_name])
   26:             return bucket
   27:           end
   28:
   29:           response = Excon::Response.new
(byebug) bucket_name
"news-app-test"
(byebug) self.data[:buckets]
{"exercises-test"=>{:objects=>{}, "Name"=>"exercises-test", "CreationDate"=>2015-04-02 07:11:51 -0400, "Owner"=>{"DisplayName"=>"owner", "ID"=>"some_id"}, "Payer"=>"BucketOwner", "LocationConstraint"=>"us-west-1"}}
(byebug)
{% endhighlight %}

There is no "news-app-test" bucket! Only "exercises-test". I search for `exercises-` in the project and found out that the fog directory is being set in the `CarrierWave` configuration file:

{% highlight ruby linenos %}
CarrierWave.configure do |config|
  config.fog_credentials = {
    :provider => 'AWS',
    aws_access_key_id: 'somekeyid',
  	aws_secret_access_key: 'somesecretaccesskey',
  	region: 'us-west-1'
  }
  config.fog_directory = "exercises-#{Rails.env}"
  config.cache_dir = "#{Rails.root}/tmp/uploads"
end
{% endhighlight %}

I go back to `rails_helper` and inspect `CarrierWave::Uploader::Base.fog_directory`:

{% highlight bash %}
$ rspec spec/uploaders/article_csv_uploader_spec.rb:11
Using Rack::Test

[42, 51] in /Users/eddericugaddan/Developer/Lingraphica/Lingraphica-Exercise-Editor/spec/rails_helper.rb
   42:
   43: Fog.mock!
   44: Fog.credentials_path = Rails.root.join('config/fog_credentials.yml')
   45: connection = Fog::Storage.new(:provider => 'AWS')
   46: require 'byebug'; byebug
=> 47: connection.directories.create(:key => CarrierWave::Uploader::Base.fog_directory)
   48: #
   49: # needed for ArticleCSVUploader, ArticleImageUploader, and ArticleSonudUploader
   50: connection.directories.create(:key => 'news-app-test')
   51:
(byebug) CarrierWave::Uploader::Base.fog_directory
"exercises-test"
(byebug)
{% endhighlight %}

This gave me the idea of adding the following line:
{% highlight ruby %}
connection.directories.create(:key => 'news-app-test')
{% endhighlight %}

That got the tests to go all green.

## Final words

The lesson that I got here is that sometimes it's a really good idea to source dive
to improve the debugging experience. Sometimes, the error we get is not verbose enough
to tell us specifically why something is not working right. Jumping into the innards of
an external, traditionally blackbox, library and sprinkling in some debugging statements
could give us the next hint that could help us to ultimately solve the problem at hand.

