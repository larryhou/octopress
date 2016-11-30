---
layout: post
title: "Markdown示例集锦"
date: 2015-09-01 14:22:57 +0800
comments: true
categories: markdown
---

###代码块语法

	``` [language] [title] [url] [link text]
	code snippet
	```
不使用语法高亮

	```
	$ git clone git@github.com:imathis/octopress.git # fork octopress
	```
```
$ git clone git@github.com:imathis/octopress.git # fork octopress
```
<!-- more -->
使用语法高亮功能，并添加链接文字

	``` ruby 查找素数 http://www.noulakaz.net/weblog/2007/03/18/a-regular-expression-to-check-for-prime-numbers/ 源码链接
	class Fixnum
	  def prime?
	    ('1' * self) !~ /^1?$|^(11+?)\1+$/
	  end
	end
	```
``` ruby 查找素数 http://www.noulakaz.net/weblog/2007/03/18/a-regular-expression-to-check-for-prime-numbers/ 源码链接
class Fixnum
  def prime?
    ('1' * self) !~ /^1?$|^(11+?)\1+$/
  end
end
```
通过<code>&#123;% codeblock %&#125;</code>...<code>&#123;% endcodeblock %&#125;</code>同样可以显示代码高亮
<pre>
&#123;% codeblock [lang:language] [title] [url] [link text] %&#125;
code snippet
&#123;% endcodeblock %&#125;
</pre>
<pre>&#123;% codeblock lang:objc %&#125;
[rectangle setX: 10 y: 10 width: 20 height: 20];
&#123;% endcodeblock %&#125;</pre>

{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}

<pre>
&#123;% codeblock C#泛型 lang:csharp https://github.com/larryhou/XUPorter/blob/master/XCMod.cs 源码链接 %&#125;
private T fetch&lt;T&gt;(string key) where T:new()
&#123;
	if(_datastore != null &amp;&amp; _datastore.Contains(key))
	&#123;
		return (T)_datastore[key];
	&#125;
	return new T();
&#125;
&#123;% endcodeblock %&#125;
</pre>
{% codeblock C#泛型 lang:csharp https://github.com/larryhou/XUPorter/blob/master/XCMod.cs 源码链接 %}
private T fetch<T>(string key) where T:new()
{
	if(_datastore != null &amp;&amp; _datastore.Contains(key))
	{
		return (T)_datastore[key];
	}
	return new T();
}
{% endcodeblock %}

###引用级别样式

	> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
	> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
	> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
	>
	> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
	> id sem consectetuer libero luctus adipiscing.

> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
> 
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.

	> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
	consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
	Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

	> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
	id sem consectetuer libero luctus adipiscing.
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.

	> ## This is a header.
	> 
	> 1.   This is the first list item.
	> 2.   This is the second list item.
	> 
	> Here's some example code:
	> 
	>     return shell_exec("echo $input | $markdown_script");
> ## This is a header.
> 
> 1.   This is the first list item.
> 2.   This is the second list item.
> 
> Here's some example code:
> 
>     return shell_exec("echo $input | $markdown_script");

###清单
<pre>
*   Red
*   Green
*   Blue
</pre>

*   Red
*   Green
*   Blue

<pre>
+   Red
+   Green
+   Blue
</pre>

+   Red
+   Green
+   Blue

<pre>
-   Red
-   Green
-   Blue
</pre>

-   Red
-   Green
-   Blue

<pre>
1.  Bird
2.  McHale
3.  Parish
</pre>

1.  Bird
2.  McHale
3.  Parish

<pre>
&lt;ol&gt;
&lt;li&gt;Bird&lt;/li&gt;
&lt;li&gt;McHale&lt;/li&gt;
&lt;li&gt;Parish&lt;/li&gt;
&lt;/ol&gt;
</pre>
	
<ol>
<li>Bird</li>
<li>McHale</li>
<li>Parish</li>
</ol>

<pre>
1.  Bird
1.  McHale
1.  Parish
</pre>
	
1.  Bird
1.  McHale
1.  Parish

<pre>
3. Bird
1. McHale
8. Parish
</pre>
	
3. Bird
1. McHale
8. Parish

<pre>
*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.
</pre>

*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.
	
<pre>
*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
Suspendisse id sem consectetuer libero luctus adipiscing.
</pre>
*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
Suspendisse id sem consectetuer libero luctus adipiscing.
<pre>
*   This is a list item with two paragraphs.

    This is the second paragraph in the list item. You're
only required to indent the first line. Lorem ipsum dolor
sit amet, consectetuer adipiscing elit.

*   Another item in the same list.
</pre>
*   This is a list item with two paragraphs.

    This is the second paragraph in the list item. You're
only required to indent the first line. Lorem ipsum dolor
sit amet, consectetuer adipiscing elit.

*   Another item in the same list.

<pre>
*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.
</pre>
*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.
	
<pre>
Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell
</pre>
	
Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell