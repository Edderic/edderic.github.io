# Implementing a Scoring Algorithm of NJ SEEDS Alumni

I recently got the chance to attend this year's NJ SEEDS Alumni Association's
alumni retreat. [NJ SEEDS](http://njseeds.org/) helps bright students from
low-income families improve their life outcomes by putting its scholars into
environments that increase students' chances of getting into highly competitive
colleges. Anyway, the alums got to brainstorm ideas that we would like to try
in order to improve alumni commitment to the program. One thing that was
mentioned was the idea of a scoring algorithm that stands as a proxy for how
committed an alum is to the organization; apparently Stanford does this with
their alumni for a variety of reasons:

  1. They quantitatively know which alums are the most likely to help out when the
     organization needs something, because people who have invested a lot in terms of
     time, energy, and/or money probably enjoy doing so and therefore are likely to
     keep investing and supporting the organization.

  2. If Alum \\(X\\) needs something from the organization, they know how invested
     they should be in entertaining a graduate's request.

Other reasons to have a scoring algorithm might be to actually incentivize good
behavior and utilize the competitive nature of SEEDS alum, like how Fitbit shows
individuals how they are doing every week, compared to their peers:

<figure>
<img src="/images/boat-shoe-badge-email.png" alt="Boat-Shoe Badge by Fitbit">
<figcaption>Reward for reaching a milestone</figcaption>
</figure>

<figure>
<img src="/images/weekly-stats-fitbit.png" alt="Weekly Stats by Fitbit">
<figcaption>Show stats and encourage friends to push each other</figcaption>
</figure>

In this article, I propose a simple algorithm that takes into account several
features that signify alumni behavior that is beneficial to NJ SEEDS.

## Algorithm

### Version 1: All-Time

An alumni's score can take into consideration the following features:

  * total amount of money donated
  * total number of times donated
  * number of events attended
  * number of events hosted
  * average number of alum "pulled" in per event

The first two metrics are money-related. Number of events attended, number of
events hosted, and average number of alums "pulled" into events, on the other
hand, focus more on social aspects that I think are important in maintaining
and improving relationships within alumni.

Using the total amount of money donated as a metric is obvious -- more money donated
to SEEDS is a good thing and helps the non-profit organization run.

The total number of times donated, on the other hand, is less obvious. The
benefit of this metric is that alums who might not be in good financial status
-- and therefore, might have a harder time donating money -- can still do well
in supporting SEEDS. A lot of potential donors apparently decide whether or not
they are going to contribute on the basis of alumni participation in donations.
In this case, the total amount of money donated by one alum is not as important
as having very many alum donating, even if the donations are individually
small.

Number of events attended measures the time commitment of alumni to the
organization. This could be related to social events or even volunteering
events that help SEEDS in one shape or form.

Number of events hosted rewards alumni who are hosting events. A problem I see
right now is that the people hosting alumni events might be "pulling" in the
same people most of the time. By having other people host events, they might be
able to "pull" people that might not show up otherwise.

Lastly, the average number of alum "pulled" in per event is a measure of social
influence. If person \\(A\\) invites person \\(B\\) to a SEEDS event, and
person \\(B\\) says in a survey that part of the reason he/she/(insert
preferred pronoun here) attended an event is because of Person \\(A\\), then
person \\(A\\) has "pulling" power. Over time, if it becomes a habit for Person
\\(B\\) to attend events, and person \\(B\\) attends events because it is a
habit and does not list person \\(A\\) as a reason of attendance, then Person
\\(A\\) has to bring in other alumni that haven't been going to the events, in
order to improve performance on this metric.

#### Examples

For example, let's say that Jenny, an alumnus who has contributed so much to
the organization in countless years has donated a total of $8,000, donated a
total of \\(30\\) times, attended \\(50\\) SEEDS events, hosted \\(3\\) events,
and had an average of bringing \\(4\\) alumni to events:

$$
\begin{align}
    J_{total\ donated\ dollars} &= 10,000 \\
    J_{donation\ absolute\ frequency} &= 30 \\
    J_{events\ attended} &= 50 \\
    J_{events\ hosted} &= 3 \\
    J_{avg\ num\ alum\ pulled} &= 4
\end{align}
$$

A recent and excited graduate of SEEDS, George, has donated \\($11,000\\),
donated \\(5\\) times, attended \\(3\\) SEEDS events, hosted \\(0\\) events,
and had an average of bringing \\(0\\) alumni to events:

$$
\begin{align}
    G_{total\ donated\ dollars} &= 11,000 \\
    G_{donation\ absolute\ frequency} &= 5 \\
    G_{events\ attended} &= 3 \\
    G_{events\ hosted} &= 0 \\
    G_{avg\ num\ alum\ pulled} &= 0
\end{align}
$$

To calculate the scores for each person, we find the maximum values of each feature:

$$
\begin{align}
    max(total\ donated\ dollars) &= 11,000 \\
    max(donation\ absolute\ frequency) &= 30 \\
    max(events\ attended) &= 50 \\
    max(events\ hosted) &= 3 \\
    max(avg\ num\ alum\ pulled) &= 4 \\
\end{align}
$$

We then divide each person's performance in each category by the corresponding
maximum values and average them out.

Jenny's score can be calculated as follows:

$$
\begin{align}
    score(J) &= \frac{\frac{J_{total\ donated\ dollars}}{max(total\ donated\ dollars)} +
                      \frac{J_{donation\ absolute\ frequency}}{max(donation\ absolute\ frequency)} +
                      \frac{J_{events\ attended}}{max(events\ attended)} +
                      \frac{J_{events\ hosted}}{max(events\ hosted)} +
                      \frac{J_{avg\ num\ alum\ pulled}}{max(avg\ num\ alum\ pulled)}
                     }{5} \\
             &= \frac{\frac{10,000}{11,000} +
                      \frac{30}{30} +
                      \frac{50}{50} +
                      \frac{3}{3} +
                      \frac{4}{4}
                     }{5} \\
             &= \frac{10/11 + 4}{5} \\
             &\approx 0.982
\end{align}
$$

The number reflects the idea that Jenny is a superstar alumni.

Let's calculate George's score:


$$
\begin{align}
    score(G) &= \frac{\frac{G_{total\ donated\ dollars}}{max(total\ donated\ dollars)} +
                      \frac{G_{donation\ absolute\ frequency}}{max(donation\ absolute\ frequency)} +
                      \frac{G_{events\ attended}}{max(events\ attended)} +
                      \frac{G_{events\ hosted}}{max(events\ hosted)} +
                      \frac{G_{avg\ num\ alum\ pulled}}{max(avg\ num\ alum\ pulled)}
                     }{5} \\
             &= \frac{\frac{11,000}{11,000} +
                      \frac{5}{30} +
                      \frac{3}{50} +
                      \frac{0}{2} +
                      \frac{0}{4}
                     }{5} \\
             &= \frac{1 + \frac{5}{30} + \frac{3}{50}}{5} \\
             &\approx 0.245
\end{align}
$$

So even though George was able to raise the most amount in terms of donations
(\\($11,000\\)), he did not perform as well as Jenny because she performed
strongly in all the metrics -- not just one section. The benefit of this
approach is that it considers the long term performance of alumni, and is
biased towards high-performing senior alum. A senior alum who has been active
in the community many years will generally have a higher score than someone who
just became an alumni but performs strongly.  However, this benefit could also
a weakness; new members, even though they might be giving their all in
supporting SEEDS as alum, might be turned off because their current efforts are
just not as successful as the seniors because the seniors have had years of a
head start.

### Version 2: Averaged Per Year

Maybe we could augment this all-time scoring algorithm with one that takes
more averages into account. Junior members of the SEEDS community can better
compete with veteran alums by considering:

  * average amount of money donated per year
  * average number of events attended per year
  * average number of events hosted per year
  * average number of times donated per year
  * average number of alum "pulled" in per event.

#### Examples

A scenario for Jenny and George in this case could be the following:

Jenny raised an average of \\($750\\) per year, attended an average of \\(5\\)
events per year, hosted an average of \\(2\\) events per year, donated an
average of \\(5\\) times per year, and brought \\(4\\) other alumni. On the
other hand, George has raised \\($4,000\\) per year, attended \\(4\\) events
per year, hosted \\(0\\) events, donated \\(5\\) times per year, and brings
\\(5\\) alumni to events per year on average.

Calculating the score this way is as follows:

$$
\begin{align}
    score(J) &= \frac{\frac{J_{avg\ donated\ dollars}}{max(avg\ donated\ dollars)} +
                      \frac{J_{avg\ donation\ freq}}{max(avg\ donation\ freq)} +
                      \frac{J_{avg\ events\ attended}}{max(avg\ events\ attended)} +
                      \frac{J_{avg\ events\ hosted}}{max(avg\ events\ hosted)} +
                      \frac{J_{avg\ num\ alum\ pulled}}{max(avg\ num\ alum\ pulled)}
                     }{5} \\
             &= \frac{\frac{750}{4,000} +
                      \frac{5}{5} +
                      \frac{5}{5} +
                      \frac{2}{2} +
                      \frac{4}{5}
                     }{5} \\
             &= \frac{3.9875}{5} \\
             &= 79.75\%
\end{align}
$$

$$
\begin{align}
    score(G) &= \frac{\frac{G_{avg\ donated\ dollars}}{max(avg\ donated\ dollars)} +
                      \frac{G_{avg\ donation\ freq}}{max(avg\ donation\ freq)} +
                      \frac{G_{avg\ events\ attended}}{max(avg\ events\ attended)} +
                      \frac{G_{avg\ events\ hosted}}{max(avg\ events\ hosted)} +
                      \frac{G_{avg\ num\ alum\ pulled}}{max(avg\ num\ alum\ pulled)}
                     }{5} \\
             &= \frac{\frac{4,000}{4,000} +
                      \frac{5}{5} +
                      \frac{4}{5} +
                      \frac{0}{2} +
                      \frac{5}{5}
                     }{5} \\
             &= \frac{3.8}{5} \\
             &= 76\%
\end{align}
$$

In the case of averaging, veteran superstar alumnus Jenny and junior superstar
alumnus George do comparably well.

