# 500 Class 05: 2019-03-07

- Slides for Class 5 are available, above, in R Markdown or PDF. 
    - In a change of plans, we'll be discussing sensitivity analysis for matched samples.
- We will post the audio recording above, as soon as we can.

## Video of the Day / Why I Code in R Markdown

Here's a [video we'll watch today](https://www.youtube.com/watch?time_continue=1&v=s3JldKoA0zw). Apologies to those of you who've seen this before.

- I was motivated to show you this by David Keyes (@dgkeyes) [who had a nice set of posts](https://twitter.com/dgkeyes/status/1101554699566641152) about the benefits of R Markdown, to which Jenny Bryan responded by linking to the [1 minute 44 second video](https://www.youtube.com/watch?time_continue=1&v=s3JldKoA0zw).
- There's a [nice repository](https://github.com/EvaMaeRey/from_raw_data_to_paper_and_presentation) by Gina Reynolds (EvaMaeRey) showing [examples of implementing a reproducible workflow using R Markdown](https://github.com/EvaMaeRey/from_raw_data_to_paper_and_presentation) from raw data to a research paper, slides, and a poster.
- From that same thread, comes a link to [posterdown](https://github.com/brentthorne/posterdown) which looks like a nice tool for generating PDF posters of your research using R Markdown.

## Project Proposals and Scheduling

The "final" version of your [Project Proposal](https://github.com/THOMASELOVE/2019-500/tree/master/projects/proposal) was due Tuesday 2019-03-05 at ~noon~ 6 PM. The [Project Presentation Scheduling Form](http://bit.ly/500-2019-project-scheduling-form) was due then, too.

- The dates for the project presentations are all on Thursdays: April 18, April 25 and May 2. I had the last date wrong on the form, and when I fixed it, some people's checks disappeared (I let them know via email.)
- We have 25 students in the class, and 22 projects in total to hear. So we'll do 8 one day and 7 on the other two days. 

When your grade on the Project Proposal (Final Version) on Canvas is 10/10, I'm satisfied and your proposal is approved. Your next task is to do the project, and your next deliverable regarding the project is the [Project Update](https://github.com/THOMASELOVE/2019-500/tree/master/projects/update) due at the start of April.

### Project Presentation Schedule 

Time | April 18 | April 25 | May 2
:-----------------: | :------: | :------: | :------: 
8:35 AM to 8:50 AM | Sarah | Harry | Julijana
8:52 AM to 9:07 AM | Gwen/Roberto | Brian | Hyun Jo
9:09 AM to 9:24 AM | Laura B. | Sneha | Kelly
9:26 AM to 9:41 AM | Andrew | Sebastian | Bob
9:41 AM to 9:52 AM | BREAK | BREAK | BREAK
9:52 AM to 10:07 AM | Michael | Laura C. | Jenny
10:09 AM to 10:24 AM | Jordan | Xin-Xin | Hasina/Gi-Ming
10:26 AM to 10:41 AM | Zhanwen | Kedar | Abhishek/Sandra
10:43 AM to 10:58 AM | Dr. Love | Yousef | Dr. Love

- Does this work for you, personally?

## Coming Soon

Due to CWRU Spring Break, our next class will be 2019-03-21, and we'll discuss matching approaches in detail, and work through a case study. Due that day (at noon) are [Homework 3](https://github.com/THOMASELOVE/2019-500/tree/master/assignments/homework3) and [Chapter 8 Essay](https://github.com/THOMASELOVE/2019-500/blob/master/assignments/essayprompts.md).

- [Homework 3](https://github.com/THOMASELOVE/2019-500/tree/master/assignments/homework3) requires you to do several tasks we did with the `toy` data last week, using a new (simulated) data set. This includes unadjusted outcome analyses (on two binary outcomes), fitting a straightforward main-effects-only propensity model to balance eight covariates, estimating Rubin's Rules 1 and 2 prior to propensity adjustment, using direct adjustment for the (logit of the) propensity score, using subclassification by propensity score quintile, and matching 1:1 without replacement, then comparing the results on one of the two outcomes after adjustment to the unadjusted estimate. It will take a while to get all of that done, so I encourage you to get started soon.
- Chapter 8 of Rosenbaum is about Quasi-Experimental Devices, including the use of multiple control groups, control by systematic variation, counterparts and control outcomes. There's also a little discussion of discontinuity designs. [The required essay](https://github.com/THOMASELOVE/2019-500/blob/master/assignments/essayprompts.md#prompt-for-chapter-8-quasi-experimental-devices-due-for-class-6) asks you to describe a setting where multiple control groups could be used productively.

## Rosenbaum Essays after Chapter 7

I've gathered some comments (and a few examples of your writing) about elaborate theories and their role in designing and developing compelling observational studies [here](https://github.com/THOMASELOVE/2019-500/tree/master/assignments/essay07). Please take a look.

## Sensitivity Analysis for Matched Samples

Visit [this link on our Data and Code page](https://github.com/THOMASELOVE/2019-500/tree/master/data-and-code#sensitivity-spreadsheet-beware---this-was-built-in-2008) for some examples of sensitivity analysis for matched samples using both a spreadsheet and `rbounds`. We'll discuss these tools today in class.

