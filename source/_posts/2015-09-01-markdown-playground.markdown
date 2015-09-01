---
layout: post
title: "Markdown Playground"
date: 2015-09-01 14:22:57 +0800
comments: true
categories: 
---

###Syntax

	``` [language] [title] [url] [link text]
	code snippet
	```
###Usage

	```
	$ git clone git@github.com:imathis/octopress.git # fork octopress
	```
```
$ git clone git@github.com:imathis/octopress.git # fork octopress
```
<!-- more -->
	``` ruby Discover if a number is prime http://www.noulakaz.net/weblog/2007/03/18/a-regular-expression-to-check-for-prime-numbers/ Source Article
	class Fixnum
	  def prime?
	    ('1' * self) !~ /^1?$|^(11+?)\1+$/
	  end
	end
	```
``` ruby Discover if a number is prime http://www.noulakaz.net/weblog/2007/03/18/a-regular-expression-to-check-for-prime-numbers/ Source Article
class Fixnum
  def prime?
    ('1' * self) !~ /^1?$|^(11+?)\1+$/
  end
end
```

{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}

{% codeblock Javascript Array Syntax lang:js http://j.mp/pPUUmW MDN Documentation %}
var arr1 = new Array(arrayLength);
var arr2 = new Array(element0, element1, ..., elementN);
{% endcodeblock %}

{% gist 9dd0f29acfa0d4622c40 %}

<!-- {% gist 1059334 svg_bullets.rb %}
{% gist 1059334 usage.scss %} -->