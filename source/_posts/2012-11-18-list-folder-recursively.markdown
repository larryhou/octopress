---
layout: post
title: "使用AppleScript递归遍历文件夹"
date: 2012-11-18 23:11
comments: true
categories: 
---

最近对AppleScript很感兴趣，使用它可以做一些自动化处理，类似WIN系统的*.bat脚本，不过AppleScript要比它强大很多，对系统的融合更加深入。如果结合Calendar还可以做一些定时计划任务，非常的方便。

现在我写了一个监视共享目录的脚本，它会把最近30天、大于500MB的影片输出一个列表，虽然写了很久，不过也熟悉好多命令以及编写脚本的流程，收获还是蛮大的。在写这个脚本的时候，走了很多弯路，因为我觉得文件夹操作只需要<code>Finder.app</code>就可以，结果出现各种问题，一度想到放弃，不过最后研究AppleScript自带的脚本示例发现要用<code>System Events</code>，可是到现在我也不知道为什么要这样写，因为AppleScript <code>Dictionary</code> 帮助文档已经写得很清楚了...oops

<!--more-->
{% codeblock lang:applescript %}
global SAVE_FOLDER
set SAVE_FOLDER to "movies"

global OUTPUT_FILE
set OUTPUT_FILE to POSIX file (POSIX path of (path to desktop) & SAVE_FOLDER as text)

global MOVIE_SIZE
set MOVIE_SIZE to 500 * 1024 * 1024

global MOVIE_FORMATS
set MOVIE_FORMATS to {"mov", "mkv", "mp4", "rmvb"}

tell application "Finder"
	if not (exists OUTPUT_FILE) then
		make new folder at (path to desktop) with properties {name:SAVE_FOLDER}
	end if
end tell

set OUTPUT_FILE to POSIX file ((POSIX path of OUTPUT_FILE) & "/" & timestamp() & ".txt" as text)

-- connet remote sharing resource
mount volume "smb://10.11.8.66/IEDmovie$" as user name "larryhou" with password "password"

-- script entry
tell application "System Events"
	set _root to alias (path of disk "IEDmovie$")
	
	set _list to (list folder _root without invisibles)
	set _path to path of _root
	
	try
		-- open file access if possible
		open for access OUTPUT_FILE with write permission
	end try
	
	set eof OUTPUT_FILE to 0
	set _result to (my lookForFiles(_path, _list))
	
	close access OUTPUT_FILE
	
end tell

beep 2 -- notification of finishing task with 2 times beep
display dialog "DONE!!" with icon stop giving up after 60 * 2

-- filter kernel
-- if return true, will be kept, or discarded
on processFile(_file)
	tell application "System Events"
		set _size to size of _file
		set _extension to name extension of _file
		
		-- keep files larger than MOVIE_SIZE and with specific file extension
		set _available to (_size ≥ MOVIE_SIZE and (MOVIE_FORMATS contains _extension))
		
		set _date to (modification date of _file)
		set _current to current date
		
		-- keep files modified within last month
		set _available to _available and ((_current - _date) / (24 * 3600) ≤ 30)
		
		return _available
	end tell
end processFile

-- search files recursively
on lookForFiles(prefix, names)
	set _result to {}
	tell application "System Events"
		repeat with var in names
			set _item to (alias (prefix & var as text))
			if kind of _item is "文件夹" then
				set _path to path of _item
				set _list to list folder _item without invisibles
				
				set _result to _result & (my lookForFiles(_path, _list))
			else
				if my processFile(_item) then
					set _itemPath to POSIX path of _item
					
					set _date to modification date of _item
					
					set _info to (year of _date & "-")
					set _info to (_info & my substr(month of _date as text, 1, 3) & "-")
					set _info to (_info & my padding(day of _date) & ": ")
					
					set _current to current date
					set _offset to (_current - _date) / (24 * 3600)
					set _offset to (_offset as integer)
					
					set _info to _info & my padding(_offset) & ": "
					set _info to _info & name of _item & ": "
					
					-- append file path and return
					set _info to _info & _itemPath & (ASCII character 13)
					
					-- save to UTF-8 encoding file
					set _result to _result & _info
					
					write (_info as string) to OUTPUT_FILE as «class utf8»
					
				end if
			end if
			
		end repeat
	end tell
	return _result
end lookForFiles

on timestamp()
	set _date to current date
	
	set _result to {}
	set _result to _result & (year of _date)
	set _result to _result & (my substr((month of _date as text), 1, 3))
	set _result to _result & padding(day of _date)
	set _result to _result & padding(hours of _date)
	--set _result to _result & padding(minutes of _date)
	--set _result to _result & padding((time of _date) mod 60)
	
	return _result as text
end timestamp

on padding(_data)
	set _str to (_data as text)
	repeat
		if length of _str < 2 then
			set _str to ("0" & _str as text)
		else
			exit repeat
		end if
	end repeat
	return _str
end padding

-- get substring from text string
on substr(_str, _offset, _length)
	set _strlen to length of _str
	if _length > _strlen then
		set _length to _strlen
	end if
	
	if _offset < 1 then
		set _offset to 1
	end if
	
	return text _offset thru (_offset + _length - 1) of _str as text
end substr

{% endcodeblock %}

{% codeblock list folder recursively lang:applescript %}
on recurseFolder(_folder)
	set _result to {}
	set _list to list folder _folder without invisibles
	set _path to _folder as string
	
	repeat with _name in _list
		set _item to alias (_path & _name as string)
		set _info to info for _item
		
		if folder of _info then
			set _result to _result & my recurseFolder(_item)
		else
			set _result to _result & POSIX path of _item
		end if
	end repeat
	
	return _result
end recurseFolder
{% endcodeblock %}

再补充一个shell版本同功能的脚本

{% codeblock lang:sh %}
#!/bin/bash

cd ~/remote/movie

TIMESTAMP=$(eval date '+%Y%m%d%h')
OUTPUT=~/Desktop/movies/$TIMESTAMP.txt

mount_smbfs //larryhou@10.11.8.66/IEDmovie$ .
find -E . -regex '.*\.(mp4|rmvb|mkv)$' -size +300M -ctime -2d -exec ls -lhc {} \; | sed -E 's|^.+staff[^a-z0-9]*||' | sed -E 's|./([^/]+/)+([^/]+)$|\2 @&|g' > $OUTPUT

#| sed -E 's|([0-9:]+ )+||g' > $OUTPUT
diskutil unmount force .

mate $OUTPUT


{% endcodeblock %}
