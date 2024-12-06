Authors: [Pheobe](pxyi@umich.edu) and [Omkar](omkarn@umich.edu)
--- 

## Introduction
In this study we attempt to develop a classification model that predicts the political leaning of an adolecent 
based on the quality and quantity of thier social interations. Monitoring the Future is a long runing study at 
the Univerisy of Michigan that surveys 12th,10th and 8th grade students. 

Initially we assume that lonelier peope will tend 
to vote towards the conservative party in the US. 

## Workflow 
    1. Reseach symptoms of a lack of quality and healthy quality of social interation, ie. loneliness
    2. Find questions that match up with the symptoms
    3. Find the most important questions (variables) 
        3.1 Lasso Regularization
    4. Build a classification model 
    5. Analyse the result


## Data Cleaning and Exploratory Data Analysis

In order to find appropriate variables for out analysis, we needed to find the right symptoms 
to look for in our data. Naturally, this led us to look for symptoms of loneliness. This led 
us to find the following variables from our data set:

1. NumSibilings - V17
2. SibilingBool - V18
3. NonRelBool - V26
4. FriendSAT - V1646
5. ParentSAT - V1647
6. TrustPPl - V1669
7. AlcAlone - V1217
8. FatherPres - V155
9. MotherPres - V156
10. Lonely - V5313
11. NumGoOut - V194

By cross referenceing the total collecetions of symptoms we extracted from out reseach to the
available questions asked in the overall dataset, we ended our hunt relevant variables with 
10 key variables. 

## Model Development 
Once we had an abundance of variables to works with. 

