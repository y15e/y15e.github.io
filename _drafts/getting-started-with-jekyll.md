---
layout: post
title: "Getting started with Jekyll"
---

$ gem install jekyll bundler
```
WARNING:  You don't have /home/d6er/.gem/ruby/2.4.0/bin in your PATH,
          gem executables will not run.
```

$ vi ~/.profile
```
PATH="$HOME/.gem/ruby/2.4.0/bin:$PATH"
```

$ source ~/.profile

$ printenv PATH

$ jekyll new d6er.com

$ tree d6er.com
```
d6er/
├── about.md
├── _config.yml
├── Gemfile
├── Gemfile.lock
├── index.md
└── _posts
    └── 2017-04-16-welcome-to-jekyll.markdown

1 directory, 6 files
```

$ cd d6er.com

$ git init

$ git add .

$ git commit -m "Initial commit" .

