
Authors: [Phoebe Yi](pxyi@umich.edu) and [Omkar Nayak](omkarn@umich.edu)

## Introduction

[Social Network Size](https://www.cmu.edu/common-cold-project/measures-by-study/psychological-and-social-constructs/social-relationships-loneliness-measures/social-integration-network-size.html#:~:text=Number%20of%20People%20in%20Social%20Network%20(Social%20Network%20Size)&text=Accordingly%2C%20social%20network%20size%20is,least%20once%20every%20two%20weeks.) (structure) refers to the overall number of relationships one may have. Formally, it measures the total number of people that a person is in contact with at least once every two weeks. On the other hand, the quality of social relationships is often referred to as [Function](https://link.springer.com/chapter/10.1007/978-3-030-97722-1_2). Most studies on social relationships consider some combination of both aspects to derive insight into some aspect of human behavior. For the purpose of this study, we will follow the terminology of the book [Social Networks and Health Inequalities](https://link.springer.com/book/10.1007/978-3-030-97722-1) and refer to the combination of both the structural and functional aspects of social relationships as [Social Networks](https://pmc.ncbi.nlm.nih.gov/articles/PMC3150158/).


Monitoring The Future (MTF) is a long-running study conducted by the Institute of Social Research at the University of Michigan that surveys 12th, 10th, and 8th-grade students. As a result, this survey gathers and maintains critical insights into the behaviors, attitudes, and values of adolescents. The MTF survey has proven instrumental in the development of prevention programs, public health policies, and educational campaigns.

In this study, our central question is: **How does the quality and quantity of a person's social interactions determine their Political Leaning?** Here, we will use Data Analysis processes to explore and identify how indicators of loneliness suggest the political disposition of an adolescent. With the following results, we will develop a classification model that predicts the political leaning of an adolescent based on the overall state of the person's Social Network.


## Workflow 
    1. Reseach symptoms of a lack of quality and healthy quality of social interation, ie. loneliness
    2. Find questions that match up with the symptoms
    3. Find the most important questions (variables) 
        3.1 Lasso Regularization
    4. Build a classification model 
    5. Analyse the result

### The Columns 
In order to find appropriate variables for out analysis, we needed to find the right symptoms 
to look for in our data. Naturally, this led us to research the symptoms of loneliness. After finding some 
inspiration from the litrature, we found the following variables from our data set by cross referenceing
the total collecetions of symptoms we extracted to the available questions asked in the overall dataset.
Finally, we found 8 relevant variables:

* <span style="background-color: #ff8c9c80">PolBel: </span> A catagorical variable that indicates one's political leaning. The variable we are trying to predict using our classifier. 
* <span style="background-color: #ff8c9c80">NumSibilings: </span> A numeric variable that identifies of sibilings one has. It allows us to idetify how many poeple of that person's generation they have in thier home life.
* <span style="background-color: #ff8c9c80">BR/SRinhouse: </span> A boolean value that identifies if one has sibilings in thier house. This allows us to see the effect of multiple sibilings. 
* <span style="background-color: #ff8c9c80">FatherPres: </span> A boolean variable that identifies wether thier father is present. This allows us to observe an crucial node is an adolecent's Social Network.  
* <span style="background-color: #ff8c9c80">MotherPres: </span> A boolean variable that identifies wether thier father is present. This allows us to observe an crucial node is an adolecent's Social Network.  
* <span style="background-color: #ff8c9c80">Lonely: </span> A catagorical variable that identifies how lonley one feels. Among all the variables,the one that is direct and clearly associated with this study. 
* <span style="background-color: #ff8c9c80">WishMoreFrinds: </span> A catagorical variable that identfies how strongly one feels about wanting to make more friends. Strongly indicates one's Social Network State.
* <span style="background-color: #ff8c9c80">UsuallyFriends: </span> A catagorical variable that identifies wether one belives they have friends to spend time with. Another strong indicator of how strong the state of one's Social Network is. 
* <span style="background-color: #ff8c9c80">Sex: </span> A catagorical variable that identifies the Sex of a responder. This will provide us with some extra general information about the responder. 
* <span style="background-color: #ff8c9c80">Race: </span>A catagorical variable that identifies the Race of a responder. This will provide us with some extra general information about the responder. 



## Data Cleaning and Exploratory Data Analysis

Because of the sheer scope and quantity of questions that the MTF survey contains, there are 7 datasets with a few overlapping questions for every year. For the purposes of this study, we needed to use variables located in two distinct datasets, but there was no guarantee that the same people who provided information for dataset 1 would also appear in dataset 6. Fortunately, every observation in the datasets had a "Responder ID." Using the IDs of each observation, we were able to merge both datasets using an inner join (based on Responder ID) to get a merged set of people who responded to both the core questions and the extra questions relevant to this study. 

```py
df1 = pd.read_stata(form1_path)
df6 = pd.read_stata(form6_path)

df_merged = df1.merge(df6, on="RESPONDENT_ID", how="inner")
```
Once we merged our data, we still retained well over a thousand observations, confirming that it is a viable strategy for data collection! After we successfully combined all the data we needed into a single dataframe, we quickly noticed that Sex and Race were often redacted for security purposes. Since it made little sense to impute this information (which is generally not advised in social science research), we decided not to include these two columns in the training of our model. Additionally, by dropping the Sex and Race columns, we could focus on a specific responder's Social Network rather than letting the model be influenced by any physiological or cultural differences between responders.

Due to this data being available to the public for academic use and the youth of the responders, many of the responses in critical variables were either unusable or redacted. We see this clearly in variables such as political leaning, where a significant portion of responses were "Unsure," "Blank," or "Redacted." As a result, we dropped the observations that did not provide a direct response regarding their political leaning.

Cleaned data: 

<table style="border: 1px solid black; border-collapse: collapse;">
  <tr>
    <th>RESPONDENT_ID</th>
    <th>V1_x</th>
    <th>SEX</th>
    <th>POL_BELIEFS</th>
    <th>MOTHR_PRES</th>
    <th>LONELY</th>
    <th>WISH_MORE_FRNDS</th>
    <th>USLLY_FRNDS</th>
  </tr>
  <tr>
    <td>50001</td>
    <td>2023</td>
    <td>1.0</td>
    <td>3.0</td>
    <td>1.0</td>
    <td>5.0</td>
    <td>5.0</td>
    <td>4.0</td>
  </tr>
  <tr>
    <td>50002</td>
    <td>2023</td>
    <td>1.0</td>
    <td>4.0</td>
    <td>1.0</td>
    <td>5.0</td>
    <td>4.0</td>
    <td>4.0</td>
  </tr>
  <tr>
    <td>50005</td>
    <td>2023</td>
    <td>0.0</td>
    <td>0.0</td>
    <td>1.0</td>
    <td>3.0</td>
    <td>1.0</td>
    <td>1.0</td>
  </tr>
  <tr>
    <td>50006</td>
    <td>2023</td>
    <td>1.0</td>
    <td>2.0</td>
    <td>1.0</td>
    <td>4.0</td>
    <td>3.0</td>
    <td>4.0</td>
  </tr>
  <tr>
    <td>50007</td>
    <td>2023</td>
    <td>0.0</td>
    <td>0.0</td>
    <td>1.0</td>
    <td>5.0</td>
    <td>1.0</td>
    <td>5.0</td>
  </tr>
</table>


The dataset above is only an example of the overall dataset that is used the prediction model. 


### Univaritate Analysis
#### Political beliefs distribution:
<iframe
  src="assets/plot1PB.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The figure above is a bar chart that shows the total number of people in each category from the survey. The bar chart reflects an intuitive result: most adolescents don't know what their political leanings are. Another interesting observation is that the population of "Moderate" responders far eclipses the "Strong Conservative" and "Strong Liberal" populations, clearly depicting the importance of the "Undecided voter" during elections.

### Bivariate Analysis
#### Political Beliefs Distribution Compared to Reported Loneliness:
The survey included a vital variable that allowed people to report how lonely they felt and another variable that quantified their political leaning. With these two variables, we wanted to observe the correlation between them. To do this, we decided to use a heatmap to visually depict any possible tendencies in the data.
<iframe
  src="assets/plot2HM.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The heatmap suggests that the vast majority of students do not classify themselves as lonely, and they also don't know what their political leaning is. Based on the heatmap, there are a few details to note. People who self-reported as "Strong Liberals" rarely classified themselves as "Very Lonely" (5) or "Rarely Lonely" (1). Rather, they seemed to be spread out in the middle of the "Loneliness scale." By contrast, people in the "Strong Conservative" and "Conservative" categories tend to be more polarized, with a greater concentration in the "Not Lonely" and "Somewhat Lonely" ranges.

#### Sex and Social Netowrks Size (Friends)

Considering these responders are in the 12th grade, it is reasonable to assume that the majority of their social network consists of their friends. Based on this assumption, we conducted a second bivariate analysis to explore how social network strength differed between the two sexes. We did this by isolating a variable that quantified the perceived strength of one's social network and creating a box plot based on the number of people in each category.

<iframe
  src="assets/plot3BS.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Based on the figure, we find that females tended to have more established friend groups than males. This is evident from the lower fence of the Self-Reported Social Network Strength in the female category, which is the same as the median in the male category. Despite this, the upper fence for both males and females is 5. This indicates that, on average, both males and females have an established friend group by the 12th grade.

## Interesting findings 

The survey included a vital variable that allowed people to report how lonely they felt and another variable that quantified the strength of a responder's friend group. For most students in the 12th grade, it is reasonable to assume that their social network is largely grounded in their friend groups. Given these two variables, we wanted to observe the correlation between one's perceived social network strength and their self-reported loneliness. To do this in a "Table" format, we used the pandas crosstab function to gain an empirical understanding of how social network strength and loneliness are related.

```py
pivot_table = pd.crosstab(Alonescale, group_of_friends)
```
<table style="border: 1px solid black; border-collapse: collapse;">
  <thead>
    <tr>
      <th style="border: 1px solid black; padding: 5px;">Alonescale</th>
      <th style="border: 1px solid black; padding: 5px;">1</th>
      <th style="border: 1px solid black; padding: 5px;">2</th>
      <th style="border: 1px solid black; padding: 5px;">3</th>
      <th style="border: 1px solid black; padding: 5px;">4</th>
      <th style="border: 1px solid black; padding: 5px;">5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid black; padding: 5px;">1</td>
      <td style="border: 1px solid black; padding: 5px;">28</td>
      <td style="border: 1px solid black; padding: 5px;">4</td>
      <td style="border: 1px solid black; padding: 5px;">6</td>
      <td style="border: 1px solid black; padding: 5px;">7</td>
      <td style="border: 1px solid black; padding: 5px;">24</td>
    </tr>
    <tr>
      <td style="border: 1px solid black; padding: 5px;">2</td>
      <td style="border: 1px solid black; padding: 5px;">5</td>
      <td style="border: 1px solid black; padding: 5px;">13</td>
      <td style="border: 1px solid black; padding: 5px;">5</td>
      <td style="border: 1px solid black; padding: 5px;">23</td>
      <td style="border: 1px solid black; padding: 5px;">27</td>
    </tr>
    <tr>
      <td style="border: 1px solid black; padding: 5px;">3</td>
      <td style="border: 1px solid black; padding: 5px;">5</td>
      <td style="border: 1px solid black; padding: 5px;">10</td>
      <td style="border: 1px solid black; padding: 5px;">69</td>
      <td style="border: 1px solid black; padding: 5px;">27</td>
      <td style="border: 1px solid black; padding: 5px;">28</td>
    </tr>
    <tr>
      <td style="border: 1px solid black; padding: 5px;">4</td>
      <td style="border: 1px solid black; padding: 5px;">55</td>
      <td style="border: 1px solid black; padding: 5px;">84</td>
      <td style="border: 1px solid black; padding: 5px;">67</td>
      <td style="border: 1px solid black; padding: 5px;">136</td>
      <td style="border: 1px solid black; padding: 5px;">63</td>
    </tr>
    <tr>
      <td style="border: 1px solid black; padding: 5px;">5</td>
      <td style="border: 1px solid black; padding: 5px;">149</td>
      <td style="border: 1px solid black; padding: 5px;">75</td>
      <td style="border: 1px solid black; padding: 5px;">66</td>
      <td style="border: 1px solid black; padding: 5px;">58</td>
      <td style="border: 1px solid black; padding: 5px;">60</td>
    </tr>
  </tbody>
</table>


## Framing a Prediction Problem

From the previous sections (especially Figure 2), it is clear that there is some correlation between how lonely people feel and their political leaning. Due to this trend, we want to explore any possible way to predict a student's political leaning using these indicators. This naturally leads us to explore classification algorithms and how we may use multiclass classification to identify a student's political disposition.

Formally, we are trying to use relevant variables that indicate the state of a responder's social network, based on a survey, to train a multiclass classification model. On the micro scale, the algorithm would allow us to predict the political leaning of a single respondent, but on the macro scale, we can observe the sentiment of the entire class as a whole. In order to see how the overall sentiment of 12th graders changes over time, we must focus on the macro scale. Thus, our prediction problem is as follows: **Can we predict the overall political leaning of the class of 12th graders based on each individual's social network state?**

Because the data is constructed in a way that prevents overlaps of conflicting categorical data points, we don't need to modify our cleaned data for the purposes of the baseline model. In line with best model-building practices, we will use a 70-30 split, with 70% for training and the remaining 30% for testing. Since we are using a multiclass classification model, we will evaluate performance using accuracy and the F1 score for simplicity and clarity.

Finally, the training data for the prediction model is as follows:


## Baseline Model 

For the baseline Model to used a Random Forest Classifier of the 3 of the featues, <span style="background-color: #ff8c9c80">BR/SRinhouse: </span>, <span style="background-color: #ff8c9c80">Lonely: </span>, and <span style="background-color: #ff8c9c80">WishMoreFrinds: </span>. Using the following three variables made sense at it focued on 3 relevant aspects of a 12th's graders Social Network State.



## Final Model 

We added the rest of the variables and used Grid Search Cv to find the best tree depth for the model.







