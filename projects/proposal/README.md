# Task 1: The Project Proposal

## Submission

The Proposal is submitted through canvas.case.edu at any time in the month of February and must be approved by March 1.

## Contents

Your proposal will be a summary (moving towards an abstract) of your proposed study, and must include:

1. A good, interesting title. You will work hard on this: please don't call it "Observational Studies Project."  A vast majority of your intended audience will never get past the title and abstract of the final report. Get off to a good start. Avoid deadwood like "The Study of..." or "An Analysis of..."
2. Your name and the names of any co-investigators (in which case you should indicate their role in this work.)
3. No more than a paragraph (and, perhaps, one figure) of background information, meant to help me understand the study's objective. Use words I know.
4. An objective or list of study objectives, which leads directly to the research question.
    - Be sure you specify the population, key outcome(s), and exposure/treatment (as well as, perhaps, some of the covariates of interest) in developing your objective.
    - This is a **SMALL** study. Do not boil the ocean.
5. A careful statement of the research question(s), with indications about anticipated directions for any hypotheses. 
    - Please state research questions as questions.
6. A classification of the type of research design (i.e. prospective cohort, etc.)
7. A description of the setting in which the data were collected (i.e. MHMC burn unit)
8. A brief description of the participants, including key inclusion or exclusion criteria, as well as the size and style of the sample (i.e. 200 consecutive male patients between November and May with burns over more than 15% of their bodies)
9. A brief description of the intervention or exposure of interest
10. A description of the exposure's method of allocation to participants
11. A listing of primary outcome measures, which should be clearly linked to the objectives.
    - Be sure to indicate clearly why these outcome measures are important. Do not assume that I know.
    - Also, please indicate clearly how these outcome measures will be obtained and (one hopes) validated.
12. A paragraph or two describing the available data set, and confirming that you either have it or describing why you will certainly be able to get it well before the April 1 deadline.
13. A paragraph or two describing your planned statistical methodology for answering your research questions. Obviously, you won't have developed a complete tool set here, but do the best you can. Here is a sample recipe for this last piece:
    - Statistical Methods: Appropriate graphical and numerical data summaries across *the exposure groups*, followed by propensity score matching and weighting methods to address selection bias. For outcomes analysis, our primary tool will be *primary tool* on propensity-matched pairs, as well as unadjusted and propensity-weighted comparisons of *the exposure groups* on *our primary outcome*.
    - Note that you'll need to insert the information *in italics* yourself, including the specific exposure groups you're comparing and your primary outcome measure. In most cases your primary tool is determined by the type of outcome you are working with, as follows:
        - If your primary outcome is continuous, your primary tool will usually be linear regression.
        - If your primary outcome is binary (yes/no), your primary tool will usually be logistic regression. 
        - If your primary outcome is time-to-event, your primary tool will usually be Cox regression.

That should be sufficient for this first draft. You'll need to fill in additional details by the time you submit the revised abstract later in the semester. If you've written three pages or more, go back and edit until you're down to about two pages. Your eventual abstract will also include results and conclusions, but we're not there yet. All materials for the project should be submitted through canvas.case.edu

## Frequently Asked Questions about the Proposal

1. I want to run a project idea past you prior to doing a formal proposal. What information do you need to see immediately to understand whether or not a more complete proposal is likely to be successful?
    - There are four things I will need, at a minimum. 
        - What is the exposure - what are the two groups of patients you intend to compare, and how many patients are in each of those groups (it's also helpful to tell me where the patients come from, and how they're selected to be in the study.)
        - What is the primary outcome you wish to compare them on, and how is that variable measured? Hearing about secondary outcomes is also helpful, but you should limit yourself to no more than two outcomes, total, in this study.
        - What is the nature of the covariate information - what variables do you have, specifically, that you propose to include in your Table 1 comparing the two groups, and in the propensity model? Are they all measured PRIOR to the decision to apply or not apply the exposure of interest to patients?
        - Do you have the data in hand? What are the steps that need to happen to get the data in hand? Are there any IRB/HIPAA concerns worth mentioning at this point?
        
2. What are the characteristics of a data set that makes it highly appropriate for this project?
    - You have the data, and can prove to me that you can present it to the class without drawing the ire of any regulatory body or review board.
    - You know how the data were gathered, and can investigate problems in the data yourself. You are capable of cleaning and managing the entire data set that you plan to use, yourself.
    - The data have not previously been analyzed using propensity scores, though it is possible that you have new data and wish to partially replicate an existing study.
    - The data compares two groups of subjects, some of whom received an exposure of interest and some of whom did not (or received an alternative exposure) for reasons that are not directly related to a random allocation.
    - There are multiple covariates which can help explain why the subjects did or did not receive the exposure of interest.
    - There is at least one well-measured outcome of interest, which you believe to be both important to learn about and to potentially be causally linked to the exposure, usually on the basis of both a logical argument, some (biological or other) theory and some prior empirical evidence.
    - You have sufficient numbers of subjects and covariates for propensity score methodology to be plausible. On some level, the more observations you have, the better, but not if you're still collecting or cleaning the data. If you have more than a half-dozen covariates you wish to include in the propensity score, and have at least 100 patients in the smaller of your two exposure groups, I am not likely to be especially concerned about the size of your data set. If you cannot meet these standards with a data set in which you have a serious interest, contact me to discuss the matter, soon.

3. Will you help me find a data set to use?
    - That's your job. I will happily help you decide whether a particular observational study is likely to work well for this project, but I am not going to find data for you.

4. I have multiple outcomes I'm interested in - it's hard to pick a primary one in advance - will I have time to look at multiple outcomes in the presentation?}
    - You'll likely run models looking at multiple outcomes - expect to wind up only presenting some of those outcomes, and perhaps only one in detail, for the class. But there's no reason to settle on which one you'll present in advance if all of the data are easily available. If you have all of the data, you can easily re-run things with a series of different outcomes once you've set up the main propensity analyses.

5. I have some variables which will have missing data. What should I do?
    - It depends, to some degree, on how much missingness you actually have. Let me know about the missingness as soon as you do, and we can discuss it.
    - Specifically for the projects (this isn't to be interpreted as globally accurate advice), I often suggest that the problem is modest in a covariate if the missingness affects less than 20 observations total, and also less than 10\% of the total sample size. Outcome or exposure missingness is a bigger problem, and it is often necessary to drop those cases from the data set. 

6. I have some variables which I could code in several ways - for instance, I could code as "yes/no" for meeting a standard or I could code as "low/middle/high" in terms of severity or I could code as the continuous measured value? Which should I do?
    - Always code everything in the least collapsed way possible at the start of building a data set. 
    - You definitely want to build your data set using the data in the least aggregated (most granular) manner possible. It is always easy to collapse categories (taking low/middle/high to low vs not low, for instance) but it is always hard to expand them (taking low vs. not low to low/middle/high). 
    - If any of your categorical variables are based on a continuous variable that you have also measured, then you should definitely include the continuous variable in your data set either instead of or along with the categorized version. Again, you can always get the categories again if you need them from the continuous results, but you can't go the other way. 
