---
layout: post
title: "Add Disqus comment form on github pages with Jekyll"
---

Disqus comment form can be embedded with following steps.

1. Get "Universal Code" from Disqus admin page.

2. Put the html code into _includes/disqus.html file.

3. Add {% raw %}{% include disqus.html %}{% endraw %} at bottom of _layouts/post.html.

**_includes/disqus.html**

```
<div id="disqus_thread"></div>
<script type="text/javascript">
/* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
var disqus_shortname = 'y15e'; // required: replace example with your forum shortname

/* * * DON'T EDIT BELOW THIS LINE * * */
(function() {
  var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
  dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
  (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
```
