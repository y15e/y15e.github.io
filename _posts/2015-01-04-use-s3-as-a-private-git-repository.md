---
layout: post
title: "Use S3 as a private git repository"
---
There are many blog posts on the internet about this topic.
This is just a note of linux commands.

**Setup**

1. Download [jgit.sh](https://repo.eclipse.org/content/groups/releases//org/eclipse/jgit/org.eclipse.jgit.pgm/3.6.0.201412230720-r/org.eclipse.jgit.pgm-3.6.0.201412230720-r.sh) and rename it to jgit, then `chmod +x jgit`.

2. Create a S3 bucket for git private repositories.
Notice: The bucket is created in "US Standard" region by default.

```
$ s3cmd mb s3://my-bucket-for-git-repo
```

**For each git repository**

```
$ cd project1
$ git init
$ git add .
$ git commit -m "Initial commit"
$ git remote add origin amazon-s3://.jgit@my-bucket-for-git-repo/project1.git
$ jgit push origin master
```
