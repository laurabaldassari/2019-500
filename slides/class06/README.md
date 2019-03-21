# 500 Class 06: 2019-03-21

- Slides for Class 6 are now available, above, in R Markdown and in PDF. 
- We will also post the audio recording, above, as soon as we can.

## After Class Update

I repaired several things we'd caught during class, and some things we hadn't in the [Right Heart Catheterization Case Study](https://github.com/THOMASELOVE/2019-500/tree/master/data-and-code/rhc_2019). I've explained the changes [here](https://github.com/THOMASELOVE/2019-500/tree/master/data-and-code/rhc_2019). We'll review the changes in Class 7.

## Today's Agenda

1. Project Details and Presentation of the 11 studies not yet discussed
2. Some Project Tips
3. Discussion of Rosenbaum Chapters 7-8 (Elaborate Theories and Quasi-Experimental Devices)
4. Discussion of [Homework 3](https://github.com/THOMASELOVE/2019-500/tree/master/assignments/homework3)
5. The [Right Heart Catheterization Case Study](https://github.com/THOMASELOVE/2019-500/tree/master/data-and-code/rhc_2019)

## Small Items

- In the **toy** example, we had an error in section 4.3 (just a typo), as part of the Task 1 for Outcome 3. This is now corrected, and you can find the revised documents as follows:
    - The code and script file written in R Markdown: [toy_2019_analysis.Rmd](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/toy_example/toy_2019_analysis.Rmd)
    - [PDF output for toy_2019_analysis](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/toy_example/toy_2019_analysis.pdf), HTML version [most easily viewed on RPubs](http://rpubs.com/TELOVE/toy_2019_analysis), and [Github Markdown version](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/toy_example/toy_2019_analysis.md).

## EpiBookClub meets at 2:30 today in Wood WG 82-C

- This week we will be discussing the last two chapters of Healy's Data Viz book - Chapter 7 (Maps) and Chapter 8 (Refining Your Plots).
- If you have any plots or graphs you'd like to share with the group (plus R code), please bring them and we can put them on the big screen.
- Think about what we should do with this club next - the book will be over with but hopefully our meetings will not be. Wyatt and I would like to continue meeting.


## Project Details

The spreadsheet at http://bit.ly/500-2019-project-list contains information on each approved project proposal. 

- Please take a look at the title, data source, outcome and type of outcome, exposure, and covariate information I have listed there, and ensure that it matches your understanding of what I've approved. If it does not, please let me know by the end of class today, in person.

In today's class, we'll hear from the authors of the projects not yet discussed in class, which are:

1. Kelly Steller "Fruit and Vegetable Intake and Body Mass Index in Adult U.S. Men and Women"
2. Hyun Jo Kim "The other side of beta blockers that doctors don't want you to know"
3. Julijana Conic "Length of survival in mitral valve repair for ischemic mitral regurgitation"
4. Yousef Mustafa "Diabetes and Blood Pressure Status in NHANES 2015-16 Subjects"
5. Laura Cremer "Is Marijuana a gateway drug?"
6. Sebastian Garcia-Medina "The influence of Marijuana consumption on sleeping habits"
7. Brian Richardson "Topology of the stomach: The effects of tumor location on gastric cancer progression"
8. Harry Persaud "Does fasting improve low-density lipoprotein and blood glucose? A re-analysis of de Toledo et al."
9. Zhanwen Du "Effect of baseline diabetes on postoperative in hospital complications"
10. Jordan Fiegl "Understanding Challenges of Primary Care for Medicaid Patients"
11. Michael King "Understanding the Impact of Physically Demanding Jobs on Sleep"

Each of these people will tell us just a little bit about their data source, outcome and treatment/exposure, and why they are studying this issue.

## Some Project Tips (in addition to [these tips shared previously](https://github.com/THOMASELOVE/2019-500/blob/master/projects/tips.md))

1. If your project has roughly equal numbers of "exposed" and "control" subjects, you will run into a problem if you try to do 1:1 matching without replacement, in that your results will be virtually unchanged. You have the following alternatives available to you:
    - Match 1:1 with replacement (which may still have only a small impact, depending on how you do it)
    - Match 1:k with replacement, where k > 1 (which may or may not useful)
    - Match 1:1 without replacement, but only on a random sample of (perhaps 1/3 of) your "exposed" subjects.
    - For more on matching, you probably want to look at the [Right Heart Catheterization](https://github.com/THOMASELOVE/2019-500/tree/master/data-and-code/rhc_2019) case study that we'll discuss today.
2. If you have more than 4000 observations in total, I suggest sampling down (without replacement) to 3000 (at most) to develop your project. You should do this with code near the start of your R Markdown file, that can be tweaked as necessary, either to take a different sample, or not sample at all.
    - If you're going to sample down like this, I recommend you maintain the rate of exposure that you see in the data as a whole, unless that rate is close to 50%, in which case I suggest you sample down to a rate that is 25-35% exposed and the rest unexposed, so that 1:1 matching without replacement will be more likely to produce useful results.
3. The definition of which group is the "exposed" group and which is the "control" group matters analytically, although it's essentially an arbitrary selection. You will make your life easier for our purposes in developing the project by making your "exposed" group the smaller of the two groups, if possible.

## Explorable Multiverse Analyses

[This is just amazing to me](https://explorablemultiverse.github.io/).

I learned about it from [Matthew Kay's twitter thread](https://twitter.com/mjskay/status/1106742607420497921)

![](https://github.com/THOMASELOVE/2019-500/blob/master/slides/class06/figures/kay-tw.PNG)


## Next Time

We'll finish the [Right Heart Catheterization example](https://github.com/THOMASELOVE/2019-500/tree/master/data-and-code/rhc_2019), and we'll also discuss: 

- the [2001 paper by Donald Rubin about the tobacco litigation](https://github.com/THOMASELOVE/2019-500/blob/master/texts/Rubin%202001%20Tobacco%20Litigation%20article.pdf) that led to Rubin's Rules 1-3, among other things, and ...
- Chapter 9 (on Sensitivity to Bias) from Rosenbaum, 
- [Homework 4](https://github.com/THOMASELOVE/2019-500/tree/master/assignments/homework4)
