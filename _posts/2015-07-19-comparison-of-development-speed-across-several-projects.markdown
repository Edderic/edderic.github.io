# Comparison of Development Speeds Across Several Backlogs

In this post I take advantage of [my
findings](/2015/07/12/probability-of-hitting-deadlines-based-on-pivotal-tracker-points.html)
in incorporating variability in time taken to finish stories based on their
complexity estimates (`1`-point vs `2`-points). I would like to see how
different backlogs at Lingraphica compare in terms of quickly getting `1`-point
and `2`-point stories done. For kicks, I want to see the probability that a
set of stories (`5` `1`-pointers and `4` `2`-pointers) will get done under `8`
hours.

## Product Development
<figure>
<img src="/images/5-1-pointers-pd-under-8-hrs.png" alt="5 1-pointers distribution from Product Development">
<figcaption>
5 1-pointers distribution from Product Development
</figcaption>
</figure>

<figure>
<img src="/images/2-2-pointers-pd-under-8-hrs.png" alt="2 2-pointers distribution from Product Development">
<figcaption>
2 2-pointers distribution from Product Development
</figcaption>
</figure>

## SGDs

<figure>
<img src="/images/5-1-pointers-sgd-under-8-hrs.png" alt="5 1-pointers distribution from SGDs">
<figcaption>
5 1-pointers distribution from SGDs
</figcaption>
</figure>

<figure>
<img src="/images/2-2-pointers-sgd-under-8-hrs.png" alt="2 2-pointers distribution from SGDs">
<figcaption>
2 2-pointers distribution from SGDs
</figcaption>
</figure>

## Website Development

<figure>
<img src="/images/5-1-pointers-web-dev-under-8-hrs.png" alt="5 1-pointers distribution from Website Development">
<figcaption>
5 1-pointers distribution from Website Development
</figcaption>
</figure>

<figure>
<img src="/images/2-2-pointers-web-dev-under-8-hrs.png" alt="2 2-pointers distribution from Website Development">
<figcaption>
2 2-pointers distribution from Website Development
</figcaption>
</figure>

## Notes

With regards to the probability that `5` `1`-point stories can be done in `8` hours,
Website Development does the best (`100%`). SGD follows next (`59.1%`), while
Product Development lags only slightly behind SGDs (`54.6%`).

On the other hand, with regards to the probability that `2` `2`-point stories
can be done in `8` hours, Product Development does the best (`33%`), Website
Development does second best, although the probability precipitously drops
(`25%`), and SGDs does the worst (`18%`).

## Possible Questions to Explore in the Future

Are `2`-point stories in SGDs more complex than `2`-point stories in Product
Development and Website Development?

Are `1`-point stories in Website Development much easier than `1`-point stories
in either Product Development and SGDs?

Why is there such a big variation in the `2` `2`-pointer set of stories in
Website Development, relative to SGDs and Product Development? Is this because
designing the website inherently takes a lot of time (i.e. Are 2-pointer
stories involving design more open-ended than stories involving development)?
Or is it because of something else entirely?

Can more pairing speed up finish `2`-pointers faster in SGDs and Website
Development?
