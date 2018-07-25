---
title: Picking a custom search engine for your website
author: Justin Bagley
date: '2018-07-25'
slug: picking-a-custom-search-engine-for-your-website
categories:
  - website
  - code
  - software
  - development
tags:
  - website
  - development
  - search
  - search engine
  - free
  - API
  - open source
  - stackoverflow
  - software
  - bootstrap
---

_First, if you'd like to and see this blog entry in its original context, then read my original <a href="https://stackoverflow.com">stackoverflow</a> answer <a href="https://stackoverflow.com/questions/42247025/google-custom-search-engine-alternatives">here</a>._

So, according to blogdown authors (<a href="https://bookdown.org/yihui/blogdown/">Xie et al. 2018</a>), it's been said before that,

>_"If you don’t have a website nowadays, you don’t exist"_
>--Carlos Scheidegger.

A quick search online returns blog posts and sites with several variations on this them (e.g. <a href="https://www.capgemini.com/2010/01/if-you-are-not-in-google-you-dont-exist/">here</a> and <a href="https://checkin.hrs.com/en/if-you-re-not-online-you-don-t-exist-interview-how-well-equipped-is-the-hotel-industry-for-the-digital-era">here</a>) acknowledging the axiomatic importance of an online presence these days. 

Recently, I decided to rewrite my personal academic <a href="https://justinbagley.org">website</a>, a site that I had based on Wordpress (with only two theme changes!) from 2011 to earlier in 2018, in <a href="https://getbootstrap.com">Bootstrap 4</a>. I will write a separate blog post on how I made the transition, which was a major step towards _getting with the times_ for me, and fortunately not too painful.

**The present post is about search engines...**

Specifically, while redoing my site, I realized that I would have to find/write code, or install plugins, to customize my site and make it more interactive. One of the first things I realized would not be automatically available to me (as it was in Wordpress themes) was a functional search bar. Thus the search for hopefully easy, client-side search engine code began. During this process, I've learned about at least three different classes of options from a development standpoint--outsourced (custom), back-end (requiring a server), and client-side (no server). And I've also found several options listed _below_, which we can divide into paid _versus_ free/open-source options:

**1. Paid or Free-trial-with-premium options:**

These options are generally limited to a couple of hundred pages and 1000-2000 page views per month, and the free versions will crawl your site on a sparse timetable (e.g. monthly) and provide limited functionality. Paid versions are IMHO _very expensive_ and more appropriate for business/company sites (websites that generate income and have large numbers of visitors). All of these intend to be simple and scalable for the average user, and to solve additional problems other than search (e.g. related to SEO).

 - <a href="https://www.cludo.com/site-search-features/">Cludo Site Search</a>
 - <a href="https://www.algolia.com/products/search">Algolia Search</a>
 - <a href="https://swiftype.com/site-search">Swiftype Site Search</a>
 - <a href="https://aws.amazon.com/cloudsearch/">Amazon Cloudsearch</a>

**2. Free/open source custom search options:**

 - <a href="http://lucene.apache.org/solr/">Solr</a> - an Apache project built on Apache Lucene (_requires a server_ and working with APIs; see system requirements in the documentation<a href="http://lucene.apache.org/solr/guide/7_4/solr-tutorial.html">here</a>, specifically <a href="https://lucene.apache.org/solr/7_4_0//SYSTEM_REQUIREMENTS.html">here</a>)
 - <a href="https://developers.google.com/custom-search/json-api/v1/overview">Google Custom Search JSON API</a> - integrates with Custom Search Engine and allows obtaining search results without ads
 - <a href="http://www.tipue.com/search/">Tipue Search</a>, jQuery site search code which is meant to be used with json files built with their <a href="http://www.tipue.com/beaty/">Beaty</a> tool
 - <a href="http://elasticlunr.com">Elasticlunr.js</a> - full text site search engine written in Javascript (requires working with configuration files and APIs)

**My choice**

In the end, I decided to start with <a href="https://cse.google.com/cse/">Google Custom Search</a> free edition (with Google's ads/promotions at the top of my search results; you can pay to have them remove the advertisements), while using test pages to try out other options. By doing this, I've been able to quickly and rather painlessly add custom search bars to the footer of all pages for my website that search only my site and my blog. IMHO, I think the result is very resourceful, easy to find on page (obvious to reader), and does not interfere with my nice permanent or sticky top-navbar designs. 

My next step is that I am planning to test <a href="http://elasticlunr.com">elasticlunr.js</a> to provide a fully client-side search option. I would love to hear from others who have implemented elasticlunr about their experiences, or from anyone who has encountered a better client-side option.

Good luck!

~J

**References**

Xie Y, Thomas A, Hill AP (2018). Blogdown: creating websites with R markdown. CRC Press. Available at: https://bookdown.org/yihui/blogdown/.