---
layout: post
title: "Convert SWF vector shape to SVG image"
date: 2015-09-05 02:06:44 +0800
comments: true
categories: 
---

<a href="/assets/swf-svg/graph-01.svg" target="_blank"><img src="/assets/swf-svg/graph-01.svg"></img></a>
<!-- more -->
<a href="/assets/swf-svg/graph-02.svg" target="_blank"><img src="/assets/swf-svg/graph-02.svg"></img></a>

``` html Display SVG in HTML: #1
<img src="/assets/swf-svg/graph-01.svg"></img>
```

``` html Display SVG in HTML: #2
<embed src="/assets/swf-svg/graph-01.svg" width="300" height="100" type="image/svg+xml"
    pluginspage="http://www.adobe.com/svg/viewer/install/" />
```

``` html Display SVG in HTML: #3
<object data="/assets/swf-svg/graph-01.svg" width="300" height="100" type="image/svg+xml"
    codebase="http://www.adobe.com/svg/viewer/install/" />
```

``` html Display SVG in HTML: #4
<iframe src="/assets/swf-svg/graph-01.svg" width="300" height="100"></iframe>
```

``` html Not Yet Today
<html xmlns:svg="http://www.w3.org/2000/svg">
    <body>

    <p>This is an HTML paragraph</p>

    <svg:svg width="300" height="100" version="1.1" >
    <svg:circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red" />
    </svg:svg>

    </body>
</html>
```

{% gist e0131d953ef1d407d72a %}