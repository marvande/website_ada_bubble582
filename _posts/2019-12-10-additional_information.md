---
layout: post
title:  "Additionnal information about the data story."
date:   2019-12-12
excerpt: "A story about shopping patterns."
image: "/assets/images/preprossessing.jpeg"
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
<h4>Preface.</h4>
<p>
As in most cases, the people who collect the data are not the same as those who analyse them, and they are often not data analysis specialists. In Duck's investigation, it is not a different story. Thus, to be able to get useful information from the data, he first had to preprossess them, and search in a multitude of directions to get an idea of what he was manipulating.

Please find below the additionnal analysis he could not present in his main report. 
</p>

<!--CHAPTER 1: -->
<h4>Chapter 1. Preprocessing of the data.</h4>

<p><em><strong>Households.</strong></em></p> 
<p>
As you saw in the main report, Duck filtered out about one third of the households. Here, you will find the answer to your obvious question : "WHY?".
First of all, to analyse the relationship between the purchase habits and the demographic data, he had to drop the households from the transaction table for which the demographic data were not given.
Secondly, he tried to get an idea of the distributions. See below the graphs of the demographic information about the customers.
<p>

<img class="center" src="{{ "/assets/images/demographics_distribution.png" | absolute_url }}" alt="Markdown Monster icon" width = "600" height = "450" />

<p>
From this he swa that the demographic data was not distributed uniformly. Indeed:
<ul>
    <li>most of our households were between 35-54 years old.</li>
    <li>the majority of households had a size 1 or 2.</li>
    <li>most people earned between 35K and 75K (note that the average American income is 50K)</li>
</ul>

<p>
After that, he noticed some inconsistencies. His conclusions were the following:
<ul>
    <li>the marital status was not always coherent with the household size and the number of kids. In the cases where the household composition was wrong, he discared the households. </li>
    <li>there were some incongruities in the household size / number of kids when the marital status was Single. He discarded those households. </li>
    <li>if the marital status was Unknown,he fell back on the household size / number of children information, so gave the corresponding marital status, when it made sense</li>
</ul>

<p><em><strong>Products.</strong></em></p>

<p>
In the products table, there were originally 44 departments of products, and Duck noticed that some were redundant. He cleaned the departments and labels, and ended up with the following categories for the products, with the representation of each category in terms of number of products:
<p>
    
<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~marvande/6.embed" height="525" width="100%"></iframe>

<p>
Note that most of our products fell under cookies and snacks, meat and households.
<p>

<p><em><strong>Transactions</strong></em></p>

<p>
Duck found out that there were 2,595,732 transactions over the year. When he looked deeper into what products were sold in the transactions, he ended up with the following graph:
<p>

<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~marvande/17/#/" height="525" width="100%"></iframe>

    
<p>
Because he wanted to look at how much households spent on groceries, he decided to keep only transactions that were in the department of Groceries, Drug and General Merchandise, Produce Meat, Deli and Packaged Meat.
<p>

<p>
After that, he wanted to go deeper and look at the purchase behaviour of the customers. Firts, he looked at the distribution of the number of purchases per year.
<p>

<img class="center" src="{{ "/assets/images/distri_number_purchase.png" | absolute_url }}" alt="Markdown Monster icon" width = "800" height = "600" />

<p>
At this point, he suspected that about half of the households did not use this retailer as their principal retailer, because they bought there less that once a week.To explore this further, he thought that looking at the spendings would give a good indication.
<p>
    
<img class="center" src="{{ "/assets/images/spending_vs_income.png" | absolute_url }}" alt="Markdown Monster icon" width = "800" height = "600" />

<p>
Indeed, when he plotted the average yearly and weekly spending against the income, he figured out that there were quite a lot of households who spent less than $50 a week, which seemed too low for a weekly budget of full groceries as the weekly amount set by "Business insider" for the US is around $70.
In addition, according to the "Bureau of Labor statistics", each household should have spent at least around $2500 dollars per year. Households that spent less than that did not participate in the study fully and bought groceries elsewhere. He thus hypothesized that to be a "loyal" shopper, they should have spent at least $2500 per year. But, when he wanted to filter them out to keep only the loyal shoppers, he ended up with only 286 households left, which was really too low for a relevant analysis. 
His conclusion was : "let's keep everybody for now".
<p>
    
<p>
To complete his understanding of the data, he looked at the distribution of the participation to the study:
<p>
    
<img class="center" src="{{ "/assets/images/participation.png" | absolute_url }}" alt="Markdown Monster icon" width = "400" height = "300" />

<p>
He observed that most households only participated between 20 and 80 weeks. Only 3 households did over 100 weeks. But for the same reasons as before, he decided to keep them anyway, because with the filtering he would not have had much to analyze. And that's the story of his pre-processing.
<p>