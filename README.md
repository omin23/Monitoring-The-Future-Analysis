
Authors: [Phoebe Yi](pxyi@umich.edu) and [Omkar Nayak](omkarn@umich.edu)

## Introduction

[Social Network Size](https://www.cmu.edu/common-cold-project/measures-by-study/psychological-and-social-constructs/social-relationships-loneliness-measures/social-integration-network-size.html#:~:text=Number%20of%20People%20in%20Social%20Network%20(Social%20Network%20Size)&text=Accordingly%2C%20social%20network%20size%20is,least%20once%20every%20two%20weeks.)
(structure) refers to the overall number of relationships one may have. Formally, it mesures the total number of poeople that a person is in
contant with at least once every two weeks. On the other hand, the quality of social relationships is often refered to as
(Function)[https://link.springer.com/chapter/10.1007/978-3-030-97722-1_2]. Most studys on social relationships consider some
comibnation of both aspects to derrive some insight about some aspect of human behavior. For the purpouse of this study, we will 
follow the terminoly of the book (Social Networks and Health Inequalities)[https://link.springer.com/book/10.1007/978-3-030-97722-1] and 
refer to the comibnation of both the structural and functional aspects of social relationships as [Social Networks](https://pmc.ncbi.nlm.nih.gov/articles/PMC3150158/).

Monitoring The Future (MTF) is a long runing study conducted by the the Institute of Social Reseach at the Univerisy of Michigan
that surveys 12th, 10th and 8th grade students. As a result, this survey gathers and maintains critical insights into the 
behaviors, attitudes, and values of adolescents. The MTF survey has proven instrumental in the development of prevention programmes,
public health policies and educational campaigns. 

In this study, our central question is **How does the quality and quantity of a person's social interations determine thier Political Leaning**. 
Here we will use Data Analysis processes to explaore and identify how indicators of loneliness suggest the political disposition of an 
adolescent. With the following results, we will develop a classification model that predicts the political leaning of an adolescent based on 
the overall state of the person's Social Network.  

### Introduction to Columns 

* <span style="background-color: #a199f7">NumSibilings: </span> A numeric variable that identifies of sibilings one has. It allows us to idetify
how many poeple of that person's generation they have in thier home life.
* <span style="background-color: #a199f7">SibilingBool: </span> A boolean variable that identifies if one has sibilings or not. This allows us
to assess wether simply having sibilings to any capacity changes one's political leaning. 
* <span style="background-color: #a199f7">NonRelBool: </span> A boolean variable that identifies if one lives with Non-Relatives (nannies, roomate, etc.).
This allows us to observe how living in palces where a one is lives with Non-Relative(s) affects thier political leaning. 
* <span style="background-color: #a199f7">FriendSAT: </span> A categorical variable that identifies how satisfied one is with thier friends. This allows
us to measure one asepct of Social Funtion. 
* <span style="background-color: #a199f7">ParentSAT: </span> A categorical variable that identifies how satisfied one is with thier parents. This allows
us to measure one asepct of Social Funtion. 
* <span style="background-color: #a199f7">TrustPPl: </span> A categorical variable that identifies how one feels abour trusting people . This allows
us to measure one asepct of Social Funtion. 
* <span style="background-color: #a199f7">AlcAlone: </span> 

* <span style="background-color: #a199f7">FatherPres: </span>

* <span style="background-color: #a199f7">MotherPres: </span>

* <span style="background-color: #a199f7">Lonely: </span>

* <span style="background-color: #a199f7">NumGoOut: </span>



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

