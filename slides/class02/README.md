# 500 Class 02: 2019-01-31

- The slides for Class 2 are [now available in PDF](https://github.com/THOMASELOVE/2019-500/blob/master/slides/class01/500_2019_slides_class02.pdf).
- We will post the audio recording above, as soon as we can.
- The [Course Schedule](https://github.com/THOMASELOVE/2019-500/blob/master/SCHEDULE.md) is the place to go for all deadlines and deliverables information. 

## Today, we will discuss...

- A Motivating Example on Aspirin and Mortality based on the Gum paper, linked on [our Texts page](https://github.com/THOMASELOVE/2019-500/blob/master/texts/README.md)
- [Homework 1](https://github.com/THOMASELOVE/2019-500/tree/master/assignments/homework1), especially Questions 2 and 3
- The Hormone Replacement Therapy Story
- Rosenbaum *Observation and Experiment* Preface and Chapters 1-4
- Tools for Assessing Causal Effects
- Cochran's Smoking Example

## A Useful Tip when using R to `mutate`

See [@_ColinFay's Tweet from 2019-01-23](https://twitter.com/_ColinFay/status/1088022736117645314):

![](https://github.com/THOMASELOVE/2019-500/blob/master/slides/class02/tweet_fay.png)

## NEW! A nice tutorial on "positivity" and what it means

- Ellie Murray (@EpiEllie on Twitter) posted a [nice causal inference explainer to Twitter on positivity](https://twitter.com/EpiEllie/status/1089219830052474880).
- If you want a more thorough presentation (all in one place, fewer GIFs), check out the closely related version she posted to [Medium.com](https://medium.com/@EpiEllie/positivity-what-it-is-and-why-it-matters-for-data-science-d5e9c0bc1fcb), entitled "[Positivity: what it is and why it matters for data science](https://medium.com/@EpiEllie/positivity-what-it-is-and-why-it-matters-for-data-science-d5e9c0bc1fcb)". Here's her tag line:

![]()

> Positivity means that if we want to understand causal effects of an exposure we should only include people who have a chance of having every level of exposure we care about. For example, if we always treat pregnant women, then we should not include these women in our study. Similarly if we never treat those who are allergic, we shouldn’t include them either. But if we sometimes treat people who are in pain and sometimes don’t, that’s the right set of people to look at!
