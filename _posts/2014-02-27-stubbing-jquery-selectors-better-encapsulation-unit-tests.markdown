---
layout: default
---

# Stubbing jQuery Selectors For Better Encapsulation in Unit Tests

I use a lot of jQuery at work for DOM manipulation and interaction in our
web apps.  In our unit tests, we tended not to stub out this external dependency,
and made sure to use appropriate HTML fixtures so that jQuery calls can give us
the expected outputs.

{% highlight javascript linenos %}
describe('AnalogClockWidget', function() {
  describe('on resize', function() {
    it('should recreate the clock circle', function() {
      var clockHTML = '<div class="clock">' +
        '<div class="short-hand"></div>' +
        '<div class="long-hand"></div>' +
        '</div>';

      $('#jasmine_content').html(clockHTML);

      // expectations down here...
    });
  });

  // More tests...
});
{% endhighlight %}

More recently, however, I was tasked to make use of the `jstree` plugin. Following the same theme of using
HTML fixtures, I got something like this:

{% highlight javascript linenos %}
describe('SomeTree', function() {
  it('reconstructs the tree', function() {
    var content = '<ul class="jstree-container-ul jstree-children" role="group"><li role="treeitem" data-node-id="12" aria-selected="false" aria-level="1" aria-labelledby="j1_1_anchor" aria-expanded="false" id="j1_1" class="jstree-node  jstree-closed jstree-last"><i class="jstree-icon jstree-ocl" role="presentation"></i><a class="jstree-anchor" href="#" tabindex="-1" id="j1_1_anchor"><i class="jstree-icon jstree-themeicon" role="presentation"></i>MyString(+)</a></li></ul>'
    $('#jasmine_content').html(content)

    // more setup and expectations here...
  })
})
{% endhighlight %}

As you can see, it does not look pretty. The `content` HTML is showing us
a lot of the innards of the `jstree` plugin, a lot of which should be black
box -- from my perspective as a client of third-party plugins at least. We
could perhaps load the HTML fixtures and hide the horrendous HTML if we use
<a href="https://github.com/velesin/jasmine-jquery">veselin/jasmine-jquery</a> gem:


{% highlight javascript linenos %}

loadFixtures('myfixture.html')
$('#my-fixture').myTestedPlugin()
expect($('#my-fixture')).to...

{% endhighlight %}

However, that would add another <a
href="https://robots.thoughtbot.com/mystery-guest">Mystery Guest</a>
to this test, and still not solve the issue of having *irrelevant information*.
What we care about in this `jstree` HTML example, as far as encapsulation and
my application logic is concerned, is that each of the `li` tags have
`data-node-id` attributes, and nothing else, but those attributes are being hidden
by other attributes and boilerplate tags like `aria-selected`, `aria-level`, etc.
Those attributes and tags are vital for `jstree` to work, they just make it
harder for other software developers to understand what really matters, in the
context of the unit test.

## Solution: Stub jQuery Selectors

{% highlight javascript linenos %}
// in the context of 'beforeEach' or 'it' block

// var positionValSpy, etc.

positionValSpy = jasmine.createSpy('val')
parentIdValSpy = jasmine.createSpy('val')
showModalSpy = jasmine.createSpy('showModal')
closeSpy = jasmine.createSpy('close')
cancelSpy = jasmine.createSpy('cancel')
htmlSpy = jasmine.createSpy('html')
appendSpy = jasmine.createSpy('appendSpy')
getSgdObjectsSpy = spyOn($, 'get')

jQueryStub = function(param) {
  switch(param) {
    case '#sgd_node_position':
      return { val: positionValSpy };
    case '#sgd_node_parent_id':
      return { val: parentIdValSpy };
    case '#sgd_node_sgd_object_id':
      return { html: htmlSpy, append: appendSpy };
    case '#nodeDialog':
      return [
        { showModal: showModalSpy, close: closeSpy }
      ];
    case '#cancel':
      return { click: cancelSpy };
    case '.new_sgd_node input[type="submit"]':
      return { click: function() { } };
    default:
      throw "Error: Did not recognize the selector";
  }
}

spyOn(window, '$').and.callFake(jQueryStub)


{% endhighlight %}

Stubbing `jQuery` lets us do queries like `$('#sgd_node_position').val()`,
which will return us fake objects that just have the right amount of
information we need in the context of a unit-test.

