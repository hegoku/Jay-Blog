#JBlog 是什么

Jay Blog 是一个用Git来提交博客,用Markdown写博客的PHP博客框架。

#安装

####服务器:

```sh
$ mkdir /www/blog
$ mkdir blog.git
$ chmod +x /www/blog
$ cd blog.git
$ git init --bare
```

打开 ``post-receive`` 文件,将下列行的内容改为自己的设置:

```python
#博客网站路径
webPath="/www/blog"
#博客文章路径
articlePath=webPath+"/article"
#sqlite3数据库路劲
datePath=webPath+"/data.sqlite"
```

然后将 ``post-receive`` 这个文件上传至 ``blog.git/hooks`` 目录里,将data.sqlite上传到你设置的目录里,并修改属性为可写:

```sh
$ chmod +w data.sqlite
```
接着创建你设置的博客文章路径

这一步创建了两个目录:

1. ``/www/blog`` 博客网站的存放目录
2. ``blog.git`` 线上git仓库

####本地:

```sh
$ mkdir ~/blog && cd blog
$ git init
```

然后将 [Jay-Framework](https://github.com/hegoku/Jay-Framework) (一个定位于轻量级的类Yii的PHP框架,具体用法请按连接) 文件夹里的内容复制到 ``blog`` 这个文件夹里，并建立存放你的以Markdown格式写的博客。因为上面我们设置的目录名位 ``article`` ,所以我们在 ``blog`` 这个目录建立这个目录:

```sh
$ mkdir article
```

开打 ``config.php`` 文件,修改数据库路径:

```php
'db'=>new Sqlite("data.sqlite"),
```

然后添加git远程服务器提交信息:

```sh
$ git remote add web ssh://username@host/home/user/blog.git
```

####更新博客

```sh
$ git push web +master:refs/heads/master
```

至此,设置都完成了,之后就可以根据自己的需要编写网站代码了.

##数据库结构

Article表:

|Field|Type|说明|
|-----|----|---|
| id  | integer | 主键 |
| title | varchar(40) | 标题 |
| date | date | 创建日期 |
| modifydate | date | 修改日期 |
| category | varchar(40) | 分类 |
| file | varchar(40) | 文件名 |
| content | text | 转成html格式的内容 |

##markdown博客格式

```md
title: JBlog说明
date: 2012-9-18 19:38
modifydate: 2012-9-18 19:38
category: 项目说明
tags: git,markdown

具体内容...
```
