---
layout: post
title: "mod_wsgi installation problem"
---

When I tried to install mod_wsgi-3.3, make install failed.

> Warning! dlname not found in /usr/local/httpd-2.2.16/modules/mod_wsgi.la.
> 
> Assuming installing a .so rather than a libtool archive.
> chmod 755 /usr/local/httpd-2.2.16/modules/mod_wsgi.so
> chmod: cannot access `/usr/local/httpd-2.2.16/modules/mod_wsgi.so': No such file or directory
> apxs:Error: Command failed with rc=65536
> .
> make: *** [install] Error 1
