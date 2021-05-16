# Assessment of Brazil's electricity generation auctions
## Francisco Ebeling
### *May 2021*

This Project explores Visualisation and Analysis of Brazilian Electricity Generation Auctions.


## Content

- [Project Outline](#project-outline)
- [The Data](#the-data)
- [Statistical Analysis](#statistical-analysis)
- [Visualisation](#visualisation)
- [Insights and concluding thoughts](#insights-and-concluding-thoughts)

## Project Outline

The objetive of this projects is to evaluate the performance of Brazil's electricity industry generation auctions, which have been taking place since 2005. The generation auctions system has been devised to increase security of supply, in response to 1990's failed experience of leaving the coordination of capacity and investments expansion to the market. These are, then, strictly regulated auctions, which aim at attracting new investment to the sector, at opening opportunities to the entry of new market participants from the private sector, but that also leave space for the public sector's guiding intervention. There is a considerably large database that is published by Brazil's electricity sector regulatory agency, ANEEL, with data regarding the more than 1,000 plants that have been auctioned so far. Based on this database and after an initial exploratory analysis. two classes of machine learning models are conducted: unsupervised Random Forest multiclass classification and regression (supervised linear and polynomial and unsupervised RAndom Forest. The first question is that is answered 

![Project Outline](figures/FinalProjectDiagram.png?raw=true "Project Outline")


## The Data

Brazil's electricity sector regulatory agency ANEEL publishes a spreadsheet containing [data](https://www.aneel.gov.br/documents/654791/0/CEL_Resultados_Leil%C3%B5es_Gera%C3%A7%C3%A3o_2005a2019_28102019/b56f496f-92d1-3905-b57e-2dedbde2738a) about every winning plant of its generation auctions 


reports and regarding 

https://www.aneel.gov.br/resultados-de-leiloes

Using Python I was able to automate the process of collecting and combining data from numerous pages. I scraped a number of different tables into Pandas Dataframes and began to explore and clean the data. After gathering information that I thought was the most useful and relevant, I exported the clean dataframes to CSV files to be used for further analysis in SQL and Tableau.

[Jupyter Notebooks can be found here.](https://github.com/surelybassy/SportStatsAnalysis/tree/master/JupyterNotebooks)

## Statistical Analysis

With lots of data collected and stored, I attempted to answer a number of statistical questions.

***1. Can you predict the total amount of goals a team will score in a season based on statistics from the games played?***

Using data from past Premier League seasons, I used a number of different regression models to try to predict the total amount of goals scored by a team. I found that I achieved the best accuracy using the Scikit-Learn Linear Regressor, giving a score of 88%.

[The Jupyter Notebook can be found here.](https://github.com/surelybassy/SportStatsAnalysis/blob/master/JupyterNotebooks/TotalGoalsPrediction.ipynb)

![Python Data Analysis](figures/PythonAnalysis.png?raw=true "Python Data Analysis")


***2. With the introduction of VAR, will we see an increase in the amount of penalties awarded?***

I wanted to investigate whether changes to the way the game is refereed is having a significant effect on the number of penalties awarded. Using data from all the Premier League games I had, as the population and the games from the start of the 2020 season as the sample, I used the formula below to conduct a hypothesis test.

![Hypothesis testing](figures/HypothesisFormula.png?raw=true "Hypothesis Testing")

The population mean was 0.106 and the sample mean was  0.231 with a standard deviation of 0.176. This gave a Z-score of 3.18. Testing first for a 95% confidence level, the critical value of 2.09 is below 3.18 so we can reject the null hypothesis and accept the alternative hypothesis. Testing again for a 99% confidence level,the critical value is 2.86, which is still below the Z-score. Therefore we can say with 99% certainty that we have seen a significant increase in the number of penalties awarded this season.

***3. With Corona regulations barring fans from entering the stadium, will we still see a home ground advantage?***

Looking at the statistics for games played before the 2020 season, **46%** of the time the team playing at home won. Comparing this to the games played under strict Covid lockdown rules, we see this number decrease to **38%**. With restrictions currently beginning to be eased and fans returning to stadiums, it would be interesting to see if this number rises back to the previous level.

## Visualisation

Using Tableau I was able to easily visualise different aspects of the team's performance and focus on how individual players were performing in different areas. I spent lots of time experimenting with different and creative ways to display the numerous features in the data and created several interactive dashboards. 

[The final Tableau story can be found here.](https://public.tableau.com/profile/andrew.ashdown#!/vizhome/SportStatisticsAnalysis/LeedsStatsStory)

![Dashboards](figures/Dashboards.png?raw=true "Tableau Dashboards")

## Insights and concluding thoughts

At the start of the project I was keen to demonstrate a number of different analytic and data science techniques, setting a number of goals I wanted to achieve, but leaving space to explore other areas along the way. 

- Using Python I collected, cleaned and exported several datasets, and created code that I can reuse to update them after every new game. Using the data I then built a machine learning model to predict how many goals a team will score in a season.

- As the data collection was relatively straight forward, I had lots of time to experiment with the visualisations in Tableau, creating a collection of visually appealing dashboards that offer interesting insight into the team's performance.

- Using the MySQL database and Flask libraries in Python, I created a simple API with a number of different routes, delivering either JSON or HTML to a user. 
