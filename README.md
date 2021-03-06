# What is satisfaction for a programmer?
## Analyzing Stack Overflow's annual Developer Surveys

![Developer Salary by Overpaid feeling, 2017](pics/job_satisfaction_language_2020_v2.png)

All the surveys data can be downloaded here:
https://insights.stackoverflow.com/survey

For this research I've used data sets from the following years: 2017, 2018, 2019 and 2020.

## Table of Contents
1. [Introduction](https://github.com/abitfrosty/Stack_Overflow_Surveys#introduction)
2. [Objective](https://github.com/abitfrosty/Stack_Overflow_Surveys#objective)
3. [Installations](https://github.com/abitfrosty/Stack_Overflow_Surveys#installations)
4. [CRISP-DM](https://github.com/abitfrosty/Stack_Overflow_Surveys#crisp-dm-methodology-analysis)
	1. [Business understanding](https://github.com/abitfrosty/Stack_Overflow_Surveys#1-business-understanding)
	2. [Data understanding](https://github.com/abitfrosty/Stack_Overflow_Surveys#2-data-understanding)
	3. [Data preparation](https://github.com/abitfrosty/Stack_Overflow_Surveys#3-data-preparation)
	4. [Modeling](https://github.com/abitfrosty/Stack_Overflow_Surveys#4-modeling)
	5. [Evaluation](https://github.com/abitfrosty/Stack_Overflow_Surveys#5-evaluation)
	6. [Deployment](https://github.com/abitfrosty/Stack_Overflow_Surveys#6-deployment)
5. [File Description](https://github.com/abitfrosty/Stack_Overflow_Surveys#file-description)
6. [Results](https://github.com/abitfrosty/Stack_Overflow_Surveys#results)
7. [Licensing, Authors, and Acknowledgements](https://github.com/abitfrosty/Stack_Overflow_Surveys#licensing-authors-acknowledgements)

### Introduction
I have analyzed annual developers surveys. Each row in the data provides information about the programmer. I've used the data to visualize salary and how they feel about it in terms of being overpaid or underpaid, job and career satisfaction of the developers that use different programming languages, compared popularity of different languages on an absolute and percentage scale.

### Objective
To explore and find out correlation between popular or unpopular programming languages and satisfaction for developers that use them.

### Installations
1. Python 3.+
2. Required libraries that can be installed via "pip install": pandas, matplotlib, numpy, scipy
3. This comes with archives that need to be unzipped in the same git folder under the archive name.
	- developer_survey_2017.zip > developer_survey_2017
	- developer_survey_2018.zip > developer_survey_2018
	- developer_survey_2019.zip > developer_survey_2019
	- developer_survey_2020.zip > developer_survey_2020
	
*Alternatively all these data sets can be downloaded from the link at the top.*

### CRISP-DM methodology analysis (CRISP-DM stands for cross-industry process for data mining. The CRISP-DM methodology provides a structured approach to planning a data mining project.)
#### 1. Business understanding
	- Idea of this research is to provide the main aspects on developers' satisfaction for the organization. Why is this important? Because then the organization can be more succesful in hiring more qualified developer or less paid developer who prefers to downshift to a comfortable company for him.
	- Assumptions:
		1. Unpopular languages tend to be more satisfying, is it true?
		2. Overall satisfaction in programming languages does not change, is it true?
	- Questions to be answered:
		1. Underpaid/overpaid feeling and what are the break points in salary?
		2. How rare is 50,000, 100,000 or 150,000 USD salary among developers?
		3. Which language was the most popular in 2017, 2018, 2019, 2020?
		4. Which language had the best ratio of satisfaction/unsatisfaction in 2017, 2018, 2019, 2020?
	
#### 2. Data understanding
	- The data is distributed over 4 files each containing survey questions for the certain year.
	- Every survey data contains information about developer's age, gender, education, country, languages worked with, job and career satisfaction, years of coding, organization etc.
	- These columns in the datasets will be used for the analysis:
		- JobSatisfaction: Job satisfaction rating
		- CareerSatisfaction: Career satisfaction rating
		- HaveWorkedLanguage: Which of the following languages have you done extensive development work in over the past year, and which do you want to work in over the next year?
		- Overpaid: Compared to your estimate of your own market value, do you think you are...?
		- Salary: What is your current annual base salary, before taxes, and excluding bonuses, grants, or other compensation?
	- Exploration of the data:
		1. Survey 2017 shape: (51392, 154)
			- "Salary" NULL values: 38501, to total: 74.92%
				- "Salary" "0" values: 6, to total: 0.01%
			- "Overpaid" NULL values: 38005, to total: 73.95%
				- "Overpaid" NULL but "Salary" !NULL: 33, to total: 0.06%
				- "Salary" NULL but "Overpaid" !NULL: 529, to total: 1.03%
			- "JobSatisfaction" NULL values: 11016, to total: 21.44%
				- "JobSatisfaction" NULL but CareerSatisfaction !NULL: 2343, to total: 4.56%
			- "CareerSatisfaction" NULL values: 8697, to total: 16.92%
				- "CareerSatisfaction" NULL but JobSatisfaction !NULL: 24, to total: 0.05%
			- "HaveWorkedLanguage" NULL values: 14767, to total: 28.73%

		2. Survey 2018 shape: (98855, 129)
			- "Salary" NULL values: 48277, to total: 48.84%
				- "Salary" "0" values: 1121, to total: 1.13%
			- "JobSatisfaction" NULL values: 29579, to total: 29.92%
				- "JobSatisfaction" NULL but CareerSatisfaction !NULL: 7228, to total: 7.31%
			- "CareerSatisfaction" NULL values: 22351, to total: 22.61%
				- "CareerSatisfaction" NULL but JobSatisfaction !NULL: 0, to total: 0.00%
			- "LanguageWorkedWith" NULL values: 20521, to total: 20.76%

		3. Survey 2019 shape: (88883, 85)
			- "JobSat" NULL values: 17895, to total: 20.13%
				- "JobSat" NULL but CareerSat !NULL: 1859, to total: 2.09%
			- "CareerSat" NULL values: 16036, to total: 18.04%
				- "CareerSat" NULL but JobSat !NULL: 0, to total: 0.00%
			- "LanguageWorkedWith" NULL values: 1314, to total: 1.48%

		4. Survey 2020 shape: (64461, 61)
			- "JobSat" NULL values: 19267, to total: 29.89%
			- "LanguageWorkedWith" NULL values: 7083, to total: 10.99%
	
#### 3. Data preparation
	1. "Salary":
		- Will investigate further how absense of salary correlated to any column and if there is any correlation.
		- Also I will keep "0" salary values as is as I'm not sure if it's a missing value or some kind of probation.
		- If "Salary" is missing but "Overpaid" isn't missing I will fill with median.
	2. "Overpaid":
		- Missing values will fill as "Not sure" so they will be kept in the analysis.
	3. "JobSatisfaction":
		- Missing values will fill with "CareerSatisfaction" as they are highly correlated.
	4. "CareerSatisfaction":
		- Missing values will fill with "JobSatisfaction" as they are correlated.
	5. "LanguageWorkedWith":
		- Missing values will be dropped as I'm not predicting which language developer used recently.
		- 'HTML/CSS': 
			- In 2017 wasn't present and will not be included in 2020 to 2017 plot.
			- In 2018, 2019 was present as one answer, so will be included in 2020 to 2018 and 2020 to 2019 plots.
			- In 2020 became split different languages, so will be processed as mean value of HTML+CSS.
		- 'Bash/Shell/PowerShell':
			- In 2017 wasn't present and will not be included in 2020 to 2017 plot.
			- In 2018 was present as 'Bash/Shell', so will be renamed to match the same name.
		- 'TypeScript':
			In 2018 wasn't present and will not be included in 2020 to 2018 plot.
	
#### 4. Modeling
	- The question does not require machine learning.
	- For visualization I'm using bar plots, scatter plots, line plots.
![Programming Language Popularity vs Satisfaction, 2017](pics/language_popularity_vs_satisfaction_2017_v2.png)
![Programming Language Popularity vs Satisfaction KDE, 2017](pics/language_satisfaction_kde_2017_v2.png)

#### 5. Evaluation
	- Statistical methods used: 
		- ??omparison method.
		- Regression line.
		- KDE (Kernel Density Estimation) with medians.
		- R-value (Rs), Pearson's correlation coefficient.
		- R-value (Rs), p-value, Spearman's correlation coefficient and probability.
	
The correlation's (Rs) strength
|R-value (positive or negative)|Meaning|
|-|-|
|0.00 - 0.19|A very weak correlation|
|0.20 to 0.39|A weak correlation|
|0.40 to 0.69|A moderate correlation|
|0.70 to 0.89|A strong correlation|
|0.90 to 1.00|A very strong correlation|

P-value of 0.05 (5%) or less is considered statistically significant and states the strong evidence for rejecting the H0 null hypothesis.
|P-value|P-value, %|Evidence for rejecting H0|
|-|-|-|
|More than 0.1|>10%|Very weak to none|
|Between 0.1 - 0.05|10%-5%|Weak|
|Between 0.05 - 0.01|5%-1%|Strong|
|Less than 0.01|<1%|Very strong|

For example, the H0 (null hypothesis) states that there's no correlation between programming language popularity and developer's satisfaction in 2017 year data.
But analyzing 2 previous charts in [Modeling](https://github.com/abitfrosty/Stack_Overflow_Surveys#Modeling) step with such properties:
	- Pearson correlation coefficient (blue): 0.492
	- SpearmanrResult(correlation=0.5360195360195361, pvalue=0.003953395285996525)

*Blue are unpopular languages, red are popular languages*

We can reject the H0 hypothesis based on a moderate correlation value (~**0.49** Pearson's Rs and ~**0.54** Spearman's Rs) and very low p-value of ~**0.004** that states this correlation isn't due to a chance. And accept alternative hypothesis that says there is a moderate positive linear correlation between programming language popularity and developer's satisfaction in 2017 year data.

#### 6. Deployment

##### Final conclusion on programming language satisfaction:
		1. Unpopular languages tend to be more satisfying, is it true?
			- No. The correlation was found in 2017 and 2018 but not in 2019 and 2020.
		2. Overall satisfaction in programming languages does not change, is it true?
			- No. There is a falling trend in languages' satisfaction that occurs not only in popular languages but in whole.
	- Questions to be answered:
		1. Underpaid/overpaid feeling and what are the break points in salary?
			- Underpaid: 35,000, 55,000, 75,000, 110,000.
			- Overpaid: 55,000, 85,000, 110,000.
		2. How rare is 50,000, 100,000 or 150,000 USD salary among developers?
			- Salary of 50,000 is around the 50th percentile.
			- Salary of 100,000 is around the 90th percentile.
			- Salary of 150,000 is around the 99th percentile.
		3. Which language was the most popular in 2017, 2018, 2019, 2020?
			- JavaScript is the most popular and the most satisfying programming language in the analysis of 2017, 2018, 2019 and 2020 years surveys.
		4. Which language had the best ratio of satisfaction/unsatisfaction in 2017, 2018, 2019, 2020?
			Smalltalk in 2017, Groovy in 2018, Ruby in 2019, R in 2020.

### File Description
In this repository you can find zipped archives with .CSV files which is the datasets used in the analysis and a .ipynb files which is a jupyter notebook files that contain the code for analysis.
The are 2 .ipynb files:
1. Exploration - exploration of the dataset.
2. Project - the main part of the analysis.

### Results
All the assumptions and questions both were answered and visualized in the notebook.

The main findings of the code can be found at the post available here: https://abitfrosty.medium.com/what-is-satisfaction-for-a-programmer-aec644b29476

### Licensing, Authors, Acknowledgements
Must give credit to https://github.com/abitfrosty.
