
Authors: [Phoebe Yi](pxyi@umich.edu) and [Omkar Nayak](omkarn@umich.edu)

## Introduction

[Social Network Size](https://www.cmu.edu/common-cold-project/measures-by-study/psychological-and-social-constructs/social-relationships-loneliness-measures/social-integration-network-size.html#:~:text=Number%20of%20People%20in%20Social%20Network%20(Social%20Network%20Size)&text=Accordingly%2C%20social%20network%20size%20is,least%20once%20every%20two%20weeks.)
(structure) refers to the overall number of relationships one may have. Formally, it mesures the total number of poeople that a person is in
contant with at least once every two weeks. On the other hand, the quality of social relationships is often refered to as
[Function](https://link.springer.com/chapter/10.1007/978-3-030-97722-1_2). Most studys on social relationships consider some
comibnation of both aspects to derrive some insight about some aspect of human behavior. For the purpouse of this study, we will 
follow the terminoly of the book [Social Networks and Health Inequalities](https://link.springer.com/book/10.1007/978-3-030-97722-1) and 
refer to the comibnation of both the structural and functional aspects of social relationships as [Social Networks](https://pmc.ncbi.nlm.nih.gov/articles/PMC3150158/).

Monitoring The Future (MTF) is a long runing study conducted by the the Institute of Social Reseach at the Univerisy of Michigan
that surveys 12th, 10th and 8th grade students. As a result, this survey gathers and maintains critical insights into the 
behaviors, attitudes, and values of adolescents. The MTF survey has proven instrumental in the development of prevention programmes,
public health policies and educational campaigns. 

In this study, our central question is **How does the quality and quantity of a person's social interations determine thier Political Leaning**. 
Here we will use Data Analysis processes to explaore and identify how indicators of loneliness suggest the political disposition of an 
adolescent. With the following results, we will develop a classification model that predicts the political leaning of an adolescent based on 
the overall state of the person's Social Network.  

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

* <span style="background-color: #ff8c9c">PolBel: </span> A catagorical variable that indicates one's political leaning. The variable we are trying to predict using our classifier. 
* <span style="background-color: #ff8c9c">NumSibilings: </span> A numeric variable that identifies of sibilings one has. It allows us to idetify how many poeple of that person's generation they have in thier home life.
* <span style="background-color: #ff8c9c">BR/SRinhouse: </span> A boolean value that identifies if one has sibilings in thier house. This allows us to see the effect of multiple sibilings. 
* <span style="background-color: #ff8c9c">FatherPres: </span> A boolean variable that identifies wether thier father is present. This allows us to observe an crucial node is an adolecent's Social Network.  
* <span style="background-color: #ff8c9c">MotherPres: </span> A boolean variable that identifies wether thier father is present. This allows us to observe an crucial node is an adolecent's Social Network.  
* <span style="background-color: #ff8c9c">Lonely: </span> A catagorical variable that identifies how lonley one feels. Among all the variables,the one that is direct and clearly associated with this study. 
* <span style="background-color: #ff8c9c">WishMoreFrinds: </span> A catagorical variable that identfies how strongly one feels about wanting to make more friends. Strongly indicates one's Social Network State.
* <span style="background-color: #ff8c9c">UsuallyFriends: </span> A catagorical variable that identifies wether one belives they have friends to spend time with. Another strong indicator of how strong the state of one's Social Network is. 


## Data Cleaning and Exploratory Data Analysis



### Univaritate Analysis
#### Political belifs distrobution: 

![first plot](Monitoring-The-Future-Analysis/plot1PB.png)



## Model Development 
Once we had an abundance of variables to works with. 

