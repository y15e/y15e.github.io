---
layout: post
title: "How to install mod_evasive apache module"
---

I got an error when I installed mod_evasive by following original README.

> Warning! dlname not found in /usr/local/httpd/modules/mod_evasive20.la.
> Assuming installing a .so rather than a libtool archive.

I found [this article](http://blog.enjoitech.jp/article/131) and the issue has been solved.

```
$ cd /usr/local/src
$ tar zxvf mod_evasive_1.10.1.tar.gz
$ cd mod_evasive
$ /usr/local/httpd/bin/apxs -c mod_evasive20.c
$ gcc -shared -o mod_evasive20.so mod_evasive20.o
$ sudo cp mod_evasive20.so /usr/local/httpd/modules/
$ sudo /usr/local/httpd/bin/apxs -ian mod_evasive20 mod_evasive20.la
```
