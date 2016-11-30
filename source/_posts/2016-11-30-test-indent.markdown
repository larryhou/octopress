---
layout: post
title: "markdown缩进语法"
date: 2016-11-30 17:01:54 +0800
comments: true
categories: markdown
---
行首添加TAB符号，如下脚本
{% codeblock lang:sh %}
   #!/bin/bash
	sudo sysctl net.inet.ip.forwarding=1
	sudo sysctl net.inet.ip.redirect=1
	sudo sysctl net.inet6.ip6.forwarding=1
	sudo sysctl net.inet6.ip6.redirect=1
	sudo pfctl -d
	sleep 1

	sudo pfctl -F all -f /etc/pf.conf
	sleep 1

	echo "
	 nat on en4 from bridge100:network to any -> (en4)
	 rdr pass on bridge100 inet proto tcp to port {443,80} -> 127.0.0.1 port 8888" | sudo pfctl -evf -

	export MITMPROXY_SSLKEYLOGFILE=~/Documents/master-secret.log
	mitmproxy -T -p 8888
{% endcodeblock %}

可以转换成如下样式

	#!/bin/bash	
	sudo sysctl net.inet.ip.forwarding=1
	sudo sysctl net.inet.ip.redirect=1
	sudo sysctl net.inet6.ip6.forwarding=1
	sudo sysctl net.inet6.ip6.redirect=1
	sudo pfctl -d
	sleep 1

	sudo pfctl -F all -f /etc/pf.conf
	sleep 1

	echo "
	nat on en4 from bridge100:network to any -> (en4)
	rdr pass on bridge100 inet proto tcp to port {443,80} -> 127.0.0.1 port 8888" | sudo pfctl -evf -

	export MITMPROXY_SSLKEYLOGFILE=~/Documents/master-secret.log
	mitmproxy -T -p 8888
