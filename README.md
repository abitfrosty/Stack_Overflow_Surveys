# What is satisfaction for a programmer?
## Analyzing Stack Overflow's annual Developer Surveys

All the surveys data can be downloaded here:
https://insights.stackoverflow.com/survey

For this research I've used data sets from the following years: 2017, 2018, 2019 and 2020.

# Table of Contents
1. [Introduction](https://github.com/abitfrosty/Stack_Overflow_Surveys#Introduction)
2. [Objective](https://github.com/abitfrosty/Stack_Overflow_Surveys#Objective)
3. [Installations](https://github.com/abitfrosty/Stack_Overflow_Surveys#Installations)
4. [Project Motivation](https://github.com/abitfrosty/Stack_Overflow_Surveys#Project-Motivation)
5. [File Description](https://github.com/abitfrosty/Stack_Overflow_Surveys#File-Description)
6. [Results](https://github.com/abitfrosty/Stack_Overflow_Surveys#Results)
7. [Licensing, Authors, and Acknowledgements](https://github.com/abitfrosty/Stack_Overflow_Surveys#Licensing,-Authors,-and-Acknowledgements)

# Introduction
I have analyzed annual developers surveys. Each row in the data provides information about the programmer. I've used the data to visualize salary and how they feel about it in terms of being overpaid or underpaid, job and career satisfaction of the developers that use different programming languages, compared popularity of different languages on an absolute and percentage scale.

# Objective
To explore and find out correlation between popular or unpopular programming languages and satisfaction for developers that use them.

# Installations
1. Python 3.+
2. Required libraries that can be installed via "pip install": pandas, matplotlib, numpy, scipy
3. This comes with archives that need to be unzipped in the same git folder under the archive name.
	- developer_survey_2017.zip > developer_survey_2017
	- developer_survey_2018.zip > developer_survey_2018
	- developer_survey_2019.zip > developer_survey_2019
	- developer_survey_2020.zip > developer_survey_2020
	
*Alternatively all these data sets can be downloaded from the link at the top.*

# Project Motivation
For this project, I was interestested in using developers surveys to explore:

# Assumptions:
1. Unpopular languages tend to be more satisfying, is it true?
2. There is a correlation between languge popularity and its satisfaction, is it true?
3. Overall satisfaction in programming languages does not change, is it true?

# Questions to be answered:

1. Underpaid/overpaid feeling and what are the break points in salary?
2. How rare is 50,000, 100,000 or 150,000 USD salary among developers?
3. Which language was the most popular in 2017, 2018, 2019, 2020?

# File Description
In this repository you can find zipped archives with .CSV files which is the datasets used in our analysis and a .ipynb file which is a jupyter notebook file that contains the code for analysis.

- survey_results_public.csv: The csv contains data related to developers such as:
- CareerSatisfaction: Career satisfaction rating
- JobSatisfaction: Job satisfaction rating
- Overpaid: Compared to your estimate of your own market value, do you think you are...?
- Salary: What is your current annual base salary, before taxes, and excluding bonuses, grants, or other compensation?
- HaveWorkedLanguage: Which of the following languages have you done extensive development work in over the past year, and which do you want to work in over the next year?

# Results
All the assumptions and questions both were answered and visualized in the notebook.

The main findings of the code can be found at the post available here: https://abitfrosty.medium.com/what-is-satisfaction-for-a-programmer-aec644b29476

# Licensing, Authors, Acknowledgements
Must give credit to https://github.com/abitfrosty.
