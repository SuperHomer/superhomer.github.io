---
layout: post
title:  "Deploy your Jekyll site with Github Pages"
date:   2022-03-20 12:31:50 +0100
categories: jekyll deploy github pages
---

With Github Pages, it is very easy and free to deploy static website. In this post, a jekyll blog will be deploy. Checkout the previous post about [creating a blog with Jekyll]({% post_url 2022-03-19-create-a-blog-with-jekyll-on-m1-mac %}). This method is straightforward but there are others.

## Create the repo on Github
The first step is to create a repo with this name: `<username>.github.io` and has public. Replace with your username (in lowercase). You can follow the steps [here](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll) to create a repo.

## Update the Gemfile
In the Gemfile of your Jenkyll site, comment the line containing `gem "jekyll", ...` by adding a `#` at the beginning of the line. Then, uncomment the line containing `gem "github-pages", ...` by removing the `#`.

## Add your site to your repo
For the last step, simply push your site on git:
```bash
$ git init
$ git add .
$ git commit -m "First commit"
$ git branch -M main
$ git remote add origin git@github.com:<YourUsername>/<username>.github.io.git
$ git push -u origin main
```
You can now go to the link to checkout that the site is correctly published: `https://<username>.github.io/`
