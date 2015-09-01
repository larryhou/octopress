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

{% gist 4321346 %}