# Personal Solutions to David Barber's Bayesian Reasoning and Machine Learning (Chapter 1)

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
  \\(p(x,y \mid  z) = p(x\mid z)p(y\mid x,z)\\)

  $$
  \begin{align}
  p(x,y \mid  z) &= \frac{p(x,y,z)}{p(z)} \\
  p(x\mid z) &= \frac{p(x,z)}{p(z)} \\
  p(y\mid x,z) &= \frac{p(x,y,z)}{p(x,z)} \\
  \frac{p(x,y,z)}{p(z)} &= \frac{p(x,z)}{p(z)}\frac{p(x,y,z)}{p(x,z)} \\
  \frac{p(x,y,z)}{p(z)} &= \frac{p(x,y,z)}{p(z)} \\
  p(x,y \mid  z) &= p(x\mid z)p(y\mid x,z)
  \end{align}
  $$

Prove
  \\(p(x\mid y,z) = \frac{p(y\mid x,z)p(x\mid z)}{p(y\mid z)}\\)

  $$
  \begin{align}
  p(x\mid y,z) &= \frac{p(x,y,z)}{p(y,z)} \\
  p(y\mid x,z) &= \frac{p(x,y,z)}{p(x,z)} \\
  p(x\mid z) &= \frac{p(x,z)}{p(z)} \\
  p(y\mid z) &= \frac{p(y,z)}{p(z)} \\
  \frac{p(x,y,z)}{p(y,z)} &= \frac{\frac{p(x,y,z)}{p(x,z)}\frac{p(x,z)}{p(z)}}{\frac{p(y,z)}{p(z)}} \\
  &= \frac{\frac{p(x,y,z)}{p(z)}}{\frac{p(y,z)}{p(z)}} \\
  &= \frac{p(x,y,z)}{p(z)}\frac{p(z)}{p(y,z)} \\
  &= \frac{p(x,y,z)}{p(y,z)} \\
  p(x\mid y,z) &= \frac{p(y\mid x,z)p(x\mid z)}{p(y\mid z)}
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
 p(color=red \mid  box=1) &= \frac{3}{8} \\
 p(color=white \mid  box=1) &= \frac{5}{8} \\
 p(color=red \mid  box=2) &= \frac{2}{7} \\
 p(color=white \mid  box=2) &= \frac{5}{7} \\
\end{align}
$$

We use Bayes' Rule to figure out the probability that the box is 1 given
that the picked ball is red:

$$
\begin{align}
 p(box=1 \mid  color=red ) &= \frac{p(color=red,box=1)}{p(color=red)} \\
  &= \frac{p(color=red\mid box=1)p(box=1)}{p(color=red)} \\
\end{align}
$$

We calculate the numerator:

$$
\begin{align}
p(color=red\mid box=1)p(box=1) &= \frac{1}{2}\times\frac{3}{8}
\end{align}
$$

We find the marginal distribution of the color of the ball being red,
so that we can substitute it in the denominator:

$$
\begin{align}
 p(color=red) &= \sum_b p(color=red,box=b) \\
  &= \sum_b p(color=red\mid box=b)p(box=b) \\
  &= p(color=red\mid box=1)p(box=1) \\
  &+ p(color=red\mid box=2)p(box=2) \\
  &= \frac{3}{8}\times\frac{1}{2} + \frac{2}{7}\times\frac{1}{2} \\
\end{align}
$$

Finally, we substitute:

$$
\begin{align}
  p(box=1 \mid  color=red ) &= \frac{\frac{3}{8}}{\frac{3}{8} + \frac{2}{7}} \\
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
  p(ball=white\mid coin=heads) &= 1 \\
  p(ball=red\mid coin=tails) &= 1 \\

  p(ball=white\mid coin=tails) &= 0 \\
  p(ball=red\mid coin=heads) &= 0

\end{align}
$$

We marginalize over the coin values to get the overall probability that
a ball is white:

$$
\begin{align}
  p(ball=white) &= \sum_c p(ball=white, coin=c) \\
    &= \sum_c p(ball=white\mid  coin=c)p(coin=c) \\
    &= p(ball=white\mid  coin=heads)p(coin=heads)  \\
    &+ p(ball=white\mid  coin=tails)p(coin=tails) \\
    &= 1(\frac{1}{2}) + 0(\frac{1}{2}) \\
    &= \frac{1}{2}
\end{align}
$$

We do the same thing to get the overall probability that a ball is red:

$$
\begin{align}
  p(ball=red) &= \sum_c p(ball=red, coin=c) \\
    &= \sum_c p(ball=red\mid  coin=c)p(coin=c) \\
    &= p(ball=red\mid  coin=heads)p(coin=heads)  \\
    &+ p(ball=red\mid  coin=tails)p(coin=tails) \\
    &= 0(\frac{1}{2}) + 1(\frac{1}{2}) \\
    &= \frac{1}{2}
\end{align}
$$

We calculate the probability that a ball picked is red, taking into
consideration the balls' colors:

$$
\begin{align}
p(pick=red\mid ball_1=red, ball_2=red) &= 1 \\
p(pick=red\mid ball_1=white, ball_2=red) &= \frac{1}{2} \\
p(pick=red\mid ball_1=red, ball_2=white) &= \frac{1}{2} \\
p(pick=red\mid ball_1=white, ball_2=white) &= 0 \\
\end{align}
$$

We use Bayes' Rule to figure out the posterior probability that both balls
are actually red, given that the three picks have been all red:

$$
  p(B_1=r, B_2=r \mid  P_1=r, P_2=r, P_3=r) \\
  = \frac{p(P_1=r,P_2=r,P_3=r\mid  B_1=r, B_2=r)p(B_1=r,B_2=r)}{p(P_1=r,P_2=r,P_3=r)} \\
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
p(P_1=r,P_2=r,P_3=r\mid  B_1=r, B_2=r) \\
= p(P_1=r\mid  B_1=r, B_2=r) \\
\times p(P_2=r\mid  B_1=r, B_2=r) \\
\times p(P_3=r\mid  B_1=r, B_2=r) \\
= 1 \times 1 \times 1
$$

In the denominator, we marginalize out the ball values over the joint distribution:

$$
p(P_1=r,P_2=r,P_3=r) \\
= \sum_{b_2, b_1} p(P_1=r, P_2=r, P_3=r, B_1=b_1, B_2=b_2) \\
= \sum_{b_2, b_1} p(P_1=r, P_2=r, P_3=r\mid B_1=b_1, B_2=b_2) \\
\times p(B_1=b_1, B_2=b_2) \\
= p(B_1=b_1, B_2=b_2) \\
\times \sum_{b_2, b_1} p(P_1=r, P_2=r, P_3=r\mid B_1=b_1, B_2=b_2) \\
$$

We substitute \\(p(B_1=b_1, B_2=b_2)\\) into the equation right above:

$$
= \frac{1}{4} \sum_{b_2,b_1} p(P_1=r, P_2=r, P_3=r\mid B_1=b_1, B_2=b_2) \\
$$

We make the summation explicit:

$$
= \frac{1}{4} (p(P_1=r, P_2=r, P_3=r\mid B_1=r, B_2=r) \\
+ p(P_1=r, P_2=r, P_3=r\mid B_1=r, B_2=w) \\
+ p(P_1=r, P_2=r, P_3=r\mid B_1=w, B_2=r) \\
+ p(P_1=r, P_2=r, P_3=r\mid B_1=w, B_2=w)) \\
$$

Again, the event of picking a ball is independent of picking another ball
because of replacement. We already calculated the case when someone picks
three balls with replacement and both balls are actually red, so we'll just
calculate the rest of the combinations:

$$
p(P_1=r, P_2=r, P_3=r\mid B_1=r, B_2=w) \\
= p(P_1=r\mid B_1=r, B_2=w) \\
\times p(P_2=r\mid B_1=r, B_2=w) \\
\times p(P_2=r\mid B_1=r, B_2=w) \\
= \frac{1}{2} \times \frac{1}{2} \times \frac{1}{2} \\
= \frac{1}{8}
$$

$$
p(P_1=r, P_2=r, P_3=r\mid B_1=w, B_2=r) \\
= p(P_1=r\mid B_1=w, B_2=r) \\
\times p(P_2=r\mid B_1=w, B_2=r) \\
\times p(P_2=r\mid B_1=w, B_2=r) \\
= \frac{1}{2} \times \frac{1}{2} \times \frac{1}{2} \\
= \frac{1}{8}
$$

$$
p(P_1=r, P_2=r, P_3=r\mid B_1=w, B_2=w) \\
= p(P_1=r\mid B_1=w, B_2=w) \\
\times p(P_2=r\mid B_1=w, B_2=w) \\
\times p(P_2=r\mid B_1=w, B_2=w) \\
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
  p(B_1=r, B_2=r \mid  P_1=r, P_2=r, P_3=r) &= \frac{\frac{1}{4}}{\frac{1}{4}(\frac{5}{4})} \\
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
p(label=true\mid terrorist=true) = 0.95
$$

We can infer from the former that only 5% of terrorists got mislabeled as
good people (false negative):

$$
p(label=false\mid terrorist=true) = 0.05
$$

"95% of all upstanding citizens are identified as such":

$$
p(label=false\mid terrorist=false) = 0.95
$$

We can infer, based on the previous equation, that 5% of good citizens get
misclassified as terrorists (false positive):

$$
p(label=true\mid terrorist=false) = 0.05
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
p(terrorist=true\mid label=true) \\
= \frac{p(label=true\mid terrorist=true)p(terrorist=true)}{p(label=true)} \\
$$

To find out the denominator, we can marginalize over the joint distribution
of \\(p(label=true)\\) and \\(p(terrorist)\\):

$$
    p(label=true) \\
    = \sum_{t} p(label=true, terrorist=t) \\
    = \sum_{t} p(label=true\mid  terrorist=t)p(terrorist=t) \\
$$

We make the summation explicit:

$$
    p(label=true) \\
    = p(label=true\mid  terrorist=true)p(terrorist=true) \\
    + p(label=true\mid  terrorist=false)p(terrorist=false) \\
    = 0.95(0.01) + 0.05(0.99) \\
    = 0.059
$$

Substituting all the values into Bayes' Rule, we find out that even though
the detector is "reliable," we still get a low posterior probability that the
person suspected of being a terrorist is actually a terrorist:

$$
p(terrorist=true\mid label=true) \\
= \frac{p(label=true\mid terrorist=true)p(terrorist=true)}{p(label=true)} \\
= \frac{0.95(0.01)}{.059} \\
= 0.1610169492 \\
$$

### Exercise 1.7

Repeat the Inspector Clouseau scenario, example(\\(1.3\\)), but with the restriction
that either the maid or the butler is the murderer, but not both. Explicitly,
the probability of the maid being the murderer and not the butler is \\(0.04\\), the
probability of the butler being the murderer and not the maid is \\(0.64\\). Modify
*demoClouseau.m* to implement this.)

{% highlight matlab %}
pot(knife).variables=[knife,butler,maid];

pot(knife).table(used, notmurderer, notmurderer)=0.3;
pot(knife).table(used, notmurderer, murderer)   =0.04;
pot(knife).table(used, murderer,    notmurderer)=0.64;
pot(knife).table(used, murderer,    murderer)   =0.0;
{% endhighlight %}

Results:

    p(butler\mid knife=used):
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
    p(x\mid z) = \sum_y p(x\mid y, z)p(y\mid z) = \sum_{y,w} p(x\mid w, y, z)p(w\mid y, z)p(y\mid z)
$$

$$

\begin{align}
    \sum_y p(x\mid y, z)p(y\mid z)  &= \sum_y \frac{p(x,y, z)}{p(y,z)}\frac{p(y,z)}{p(z)} \\
    &= \sum_y \frac{p(x,y,z)}{p(z)} \\
    &= \frac{p(x,z)}{p(z)} \\
    &= p(x\mid z) \\
    \sum_{y,w} p(x\mid w,y,z)p(w\mid y,z)p(y\mid z) &= \sum_{y,w}\frac{p(x,w,y,z)}{p(w,y,z)}\frac{p(w,y,z)}{p(y,z)}\frac{p(y,z)}{p(z)} \\
    &= \sum_{y,w}\frac{p(x,w,y,z)}{p(z)} \\
    &= \frac{p(x,z)}{p(z)} \\
    &= p(x\mid z) \\
\end{align}
$$

### Exercise 1.10

As a young man Mr Gott visits Berlin in \\(1969\\). He’s surprised that he cannot
cross into East Berlin since there is a wall separating the two halves of the
city. He’s told that the wall was erected \\(8\\) years previously. He reasons that :
The wall will have a finite lifespan; his ignorance means that he arrives
uniformly at random at some time in the lifespan of the wall. Since only \\(5\\%\\) of
the time one would arrive in the first or last \\(2.5\\%\\) of the lifespan of the wall
he asserts that with \\(95\\%\\) confidence the wall will survive between \\(8/0.975 \approx 8.2\\)
and \\(8/0.025 = 320\\) years. In \\(1989\\) the now Professor Gott is pleased to find that
his prediction was correct and promotes his prediction method in prestigious
journals. This ‘delta-t’ method is widely adopted and used to form predictions
in a range of scenarios about which researchers are ‘totally ignorant’. Would
you ‘buy’ a prediction from Prof. Gott? Explain carefully your reasoning.

I would think that it would be hard to be totally ignorant about something
if we are really trying hard to create a good model that predicts the lifespan
of something. In this specific case of the Berlin Wall, I believe that knowing
about tensions between East Germany and West Germany would seriously change
someone's prior belief that it will fall in a certain period of time. Therefore,
I would not 'buy' a prediction from Prof. Gott.

### Exercise 1.11

Implement the soft XOR gate, example(\\(1.7\\)) using BRMLtoolbox. You may find
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
\\(dom(hamburgers) = dom(KJ) = \\{tr, fa\\}.\\)

TODO


### Exercise 1.13

Implement the two-dice example, section(\\(1.3.1\\)) using BRMLtoolbox.

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

### Exercise 1.14

A redistribution lottery involves picking the correct four numbers from \\(1\\)
to \\(9\\) (without replacement, so \\(3,4,4,1\\) for example is not possible).
The order of the picked numbers is irrelevant. Every week a million people play
this game, each paying \\(\unicode{163} 1\\) enter, with the numbers
\\(3,5,7,9\\) being the most popular (\\(1\\) in every \\(100\\) people chooses
these numbers). Given that the million pounds prize money is split equally
between winners, and that any four (different) numbers come up at random, what
is the expected amount of money each of the players choosing \\(3,5,7,9\\) will
win each week? The least popular set of numbers is \\(1,2,3,4\\) with only
\\(1\\) in \\(10,000\\) people choosing this. How much do they profit each
week, on average? Do you think there is any ‘skill’ involved in playing this
lottery?

One out of a hundred people pick the set \\(\\{3, 5, 7, 9\\}\\):

$$
p(pick\{3,5,7,9\}) = \frac{1}{100}
$$

One out of a ten-thousand people pick the set \\(\\{1, 2, 3, 4\\}\\):

$$
p(pick\{1,2,3,4\}) = \frac{1}{10,000}
$$

There are \\(9\\) options in the first pick, \\(8\\) in the second, \\(7\\)
in the third, and \\(6\\) in the fourth, giving us \\(3,024\\) ordered ways.

$$
9 \times 8 \times 7 \times 6 = 3,024
$$


One can arrange the numbers of any set of four numbers in \\(24\\) ways:

$$
\begin{align}
  4! &= 4 \times 3 \times 2 \times 1 \\
  &= 24
\end{align}
$$

For the visual learners out there, there are the all the \\(24\\) possible ways
of ordering a set with four numbers. Let's use \\(\\{3,5,7,9\\}\\) for example:

$$
  5\ 3\ 7\ 9\\
  5\ 3\ 9\ 7\\
  5\ 7\ 3\ 9\\
  5\ 7\ 9\ 3\\
  5\ 9\ 7\ 3\\
  5\ 9\ 3\ 7\\
$$

$$
  9\ 5\ 7\ 3\\
  9\ 5\ 3\ 7\\
  9\ 7\ 5\ 3\\
  9\ 7\ 3\ 5\\
  9\ 3\ 7\ 5\\
  9\ 3\ 5\ 7\\
$$

$$
  3\ 5\ 7\ 9\\
  3\ 5\ 9\ 7\\
  3\ 9\ 7\ 5\\
  3\ 9\ 5\ 7\\
  3\ 7\ 9\ 5\\
  3\ 7\ 5\ 9\\
$$

$$
  7\ 3\ 5\ 9\\
  7\ 3\ 9\ 5\\
  7\ 5\ 3\ 9\\
  7\ 5\ 9\ 3\\
  7\ 9\ 3\ 5\\
  7\ 9\ 5\ 3\\
$$

Therefore, the probability of winning, without order mattering, is
\\(\frac{1}{126}\\):

$$
\begin{align}
  p(win=true) &= \frac{24}{3,024} \\
              &= \frac{1}{126} \\
\end{align}
$$

Amount of money to be distributed:

$$
\unicode{163} 1,000,000
$$

Number of people choosing the set \\(\\{3,5,7,9\\}\\):

$$
\begin{align}
    num\ people_\{3,5,7,9\} &= total\ num\ people \times p(pick\{3,5,7,9\}) \\
  &= 1,000,000\times\frac{1}{100} \\
  &= 10,000
  \end{align}
$$

Amount that someone wins, given that that person picked the
set\\(\\{3,5,7,9\\}\\) and that those sets of numbers are the winning
set:

$$
\begin{align}
    prize_{winner=\{3,5,7,9\}} &= \frac{total\ cash\ prize}{num\ people_{\{3,5,7,9\}} } \\
&= \frac{\unicode{163} 1,000,000}{10,000} \\
&= \unicode{163} 100
\end{align}
$$

Average amount that a person picking \\(\\{3,5,7,9\\}\\) wins, considering the
likelihood of winning:

$$
\begin{align}
  avg\ prize_{winner=\{3,5,7,9\}} &= prize_{winner=\{3,5,7,9\}} \times p(win=true) \\
  &= \unicode{163} 100 \times \frac{1}{126} \\
  &= \unicode{163} 0.79
\end{align}
$$

Amount that someone wins, given that that person picked the
set\\(\\{1,2,3,4\\}\\) and that those sets of numbers are the winning
set:

$$
\begin{align}
  prize_{winner=\{1,2,3,4\}} &= \frac{total\ cash\ prize}{sum\ people_{\{1,2,3,4\}} } \\
&= \frac{\unicode{163} 1,000,000}{100} \\
&= \unicode{163} 10,000
\end{align}
$$

Average amount that a person picking \\(\\{1,2,3,4\\}\\) wins, considering the
likelihood of winning:

$$
\begin{align}
  avg\ prize_{winner=\{1,2,3,4\}} &= prize_{winner=\{1,2,3,4\}} \times p(win=true) \\
  &= \unicode{163} 10,000 \times \frac{1}{126} \\
  &= \unicode{163} 79.37
\end{align}
$$

Since the numbers are picked randomly and there is nothing that suggests that
one set of four (unique) numbers is more likely to be picked than another, the
only difference really is the number of people betting on a set of numbers.
Someone cannot increase their chances of winning. However, by somehow figuring
out which sets of numbers are the least popular and choosing the least popular
one, this person can increase the possible amount of money won in the case that
that person does win.

### Exercise 1.15

In a test of ‘psychometry’ the car keys and wrist watches of \\(5\\) people are given
to a medium. The medium then attempts to match the wrist watch with the car key
of each person. What is the expected number of correct matches that the medium
will make (by chance)? What is the probability that the medium will obtain at
least \\(1\\) correct match?

There are \\(120 \\) ways to match the car keys with the wrist watches:

$$
\begin{align}
  5! &= 5 \times 4 \times 3 \times 2 \times 1 \\
     &= 120
\end{align}
$$

I automated the process of finding out the absolute frequency of each
number of matches occuring (\\(0\\) matches, \\(1\\) matches, etc.):

{% highlight ruby linenos %}
require 'spec_helper'

describe Psychometry do
  describe 'when there are five pairs to be matched' do
    describe '#absolute_frequencies_of_matches' do
      it 'should return an array of absolute frequencies' do
        # 0 matches occurs 44 times, 1 match occurs 45 times, etc.
        psychometry = Psychometry.new

        abs_freq = [44, 45, 20, 10, 0, 1]
        expect(psychometry.absolute_frequencies_of_matches).
          to eq abs_freq
      end
    end

    describe '#permutations' do
      before {@psychometry = Psychometry.new}

      it 'should include ABCDE, EBACD' do
        expect( @psychometry.permutations).
          to include(['A', 'B', 'C', 'D', 'E'])
        expect( @psychometry.permutations).
          to include(['E', 'B', 'A', 'C', 'D'])
      end

      it 'should not include AAAAA' do
        expect( @psychometry.permutations).
          not_to include(['A', 'A', 'A', 'A', 'A'])
      end
    end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}

class Psychometry
  def initialize
    @num_pairs = 5
  end

  def absolute_frequencies_of_matches
    permutations.inject(init_hash) do |accum, permutation|
      accum[num_matches_in_one(permutation)] =
        accum[num_matches_in_one(permutation)] + 1
      accum
    end
  end

  def permutations
    combinations.inject([]) do |accum, combination|
      permutation?(combination) ? (accum << combination) : accum
    end
  end

  private

  def num_matches
    permutations.inject(0) do |accum, permutation|
      accum += num_matches_in_one(permutation)
    end
  end

  def num_matches_in_one(permutation)
    (0..@num_pairs-1).inject(0) do |accum_2, index|
      if permutation[index] == characters[index]
        accum_2 += 1
      else
        accum_2
      end
    end
  end

  def init_hash
    (0..@num_pairs).inject([]) { |accum, val| accum << 0 }
  end

  def combinations
    characters.inject([]) do |accum_1, char_1|
      accum_1 | characters.inject([]) do |accum_2, char_2|
        accum_2 | characters.inject([]) do |accum_3, char_3|
          accum_3 | characters.inject([]) do |accum_4, char_4|
            accum_4 | characters.map do |char_5|
              [char_1, char_2, char_3, char_4, char_5]
            end
          end
        end
      end
    end
  end

  def permutation?(combination)
    combination.uniq.length == combination.length
  end

  def characters
    ('A'..'Z').to_a[0..@num_pairs-1]
  end
end


{% endhighlight %}

I found out through my program that the most likely number of matches
to occur is one; there are \\(45\\) ways to get one match.

I also found out through my program that having no matches occurs \\(44\\)
times:

$$
p(W=0) = \frac{44}{120}
$$

We know that the probabilities of all states (nothing matching, one
matching, ..., all matching) must sum up to \\(1\\):

$$
p(W=0) + \\ p(W=1\ only) + \\ p(W=2\ only) + \\ p(W=3\ only) + \\ p(W=4\ only) + \\
p(W=5) = 1
$$

In short:

$$
p(W=0) + p(W\neq0) = 1
$$

Therefore, the probability of getting at least one match is:

$$
\begin{align}
p(W\neq 0) &= 1 - p(W=0) \\
&= 1 - \frac{44}{120} \\
&= \frac{76}{120} \\
&\approx 63.3%
\end{align}
$$

Just to increase my confidence in the correctness of my program, I want
to see that the answers it gives regarding the number of times 5 matches, 4
matches, and 3 matches occurs make sense.

Let's say we have the keys set up as follows:

$$
ABCDE
$$

Since there is only one way to get all \\(5\\) correctly:

$$
ABCDE
$$

$$
p(W=5) = \frac{1}{120}
$$

We also know that getting \\(4\\) correctly actually is the same event as
getting \\(5\\) correctly, since if we have \\(4\\) correctly matched, then the
last one must match. If one does not match, then we know another set of
watch-to-key will be a mismatch. In other words, \\(4\\) matching pairs cannot
exist without the last one also matching. Therefore:

$$
p(W=4\ only) = 0
$$

There are exactly \\(10\\) ways to getting only 3 correct.

$$
\begin{align}
ABCED\\
ABDCE\\
ABEDC\\
ACBDE\\
ADCBE\\
AECDB\\
\end{align}
$$

$$
BACDE
$$

$$
CBADE
$$

$$
DBCAE
$$

$$
EBCDA
$$

Therefore:

$$
\begin{align}
p(W=3\ only) &= \frac{10}{120}\\
\end{align}
$$

These numbers are in line with the output of the program. Therefore,
I am more confident that the program is correct.

### Exercise 1.16.1

Show that for any function \\(f\\)

$$
\sum_xp(x\mid y)f(y) = f(y)
$$

$$
\begin{align}
\sum_xp(x\mid y)f(y) &= \sum_x\frac{p(x,y)}{p(y)}f(y) \\
                 &= \sum_x\frac{p(x)p(y)}{p(y)}f(y) \\
                 &= \sum_xp(x)f(y) \\
                 &= f(y)\sum_xp(x) \\
                 &= f(y)\times 1 \\
                 &= f(y)
\end{align}
$$

### Exercise 1.16.2

Explain why, in general,

$$
\sum_xp(x\mid y)f(x,y) \neq \sum_xf(x,y)
$$

$$
\begin{align}
\sum_xp(x\mid y)f(x,y) &= \sum_x\frac{p(x,y)}{p(y)}f(x,y) \\
                   &= \sum_x\frac{p(x)p(y)}{p(y)}f(x,y) \\
                   &= \sum_xp(x)f(x,y) \\
                   &= f(x,y)\sum_xp(x) \\
                   &= f(x,y) \\
                   &\neq \sum_xf(x,y) \\
\end{align}
$$

### Exercise 1.17

#### Part I

(Inspired by singingbanana.com). Seven friends decide to order
pizzas by telephone from Pizza4U based on a flyer pushed through their
letterbox. Pizza4U has only \\(4\\) kinds of pizza, and each person chooses a
pizza independently. Bob phones Pizza4U and places the combined pizza order,
simply stating how many pizzas of each kind are required. Unfortunately, the
precise order is lost, so the chef makes seven randomly chosen pizzas and then
passes them to the delivery boy.

How many different combined orders are possible?

I got all the combinations and filtered out the duplicates.  There seems to be
\\(120\\) different combined orders:

{% highlight ruby linenos %}
require 'spec_helper'

describe Pizza4U do
  describe '#unique_combinations' do
    it 'should not return any duplicates' do
      pizza_4_u = Pizza4U.new
      uniq_combs = pizza_4_u.unique_combinations

      orig = ['A', 'A', 'A', 'A', 'A', 'A', 'B']
      rearranged_1 = ['A', 'A', 'A', 'A', 'A', 'B', 'A']
      rearranged_2 = ['A', 'B', 'A', 'A', 'A', 'A', 'A']

      orig_1 = ['A', 'A', 'A', 'A', 'A', 'B', 'B']
      rearranged_3 = ['A', 'B', 'A', 'B', 'A', 'A', 'A']
      rearranged_4 = ['B', 'B', 'A', 'A', 'A', 'A', 'A']

      orig_2 = [ 'B', 'B', 'D', 'D', 'D', 'D', 'D']

      # should not be included because there are only four
      # pizzas to choose from, not 5.
      orig_3 = [ 'E','E','E','E','E','E','E' ]


      expect(uniq_combs).to include(orig)
      expect(uniq_combs).to include(orig_1)
      expect(uniq_combs).to include(orig_2)
      expect(uniq_combs).not_to include(orig_3)
      expect(uniq_combs).not_to include(rearranged_1)
      expect(uniq_combs).not_to include(rearranged_2)
      expect(uniq_combs).not_to include(rearranged_3)
      expect(uniq_combs).not_to include(rearranged_4)
      expect(uniq_combs.count).to eq 120
    end
  end

  describe '#accuracy(num_times)' do
    it 'picks a random combination of pizzas (ordered by people) and compares it with another randomly-picked combination of pizzas (picked by the chef) and gives us a score' do
      pizza_4_u = Pizza4U.new
      accuracy = pizza_4_u.accuracy(1000000)

      expect(accuracy).to eq 1/120.0
    end
  end

  describe '#unique_absolute_freqs' do
    it 'should return a dictionary with unique combinations as keys and absolute freqs as values' do

      pizza_4_u = Pizza4U.new
      unique_absolute_freqs = pizza_4_u.unique_absolute_freqs

      total_count =  unique_absolute_freqs.inject(0){|accum,(k,v)| accum = accum + v; accum}
      expect(total_count).to eq 16384
      expect(unique_absolute_freqs['AAAAAAA']).to be 1
      expect(unique_absolute_freqs['AAAAAAB']).to be 7
    end
  end

  describe '#prob_correct' do
    it 'gives us the chance that the chef was correct' do
      pizza_4_u = Pizza4U.new
      expect(pizza_4_u.prob_correct.round(3)).to eq 0.018383.round(3)
    end
  end
end
{% endhighlight %}

{% highlight ruby linenos %}

require 'utils'

class Pizza4U
  attr_reader :combinations, :unique_combinations, :combinations_size, :unique_absolute_freqs

  def initialize
    @utils = Utils.new(4)
    @combinations = @utils.combinations(7)
    @unique_combinations = combinations.map {|combination| combination.sort}.uniq

    @combinations_size = combinations.count
    @unique_absolute_freqs = unique_combinations.inject({}) do |accum, uniq_combo|
      accum[uniq_combo.join] = combinations.select{|combination| same_unique_combo(combination, uniq_combo)}.count
      accum
    end
  end

  def accuracy(num_times)
    score(num_times) / num_times.to_f
  end

  def prob_correct
    corrects_of_joint_distribution.inject(0) do |accum, hash|
      accum = accum + hash[:posterior_prob]
      accum
    end
  end

  private

  def corrects_of_joint_distribution
    joint_distribution.select{|item| item[:correct] == true}
  end

  def joint_distribution
    unique_absolute_freqs.inject([]) do |accum_1, (chef_k,chef_v)|
      accum_1 + unique_absolute_freqs.inject([]) do |accum_2, (customers_k,customers_v)|
        posterior_prob = chef_v / combinations_size.to_f * customers_v / combinations_size.to_f
        hash = { correct: false, posterior_prob: posterior_prob}

        if chef_k == customers_k
          hash[:correct] = true
        end

        accum_2 << hash
      end
    end
  end

  def score(num_times)
    r = Random.new

    (0..num_times-1).inject(0) do |accum, count|
      customers_pick = pick(r)
      chefs_pick = pick(r)

      if same_unique_combo(customers_pick, chefs_pick)
        accum = accum + 1
      else
        accum
      end
    end
  end

  def same_unique_combo(pick1, pick2)
    pick1.sort == pick2.sort
  end

  def pick(r)
    pick_index = r.rand * combinations.length - 1
    combinations[pick_index]
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
class Utils
  def initialize(num_pairs)
    @num_pairs = num_pairs
  end

  def combinations(num_iteration)
    combine(characters, num_iteration)
  end

  def combine(accum, num_iteration)
    return accum if num_iteration <= 1

    new_accum = characters.inject([]) do |accum_1, char|
      accum_1 | accum.map do |item|
        [char, item].flatten
      end
    end

    combine(new_accum, num_iteration - 1)
  end

  def characters
    ('A'..'Z').to_a[0..@num_pairs-1]
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
require 'spec_helper'

describe Utils do
  describe '#combinations' do
    it 'should return the right amount of items' do
      num_items_to_choose_from = 4
      num_times_to_combine = 7
      utils = Utils.new(num_items_to_choose_from)
      combinations = utils.combinations(num_times_to_combine)
      expect(combinations.count).to eq 16384
      expect(combinations).to include(['A', 'A', 'A', 'A', 'A', 'A', 'A'])
    end
  end
end

{% endhighlight %}


#### Part II

What is the probability that the delivery boy has the right order?

Let \\(p(p_{x_y}=z)\\) where \\(dom(x)=\\{chef, customer\\}\\),
\\(dom(y)=\\{1,2,3,4\\}\\), and \\(dom(z)=\\{1,2,...,6,7\\}\\).
\\(y\\) corresponds to the pizza options available to each customer,
and \\(z\\) corresponds to the seven customers.

The overall correctness of the delivery person, regardless of what the chef
or customers have picked can be represented as follows:

$$
\begin{align}

p(correct) &= \sum_{a,b,c,d,e,f,g,h}
p(correct,
p_{cu_1}=a,
 p_{cu_2}=b,
 p_{cu_3}=c,
 p_{cu_4}=d,
 p_{ch_1}=e,
 p_{ch_2}=f,
 p_{ch_3}=g,
 p_{ch_4}=h) \\
&= \sum_{a,b,c,d,e,f,g,h}
p(correct \mid
p_{cu_1}=a,
 p_{cu_2}=b,
 p_{cu_3}=c,
 p_{cu_4}=d,
 p_{ch_1}=e,
 p_{ch_2}=f,
 p_{ch_3}=g,
 p_{ch_4}=h)
p(
p_{cu_1}=a,
 p_{cu_2}=b,
 p_{cu_3}=c,
 p_{cu_4}=d,
 p_{ch_1}=e,
 p_{ch_2}=f,
 p_{ch_3}=g,
 p_{ch_4}=h) \\
&= \sum_{a,b,c,d,e,f,g,h}
p(correct \mid
p_{cu_1}=a,
 p_{cu_2}=b,
 p_{cu_3}=c,
 p_{cu_4}=d,
 p_{ch_1}=e,
 p_{ch_2}=f,
 p_{ch_3}=g,
 p_{ch_4}=h)
p(
p_{cu_1}=a,
 p_{cu_2}=b,
 p_{cu_3}=c,
 p_{cu_4}=d
)
p(
 p_{ch_1}=e,
 p_{ch_2}=f,
 p_{ch_3}=g,
 p_{ch_4}=h) \\
\end{align}
$$

Calculating the probability that the delivery person has the correct order,
regardless of what the customers and the chef actually chose, gives us
\\(1.84\%\\).

### Exercise 1.18

Sally is new to the area and listens to some friends discussing about another
female friend. Sally knows that they are talking about either Alice or Bella
but doesn’t know which. From previous conversations Sally knows some
independent pieces of information: She’s \\(90\%\\) sure that Alice has a white
car, but doesn’t know if Bella’s car is white or black. Similarly, she’s
\\(90\%\\) sure that Bella likes sushi, but doesn’t know if Alice likes sushi.
Sally hears from the conversation that the person being discussed hates sushi
and drives a white car. What is the probability that the friends are talking
about Alice?  Assume maximal uncertainty in the absence of any knowledge of the
probabilities.

"Sally knows that they are talking about either Alice or Bella but doesn’t
know which.":

$$
\begin{align}
p(person = Alice) &= 50 \% \\
p(person = Bella) &= 50 \% \\
\end{align}
$$

"She’s \\(90\%\\) sure that Alice has a white car." In other words, if the
person is Alice, then the probability of the car being white is \\(90\%\\),
etc:

$$
p(car = white \mid person = Alice) = 90\%
$$

From this we can infer that Sally thinks that if the person is Alice, then
there's only a \\(10\%\\) chance that the car is not white:

$$
p(car \neq white \mid person = Alice ) = 10\%
$$


"...but doesn’t know if Bella’s car is white or black.":

$$
p(car = white \mid person = Bella) = 50\%
$$

$$
p(car \neq white \mid person = Bella) = 50\%
$$

"Similarly, she’s \\(90\%\\) sure that Bella likes sushi":

$$
p( sushi = true \mid person = Bella) = 90\%
$$

From this we can infer that Sally thinks that if the person is Bella then
there's only a \\(10\%\\) chance that the person hates sushi:

$$
p( sushi = false\mid person = Bella) = 10\%
$$

"... but doesn’t know if Alice likes sushi.":

$$
p( sushi = true\mid person = Alice) = 50\%
$$

$$
p( sushi = false\mid person = Alice) = 50\%
$$

"Sally hears from the conversation that the person being discussed hates sushi
and drives a white car.":

$$
\begin{align}
p(sushi = false) &= 1.0 \\
p(sushi = true) &= 0.0 \\
\end{align}
$$

$$
\begin{align}
p(car = white) &= 1.0 \\
p(car \neq white) &= 0.0 \\
\end{align}
$$

"What is the probability that the friends are talking about Alice?":

$$
\begin{align}
p(person = Alice \mid car = white, sushi=false)
&= \frac{p(car = white, sushi = false \mid person = Alice)p(person =
Alice)}{p(car = white, sushi = false)} \\
    &= \frac{p(car = white, sushi = false \mid person = Alice)p(person =
    Alice)}{\sum_{p}p(person = p, car = white, sushi = false)} \\
\end{align}
$$

$$
\begin{align}
p(car = white, sushi = false \mid person = Alice) &= p(car = white \mid person = Alice)p(sushi = false \mid person = Alice) \\
                                                  &= 0.90 \times 0.50 \\
                                                  &= 0.45
\end{align}
$$

$$
    \sum_{p}p(person = p, car = white, sushi = false) \\
    = p(car = white, sushi = false \mid person = Alice)p(Alice) \\
     + p(car = white, sushi = false \mid person = Bella)p(Bella) \\
    = p(car = white\mid person = Alice)p(sushi = false \mid person = Alice)p(Alice) \\
     + p(car = white\mid person = Bella)p(sushi = false \mid person = Bella)p(Bella) \\
    = 0.90 \times 0.50 \times 0.50 + 0.50 \times 0.10 \times 0.50 \\
    = 0.225 + 0.025 \\
    = 0.25 \\
$$

Therefore, Sally should be quite certain that the person her friends are
talking about is Alice (\\(90\%\\)):

$$
\begin{align}
p(person = Alice \mid car = white, sushi=false)
&= \frac{0.45\times0.5}{0.25} \\
&= 0.90 \\
\end{align}
$$

### Exercise 1.19

The weather in London can be summarised as: if it rains one day there’s a \\(70\%\\)
chance it will rain the following day; if it’s sunny one day there’s a \\(40\%\\)
chance it will be sunny the following day.

$$
p(today=rainy \mid yesterday=rainy) = 70\%
$$

$$
p(today=sunny \mid yesterday=sunny) = 40\%
$$

From these likelihoods, I infer the following:

$$
p(today=sunny \mid yesterday=rainy) = 30\%
$$

$$
p(today=rainy \mid yesterday=sunny) = 60\%
$$

#### Part I

Assuming that the prior probability it rained yesterday is \\(0.5\\), what is the
probability that it was raining yesterday given that it’s sunny today?

$$
p(yesterday=rainy) = 50\%
$$

I infer from this that the probability of being sunny yesterday is also \\(50\%\\):

$$
p(yesterday=sunny) = 50\%
$$

$$
\begin{align}
p(yesterday=rainy \mid today=sunny) &= \frac{p(today=sunny \mid yesterday=sunny)p(yesterday=rainy)}{p(today=sunny)} \\
\end{align}
$$

$$
\begin{align}
    p(today=sunny) &= \sum_{y}p(today=sunny,yesterday=y) \\
                   &= \sum_{y}p(today=sunny \mid yesterday=y)p(yesterday=y) \\
                   &= p(today=sunny \mid yesterday=sunny)p(yesterday=sunny) + p(today=sunny \mid yesterday=rainy)p(yesterday=rainy) \\
                   &= 0.40 \times 0.5 + 0.30 \times 0.50 \\
                   &= 0.20 + 0.15 \\
                   &= 0.35 \\
\end{align}
$$

Thus, the probability of raining yesterday given that today is sunny:

$$
\begin{align}
p(yesterday=rainy \mid today=sunny) &= \frac{0.20}{0.35} \\
                                   &= 57.14 \%
\end{align}
$$

#### Part 2

If the weather follows the same pattern as above, day after day, what is the
probability that it will rain on any day (based on an effectively infinite
number of days of observing the weather)?

On any day, not considering whether it rained or not the day before, the
probability of raining is:

$$
\begin{align}
p(today=rainy) &= \sum_y p(today=rainy, yesterday=y) \\
               &= \sum_y p(today=rainy \mid yesterday=y)p(yesterday=y) \\
               &= p(today=rainy \mid yesterday=rainy)p(yesterday=rainy) + p(today=rainy \mid yesterday=sunny)p(yesterday=sunny) \\
               &= 0.7 \times 0.5 + 0.6 \times 0.5 \\
               &= 0.65 \\
\end{align}
$$

#### Part 3

Use the result from part \\(2\\) above as a new prior probability of rain
yesterday and recompute the probability that it was raining yesterday given
that it’s sunny today.)

$$
\begin{align}
p(yesterday=rainy) &= 0.65 \\
\end{align}
$$

Therefore:

$$
\begin{align}
p(yesterday=sunny) &= 0.35 \\
\end{align}
$$

$$
\begin{align}
p(yesterday=rainy \mid today=sunny) &= \frac{p(today=sunny \mid yesterday=rainy)p(yesterday=rainy)}{p(today=sunny)} \\
\end{align}
$$

$$
\begin{align}
p(today=sunny) &= \sum_y p(today=sunny, yesterday=y) \\
               &= \sum_y p(today=sunny \mid yesterday=y)p(yesterday=y) \\
               &= p(today=sunny \mid yesterday=sunny)p(yesterday=sunny) + p(today=sunny \mid yesterday=rainy)p(yesterday=rainy) \\
               &= 0.40 \times 0.35 + 0.30 \times 0.65 \\
               &= 0.14 + 0.195 \\
               &= 0.335 \\
\end{align}
$$

$$
\begin{align}
p(yesterday=rainy \mid today=sunny) &= \frac{0.30 \times 0.65}{0.335} \\
                                    &= 58.21\% \\
\end{align}
$$

Very interesting. The probability of raining has increased a little bit after
updating the prior probabilities. Since it was likely that it rained yesterday,
it's slightly more likely that it will rain today.

### Exercise 1.20

A game of Battleships is played on a \\(10 \times 10\\) pixel grid. There are
two \\(5\\)-pixel length ships placed uniformly at random on the grid, subject
to the constraints that (i) the ships cannot overlap and (ii) one ship is
vertical and the other horizontal. After 10 unsuccessful ‘misses’ in locations
\\((1,10)\\),\\((2,2)\\),\\((3,8)\\),\\((4,4)\\),\\((5,6)\\),\\((6,5)\\),\\((7,4)\\),\\((7,7)\\),\\((9,2)\\),\\((9,9)\\)
calculate which pixel has the highest probability of containing a ship. State
this pixel and the value of the highest probability.

Here's a diagram:

<figure>
<pre>
   |1 |2 |3 |4 |5 |6 |7 |8 |9 |10
---|--|--|--|--|--|--|--|--|--|--
 1                             M
---|--|--|--|--|--|--|--|--|--|--
 2     M
---|--|--|--|--|--|--|--|--|--|--
 3                       M
---|--|--|--|--|--|--|--|--|--|--
 4           M
---|--|--|--|--|--|--|--|--|--|--
 5                 M
---|--|--|--|--|--|--|--|--|--|--
 6              M
---|--|--|--|--|--|--|--|--|--|--
 7           M        M
---|--|--|--|--|--|--|--|--|--|--
 8
---|--|--|--|--|--|--|--|--|--|--
 9     M                    M
---|--|--|--|--|--|--|--|--|--|--
10
---|--|--|--|--|--|--|--|--|--|--
</pre>
<figcaption>
Misses in the game of Battleship
</figcaption>
</figure>


The way I computed the probability of a given point being a hit is by using the
available ships that I have (\\(1\\) horizontal and \\(1\\) vertical) and sliding
them across the board; if the ship occupies valid points (points on the board
and no point being labeled as "miss"), then we update the absolute frequencies of
those points by one. The points with the highest (absolute and relative) frequencies
are good candidates to be pegged next.

Here are the computed absolute frequencies:

<figure>
<pre>
[[2, 2, 4, 4, 6, 4, 4, 2, 2, 0],
 [2, 0, 3, 2, 4, 4, 6, 3, 4, 2],
 [4, 3, 6, 3, 4, 2, 3, 0, 3, 2],
 [4, 2, 4, 0, 2, 2, 4, 3, 6, 4],
 [6, 3, 6, 1, 2, 0, 2, 2, 4, 4],
 [5, 2, 5, 0, 0, 2, 2, 4, 4, 6],
 [4, 2, 4, 0, 0, 1, 0, 3, 2, 4],
 [4, 3, 6, 4, 5, 6, 4, 6, 3, 4],
 [2, 0, 3, 2, 2, 3, 2, 3, 0, 2],
 [2, 2, 4, 4, 5, 6, 4, 4, 2, 2]]
</pre>
<figcaption>
Absolute frequencies of possible hits
</figcaption>
</figure>

<figure>
<pre>
  <div id="heatmap"></div>
</pre>
<figcaption>
Heatmap of targets (Red is more likely)
</figcaption>
</figure>

The points with the most likely hits are the following \\((1,5)\\),
\\((2,7)\\), \\((3,3)\\), \\((4,9)\\), \\((5,1)\\),
\\((5,3)\\),\\((6,10)\\),\\((8,3)\\),\\((8,6)\\),\\((8,8)\\), \\((10,6)\\).
The probability of the ship being in one of these points is \\(0.02\\).

Here's the code:

{% highlight ruby linenos %}
module Battleship
  class Board
    attr_reader :table

    def initialize(init_hash)
      @misses = init_hash[:misses]
      @ships = init_hash[:ships]
      @table = Battleship::Table.new(row_length:row_length,
                                     col_length: col_length,
                                     misses: @misses,
                                     ships: @ships)
      # table should listen to changes in ship status
      # if hit, then recalculate frequencies...
      @table.recalculate_abs_freq!
    end

    def miss?(point)
      @misses.select {|miss| miss.same_as?(point) }.count >= 1
    end

    def row_length
      10
    end

    def col_length
      10
    end

    def best_targets
      @table.select {|point| point.abs_freq == @table.max_abs_freq}
    end

    def abs_freqs
      @table.rows.map do |row|
        row.map do |point|
          point.abs_freq
        end
      end
    end

    def rel_freqs
      abs_freqs.map do |row|
        row.map do |abs_freq|
          abs_freq / @table.sum_of_abs_freqs.to_f
        end
      end
    end

    def abs_freq_at(point)
      point_at(point).abs_freq
    end

    def point_at(*args)
      @table.point_at(args)
   end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
require 'spec_helper'

describe Battleship::Board do
  before do
    @miss_1 = Battleship::Point.new(1, 10, :missed)
    @miss_2 = Battleship::Point.new(2, 2, :missed)
    @miss_3 = Battleship::Point.new(3, 8, :missed)
    @miss_4 = Battleship::Point.new(4, 4, :missed)
    @miss_5 = Battleship::Point.new(5, 6, :missed)
    @miss_6 = Battleship::Point.new(6, 5, :missed)
    @miss_7 = Battleship::Point.new(7, 4, :missed)
    @miss_8 = Battleship::Point.new(7, 7, :missed)
    @miss_9 = Battleship::Point.new(9, 2, :missed)
    @miss_10 = Battleship::Point.new(9, 9, :missed)

    @misses = [@miss_1, @miss_2, @miss_3, @miss_4, @miss_5,
               @miss_6, @miss_7, @miss_8, @miss_9, @miss_10 ]

    @ship_1 = Battleship::VerticalShip.new(length: 5)
    @ship_2 = Battleship::HorizontalShip.new(length: 5)

    @ships = [@ship_1, @ship_2]

    @board = Battleship::Board.new(misses: @misses, ships: @ships)
  end

  describe '#row_length' do
    it 'should return 10' do
      expect(@board.row_length).to eq 10
    end
  end

  describe '#col_length' do
    it 'should return 10' do
      expect(@board.col_length).to eq 10
    end
  end

  describe '#miss?(point)' do
    it 'should return true if the point was a miss' do
      miss_point = Battleship::Point.new(1, 10 , :missed)
      expect( @board.miss?(miss_point)).to eq true
    end

    it 'should return false if the point was not a miss' do
      miss_point = Battleship::Point.new(1, 9 , :missed)
      expect( @board.miss?(miss_point)).to eq false
    end
  end

  describe '#point_at(row, col)' do
    it 'should return the point with those attributes' do
      row = 1
      col = 1

      point = @board.point_at(row, col)

      expect(point.row).to eq row
      expect(point.col).to eq col
    end
  end

  describe '#abs_freq_at(point)' do
    it'should return the number of possible hits' do
      point_of_interest = Battleship::Point.new(1, 1, :missed)
      expect(@board.abs_freq_at(point_of_interest)).to eq 2
    end
  end

  describe '#best_targets' do
    it 'returns the points with the highest likelihood of overlapping with a ship' do
      def has_point(some_point, occupied_points)
        occupied_points.any? {|point| point.row == some_point.row && point.col == some_point.col}
      end
      expect(has_point(Battleship::Point.new(1,5), @board.best_targets)).to eq true
      expect(has_point(Battleship::Point.new(2,7), @board.best_targets)).to eq true
      expect(has_point(Battleship::Point.new(3,3), @board.best_targets)).to eq true
      expect(has_point(Battleship::Point.new(4,9), @board.best_targets)).to eq true
      expect(has_point(Battleship::Point.new(5,1), @board.best_targets)).to eq true
      expect(has_point(Battleship::Point.new(5,3), @board.best_targets)).to eq true
      expect(has_point(Battleship::Point.new(6,10), @board.best_targets)).to eq true
      expect(has_point(Battleship::Point.new(8,3), @board.best_targets)).to eq true
      expect(has_point(Battleship::Point.new(8,6), @board.best_targets)).to eq true
      expect(has_point(Battleship::Point.new(8,8), @board.best_targets)).to eq true
      expect(has_point(Battleship::Point.new(10,6), @board.best_targets)).to eq true
    end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
module Battleship
  class Table
    include Enumerable

    attr_reader :row_length, :col_length

    def initialize(hash)
      @row_length = hash.fetch(:row_length)
      @col_length = hash.fetch(:col_length)
      @ships = hash.fetch(:ships)
      @misses = hash.fetch(:misses)
      recreate!
    end

    def max_abs_freq
      self.max {|point1, point2| point1.abs_freq <=> point2.abs_freq}.abs_freq
    end

    def rows
      @table
    end

    def recreate!
      @table = (1..row_length).inject([]) do |accum1, item1 |
        accum1 << (1..col_length).inject([]) do |accum2, item2|
        accum2 << Battleship::Point.new(item1, item2)
      end
      end

      @misses.each {|miss| point_at(miss).miss!}
    end

    def each(&block)
      (1..row_length).each do |row|
        (1..col_length).each do |col|
          block.call(point_at([row,col]))
        end
      end
    end

    def sum_of_abs_freqs
      self.inject(0) {|accum, point| accum = accum + point.abs_freq }
    end

    def recalculate_abs_freq!
      recreate!

      @ships.each do |ship|
        ship.table = self
        self.each do |point|
          ship.start_at(point)
          ship.abs_freq!
        end
      end
    end

    def point_at(*args)
      args.flatten!
      row, col = 0,0

      if args.length == 1
        point = args.first
        row, col = point.row, point.col
      else
        row = args[0]
        col = args[1]
      end

      @table[row-1][col-1]
    end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
require 'spec_helper'

describe Battleship::Table do
  describe '#rows' do
    it 'should return the rows' do
      ships = []
      misses = []
      hash = {row_length: 2, col_length: 1, ships: ships, misses: misses}
      table = Battleship::Table.new(hash)
      table.recreate!
      expect(table.rows[0][0].row).to eq 1
      expect(table.rows[0][0].col).to eq 1

      expect(table.rows[1][0].row).to eq 2
      expect(table.rows[1][0].col).to eq 1
    end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
module Battleship
  class VerticalShip < Battleship::Ship
    def occupies_point?(row, col)
      starting_point.col == col &&
        (starting_point.row...starting_point.row + @length).any? {|item| item == row}
    end

    def fully_onboard?
      @table.row_length >= @starting_point.row - 1 + @length
    end

    def occupied_points
      (@starting_point.row...@starting_point.row + @length).map do |row|
        @table.point_at(row, @starting_point.col)
      end
    end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
require 'spec_helper'

describe Battleship::VerticalShip do
  before do
    @starting_point = Battleship::Point.new(1,1)
    @table = (1..3).map do |row|
      (1..3).map do |col|
        Battleship::Point.new(row,col)
      end
    end

    def @table.row_length; 3; end
    def @table.col_length; 3; end
    def @table.point_at(row, col)
      self[row-1][col-1]
    end
    @table[2][2].miss!

    def has_point(some_point, occupied_points)
      occupied_points.any? {|point| point.row == some_point.row && point.col == some_point.col}
    end
  end

  describe '#occupied_points' do
    it 'returns a list of occupied points' do
      def @table.point_at(row, col)
        self[row-1][col-1]
      end
      vertical_ship = Battleship::VerticalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: @starting_point)

      occupied_points = vertical_ship.occupied_points

      expect(has_point(Battleship::Point.new(1,1), occupied_points)).to eq true
      expect(has_point(Battleship::Point.new(2,1), occupied_points)).to eq true
      expect(has_point(Battleship::Point.new(3,1), occupied_points)).to eq false
    end
  end

  describe '#occupies_a_missed_point?' do
    it 'returns true if ship occupies a missed point' do
      starting_point = Battleship::Point.new(2,3)
      vertical_ship = Battleship::VerticalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: starting_point)
      expect(vertical_ship).to be_occupies_a_missed_point
    end

    it 'returns false if ship does not occupy a missed point' do
      starting_point = Battleship::Point.new(1,1)
      vertical_ship = Battleship::VerticalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: starting_point)
      expect(vertical_ship).not_to be_occupies_a_missed_point
    end
  end

  describe '#occupies?(point)' do
    it 'returns true if occupies the point' do
      vertical_ship = Battleship::VerticalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: @starting_point)

      expect(vertical_ship.occupies_point?(1,1)).to eq true
      expect(vertical_ship.occupies_point?(2,1)).to eq true
      expect(vertical_ship.occupies_point?(3,1)).to eq false
    end
  end

  describe '#fully_onboard?' do
    it 'returns true if no part of the ship is off the board' do
      vertical_ship = Battleship::VerticalShip.new(length: 2,
                                                   orientation: :vertical,
                                                   table: @table,
                                                   starting_point: @starting_point)
      expect(vertical_ship).to be_fully_onboard

      vertical_ship.start_at(Battleship::Point.new(2,1))
      expect(vertical_ship).to be_fully_onboard

    end

    it 'returns false if part of the ship is off the board' do
      vertical_ship = Battleship::VerticalShip.new(length: 2,
                                                   orientation: :vertical,
                                                   table: @table,
                                                   starting_point: @starting_point)
      vertical_ship.start_at(Battleship::Point.new(3,1))
      expect(vertical_ship).not_to be_fully_onboard
    end
  end

  describe '#abs_freq!' do
    it 'should update the values of occupied points' do
      vertical_ship = Battleship::VerticalShip.new(length: 2,
                                                   orientation: :vertical,
                                                   table: @table,
                                                   starting_point: @starting_point)
      vertical_ship.abs_freq!
      expect(@table.point_at(1,1).abs_freq).to eq 1
    end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
module Battleship
  class HorizontalShip < Battleship::Ship
    def fully_onboard?
      @table.col_length >= @starting_point.col - 1 + @length
    end

    def occupies_point?(row, col)
      starting_point.row == row &&
        (starting_point.col...starting_point.col + @length).any? {|item| item == col}
    end

    def occupied_points
      (@starting_point.col...@starting_point.col + @length).map do |col|
        @table.point_at(@starting_point.row, col)
      end
    end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
require 'spec_helper'

describe Battleship::HorizontalShip do
  before do
    @starting_point = Battleship::Point.new(1,1)
    @table = (1..3).map do |row|
      (1..3).map do |col|
        Battleship::Point.new(row,col)
      end
    end

    def @table.row_length; 3; end
    def @table.col_length; 3; end
    def has_point(some_point, occupied_points)
      occupied_points.any? {|point| point.row == some_point.row && point.col == some_point.col}
    end
    @table[2][2].miss!

    def @table.point_at(row, col)
      self[row-1][col-1]
    end
  end

  describe '#occupies?(point)' do
    it 'returns true if occupies the point' do
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: @starting_point)

      expect(horizontal_ship.occupies_point?(1,1)).to eq true
      expect(horizontal_ship.occupies_point?(1,2)).to eq true
      expect(horizontal_ship.occupies_point?(1,3)).to eq false
    end
  end

  describe '#occupied_points' do
    it 'returns a list of occupied points' do
      def @table.point_at(row, col)
        self[row-1][col-1]
      end
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: @starting_point)

      occupied_points = horizontal_ship.occupied_points

      expect(has_point(Battleship::Point.new(1,1), occupied_points)).to eq true
      expect(has_point(Battleship::Point.new(1,2), occupied_points)).to eq true
      expect(has_point(Battleship::Point.new(1,3), occupied_points)).to eq false
    end
  end

  describe '#occupies_a_missed_point?' do
    it 'returns true if ship occupies a missed point' do
      starting_point = Battleship::Point.new(3,2)
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: starting_point)
      expect(horizontal_ship).to be_occupies_a_missed_point
    end

    it 'returns false if ship does not occupy a missed point' do
      starting_point = Battleship::Point.new(2,2)
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: starting_point)
      expect(horizontal_ship).not_to be_occupies_a_missed_point
    end
  end

  describe '#occupies_valid_points?' do
    it 'returns true if all points are valid' do
      starting_point = Battleship::Point.new(1,1)
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: starting_point)
      expect(horizontal_ship).to be_occupies_valid_points
    end

    it 'returns false if some points are not valid' do
      starting_point = Battleship::Point.new(3,3)
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: starting_point)
      expect(horizontal_ship).not_to be_occupies_valid_points
    end
  end

  describe '#fully_onboard?' do
    it 'returns true if no part of the ship is off the board' do
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: @starting_point)
      expect(horizontal_ship).to be_fully_onboard

      horizontal_ship.start_at(Battleship::Point.new(1,2))
      expect(horizontal_ship).to be_fully_onboard
    end

    it 'returns false if part of the ship is off the board' do
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: @starting_point)
      horizontal_ship.start_at(Battleship::Point.new(1,3))
      expect(horizontal_ship).not_to be_fully_onboard
    end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
module Battleship
  class Ship
    attr_reader :orientation, :starting_point
    attr_accessor :table

    def initialize(hash)
      @length = hash.fetch(:length)
      @table = hash.fetch(:table) { :no_table_initialized }
      @starting_point = hash.fetch(:starting_point) { :no_starting_point }
    end

    def start_at(point)
      @starting_point = point
    end

    def occupies_valid_points?
      fully_onboard? && !occupies_a_missed_point?
    end

    def occupies_a_missed_point?
      occupied_points.any? {|point| point.missed? }
    end

    def abs_freq!
      occupied_points.each {|point| point.abs_freq += 1} if self.occupies_valid_points?
    end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
require 'spec_helper'

describe Battleship::Ship do
  before do
    @starting_point = Battleship::Point.new(1,1)
    @table = (1..3).map do |row|
      (1..3).map do |col|
        Battleship::Point.new(row,col)
      end
    end

    def @table.row_length; 3; end
    def @table.col_length; 3; end
  end

  describe '#occupies?(point)' do
    it 'returns true if occupies the point' do
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: @starting_point)

      expect(horizontal_ship.occupies_point?(1,1)).to eq true
      expect(horizontal_ship.occupies_point?(1,2)).to eq true
      expect(horizontal_ship.occupies_point?(1,3)).to eq false
    end
  end

  describe '#occupied_points' do
    it 'returns a list of occupied points' do
      def @table.point_at(row, col)
        self[row-1][col-1]
      end
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: @starting_point)

      occupied_points = horizontal_ship.occupied_points
      def has_point(some_point, occupied_points)
        occupied_points.any? {|point| point.row == some_point.row && point.col == some_point.col}
      end

      expect(has_point(Battleship::Point.new(1,1), occupied_points)).to eq true
      expect(has_point(Battleship::Point.new(1,2), occupied_points)).to eq true
      expect(has_point(Battleship::Point.new(1,3), occupied_points)).to eq false
    end
  end

  describe '#fully_onboard?' do
    it 'returns true if no part of the ship is off the board' do
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: @starting_point)
      expect(horizontal_ship).to be_fully_onboard

      horizontal_ship.start_at(Battleship::Point.new(1,2))
      expect(horizontal_ship).to be_fully_onboard

    end

    it 'returns false if part of the ship is off the board' do
      horizontal_ship = Battleship::HorizontalShip.new(length: 2,
                                                       table: @table,
                                                       starting_point: @starting_point)
      horizontal_ship.start_at(Battleship::Point.new(1,3))
      expect(horizontal_ship).not_to be_fully_onboard
    end

  end
end

{% endhighlight %}

{% highlight ruby linenos %}
module Battleship
  class Point
    attr_reader :row, :col
    attr_accessor :abs_freq

    def initialize(row, col, *args)
      @row = row
      @col = col
      @abs_freq = 0
      @state = args.first || :untried
    end

    def hit!
      @state = :hit
    end

    def hit?
      @state == :hit
    end

    def miss!
      @state = :missed
    end

    def missed?
      @state == :missed
    end

    def untried?
      @state == :untried
    end

    def same_as?(point)
      row == point.row && col == point.col
    end
  end
end

{% endhighlight %}

{% highlight ruby linenos %}
require 'spec_helper'

describe Battleship::Point do
  describe '#row' do
    it 'should return the row' do
      bp = Battleship::Point.new(1,2)
      expect(bp.row).to eq 1
    end
  end

  describe '#col' do
    it 'should return the col' do
      bp = Battleship::Point.new(1,2)
      expect(bp.col).to eq 2
    end
  end

  describe '#miss!' do
    it 'sets the state of the point to :miss' do
      bp = Battleship::Point.new(1,2)
      bp.miss!

      expect(bp).to be_missed
    end
  end

  describe '#same_as?(point)' do
    it 'should be true if point has the same coordinates as the given point' do
      bp = Battleship::Point.new(1,2)
      expect(bp.same_as?(bp)).to eq true
    end
  end

  describe '#hit!' do
    it 'sets the state of the point to :hit' do
      bp = Battleship::Point.new(1,2)
      bp.hit!

      expect(bp).to be_hit
    end
  end

  it 'should be untried at first' do
    bp = Battleship::Point.new(1,2)
    expect(bp).to be_untried
  end

  it 'can be initialized to being missed' do
    bp = Battleship::Point.new(1,2, :missed)
    expect(bp).to be_missed
  end
end

{% endhighlight %}
  <script src="http://d3js.org/d3.v3.js"></script>
  <script type="text/javascript">
  var unprocessed_data = [[0.3333333333333333, 0.3333333333333333, 0.6666666666666666, 0.6666666666666666, 1.0, 0.6666666666666666, 0.6666666666666666, 0.3333333333333333, 0.3333333333333333, 0.0], [0.3333333333333333, 0.0, 0.5, 0.3333333333333333, 0.6666666666666666, 0.6666666666666666, 1.0, 0.5, 0.6666666666666666, 0.3333333333333333], [0.6666666666666666, 0.5, 1.0, 0.5, 0.6666666666666666, 0.3333333333333333, 0.5, 0.0, 0.5, 0.3333333333333333], [0.6666666666666666, 0.3333333333333333, 0.6666666666666666, 0.0, 0.3333333333333333, 0.3333333333333333, 0.6666666666666666, 0.5, 1.0, 0.6666666666666666], [1.0, 0.5, 1.0, 0.16666666666666666, 0.3333333333333333, 0.0, 0.3333333333333333, 0.3333333333333333, 0.6666666666666666, 0.6666666666666666], [0.8333333333333334, 0.3333333333333333, 0.8333333333333334, 0.0, 0.0, 0.3333333333333333, 0.3333333333333333, 0.6666666666666666, 0.6666666666666666, 1.0], [0.6666666666666666, 0.3333333333333333, 0.6666666666666666, 0.0, 0.0, 0.16666666666666666, 0.0, 0.5, 0.3333333333333333, 0.6666666666666666], [0.6666666666666666, 0.5, 1.0, 0.6666666666666666, 0.8333333333333334, 1.0, 0.6666666666666666, 1.0, 0.5, 0.6666666666666666], [0.3333333333333333, 0.0, 0.5, 0.3333333333333333, 0.3333333333333333, 0.5, 0.3333333333333333, 0.5, 0.0, 0.3333333333333333], [0.3333333333333333, 0.3333333333333333, 0.6666666666666666, 0.6666666666666666, 0.8333333333333334, 1.0, 0.6666666666666666, 0.6666666666666666, 0.3333333333333333, 0.3333333333333333]]
  var row_length = unprocessed_data[0].length
  var col_length = unprocessed_data.length
  var data = []
  for (row=0; row< row_length; row++) {
    for (col=0; col< col_length; col++) {
      data.push({score: unprocessed_data[col][row], row: row, col: col})
    }
  }

//height of each row in the heatmap
//width of each column in the heatmap
var gridSize = 20,
    h = gridSize,
    w = gridSize,
    rectPadding = 60;

var colorLow = 'green', colorMed = 'yellow', colorHigh = 'red';

var margin = {top: 20, right: 80, bottom: 30, left: 50},
    width = 300 - margin.left - margin.right,
    height = 230 - margin.top - margin.bottom;

  var colorScale = d3.scale.linear()
.domain([-1, 0, 1])
  .range([colorLow, colorMed, colorHigh]);

  var svg = d3.select("#heatmap").append("svg")
  .attr("width", width + margin.left + margin.right)
  .attr("height", height + margin.top + margin.bottom)
  .append("g")
  .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

  var heatMap = svg.selectAll(".heatmap")
  .data(data, function(d) { return d.col + ':' + d.row; })
  .enter().append("svg:rect")
  .attr("x", function(d) { return d.row * w; })
  .attr("y", function(d) { return d.col * h; })
  .attr("width", function(d) { return w; })
  .attr("height", function(d) { return h; })
  .style("fill", function(d) { return colorScale(d.score); });

  </script>
