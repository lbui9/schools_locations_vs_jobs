# Final Project: The College Scorecard dataset

## Summary

For the final project, you will analyze the U.S. Department of Education's *College Scorecard* dataset.

Your task is to come up with an interesting question to ask about the dataset which can then be answered using:

* visualizations
* summary statistics
* either inference or modeling

The rest of these instructions describe the dataset and what should go into your report. In addition there is a checklist at end of this document that summarizes what you need to include in your report.

## About the Dataset

You  will be working with the *College Scorecard* dataset started by The Obama Administration in September 2015. Each row in this dataset contains information about a college in the USA.

The dataset is quite large (13.5 MB), and so cannot be distributed via GitHub. **You need to download the dataset and upload it** to RStudio's folder for this project. Once you have done so, it will loaded by default in the setup block of the `final_project.Rmd` file where you will write your   report (the variable name of the dataset is `college`).

Because the dataset is so large, you will find it almost impossible to open in a tab in RStudio. Please **do not** try to open the `college` dataframe in RStudio - your RStudio will freeze up. Instead, you will have to rely on a table describing all the columns in the dataset. This is called a *data dictionary*, and is available as a Google Docs spreadsheet here: <https://docs.google.com/spreadsheets/d/1YrYiJ-J9rLhs4Qf5OCvHGMyUFyMKOMtMuGmpyt47mEY/edit?usp=sharing>.

Each row in the *data dictionary tab* of the spreadsheet describes a column in the original dataset (i.e. the name of the column and a desciption of the data contained in that column).

You will have to look through the data dictionary to understand the meaning of the variables, and this should be your starting point *before* you start running an analysis on the dataset.

If you wish to take a look at the raw `college` data in table format, you should try saving just the first few rows as a new variable, and opening that in a tab in RStudio, e.g.:

```r
college_first6rows <- head(college)
```

The `college` dataset includes data on a huge range of issues, including:

* location
* demographics
* admission standards
* tuition rates
* graduation rates
* student loans
* outcomes after graduation
* ... and many more (almost 2000 different variables!)


**This is a large dataset that that contains millions of individual cells.**
**As such, there is no one right way to approach this project.**
**There are many different avenues that you can take, so have fun with it!**


## The final project report

The final project is built around asking an interesting question about the dataset.

Your project report should contain the following sections:

* Introduction
* Preprocessing
* Visualization
* Summary Statistics
* Data Analysis
* Conclusions

Please see the description of each section for guidelines. A checklist of everything that needs to be included in your report is at the end of these instructions.

### Introduction section

In this section, you should write *at least* paragraph (or more) that introduces the question that you are investigating, and explains why it is an interesting question. You also need to state what variables you will use to answer the question, and whether you will use a hypothesis test (inference) or modeling.

#### How to come up with a question...

For this project, you have to come up with a questions that you can ask about the dataset. Here is a short list of criteria that your question must meet:

1.  You question must be answerable by either inference or modeling (as you are required to apply one of these methods). In general I would recommend phrasing your question in one of the following structures:

    i. *Is there a relationship between `response_variable` and `explanatory_variable(s)`?*
  
      This question will require you to create a linear model between the continuous response variable and the explanatory variables (which should all be continuous as well, so that it is easy to assess whether the linear model's assumptions are met).
    
    ii. *Is there a difference in `test_statistic` between two categories of `explanatory_variable`?*
  
      This question will need statistical inference to answer. The `test_statistic` will either be the difference in proportions (categorical) or the difference in means (continuous) of the response variable. The explanatory variable must be categorical.
    
    Note that each of these question templates requires *two variables*.
  
    If you have taken statistics classes before, you may want to stretch yourself and ask a different type of question. Please feel free to reach out to me if you are comfortable going beyond the statistics we have covered in this class, and want to ask a question that doesn't fit into either of the structures suggested above.
  
2. Each row in the dataset is a college in the USA. Therefore **your question must be about colleges, not about students**. For example, you cannot ask "Is there a relationship between graduation rate and ethnicity of a student", because we do not have data on students. However, you could ask "Is there a relationship between the % of non-white students in a college and the graduation rate of each college?" (however, you may not use this question - I want you to come up with your own).


3. Your question should be somewhat interesting. Ask yourself, "Would a newspaper publish an article on this topic?" (In contrast, you should not just pick two random continuous variables and throw them into a linear model to see what falls out...)

**Once you have a question ready, you need to propose it to your group members:**

* In-person sections will do this in class (you will also have a group channel in Slack, and the final list of questions you generate should be posted here).
* Online sections will post and discuss their questions in a group channel in Slack.

When proposing a question you need to provide your group members the following information:

*   The question (written as a complete sentence in one of the two examples above).

*   The names of each column you need to answer the question, as well as a brief description of what that column represents and an explanation of whether each one is an explanatory or response variable and whether each is continuous or categorical.

*   Whether you would need to use a linear model or statistical inference to answer your question.

*   1-2 sentences explaining why you think it's a worthwhile question to ask.

An example of such a message (using our "bad" question from before) might be:

> I would like to ask "Is there a relationship between the % of non-white students in a college and the graduation rate of each college?". The columns that I will use are:
> * `PCT_WHITE` (the percent of white students, which will be converted into the percentage of non-white students). This is my explanatory variable.
> * *etc. for your response variable(s)*
> Since both columns are continuous variables, I will use a linear model to answer this question.
>
> I think this question is interesting because ...

**After you have proposed your own question, you need to provide feedback on your group members questions.**

You must respond to at least one question proposed by another group member with:

* If their question is missing any information, then please point this out (e.g. "You did not specify whether this should use a linear model or a hypothesis test"). You can also supply the information yourself if you wish (e.g. "Since this question has two continuous variables, I think it would need a linear model").

* If you disagree with something in their proposal, then (politely) point this out (e.g. "I think this question would need inference instead of a linear model since both variables are categorical.")

* If the question does not seem to pass one of the criteria listed above, then point this out and explain why. (And, optionally, give a suggestion as to how the question could be improved.)

* If you have something to add, then please do so! (E.g. another reason why this might be an interesting question to ask, in addition to the original one)

Once your group has added its questions to its Slack channel, then please also post a quick message in that channel stating which question you will investigate for the rest of the project. (You can pick a question proposed by anyone in your group, including yourself, and multiple people in your group can pick the same question if they wish.)

Your instructor may veto or require you to adjust any questions that do not meet the outlined criteria or that cannot be appropriately justified. Sending these messages in Slack and interacting with your group members in a timely manner **before the Milestone 1 deadline** will be counted as part of your Final Project grade.



### Preprocessing section

This dataset is structured and mostly clean, but there is still some *data preprocessing* that needs to be done before you can begin analysis.
At a minimum, there are three clear tasks to complete and document in this first section of the R Markdown file before you continue on to the **Visualization** section:

1.  After you have decided on the question you will answer, figure out which columns in the dataset you need to answer the questions.
    Then, extract those columns using `select` and save the reduced dataset to another variable, for example `college_reduced`.
    
2.  The column names are shortened abbreviations, and should be made more human-readable using the `rename` function.
    Use the data dictionary, to help you figure out what the abbreviations mean.

3.  Categorical variables that are not easy to understand, for example the integer categories under the `REGION` column, should be relabeled using the `recode` function. You can do this within the `mutate` function. Here is an example code template (you should replace variable names as appropriate):

    ```r
    df %>%
      mutate(
        recoded_column = recode(
            original_column,
            `1` = "whatever category 1 equals",
            `2` = "whatever category 2 equals",
            ...etc.
        )
      )
    ```

Additional preprocessing steps may be necessary, depending on the question you are trying to answer.
Regardless of what you do, these steps should be documented in the usual way, where each code block is accompanied by a written explanation.

**Each question in the remaining sections must be answered starting from the preprocessed dataset you end up with at the end of this section!**

> #### Important
>
> **Resist the temptation to drop any rows containing one or more `NA` values as an early step in your analysis!**
>
> This dataset contains a lot of missing (`NA`) values relative to other datasets that you've worked with during the semester.
It is important to remember that just because some information may be missing for a school doesn't mean that the other information isn't useful, and many of the `tidyverse` commands are able to gracefully handle `NA` values.
**If you need to filter out rows with `NA` values later in your analyses (e.g. for a linear model), this should be one of the last steps you do, and it should not affect the analysis and answers provided in other questions.**


### Visualization section

In this section you should conduct Exploratory Data Analysis (EDA) of the variables you are interested in. You are encouraged to reread the [Exploratory Data Analysis chapter](https://r4ds.had.co.nz/exploratory-data-analysis.html) of R for Data Science, where Hadley Wickham lists the two general goals of EDA as:

> 1. What type of variation occurs within my variables?
>
> 2. What type of covariation occurs between my variables?

I expect you to create at least 3 different graphs to investigate the two goals of EDA listed above, and at least one of the graphs must use faceting. Exactly what graphs you create will depend on what type of variables you have. You may decide to visualize more variables than the ones that you will be using in your model or hypothesis test, if you wish to investigate how those additional variables might confound or influence your later analyses

Here are some types of graphs that you might want to plot to investigate the first goal (variation within each variable):

* *Histograms*: visualize the distribution of a continuous variable. Can use `fill` parameter to break down by a secondary categorical variable (in which case you should also use the `position = "identity"` and `alpha` parameters). Make sure to adjust either `bins` or `binwidth` suitably.

* *Density plot*: a smoothed line version of a histogram.

* *Box plot*: also visualizes the distribution of a continuous variable, along with summary statistics (such as median and IQR). Use the `x` parameter (along with the `reorder` function to break down by a secondary categorical variable).

* *Violin plot*: much like a box plot, but shows the density as well (by varying the width of the box). Use `geom_violin` instead of `geom_boxplot`, but arguments supplied to the geom functions are essentially the same.

* *Scatter plot*: for visualizing the relationship between 2 continuous variables. Can use `color` parameter to break down by a secondary categorical variable.

* *Bar plot*: for visualizing the distribution of a categorical variable (essentially the categorical equivalent of a histogram - the height of each bar is the count of rows in each category). Can use `fill` parameter to break down by a secondary categorical variable.

For the second goal (covariation between variables), refer to the *R for Data Science* book for examples of graphs to use for combinations of different types of variables:

* A (categorical and a continuous)[https://r4ds.had.co.nz/exploratory-data-analysis.html#cat-cont] variable

* (Two categorical)[https://r4ds.had.co.nz/exploratory-data-analysis.html#two-categorical-variables] variables

* (Two continuous)[https://r4ds.had.co.nz/exploratory-data-analysis.html#two-continuous-variables] variables


Here are some additional points to bear in mind:

* You need at least 3 distinctly different graphs (i.e. different variables or different geom_function), but you are encouraged to make more. This is your chance to impress me with how much you have learned.

* The graphs must be relevant to your question of interest!

* At least one of these graphs should facet over a categorical variable (using `facet_wrap` or `facet_grid`). Depending on your question of interest (see previous point...), there are a number of ways you could satisfy this requirement:

  * `pivot_longer()` multiple original columns into _name_ and _value_ columns, and facet over the categorical key column.
  
  * Facet over a categorical variable that you are already using in your analysis.
  
  * Pick a new categorical variable that you think might affect your data, and facet over that.

* Every graph should be properly labeled (titles and axes).

* Each graph should be preceded by a sentence or two of text stating *why* you are creating this graph.

* Each graph should be followed by a short description of the patterns that you observe in the graph. For example:

  * If a type of plot showing the variance of a variable (e.g. a histogram), describe the variance (center, shape, patterns, outliers, etc.). 
  * If a type of plot showing the covariance between multiple variables, describe any patterns or relationships. How strong are these? What other variables might influence these patterns? 
  * If you have broken the graph down by another categorical variable (using `fill`, `color`, or faceting), describe how the variation is different between these different subsets of the data.



### Summary Statistics section

You should calculate the summary statistics for each of the main variables that you will be including in your *Data Analysis* section. Most people will have two variables, if they followed the question structure suggested in the *Introduction* instructions above.

For each categorical variable:

* `group_by` itself

* Within the `summarize` function, calculate the count of rows in each category (use the `n()` function).

For each continuous variable:

* `group_by` a categorical variable, if you have one. (If you are analyzing two continuous variables only, there is no need to group by anything.)

* Using `summarize` calculate: the count of observations (use the `n()` function), mean, median, range, standard deviation, and interquartile range (use the `IQR()` function) of this continuous variable.



### Data Analysis section

In this question, you need to answer your question using either modeling or inference. Your analysis code also needs to be documented using plain text descriptions that explain what each code block does, and interprets the output.

You should be modeling if your question is asking whether a continuous response variable is linearly related to one or more explanatory variables. For example, "is a person's height related to their arm span?"

You should be using a hypothesis test if you question is asking whether there is a statistically significant difference (compared to random variation) in the reponse variable between two categories of a categorical explanatory variable. For example, "is there a statistically significant difference in height between short-armed and long-armed people?"

#### If you are modeling...

In this project we are modeling for explanation and understanding, not prediction (so we do NOT need to worry about any predictive modeling steps such as splitting our data up into test and train sets, or cross validating, or measuring predictive accuracy.)

If you are modeling, your Data Analysis section should do the following:

* Create a linear model using `lm(...)`

* Report the model coefficients and the model's performance using `tidy` and `glance`, and include a short written discussion of what these numbers mean for your model.

* Assess how well the assumptions of the linear model are met in your situation, using:

  * observed vs. predicted plot
  
  * residual vs. predicted plot
  
  * Q-Q plot

  and follow these with a short written discussion of what these plots imply for the 3 assumptions.

#### If you perfoming inference (i.e. a hypothesis test)...

If you are doing inference, your Data Analysis section should do the following:

* State your null *and* alternative hypotheses at the start of this section (in text, not code).

* State whether you are performing a one-sided or two-sided test. (You should probably be using a two-sided test.)

* State what the test statistic is.

* Use the `infer` package to test these hypothesis by following the workflow we have used in the assignments:

  * Calculate the observed test statistic (i.e. the actual difference in the response variable between the two categories of the explanatory variable)
  
  * Create a null distribution by running 10,000 permutations of the original data.
  
  * Calculate the p-value.
  
  * Visualize the p-value using the `visualize` and `shade_p_value` functions.
  
  * Finally, write down whether you can reject your null hypothesis or not, and what this means for your original *question of interest*.


### Conclusions section

In this section you should write 1-2 paragraphs summarizing your findings from all the previous sections (i.e. visualizations, summary statistics, and data analysis), and answering your original question of interest. Here are some things to think about as you are writing your conclusion:

- what conclusion(s) can you draw from these analyses?

- how would you answer your original question of interest?

- do the analyses from these difference sections support each other, or conflict with each other?

- are there any potentially confounding factors? (E.g. were there variables that looked important in your exploratory data analysis that you did not include in your model/hypothesis test?)

- what does your finding imply for society? (I.e. why was this an interesting question to study in the first place?)

Feel free to discuss other things that you think might be relevant to your analyses!


> #### Important
>
> Below are two common misconceptions regarding this dataset that you should be aware of as you analyze your data and draw conclusions:
>
> *   **It is not possible to make statements about individual students using this dataset!**
>    
>     Each observation (row) in the dataset is a single college/university and the variables (columns) frequently represent **aggregated information** about students.
    This means that many of the columns are often an average, sum, or a percentile for the entire student body or a specific subgroup of students.
>
> *   **It is not possible to extract data about a subgroup of students from a column that was aggregated over the entire student body.**
>
>     As an example, if one column is "median salary 5 years after gradution" and another column is "percentage of students majoring in data science", you cannot use these two columns to figure out the median salary for students graduating with a data science degree.
    In general, the only way to make statements about different groups is if the column itself mentions that the quantity is aggregated over a specific subgroup.


## Additional guidelines

The following are additional guidelines for your Final Project submission:

*   You should use the `tidyverse` functions in your work (particularly the ones in the lecture slides or the textbook), and not "base R" functions (`subset`, for example).
    
*   Your R code should be clean and readable, which includes what it looks like after knitting.
    **Code blocks should not run off the side of the page when knitted to PDF!**

*   **The report's tone should be professional and should not read like a social media feed or personal blog**.
    Refrain from editorializing about the project as a whole or about a specific question, as this is not an opinion paper.
    Do not speculate, instead support your claims and explanations using data and analysis.
    Avoid self-narration or writing about how you felt or what you were thinking as you complete each question, instead write as if you are constructing a step-by-step tutorial for others to use.

*   **Late submissions for the final project will not be accepted, no exceptions.**


## Checklist

* **General**
  * Answers are written in full sentences and paragraphs.
  * Answers are clear and not garbled.
  * Tone is professional.
  * Correct spelling and grammar.
  * All graphs appropriately labelled (title and axes).
  * Code should be accompanied by written descriptions and interpretations (ask yourself "Would a random reader understand why I created this code chunk and what its code is doing?").
  * Formatting:
    * Don't display tables longer than 1 page (instead, use `head()` to show first 6 rows only).
    * Tables do not overrun right margin.
    * Code does not overrun right margin.
  * Did you change your name at the start of the document?
  * Did you sumbit a PDF on Blackboard *and* push to GitHub?
* **Introduction section**
  * Question of interest is stated.
  * Explanation of why this question is interesting.
  * State the columns you will be using to answer this question, and describe what data each variable contains.
  * State whether you will be using modeling or inference to answer your question.
* **Preprocessing section**
  * Extract the columns that you need.
  * Rename this columns more descriptively.
  * Recode any integer categorical variables.
  * Do *not* remove missing data at this stage.
  * Steps are documented with written descriptions of what each code chunk is doing.
* **Visualization section**
  * At least 3 graphs (relevant to question, and showing distinctly different information).
  * One graph must use faceting to show multiple sub-plots.
  * Each graph introduced by sentence(s) explaining why it has been created.
  * Each graph followed by an interpretation.
  * (Optional) A brief conclusion summarizing any overall patterns that you think are most relevant to your question of interest, if you found any.
* **Summary Statistics section**
  * Summary stats calculated for each of the variables identified in the Introduction section.
  * Written interpretations of the numbers you have just calculated.
* **Data Analysis section**
  * Code should be accompanied by written descriptions and interpretations.
  * If using inference:
    * State null and alternative hypotheses.
    * State whether you are using a one- or two-sided test.
    * State what you test statistic is.
    * Calculate your observed test statistic.
    * Create a null distribution.
    * Use null distribution to calculate the p-value of the observed statistic.
    * Visualize the p-value by plotting the observed statistic and the null distribution.
    * Compare the p-value to alpha, and interpret what this means for your original hypotheses.
  * If using modeling:
    * Create a linear model.
    * Report coefficients (slope(s) and intercept) and R<sup>2</sup>, and discuss what these numbers mean for your model.
    * Create 3 graphs to check the model assumptions:
      * Observed vs. predicted plot
      * Residuals vs predicted plot
      * Q-Q plot.
    * Interpret these plots.
* **Conclusions section**
  * Integrate the results from *all* previous sections in this project (aim to write at least two paragraphs).

## Grade

Grades for the final project will be based on the correctness and readability of your R code, how well your report is written (the report should be structured, coherent, and follow the standard rules of spelling and grammar), and how well you answered your question of interest using your visualizations, analysis, and written answers.


## How to submit

To submit:

1.  Commit and push your code to GitHub.

2.  Knit your Markdown document to the PDF format, export (download) the PDF file from RStudio Server, and then upload it to *Final Project* posting on Blackboard.

## Cheatsheets

You are encouraged to review and keep the following cheatsheets handy while working on the final project:

*   [Data transformation cheatsheet][data-transformation-cheatsheet]

*   [Data import cheatsheet][data-import-cheatsheet]

*   [ggplot2 cheatsheet][ggplot2-cheatsheet]

*   [RStudio cheatsheet][rstudio-cheatsheet]

*   [RMarkdown cheatsheet][rmarkdown-cheatsheet]

*   [RMarkdown reference][rmarkdown-reference]



[ggplot2-cheatsheet]:             https://github.com/rstudio/cheatsheets/raw/master/data-visualization-2.1.pdf
[rstudio-cheatsheet]:             https://github.com/rstudio/cheatsheets/raw/master/rstudio-ide.pdf
[rmarkdown-reference]:            https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf
[rmarkdown-cheatsheet]:           https://github.com/rstudio/cheatsheets/raw/master/rmarkdown-2.0.pdf
[data-import-cheatsheet]:         https://github.com/rstudio/cheatsheets/raw/master/data-import.pdf
[data-transformation-cheatsheet]: https://github.com/rstudio/cheatsheets/raw/master/data-transformation.pdf
