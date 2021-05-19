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

There is a considerably large database that is published by Brazil's electricity sector regulatory agency, ANEEL, with data regarding the more than 1,000 plants that have been auctioned so far. The hypothesis is that although these auctions have been sucessful in attracting new investors, in diversifying sources of supply, in attracting new investments in power generation to a wide variety of Brazilian states, the long-term risk of energy scarcity has not been ruled out. Brazil's predominantly hydro based interconnected system is still subjected to the risk posed by variations in rainfall, at the same that the additions that are been made to the system's installed capacity (as measured by physical guarantee, which is a measure of availability of a plant's capacity) through the auctions are tendentially becoming smaller. This relationship can be clearly visualized in the following graph, which relates the the total physical guaranteed secured in every auction with the average size of it. Thus, if the number of auctioned plants in the next round falls, Brazil may face a long term security of supply problem.

<p align="center">
  <img width="100%" height="100%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/2.png"> 
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

***1. Is it possible to predict what the profile of a probable next winning bid in the generation auctions would be like?***

To answer that question, the Random Forest multiclass classification algorithm was run 6 times, predicting, for a hypothetically new selected plant, respectively, its:
- Investments in US$
- Physical Guarantee (Avg. Mw) 
- Physical Guarantee (Avg. Mw) (Physical Guarantee (Avg. Mw) / No. of winning bids in auction)
- State 
- Source
- Number of contracted plants in auction

Because the data is highly imbalanced towards chiefly low investments and physical guarantee levels, I ran the Random Forest classification algorithm using class weighting. Hence, the following code was used for specifying the model:

```
classifier = RandomForestClassifier(criterion = 'entropy', random_state=42, 
class_weight='balanced') 
```

The following table synthetizes the main results of the three takes of the Random Forest multiclass classification model used:

<img width="95%" height="95%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/table1.png">

The results suggests that the hypothetical new auctioned plant would likely have a **low** level of investment (bin A), a **very low** physical guarantee, a **very low** physical guarantee size in relation to the auction, would probably be located in a **Northeastern state** (BA, RN, CE), would be a **wind power plant** and would be **one among many widding bids** (in the prediciton of number of contracted plants in auction the bins "D" and "C", which correspond to a middle to high number, where the most likely). With this, it can be concluded that, although a typical next plant will have a **low** level of investments and **very low** level of physical guarantee, because in the hypothetical auction the number of approved plants will be **medium to high (within the C-D range)**, there are reason to believe that the country **may safeguard its electric power security of supply**.    

On the other hand, because the algorithm was instructed to perform **class weighting** in its prediction exercise, there is always a chance that the predicted classes are actually the outliers. It was seen, for example, that the energy source **solar**, which ranks third place among the most auctioned, was predicted to be more likely the predicted class than **hydro**, which occupies second spot. The same happened with the number of contracted plants in auctions, where the algorithm predicted with considerable precision that the outlier "A", which corresponds to a small number of contracted plants in auction, might be the predicted class. In this unlikely case, Brazil would **not be able to safeguard its electric power security of supply**.  

- [Jupyter Notebook with investments bins prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_investments.ipynb)
- [Jupyter Notebook with physical guarantee bins prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_physical_guarantee.ipynb)
- [Jupyter Notebook with average physical guarantee size per auction bins prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_size_bins.ipynb)
- [Jupyter Notebook with sources prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_sources.ipynb)
- [Jupyter Notebook with states prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_states.ipynb)
- [Jupyter Notebook with number of approved plants per auction prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_number_bins.ipynb)

***2. What can be done to minimize the chances of the doomsday scenario materializing? What are the determinants of investment behaviour in electricity generation?***

The second part of the statistical analysis of this projected consisted in answering the question of what can be done about the scenario found in part one. There it was found that while the price of every winning bid will inexorably tend to fall, which is explained by a technological and economic learning curve, the average size of the investments and of the average size of the physical guarantee tends to be small, which may threaten security of supply in the future and also become a macroeconomic burden. The counterveiling factor to minimize the chances of this event materializing is to **increase the number of winning bids**. Even though they have a **low** investments and **very low** physical guarantee profile, when added up they also may permit to accomplish the goal of safeguarding security of supply. What then, can be done about it, to improve this scenario? To analyse this question, a machine learning regression analysis is employed, using three different takes is employed: linear, polynomial and Random forest regression.

To choose the most suitable model for the regression, simple OLS models where regressions, in four different scenarios. In the first two scenarios, the dependent variable is investments. In the second one, dummmies of energy source are added. In the second last scenarios, the dependendent variable is the average size of investments in relation to the number of winning bids in a single auction. In the fourth scenario the same dummies were also added. The scenario with the best performance was the first one, as can be seen in the table below. 

<img width="95%" height="95%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/table3.png">

Therefore the equation to be regressed by the supervised ML regression models was the following: 

```
# As specified for OLS modelling exercise
Y = df['inv_US$'] 
X = df[['g', 'risk_embi', 'primary_energy_consumption', 'physical_guarantee', 'exch']] 
X = sm.add_constant(X) 
model = sm.OLS(Y,X) 

# As specified for the ML supervised regression algorithm
X = df2.iloc[:,0:5].values 
y = df2.iloc[:,5].values

# The 'g' stands for government expenditures, 'risk_embi' is a measure of country risk and 
'exch' is the exchange rate (R$ per US$ dollar)

```
The following table synthetizes the results for the three models. 

<img width="95%" height="95%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/table4.png">

This table is telling us that while the Linear Regression machine learning algorithm serves two basic purposes, the Polynomial Regression ML and the Random Forest (unsupervised) ML algorithms tend to have only one. While in the first case both a prediction, the coefficient array and intercept are provided, in the two latter cases in practice only the prediction array has substantial analytical value. While the Polynomial Regression ML algorithm does provide estimations of an intercept and a coefficient, the nature of the equation makes their interpretation less straightforward. In the Random Forest case, there is no meaningful concept of coefficients as a takeaway for the modeller. **On the other hand, while using Linear Regressions serve this twofold purpose, it comes at the cost of much less statistically robust and accurate predictions, as measured by the R2 and the RMSE**.

Despite the fact that the Polynomial and Random Forest regression cannot answer the questions of what the determinants of investments in electricity plants are (at least, not in a meaningful way), they do provide ancillary diagnosis for the question posed in the previous section. The average investment mean of the entire population of winning bids was US$80,134,187. While the linear regression predicted an average mean of US$74,959,601 (very close to the y-test's mean), the polynomial regression and random forest regressions predicted lower values, of respectively, US$70,446,797 and US$71,195,097. By tuning the random forest's parameters, I manage to achieve a mean that was less than US$55,000,000, at the cost, however, of a much lower R2 and a higher RMSE. *Knowing how to trim the trees' branches and optimize its growth is, then, an intricate art!* 

<p align="center">
  <img width="55%" height="55%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/tenor.gif"> 
</p> 

One possible interpretation is that these models are effectively extrapolating and predicting average investments in the future that are much lower than the current mean, given the parameters provided. This interpretation would ledence to the argument provided in the previous section that the size of the investments that are accorded by every winning bid are declining in time. 

Returning to the question that is being answered in this section demands returning to the linear regression ML modelling world. These are the predicted intercept and coefficients:

### y = intercept + g + risk_embi + primary_energy_consumption + physical_guarantee + exch
### y = 251859563 + 2120118.19 + 110299.05 - 26798765.20 + 739.74 - 56555517.10

From the previous sections it was found that the average contracted price in each auction is bound to fall, and that increasing the number of contracted plants in each auction is a tool to increase investments and the physical guarantee. The most important result of the machine learning regression models is that the investments involved in the construction of a power plant is strongly dependent on its size, which is given by its physical guarantee, which is positively correlated with the dependent variable. Why, then, doesn't the government simply phases away the risk of electricity undersupply by constructing more large hydro plants, whose physical guarantee is generally very large?  The answer is that it can't! It is not that simple. The construction of large hydro dams has been usually related to large social, economic and environmental externalities. The Belo Monte power plant, built in the Amazon Forest on the Xingu river, is just one among a series projects that have, for more than 60 years, exchanged security of supply for these costs. For instance Balbina's plant "kilowatts per Hectare", which measures how much area has to be flooded for the construction of the reservior to get a certain amount of energy is so low (only 2) that the result is environmental destruction on a vast scale, as can seen in the picture below. For comparison, some hydro plants' "kilowatts per Hectare" is larger than 1000!

<p align="center">
  <img width="80%" height="80%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/arvores-mortas.jpg">
</p>

By contrast, the average size of wind, solar, bagasse and biomass projects is relatively small. The analysis suggests that one option is to increase the number of winning bids in every auction. The results of the ML models results - chiefly of the parameter's signs - suggests that there are options. While these are not necessarily are controllable by the electricity agency, they may be controlled by government policy. Two of these are increasing the government's investments - whose positive sign suggests that there is a positive correlation between this variable and investments committed in the auction - and by lowering the level of the exchange rate to the dollar. While it would be expected that a higher exchange rate would encourage FDI in the country, the probable causal mechanism for this finding is that lower exchange rates make investments more attractive because of the cost of importing goods and services for the assembly of a new power plant factor. 

The analysis also suggests that increasing energy consumption per se is not an option to increase investments, as there is a negative correlation between these two factors. This suggests that investments in electricity have been following, and not have been anticipating demand increase. This suggests that in the future a possible bottleneck may arise. Finally, the analysis of the investment risk factor (EMBI+), which positively correlates with investments, suggests that a lower country risk does not necessarily postively affects investments. This would have occured if a negative correlation had been found, because the EMBI+ index tells that the lower the indicator, the safer it is to invest in the country.

- [Jupyter Notebook with the ML regression models.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/Regression.ipynb)

## Insights and concluding thoughts

-
-
-
-

<p align="center">
  <img width="55%" height="55%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/tenor.gif"> 
</p> 



