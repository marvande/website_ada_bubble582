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
Living in a time and age where every piece of our data is stored and analysed, the consumer advocacy group wondered what information retailers can gather and infer about consumers. Nevertheless, to answer their question, the group could only provide Detective Duck with information about a two year shopping spree of 2500 clients of an unknown shopping center based in the US. Based on this data, Duck was tasked with identifying possible links, if they exist, between demographic information (e.g. marital status, income, number of children, etc) and purchase patterns. In other words, he needed to find ou how easy it is for retailers to infer a specific customer profile based on their shopping habits. This was crucial to the consumer advocacy group as precise customer profiles lead to targeted marketing and loss of privacy. Luckily, Detective Duck followed the autumn 2019 Applied Data Analysis course at the EPFL and applied his newly aquired knowledge with diligence to this case. 

</p>

<br/>
<hr/>
<!--CHAPTER 1: -->
<h4>Chapter 1. A rocky start to a rocky investigation.</h4> 
<p><em><strong>A Dunnhumby dataset.</strong></em></p> 

<p>
    The consumer advocacy group provided Detective Duck with a dataset owned by Dunhumby, an American Data Science company. This included the results of a two years long study, over 2500 voluntary households. When looking at the dataset, Duck quickly realised that this dataset was quite big and had a lot of miscellaneous information. Nevertheless, our favourite detective has learned that when faced with this challenge, one needs to start by pre-processing and cleaning the available information. For this, he kept only households which showed coherent and sufficient demographic data. Furthermore, he labelled all 10'000 products into precise grocery categories shown below. 
        
<img class="center" src="{{ "/assets/images/products_trans_newlabel.png" | absolute_url }}" alt="Markdown Monster icon" width = "900" height = "700" /> 
</p>

<p><em><strong>Know thy households.</strong></em></p> 

<p>
   Before starting to hunt for clues, Detective Duck first had to know what kind of households were present in his data. This is where he had his first schock of the investigation. Indeed, over the 2500 households studied by Dunhumby, only 750 provided their demographic information and remained after cleaning. At this moment, suspicions started to arise in detective Duck's mind that the consumer advocacy group had provided him with quite a challenge. Undoubtetly, a small dataset would cause troubles when trying to draw predictions. Duck regretted ever leaving his cozy pond. 

</p>

<img class="center" src="{{ "/assets/images/pic09.png" | absolute_url }}" alt="Markdown Monster icon" width = "300" height = "150" />
<p>
Still, Duck aimed to extract the client's main consumption patterns and correlate them to their demographic features. For this, he developped several strategies that will be developped below. </p>

<br/>
<hr/>
<!--CHAPTER 2: -->
<h4>Chaptre 2. Profiling is not a piece of cake..</h4>

<p>
   Once the data was ready for analysis, Detective Duck was excited to face the real challenge: customer profile hunting. 
</p>

<p><em><strong> A hunt for correlations.</strong></em></p> 
<p>
   Detective Duck seekd for major correlation patterns in the whole data. After some coding, he produced the following matrix to illustrate the relation strength in between demographic features, spendings and the products quantities for the most common labels. 
</p>

<img class="center" src="{{ "/assets/images/correlation-matrix1.png" | absolute_url }}" alt="Markdown Monster icon" width = "600" height = "400" />

<p>
From this, he learned that there is some high correlation between demographic information. Specifically, household size is highly correlation to the number of kids and marital status. This did not surprise Duck as any good detective could have deduced that. Nevertheless, he noted in a part of his mind that most households with kids were married in this study. Furthermore, the mean and yearly spending were also correlated (0.7) with the different products quantities. This also did not raise any alarms, as spending more usually means buying more products in a grocery store. Nonetheless, Duck could not find any direct link between demographics and product quantities. Not satisfied with this result, he decided to pursue the matter further, as it seemed too easy. He speculated that no correlation between labels and demographics could mean that the labels were not specific enough, as all households probably just bought globally the same amount in the categories of vegetables, meat, dairy products, etc. Thus, in general, except for outliers with extreme diets, all households seem to buy from the same grocery categories. </p>

<iframe src='https://gfycat.com/ifr/AdmiredGlumBluebreastedkookaburra' frameborder='0' scrolling='no' width='60%' height='60%' style='position:absolute;top:0;left:0;' allowfullscreen>
</iframe>

<br/>
<hr/>
<p><em><strong> A duck in a random forest.</strong></em></p> 

<p>
Our favourite duck is not the kind of duck that gives up when discovering weak correlations, the consumer group hired him because he is the best in the field. Thus, he decided to follow another path and to seek help from Machine Learning, more specifically, Random Forests. He built a predictive model that would hopefully find things, he as a simple duck, could not. First, he fitted a decision tree on the monthly product quantities bought by all households with available demographic information. The results for this were regretfully bad. So bad that Duck could have just randomly set a random demographic parameter for each household and the result would have been better (e.g. the ROC AUC score barely exceeded the baseline score). The same occurred when fitting a random forest model. Thus, he concluded that, using only labels, there was not enough data to train a good machine learning model and infer satisfying customer profiles. Disappointed but not surprised as he had already suspected something of the sort would happen (see section <i>Know thy households</i>), Duck resigned to pursue another investigation path, as he had not yet said his last word.
</p>

<img class="center" src="{{ "/assets/images/pic10.jpg" | absolute_url }}" alt="Markdown Monster icon" width = "400" height = "200" />

<p><em><strong>Smart clustering by a strategic duck.</strong></em></p>   
<p>
Duck needed to change his plan of action as he had promised to deliver. Thus, he decided to search for typical grocery carts present in the data. From this, he hoped to be able to relate them to demographic parameters. To look for typical carts, he pursued several ideas.
</p>

<p><i>Product clusters:</i></p>

<p>His first idea was to toss aside labels and focus on specific products. So, he looked to cluster households by the exact weekly product quantities they bought, the hope being that different typical weekly shopping carts would appear (e.g. a weekly shopping cart with bananas and cheddar cheese). To identify the ideal number of clusters in the data, he used the elbow method and found a number between 5 and 9. This he used with k-means and created 7 households clusters. To identify what those clusters bought weekly, he decided that for a product to caracterize a cluster, it had to be bought by at least a third of the households in the clutster (a very generous threshold).  Looking at the results, Duck saw that two clusters contained only a single household and that one contained around a 1000 but had no product in common and dismissed those. Furthermore, the remaining clusters had either bananas or dairy as their caracteristic product. From this, Duck started to wonder if this dataset was a cruel joke that someone had played on him, or wether this shopping center was frequented by what seemed to be a troop of monkeys. Detective Duck concluded that though labels were too vague, clustering on products was probably too precise as there were several product IDs for the same type of product (e.g. 5 different milk IDs). So though some households maybe bought the same weekly quantity of milk, because they bought a different brand there carts were not assimilated as the same. 
</p>

<div class="row">
  <div class="column">
    <img class="center" src="{{ "/assets/images/elbow7.png" | absolute_url }}" alt="Markdown Monster icon" width = "200" height = "50" />
  </div>
  <div class="column">
    <img class="center" src="{{ "/assets/images/elbow7.png" | absolute_url }}" alt="Markdown Monster icon" width = "200" height = "50" />
  </div>
</div>

<p>
<b>CONTINUE EDITING FROM HERE</b>
</p>

<p>

<p><i>Department clusters:</i></p>

<p>
Barely recovered from his banana and milk experience, Duck's second idea was to look for clusters in the departments of the products. After an SVD on the weekly average amount of products bought per deparments, the detective found that two dimensions explain 96% of total variance. So, he plotted the data along these two dimensions and colored it according to different demographic labels to search for clusters. 
</p>

<img class="center" src="{{ "/assets/images/BAD-corrplots.png" | absolute_url }}" alt="Markdown Monster icon" width = "800" height = "600" />

<p>Though visually he could not find any, he still wanted to be sure that none were hiding so he applied the elbow method for a cluster number from 2 to 20. o make sure that this visualization does not hide any clusters, we use elbow to find a good cluster’s number. However no good clustering arise from this analysis.</p>


<img class="center" src="{{ "/assets/images/BAD-elbow.png" | absolute_url }}" alt="Markdown Monster icon" width = "500" height = "300" />

<p><i>Redefining labels:</i></p>
<p>
In a third time, Duck reproduces the second strategy but taking a step back, and looking at the department instead of the labels. Elbow finds an ideal clustering for 4 clusters. Interestingly the K-mean clustering shows 4 groups mainly characterized by the quantities bought in the grocery department. 
</p>

<div class="row">
  <div class="column">
    <img class="center" src="{{ "/assets/images/elbow4.png" | absolute_url }}" alt="Markdown Monster icon" width = "400" height = "275" />
  </div>
  <div class="column">
    <img class="center" src="{{ "/assets/images/clusters.png" | absolute_url }}" alt="Markdown Monster icon" width = "375" height = "250" />
  </div>
</div>


<p><i>Best prediction further analysis</i></p>
<p>
Duck finally selects the third strategy, which gave the best results, and goes deeper into details. He looks at how precise it is possible to be when predicting demographics. He picks the biggest cluster and plots its correlation matrix in between the product quantities per label, the demographic features, the spendings and the participation rate. The correlations are now way stronger than within the overall households. The highest scores (around 0.8) are for the dairy products and the processed foods correlated to the households size or number of kids. Interestingly, it reminds the detective about his finding using the first strategy. Moreover, the other correlations are mainly strong but not really strong. This implies that the retailer would need to compare the households over an important number of features to acceptably predict their demographics.  
The G.A.C might be interested.
</p>

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