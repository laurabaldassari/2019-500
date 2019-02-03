# Final Materials for 500 Projects

## Submission Details

You will submit your final project materials in two parts. Submit all project materials through [Canvas](https://canvas.case.edu/).

1. By the deadline specified in the [Course Schedule](https://github.com/THOMASELOVE/2019-500/blob/master/SCHEDULE.md), you will submit your pre-presentation versions of your [Abstract](https://github.com/THOMASELOVE/2019-500/blob/master/projects/final/README.md#the-abstract) and [Slides](https://github.com/THOMASELOVE/2019-500/blob/master/projects/final/README.md#the-presentation). The same deadline for the Abstract applies to everyone, and the deadline for the Slides depends on when you are actually giving your presentation.
2. By **noon on May 6**, after you've all given your presentations and received feedback on them, you will submit your final set of materials, including your abstract and slides (again, with revisions as necessary), your data set, R Markdown file and HTML document including a **discussion** [as outlined below](https://github.com/THOMASELOVE/2019-500/blob/master/projects/final/README.md#the-final-set-of-deliverables-due-may-6-at-noon).

The remainder of this document describes these pieces, and also provides some insight on [how I'd like to see you put together your presentation](https://github.com/THOMASELOVE/2019-500/blob/master/projects/final/README.md#some-suggestions-and-a-potential-outline-for-your-presentation), and [how you will be evaluating the presentations](https://github.com/THOMASELOVE/2019-500/blob/master/projects/final/README.md#evaluating-the-project-presentations).

**ASK QUESTIONS EARLY. It's always easier to make adjustments when time pressure isn't a major issue.**

## The Abstract

Your abstract should be no longer than 2 pages (perhaps 4,000 characters at the most) and contains much of your approved proposal (perhaps more succinctly summarizing some of the background, data set, and methodological details to meet the character limit.) To this, you will add (still within the character limit) brief Results and Conclusions sections. Unlike our previous versions of this task, this version of the Abstract should be divided into four sections, as indicated below:

- a **Background** section, to include basic descriptive information about the problem of interest and its clinical relevance, leading to a study objective, and concluding with a careful statement of the main research question, or hypothesis.
- a **Methods** section, to include the classification of the type of research design, a description of the setting and participants, the specific details on the intervention or exposure of interest, and how it is allocated to participants, along with a listing of primary outcome measures and a description of the data set. You'll also need to specify (in general terms) the covariates used in building your propensity score. This should then be followed by a paragraph or two describing the statistical methodology used for both developing the balanced covariate information through (in one analysis) matching on the propensity score and (in another analysis) some other method involving propensity weighting, as well as specifying the actual method of comparing outcomes after propensity scores have been used.
- a **Results** section, to include the results for your primary outcome, and any secondary outcomes, probably described using point estimates and confidence intervals, rather than *p* values, and also describing the effectiveness of the propensity score work you did in improving covariate balance across your exposure groups. Any sensitivity analyses should also be reported here, though in a manuscript, they might make the discussion section instead of the Results.
- a **Conclusions** section, to include a brief summary of the key conclusions, related directly to the research questions posed in the Background section, along with some indication of plans for future work.

The version of your Abstract that you submit on April 18 should be complete. If you decide to make changes as a result of comments made in the course of your Presentation, then the version you submit on May 1 should reflect that. 

## The Presentation

After all of the project proposals have been approved, we will settle on a schedule for the presentations (some will be on April 25, some on May 1.) Your slides must be submitted prior to the presentation (by 6 PM on April 24) in either PDF or Powerpoint format, regardless of which day you are speaking on.

Broadly, your slides will include an introduction which provides a foundation by motivating and clearly stating the research questions you studied, a main section which summarizes your pre-data collection beliefs, the key models and analytical results, and the critical findings of the study, and a conclusion, which provides insight into how your knowledge of the problem you studied has changed as a result of the project, as well as highlighting what you believe to be the key takeaways (both statistical and study-specific) for your audience. These sections should be keyed to slides, smoothing transitions, and forcing you to "tell us what you're going to tell us, tell us, then tell us what you told us."  

**NOTE THE CHANGE IN TIME**: Plan for 15 minutes of total time, which should include about 12-13 minutes of slides, allowing 1-2 minutes for asking and answering questions during the talk, and 1-2 minutes between talks.

### Some Suggestions and a Potential Outline for Your Presentation

Don't use more than 20 slides (in fact, 15-16 should be sufficient), including a title slide containing the project title, and your name, email and affiliation(s). Use large, extremely readable fonts. Class slides provide insight into what I think works well. 

Here's how I might outline such a talk. Do not feel obligated to follow this outline precisely, but I thought it might help to see what I'm thinking about when I say 15-16 slides is sufficient. You are only going to have time to talk about a primary outcome, so choose it well.

- Slide 1: Meaningful Title, with your contact details, affiliations, and the date. 
- Slides 2-3: Background slides (if you don't need two slides, use 1) - Include a VERY small amount of background material – just enough to let us understand the major clinical issues involved well enough to evaluate your results. Most students err here on the side of providing too much information. This project presentation should focus on the methodological issues. This shouldn't be more than 1  minute.
- Slide 4: A slide for the research question and population of interest
- Slide 5: A slide for data source, exposure and outcome definitions – the slides should clearly state the source of data (perhaps with the description of the population), the definition of the exposure and the key outcome you will focus on (with details as needed so we understand what we're looking at) and specifically including the number of patients in each exposure group prior to matching
- Slide 6: A slide to list the covariates in groups, explaining why you chose what you did, without reading a long list to us. You should be able to explain each of the measures involved if asked, but don't read the list to us – just have it, and be able to tell us how many variables were in your propensity model. It's helpful to group the covariates by type rather than, say, alphabetically. You should also be able to indicate which variables (if any) you had to impute, and what approaches of those I provided (or others, if applicable) that you used to do that imputation.
- Slide 7: A slide to describe the analyses you did – matching (including how many matches you made, and whether you did anything other than 1:1 greedy matching) and then your second analysis – as discussed earlier.
    - Suppose you run a 1:1 propensity match WITH REPLACEMENT. You should want to know a. how many treated subjects are in your matched sample and b. how many control subjects are in your matched sample. If you run a match with `match_with_replacement <- Match(Y, Tr, X, M=1)` then these answers come from `n_distinct(match_with_replacement$index.treated)` and `n_distinct(match_with_replacement$index.control)`, respectively. This method works for any match obtained using the `Matching` package. Those of you matching in any way other than 1:1 without replacement, get this summary pair of counts into your report.
- Slide 8: A slide to indicate how you fit the propensity score (i.e. propensity to be in which group?) and its results – specifically, how many covariates did you include, what was the minimum and maximum propensity score within each exposure group (so we can see that they're not too close to 0 or 1), and perhaps a density plot to compare the propensity scores.
- Slide 9: A Love plot to describe covariate balance in terms of standardized differences before and after matching.
- Slide 10: An assessment/table of Rubin's Rules before and after matching. No need to show the Rubin's Rule 3 plot or the variance ratio plot – you can just summarize important details.
- Slide 11: A slide describing the primary outcome result after matching – showing the estimated causal effect (perhaps an odds ratio, hazard rate or risk difference, or whatever) properly labeled, explained in detail, and accompanied by a 95\% confidence interval, and a comparison to the original (unadjusted) estimate and confidence interval.
- Slides 12: A slide describing what sort of weighted analysis you did and how it worked out in terms of improving covariate balance and reducing selection bias (if this is weighting alone, for instance, highlights of an assessment of balance after weighting would probably just take one slide)
- Slide 13: A slide describing the primary outcome result after your second propensity-based analysis – showing the estimated causal effect (perhaps an odds ratio, hazard rate or risk difference, or whatever) properly labeled, explained in detail, and accompanied by a 95% confidence interval, and a comparison to both the matched and the original (unadjusted) estimates and confidence intervals. You should be prepared to indicate which analysis is more appropriate in your view, on the basis of the quality of balance achieved, mostly.
- Slide 14: If your 1:1 matched analysis was statistically significant, you should present a sensitivity analysis, with a gamma estimate, in terms of an actual sentence or two in English. If it wasn't, you should present some thoughts on potential stability analyses.
- Slide 15: A slide with clinical conclusions, focusing on the primary outcome.
- Slide 16: A slide with statistical conclusions – additional methodological considerations. What do you know now that you wish you knew at the beginning, or that you think might be useful to others, or that you think might be useful to you after much of the class has faded into memory?

### Evaluating the Project Presentations

All students must attend all presentations (you will be providing both oral and written feedback to your colleagues). A sampling of the questions I have used in past evaluation sheets with this class follows.

- (Open Response) What was the most important thing you learned from this presentation?
- (Open Response) What was the muddiest, most confusing part of this presentation?
- (Likert scales 6 = Strongly Agree to 1 = Strongly disagree)
    - The research question(s) were stated clearly and motivated by the introduction.
    - The speaker motivated their choices about study design well.
    - The speaker developed reasonable solutions to analytic problems.
    - The speaker focused on important issues in the presentation.
    - I believe the speaker's conclusions.
    - This presentation was informative and left me with "take away" value.
- (Open Response) Make your best suggestion to improve this presentation, or study.

I am open to suggestions about other questions that might be useful. Just send them along. Thanks.

## The Final Set of Deliverables (due May 6 at NOON)

Submit via canvas.case.edu your final project materials by NOON on May 6. This will include five key items:

1. An updated **Abstract** with any necessary corrections to the one submitted previously (if there are no changes, please submit this anyway and indicate that you have made no changes.)
2. Updated **Slides** with necessary corrections or amplifications to that presented in class (again, if there are no changes, please submit this anyway and indicate that you have made no changes.)
3. A copy of the **Data Set** (as a .csv file) or, if that is impossible, a dummy data set containing all variables used in your analyses, and a single, representative (though possibly disguised) row of data,
4. a well-annotated **R Markdown** file that takes your submitted data set and flawlessly produces a document containing all of the analyses described in your abstract, slides or discussion, and
5. an **HTML version** of the results of running your Markdown file.

Note that your Markdown/HTML file should produce a readable discussion of your entire project.

- This discussion should describe both your analyses and conclusions in a larger context and describe implications of your current work, and potential future work, likely in more detail than you will be able to provide in your presentation. 
- Include a paragraph (or more) at the end of this discussion specifying what you learned from doing this project, and what you still need to learn in order to complete your study to your satisfaction.
- You may incorporate as many figures as are crucial in your discussion, but edit your Markdown file to only produce the plots and output you intend to comment on, certainly including anything that is included in your Abstract or Slides, but also potentially including other things that did not make it into those pieces. 
- Frank Harrell's [Manuscript Checklist of Statistical Problems to Detect and Avoid](http://biostat.mc.vanderbilt.edu/wiki/Main/ManuscriptChecklist) may be helpful.
