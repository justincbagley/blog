---
title: How I moved my blog from Wordpress to a blogdown blog deployed by Netlify
author: Justin Bagley
date: '2018-08-01'
slug: how-i-moved-my-blog-from-wordpress-to-a-blogdown-blog-deployed-by-netlify
categories:
  - website
  - blog
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

<!--# How I moved my blog from Wordpress to a blogdown blog hosted on GitHub Pages and deployed by Netlify-->

In a recent post, I detailed how I moved my main website [from Wordpress to GitHub Pages](https://justinbagley.rbind.io/2018/07/29/how-i-moved-my-website-from-wordpress-to-github-pages/) with HTML in a <a href="https://getbootstrap.com">Bootstrap 4</a> front-end. This post represents the next installment in this series and will focus on how I moved my blog from the Wordpress site to <a href="https://pages.github.com">GitHub Pages</a>, and specifically to a blogdown-style blog hosted on GitHub and deployed by <a href="https://www.netlify.com">Netlify</a>. I don't currently have time to produce a _more detailed_ post now, but I give notes below on the 10 main steps that I took during this process. 

## 10 Steps

1. **Backup Wordpress** blog using backup plugin, and by downloading an archived version of my 'public_html' folder.

2. **Download/install and use <a href="https://github.com/thomasf/exitwp">exitwp</a>** to convert all HTML blog post pages into Markdown.
 - _Time-consuming step:_ Editing image links, metadata, and other aspects of the converted Markdown files by hand (several hours, over 2 days).

3. **Create 'blog' GitHub repository** _without_ default README.md file.
 - Leave at 'master' branch (not really important for my purposes, since I will use a custom domain, but this means the blog would be at https://justinbagley.github.io/blog/ under the default scenario).

4. **Make GitHub Pages site from blog repository** and make local README file that will eventually give details and license information.
 - Choose and indicate Creative Commons license for text/content, and prepare local MIT License file ('LICENSE') to cover all code on blog.

5. **Follow instructions on Alison Permanes Hill's (APH) <a href="https://alison.rbind.io/post/up-and-running-with-blogdown/">"Up and running with blogdown" blog post</a>, starting with step 5**:
 - **APH step 5.** Install blogdown and Hugo in ```R```. (I also installed Hugo locally.)
 - **APH step 6.** Build site in RStudio with default Hugo Lithium theme; set configuration; make new blog post.
 - **APH step 7.** Deploy to Netlify--involved creating Netlify account.
 - **APH step 8.3.** '*rbind.io' custom domain--requested custom domain 'justinbagley.rbind.io' from <a href="https://github.com/rbind/support/issues">rbind support on GitHub</a>, waited for custom domain to be fixed on rbind's side, and added custom domain in Netlify and GitHub Pages.

6. **Edit css, HTML, and blog posts, and add all previous blog posts to the /content/post/ folder.**
 - Inspiration for css was kbroman.org and my website jbagley.org.

7. **Set options to enforce "https://" URL**, first at Netlify, then at GitHub pages.

8. Add **Google and Keybase authentications** (files) for site.

9. **Add new posts and content by creating each new post (usually) in RStudio**, then editing in RStudio or GitHub.

10. **Update sitemap and add to Google Search Console.**

This was a little time consuming, because it involved editing the converted Markdown files by hand, familiarizing myself with blogdown (i.e. reading the book documentation), studying other blogdown blogs like Karl's <a href="https://kbroman.org/blog">blog</a>, and solving some other issues (e.g. with Netlify). I am still thinking of ways to improve what I have, but I really like my new blogdown blog. And the beauty of it is of course that it will allow me to embed math and generate plots from ```R``` code within a post--two awesome advantages of blogdown. 

~J
