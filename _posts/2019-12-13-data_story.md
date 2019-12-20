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

div{
  display: block;
  visibility: visible;
}

</style>

<!--PREFACE: -->
<h4>Preface.</h4>
<p>
Due to rumours about the troublesome ability of shopping centers to infer consumer information based on their shopping patterns, a private investigator, Detective Duck, was hired by a consumer advocacy group to investigate the matter. Here are the details of his investigation.
</p>
 
<img class="center" src="{{ "/assets/images/pic08.png" | absolute_url }}" alt="Markdown Monster icon" width = "200" height = "150" />

<p>
Living in a time and age when every piece of our data is stored and analysed, the consumer advocacy group wondered what information retailers can gather and infer about consumers. Nevertheless, to answer their question, the group could only provide Detective Duck with information about a two year shopping spree of  the clients of an unknown shopping center located somewhere in the US. Based on this data, Duck was tasked with identifying possible links, if they exist, between demographic information (e.g. marital status, income, number of children, etc) and purchase patterns. In other words, he needed to find out how easy it is for retailers to infer a specific customer profile based on their shopping habits. This was crucial to the consumer advocacy group. Indeed, precise customer profiles can lead targeted marketing aimed at increasing consumers' spending habits, and also to a loss of privacy. Luckily, Detective Duck followed the autumn 2019 Applied Data Analysis course at the EPFL and trained his newly skills with diligence to this case.
</p>

<br/>
<hr/>
<!--CHAPTER 1: -->
<h4>Chapter 1. A rocky start to a rocky investigation.</h4> 
<p><em><strong>A Dunnhumby dataset.</strong></em></p> 

<p>
    The consumer advocacy group provided Detective Duck with a dataset owned by Dunnhumby, an American Data Science company. This included the results of a two years long study, over 2500 voluntary households. When looking at the dataset, Duck quickly realised that it was rather big and had a lot of miscellaneous information. Nevertheless, our favourite detective had learned that when faced with this kind of challenges, he has to start by pre-processing and cleaning the available information. For this, he kept only households which showed coherent and sufficient demographic data. Furthermore, he labelled all 10'000 products into precise grocery categories, as shown below. In this graph, Duck plotted the number of occurences per label for all the transactions. That is how he noticed that most transactions fell into five major labels : vegetables, meat & seafood, cookies & snacks & candy, dairy and beverages. This was not a major surprise to him. 
    
<img class="center" src="{{ "/assets/images/products_trans_newlabel.png" | absolute_url }}" alt="Markdown Monster icon" width = "900" height = "700" /> 
</p>

<p><em><strong>A good detective always gets to know his suspects.</strong></em></p> 

<p>
   Before starting to hunt for clues, Detective Duck needed know better the households participating to the study. Things started getting tricky for the first time in his investigation. Indeed, after cleaning the 2500 households studied by Dunnhumby, only 750 remained that provided their demographic information. At this moment, doubt started to arise in detective Duck's mind. The consumer advocacy group had provided him with a hard task. Undoubtetly, such a small dataset would cause troubles when trying to draw predictions. Duck regretted ever leaving his cozy pond. 

</p>

<img class="center" src="{{ "/assets/images/pic09.png" | absolute_url }}" alt="Markdown Monster icon" width = "300" height = "150" />
<p>
Still, Duck decided to extract the clients' main consumption patterns and to correlate them with their demographic features. For this, he developped several strategies that are explained below. </p>

<br/>
<hr/>
<!--CHAPTER 2: -->
<h4>Chapter 2. Profiling is not a piece of cake.</h4>

<p>
   Once the data was ready for analysis, Detective Duck was excited to face the real challenge: customer profile hunting. 
</p>

<p><em><strong> A hunt for correlations.</strong></em></p> 
<p>
   Detective Duck seeked for major correlation patterns in the whole data. After some coding, he produced the following matrix illustrating the strength of relation between demographic features, spendings and the products quantities for the most common labels. 
</p>

<img class="center" src="{{ "/assets/images/correlation-matrix1.png" | absolute_url }}" alt="Markdown Monster icon" width = "600" height = "400" />

<p>
From this, he learned that there is some high correlation between demographic information. Specifically, household size is highly correlated to the number of kids and marital status. This did not surprise Duck, any good detective could have deduced it. Nevertheless, he noted that most households with kids were married in this study. Furthermore, the mean and yearly spending were also correlated (0.7) with the different products quantities. This did not alarm Duck, as spending more usually means buying more products in a grocery store. Unfortunately, he could not find any direct link between demographics and product quantities. Unsatisfied with this result, he decided to further pursue the matter. Duck supposed that no correlation between labels and demographics could mean that the labels were not specific enough. Indeed, all households probably buy globally the same amounts in the categories of vegetables, meat, dairy products, etc. Thus, except for outliers with extreme diets, all households seem to buy from the same grocery categories. </p>

<iframe src='https://gfycat.com/ifr/AdmiredGlumBluebreastedkookaburra' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'></iframe>


<br/>
<hr/>
<p><em><strong> A duck in a random forest.</strong></em></p> 

<p>
Our favourite duck is not the kind of duck that gives up when discovering weak correlations. Thus, he decided to follow another path and to seek for help from Machine Learning, more specifically, Random Forests. He built a predictive model that would hopefully find things, he as a simple duck, could not. First, he fitted a decision tree on the monthly product quantities bought by all households with available demographic information. The results for this were regretfully bad. So bad that Duck could have just randomly set a random demographic parameter for each household and the result would have been better (e.g. the ROC AUC score barely exceeded the baseline score). The same occurred when fitting a random forest model. Thus, he concluded that, using only labels, there was not enough data to train a good machine learning model and infer satisfying customer profiles. Disappointed, he was however not surprised (see section <i>A good detective always gets to know his suspects.</i>), Duck resigned to pursue another investigation path, he had not yet said his last word.
</p>

<img class="center" src="{{ "/assets/images/pic10.jpg" | absolute_url }}" alt="Markdown Monster icon" width = "400" height = "200" />

<p><em><strong>Smart clustering by a strategic duck.</strong></em></p>   
<p>
Duck needed to change his plan of action as he had promised to deliver. Thus, he decided to search for typical grocery carts present in the data. From this, he hoped to be able to relate them to demographic parameters. To look for general carts, he pursued several ideas.
</p>


<p><i>Product clusters:</i></p>

<p>His first idea was to toss aside labels and focus on specific products. So, he looked to cluster households by the exact weekly product quantities they bought. He was hoping to identify different typical weekly shopping carts (e.g. a weekly shopping cart with bananas and cheddar cheese). To find the ideal number of clusters in the data, he used the elbow method and found a number between 5 and 9. </p>
<img class="center" src="{{ "/assets/images/elbow7.png" | absolute_url }}" alt="Markdown Monster icon" width = "500" height = "400" />

<p>
Duck used the k-means algorithm to finally create 7 households clusters. Duck set a threshold to determine if a product would characterize a certain cluster or not: The product had to be bought by at least a third of the households in the clutster (a very generous threshold) to be said as a product characterizing the cluster. Looking at the results, Duck saw that two clusters contained only a single household and that one contained around a 1000 but had no product in common. He dismissed those. Furthermore, the remaining clusters had either bananas or dairy as their caracteristic products. From this, Duck started to wonder if this dataset was a cruel joke that someone had played on him, or wether this shopping center was frequented by what seemed to be a troop of monkeys. Detective Duck concluded that even though the labels were too vague, clustering on products was probably too precise as there were several product IDs for the same type of product (e.g. 5 different milk IDs). So, though some households maybe bought the same weekly quantity of milk, because they bought a different brand, their carts were not assimilated as the same. 
</p>
  
<p>
<p><i>Department clusters:</i></p>

<p>
Barely recovered from his banana and milk experience, Duck's second idea was to look for clusters in the labels and departments of the products. Reminder, the department includes "Produce", "Grocery", "Drug and general merchandise", etc. After an SVD on the weekly average amount of products bought per deparment and on labels, the detective found that two dimensions explain 96% of total variance in the departments and 70% in the labels. So, he plotted the data along these two dimensions and colored it according to different demographic labels to search for clusters. See below, a 2D representation of the department and label data colored according to different demographics. 
</p>

<div class="row justify-content-md-center">
  <div class="column">
    <img class="center" src="{{ "/assets/images/notebook_images/departsvd1.png" | absolute_url }}" alt="Markdown Monster icon" width = "360" height = "250" />
  </div>
  <div class="column">
    <img class="center" src="{{ "/assets/images/notebook_images/departsvd2.png" | absolute_url }}" alt="Markdown Monster icon" width = "360" height = "250" />
  </div>
</div>

<div class="row justify-content-md-center">
  <div class="column">
    <img class="center" src="{{ "/assets/images/notebook_images/labelsvd1.png" | absolute_url }}" alt="Markdown Monster icon" width = "360" height = "250" />
  </div>
  <div class="column">
    <img class="center" src="{{ "/assets/images/notebook_images/labelsvd2.png" | absolute_url }}" alt="Markdown Monster icon" width = "360" height = "250" />
  </div>
</div>

<p>Though visually he could not find any cluster, he still wanted to be sure that none were still hidden. He decided to apply the heuristic elbow method for a cluster number from 2 to 20. This method found an ideal number of 4 clusters for departments but none for labels. Full of hope, Duck applied K-means with 4 clusters to the department data and had a closer look at them in the hope of discovering something.</p>

<!--
<div>
  <iframe id="igraph" seamless="seamless" src="https://plot.ly/~marvande/1.embed" frameborder="0" scrolling="no" onload="" allowtransparency="true"
></iframe>
</div>
-->

<div class="row">
  <div class="column">
    <img class="center" src="{{ "/assets/images/notebook_images/department_clusters.png" | absolute_url }}" alt="Markdown Monster icon" width = "400" height = "250" />
  </div>
  <div class="column">
    <img class="center" src="{{ "/assets/images/notebook_images/barclusters.png" | absolute_url }}" alt="Markdown Monster icon" width = "375" height = "300" />
  </div>
</div>

<p>Interestingly, Duck noticed that the clusters were influenced by the quantity of groceries bought. So, the only thing that seemed to distinguish households was how much groceries they bought weekly at this retailer. To see whether there were any other indicators in those clusters, Detective Duck decided to look at the biggest cluster in order to see whether there was any correlation within the cluster. Note: though there are around 1000 households in this cluster, to calculate correlation between labels, there is only demographic information for 22 of them. All correlation calculations between demographics and anything else were done with only 22 datapoints.
</p>

<img class="center" src="{{ "/assets/images/notebook_images/cluster4_correlation.png" | absolute_url }}" alt="Markdown Monster icon" width = "600" height = "400" />

<p>
To Duck's delight, some bigger correlations appeared within the cluster. Notably, within this cluster there seemed to be some indication of a link between the weekly quantity of dairy bought and the number of kids/household size. This reminds the detective of the weird dairy and banana clusters that appeared when evaluating products. These clusters could be an indicator that, when separating households according to how much they bought weekly at this retailer, one might get a better idea of their shopping patterns. And this way relate them better to their demographics. Nevertheless, to conclude anything solid, Duck would have needed way more demographic data. 
</p>


<p>
Though the correlation data had to be taken into account carefully because of the scarcity of demographic data. Not wanting to give up on his newly found clusters, Detective Duck decided to look at the proportion of label consumption for each cluster. He was interested to see if there was anything separating them except the quantity of weekly groceries bought. Disappointingly, the proportions seemed more or less similar. Duck suspected that this was due to the fact that, as seen previously, labels are too global and most households buy the same things. Instead of looking at average proportions, Duck suspected he should have looked at the proportions of outsiders in the clusters instead. But again, there was not enough data for that and our beloved detective was short on time. 
</p>

<div class="row">
  <div class="column">
    <img class="center" src="{{ "/assets/images/notebook_images/clusterprop_1.png" | absolute_url }}" alt="Markdown Monster icon" width = "375" height = "300" />
  </div>
  <div class="column">
    <img class="center" src="{{ "/assets/images/notebook_images/clusterprop_2.png" | absolute_url }}" alt="Markdown Monster icon" width = "375" height = "300" />
  </div>
</div>
<div class="row">
  <div class="column">
    <img class="center" src="{{ "/assets/images/notebook_images/clusterprop_3.png" | absolute_url }}" alt="Markdown Monster icon" width = "375" height = "300" />
  </div>
  <div class="column">
    <img class="center" src="{{ "/assets/images/notebook_images/clusterprop_4.png" | absolute_url }}" alt="Markdown Monster icon" width = "375" height = "300" />
  </div>
</div>

<!--CHAPTER 3: -->
<br/>
<hr/>
<p>
<h4>Chapter 3. A reassuring report to the Consumer Advocacy Group</h4>
<p>
<p>
After this investigation full of twists and turns, Duck's report to the C.A.G was the following: </p>

<p><i>
“Due to the results, there should be no cause for immediate worry. Though armed with extended data analysis ressources, I did not discover anything big from clients'shopping habits, at least not at the scale of this single retailer. To find anything signficant, retailers would need to build a clever data collection. So, to infer who their customers are, they would need to harvest a lot more demographic information of a way bigger and more diverse client sample. Indeed, globally households behave quite similarly, no matter their social class. The main danger right now, is retailers collecting personal shopping habits and targetting indivdually their clients. Nevertheless, it seems that it is hard (at least it was for me) to predict who you are.” </i></p>

<p><i>What Duck could have done better.</i></p>
<p>
The data collection the detective has analyzed might have been atypical. Since he did not have any information about the location nor the identity of the shopping center, he could not claim that it represented an average American grocery store. 
Moreover, the number of households who gave their demographic features was very limited. As accuracies of machine learning models highly rely on the dataset size, Duck stipulates that his results were probably biased by a too small dataset. 
Furthermore, he chose the product’s labels arbitrarily. They were set based on the common classes of food he personally knew. This could have been done wiht higher precision, based on existing labeling available or using classification based on machine learning. 
</p>
    
<p><i>An open investigation.</i></p>
<p>
To be completely re-assured, Duck advised the C.A.G to run a meta analysis among several shopping centers, in order to confirm or infirm his conclusions. The household set giving their personal data for each center should preferably be bigger and the products classification should be comparable in between the different grocery stores. 
<p>

<p>Good job detective Duck. But our favorite detective does not even hear us. The smart little guy is already on his way to a new investigation.</p>

<img class="center" src="{{ "/assets/images/ducktective_murder.png" | absolute_url }}" alt="Markdown Monster icon" width = "200" height = "150" />