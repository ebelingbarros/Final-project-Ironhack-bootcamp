# Assessment of Brazil's electricity generation auctions
![Header](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/header3.jpg)

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

The objetive of this project is to assess the performance of Brazil's electricity industry generation auctions, which have been taking place since 2005. The generation auctions system has been devised to increase security of supply, in response to the 1990's failed experience of leaving the coordination of capacity and investments expansion to the market. These are, then, strictly regulated auctions, which aim at attracting new investments to the sector, at opening opportunities to the entry of new market participants from the private sector, but that also leave space for the public sector's guiding intervention. By clicking [here](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/historicaloverview.md), you can read a detailed historical account of the process that lead to the launching of the auctions system, densely illustrated by charts. 

There is a considerably large database that is published by Brazil's electricity sector regulatory agency, ANEEL, with data regarding the more than 1,000 plants that have been auctioned so far. The hypothesis is that although these auctions have been sucessful in attracting new investors, in diversifying sources of supply, in attracting new investments in power generation to a wide variety of Brazilian states, the long-term risk of energy scarcity has not been ruled out. Brazil's predominantly hydro based interconnected system is still subjected to the risk posed by variations in rainfall, at the same that the additions that are been made to the system's installed capacity (as measured by physical guarantee) through the auctions are tendentially becoming smaller. If the number of auctioned plants in the next round falls, Brazil may face a long term security of supply problem. 

<p align="center">
  <img width="95%" height="95%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/2.png"> 
</p> 


Based on this database and after an initial exploratory analysis, two classes of machine learning models are conducted: unsupervised Random Forest multiclass classification and regression and supervised linear and polynomial regression. The first Random Forest multiclass algorithm is employed to answer the question of what an hypothetical new auction may look like in terms of investments, physicial guarantee, selected energy sources, states where the new plants will be built, the average size of the physical guarantee, and the likely number of selected plants. With these predictions, it is possible to test the formulated hypothesis. 

The regression exercise answers another question, which is what can be done about it. I regress the determinants of investments in new capacity, having in mind that physical guarantee and investments are closely correlated. What, then, are the policy tools that may be employed to avoid the problem of faltering security of supply?

<p align="center">
  <img width="75%" height="75%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/processo.png"> 
</p> 



## The Data

Brazil's electricity sector regulatory agency ANEEL publishes a spreadsheet containing [data](https://www.aneel.gov.br/documents/654791/0/CEL_Resultados_Leil%C3%B5es_Gera%C3%A7%C3%A3o_2005a2019_28102019/b56f496f-92d1-3905-b57e-2dedbde2738a) about every winning plant of its generation auctions and reports the main features of the 45 auctions held since 2005 in a Powerbi format [dashboards](https://app.powerbi.com/view?r=eyJrIjoiZTZiNDhjNjctZTQ2NC00YzFmLTgxYTUtZmY5YjEzNmI3MjdkIiwidCI6IjQwZDZmOWI4LWVjYTctNDZhMi05MmQ0LWVhNGU5YzAxNzBlMSIsImMiOjR9). After assessing this data, I used to Python to explore and assess the data, clean it, translate from portuguese to english, and create new variables. Throughout this process, some variables were converted from R$ to US$. The cleaned dataframe was exported to a CSV files to be used throughout the first step of the statistical analysis process. When considered pertinent, new variables where also created within the Machine Learning Jupyter Notebooks. 

For the regression models, the cleaned dataframe was suplemented with data regarding Gross Capital Formation (GKF), Government Investments (G), Foreign Direct Investment (FDI), country specific risk (EMBI+) primary energy consumption (E), and exchange rate (R$ to US$). The data was gathered from the World Bank's statistics [website](https://data.worldbank.org/) (World Bank Open Data), from [IPEADATA](http://ipeadata.gov.br/Default.aspx) and from [BP's statistical review of World Energy](https://www.bp.com/en/global/corporate/energy-economics/statistical-review-of-world-energy.html).

<p align="center">
  <img width="95%" height="95%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/headerdata.png"> 
</p> 

[The Jupyter Notebook can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/Basic_eda.ipynb)

## Visualisation in Tableau

After this, Tableau was used to present graphs and dashboards that explored the features of the original database, plus some variables that have been created along the EDA/Data cleaning phase. 

[The final Tableau story can be found here.](https://public.tableau.com/profile/francisco.ebeling#!/vizhome/FinalProject_16213560028780/Story)
<p>&nbsp;</p>
<p align="center">
  <img width="95%" height="95%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/ezgif.com-gif-maker%20(1).gif">
</p> 

## Statistical Analysis

After the data was gathered and processed, the next step of the project was to answer a series of statistical questions. 

***1. Is it possible to predict the profile of a probable next winning bid in the generation auctions would be like?***

To answer that question, the Random Forest model multiclass was used in three different configurations. In the first one, I used the id of the individual winning bids themselves as classes to predicted. By using the "gini" criterion for prediction, it was possible to predict that that the probable average physical guarantee of the next auctioned would be in average 19.69 MW, and that the contracted electricty price would be US$22.5 per MW. It would be a wind energy plant and would be one out of 62 plants contracted in a hypothetical auction. It was shown that the physical guarantee and the probable investments associated with this hypothetical plants' construction are at the lower tier, but that the price negotiated would be very favorable. In this hypothetical scenario, the large number of plants contracted would to some extent compensate for the low physical guarantee and investments. The downside of this modeling approach was its very low accuracy score (0.00) and the fact that creating a confusion matrix added no practical value to the analysis due to the very large number of classes.

Because of the low level of statisfical significance of this first take, the model was run two more times. While a second predicted the probable bins (quantile) of the hypothetical physical guarantee of the next winning bid, the third one predicted the probable bins (quantile) of the hypothetical invesmtents. Because I wanted to observe how parameterization alters the test statistics, in the second exercise I experimented much more intensively with the Sklearn Random Forest classifier's available tuning options than in the third one. The results of the first modelling approach suggest that although the lower bins/quantiles (0-20%, 20-40%, and 40-60%) tend to appear with much more frequency in the results, suggesting the intial hypothesis that indeed the pyhsical guarantee of winning bids is declining, the results are highly dependent on which paramters are used and how. In other words, the modeller has the option to effectively guide the algorithm. 

<p align="center">
  <img width="55%" height="55%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/tenor.gif"> 
</p> 

In the third take, where I wanted to predicted the probable bins (quantile) of the hypothetical investments in the next approved power plant, I also found that there tends to be a larger probability of the the next selected power plant to be concentrated on the lower bins. However, by looking at the confusion matrix it was possible to observe that the the higher quantiles predicted (20-40%, 40-60%, 60-80%) where the ones with the largest number of False Positives and False Negatives, which suggests that the modelling may have underpredicted the probability of a next power plant having a low level of investments.

The following table synthetizes the main results of the three takes of the Random Forest multiclass classification model used.

![Python Data Analysis](figures/PythonAnalysis.png?raw=true "Python Data Analysis")

- [Jupyter Notebook with ids as the class to be predicted can be accessed here.](https://github.com/surelybassy/SportStatsAnalysis/blob/master/JupyterNotebooks/TotalGoalsPrediction.ipynb)
- [Jupyter Notebook with bins of physical guarantee to be producted can be accessed here.](https://github.com/surelybassy/SportStatsAnalysis/blob/master/JupyterNotebooks/TotalGoalsPrediction.ipynb)
- [Jupyter Notebook with bins of investments can be found here.](https://github.com/surelybassy/SportStatsAnalysis/blob/master/JupyterNotebooks/TotalGoalsPrediction.ipynb)

***2. What are the determinants of investment behaviour and what can be done about it?***

The second part of the statistical analysis of this projected consisted in answering the question of what can be done about the scenario found in part one. There it was found that while the price of every winning bid will inexorably tend to fall, which is explained by a technological and economic learning curve, the average size of the investments and of the average size of the physical guarantee tends to be small, which may threaten security of supply in the future and also become a macroeconomic burden. What then, can be done about it, to improve this scenario? To improve this scenario, a machine learning regression analysis is employed, using three different takes is employed (linear, polynomila and Random forest regression). 

To choose the most suitable model for the regression, simple OLS models where conducted, in four different scenarios. In the first two scenarios, the dependent variable is investments. In the second one, dummmies of energy source are added. In the second last scenarios, the dependendent variable is the average size of investments in relation to the number of winning bids in a single auction. In the fourth scenario the same dummies were also added. The scenario with the best performance was the first one, as can be seen int the table below. 

<p align="center">
  <img width="39%" height="39%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/equation2.png">
</p>

Therefore the equation to be regressed by the supervised ML regression models was the following: 

<p align="center">
  <img width="29%" height="29%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/equation2.png">
</p>

where "g" stands for Government expenditures, "r", which refers to embi+, which is a country specific risk measure, "e", referring to primary energy consumption, "p", referring to the physical guarantee and "xr", which is the exchange rate. The following table synthetizes the results for the three models. 

<p align="center">
  <img width="39%" height="39%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/equation2.png">
</p>

From the previous sections it was found that the average contracted price in each auction is bound to fall, and that increasing the number of contracted plants in each auction is a tool to increase investments and the physical guarantee. The most important result of the machine learning regression models is that the investments involved in the construction of a power plant is strongly dependent on its size, which is given by its physical guarantee. 

Constructing ever larger plants to maximize may not be in the realm of the possible due to environmental reasons. After having been side-lined because of strong environmental and social opposition during the 1980s, massive investments in big hydroelectricity projects made a comeback through the carrying out of public energy auctions in the late 2000s. These projects’ configuration was shaped by the aim to minimize the environmental impact of hydropower construction in the Amazon region, which led the new generation of hydro dams to be built with the run-of-river technique.  However, the problem is that this construction technique reduces energy generation capacity (Viola and Franchini, 2017, p. 111). For example, Belo Monte’s capacity factor was only 40% (Carvalho, 2008, p. 220). This is tendentially worsened by frequent, prolonged droughts in the Amazon region (Viola and Franchini, 2017, p. 111). The construction of large hydro plants in the Amazon was subjected to heavy criticism from socio-environmental NGOs and local and indigenous communities directly affected by the projects (ibid, p. 143). It was believed that these massive hydro dams would encourage further forest degradation and also led to the dislocation of indigenous and local communities (ibid, p. 110-1). The licensing and implementation of the Belo Monte dam, which has been the subject of intricate and longstanding legal battles (Hochstetler, 2011, p. 359), led to multiple violations of domestic constitutional provisions, laws, and international treaties.  There are charges that the local population’s and indigenous concerns have not been sufficiently considered and that the environmental licensing process was fraught with substantial weakness (ibid, p. 359-363). Due to these factors, it may not be possible to rely on hydro power's sheer size to maximize investments and physical guarantee. 

By contrast, the average size of wind, solar, bagasse and biomass projects is relatively small. The analysis suggests that one option is to increase the number of winning bids in every auction. The results of the ML models results - chiefly of the parameter's signs - suggests that there are options. While these are not necessarily are controllable by the electricity agency, they may be controlled by government policy. Two of these are increasing the government's investments - whose positive sign suggests that there is a positive correlation between this variable and investments committed in the auction - and by lowering the level of the exchange rate to the dollar. While it would be expected that a higher exchange rate would encourage FDI in the country, the probable causal mechanism for this finding is that lower exchange rates make investments more attractive because of the cost of importing goods and services for the assembly of a new power plant factor. 

The analysis also suggests that increasing energy consumption per se is not an option to increase investments, as there is a negative correlation between these two factors. This suggests that investments in electricity have been following, and not have been anticipating demand increase. This suggests that in the future a possible bottleneck may arise. Finally, the analysis of the investment risk factor (EMBI+), which positively correlates with investments, suggests that a lower country risk does not necessarily postively affects investments. This would have occured if a negative correlation had been found, because the EMBI+ index tells that the lower the indicator, the safer it is to invest in the country.

## Insights and concluding thoughts

At the start of the project I was keen to demonstrate a number of different analytic and data science techniques, setting a number of goals I wanted to achieve, but leaving space to explore other areas along the way. 

- Using Python I collected, cleaned and exported several datasets, and created code that I can reuse to update them after every new game. Using the data I then built a machine learning model to predict how many goals a team will score in a season.

- As the data collection was relatively straight forward, I had lots of time to experiment with the visualisations in Tableau, creating a collection of visually appealing dashboards that offer interesting insight into the team's performance.

- Using the MySQL database and Flask libraries in Python, I created a simple API with a number of different routes, delivering either JSON or HTML to a user. 

## References

- Carvalho, J. F. D. (2008). Prioridades para investimentos em usinas elétricas. Estudos avançados, 22(64), 215-225.
- Hochstetler, K. (2011). The politics of environmental licensing: Energy projects of the past and future in Brazil. Studies in Comparative International Development, 46(4), 349-371.
- Viola, E., Franchini, M. (2017). Brazil and climate change: beyond the Amazon. Abingdon: Routledge.

