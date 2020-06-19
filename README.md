# Random Forest
Random forest is an **Ensemble** machine learning algorithm. Earlier the decision of classification was based on one model, either a logistic or a decision tree, Random Forest uses n decision trees to classify a sample in it's respective class. It uses different parts of data to build trees and each tree has a say in final decision making.

Also, there are a few shortcomings of decision trees:
* They can fit the data in hand well but when it comes to classifying new data, they do not have enough flexibility to accomodate that

Random Forest combines the simplicity of a decision tree with flexibity to accomodate new data resulting into vast improvement in accuracy.

## Steps to create a Random Forest

* Bootstrapping: We randomly select a sample from our dataset, here one record can be selected multiple times
* Now we create a decision tree using the bootstrap dataset, say we have 10 independent variables
  * Here, at each step, we need to randomply select n variables and check which splits the best
  * Say we have fixed the # of random variables for making decision at each step to 4
  * For root node, we randomly select 4 out of 10 variables
  * For each variable, we check which gives the best split, same as decision trees
  * Say variable 3 gave the best split, then it'll become our root node
  * The root node splits into 2 nodes, one in right and one in left, now we take the left one
  * We consider all variables apart from variable 3(as it's already used in root node) and randomly select 4 out of 9
  * We continue this process until we have a fully grown decision tree
  * We can choose the number of variables required to analyzed to create a node, it can be any number <= total variables
  * NOTE- all variables are up for selection in random list apart from the one which has split the node we are working on
* The above steps are repaeated 100s of times (from bootstrapping to making a tree based on above logic)
* This complete process results into a wide variety of trees, this variety makes Random Forest more effictive than a decision tree

## Decision Making using Random Forest

* Say we have built a 100 trees using the above algorithm
* We have got a new sample, we run the new sample through all the trees
* 75 trees classify the sample as 1 and 25 as 0
* We will classify the new sample as 1 as it gets majority of votes

This complete process including Bootstrapping the data and using aggregate votes to make a decision is called **Bagging**.

## Measuring How Good a Random Forest is

* Say we had 1000 records in our training dataset
* When we built the 1st bootstrapped dataset, we got 750 distinct records and since some were chosen multiple times, we had total of 1000 records
* This means 250 records were not chosen in bootstrapped dataset 1
* We run these 250 records through all trees and check if they are correctly classified
* We calculate the error for missclassification
* Same is done for all the not selected records for each bootstrapped dataset
* Say in every bootstrapped dataset we had 250 records not selected (random ones) we will get 250 * Total bootstrapped trees made i.e. 100 = 25,000 records to be checked for accuracy for Random Forest
