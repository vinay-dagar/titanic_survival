# Titanic Survival

[Link to original Titanic Dataset](https://www.kaggle.com/c/titanic/data)

_______


![The Titanic Image](https://media.nationalgeographic.org/assets/photos/000/273/27302.jpg)


In this data set we've two dataset, that include passenger information like name, age, gender, class etc. One dataset is titled `train.csv` and the other is titled `test.csv`.

The `train.csv` will contain the details of a subset of the passengers on board (891 to be exact) and importantly, will reveal whether they survived or not, also known as the *“ground truth”*.

The `test.csv` dataset contains similar information but does not disclose the “ground truth” for each passenger. We will analyze the `train.csv` and train our classification model to predict the outcomes for `test.csv`.

### Which features contain blank, null or empty values?

Cabin, Age, Embarked features contain a number of null values in that order for the training dataset.
Cabin, Age are incomplete in case of test dataset.

### Assumtions based on data analysis
We arrive at following assumptions based on data analysis done so far. We may validate these assumptions further before taking appropriate actions.

* Correlating
    * We want to know how well does each feature correlate with Survival.
  
* Completing
    * complete Age feature as it is definitely correlated to survival.
    * complete the Embarked feature as it may also correlate with survival or another important feature.
    
* Classifying.
    * Women (Sex=female) were more likely to have survived.
    * Children (Age<?) were more likely to have survived.
    * The upper-class passengers (Pclass=1) were more likely to have survived.
    
## Analyzing features coorelation

_______


> At this stage, It only make sense only for features which do not have any empty values and also are categorical


* Pclass We observe significant correlation (>0.5) among Pclass=1 and Survived
* Sex We confirm the observation during problem definition that Sex=female had very high survival rate at 74%
* SibSp and Parch These features have zero correlation for certain values.

## Analyze by visualizing data

After observing coorelation features, we can now analyze the data by visualization 

* Pclass=3 had most passengers, however most did not survive. Confirms our classifying assumption #2.
* Infant passengers in Pclass=2 and Pclass=3 mostly survived. Further qualifies our classifying assumption #2.
* Most passengers in Pclass=1 survived. Confirms our classifying assumption #3.
* Pclass varies in terms of Age distribution of passengers.


> We can extract Title feature using regular expressions.

* The RegEx pattern (\w+\.) matches the first word which ends with a dot character within Name feature.
* We can replace many titles with a more common name or classify them as `Rare`.
* We can convert the categorical Titles into ordinal

## Converting a categorical feature

we can convert features which contain strings to numerical values. This is required by most model algorithms.
_____

### Filling missing categorical features

Embarked feature takes S, Q, C values based on port of embarkation. Our training dataset has two missing values. We simply fill these with the most common occurance.


> After that we can convert the Embarked categorical feature into numerical 

____________
> Now we are ready to train a model and predict the required solution. 

Our problem is a classification and regression problem. We want to identify relationship between output (Survived or not) with other variables or features

______

We can use Logistic Regression to validate our assumptions and decisions for feature creating and completing goals. This can be done by calculating the coefficient of the features in the decision function.


* Sex is highest positivie coefficient, implying as the Sex value increases (male: 0 to female: 1), the probability of Survived=1 increases the most.
* Inversely as Pclass increases, probability of Survived=1 decreases the most.
* This way Age*Class is a good artificial feature to model as it has second highest negative correlation with Survived.
* So is Title as second highest positive correlation.

> Finally, we'l, use some classification Models to predict the outcome of `test.csv` data set.

After all we can see that Random Forest, Decision Tree results the highest socre with over 84% of accuracy
