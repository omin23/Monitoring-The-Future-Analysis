# Monitoring-The-Future-Analysis

### Introduction
In this study we attempt to create a model that predicts the political leaning of an adolecent 
based on the quality and quantity of thier social interations. Initially we assume that lonlier 
peope will tend to vote towards the conservative party in the US. 

### Workflow 
    1. Reseach symptoms of a lack of quality and healthy quality of social interation, ie. loneliness
    2. Find questions that match up with the symptoms
    3. Find the most important questions (variables) 
        3.1 Lasso Regularization
    4. Build a classification model 
    5. Analyse the result

### Step 1
We just looked into some litrature to make sure that our origional hypothesis had some basis. 

### Step 2

In order to find appropriate variables for out analysis, we needed to find the right symptoms 
to look for in our data. Naturally, this led us to look for symptoms of loneliness. This led 
us to find the following variables from our data set:

1. How many brothers and sisters do you have? (Include step-brothers and sisters and half-brothers and sisters.) - V17 - # SIBLINGS
2. Which of the following people live in the same household with you? Sibiling - V18 - R'S HSHLD ALONE
3. Which of the following people live in the same household with you? Non-relative - V26 - R'S HSHLD NONRLT
4. How satisfied are you with... A006F: Your friends and other people you spend time with? - V1646 - SAT OWN FRIENDS
5. How satisfied are you with... A006G: The way you get along with your parents? - V1647 - SAT GT ALNG PRN
6. Generally speaking, would you say that most people can be trusted or 
that you can't be too careful in dealing with people? -  V1669 - PPL CAN B TRSTD
7. When you used alcohol during the last year, how often did you use it in each of the following situations? 
(Mark one circle for each line.) B008A: When you were alone -  V1217 - X/YR ALC ALONE
8. Which of the following people live in the same household with you? 
(Mark ALL that apply.) B. Father (or male guardian) - V155 - R'S HSHLD FATHER
9. Which of the following people live in the same household with you? 
(Mark ALL that apply.) C. Mother (or female guardian) - V156 - R'S HSHLD MOTHER
10. A lot of times I feel lonely - V5313 - OFTN FEEL LONELY
11. During a typical week, on how many evenings do you go out for fun and recreation? - V194 - #X/AV WK GO OUT


By cross referenceing the total collecetions of symptoms we extracted from out reseach to the
available questions asked in the overall dataset, we ended our hunt relevant variables with 
10 key variables. 

### Step 3 
Once we had an abundance of variables to works with. 

