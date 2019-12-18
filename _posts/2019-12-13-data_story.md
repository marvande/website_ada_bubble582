---
layout: post
title:  "Tell me what you buy, I will tell you who you are. A data story."
date:   2019-12-12
excerpt: "A story about shopping patterns."
image: "/assets/images/pic07.jpg"
---

## Preface: 
Due to rumours about the troublesome ability of shopping centers to infer consumer information based on their shopping patterns, a private investigator, detective Duck, was hired by a consumer advocacy group to investigate the matter. Here are the details of his investigation. 

<style>
    .img-container{
        text-align: center;
    }
</style>
<body>
<div class = 'img-container'>
<img src="{{ "/assets/images/pic08.png" | absolute_url }}"
    alt="Markdown Monster icon" width = "200" height = "300" />
</div>
</body>

Living in a time and age where every piece of our data is stored and analysed, the consumer advocacy group wonders what information retailers can gather and infer about consumers. To answer their question, detective Duck only gets information about a two year shopping spree of a group of 2500 clients of an unknown shopping center in the US. Based on this data, he seeks to identify possible links, if they exist, between demographic information (e.g. marital status, income, number of children, etc) and  purchase patterns. In other words, he would like to see how "easy" and how precise it is for retailers to infer a specific customer profile based on what their shopping habits as this could lead to easy targeted marketing. Luckily, detective Duck has followed the autumn 2019 Applied Data Analysis at the EPFL and counts on applying his newly aquired knowledge to this case. 

## Chapter 1. A rocky start to a rocky investigation. 

**A Dunnhumby dataset.** QW

The dataset detective Duck was provided by the consumer advocacy group, from now on referred to as the C.A.G, is owned by Dunhumby, which is an american data science company. This dataset includes the results of a two years long study, over 2500 voluntary households. Detective Duck knows that companies use harvested data to perform targeted marketing, but using his skills in data analysis, he plans to find out exactly what can be found out about clients. He expects to find that consumption habits will be influenced by demographic characteristics. For example, he suspects that the income category will influence the amount and price range of groceries bought weekly. 

*Preprocessing.*

When facing a huge amount of data, detective Duck has learnt to start by preprocessing and cleaning the available information to hunt for clues. For this, he kept only households which portrayed coherent and sufficient demographic data and tried to label products into precise categories that made sense. A challenge he faced doing this was that on 2500 households, demographic information was only provided for 780. Of these, around 750 were left after cleaning. At that moment, suspicions started to arise in detective Duck's mind that this might cause troubles. Nevertheless, after a long night of working and cursing, the data was finally usable and analysable. 

<style>
    .img-container{
        text-align: center;
    }
</style>
<body>
<div class = 'img-container'>
<img src="{{ "/assets/images/pic09.png" | absolute_url }}"
    alt="Markdown Monster icon" width = "400" height = "300" />
</div>
</body>

Now detective Duck is faced with the real challenge. He aims to try and extract the main consumption patterns of the clients and correlate them to their demographic features. For this, he developped several strategies as the investigation turned out to be harder than he tought when venturing into this case. Looking at the data, he quickly regretted ever leaving his cozy pond. 


Products data
After families selection we still need to look at what they buy. Our 750 families had access to a total of 92353 different products in their shopping center. These products are defined by their department (the place at which we find them) and by two different and non standard descriptive words sequences (commodity and sub-commodity). To be able to classify these products we created a function that compares both the commodity and the sub-commodity to a list of expressions from the lexical field of the grocery. Each expression was associated to a certain grocery category. Since the products' descriptions are atypical, we gave them a "score of similarity" with the expressions in the list. The highest score, above a certain threshold determines the label of the product. We used the Fuzzywuzzy library to calculate this score. Fuzzywuzzy is based on Levenshtein Distance to calculate the differences and similarities between string sequences. 


