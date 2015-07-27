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

$$
\begin{align}

 p(color=red | box=1) &= \frac{3}{8} \\
 p(color=white | box=1) &= \frac{5}{8} \\
 p(color=red | box=2) &= \frac{2}{7} \\
 p(color=white | box=2) &= \frac{5}{7} \\
 p(box=1 | color=red ) &= \frac{p(color=red,box=1)}{p(color=red)} \\
  &= \frac{p(color=red|box=1)p(box=1)}{p(color=red)} \\
  &= \frac{p(color=red|box=1)p(box=1)}{\Sigma_b p(color=red,box=b)} \\
  &= \frac{p(color=red|box=1)p(box=1)}{\Sigma_b p(color=red|box=b)p(box=b)} \\
  &= \frac{p(color=red|box=1)p(box=1)}{p(color=red|box=1)p(box=1) + p(color=red|box=2)p(box=2)} \\
  &= \frac{\frac{3}{8}\times\frac{1}{2}}{\frac{3}{8}\times\frac{1}{2} + \frac{2}{7}\times\frac{1}{2}} \\
  &= \frac{\frac{1}{2}\times\frac{3}{8}}{\frac{1}{2}(\frac{3}{8} + \frac{2}{7})} \\
  &= \frac{\frac{3}{8}}{\frac{3}{8} + \frac{2}{7}} \\
  &= \frac{\frac{3}{8}}{\frac{21}{56} + \frac{16}{56}} \\
  &= \frac{\frac{3}{8}}{\frac{37}{56}} \\
  &= \frac{3}{8}\times\frac{56}{37} \\
  &= \frac{21}{37} \\
\end{align}
$$
