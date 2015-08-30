---
layout: post
title: "Install git with macport"
date: 2012-10-26 16:27
comments: true
---

不知道怎么回事儿，我的git有时候会抽风，现在又抽风了：我的<code>git-svn</code>不见了，这里是用<code>macport</code>安装的脚本，以备下次重装又要google半天...

{% codeblock install git with svn%}
sudo port install git-core +svn +doc +bash_completion +gitweb
{% endcodeblock%}