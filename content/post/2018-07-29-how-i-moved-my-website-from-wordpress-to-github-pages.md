---
title: How I moved my website from Wordpress to GitHub Pages
author: Justin Bagley
date: '2018-07-29'
slug: how-i-moved-my-website-from-wordpress-to-github-pages
categories:
  - website
  - Wordpress
  - GitHub
  - GitHub Pages
  - Bootstrap
tags:
  - Wordpress
  - GitHub
  - R
  - Markdown
  - kramdown
  - HTML
  - Bootstrap
  - Bootstrap 4
  - code
  - development
  - migration
  - jekyll
  - hosting
  - academic
  - website
  - exitwp
---

During my PhD, I created a <a href="https://www.elsevier.com/connect/creating-a-simple-and-effective-academic-personal-website">personal academic website</a> built with <a href="https://wordpress.com">Wordpress</a> and hosted by 
<a href="https://www.hostgator.com">HostGator</a> in order to establish my online presence. I then started blogging here and there 
about software programs, and eventually ```R``` code etc., that I was using or found helpful when conducting evolutionary genetic analyses for my previous or ongoing collaborations.

That all started around seven years ago...

I could write a lot about what I learned from using Wordpress (e.g. basic CSS and PHP) and maintaining a dynamic site that started drawing >2000 visitors a month with shared interests in Bayesian evolutionary analysis or molecular clocks. I even had to increase my plan at HostGator to accomodate all the traffic I was getting. People were becoming more interested in my research too. But I won't write about that now. I'll just say that it took _a lot of effort_ to keep the Wordpress site updated and looking and running smoothly. _It seemed that every couple of days, I had to update those pesky Wordpress plugins or my site would slow down!_ I did come to enjoy the site and I liked the way that it looked (see _below_).

<img src="/images/wordpress_site_scrnsht1.png" title="Justin's previous Wordpress site" alt="Justin's previous Wordpress site" width="700px"></img>

Fast forward to today, during the prime time of my postdoc years...

I now have a lot more research experience as well as coding and analysis skills. I've enjoyed learning bioinformatics and adapting to new genomic approaches and ways of analyzing massive amounts of genetic data. With this has come more regular coding and usage of <a href="https://github.com">GitHub</a>, which breeds greater awareness of who is doing what, the tools and coding approaches people are using, how to solve coding problems or make pipelines, and along with that the ways that people are coding and hosting their _websites_ (e.g. for research projects or for software distributions).

## GitHub Pages & jekyll

Then, surprisingly recently, I learned about <a href="https://pages.github.com">GitHub Pages</a> all because of <a href="https://jekyllrb.com">jekyll</a>.

After seeing GitHub Pages-hosted sites powered by jekyll cropping up from several other biologists in my field that I just happened to be checking out or to run across online (e.g. Erik Enbody's site <a href="https://erikenbody.github.io">here</a> and Karl Broman's site <a href="https://kbroman.org">here</a>), my interest was piqued.

I learned what jekyll was (homepage below) and that GitHub Pages not only provided a free platform, but also provided free site hosting for your user account and all of your project repositories! #awesome!

<img src="/images/jekyll_fpg.png" title="jekyll home page" alt="jekyll home page" width="700px"></img>

I also read about the benefits of switching to a static site, as well as the experiences of several developers in migrating from 
Wordpress to jekyll/GitHub Pages. See for example, Daniel Takeshi's <a href="https://danieltakeshi.github.io/2015/05/14/moved-to-jekyll/#fnref:commands">post</a>, or Tomomi Imura's post about this topic <a href="https://girliemac.com/blog/2013/12/27/wordpress-to-jekyll/">here</a>. Also I also read Igal Tabachnik's post <a href="https://hmemcpy.com/2016/06/getting-with-the-times-migrating-from-wordpress-to-github-pages-with-hexo/">here</a> about using Hexo for this purpose.

You could say I was inspired.

Ultimately, some of what the developers were suggesting in detailed posts above seemed out of reach for me, or too time consuming given my schedule. But I saw several paths open up to me. 

I immediately went to Wordpress and backed up my site. I downloaded the backup. I then went to HostGator and backed up everything. Now all of my files were on my local machine. I needed to experiment with my master GitHub Pages site, which for me would be https://justinbagley.github.io by default (general form is "\<username\>.github.io"); but I also knew that I wanted to change this to point to my custom domain owned through HostGator--that of my previous/existing site, justinbagley.org. I realized too that my existing Wordpress/HostGator site security seemed lower than expected, as I had not been using the safer "https" domain that would be available to me instantly on GitHub, only "http". 

I started with jekyll and twitter bootstrap. I cloned <a href="https://github.com/kbroman/kbroman.github.io">Karl Broman's website repo</a> and modified my html files from Wordpress (e.g. my about, research, and publications pages--three important pages for personal academic websites), changing their html formatting to Markdown using <a href="https://github.com/thomasf/exitwp">exitwp</a> and my own modifications. I read through Karl's helpful <a href="https://kbroman.org/simple_site/">"simple site" tutorial</a> and related <a href="https://kbroman.org/tutorials.html">tutorials</a>. I would be uploading Markdown files and they would be converted to HTML with <a href="https://kramdown.gettalong.org/documentation.html">kramdown</a>. How great! Screenshot of about page looked like this:

<img src="/images/kbroman_style_site.png" alt="Justin's jekyll twitter bootstrap site, based on code from K Broman" width="700px"></img>

I did the whole thing in a day or two, and then realized I wanted the most up-to-date bootstrap code, <a href="getbootstrap.com">Bootstrap 4</a>, and twitter bootstrap theme seemed to be using bootstrap akin to v2 or v3. Karl's setup was awesome, and I liked the CSS, the simple portfolio styling, and the navbar look. It was aslo _responsive_. _But something was missing..._

## Bootstrap 4

<a href="http://getbootstrap.com"><img src="/images/Bootstrap_logo.png" alt="Bootstrap 4" width="300px"></img></a>

At the stage I was in, I needed to convert some more complex HTML pages I had to Markdown but didn't want to fool with any more conversions. I wanted to use Bootstrap 4 functionality and Javascript plugins. I said, 

>_"Forget it. I need another test just with Bootstrap, then to make the comparison. If I build ground-up in Bootstrap, then I can modify the existing HTML with Bootstrap headers and footers and classes. I'll be closer to the moving edge and my code will go out of date later rather than sooner."_
>

I backed up and renamed my newly minted GitHub pages repo and started over with a skimming of Bootstrap 4 documentation and a smattering of Bootstrap example code and starter templates such as those in <a href="https://getbootstrap.com/docs/4.0/examples/">Examples</a>, and at <a href="https://startbootstrap.com">Start Bootstrap</a>. It hurt, but I picked a 1-column portfolio template and started building. I redid the pages I had in HTML, customized the CSS so it was more like Karl's (which seemed familiar somehow, almost the way I would have done it), and failed miserably at adding a client-side search engine with <a href="http://www.tipue.com/search/">Tipue Search</a>----to date, a \*big\* waste of my time that I haven't fully rooted out/deleted from site but that never worked for me. I made custom search bars with Google Custom Search. I redid the subnav bars and worked to finish the longer HTML pages from my previous site that I hadn't had time to add to the jekyll twitter bootstrap incarnation from the day before. I also figured out how to do dropdown menus and added an embedded PDF version of my <a href="https://justinbagley.org/pages/cv.html">Curriculum Vitate, or "CV"</a>, which a year or two ago was something I only thought I could do with a Wordpress plugin (boy, was I wrong).

And voila! My new site was born!

_Then came the custom domain issue..._

## Custom domain, sitemaps, etc.

I followed the GitHub Help instructions for <a href="https://help.github.com/articles/using-a-custom-domain-with-github-pages/">"Using a custom domain with GitHub Pages"</a>, which was nicely done and pretty straightforward. I first added the custom domain at GitHub Pages. I then went to my HostGator CPanel and found the area for editing DNS zones. I scrapped the old A name listing and followed the GitHub Pages instructions for adding four new A names, and checking for any conflicts. I gave the change 24 h to fully register.

Next, I claimed and secured my site using the new free security app <a href="https://keybase.io">Keybase</a>, and Google. This means that I put Keybase and Google authentication code into my website repository on GitHub, verifying myself as the owner of the site.

<a href="https://keybase.io"><img src="/images/keybase_logo.png" alt="Keybase" width="250px"></img></a>

I then made new site maps and added them to Google through my <a href="https://www.google.com/webmasters/tools/home?hl=en>Google Search Console</a> (webmasters tools). I used the sitemap functions in a free version of <a href="https://www.screamingfrog.co.uk">Screaming Frog</a> for this, and edited the sitemap by hand. I also tested several free online sitemap generators. I am still experimenting with those and options to improve my sitemap and make a better-looking HTML sitemap for user convenience. In the end the 500 page limit of the SF free trial proved too restrictive; so I wound up using the 30-day free trial of <a href="https://techseo360.com">TechSEO360</a> for creating new/final sitemaps for my blog and website.

**_Overall_, my new website is now up at my custom domain https://justinbagley.org, is super fast loading, and is hosted through GitHub Pages for _free_!** Here's a screenshot of the frong page:

<a href="https://justinbagley.org"><img src="/images/justinbagley.org_scrnsht.png" alt="Justin's new Bootstrap 4 GitHub Pages website" width="800px"></img></a>

I was also able to avoid jekyll or Hugo themes that look good now but that I might not be happy with later on, and instead go with a simple Bootstrap 4 look for my site that has responsive characteristics that I wanted, and which I feel have staying power. I also got the satisfaction of learning and using among the most up-to-date methods for publishing your own website online, including probably the most popular front-end platform. In the end, make no mistake that I will be in a continued process of maintaining, updating, and improving my site, and so some of these things are subject to change.

_But, as long as I stay with GitHub Pages, at least I will never have to update Wordpress plugins or PHP *ever* again..._


~J
