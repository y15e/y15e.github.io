---
layout: post
title: "How to install mod_evasive to Apache2"
---
When I installed mod_evasive by following original README file, I got an error.

> Warning! dlname not found in /usr/local/httpd/modules/mod_evasive20.la.
> Assuming installing a .so rather than a libtool archive.

After googling, I found [this article](http://blog.enjoitech.jp/article/131) and solved this problem! Thank you Enjoi Blog!

```
#!/bin/sh

cd /usr/local/src

tar zxvf mod_evasive_1.10.1.tar.gz

cd mod_evasive

/usr/local/httpd/bin/apxs -c mod_evasive20.c

gcc -shared -o mod_evasive20.so mod_evasive20.o

sudo cp mod_evasive20.so /usr/local/httpd/modules/

sudo /usr/local/httpd/bin/apxs -ian mod_evasive20 mod_evasive20.la
```
