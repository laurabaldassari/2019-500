# 500 Class 03: 2019-02-14

- The slides for Class 3 are [available in PDF](https://github.com/THOMASELOVE/2019-500/blob/master/slides/class03/500_2019_slides_class03.pdf).
- We will post the audio recording above, as soon as we can.
- The [Course Schedule](https://github.com/THOMASELOVE/2019-500/blob/master/SCHEDULE.md) is the place to go for all deadlines and deliverables information. 
- Happy Valentine's Day, and Happy Birthday (to me)!

## Today, we will discuss...

- How The Propensity Score Is Used
    - Propensity Score Subclassification or Stratification
    - Direct Adjustment for the Propensity Score
    - Propensity Score Weighting
    - Multivariate Matching with the Propensity Score
    - Gum et al.'s Aspirin Example ([pdf of the paper is on our Texts page](https://github.com/THOMASELOVE/2019-500/blob/master/texts/Gum%202001%20JAMA%20Aspirin%20Use%20Propensity%20Analysis.pdf))
- Positivity and Other Important Requirements for Causal Inference
- Homework 2, which is due 2019-02-14 at noon
- Rosenbaum, Chapters 5 and 6
- Setting Up [The Toy Example](https://github.com/THOMASELOVE/2019-500/tree/master/data-and-code/toy_example) for Class 04

## Announcements

1. The Cleveland Chapter of the American Statistical Association's Annual Spring Conference will be held 2019-05-10, featuring Mark Ward and Doug Crabill on *Query, Wrangle, Scrape or Parse Your Big Data into Submission!*. 

> This (full-day) seminar will be an introduction to the basics of data analysis tools, such as R, SQL, UNIX, awk, and data formats such as XML and/or JSON. It is a hands-on workshop. Participants will be expected to bring a laptop computer and to be prepared to learn-by-doing. No prerequisite knowledge is assumed. Instead, it is expected that participants will be eager to learn some tools for working with large data. Active learning will be used throughout the day. 

- For more details, [visit this link](https://sites.google.com/view/cleveland-asa/conferences/upcoming-conference). The price for full-time students is just $50 until 2019-04-15, and pre-registration is required.

2. If you're interested in attending what I believe to be the most useful academic conference I attend, or just in visiting San Diego in January 2020, consider the [International Conference on Health Policy Statistics](http://ww2.amstat.org/meetings/ichps/2020/). As [Liz Stuart reminds me](https://twitter.com/Lizstuartdc/status/1095372654155100160), invited session proposals are due March 4, but regular abstracts are due later this year.

3. A reminder that we will not meet next week. Our next class is 2019-02-28, when we will discuss the [Toy Example](https://github.com/THOMASELOVE/2019-500/tree/master/data-and-code/toy_example).


## NEW! A nice tutorial on "positivity" and what it means

- Ellie Murray (@EpiEllie on Twitter) posted a [nice causal inference explainer to Twitter on positivity](https://twitter.com/EpiEllie/status/1089219830052474880).

> If you are interested in understanding causal effects from data, then you need to understand the concept of positivity. This article explains what this means and why it’s important.

- If you want a more thorough presentation (all in one place, fewer GIFs), check out the closely related version Ellie posted to [Medium.com](https://medium.com/@EpiEllie/positivity-what-it-is-and-why-it-matters-for-data-science-d5e9c0bc1fcb), entitled "[Positivity: what it is and why it matters for data science](https://medium.com/@EpiEllie/positivity-what-it-is-and-why-it-matters-for-data-science-d5e9c0bc1fcb)". Here's her tag line:

![](https://github.com/THOMASELOVE/2019-500/blob/master/slides/class02/figures/ellie_positivity.PNG)

## Another interesting problem with some "research"?

[Vince Buffalo](https://twitter.com/vsbuffalo/status/1091790085610065920?s=11) made a number of interesting points in a tweet about Julia Belluz' article in Vox from 2019-02-01, entitled "[Eating breakfast is not a good weight loss strategy, scientists confirm](https://www.vox.com/2019/2/1/18206873/breakfast-diet-weight-loss)".


