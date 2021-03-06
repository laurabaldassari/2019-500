# Course Projects for 500, Spring 2018

## Introduction

As a substantial part of your course grade, you will complete a small observational study comparing two exposures on one or more outcome(s) in time to generate an abstract, give a presentation, and complete a thorough written discussion using R Markdown.

"It is hard to learn statistics (or anything else) passively; concurrent theory and application are essential."

Though hardly an original idea in general, this particular phrasing is stolen from Harry Roberts, as are several of the bulleted points to follow, originally prepared for his courses at the University of Chicago. I am also grateful to Doug Zahn, for several helpful suggestions swiped from his work at Florida State University, and to Dave Hildebrand, for many things, not least his excellent example at Wharton. 

There is more to a statistical application than the analysis of a canned data set, even a good canned data set. George Box noted that "statistics has no reason for existence except as the catalyst for investigation and discovery." Expert clinical researchers and statisticians repeatedly emphasize how important it is that people be able to write well, present clearly, work to solve problems, and show initiative. This project assignment is designed to help you develop your abilities and have a memorable experience.

## Deliverables and their Deadlines

I want you to establish relevant and interesting research questions related to a problem of interest, procure data to help answer the questions and pose others, and communicate your results to an audience of your peers. You will be responsible for the following elements of a project, described in detail in the rest of this document. All materials for the project should be submitted through canvas.case.edu

**Please don't be shy about asking for help sooner, rather than later. Options narrow as an investigation progresses. The earlier I hear about a problem, the more likely I will be able to help solve it.**

**Note also that some tips for the project are provided** [on this tips page (about coding and strategy)](https://github.com/THOMASELOVE/2019-500/blob/master/projects/tips.md).

**NEW** You can work alone, or in a team of two on this project. To work as a team of two, you and your partner need to email Dr. Love to tell him of your desire to work together on this no later than noon on 2019-02-14.

**NEW** Fill out [this form](http://bit.ly/500-2019-project-scheduling-form) to express your preferences about the timing of your final project presentation. [The form](http://bit.ly/500-2019-project-scheduling-form) is due at noon on 2019-03-05.

1. The [Project Proposal](https://github.com/THOMASELOVE/2019-500/tree/master/projects/proposal) for which you will submit an initial draft in February, and then a final version in March, following the deadlines in the [Course Schedule](https://github.com/THOMASELOVE/2019-500/blob/master/SCHEDULE.md). For complete details on the proposal, [go here](https://github.com/THOMASELOVE/2019-500/tree/master/projects/proposal).

2. The [Project Update](https://github.com/THOMASELOVE/2019-500/tree/master/projects/update) is due at the start of April, as specified in the [Course Schedule](https://github.com/THOMASELOVE/2019-500/blob/master/SCHEDULE.md). Here you will be revising your proposal, verifying that you have the data and are proceeding appropriately. For complete details on the update, [go here](https://github.com/THOMASELOVE/2019-500/tree/master/projects/update).

3. The [Final Materials](https://github.com/THOMASELOVE/2019-500/tree/master/projects/final) which you will submit near the end of the term. This includes:

- An **abstract** and final **presentation** to the class about your results. 
    - Presentations will be given at the last three class sessions, according to a schedule to be established in early March. See the [Course Schedule](https://github.com/THOMASELOVE/2019-500/blob/master/SCHEDULE.md) for details.
- A final set of materials, including a revised abstract and presentation slides, but also a data set, R Markdown file and HTML results, including a **discussion** is due at noon on May 6, as specified in the [Course Schedule](https://github.com/THOMASELOVE/2019-500/blob/master/SCHEDULE.md).
- For more details on the final set of materials for the project, [go here](https://github.com/THOMASELOVE/2019-500/tree/master/projects/final).

Every part of the Course Project should be submitted through [Canvas](https://canvas.case.edu/) unless I explicitly state otherwise.

## If you are completely out of ideas for a project in 500, here are three possibilities (Sent via email 2019-03-03)

1.  Use [County Health Rankings](http://www.countyhealthrankings.org/explore-health-rankings/rankings-data-documentation) data. 

> As of 2016, there were 3,007 counties, 64 parishes, 19 organized boroughs, 10 census areas, 41 independent cities, and the District of Columbia for a total of 3,142 counties and county-equivalents in the 50 states and District of Columbia. There are an additional 100 county equivalents in the territories of the United States. (Wikipedia). 

- I could imagine, for instance, your pulling down data from a series of states until you have a reasonable cross-section of information from the most recent County Health Rankings for, say, 1500 counties, for which you have a quantitative outcome like age-adjusted years of potential life lost per 100,000 population, or percentage of adults reporting fair or poor health, an exposure variable that you develop from the data - like whether the income inequality ratio was above or below a certain threshold (or, perhaps better, whether it was in the top quarter or the bottom half of counties as a whole so you'd have something like a 1:2 ratio between exposed (to, for instance, high income inequality) and control). Then, as covariates you would have a lot of county specific information.

2. Use [NHANES](https://www.cdc.gov/nchs/nhanes/index.htm) data. The National Health and Nutrition Examination Survey is an excellent source of potential data for you, with lots of interesting outcomes, treatments and covariates to explore.

3. Use [500 Cities](https://www.cdc.gov/500cities/index.htm) data. This is a pretty easy download, and there are lots of approaches you could take that would be interesting. Again, the hard work would be identifying a treatment, outcome and covariates that make sense.
