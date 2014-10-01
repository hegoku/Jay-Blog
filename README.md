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

然后将 ``post-receive`` 这个文件上传至 ``blog.git/hools`` 目录里,将data.sqlite上传到你设置的目录里,并修改属性为可写:

```sh
$ chmod +w data.sqlite
```

这一步创建了两个目录:

1. ``/www/blog`` 博客网站的存放目录
2. ``blog.git`` 线上git仓库

####本地:

```sh
$ mkdir ~/blog && cd blog
$ git init
```

然后将文件和目录复制到 ``blog`` 这个文件夹里

``article``这个目录是存放你的以Markdown格式写的博客

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
