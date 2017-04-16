---
layout: post
title: "Add Google Analytics Tracking Code On Github Pages With Jekyll"
---

You can embed disqus comment form by following step.

1. Get a tracking code from Google Analytics "Tracking Info" section of your PROPERTY.

2. Put the html code into _includes/google-analytics.html file.

3. Add {% raw %}{% include google-analytics.html %}{% endraw %} at before </body> tag of _layouts/default.html.

**_includes/google-analytics.html**

```
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-58185705-1', 'auto');
  ga('send', 'pageview');

</script>
```
