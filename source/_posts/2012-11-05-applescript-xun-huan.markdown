---
layout: post
title: "AppleScript：循环"
date: 2012-11-05 01:07
comments: true
categories: 
---
AppleScript是一个比较接近自然语言脚本语言，习惯了传统编程的程序猿一时还真难以适应这种表达和思考方式，不过了解其中的规律后，你就会发现AppleScript其实是一种非常容易、非常生活化的编程语言。在这篇文章里面着重介绍循环控制指令。
<!--more-->

在Applescript里面实现循环效果就要使用<code>repeat</code>命令，结合不同的关键字又有不同的循环控制效果。尽管如此，在任何时候想结束循环的地方使用<code>exit</code>命令则可随时退出。

### repeat  
该命令执行无限循环，直至执行遇到<code>exit [repeat]</code>命令
{% codeblock repeat lang:applescript %}
set var to 0
repeat
	if var ≥ 100 then
		exit repeat
	end if
end repeat
{% endcodeblock %}


### repeat *n* [times]
该命令执行***n***次循环，除非遇到<code>exit [repeat]</code>命令
{% codeblock repeat ... times lang:applescript %}
set var to 0
repeat 5 times
	set var to var + 1
	log var
end repeat
{% endcodeblock %}

### repeat until *condition*
该命令执行循环直至***until***条件成立，除非遇到<code>exit [repeat]</code>命令
{% codeblock repeat until ... lang:applescript %}
set var to 0
repeat until var ≥ 100
	set var to var + 1
	log var
end repeat
{% endcodeblock %}

### repeat while *condition*
该命令执行循环只要***while***条件成立，除非遇到<code>exit [repeat]</code>命令
{% codeblock repeat while ... lang:applescript %}
set var to 0
repeat while var < 100
	set var to var + 1
	log var
end repeat
{% endcodeblock %}
### repeat with *var* from *start* to *end* [by *step*]
该命令执行循环只要***while***条件成立，除非遇到<code>exit [repeat]</code>命令
{% codeblock repeat with var from ... to ... by ... lang:applescript %}
repeat with var from 0 to 100 by 5
	log var
end repeat
{% endcodeblock %}

如果***by***参数没有，则默认<code>var</code>每个循环+1
{% codeblock repeat with var from ... to ... lang:applescript %}
repeat with var from 0 to 100
	log var
end repeat
{% endcodeblock %}

### repeat with *var* in *list*
该命令可以实现列表遍历的效果，除非遇到<code>exit [repeat]</code>命令
{% codeblock repeat with var in ... lang:applescript %}
set _list to {1, 2, 3, 4, 5, 6, 7}
repeat with var in _list
	log var
end repeat
{% endcodeblock %}