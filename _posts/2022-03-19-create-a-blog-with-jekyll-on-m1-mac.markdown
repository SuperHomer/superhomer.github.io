---
layout: post
title:  "Create a blog with Jekyll on M1 Mac"
date:   2022-03-19 12:40:00 +0100
categories: jekyll setup configuration m1 blog
---

Whenever you want to install some stuff on M1 Mac, it can very easy or not. With M1, you can find yourself strugling and waste time for something very basic. Like the installation of Jekyll to build this awesome blog 😁 .

## Table of Contents
1. [Prerequisites](#prerequisites)
1. [Install ruby](#install-ruby)
1. [Create a Jekyll site](#create-a-jekyll-site)
1. [Run Jekyll server](#run-jekyll-server)
1. [Sources](#sources)

## Prerequisites
- Homebrew installed

## Install ruby
First but not the least, ruby comes pre-installed on the M1 Mac (v2.6) and you have to install a newer version to be able to run Jekyll.
> Don't use pre-installed ruby version !

Install ruby:
```bash
$ brew install ruby
$ echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
```
After that, you must quit your terminal.

Run the terminal again and check the ruby version installed:
```bash
$ ruby -v
ruby 3.1.1p18 ...
```
Make sure the version is no more v2.6.

## Install Jekyll
```bash
$ gem install --user-install bundler jekyll
$ echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.zshrc
```
Replace the `X` with your ruby version installed.


## Create a Jekyll site
```bash
$ jekyll new blog
```

You should get something like this:
```bash
.
└── blog
    ├── 404.html
    ├── Gemfile
    ├── Gemfile.lock
    ├── _config.yml
    ├── _posts
    ├── _site
    ├── about.markdown
    └── index.markdown
```

## Run Jekyll server
```bash
$ cd blog
$ bundle exec jekyll serve --livereload
```
The `--livereload` option is not mandatory. It is for hot relaod when you update the site.

You might enconter an error with the latest command like this one:
```bash
/Users/yourusername/.gem/ruby/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve/servlet.rb:3:in `require': cannot load such file -- webrick (LoadError) ...`
```

You can fix it with this command:
```bash
$ bundle add webrick
```
After that, you ca rerun the previous command to run the server and go to: <http://127.0.0.1:4000> 

## Sources
- <https://www.section.io/engineering-education/build-a-jekyll-site/>
- <https://github.com/BillRaymond/install-jekyll-apple-silicon/blob/main/README.md>
- <https://talk.jekyllrb.com/t/load-error-cannot-load-such-file-webrick/5417/5>