# Probability of Hitting Deadlines Based on Pivotal Tracker Points

## Introduction

As software developers, we know how important it is to give reliable time
estimates to the business.  Business people would like to know how long
milestones will get done so that they can reprioritize goals if needed.
However, estimating the time it takes to develop software is hard:

<figure>
   <img src="http://imgs.xkcd.com/comics/estimation.png" alt="Estimation is hard">
<figcaption>
Estimation is hard
</figcaption>
</figure>

 So many
things can introduce variability into how long stories get done in relation to
the estimates:

* unforeseen complications (i.e. it was harder than was previously thought).
* someone who used to work on your backlog is pulled out and tasked to focus on a different project.
* someone you need in order to keep moving on the story, is in a meeting with other people.
* coworker takes paid time off.

Time estimation is hard, and that is why agile project management software like
Pivotal Tracker lets developers estimate *complexity* instead: stories
estimated as "1" are easy, "2" as medium, etc. Pivotal Tracker calculates
*velocity* and *volatility*, which are useful in reporting to the business.
Velocity is how fast the team is able to finish stories, taking into account
the complexity, and averaged over time.  Volatility calculates how much the
velocity has changed over time, which affects our confidence on the velocity.

However, this system might be too simplistic. For example, 20 points made up of
20 1-pointers might drastically be done faster than 10 2-pointers. In order to
test this hunch, I extracted the product development accepted stories (feature,
bug, chore) and calculated the elapsed time between the time stories were
started and the time stories were delivered, for the last six months. I came up
with the following probability distributions (binned to the nearest hour, with
major outliers removed):


<figure>
   <img src="/images/1-point-distribution-over-time.png" alt="1-point distribution">
<figcaption>
</figcaption>
</figure>

<figure>
   <img src="/images/2-point-distribution-over-time.png" alt="2-point distribution">
<figcaption>
</figcaption>
</figure>

Looking at the histograms of 1-point stories and 2-point stories verifies the
intuition that a backlog that is dominated by two-point stories will probably
take longer than a backlog that isn't, given that the total points are the same.
The 2-point probability distribution has a significant amount of stories that take
longer than 10 hours. Summing the probabilities from 11th hour to the end shows that
there is about a 30% chance that a 2-point story will take longer than 10 hours.
On the other hand, there is a 0% chance that a 1-point story will take longer than
ten hours, given this data without outliers.

## Computing the probability of how long milestones will take

So how do we calculate our "confidence" in finishing a milestone, given that
`X` amount of stories are estimated to be 1-point and `Y` amount of stories are
estimated to be 2-points?

According to [Wikipedia](https://en.wikipedia.org/wiki/Convolution):

> In probability theory, the probability distribution of the sum of two
> independent random variables is the convolution of their individual
> distributions.


<figure>
   <img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Convolution_of_spiky_function_with_box2.gif" alt="Convolution of spiky function with box">
<figcaption>
  Convolution of spiky function with box
</figcaption>
</figure>

The independent random variables we would like to consider, more explicitly, are
that of times elapsed given a story estimate (one-point and two-points).

For example, let's say a milestone has 5 1-pointers and 2 2-pointers. Let's
represent the time-elapsed distribution over a 1-pointer as `A`, and let's
represent the time-elapsed distribution over a 2-pointer as `B`. Thus, we could
get the `T` total distribution by convolving the distributions as follows:

```
T(t) = A(t) * A(t) * A(t) * A(t) * A(t) *
B(t) * B(t)
```

where `*` is the convolution operator.

## Experiment

Let's derive the total distribution iteratively and see whether our gut
feelings agree with the total distribution.

### Nine 1-pointers

<figure>
   <img src="/images/one-1-point.png" alt="Original 1-point">
<figcaption>
  Original 1-point time-elapsed distribution
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself.png" alt="One-point convolved with itself">
<figcaption>
  A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-twice.png" alt="One-point convolved with itselftwice">
<figcaption>
  A(t) * A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-thrice.png" alt="One-point convolved with itself thrice">
<figcaption>
  A(t) * A(t) * A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-four-times.png" alt="One-point convolved with itself four times">
<figcaption>
  A(t) * A(t) * A(t) * A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-five-times.png" alt="One-point convolved with itself five times">
<figcaption>
  A(t) * A(t) * A(t) * A(t) * A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-six-times.png" alt="One-point convolved with itself six times">
<figcaption>
  A(t) * A(t) * A(t) * A(t) * A(t) * A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-seven-times.png" alt="One-point convolved with itself seven times">
<figcaption>
  A(t) * A(t) * A(t) * A(t) * A(t) * A(t) * A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-eight-times.png" alt="One-point convolved with itself eight times">
<figcaption>
  A(t) * A(t) * A(t) * A(t) * A(t) * A(t) * A(t) * A(t) * A(t)
</figcaption>
</figure>

With regards to nine 1-pointers, 24 hours gives us a 95.7% probability, while
48 and 72 hours give us 99.9%. One might think that the 24-hour estimate for
nine 1-pointers might too optimistic. I'd argue that it makes sense since
a large chunk, 35%, a little bit over a third, of 1-pointers took less than 30
minutes to complete.

### Five 1-pointers and Two 2-pointers

Again let's use the example 5 1-pointers and 2 2-pointers.


<figure>
   <img src="/images/one-1-point.png" alt="Original 1-point">
<figcaption>
  Original 1-point time-elapsed distribution
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself.png" alt="One-point convolved with itself">
<figcaption>
  A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-twice.png" alt="One-point convolved with itselftwice">
<figcaption>
  A(t) * A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-thrice.png" alt="One-point convolved with itself thrice">
<figcaption>
  A(t) * A(t) * A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-four-times.png" alt="One-point convolved with itself four times">
<figcaption>
  A(t) * A(t) * A(t) * A(t) * A(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-four-times-then-convolved-with-2-point.png" alt="One-point convolved with itself four times then convolved with two-point">
<figcaption>
  A(t) * A(t) * A(t) * A(t) * A(t) * B(t)
</figcaption>
</figure>

<figure>
   <img src="/images/1-point-convolved-with-itself-four-times-then-convolved-with-2-point-twice.png" alt="One-point convolved with itself four times then convolved with two-point twice">
<figcaption>
  A(t) * A(t) * A(t) * A(t) * A(t) * B(t) * B(t)
</figcaption>
</figure>

According to my program, the team will be able to finish the milestone with 5
1-point and 2 2-point stories with 49.5% confidence in 24 hours, 78.3% in 48
hours, and 95.5% in 72 hours. It makes sense that the introduction of 2-pointers
significantly lowered the confidence since 2-pointers have much more variability.

### Four 2-pointers

<figure>
   <img src="/images/2-point-distribution-over-time.png" alt="Two-point distribution over time">
<figcaption>
  B(t)
</figcaption>
</figure>

<figure>
   <img src="/images/2-point-convolved-with-itself.png" alt="Two-point convolved with itself">
<figcaption>
  B(t) * B(t)
</figcaption>
</figure>

<figure>
   <img src="/images/2-point-convolved-with-itself-twice.png" alt="Two-point convolved with itself-twice">
<figcaption>
  B(t) * B(t) * B(t)
</figcaption>
</figure>

<figure>
   <img src="/images/2-point-convolved-with-itself-thrice.png" alt="Two-point convolved with itself-thrice">
<figcaption>
  B(t) * B(t) * B(t) * B(t)
</figcaption>
</figure>

24 hours gives us 26.7%. 48 hours gives us 55.6%. 72 hours gives us 80.5%.
This is inline with our thinking -- that a milestone with 2-pointers probably
will take longer to do than a milestone with 1-pointers, given equal total
estimates. In this case, the milestone with 4 2-pointers is much more likely to
take longer than 9 1-pointers, even though the total points assigned to the
former is less than the total points assigned to the latter.

## Conclusion

Total of assigned points in a milestone might not be sufficient in accurately
predicting how long the milestone will take to get finished. I have come up
with a way to incorporate variability introduced by different point estimates
into determining what the probability of hitting a milestone is, based on past
activity. I hope that this might be able to guide software development teams in
accurately and reliably reporting estimates so that businesses can make better
decisions.  Stay tuned for another post -- I might actually share the code that
pulls-in the data, cleans it, and computes the probabilities. Till next time.
