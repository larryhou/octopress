---
layout: post
title: "在OSX系统使用AS3版protobuf"
date: 2012-11-10 23:30
comments: true
categories: 
---

[该项目][3]搭建了 AS3 protobuf 所需的OSX运行环境以及AS3类库，整合了Google [protobuf][1]和[protobuf-actionscript3][2]第三方插件资源，本文来介绍一下AS3版protobuf的使用方法。
[1]: http://code.google.com/p/protobuf/ "[v2.3.0] http://code.google.com/p/protobuf/"
[2]: http://code.google.com/p/protobuf-actionscript3/ "http://code.google.com/p/protobuf-actionscript3/"
[3]: https://github.com/larryhou/as3proto-osx  "Actionscript3.0版protobuf"
<!--more-->    

* **编译安装protoc命令行**     
在Terminal里面进入sdk/project目录，运行下面脚本
{% codeblock lang:sh %}
./configure
	
make
make check
sudo make install
{% endcodeblock %}
	
* **检查protobuf是否安装成功**  
在Terminal中输入，回车
{% codeblock lang:sh %}
protoc --help
{% endcodeblock %}
	
检查一下帮助内容是否包含--as3_out选项
{% codeblock lang:sh %}
--as3_out=OUT_DIR           Generate ActionScript source file.
--cpp_out=OUT_DIR           Generate C++ header and source.
--java_out=OUT_DIR          Generate Java source file.
--python_out=OUT_DIR        Generate Python source file.
{% endcodeblock %}
	
* **使用命令行生成AS3代码**  	
{% codeblock lang:sh %}
protoc --proto_path=proto --as3_out=output proto/hello.proto
{% endcodeblock %}
	
* **使用protobuf.sh快速代码生成**  
打开protobuf.sh文本文件
	* 把OUTPUT_DIR设置成AS3保存目录，支持绝对目录、相对目录
	* 把PROTO_DIR设置成\*.proto文件存储目录   
	
在Terminal里面进入protobuf.sh所在目录  
	
hell.proto文件内容  
{% codeblock lang:as3 %}
message HelloWorld{
    optional int32 code = 1;
    optional string name = 2;
    optional Info info = 3;

    message Info{
        optional string version = 1;
    }
}
{% endcodeblock %}
	
运行  
	
{% codeblock lang:sh %}
sh protobuf.sh
	
- - - - - - - - - - - - -
Type proto file name:
hello

-> proto/hello.proto
- - - - -

DONE! Press ENTER key to continue...

{% endcodeblock %}
	
在OUTPUT_DIR目录里面就可以得到相应的AS3代码  
	
HelloWorld.as代码内容  
{% codeblock lang:as3 %}
// Generated by the protocol buffer compiler.  DO NOT EDIT!

package  {

  import com.google.protobuf.*;
  import flash.utils.*;
  import com.hurlant.math.BigInteger;
  import Info;
  public final class HelloWorld extends Message {
    public function HelloWorld() {
      registerField("code","",Descriptor.INT32,Descriptor.LABEL_OPTIONAL,1);
      registerField("name","",Descriptor.STRING,Descriptor.LABEL_OPTIONAL,2);
      registerField("info","Info",Descriptor.MESSAGE,Descriptor.LABEL_OPTIONAL,3);
    }
    // optional int32 code = 1;
    public var code:int = 0;
    
    // optional string name = 2;
    public var name:String = "";
    
    // optional .HelloWorld.Info info = 3;
    public var info:Info = null;
    
  
  }
}	
	
{% endcodeblock %}
	
Info.as代码内容  
{% codeblock lang:as3 %}
// Generated by the protocol buffer compiler.  DO NOT EDIT!

package  {

  import com.google.protobuf.*;
  import flash.utils.*;
  import com.hurlant.math.BigInteger;
  public final class Info extends Message {
    public function Info() {
      registerField("version","",Descriptor.STRING,Descriptor.LABEL_OPTIONAL,1);
    }
    // optional string version = 1;
    public var version:String = "";
    
  
  }
}
{% endcodeblock %}
	