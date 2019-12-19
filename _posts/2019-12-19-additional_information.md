---
layout: post
title:  "Additionnal information about the analysis."
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
<h4>Chapter 0. Preface.</h4>
<p>
As in most cases, the people who collect the data are not the same as those who analyse them, and they are often not data analysis specialists. In Duck's investigation, it is not a different story. Thus, to be able to get useful information from the data, he first had to preprossess them, and search is a multitude of directions to get an idea of what he was manipulating.
See below the additionnal analysis he could not present in the main blog.
</p>

<!--CHAPTER 1: -->
<h4>Chapter 1. Preprocessing of the data.</h4>

<p><em><strong>Households</strong></em></p> 
<p>
As you saw in the main blog, Duck filtered out about one third of the households. Here, you will find the answer to your obvious question : "WHY?".
First of all, to analyse the relationship between the purchase habits and the demographic data, he had to drop the households from the transaction table for which the demographic data were not given.
Second, he tried to get an idea of the distributions. See below the graphs of the demographic information about the customers.
<p>

<img class="center" src="{{ "/assets/images/demographics_distribution.png" | absolute_url }}" alt="Markdown Monster icon" width = "600" height = "450" />

<p>
As he did, you can see that the demographic data is not distributed uniformly. Indeed:
<ul>
    <li>most of our households are between 35-54 years old.</li>
    <li>the majority of households have a size 1 or 2.</li>
    <li>most people earn between 35K and 75K (note that the average American income is 50K)</li>
</ul>

<p>
After that, he noticed some inconsistencies. His conclusions were the following:
<ul>
    <li>the marital status is always coherent with the household size and the number of kids. In these cases where the household composition is wrong, let's just discard that information.</li>
    <li>there are some incongruities in the household size / number of kids when the marital status is Single, so let's discard these entries.</li>
    <li>if the marital status is Unknown, we fall back on the household size / number of children information, so let's give the corresponding marital status, when it makes sense</li>
</ul>

<p><em><strong>Products</strong></em></p>

<p>
In the products table, there were originally 44 departments of products, and Duck noticed that some were redundant. He cleaned the departments and labels, and ended up with the following categories for the products, with the representation of each category in terms of number of products:
<p>
    
<img class="center" src="{{ "/assets/images/products_newlabel.png" | absolute_url }}" alt="Markdown Monster icon" width = "800" height = "600" />

<p>
Note that most of our products fall under processed foods and households.
<p>

<p><em><strong>Transactions</strong></em></p>

<p>
Duck found out that there were 2,595,732 transactions over the year, knowing that one transaction is one household which proceeds to checkout.
When he looked deeper into what products are sold in the transactions, he ended up with the following graph:
<p>

<img class="center" src="{{ "/assets/images/products_trans_department.png" | absolute_url }}" alt="Markdown Monster icon" width = "800" height = "600" />
    
<p>
Because he wanted to look at how much households spend on groceries, he decided to keep only transactions that are in the department of Groceries, Drug and General Merchandise, Produce Meat, Deli and Packaged meat.
<p>

<p>
After that, he wanted to go deeper and look at the purchase behaviour of the customers. Firts, he looked at the distribution of the number of purchases per year.
See below the graph he obtained:
<p>

<img class="center" src="{{ "/assets/images/distri_number_purchase.png" | absolute_url }}" alt="Markdown Monster icon" width = "800" height = "600" />

<p>
At this point, he suspected that about half of the households don't use this retailer as their principal retailer, because they buy less that once a week. But he wanted to explore more on this idea, and thought that looking at the spendings could give a good indication.
<p>
    
<img class="center" src="{{ "/assets/images/spending_vs_income.png" | absolute_url }}" alt="Markdown Monster icon" width = "800" height = "600" />

<p>
Indeed, when he plotted the average yearly and weekly spending against the income, he figured out that there are quite a lot of households who spend less than $50 a week, which seems too low for a weekly budget of full groceries as the weekly amount set by "Business insider" for the US is around $70.
In addition, according to the "Bureau of Labor statistics", each household should have spent at least around $2500 dollars per year. Households that spent less than that did not participate in the study fully and bought groceries elsewhere. He thus hypothesized that to be a "loyal" shopper, they should spend at least $2500 per year. But, when he wanted to filter out to keep only the loyal shoppers, he ended up with only 286 households left, which is really too low for a relevant analysis. 
His conclusion was : "let's keep everybody for now".
<p>
    
<p>
To complete his understanding of the data, he looked at the distribution of the participation to the study:
<p>
    
<img class="center" src="{{ "/assets/images/participation.png" | absolute_url }}" alt="Markdown Monster icon" width = "400" height = "300" />

<p>
You can observe that most households only participated between 20 and 80 weeks. Only 3 households did over 100 weeks. But for the same reasons as before, he decided to keep them anyway, because with the filtering he would not have had muwh to analyze.
<p>