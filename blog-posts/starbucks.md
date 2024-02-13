# Evaluating Starbucks Promotional Offers - Capstone - Challenge
<!-- ![Starbuckies](./images/starbucks.jpeg)  -->
<img src="./images/starbucks.jpeg" alt="Starbucks " width="75%"/>
 

Image credit : https://towardsdatascience.com/starbucks-analyze-a-coffee-b4eef811aa4a




Starbucks sends out an offer to users of the mobile app. An offer can be merely an advertisement for a drink or an actual offer such as a discount, informational, or BOGO (buy one get one free). Some users might not receive any offers during certain weeks. Not all users receive the same offer, and that is the challenge to solve with this data set.
This is a part of the Capstone Project for Udacity.
The data we will work with are of three types:
1. portfolio.json - containing offer ids and metadata about each offer (duration, type, etc.)
2. profile.json - demographic data for each customer
3. transcript.json - records for transactions, offers received, offers viewed, and offers completed.

Our primary focus will be on finding answers to these questions below:
1. What is the proportion of clients who have completed the offers based on Gender?
2. What is the proportion of clients who have completed the offers based on their Age?
3. What is the proportion of clients who have completed the offers based on their Income Level?
4. What are the most important features that help drive offers to be completed in customers?

 ## What is the proportion of Clients who have completed the offers, based on various attributes? **

** Customer Profile: Before Data Preprocessing and Cleaning **
Customer Profile based on gender, age, and income before data processing.We can see that before the data preprocessing there is erroneous data like the age factor of 120, which can be reflected in the graph. And also, there are null values that need to be handled effectively before we merge the 3 data sets. So, we need to clean the data sets, handle null and error in values, and finally merge the three data sets together before answering any questions of interest.
** Customer Profile: After Data Preprocessing and Cleaning**
After the data processing is done, we need to focus on our objective to handle only the customers who have completed offers and from that, we need the proportions of customers who completed the offer based on their attributes like age, gender, and income level. So, we first combine our data sets and do some cleaning and provide one hot encoding such that it will be easier to work with our features.
A snippet of data frame after merging and applying one-hot encoding.Now that the required data frame is obtained, we can now proceed to our interested customers that completed the offer and find the proportions of it easily along with the visualization which is shown below:
Customer who completed the offers mapped on attributes like Gender, Age, IncomeWith this above visualization, we can get a rough idea of the distribution of the customers who completed the offer. The final result that we obtained from the analysis was 
The clients who have completed the offer are male or female with an age range from 29–69 and income range between 30,000- 100,000 and their proportion is 62.35%.
### Model Creation and Evaluation
Before we move on to answer our final question regarding the important feature drivers, we need to select a supervised model that suits us and use it to evaluate the important features based on their importance.
For this, I decided to work with three machine learning models: Decision Tree Classifier, Gaussian NB, and Random Forest Classifier. Whichever performed the best would be taken into consideration for the feature selection.
After training each model on 119044 samples, their performance was evaluated using the metrics F-score and Accuracy and the time required. Their performance can be viewed below:
Performance evaluation for 3 Supervised Learning ModelsWe found out that the Random Forest Classifier works best in this case so we picked this model over others and its performance score was:
Accuracy score on testing data: 0.7881
F-score on testing data: 0.5180

Well, we can improve this model even more if we could find out the best hyperparameters for the mode. Luckily, GridSearchCV can help us achieve that.
### Model Tuning
Using GridSearch CV on our model, we could find out the best hyperparameters that make the model more efficient. We used the following parameters to evaluate:
parameters = {'max_features':['auto', 'sqrt'], 'min_samples_leaf':[2,4,6,8,10], 'min_samples_split':[2,4,6,8,10]}
We chose this because there is a little caveat to the GridsearchCV parameters selection which was that more the parameters that needed testing, more computing power was needed since we were short on this aspect, one of the cheapest solution was to change the beta score value to 0.01. 
You can find more about the beta score here in the documentation.
But in essence, The F-beta score is the weighted harmonic mean of precision and recall, reaching its optimal value at 1 and its worst value at 0.
The beta parameter determines the weight of recall in the combined score. beta <1 lends more weight to precision, while beta> 1 favors recall (beta -> 0 considers only precision, beta -> inf only recall).
Now, after changing the beta score to find the best parameters using our Random Forest Classifier, we can get the following results:
Optimized Model
Final accuracy score on the testing data: 0.7947
Final F-score on the testing data: 0.6121

** Parameters **
RandomForestClassifier(bootstrap=True, class_weight=None, criterion='gini',
 max_depth=None, max_features='auto', max_leaf_nodes=None,
 min_impurity_decrease=0.0, min_impurity_split=None,
 min_samples_leaf=10, min_samples_split=2,
 min_weight_fraction_leaf=0.0, n_estimators=20, n_jobs=1,
 oob_score=False, random_state=42, verbose=0, warm_start=False)
## What are the most important features that help drive offers to be completed in customers?
After the best model was evaluated and tuned, we could move forward to finding the important features that helped in the completion of offers.
Top features that drive offers to be completed in customersTime: time in hours since the start of the test
duration - time for the offer to be open, in days
Reward: reward given for completing an offer
difficulty: minimum required spend to complete an offer
Discount: types of offer. receive a discount when completing the offer

After evaluating the important features, we can successfully interpret the data and know the feature drivers that impact the offers which show that time is a top factor in this case. We can also make a confusion matrix to analyze our model's performance with the actual result too in order to further interpret the data.
Conclusion
In this project, we explored the Starbucks data set, analyzed, visualized to provide a solution to our queries along with creating 3 supervised machine learning models, and optimized the best one to answer our questions of interest. The model can be used to drive the necessary steps to decide on how to go about promoting offers to customers.
This project was done as a part of the Udacity Capstone Project for Data Scientist and in-depth evaluation and project development can be found on my GitHub.
