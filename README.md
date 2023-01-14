# Linear Programming, Graph Theory and Machine Learning Applications

## Introduction

Zomato is an Indian multinational restaurant aggregator and food delivery company. It provides information about restaurants, average cost for two, cuisines served, ratings etc. The dataset used for analysis is picked up from kaggle.com. This analysis would be most suitable for foodies who are looking to explore cuisines from various cities of the world based on their budget. The dataset has the following components:

●	Restaurant Id
●	Restaurant Name
●	Country Code
●	City
●	Address
●	Locality
●	Locality Verbose
●	Longitude
●	Latitude
●	Cuisines
●	Average Cost for two
●	Currency
●	Has Table booking
●	Has Online delivery
●	Is delivering
●	Switch to order menu
●	Price range
●	Aggregate Rating
●	Rating colour
●	Rating text
●	Votes

## Objective

To apply the concepts from Network Theory, Machine Learning and Optimization, and draw insights that would assist a person answer the following questions

1)	How to minimise the spending while visiting a set of predefined criteria of restaurants?
2)	What is the shortest path in which I can visit all the restaurants?
3)	If I plan to visit a particular restaurant, are there any other restaurants that I can visit on the way to minimise the travel time covering multiple restaurants?
4)	If a new restaurant was introduced in a particular city, what would be the average cost for two?
 
5)	If a new restaurant was introduced in a particular city, will the restaurant deliver food?
Exploratory Data Analysis

1)	What is the mean, median, standard deviation of various attributes of data?

![Picture 1](https://user-images.githubusercontent.com/28756098/212497249-b01ff87e-cd77-4680-91f2-ea298221ac9f.jpg)


2)	Are there null values in the dataset? There are only 9 null values in cuisines. Apart from that there are no null values.

![Picture 2](https://user-images.githubusercontent.com/28756098/212497257-e6d2cf2d-4792-4d03-8424-0b1fee3cf857.jpg)

3)	How many restaurants are present for each country in the dataset? The dataset mostly contains restaurants from India.
 
![Picture 3](https://user-images.githubusercontent.com/28756098/212497258-e17e0cba-4d08-4354-a2b3-ad37c15c37f8.jpg)

Application of concepts to Dataset Scenario
Let us imagine Adam - a foodie who recently started dating a girl and wants to take her out to restaurants in multiple cities. But he has no idea on where to start, how much it would cost etc. We will try to help him out through our analysis and provide insights so that he can impress her in the best way possible.


## Optimization - Linear Programming application

Adam is planning to take his girlfriend to Manchester but his girlfriend is pretty demanding and wants to go out on dates 20 times during their visit. But it doesn’t stop there as she has more specific demands:

1.They should visit an European restaurant at least 8 times. 2.They should visit a Fast Food restaurant at least 5 times. 3.They should visit an Asian restaurant at least 4 times.
4.They should have some other cuisine at least 2 times. 5.They cannot visit the same restaurant more than 3 times.
6.	They cannot visit a restaurant with less than a 3.5 zomato rating.

Adam, who recently started working, does not have a lot of money and wants to spend as little as possible while satisfying all his girlfriend’s demands. How can Adam achieve this?

Let us look at the data snapshot
 
![Picture 4](https://user-images.githubusercontent.com/28756098/212497297-4d8b50a5-f19b-4720-b7d4-fe076cb91e16.jpg)

We preprocessed the data to split the cuisines into multiple columns and then created dummy columns to indicate the type of cuisine served by them.

![Picture 5](https://user-images.githubusercontent.com/28756098/212497298-004ed71b-b35c-4927-aa21-d1b04d8a446c.jpg)

Using the pulp package in python the problem is formulated

![Picture 6](https://user-images.githubusercontent.com/28756098/212497299-a9af1c6a-0437-48ce-bfc2-28c9e54b0d94.png)

![Picture 7](https://user-images.githubusercontent.com/28756098/212497300-02b46683-afa3-49de-ac68-3e43e5702bb6.jpg)

  
The solution for this problem is
![Picture 8](https://user-images.githubusercontent.com/28756098/212497301-0daaacb1-ae17-4351-b6b1-88abc086d859.jpg)


Adam would need to visit ‘The Grill on Alley’ 2 times, ‘Solita’ 2 times, ‘Almost Famous Burgers’ 3 times, ‘Home Sweet Home’ 3 times, ‘Teacup’ 2 times, ‘Lahore’ 3 times, ‘Akbars’ 1 time and ‘San Carlo’ 3 times to minimise the cost.

The minimum amount that Adam would end up spending is 690 pounds.

Output from Linear optimizer:

![Picture 9](https://user-images.githubusercontent.com/28756098/212497302-a23a2746-8d03-4db8-b9a3-072e3e15f0e0.jpg)

 
## Application of Graph Theory


Scenario 1 : Adam with his girlfriend plans to visit Mumbai for a week-long trip. He decides to take her out to one restaurant each day. Adam wants to know if there are any other restaurants closer than the restaurant of interest in the same path he would take so that he can pay a visit to the closer restaurant than the one intended and reduce the expenditure on Uber.

To answer Adam’s question, we use the following subset data.

![Picture 10](https://user-images.githubusercontent.com/28756098/212497303-2ba88aec-577d-46a9-ac50-53980715b425.jpg)


To detect the current location of Adam, we have to input the city, longitude and latitude. Using the Longitude and Latitude the distance from one restaurant to every other restaurant is computed. Using distance as weight, a network is created.

Code to input the current location

![Picture 11](https://user-images.githubusercontent.com/28756098/212497304-5f30f38e-9534-4f65-9c64-7ec3fbc086c6.jpg)

Function to compute distance
 
 
![Picture 12](https://user-images.githubusercontent.com/28756098/212497305-cc061467-c65f-4ef7-87ed-e28c390503ed.jpg)

![Picture 13](https://user-images.githubusercontent.com/28756098/212497306-6a4223f5-848d-4a08-b2d3-db2374d91185.jpg)


Using the single source dijkstra algorithm we can find the shortest distance from Adam’s current location to the restaurant of interest. If there are any other restaurants in the same path, and are closer, the algorithm will return the values.

![Picture 14](https://user-images.githubusercontent.com/28756098/212497307-cec703a2-19b3-4436-ae46-d6df2c08111e.jpg)

![Picture 15](https://user-images.githubusercontent.com/28756098/212497308-4353f8a0-00a7-40f3-9b09-d59fc89a0e5d.jpg)





Scenario 2 : Adam and his girlfriend both have a sweet tooth. They decided to visit all restaurants in Mumbai which serves ‘Desserts’, using the Zomato database as a reference on a given day.They want to stop at their Hotel once to take a nap in between. How can they minimise their uber expenses

![Picture 16](https://user-images.githubusercontent.com/2875609

 
Using graph analytics, we can solve this by approximating the problem to a travelling salesman problem.

tsp = nx.approximation.traveling_salesman_problem path3=tsp(G,cycle=False)

Where ‘G’ is the above graph. The optimal path from the analysis is:

'The Rolling Pin' ➡'Mumbai Vibe' ➡'Tea Villa Cafe' ➡’Hotel’ ➡ ’R' ADDA’ ➡'145 Kala Ghoda'



## Machine Learning

Objective : To predict the “average cost for two” given the location, ratings, votes, table bookings, delivery options etc. Prediction is made on the subset data filtering for India as the country.

Relationship check with the target variable

1)	Scatter plot for votes vs average cost for two

![Picture 17](https://user-images.githubusercontent.com/28756098/212497327-69e8750c-9325-4495-92d2-3341921aaf0a.jpg)

2)	Scatter plot for ratings vs average cost for two

![Picture 18](https://user-images.githubusercontent.com/28756098/212497328-d1812d93-530b-41b6-b93f-74a451dda526.jpg)
 
Since categorical variables are present, dummy columns were created to encode the values

![Picture 19](https://user-images.githubusercontent.com/28756098/212497329-9fffce54-fb37-47dc-bc4e-478eb8a60295.jpg)

The dataset is split into 70% train and 30% test.

![Picture 20](https://user-images.githubusercontent.com/28756098/212497330-7e984b32-c401-48a8-a03e-fddf61e61444.png)


The Xgboost package is used to make predictions. Since this algorithm can run in parallel, we use thread = 4. Grid search methodology is used to find the best combination of hyperparameters for the model.

![Picture 21](https://user-images.githubusercontent.com/28756098/212497331-270f94f3-eb8c-441e-8303-538eada809fb.jpg)



The best estimated parameters for the model are selected as shown below. Some of the important selected parameters are Max_depth = 256, n_estimators = 55, learning_rate=0.1

![Picture 22](https://user-images.githubusercontent.com/28756098/212497332-5739322f-52b4-4f12-ad6c-ac4baea25ba9.jpg)

 

Xgboost model was fit using the best params from the grid search. The model achieved an r-sq of 55.37% on the test dataset.

![Picture 23](https://user-images.githubusercontent.com/28756098/212497334-629667e9-efda-4768-8d4c-b3fed3988b80.jpg)




### Visualising feature importance:


![Picture 24](https://user-images.githubusercontent.com/28756098/212497335-76e0b359-c529-4b0d-85e4-033421249493.jpg)

From the graph, we can see that the longitude and latitude, Votes and aggregate rating are the most important features in the model.
 






### Application of decision tree

Objective: To predict if a restaurant present in a certain location has a home delivery service or not.


If Adam finds a new restaurant other than the ones in the list of restaurants present in the dataset, and is unsure if the restaurant has delivery service or not, the prediction made here will come in handy for Adam to plan a visit or order food accordingly.





### Data Exploration

![Picture 25](https://user-images.githubusercontent.com/28756098/212497336-4d893ece-99a6-417a-a590-d83b7982ad00.png)

We can see that the Average Cost for two is an important differentiator for understanding whether a restaurant will deliver or not
 
![Picture 26](https://user-images.githubusercontent.com/28756098/212497337-22121f5f-78ff-4e3a-854b-c939d345e1e5.png) 

From the above graph we can see that Votes is an important differentiator for understanding whether a restaurant will deliver or not


### Model Building


Steps Undertaken:

1.	Data Treatment: We use a subset of data i.e., by filter for India as a country to make predictions.
2.	Data Split: Split the dataset to 90% train and 10% test

![Picture 27](https://user-images.githubusercontent.com/28756098/212497338-00bb6963-bc4d-4f1b-842c-48a0fa8d7c87.png)

3.	Used one hot encoding to treat the categorical variables
4.	Used grid search the find the optimal parameters for the model using AUC-ROC as the primary metric
5.	Constructed the decision tree using the optimal parameters. The optimal parameters are (max_depth - 6, n_estimators=30, learning_rate=0.3)


### Model Results:


Confusion Matrix
 
![Picture 28](https://user-images.githubusercontent.com/28756098/212497342-65e4ef5f-be6c-4dc5-98b8-461490543adf.jpg) 

![Picture 29](https://user-images.githubusercontent.com/28756098/212497339-e983523e-77bc-4662-b7bb-e24897acb7fc.jpg)


The Recall for the model is 0.7787, so our model is able to identify ~78% of the restaurants offering online delivery. But the precision is low at 0.4987, which means almost half of the restaurants which the model predicts as delivering online are not true.



Plotting ROC and AUC curve

![Picture 30](https://user-images.githubusercontent.com/28756098/212497340-286e317d-94a6-4ef4-8b79-b4f4a938219d.jpg)



Decision Tree Plots
 
![Picture 31](https://user-images.githubusercontent.com/28756098/212497341-46e41f29-0c58-4b7e-8397-b32a0fd4db7c.jpg)
 

The leaf (highlighted in red box) has the highest share of online deliveries. This leaf can be reached by partitioning the data on the basis of:

Votes>20.5 ➡ Latitude>28.395 ➡ Price range >3.5



Conclusion

Using the optimization and prediction method suggested above, Adam successfully could meet his girlfriend’s demands as well as save money by optimally spending on restaurants and Uber. Also, the suggestions made by graphs, helped Adam to impress his girlfriend with smart recommendations and further strengthened their bonding.
