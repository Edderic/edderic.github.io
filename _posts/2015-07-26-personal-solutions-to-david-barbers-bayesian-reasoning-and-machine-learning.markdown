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

We can infer from the former that only 5% of terrorists got mislabeled as
good people (false negative):

$$
p(label=false|terrorist=true) = 0.05
$$

"95% of all upstanding citizens are identified as such":

$$
p(label=false|terrorist=false) = 0.95
$$

We can infer, based on the previous equation, that 5% of good citizens get
misclassified as terrorists (false positive):

$$
p(label=true|terrorist=false) = 0.05
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

{% highlight matlab %}
pot(knife).variables=[knife,butler,maid];

pot(knife).table(used, notmurderer, notmurderer)=0.3;
pot(knife).table(used, notmurderer, murderer)   =0.04;
pot(knife).table(used, murderer,    notmurderer)=0.64;
pot(knife).table(used, murderer,    murderer)   =0.0;
{% endhighlight %}

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

### Exercise 1.9

Prove:

$$
    p(x|z) = \Sigma_y p(x|y, z)p(y|z) = \Sigma_{y,w} p(x|w, y, z)p(w|y, z)p(y|z)
$$

$$

\begin{align}
    \Sigma_y p(x|y, z)p(y|z)  &= \Sigma_y \frac{p(x,y, z)}{p(y,z)}\frac{p(y,z)}{p(z)} \\
    &= \Sigma_y \frac{p(x,y,z)}{p(z)} \\
    &= \frac{p(x,z)}{p(z)} \\
    &= p(x|z) \\
    \Sigma_{y,w} p(x|w,y,z)p(w|y,z)p(y|z) &= \Sigma_{y,w}\frac{p(x,w,y,z)}{p(w,y,z)}\frac{p(w,y,z)}{p(y,z)}\frac{p(y,z)}{p(z)} \\
    &= \Sigma_{y,w}\frac{p(x,w,y,z)}{p(z)} \\
    &= \frac{p(x,z)}{p(z)} \\
    &= p(x|z) \\
\end{align}
$$

### Exercise 1.10

*As a young man Mr Gott visits Berlin in 1969. He’s surprised that he cannot
cross into East Berlin since there is a wall separating the two halves of the
city. He’s told that the wall was erected 8 years previously. He reasons that :
The wall will have a finite lifespan; his ignorance means that he arrives
uniformly at random at some time in the lifespan of the wall. Since only 5% of
the time one would arrive in the first or last 2.5% of the lifespan of the wall
he asserts that with 95% confidence the wall will survive between 8/0.975 ≈ 8.2
and 8/0.025 = 320 years. In 1989 the now Professor Gott is pleased to find that
his prediction was correct and promotes his prediction method in prestigious
journals. This ‘delta-t’ method is widely adopted and used to form predictions
in a range of scenarios about which researchers are ‘totally ignorant’. Would
you ‘buy’ a prediction from Prof. Gott? Explain carefully your reasoning.*

I would think that it would be hard to be totally ignorant about something
if we are really trying hard to create a good model that predicts the lifespan
of something. In this specific case of the Berlin Wall, I believe that knowing
about tensions between East Germany and West Germany would seriously change
someone's prior belief that it will fall in a certain period of time. Therefore,
I would not 'buy' a prediction from Prof. Gott.

### Exercise 1.11

Implement the soft XOR gate, example(1.7) using BRMLtoolbox. You may find
condpot.m of use.)

{% highlight matlab %}

    function demoSoftXOR
    a=1; b=2; c=3; % variables
    on=1; off=2; % states

    % The following definitions of variable are not necessary for computation,
    % but are useful for displaying table entries:
    variable(a).name='a'; variable(a).domain = {'on','off'};
    variable(b).name='b'; variable(b).domain ={'on','off'};
    variable(c).name='c'; variable(c).domain={'on','off'};

    % Three potentials since p(a,b,c)=p(c|a,b)p(a)p(b).
    % potential numbering is arbitary
    pot(a).variables=a;
    pot(a).table(on)=0.65;
    pot(a).table(off)=0.35;

    pot(b).variables=b;
    pot(b).table(on)=0.77;
    pot(b).table(off)=0.23;

    pot(c).variables=[c,a,b]; % define array below using this variable order
    pot(c).table(on, off, off) =0.1;
    pot(c).table(on, off, on)  =0.99;
    pot(c).table(on, on, off)  =0.8;
    pot(c).table(on, on, on)   =0.25;
    pot(c).table(off,:,:)=1-pot(c).table(on,:,:); % due to normalisation

    jointpot = multpots(pot([a b c])); % joint distribution

    drawNet(dag(pot),variable);
    disp('p(a|c=0):')
    disptable(condpot(setpot(jointpot,c,off),a),variable);
{% endhighlight %}

Results:

    octave:6> demoSoftXOR
    p(a|c=0):
    a       =on     0.843585
    a       =off    0.156415

### Exercise 1.12

Implement the hamburgers, example(1.2) (both scenarios) using BRMLtoolbox. To
do so you will need to define the joint distribution \\(p(hamburgers,KJ)\\) in which
\\(dom(hamburgers) = dom(KJ) = {tr, fa}.\\)

TODO


### Exercise 1.13

Implement the two-dice example, section(1.3.1) using BRMLtoolbox.

{% highlight matlab %}

function demoTwoDice
%DEMOCLOUSEAU inspector clouseau example
s1=1; s2=2; t=3; % Variable order is arbitary

% define states, starting from 1.
one=1; two=2; three=3; four=4; five=5; six=6;
seven=7; eight=7; nine=7; ten=7; eleven=7; twelve=7;

% The following definitions of variable are not necessary for computation,
% but are useful for displaying table entries:
variable(s1).name='s1';
variable(s1).domain = {'one',
  'two',
  'three',
  'four',
  'five',
  'six'};
variable(s2).name='s2';
variable(s2).domain ={'one','two','three', 'four', 'five', 'six'};

variable(t).name='t';
variable(t).domain ={'two', \
  'three', \
  'four', \
  'five', \
  'six', \
  'seven', \
  'eight', \
  'nine', \
  'ten', \
  'eleven', \
  'twelve' };

% Three potentials since p(s1,s2,t)=p(t|s1,s2)p(s1)p(s2).
% potential numbering is arbitary
pot(s1).variables=s1;
pot(s1).table(one)=0.16666;
pot(s1).table(two)=0.16666;
pot(s1).table(three)=0.16666;
pot(s1).table(four)=0.16666;
pot(s1).table(five)=0.16666;
pot(s1).table(six)=0.16666;

pot(s2).variables=s2;
pot(s2).table(one)=0.16666;
pot(s2).table(two)=0.16666;
pot(s2).table(three)=0.16666;
pot(s2).table(four)=0.16666;
pot(s2).table(five)=0.16666;
pot(s2).table(six)=0.16666;

pot(t).variables=[t,s1,s2]; % define array below using this variable order
pot(t).table(2 , 1 , 1)=1;

pot(t).table(3 , 1 , 2)=1;
pot(t).table(3 , 2 , 1)=1;

pot(t).table(4 , 1 , 3)=1;
pot(t).table(4 , 3 , 1)=1;
pot(t).table(4 , 2 , 2)=1;

pot(t).table(5 , 1 , 4)=1;
pot(t).table(5 , 4 , 1)=1;
pot(t).table(5 , 2 , 3)=1;
pot(t).table(5 , 3 , 2)=1;

pot(t).table(6 , 1 , 5)=1;
pot(t).table(6 , 5 , 1)=1;
pot(t).table(6 , 2 , 4)=1;
pot(t).table(6 , 4 , 2)=1;
pot(t).table(6 , 3 , 3)=1;

pot(t).table(7 , 1 , 6)=1;
pot(t).table(7 , 6 , 1)=1;
pot(t).table(7 , 2 , 5)=1;
pot(t).table(7 , 5 , 2)=1;
pot(t).table(7 , 3 , 4)=1;
pot(t).table(7 , 4 , 3)=1;

pot(t).table(8 , 2 , 6)=1;
pot(t).table(8 , 6 , 2)=1;
pot(t).table(8 , 3 , 5)=1;
pot(t).table(8 , 5 , 3)=1;
pot(t).table(8 , 4 , 4)=1;

pot(t).table(9 , 3 , 6)=1;
pot(t).table(9 , 6 , 3)=1;
pot(t).table(9 , 4 , 5)=1;
pot(t).table(9 , 5 , 4)=1;

pot(t).table(10, 6, 4)=1;
pot(t).table(10, 4, 6)=1;
pot(t).table(10, 5, 5)=1;

pot(t).table(11, 6, 5)=1;
pot(t).table(11, 5, 6)=1;

pot(t).table(12, 6, 6)=1;

jointpot = multpots(pot([s1 s2 t])); % joint distribution

drawNet(dag(pot),variable);
disp('p(s1,s2|t=9):')
disptable(condpot(setpot(jointpot,t,9),[s1,s2]),variable);

{% endhighlight %}

Results:

    octave:27> demoTwoDice
    p(s1,s2|t=9):
    s1      =one    s2      =one    0.000000
    s1      =two    s2      =one    0.000000
    s1      =three  s2      =one    0.000000
    s1      =four   s2      =one    0.000000
    s1      =five   s2      =one    0.000000
    s1      =six    s2      =one    0.000000
    s1      =one    s2      =two    0.000000
    s1      =two    s2      =two    0.000000
    s1      =three  s2      =two    0.000000
    s1      =four   s2      =two    0.000000
    s1      =five   s2      =two    0.000000
    s1      =six    s2      =two    0.000000
    s1      =one    s2      =three  0.000000
    s1      =two    s2      =three  0.000000
    s1      =three  s2      =three  0.000000
    s1      =four   s2      =three  0.000000
    s1      =five   s2      =three  0.000000
    s1      =six    s2      =three  0.250000
    s1      =one    s2      =four   0.000000
    s1      =two    s2      =four   0.000000
    s1      =three  s2      =four   0.000000
    s1      =four   s2      =four   0.000000
    s1      =five   s2      =four   0.250000
    s1      =six    s2      =four   0.000000
    s1      =one    s2      =five   0.000000
    s1      =two    s2      =five   0.000000
    s1      =three  s2      =five   0.000000
    s1      =four   s2      =five   0.250000
    s1      =five   s2      =five   0.000000
    s1      =six    s2      =five   0.000000
    s1      =one    s2      =six    0.000000
    s1      =two    s2      =six    0.000000
    s1      =three  s2      =six    0.250000
    s1      =four   s2      =six    0.000000
    s1      =five   s2      =six    0.000000
    s1      =six    s2      =six    0.000000
