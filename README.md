# Dev-Laurin.github.io
A github pages website to showcase my prior work. A portfolio/blog. 

[View Live](https://dev-laurin.github.io/)

## Add an article
1. Create a new markdown file in _posts with the posting/creation date in the name: 2021-10-14-example-article.md
2. Add the following section at the top. Choose either work or personal for the project category. 
```md
---
layout: post
author: Laurin
title: An Example Article
img: assets/images/example.PNG
description: An example article for my future self. 
tags: markdown example
category: work
---
```
3. Place your main image for the post in assets/images. 
## Run locally
### Setup - Install dependencies
`bundle install` 
### Start Server
`bundle exec jekyll serve` 
### Preview
`http://localhost:4000`

## Future Work
1. Create a search / filter at the top, including to organize by date ranges, categories, tags, languages. 
2. Make the About Me more interesting?
3. Create snap-to navigation for the article on the right so users can go to specific sections if the article/post is long. 
4. Create project timelines and post-reflections? (pre conditions / initial design, issues, re-writes, initial timeline vs real timeline, post-reflection)
5. Project use / outcomes: Users/day, Users/month?
6. Prettier / more professional