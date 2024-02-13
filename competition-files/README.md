Linear Regression Mini-competition
================

In this repository/directory you should see the following items:

- `README.md` - this document.
- `mini-competition.Rmd` - an empty RMarkdown file for you to keep track
  of your explorations/work and provide detailed notes.

## The “rules”

This is a culminating experience for STA 631’s first learning module:
Linear Regression. Therefore, you must fit, assess, and interpret a (or
several) linear regression model(s) to a surprise dataset (revealed
below).

Then, **by the start of our class meeting on Tue, Feb 20** you and your
team must have created a Google Slide deck tor present your results. At
least one member from each team will provide a 5-minute maximum
presentation of these slides. This presentation can only contain three
total slides:

1.  One title slide (with only your team member’s names and presentation
    title),
2.  One slide summarizing your team’s insight(s) to the research
    question, and
3.  One slide that summarizes your team’s modeling process.

I may ask clarifying questions at the end of each presentation and we
will hopefully have time at the end to have a closing conversation. To
assist in creating slides quickly (so you can focus on the modeling
task), we will use Google Slides instead of creating [slides in
RMarkdown](https://rmarkdown.rstudio.com/lesson-11.html). Upload your
slides to the appropriate Google folder linked below before the start of
our class meeting:

- [Section 01 (4 - 5:15
  pm)](https://drive.google.com/drive/folders/1jraxLZkPZwV1CndX1UI3iQG95KrcTJoS?usp=sharing)
- [Section 02 (2:30 - 3:45
  pm)](https://drive.google.com/drive/folders/1GZp6xS7JY8TXNv9WCv-zGEF7r-vKUscM?usp=sharing)

Presentation order will be randomly determined at the start of class and
edits to your slides will not be allowed.

While this is a friendly competition, the main purpose is to share your
ideas/process and learn from your peers and their ideas/process. I
(Bradford) will determine the “best” group based *only* on your
presentation by assessing each of the following categories on a
“missing/attempted/sufficient”-scale (or 0/0.5/1 point-scale). I will be
very [stingy](https://www.merriam-webster.com/dictionary/stingy) with
awarding “1”s except for the last category.

- Clarity of your presentation (Did you seem prepared and have a plan of
  what you were going to say?),
- Soundness of your approach (Does the direction your team went make
  sense based on what we have covered in class?),
- Aesthetically pleasing presentation (Did you do something beyond the
  default output to make your presentation easy for your audience to
  view your work?), and
- Maximum of 5-minutes and title + two slides (only 0 or 1 possible).

The best group based on these categories will receive a prize/gift.

### Data

The data come from Torgo & Moniz (2018) and contain many rows of news
items and their respective social feedback from Facebook, Google+, and
LinkedIn. The data were collected between November 2015 and July 2015
over four topics: economy, Microsoft, Obama, and Palestine. Your tasks
is to create a linear model that best predicts the sentiment of the
sentiment score for a news items’ headline.

- If you are working on the posit Workbench, you can copy the dataset
  and data dictionary from `SharedProjects\STA631\mini-competition01` to
  your cloned RStudio Project. Or, you can download the items from the
  “working on your own computer” item below and then upload to your
  RStudio Project.
- If you are working on your own computer, you can download the dataset
  and data dictionary from this [Google
  Folder](https://drive.google.com/drive/folders/1lynSAS0nInotA1XLwIyfU3iqL6nqEYlM?usp=drive_link)

This is a relatively large data file and I do not recommend that you
upload this csv to your GitHub repository. If you set up your RStudio
project so that your csv file is at the following location, this should
be automatically handled for you:

`activity04-mini-competition/competition-files/data/news.csv`

If you have placed your file in a different location, edit the
`activity04-mini-competition/.gitignore` file to reflect this different
location.

If you have questions, ask.

#### Citation

Torgo, L. & Moniz, N. (2018). News Popularity in Multiple Social Media
Platforms. UCI Machine Learning Repository.
<https://doi.org/10.24432/C5H029>.

## Suggestions to get started

- What methods have we explored to assess a model’s “good-ness”? As a
  group, come up with this list and what each tells us. How will your
  team ensure you are all working with the same training dataset? Note
  that setting a seed one different computers does not produce the same
  random sample for each computer (but will within one computer). In
  [Additional Methods](#additional-methods) below, I provide some
  descriptive (i.e., not statistical inference focused) methods to check
  for “good-ness”.
- Make appropriate exploratory graphs and numerical summary tables for
  each variable and pairs of variables. Note that there are some
  qualitative variables in the dataset. Also, do you need to consider
  any potential interaction terms or polynomial terms?
- Explore if you need to do anything to ensure the reference groups
  listed in the variable description table.
- Fit your candidate models.
- Assess which of your candidates is “best”.

## Additional methods

The *ISL* text discusses some methods for checking a model’s “good-ness”
or adjusting for issues when checking the conditions for linear
regression models (i.e., Section 3.3.3). I briefly provide how to
implement or check for these *Potential Problems* (in order as presented
in the text), but remember that the text provides more detail with how
to interpret or know if these adjustments are necessary. Throughout this
section, I provide additional resources that I find useful.

You might have heard of the adjusted $R^2$, *Akaike information
criterion* (AIC), *Bayesian information criterion*, and *Mallow’s* $C_p$
model metrics before. We will explore these in more detail in Chapter 6
(Week 12).

### 1. Non-linearity of the data

If the *errors* display a pattern where linearity might be a concern,
you can transform variables to see if these “fix” this issue. Some
online documents that provide good overviews of transformations are:

- [Transformations: an
  introduction](http://fmwww.bc.edu/repec/bocode/t/transint.html) by
  Nicholas J. Cox, Durham University
- [A guide to Data
  Transformation](https://medium.com/analytics-vidhya/a-guide-to-data-transformation-9e5fa9ae1ca3)
  by Tim M. Schendzielorz
- [Lesson 9: Data
  Transformations](https://online.stat.psu.edu/stat501/lesson/9) by Penn
  State’s Department of Statistics

These would all be done in a data `mutate`-tion step (e.g., using your
`{dplyr}` skills). For example,

``` r
# add natural log transformation to existing dataset
data <- data %>%
  mutate(log_variable =  log(variable))
```

You would then use this transformed variable in your linear regression
model instead of the un-transformed variable.

### 2. Correlation of error terms

This should be an issue for these data and time-series is not an
expected topic for this course. However, for your project you might want
to extend your learning by performing a time-series analysis.

### 3. Non-constant variance of error terms

Transforming a variable (see above) could be one way to address this
issue. A more advanced method would be weighted least squares, but not
necessary for this model - another potential extending your learning
that is covered in Chapter 7.

### 4. Outliers

The `broom::augment` function contains a lot of additional metrics
related to assessing outliers. For example, the text mentions
*studentized residuals* which is the `.std.resid` column in the
resulting tibble from using this function.

You can also visually identify and highlight outliers (e.g.,
[`gghighlight::gghighlight`](https://yutannihilation.github.io/gghighlight/articles/gghighlight.html#gghighlight)
which combines a filtering flavor to point out specific values).

### 5. High leverage points

Again, the `broom::augment` function contains a lot of additional
metrics. The text mentions *leverage statistics* $h_i$ which is the
`.hat` column in the resulting tibble from using this function. You can
then use your `{dplyr}` skills to help you identify any extreme values
(e.g., see the text for how to calculate the suggested cutoff value).

This online document discusses outliers and high leverage points:

- [Lesson 9.1: Distinction Between Outliers and High Leverage
  Observations](https://online.stat.psu.edu/stat462/node/170/) by Drs
  Iain Pardoe, Laura Simon, and Derek Young of Penn State.

### 6. Collinearity

In addition to inspecting a correlation/scatterplot matrix (e.g.,
`GGally::ggpairs`), you can also compute the *variance inflation factor*
(VIF) for each predictor. To compute these values, explore
[`car::vif`](https://cran.r-project.org/web/packages/car/car.pdf#vif)
from Dr. John Fox (*emeritus*, McMaster University) *et al*.
