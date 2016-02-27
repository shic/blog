---
layout:     post
title:      "Jekyll Comment System"
subtitle:   "Jekyll study path"
date:       2016-2-26 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
categories: Jekyll Basic
---

#Integration step by step
1 Generate code form https://disqus.com

2 Paste the code in _includes/disqus.html 

3 Set default comments value to "true" using "

	comments: true

4 Add a boolean in disqus.html to set if you want to have comments for a certain page/post

	{% if page.comments %}	
	<div id="disqus_thread"></div>
	<script>
	...
	</script>
	{% endif %}

5 Add disqus.html in post template: 

	{% includde disqus.html disqus_identifier=page.disqus_identifier %}
	Note: Replace includde to include
