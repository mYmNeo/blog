---
title: rpmbuild easy tutorial
date: 2016-04-28 11:04:44
tags: 
    - linux
    - rpmbuild
---
1. 创建好文件夹结构
    + SOURCES 包含源代码,补丁,图标文件等
    + SPECS 包含spec文件,这些文件用来控制构建过程
    + BUILD 用来解压源代码的目录和软件构建的目录
    + RPMS 包含构建程序最后产生的RPM包
    + SPRMS 包含构建程序最后产生的源代码包文件
1. 放置源代码到SOURCES文件夹中
1. 编写spec文件
<!-- more -->
+ 常用label

|label|description|
|----|----|
|Name|表明这个包叫什么名字，通常来说，一般用软件的名字作为name，name存在于最后的包的标签和包的文件名字中|
|Version|表示这个软件被打包后的版本，版本存在于最后包的标签和包的名字|
|Release|表示这个软件的时间信息，表示何时什么版本的软件被打包，你可以当作这个是包的版本号，这个信息最后作为最后包的标签和文件名的一部分|
|Group|用来存储这个被打包的文件与其他包的组关系，这段信息由很多词构成，以/分割。从左到右描述的更为精确|
|Source|说明被打包的软件的源代码在哪里可以被发现;告诉存在SOURCES文件夹中的源文件的名字|
|URL|通常含有一个URL，像Source那行，与source的区别是，source通常给RPM提供源代码的名字，URL是用来指明被打包的软件是文档信息|
|Distribution|告知被打包的软件是属于那个产品的|
|Vendor|指明那个组织发布的这个软件|
|Packager|指明组织中那个作者打包的这个软件|
|License|许可证|
|Requires|说明这个包需要的依赖条件|
|BuildRoot|说明这个包构建的根目录|

+ 常用section

|section|description|
|----|----|
|description|更详细的描述包的内容|
|define|定义自己的macro|
|prep|创建软件的构建环境，可以执行多条shell命令|
|build|执行build的多条命令|
|install|执行install的多条命令|
|files|列出来的文件都会被打进RPM包中|
|defattr|RPM安装的文件默认的权限，拥有者和组|
|pre|在安装前执行的命令|
|post|在安装后执行的命令|
|preun|在卸载前执行的命令|
|postun|在卸载后执行的命令|
|package|生成子包|

## 创建Subpackages
{% blockquote %}
简单的来说,subpackage是同一个spec文件创建出来众多package中的一个,RPM可以创建一个主要的package同时创建一个或者多个subpackage,subpackges可以不从主要的package中产生,这些都是根据package builder的规则来确定
{% endblockquote %}
Example:
{% codeblock lang:spec example.spec %}
Name: foo
Version: 2.7
Release: 1
Source: foo-2.7.tgz
CopyRight: probably not
Summary: The foo app, and the baz library needed to build it
Group: bogus/junque
%description
This is the long description of the foo app, and the baz library needed to
build it...

# %packge server will result in the name of the subpackage being foo-server
%package server
Summary: The foo server
Group: bogus/junque
%description server
This is the long description for the foo server...

%package client
Summary: The foo client
Group: bogus/junque
%description client
This is the long description for the foo client...

# The -n option is used to change the final name of a subpackage from <mainpackage>-<subpackage> to <subpackage>. 
%package -n bazlib
Version: 5.6
Summary: The baz library
Group: bogus/junque
%description -n bazlib
This is the long description for the bazlib...


%pre
echo "This is the foo package preinstall script"

%pre server
echo "This is the foo-server subpackage preinstall script"

%pre client
echo "This is the foo-client subpackage preinstall script"

%pre -n bazlib
echo "This is the bazlib subpackage preinstall script"

%files
/usr/local/foo-file

%files server
/usr/local/server-file

%files client
/usr/local/client-file

%files -n bazlib
/usr/local/bazlib-file
{% endcodeblock %}