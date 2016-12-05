---
layout: post
title: "awk使用教程"
date: 2016-12-05 19:13:55 +0800
comments: true
categories: shell MAC awk
---
###入门
`awk`在文本处理脚本`shell`里很常用，它从管道`|`或文件中读取每一行，然后按照一定规则把每行自动分成多列，默认使用**空格**自动分列。在`awk`里面，**空格**可以是`空白字符`、`TAB制表符`。分列可以让`awk`脚本很方便地引用这些分隔开的值，`$1`表示第一列，`$2`表示第二列，等等以此类推，当然`$`后面的数字可以是个很大的值，比如`$1024`。另外，在`awk`中使用`$0`表示整行,`$NF`表示最后一列。

先来看个示例
{% codeblock lang:bash %}
echo 'this seems like a pretty nice example' | awk '{print $1}'
{% endcodeblock %}

`$1`是**this**，`$2`是**seems**，`$7`和`$NF`是**example**，在该例子中使用**空格**分隔成7列，完整语法是这样的

{% codeblock lang:bash %}
echo 'this seems like a pretty nice example' | awk -F' ' '{print $1}'
{% endcodeblock %}
可以看到`awk`多了一个`-F`参数，通过该参数可以设置各种分隔符，**单字符**、**多字符**都能很好的支持，同样的示例我可以添加`-F' like '`这样的多字符分隔符，可以得到结果**this seems**.

{% codeblock lang:bash %}
echo 'this seems like a pretty nice example' | awk -F' like ' '{print $1}'
{% endcodeblock %}

除了`NF`，`awk`还有一些其他内置变量，见下表

|内置变量|变量描述|
|:------|:------------:|
|CONVFMT|conversion format used when converting numbers (default %.6g)|
|FS     |regular expression used to separate  fields;  also  settable  by option -Ffs.|
|NF     |number of fields in the current record|
|NR     |ordinal number of the current record|
|FNR    |ordinal number of the current record in the current file|
|FILENAME |the name of the current input file|
|RS     |input record separator (default newline)|
|OFS    |output field separator (default blank)|
|ORS    |output record separator (default newline)|
|OFMT   |output format for numbers (default %.6g)|
|SUBSEP |separates multiple subscripts (default 034)|
|ARGC   |argument count, assignable|
|ARGV   |argument array, assignable; non-null members are taken as file-names|
|ENVIRON |array of environment variables; subscripts are names.|

|变量名|含义|
|:---|:---:|
|ARGC|命令行变元个数|
|ARGV|命令行变元数组|
|FILENAME|当前输入文件名|
|FNR|当前文件中的记录号|
|FS|输入域分隔符，默认为一个空格|
|RS|输入记录分隔符|
|NF|当前记录里域个数|
|NR|到目前为止记录数|
|OFS|输出域分隔符|
|ORS|输出记录分隔符|

###正则表达式
上面通过分隔符分列是`awk`的基本功能，`awk`还可以和[正则表达式结合][regex]相结合做出复杂的效果

	1048592             |FowTexture:Init ()|Color[]             
	262160              |AStar:.ctor (Map)|Int32[]             
	196684              |TheNextMoba.Module.Arena.ArenaResourceLoader:OnItemLoadSuccess (string,object)|Byte[]              
	192016              |Morefun.LockStep.LockstepProfiler/Stat:CreateFrameContext ()|FrameContext[]      
	131088              |SignedDistanceField:.ctor (Map,int)|Int16[]             
	81936               |GameObjectUtil:Init ()|String[]            
	65568               |TheNext.Moba.Logic.FOWManager:Init ()|Byte[,]             
	65568               |TheNext.Moba.Logic.FOWManager:Init ()|Byte[,]             
	65568               |TheNext.Moba.Logic.FOWSystem:Init (TheNext.Moba.Logic.EnmTeamID,TheNext.Moba.Logic.IFOWSystem)|Byte[,]             
	65568               |TheNext.Moba.Logic.FOWSystem:Init (TheNext.Moba.Logic.EnmTeamID,TheNext.Moba.Logic.IFOWSystem)|Byte[,] 

{% codeblock lang:bash %}
awk '/Init/ {print $0}'
{% endcodeblock %}
	
	1048592             |FowTexture:Init ()|Color[]             
	81936               |GameObjectUtil:Init ()|String[]            
	65568               |TheNext.Moba.Logic.FOWManager:Init ()|Byte[,]             
	65568               |TheNext.Moba.Logic.FOWManager:Init ()|Byte[,]             
	65568               |TheNext.Moba.Logic.FOWSystem:Init (TheNext.Moba.Logic.EnmTeamID,TheNext.Moba.Logic.IFOWSystem)|Byte[,]             
	65568               |TheNext.Moba.Logic.FOWSystem:Init (TheNext.Moba.Logic.EnmTeamID,TheNext.Moba.Logic.IFOWSystem)|Byte[,] 

通过`awk '/Init/'`这个简单的例子可以知道，在双斜杠`'//'`中间可以添加正则表达式，正则表达式的作用过滤出匹配的行 然后再执行花括号里面`{}`逻辑，该示例中正则对整行进行匹配操作，也可以对某一列执行匹配
{% codeblock lang:bash %}
awk -F'|' '$2 ~ /Init/ {print $0}'
{% endcodeblock %}
脚本用`|`分隔符分列，把正则表达式应用到第二列进行匹配
{% codeblock lang:bash %}
awk -F'|' '$2 ~ /Init/ {print $1,$3}'
{% endcodeblock %}

	1048592              Color[]             
	81936                String[]            
	65568                Byte[,]             
	65568                Byte[,]             
	65568                Byte[,]             
	65568                Byte[,] 
	
###表达式
`awk`也支持常见的流程控制语句`if...else`、`for`、`for...in`、`while`、`do...while`

`for`循环和三元表达式
{% codeblock lang:bash %}
echo 192.168.0.105 | awk -F'.' '{for(i=1;i<=NF;i++)printf "%02X" (i<NF?":":""),$i}'
{% endcodeblock %}
{% codeblock lang:bash %}
echo 192.168.0.105 | awk -F'.' '{for(i=1;i<=NF;i++)
										printf "%02X" (i<NF?":":""),$i }'
{% endcodeblock %}

`for`循环和`if`表达式
{% codeblock lang:bash %}
echo 192.168.0.105 | awk -F'.' '{for(i=1;i<=NF;i++){printf "%02X",$i;if(i<NF)printf ":"}}'
{% endcodeblock %}

{% codeblock lang:bash %}
echo 192.168.0.105 | awk -F'.' '{for(i=1;i<=NF;i++)
{
		printf "%02X",$i;
		if(i<NF)printf ":"
}}'
{% endcodeblock %}

	C0:A8:00:69

`for...in`和`split`
{% codeblock lang:bash %}
echo 192.168.0.105 | awk -F'.' '{split($0,a);for(i in a) printf "%d:%02X ",i,a[i]}'
{% endcodeblock %}

`while`
{% codeblock lang:bash %}
head -n 5 mono.txt | awk -F'|' '{n=1;while(n++<=NF)print $n}'
{% endcodeblock %}

	FowTexture:Init ()
	Color[]             

	AStar:.ctor (Map)
	Int32[]             

	TheNextMoba.Module.Arena.ArenaResourceLoader:OnItemLoadSuccess (string,object)
	Byte[]              

	Morefun.LockStep.LockstepProfiler/Stat:CreateFrameContext ()
	FrameContext[]      

	SignedDistanceField:.ctor (Map,int)
	Int16[]         

其他各种表达式

```
if( expression ) statement [ else statement ]
while( expression ) statement
for( expression ; expression ; expression ) statement
for( var in array ) statement
do statement while( expression )
break
continue
{ [ statement ... ] }
expression	      # commonly var = expression
print [ expression-list ] [ > expression ]
printf format [ , expression-list ] [ > expression ]
return [ expression ]
next		      # skip remaining patterns on this input line
nextfile		      # skip rest of this file, open next, start at top
delete array[ expression ]# delete an array element
delete array	      # delete all elements of array
exit [ expression ]     # exit immediately; status is expression
```

可以在表达式中使用的`awk`内置函数

|函数名|函数描述|
|:----|:----:|
|length|字符串长度|
|rand|(0<=x<1)的随机数|
|srand|设置随机种子并返回之前的随机种子|
|int|截尾转换成整数|
|substr(s,m,n)|返回字符串s自m位置(索引从1开始)开始的n个字符|
|index(s,t)|如果字符串s中包含t则返回1，否则返回0|
|match(s,r)|返回字符串s匹配正则表达式r的位置(从1开始)|
|split(s,a,fs)|把字符串s通过正则fs分隔成数组a，并返回数组a长度n，如果fs未设置，则使用FS分隔符|
|sub(r,t,s)|在字符串s中，使用正则表达式r首次匹配的位置替换成t，如果s未设置，则使用$0|
|gsub(r,t,s)|与sub(r,t,s)参数相同，不过会把匹配的字符串全部替换，并返回替换的次数|
|sprintf(fmt,expr,...)|依据printf相同的样式fmt格式表达式列表|
|system(cmd)|执行cmd并返回退出状态码|
|tolower(str)|把字符串str转换成小写|
|toupper(str)|把字符串str转换成大写|

以及各种运算符

|运算符|描述|
|:--|:---:|
|=,+=,-=,*=,/=,%=,^=,**=|赋值|
|?:|C条件表达式|
|\|\||逻辑或|
|&&|逻辑与|
|~,~!|匹配正则表达式和不匹配正则表达式|
|<,<=,>,>=,!=,==|关系运算符|
|空格|连接|
|+,-|加，减|
|*,/,&|乘，除与求余|
|+,-,!|一元加，减和逻辑非|
|^,***|求幂|
|++,--|增加或减少，作为前缀或后缀|
|$|字段引用|
|in|数组成员|



[regex]: https://www.gnu.org/software/gawk/manual/html_node/Regexp.html#Regexp  "正则表达式"



