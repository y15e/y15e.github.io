---
layout: post
title: "Create a Blog Site with Jekyll on Docker"
---

This blog site is running on Jekyll with Docker on Amazon EC2. At first, I started to use GitHub Pages and learned how to write blog articles on Jekyll. But I wanted to run my blog on my own domain. So I decided to move my blog to this environment.


```
docker run --name d6er \
       --volume=/var/www/d6er.com:/srv/jekyll \
       -d jekyll/jekyll \
       jekyll serve --incremental
```