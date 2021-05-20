# Assessment of Brazil's electricity generation auctions
![Header](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/header3.jpg)

## Francisco Ebeling
### *May 2021*

This Project explores Visualisation and Statistical Analysis of Brazilian Electricity Generation Auctions.


## Content

- [Project Outline](#project-outline)
- [The Data](#the-data)
- [Statistical Analysis](#statistical-analysis)
- [Visualisation in Tableau](#visualisation-in-tableau)
- [Insights and concluding thoughts](#insights-and-concluding-thoughts)

## Project Outline

The objetive of this project is to assess the performance of Brazil's electricity industry generation auctions, which have been taking place since 2005. The auctions system has been devised to increase security of supply, in response to the 1990's failed experience of leaving the coordination of capacity and investments expansion to the market. These are, then, strictly regulated auctions, which aim at attracting new investments to the sector, at opening opportunities to the entry of new market participants from the private sector, but that also leave space for the public sector's guiding intervention. Distribution companies are compelled by law to contract their energy in public auctions that are organized by ANEEL, the sector regulatory agency. Companies that are interested in entering the generation segment register their generation projects before the auction, in which puchase agreements are reached between them and the distribution companies, through which price minimzation is achieved. By clicking [here](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/historicaloverview.md), you can read a detailed historical account of the process that lead to the launching of the auctions system, densely illustrated by charts. 

There is a considerably large database that is published by Brazil's electricity sector regulatory agency, ANEEL, with data regarding the more than 1,000 plants that have been auctioned so far. The hypothesis is that these auctions have been sucessful in attracting new investors, in diversifying sources of supply, in attracting new investments in power generation to a wide variety of Brazilian states, and of ruling out the risk of Brazil losing security of eletricity supply. However, the system does not lead to investments maximization.

Based on this database and after an initial exploratory analysis, two classes of machine learning models are conducted: unsupervised Random Forest multiclass classification and regression and supervised linear and polynomial regression. The first Random Forest multiclass algorithm is employed to answer the question of what an hypothetical new auction may look like in terms of investments, physical guarantee, selected energy sources, states where the new plants will be built, the average size of the physical guarantee, and the likely number of selected plants. With these predictions, it is possible to test the formulated hypothesis. 

The regression exercise answers another question, which can be done to improve the sector's developmental potential in terms of investments attraction. I regress the determinants of investments in new capacity, having in mind that physical guarantee and investments are closely correlated. What, then, are the policy tools that may be employed to avoid the problem of a potentially falling developmental potential?

<p align="center">
  <img width="75%" height="75%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/processo.png"> 
</p> 

## The Data

Brazil's electricity sector regulatory agency ANEEL publishes a spreadsheet containing [data](https://www.aneel.gov.br/documents/654791/0/CEL_Resultados_Leil%C3%B5es_Gera%C3%A7%C3%A3o_2005a2019_28102019/b56f496f-92d1-3905-b57e-2dedbde2738a) about every winning plant of its generation auctions and reports the main features of the 45 auctions held since 2005 in a Powerbi format [dashboards](https://app.powerbi.com/view?r=eyJrIjoiZTZiNDhjNjctZTQ2NC00YzFmLTgxYTUtZmY5YjEzNmI3MjdkIiwidCI6IjQwZDZmOWI4LWVjYTctNDZhMi05MmQ0LWVhNGU5YzAxNzBlMSIsImMiOjR9). After assessing this data, I used to Python to explore and assess the data, clean it, translate from portuguese to english, and create new variables. Throughout this process, some variables were converted from R$ to US$. The cleaned dataframe was exported to a CSV files to be used throughout the statistical analysis process. 

For the regression models, the cleaned dataframe was suplemented with data regarding Gross Capital Formation (GKF), Government Investments (G), Foreign Direct Investment (FDI), country specific risk (EMBI+) primary energy consumption (E), and exchange rate (R$ to US$). The data was gathered from the World Bank's statistics [website](https://data.worldbank.org/) (World Bank Open Data), from [IPEADATA](http://ipeadata.gov.br/Default.aspx) and from [BP's statistical review of World Energy](https://www.bp.com/en/global/corporate/energy-economics/statistical-review-of-world-energy.html).

<p align="center">
  <img width="95%" height="95%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/headerdata.png"> 
</p> 

[The Jupyter Notebook can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/Basic_eda.ipynb)

## Visualisation in Tableau

After this, Tableau was used to present graphs and dashboards that explored the features of the original database, plus some variables that have been created along the EDA/Data cleaning phase, and from data that was additionally imported.

[The final Tableau story can be found here.](https://public.tableau.com/profile/francisco.ebeling#!/vizhome/FinalProject_16213560028780/Story)
<p>&nbsp;</p>
<p align="center">
  <img width="95%" height="95%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/ezgif.com-gif-maker%20(1).gif">
</p> 

## Statistical Analysis

After the data was gathered and processed, the next step of the project was to answer a series of statistical questions. 

***1. Is it possible to predict what the profile of a probable contracted plant in the next generation auctions would be like?***

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

The results suggests that the hypothetical new contracted plant would likely have a **low** level of investment (bin A), a **very low** physical guarantee, a **very low** physical guarantee size in relation to the auction, would probably be located in a **Northeastern state** (BA, RN, CE), would be a **wind power plant** and would be **one among many widding bids** (in the predicition of number of contracted plants in auction the bins "D" and "C", which correspond to a middle to high number, where the most likely). With this, it can be concluded that, although a typical next plant will have a **low** level of investments and **very low** level of physical guarantee, because in the hypothetical auction the number of approved plants will be **medium to high (within the C-D range)**, there are reason to believe that suppply and demand will be well coordinated.

- [Jupyter Notebook with investments bins prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_investments.ipynb)
- [Jupyter Notebook with physical guarantee bins prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_physical_guarantee.ipynb)
- [Jupyter Notebook with average physical guarantee size per auction bins prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_size_bins.ipynb)
- [Jupyter Notebook with sources prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_sources.ipynb)
- [Jupyter Notebook with states prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_states.ipynb)
- [Jupyter Notebook with number of approved plants per auction prediction can be found here.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/classification_number_bins.ipynb)

***2. What can be done to maximize the sector's investments? What are the determinants of investment behaviour in electricity generation?***

The second part of the statistical analysis consisted in answering the question of what can be done about the scenario sketched in part one, where it was seen that the average size of the investments and of the average size of the physical guarantee tends to be small, potentially becoming a macroeconomic burden. The counterveiling factor to minimize the chances of this event materializing is to **create the conditions to increasing the number of winning bids in a given auction**. Even though these would very likely have a **low** investments and **very low** physical guarantee profile, when added up they smoothly achieve the goal of coordinating supply and demand. Investments, however, would still beyond their former peak. To analyse what can be done about it, a machine learning regression analysis is employed, using three different takes is employed: linear, polynomial and Random forest regression.

To choose the most suitable model for the regression, simple OLS models where regressed, in four different scenarios. In the first two scenarios, the dependent variable is investments. In the second one, dummmies of energy source are added. In the second last scenarios, the dependendent variable is the average size of investments in relation to the number of winning bids in a single auction. In the fourth scenario the same dummies were also added. The scenario with the best performance was the first one, as can be seen in the table below. 

<img width="95%" height="95%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/table3.png">

Therefore the equation to be regressed by the ML regression models was the following: 

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
The following table synthetizes the results obtained for the three models. 

<img width="95%" height="95%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/table4.png">

This table is telling us that while the Linear Regression machine learning algorithm serves two basic purposes, the Polynomial Regression ML and the Random Forest (unsupervised) ML algorithms tend to have only one. While in the first case both a prediction and intercept + coefficient arrays are provided, in the two latter cases in practice only the prediction array has analytical value. While the Polynomial Regression ML algorithm does provide estimations of an intercept and a coefficient, the nature of the equation makes their interpretation less straightforward. In the Random Forest case, there is no meaningful concept of coefficients as a takeaway for the modeller. **On the other hand, while using Linear Regressions serve this twofold purpose, it comes at the cost of much less statistically robust and accurate predictions, as measured by the R2 and the RMSE**.

Despite the fact that the Polynomial and Random Forest regression cannot answer the questions of what the determinants of investments in electricity plants are (at least, not in a meaningful way), they do provide an answer for the question posed in the previous section. By extrapolation, the regression models are providing likely candidates for an investment level of the next selected plant, as can be seen in the following graph. 

<p align="center">
  <img width="65%" height="65%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/ezgif.com-gif-maker%20(3).gif">
</p> 

Of these, an average can be calculated. The average investment mean of the entire population of winning bids was US$80,134,187. While the linear regression predicted an average mean of US$74,959,601 (very close to the y-test's mean), the polynomial regression and random forest regressions predicted lower values, of respectively, US$70,446,797 and US$71,195,097. By tuning the random forest's parameters, I manage to achieve a mean that was less than US$55,000,000, at the cost, however, of a much lower R2 and a higher RMSE. *Knowing how to trim the trees' branches and optimize its growth is, then, an intricate art!* 

<p align="center">
  <img width="55%" height="55%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/tenor.gif"> 
</p> 

However, returning to the question that is being answered in this section demands returning to the linear regression ML modelling world. These are the predicted intercept and coefficients:

### y = intercept + g + risk_embi + primary_energy_consumption + physical_guarantee + exch
### y = 251859563 + 2120118.19 + 110299.05 - 26798765.20 + 739.74 - 56555517.10

From the previous sections it was found that the average contracted price in each auction is bound to fall, and that increasing the number of contracted plants in each auction is a tool to increase investments. The most important result of the machine learning linear regression model is that the investments involved in the construction of a power plant is strongly dependent on its size, which is given by its physical guarantee, which is positively correlated with the dependent variable. Why, then, doesn't the government simply maximizes investments by instructing its public generation companies to propose large hydro plants in the auctions?  The answer is that it can't, as it is not that simple! The construction of large hydro dams has been usually related to large negative social, economic and environmental externalities. The Belo Monte power plant, built in the Amazon Forest on the Xingu river, is just one among a series projects that have, for more than 60 years, exchanged security of supply for these costs. For instance, Balbina's plant "kilowatts per Hectare" indicator, which measures how much area has to be flooded for the construction of the reservior to get a certain amount of energy is so low (only 2) that the result is environmental destruction on a vast scale, as can seen in the picture below. For comparison, some hydro plants' "kilowatts per Hectare" is larger than 1000!

<p align="center">
  <img width="80%" height="80%" src="https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/figures/arvores-mortas.jpg">
</p>

What the analysis of the ML linear regression model results' tells us is that there are other ways of increasing sectoral investments. While these are not necessarily controllable by the electricity industry regulatory agency ANEEL, which organizes the auctions, they may be controlled by overall government policy. Two of these are increasing the government's investments - whose positive sign suggests that there is a positive correlation between this variable and investments committed in the auction - and by lowering the level of the exchange rate to the dollar. While it would be expected that a higher exchange rate would encourage FDI in the country, the probable causal mechanism for this finding is that lower exchange rates make investments more attractive because they lower the cost of importing goods and services for the assembly of a new power plant factor. The analysis of the investment risk factor (EMBI+), which positively correlates with investments, suggests that a lower country risk does not necessarily postively affects investments. This would have occured if a negative correlation had been found, because the EMBI+ index tells that the lower the indicator, the safer it is to invest in the country.

Finally, the encouragement of energy demand growth as a tool to accelerate investments, presumably via the channel of investor expectations is not effective. In fact, the model predicts a negative correlation between energy demand and investments. While in the 1970s investments anticipated demand - because of the previous memory of severe bottlenecks that had had hurt economic growth-, in the period of analysis while demand grew steadily, investments progressively fell. Energy planners believe that they can coordinate supply and demand for energy through more modern energy planning techniques that emulate the logic of the marketplace, thus yielding demand anticipation unnecessary. 

- [Jupyter Notebook with the ML regression models.](https://github.com/ebelingbarros/Final-project-Ironhack-bootcamp/blob/main/files/Regression.ipynb)

## Insights and concluding thoughts

- The Random Forest classification algorithm can be sucessfully applied to handle problems in which the data is heavily unbalanced. Key to that endeavor is to use class weighting. While the predictions tend to continue emphasizing the largest classes, room is opened for the predictions to also contemplate the outliers. The accuracy of predictions is improved as the real world is more closely resembled. The fit of the proposed approach and hypothesis to the RF classification algorithm hinged on the possibility of improving the algorithm's predictive reach.

- The RF multiclass classification algorithm and the ML regression have a comparable predictive performance vis-à-vis the empirical verification of the formulated hypothesis. Because some of the features of the auction were classes (and not binned classes) I decided to use the classification problem to have a common pool of metrics to compare the outcome. Both the RF classification algorithm and the RF regressor (if correctly tuned) have done a good job in dealing with the unbalancedness of the data.

- A next step of the present research agenda is to predict what are the likely companies/consortia that would win the next hypothetical bid. I want to analyse whether the electricity generation auctions mechanism is encouraging a larger private sector investments appetite. In other words, I want to understand whether the sector is transitioning towards private ownership and whether the auctions mechanism has been an effective public policy. This step depends on gathering data about the companies' actionary structure, which is very time-consuming.

- Another possible step is to incorporate code that attempts to simulate firms' strategic behavior into the logic of the classification algorithm, parting from auctions theory.

- This project showed me how important it is for the field of energy policy analysis and energy planning to perform "data deep dives". Some of the problems that have affected Brazil's energy sector during the last 20 years are related to a repeated tendency to shape its rules through preconceived economic principles. Getting to know what data is really telling us through state-of-the-art algorithms and visualisations is a form of reconciliating rule-making processes with reality. 




