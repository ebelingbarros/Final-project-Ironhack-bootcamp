# Exploring The Real Estate Data With Tableau 

In this file we are presenting the questions that the business wanted to answer visually.
We used Tableau to create a story that is engaging and delivers all insights. The complete story can be found [here](https://public.tableau.com/profile/federico.giuliani#!/vizhome/Mid_Project_Data/StoryProject?publish=yes)


### Here are the questions and our visual answers to them:

#### 1.) Convert the necessary measures to dimensions (the variables that are categorical in nature)

- Done with Tableau
***


#### 2.) Plot the distribution of price vs. number of bedrooms, price vs. number of bathrooms, price vs. condition, price vs. floors, price vs. grade, price vs. view, and price vs. waterfront.
State your observation for each one of those graphs. Do you see any trends in prices vs the rest of those variables individually? This can also be used for EDA to identify some data cleaning operations that you might need to perform further.

![Picture](https://github.com/Caparisun/Linear_Regression_Project/blob/master/Pictures/pricevsfeatures.png)
***
![Picture](https://github.com/Caparisun/Linear_Regression_Project/blob/master/Pictures/pricevsgrade.png)
***
![Picture](https://github.com/Caparisun/Linear_Regression_Project/blob/master/Pictures/qn51.png)
***
![Picture](https://github.com/Caparisun/Linear_Regression_Project/blob/master/Pictures/qn52.png)
***
![Picture](https://github.com/Caparisun/Linear_Regression_Project/blob/master/Pictures/qn53.png)
***



#### 3.) Draw scatter plots for price vs. sqft_above, price vs. sqft_basement, price vs. living15, price vs. sqft_lot15.

![Picture](https://github.com/Caparisun/Linear_Regression_Project/blob/master/Pictures/scatterplots.png)
***


#### 4.) Identify using tableau which state data is presented to you. Use latitude (generated), longitude (generated), and zip code for this.
Color code the zip codes based on the prices to see which areas are more expensive than the others.

![Picture](https://github.com/Caparisun/Linear_Regression_Project/blob/master/Pictures/map1.png)
***


#### 5.) Create a plot to check which are the more selling properties based on the number of bedrooms in the house. Create a plot of bedrooms vs. count of data points.

![Picture](https://github.com/Caparisun/Linear_Regression_Project/blob/master/Pictures/q5.png)
***


#### 6.) We want to see the trend in price of houses based on the year built.
From our previous plot, we know that most of our customers are interested in three and four bedroom houses. Create a filter on bedroom feature to select those properties and compare the trends in prices using line charts.

![Picture](https://github.com/Caparisun/Linear_Regression_Project/blob/master/Pictures/priceperdecade.png)
***


####  7.) Create calculated field year_built_bins for the column year_built by creating buckets as follows:
For houses built between 1900 and 2000 - category A, for houses built between 2000 and 2010 - category B, and for houses built after 2010 - category C. Use IF-ELSE statement to create the bins/buckets. Compare the prices of houses for the three categories.


####  8.) Now we want to deep dive into the categories we created in the last question. 
Let’s see how many properties are in each of the categories. Indicate the numbers as labels on each of the three categories.

####  9.) Deep dive in category A, category B and category C using filters. Identify different characteristics/trends for each of the three categories.

![Picture](https://github.com/Caparisun/Linear_Regression_Project/blob/master/Pictures/exploreyear.png)
***


####  10.) Create a visually appealing dashboard to represent the information.

The story can be found [here](https://public.tableau.com/profile/federico.giuliani#!/vizhome/Mid_Project_Data/StoryProject?publish=yes):

<div class='tableauPlaceholder' id='viz1618994686440' style='position: relative'><noscript><a href='#'><img alt='Prediciting House Prices With Linear Regression - Data exploration and visualization ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Mi&#47;Mid_Project_Data&#47;StoryProject&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Mid_Project_Data&#47;StoryProject' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Mi&#47;Mid_Project_Data&#47;StoryProject&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='de' /><param name='filter' value='publish=yes' /></object></div>
