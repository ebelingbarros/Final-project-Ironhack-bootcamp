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

The objetive of this projects is to evaluate the performance of Brazil's electricity industry generation auctions, which have been taking place since 2005. The generation auctions system has been devised to increase security of supply, in response to 1990's failed experience of leaving the coordination of capacity and investments expansion to the market. These are, then, strictly regulated auctions, which aim at attracting new investment to the sector, at opening opportunities to the entry of new market participants from the private sector, but that also leave space for the public sector's guiding intervention. By clicking [here](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/historicaloverview.md), you can read a detailed historical account of the process that lead to the launching of the auctions system, densely illustrated by charts. 

There is a considerably large database that is published by Brazil's electricity sector regulatory agency, ANEEL, with data regarding the more than 1,000 plants that have been auctioned so far. Based on this database and after an initial exploratory analysis. two classes of machine learning models are conducted: unsupervised Random Forest multiclass classification and regression (supervised linear and polynomial and unsupervised Random Forest. The first question is that is answered  

![Project Outline](figures/FinalProjectDiagram.png?raw=true "Project Outline")


## The Data

Brazil's electricity sector regulatory agency ANEEL publishes a spreadsheet containing [data](https://www.aneel.gov.br/documents/654791/0/CEL_Resultados_Leil%C3%B5es_Gera%C3%A7%C3%A3o_2005a2019_28102019/b56f496f-92d1-3905-b57e-2dedbde2738a) about every winning plant of its generation auctions and reports the main features of the 45 auctions held since 2005 in a Powerbi format [dashboards](https://app.powerbi.com/view?r=eyJrIjoiZTZiNDhjNjctZTQ2NC00YzFmLTgxYTUtZmY5YjEzNmI3MjdkIiwidCI6IjQwZDZmOWI4LWVjYTctNDZhMi05MmQ0LWVhNGU5YzAxNzBlMSIsImMiOjR9). After assessing this data, I used to Python to explore and assess the data, clean it, translate from portuguese to english, and create new variables. Throughout this process, some variables were converted from R$ to US$. The cleaned dataframe was exported to a CSV files to be used throughout the first step of the statistical analysis process. When considered pertinent, new variables where also created within the Machine Learning Jupyter Notebooks. 

![Python Data Analysis](figures/PythonAnalysis.png?raw=true "Python Data Analysis")

For the regression models, the cleaned dataframe was suplemented with data regarding Gross Capital Formation (GKF), Government Investments (G), Foreign Direct Investment (FDI), country specific risk (EMBI+) primary energy consumption (E), and exchange rate (R$ to US$). The data was gathered from the World Bank's statistics [website](https://data.worldbank.org/) (World Bank Open Data), from [IPEADATA](http://ipeadata.gov.br/Default.aspx) and from [BP's statistical review of World Energy](https://www.bp.com/en/global/corporate/energy-economics/statistical-review-of-world-energy.html).

[Jupyter Notebooks can be found here.](https://github.com/surelybassy/SportStatsAnalysis/tree/master/JupyterNotebooks)

## Statistical Analysis

After the data was gathered and processed, the next step of the project was to answer a series of statistical questions. 

***1. Is it possible to predict the profile of a probable next winning bid in the generation auctions would be like?***

To answer that question, the Random Forest model multiclass was used in three different configurations. In the first one, I used the id of the individual winning bids themselves as classes to predicted. By using the "gini" criterion for prediction, it was possible to predict that that the probable average physical guarantee of the next auctioned would be in average 19.69 MW, and that the contracted electricty price would be US$22.5 per MW. It would be a wind energy plant and would be one out of 62 plants contracted in a hypothetical auction. It was shown that the physical guarantee and the probable investments associated with this hypothetical plants' construction are at the lower tier, but that the price negotiated would be very favorable. In this hypothetical scenario, the large number of plants contracted would to some extent compensate for the low physical guarantee and investments. The downside of this modeling approach was its very low accuracy score (0.00) and the fact that creating a confusion matrix added no practical value to the analysis due to the very large number of classes.

Because of the low level of statisfical significance of this first take, the model was run two more times. While a second predicted the probable bins (quantile) of the hypothetical physical guarantee of the next winning bid, the third one predicted the probable bins (quantile) of the hypothetical invesmtents. Because I wanted to observe how parameterization alters the test statistics, in the second exercise I experimented much more intensively with the Sklearn Random Forest classifier's available tuning options than in the third one. The results of the first modelling approach suggest that although the lower bins/quantiles (0-20%, 20-40%, and 40-60%) tend to appear with much more frequency in the results, suggesting the intial hypothesis that indeed the pyhsical guarantee of winning bids is declining, the results are highly dependent on which paramters are used and how. In other words, the modeller has the option to effectively guide the algorithm. 

In the third take, where I wanted to predicted the probable bins (quantile) of the hypothetical investments in the next approved power plant, I also found that there tends to be a larger probability of the the next selected power plant to be concentrated on the lower bins. However, by looking at the confusion matrix it was possible to observe that the the higher quantiles predicted (20-40%, 40-60%, 60-80%) where the ones with the largest number of False Positives and False Negatives, which suggests that the modelling may have underpredicted the probability of a next power plant having a low level of investments.

The following table synthetizes the main results of the three takes of the Random Forest multiclass classification model used.

![Python Data Analysis](figures/PythonAnalysis.png?raw=true "Python Data Analysis")

[Jupyter Notebook with ids as the class to be predicted can be accessed here.](https://github.com/surelybassy/SportStatsAnalysis/blob/master/JupyterNotebooks/TotalGoalsPrediction.ipynb)
[Jupyter Notebook with bins of physical guarantee to be producted can be accessed here.](https://github.com/surelybassy/SportStatsAnalysis/blob/master/JupyterNotebooks/TotalGoalsPrediction.ipynb)
[Jupyter Notebook with bins of investments can be found here.](https://github.com/surelybassy/SportStatsAnalysis/blob/master/JupyterNotebooks/TotalGoalsPrediction.ipynb)

***2. What are the determinants of investment behaviour and what can be done about it?***

The second part of the statistical analysis of this projected consisted in answering the question of what can be done about the scenario found in part one. There it was found that while the price of every winning bid will inexorably tend to fall, which is explained by a technological and economic learning curve, the average size of the investments and of the average size of the physical guarantee tends to be small, which may threaten security of supply in the future and also become a macroeconomic burden. What then, can be done about it, to improve this scenario? To improve this scenario, a machine learning regression analysis is employed, using three different takes is employed (linear, polynomila and Random forest regression). 

To choose the most suitable model for the regression, simple OLS models where conducted, in four different scenarios. In the first two scenarios, the dependent variable is investments. In the second one, dummmies of energy source are added. In the second last scenarios, the dependt variable is the average size of investments in relation to the number of winning bids in a single auction. In the fourth scenario the same dummies were also added. The scenario with the best performance was the first one, and therefore the equation to be regressed by the supervised ML regression models was the following: 

![equation](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/equation.png)

where g stands for Government expenditures, “size” – which is a measure of how many power plants were selected in a given auction –, r, which refers to embi+, which is a country specific risk measuer, e, referring to primary energy consumption, p, referring to the physical guarantee and xr, which is the exchange rate.



The population mean was 0.106 and the sample mean was  0.231 with a standard deviation of 0.176. This gave a Z-score of 3.18. Testing first for a 95% confidence level, the critical value of 2.09 is below 3.18 so we can reject the null hypothesis and accept the alternative hypothesis. Testing again for a 99% confidence level,the critical value is 2.86, which is still below the Z-score. Therefore we can say with 99% certainty that we have seen a significant increase in the number of penalties awarded this season.

## Visualisation

After this, Tableau was used to present graphs and dashboards that tell a story of the entire project, parting from a visual analysis the historical process that led to the creation of the electricity generation auction system, passing through a visualization of its main features, to an exploration of the models' main results. The Tableau story may be consumed as a long version of the final project presentation.

[The final Tableau story can be found here.](https://public.tableau.com/profile/andrew.ashdown#!/vizhome/SportStatisticsAnalysis/LeedsStatsStory)

![Dashboards](figures/Dashboards.png?raw=true "Tableau Dashboards")

## Insights and concluding thoughts

At the start of the project I was keen to demonstrate a number of different analytic and data science techniques, setting a number of goals I wanted to achieve, but leaving space to explore other areas along the way. 

- Using Python I collected, cleaned and exported several datasets, and created code that I can reuse to update them after every new game. Using the data I then built a machine learning model to predict how many goals a team will score in a season.

- As the data collection was relatively straight forward, I had lots of time to experiment with the visualisations in Tableau, creating a collection of visually appealing dashboards that offer interesting insight into the team's performance.

- Using the MySQL database and Flask libraries in Python, I created a simple API with a number of different routes, delivering either JSON or HTML to a user. 
