# Personal Solutions to David Barber's Bayesian Reasoning and Machine Learning

I've decided to post my solutions to the problems in David Barber's Bayesian
Reasoning and Machine Learning book. My hope is that people who are in
self-study (such as myself) can compare answers with other people who are
self-studying. These are my own solutions to the problems and should not be
taken as reference. If you find any errors or would like to debate my answers,
please reach out to me via email in the meantime (until I add a comments
section). These will be updated regularly.

## Chapter 1

### Exercise 1.1

Prove
  \\(p(x,y | z) = p(x|z)p(y|x,z)\\)

  $$
  \begin{align}
  p(x,y | z) &= \frac{p(x,y,z)}{p(z)} \\
  p(x|z) &= \frac{p(x,z)}{p(z)} \\
  p(y|x,z) &= \frac{p(x,y,z)}{p(x,z)} \\
  \frac{p(x,y,z)}{p(z)} &= \frac{p(x,z)}{p(z)}\frac{p(x,y,z)}{p(x,z)} \\
  \frac{p(x,y,z)}{p(z)} &= \frac{p(x,y,z)}{p(z)} \\
  p(x,y | z) &= p(x|z)p(y|x,z)
  \end{align}
  $$

Prove
  \\(p(x|y,z) = \frac{p(y|x,z)p(x|z)}{p(y|z)}\\)

  $$
  \begin{align}
  p(x|y,z) &= \frac{p(x,y,z)}{p(y,z)} \\
  p(y|x,z) &= \frac{p(x,y,z)}{p(x,z)} \\
  p(x|z) &= \frac{p(x,z)}{p(z)} \\
  p(y|z) &= \frac{p(y,z)}{p(z)} \\
  \frac{p(x,y,z)}{p(y,z)} &= \frac{\frac{p(x,y,z)}{p(x,z)}\frac{p(x,z)}{p(z)}}{\frac{p(y,z)}{p(z)}} \\
  &= \frac{\frac{p(x,y,z)}{p(z)}}{\frac{p(y,z)}{p(z)}} \\
  &= \frac{p(x,y,z)}{p(z)}\frac{p(z)}{p(y,z)} \\
  &= \frac{p(x,y,z)}{p(y,z)} \\
  p(x|y,z) &= \frac{p(y|x,z)p(x|z)}{p(y|z)}
  \end{align}
  $$

### Exercise 1.2

Prove the Bonferroni inequality
\\(p(a,b) \geq p(a) + p(b) - 1\\)

$$
\begin{align}
p(a,b) &\geq p(a) + p(b) - 1 \\
p(a,b) + 1 &\geq p(a) + p(b) \\
1 &\geq p(a) + p(b) - p(a,b) \\
1 &\geq p(a \cup b)
\end{align}

$$

By definition, probabilities are always less than or equal to 1.
Therefore the statement is true.

### Exercise 1.3

There are two boxes. Box 1 contains three red and five white balls and box 2
contains two red and five white balls. A box is chosen at random \\(p(box = 1)
= p(box = 2) = 0.5\\) and a ball chosen at random from this box turns out to be
red.  What is the posterior probability that the red ball came from box 1?

We list the given information:

$$
\begin{align}
 p(color=red | box=1) &= \frac{3}{8} \\
 p(color=white | box=1) &= \frac{5}{8} \\
 p(color=red | box=2) &= \frac{2}{7} \\
 p(color=white | box=2) &= \frac{5}{7} \\
\end{align}
$$

We use Bayes' Rule to figure out the probability that the box is 1 given
that the picked ball is red:

$$
\begin{align}
 p(box=1 | color=red ) &= \frac{p(color=red,box=1)}{p(color=red)} \\
  &= \frac{p(color=red|box=1)p(box=1)}{p(color=red)} \\
\end{align}
$$

We calculate the numerator:

$$
\begin{align}
p(color=red|box=1)p(box=1) &= \frac{1}{2}\times\frac{3}{8}
\end{align}
$$

We find the marginal distribution of the color of the ball being red,
so that we can substitute it in the denominator:

$$
\begin{align}
 p(color=red) &= \Sigma_b p(color=red,box=b) \\
  &= \Sigma_b p(color=red|box=b)p(box=b) \\
  &= p(color=red|box=1)p(box=1) \\
  &+ p(color=red|box=2)p(box=2) \\
  &= \frac{3}{8}\times\frac{1}{2} + \frac{2}{7}\times\frac{1}{2} \\
\end{align}
$$

Finally, we substitute:

$$
\begin{align}
  p(box=1 | color=red ) &= \frac{\frac{3}{8}}{\frac{3}{8} + \frac{2}{7}} \\
  &= \frac{\frac{3}{8}}{\frac{21}{56} + \frac{16}{56}} \\
  &= \frac{\frac{3}{8}}{\frac{37}{56}} \\
  &= \frac{3}{8}\times\frac{56}{37} \\
  &= \frac{21}{37} \\
\end{align}
$$

### Exercise 1.4a

Two balls are placed in a box as follows: A fair coin is tossed and a white
ball is placed in the box if a head occurs, otherwise a red ball is placed in
the box. The coin is tossed again and a red ball is placed in the box if a tail
occurs, otherwise a white ball is placed in the box. Balls are drawn from the
box three times in succession (always with replacing the drawn ball back in the
box). It is found that on all three occasions a red ball is drawn. What is the
probability that both balls in the box are red?)

Because of the fair coin assumption:

$$
\begin{align}
  p(coin=heads) &= \frac{1}{2} \\
  p(coin=tails) &= \frac{1}{2}
\end{align}
$$

We calculate the probabilities of the ball being of a certain color, given the
flip of a coin:

$$
\begin{align}
  p(ball=white|coin=heads) &= 1 \\
  p(ball=red|coin=tails) &= 1 \\

  p(ball=white|coin=tails) &= 0 \\
  p(ball=red|coin=heads) &= 0

\end{align}
$$

We marginalize over the coin values to get the overall probability that
a ball is white:

$$
\begin{align}
  p(ball=white) &= \Sigma_c p(ball=white, coin=c) \\
    &= \Sigma_c p(ball=white| coin=c)p(coin=c) \\
    &= p(ball=white| coin=heads)p(coin=heads)  \\
    &+ p(ball=white| coin=tails)p(coin=tails) \\
    &= 1(\frac{1}{2}) + 0(\frac{1}{2}) \\
    &= \frac{1}{2}
\end{align}
$$

We do the same thing to get the overall probability that a ball is red:

$$
\begin{align}
  p(ball=red) &= \Sigma_c p(ball=red, coin=c) \\
    &= \Sigma_c p(ball=red| coin=c)p(coin=c) \\
    &= p(ball=red| coin=heads)p(coin=heads)  \\
    &+ p(ball=red| coin=tails)p(coin=tails) \\
    &= 0(\frac{1}{2}) + 1(\frac{1}{2}) \\
    &= \frac{1}{2}
\end{align}
$$

We calculate the probability that a ball picked is red, taking into
consideration the balls' colors:

$$
\begin{align}
p(pick=red|ball_1=red, ball_2=red) &= 1 \\
p(pick=red|ball_1=white, ball_2=red) &= \frac{1}{2} \\
p(pick=red|ball_1=red, ball_2=white) &= \frac{1}{2} \\
p(pick=red|ball_1=white, ball_2=white) &= 0 \\
\end{align}
$$

We use Bayes' Rule to figure out the posterior probability that both balls
are actually red, given that the three picks have been all red:

$$
  p(B_1=r, B_2=r | P_1=r, P_2=r, P_3=r) \\
  = \frac{p(P_1=r,P_2=r,P_3=r| B_1=r, B_2=r)p(B_1=r,B_2=r)}{p(P_1=r,P_2=r,P_3=r)} \\
$$

The probability of the color of Ball 1 is independent of the probability of the
color of Ball 2:

$$
\begin{align}
  p(B_1=r,B_2=r) &= p(B_1=r)p(B_2=r) \\
    &= \frac{1}{2} \times \frac{1}{2} \\
    &= \frac{1}{4}
\end{align}
$$

Since there is replacement of the ball after picking one, we can also assume
conditional independence:

$$
p(P_1=r,P_2=r,P_3=r| B_1=r, B_2=r) \\
= p(P_1=r| B_1=r, B_2=r) \\
\times p(P_2=r| B_1=r, B_2=r) \\
\times p(P_3=r| B_1=r, B_2=r) \\
= 1 \times 1 \times 1
$$

In the denominator, we marginalize out the ball values over the joint distribution:

$$
p(P_1=r,P_2=r,P_3=r) \\
= \Sigma_{b_2}\Sigma_{b_1} p(P_1=r, P_2=r, P_3=r, B_1=b_1, B_2=b_2) \\
= \Sigma_{b_2}\Sigma_{b_1} p(P_1=r, P_2=r, P_3=r|B_1=b_1, B_2=b_2) \\
\times p(B_1=b_1, B_2=b_2) \\
= p(B_1=b_1, B_2=b_2) \\
\times \Sigma_{b_2}\Sigma_{b_1} p(P_1=r, P_2=r, P_3=r|B_1=b_1, B_2=b_2) \\
$$

We substitute \\(p(B_1=b_1, B_2=b_2)\\) into the equation right above:

$$
= \frac{1}{4} \Sigma_{b_2}\Sigma_{b_1} p(P_1=r, P_2=r, P_3=r|B_1=b_1, B_2=b_2) \\
$$

We make the summations explicit:

$$
= \frac{1}{4} (p(P_1=r, P_2=r, P_3=r|B_1=r, B_2=r) \\
+ p(P_1=r, P_2=r, P_3=r|B_1=r, B_2=w) \\
+ p(P_1=r, P_2=r, P_3=r|B_1=w, B_2=r) \\
+ p(P_1=r, P_2=r, P_3=r|B_1=w, B_2=w)) \\
$$

Again, the event of picking a ball is independent of picking another ball
because of replacement. We already calculated the case when someone picks
three balls with replacement and both balls are actually red, so we'll just
calculate the rest of the combinations:

$$
p(P_1=r, P_2=r, P_3=r|B_1=r, B_2=w) \\
= p(P_1=r|B_1=r, B_2=w) \\
\times p(P_2=r|B_1=r, B_2=w) \\
\times p(P_2=r|B_1=r, B_2=w) \\
= \frac{1}{2} \times \frac{1}{2} \times \frac{1}{2} \\
= \frac{1}{8}
$$

$$
p(P_1=r, P_2=r, P_3=r|B_1=w, B_2=r) \\
= p(P_1=r|B_1=w, B_2=r) \\
\times p(P_2=r|B_1=w, B_2=r) \\
\times p(P_2=r|B_1=w, B_2=r) \\
= \frac{1}{2} \times \frac{1}{2} \times \frac{1}{2} \\
= \frac{1}{8}
$$

$$
p(P_1=r, P_2=r, P_3=r|B_1=w, B_2=w) \\
= p(P_1=r|B_1=w, B_2=w) \\
\times p(P_2=r|B_1=w, B_2=w) \\
\times p(P_2=r|B_1=w, B_2=w) \\
= 0 \times 0 \times 0 \\
= 0
$$

Substitute in the values:

$$
\begin{align}
p(P_1=r,P_2=r,P_3=r) &= \frac{1}{4} (1 + \frac{1}{8} + \frac{1}{8} + 0) \\
&= \frac{1}{4} (1 + \frac{1}{4}) \\
&= \frac{1}{4} (\frac{5}{4}) \\
\end{align}
$$

Finally, we substitute the values into Bayes' Rule:

$$
\begin{align}
  p(B_1=r, B_2=r | P_1=r, P_2=r, P_3=r) &= \frac{\frac{1}{4}}{\frac{1}{4}(\frac{5}{4})} \\
  &= \frac{4}{5} \\
\end{align}
$$

### Exercise 1.4b

A secret government agency has developed a scanner which determines whether a
person is a terrorist. The scanner is fairly reliable; 95% of all scanned
terrorists are identified as terrorists, and 95% of all upstanding citizens are
identified as such. An informant tells the agency that exactly one passenger of
100 aboard an aeroplane in which you are seated is a terrorist. The police haul
off the plane the first person for which the scanner tests positive. What is
the probability that this person is a terrorist?

"95% of all terrorists are identified as terrorists":

$$
p(label=true|terrorist=true) = 0.95
$$

We can infer from the former that only 5% of upstanding citizens got mislabeled
(false positive):

$$
p(label=true|terrorist=false) = 0.05
$$

"95% of all upstanding citizens are identified as such":

$$
p(label=false|terrorist=false) = 0.95
$$

We can infer, based on the previous equation, that 5% of terrorists get
misclassified (false negative):

$$
p(label=false|terrorist=true) = 0.05
$$

Assuming that the informant is correct:

$$
p(terrorist=true) = \frac{1}{100}
$$

We can then infer that \\(\frac{99}{100}\\) are not terrorists:

$$
p(terrorist=false) = \frac{99}{100}
$$

We can find out the probability that the person picked is a terrorist using Bayes' Rule:

$$
p(terrorist=true|label=true) \\
= \frac{p(label=true|terrorist=true)p(terrorist=true)}{p(label=true)} \\
$$

To find out the denominator, we can marginalize over the joint distribution
of \\(p(label=true)\\) and \\(p(terrorist)\\):

$$
    p(label=true) \\
    = \Sigma_{t} p(label=true, terrorist=t) \\
    = \Sigma_{t} p(label=true| terrorist=t)p(terrorist=t) \\
$$

We make the summation explicit:

$$
    p(label=true) \\
    = p(label=true| terrorist=true)p(terrorist=true) \\
    + p(label=true| terrorist=false)p(terrorist=false) \\
    = 0.95(0.01) + 0.05(0.99) \\
    = 0.059
$$

Substituting all the values into Bayes' Rule, we find out that even though
the detector is "reliable," we still get a low posterior probability that the
person suspected of being a terrorist is actually a terrorist:

$$
p(terrorist=true|label=true) \\
= \frac{p(label=true|terrorist=true)p(terrorist=true)}{p(label=true)} \\
= \frac{0.95(0.01)}{.059} \\
= 0.1610169492 \\
$$

### Exercise 1.7

Repeat the Inspector Clouseau scenario, example(1.3), but with the restriction
that either the maid or the butler is the murderer, but not both. Explicitly,
the probability of the maid being the murderer and not the butler is 0.04, the
probability of the butler being the murderer and not the maid is 0.64. Modify
*demoClouseau.m* to implement this.)

    pot(knife).variables=[knife,butler,maid]; % define array below using this variable order

    pot(knife).table(used, notmurderer, notmurderer)=0.3;
    pot(knife).table(used, notmurderer, murderer)   =0.04;
    pot(knife).table(used, murderer,    notmurderer)=0.64;
    pot(knife).table(used, murderer,    murderer)   =0.0;

Results:

    p(butler|knife=used):
    butler  =murderer       0.755906
    butler  =not murderer   0.244094

### Exercise 1.8

Prove \\(p(a,(b\ or\ c)) = p(a,b)+p(a,c)−p(a,b,c)\\)

$$
\begin{align}
  p(a,(b\ or\ c)) &= p(a,b)+p(a,c)−p(a,b,c) \\
  &= p(a)p(b\ or\ c) \\
  &= p(a)(p(b) + p(c) - p(b,c)) \\
  &= p(a)p(b) + p(a)p(c) - p(a)p(b,c) \\
  &= p(a,b) + p(a,c) - p(a,b,c) \\
\end{align}
$$

