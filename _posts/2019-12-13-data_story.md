---
layout: post
title:  "Tell me what you buy, I will tell you who you are. A data story."
date:   2019-12-12
excerpt: "A story about shopping patterns."
image: "/assets/images/pic07.jpg"
---

<!--Style used in the document: -->
<style>
img {
    display: block;
    margin-left: auto;
    margin-right: auto;
}
p{
    text-align: justify;
}
</style>
<font size="2.5">

<!--PREFACE: -->
<h4>Chapter 0. Preface.</h4>
<p>
Due to rumours about the troublesome ability of shopping centers to infer consumer information based on their shopping patterns, a private investigator, detective Duck, was hired by a consumer advocacy group to investigate the matter. Here are the details of his investigation.
</p>
 
<img class="center" src="{{ "/assets/images/pic08.png" | absolute_url }}" alt="Markdown Monster icon" width = "200" height = "150" />

<p>
Living in a time and age where every piece of our data is stored and analysed, the consumer advocacy group wonders what information retailers can gather and infer about consumers. To answer their question, detective Duck only gets information about a two year shopping spree of a group of 2500 clients of an unknown shopping center in the US. Based on this data, he seeks to identify possible links, if they exist, between demographic information (e.g. marital status, income, number of children, etc) and  purchase patterns. In other words, he would like to see how "easy" and how precise it is for retailers to infer a specific customer profile based on what their shopping habits as this could lead to easy targeted marketing. Luckily, detective Duck has followed the autumn 2019 Applied Data Analysis at the EPFL and counts on applying his newly aquired knowledge to this case. 
</p>

<br/>
<hr/>
<!--CHAPTER 1: -->
<h4>Chapter 1. A rocky start to a rocky investigation.</h4> 
<p><em><strong>A Dunnhumby dataset.</strong></em></p> 

<p>
    The consumer advocacy group (also called G.A.C) provided the detective Duck  with a dataset owned by Dunhumby, an american data science company. This dataset includes the results of a two years long study, over 2500 voluntary households. Detective Duck knows that companies use harvested data to perform targeted marketing. Using his skills in data analysis, he plans to find out exactly what can be predicted out about the customer's personnal information. He expects to observe an relation in between the clients's consumption habits and their demographic characteristics. For example, he suspects that the income category will influence the amount and price range of groceries bought per week. 
</p>

<p><em><strong>Preprocessing.</strong></em></p> 

<p>
   When facing a huge amount of data, detective Duck has learned to start by preprocessing and cleaning the available information. For this, he keeps only households which portrayed coherent and sufficient demographic data. In a second time he labels the products with precise categories refering to grocery shopping.
</p>
<p><em><strong>Demographics.</strong></em></p> 

<p>
   Detective Duck had to face a main issue when preprocessing his demographic data. Indeed, over the 2500 households studied by Dunhumby, only 780 provided their demographic information. Among these 780 families, around 750 were selected after cleaning. At this moment, suspicions started to arise in detective Duck's mind. A too small amount of data might cause troubles. Nevertheless, after a long night of working and cursing, the data was finally usable and analysable.
</p>

<img class="center" src="{{ "/assets/images/pic09.png" | absolute_url }}" alt="Markdown Monster icon" width = "250" height = "125" />
<p>
Now detective Duck is faced with the real challenge. He aims to try and extract the main consumption patterns of the clients and correlate them to their demographic features. For this, he developped several strategies as the investigation turned out to be harder than he tought when venturing into this case. Looking at the data, he quickly regretted ever leaving his cozy pond. 
</p>

<p><em><strong>Products.</strong></em></p> 

<p>
   After families selection, the detective Duck still needs to look at what they buy. The 750 selected families had access to a total of 92353 different products in their shopping center. These products are defined by their department (the place at which we find them) and by two different and non standard descriptive words sequences (commodity and sub-commodity). To be able to classify them the detective creates a function comparing both the commodity and the sub-commodity to a list of expressions from the lexical field of the grocery. He associates each expression to a certain grocery category. Since the products' descriptions are atypical, he give them a "score of similarity" with the expressions in the list. The highest score, above a certain threshold determines the label of the product. He uses the Fuzzywuzzy library to calculate this score. Fuzzywuzzy is based on Levenshtein Distance to calculate the differences and similarities between string sequences. 
</p>

<img class="center" src="{{ "/assets/images/BAD-products_trans_label.png" | absolute_url }}" alt="Markdown Monster icon" width = "900" height = "700" />
 


<br/>
<hr/>
<!--CHAPTER 2: -->
<h4>Chaptre 2.  Profiling is not a piece of cake..</h4>

<p>
   Now the data are ready for the analysis, the detective Duck is excited about facing the real challenge: profile prediction using machine learning. His goal is to extract the main consumption patterns of the shopping center's clients, and correlate them to their demographic features. For this purpose, he is already developping several clever strategies. Despite all his efforts, the investigation will turn out to be harder than he tought when venturing into this case. Looking at the data, he will quickly regret ever leaving his cozy pond...
</p>

<p><em><strong>First round of predictions.</strong></em></p> 
<p><i>Demographic and shopping trend correlations</i></p>
<p>
   After having prepared the data for analysis, Detective Duck seek for major correlation patterns. He produces the following matrix to show the relation strength in between demographic features, spendings and the products quantities for the most common labels. As he expected, all the features linked to the household composition are highly correlated. 
Indeed in the matrix the scores for household size correlated to the marital status and the household size correlated to the number of kids are both 0.91.
</p>

<img class="center" src="{{ "/assets/images/BAD-correlation-matrix.png" | absolute_url }}" alt="Markdown Monster icon" width = "600" height = "400" />

<p>
The mean and yearly spending are also well correlated (0.7) with the different products quantities. This probably means that, most of the families buy in average similar proportions of the different products labels per week and per year. 
For Duck, this first analysis is a good new. It means that the retailer can not find any correlation in between the product's type and the household's features. Of course, everybody needs to buy vegetables, meat, dairy products and beverages. That is why he can not find interesting patterns among the most common commodities. Outliers, in these distributions, might represent extreme diets (like vegetarianism or allergies). 
</p>

<p><i>A random forest to predict family's profile</i></p>
<p>
Duck is not the kind of people giving up when he gets weak correlations, he is a resourceful detective. He tries to build a predictive model to effectively show if it is possible to infer the family’s profile from its consumption. First he fits a decision tree with a 0.25/0.75 test/training split. The results for this prediction work are pretty bad. The ROC AUC score barely exceeds the baseline score. The detective can not pretend that, from this dataset the retailer could infer satisfying profiles of his customers. However the dataset ended up to be importantly reduced after filtering the households. Since machine learning models are rapidly limited by the amount of data, Duck is not surprised to see his predictions failing. Detective Duck has not said his last word...
</p>

<p><em><strong>Second round of predictions</strong></em></p>   
<p>
Duck needs to change his plan of attack in this second prediction attempt. He decides to focus on the typical cart itself rather than and overall consumption of the household. To do so he sorts the products and select the ⅔ of the most bought ones.
<p>
<p><i>Being a strategic Duck</i></p>
<p>
At that time, he uses different strategies to cluster his data and select the most interesting one :
<p>
<p>
<span>&#8226;</span> <em>I)</em>  His first idea is to cluster households in function of the main products they buy. He identifies the best number of clusters, which is in between 5 and 9, with elbow. Then he applies K-mean to create 7 households clusters. He uses a threshold at ⅓  of the households. Thus, a product is characterizing a cluster if and only if, at least one third of the households has bought this product. Two of the final clusters contain only one family. Interestingly 4 different clusters are characterized by the dairy products, bananas they buy. Duck wonders if the type of milk can give a hint on who is buying it. The biggest cluster, 1065 familis, is made of households buying unknown products. For the detective, it means that these households are not characterized by any common product.
<p>
<p>
<span>&#8226;</span> <em>II)</em>  His second idea is reducing the dataset of <i>the average amount of products bought per label by the household</i> 's dimensions using SVD. After the reduction, two dimensions explain 58% of the variance. The detective then plots the data along these two dimensions to see if he can observe some clusters. However he can not see clear clusters that could predict a certain demographic. 


<img class="center" src="{{ "/assets/images/BAD-corrplots.png" | absolute_url }}" alt="Markdown Monster icon" width = "800" height = "600" />


To make sure that this visualization does not hide any clusters, we use elbow to find a good cluster’s number. However no good clustering arise from this analysis.
<p>

<img class="center" src="{{ "/assets/images/BAD-elbow.png" | absolute_url }}" alt="Markdown Monster icon" width = "500" height = "300" />

<p>
<span>&#8226;</span> <em>III)</em>  In a third time, Duck reproduces the second strategy but taking a step back, and looking at the department instead of the labels. Elbow finds an ideal clustering for 4 clusters. Interestingly the K-mean clustering shows 4 groups mainly characterized by the quantities bought in the grocery department. 
<p>
<img class="center" src="{{ "/assets/images/BAD-clusters.png" | absolute_url }}" alt="Markdown Monster icon" width = "450" height = "225" />
    

<p><i>Best prediction further analysis</i></p>
<p>
Duck finally selects the third strategy, which gave the best results, and goes deeper into details. He looks at how precise it is possible to be when predicting demographics. He picks the biggest cluster and plots its correlation matrix in between the product quantities per label, the demographic features, the spendings and the participation rate. The correlations are now way stronger than within the overall households. The highest scores (around 0.8) are for the dairy products and the processed foods correlated to the households size or number of kids. Interestingly, it reminds the detective about his finding using the first strategy. Moreover, the other correlations are mainly strong but not really strong. This implies that the retailer would need to compare the households over an important number of features to acceptably predict their demographics.  
The G.A.C might be interested.
<p>

<img class="center" src="{{ "/assets/images/BAD-correlation-matrix2.png" | absolute_url }}" alt="Markdown Monster icon" width = "600" height = "400" />

<!--CHAPTER 3: -->
<p>
<h4>Chaptre 3.  Time to report the results to the C.A.G.</h4>
<p>

<p><i>What detective Duck learned from this investigation</i></p>
<p>
After this investigation full of twists and turns, Duck's answer to the C.A.G is the following: 
“First of all you should not worry too much. It is not as easy to get anything interesting from people’s shopping habits, at least not at the scale of a single retailer. Retailers would need to build a clever data collection and to invest money in a data analysis professional. Indeed families are more similar than we expected, no matters in which social class they are. However, I was still able to predict some simple features, as for instance having kids or not.” 
<p>
<p><i>What Duck could have done better</i></p>
<p>
The data collection the detective has analyzed might be atypical. Since he did not have any information about the location of the shopping center, he cannot claim that it represents the average grocery store. 
Moreover the number of households who gave their demographic features was limited. The accuracy of machine learning analysis often rely on the dataset size. Duck wonders if his work was biased by a too small dataset. 
He chose the product’s classification arbitrarily. The different labels were set depending on the common class of food he personally knew. Using a machine learning classification could have created unexpected and relevant groups of products.
<p>
    
<p><i>Project next steps</i></p>
<p>
As further work Duck advises the C.A.G to run a meta analysis among several shopping centers, in order to confirm or infirm his conclusions. The household set for each center should preferably be bigger and the products classification should be comparable in between the different grocery stores. 
<p>

Good job detective Duck. The smart little guy is already gone for a new investigation.