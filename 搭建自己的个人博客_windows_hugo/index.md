# 搭建自己的个人博客_Windows_Hugo


## 一、前言

`Hugo` 是一款基于 `Go` 语言而实现的静态网站生成器，具有简单易用、高效易扩展、快速部署的特点。

## 二、安装Hugo

预构建的二进制文件可用于各种操作系统和体系结构。访问[最新版本](https://github.com/gohugoio/hugo/releases)页面，然后向下滚动到Assets（资产）部分。

1. 下载所需版本、操作系统和体系结构的存档。建议下扩展版

   ![hugo扩展版压缩包](/image/hugo扩展版压缩包.png)

2. 提取存档，解压之后会有三个文件

3. 新建bin目录，将可执行文件移动到`E:\Hugo\bin`目录

   ![hugo文件路径](/image/hugo文件路径.png)

4. 将此目录`E:\Hugo\bin`添加到 PATH 环境变量

   高级系统设置—>环境变量—>系统变量—>Path

5. 验证您是否对文件具有*执行*权限，打开命令提示符，执行`hugo version`

   ![hugo version](/image/hugo version.png)

   出现版本号，hugo配置完成

## 三、安装Git

Git for Windows 专注于提供一组轻量级的本机工具，将 Git SCM 的完整功能集带到 Windows，同时为有经验的 [Git](https://git-scm.com/) 用户和新手提供适当的用户界面。

### 1、Git BASH

Git for Windows 提供了一个 BASH 仿真，用于从命令行运行 Git。*NIX用户应该感到宾至如归，因为BASH仿真的行为就像LINUX和UNIX环境中的“git”命令一样。

### 2、Git GUI

由于Windows用户通常期望图形用户界面，Git for Windows还提供了Git GUI，这是Git MASH的强大替代品，提供了几乎所有Git命令行函数的图形版本，以及全面的视觉差异工具。

### 3、壳体集成

只需右键单击Windows资源管理器中的文件夹即可访问BASH或GUI。

### 4、详细安装教程

[Git 详细安装教程（详解 Git 安装过程的每一个步骤）](https://blog.csdn.net/mukes/article/details/115693833)

改：2.2.6 决定初始化新项目(仓库)的主干名字——选第二种为main

![主干名](/image/主干名.png)

## 四、用Hugo来生成博客

1、假设要创建博客存放在`E:\Hugo\Sites\`目录中，进入Git Base命令行，切换到该目录下执行`hugo new site myblog`创建myblog博客

生成博客命令：

```
hugo new site myblog
```

![创建博客](/image/创建博客.png)

创建成功后会有如下目录组织

![博客文件夹](/image/博客文件夹.png)

2、目录组织：[Hugo博客目录组织介绍](https://www.jianshu.com/p/c5297a8bb1e7)

## 五、下载并设置主题

Hugo有很多的主题：[Hugo主题下载地址](https://themes.gohugo.io/)

这里以[m10c](https://themes.gohugo.io/themes/hugo-theme-m10c/)主题为例，主题里有下载及配置的教程

[path]=`E:/Hugo/Sites/myblog`

![主题下载及配置](/image/主题下载及配置.png)

## 六、在本地启动个人博客

1、启动博客命令：

```
hugo server -t  m10c --buildDrafts
```

![启动博客](/image/启动博客.png)

2、浏览器访问地址：http://localhost:1313/

![浏览器访问博客](/image/浏览器访问博客.png)

最基本的博客启动成功！

## 七、新建一篇文章

新建博客命令：

```
hugo new post/blog.md
```

![创建文章1](/image/创建文章1.png)

![创建文章](/image/创建文章.png)

## 八、将个人博客部署到远端服务器

### 1、注册或登录[github官网](https://github.com/)

![注册或登录github](/image/注册或登录github.png)

![登录github](/image/登录github.png)

### 2、创建存储仓库（输入Repository name，其他默认）

![创建存储仓库](/image/创建存储仓库.png)

### 3、生成public文件夹

——myblog路径下

命令（需对应自己的存储仓库名）：

```
hugo --theme=m10c --baseUrl="https://Winner9696.github.io/" --buildDrafts
```

![生成public文件夹](/image/生成public文件夹.png)

### 4、将public文件夹传到远程仓库

——public路径下执行

（1）初始化仓库

```
git init
```

（2）添加文件到暂存区（'.'是全部添加）

```
git add .
```

（3）将暂存区内容添加到仓库中（后跟提交信息）

```
git commit -m "update"
```

（4）本地仓库与远程仓库进行关联（需对应自己的github账号和储存仓库名）

```
git remote add origin https://github.com/Winner9696/Winner9696.github.io.git
```

（5） 上传远程代码并合并

```
git push --set-upstream origin main
```

## 九、一键部署命令

以后添加文章部署到远程仓库，提交代码的时候一般有以下步骤：

```
cd E:/Hugo/Sites/myblog
hugo --theme=m10c --baseUrl="https://Winner9696.github.io/" --buildDrafts
cd E:/Hugo/Sites/myblog/public
git add .
git commit -m 'update'
git push -u origin main
```

以上这样太麻烦，我们可以将`git blog`这个命令作为以后日常一键部署的命令。输入以下命令即可完成配置：

```
git config --global alias.blog '!cd E:/Hugo/Sites/myblog;hugo --theme=m10c --baseUrl="https://Winner9696.github.io/" --buildDrafts;cd E:/Hugo/Sites/myblog/public;git add .;git commit -m 'update';git push -u origin main'
```

使用alias即可为一系列命令配置一个别名

当你写好文章之后，就可以在任意目录执行这个命令：

```
git blog
```

这样就达到了我们的目的：通过一个命令就可以更新博客文件，并自动推送到github 上。

## 十、补充

### 1、`git add .`出现warning：in the working copy of ···LF will be replaced by CRLF the next time Git

换行符的问题，Windows下换行符和Unix下的换行符不一样，git会自动转换，但是这样有问题，所以解决方法如下：

使用命令，禁止自动转换：

```
git config --global core.autocrlf false
```

### 2、Hugo静态网站图片插入问题

#### Hugo静态资源载入逻辑

（1）hugo 的静态文件放置在 /static 文件夹下，文章 markdown 文件放在 /content/post 文件夹下

（2）hugo 生成的 public 文件夹（即整个网页静态文件），会将static里的内容放到网站根目录

（3）基于以上两点，图片的相对路径要写成这种**格式**：`![imagename](/image/imagename.png)`

（4）由于 markdown 和生成的 html 的图片路径是一致的，因此 markdown 里也要这么写。但是如果直接把图片放到 /static/image 里，在本地就无法正常显示这个文件夹

#### 解决方案

基于以上4点原因，解决方案有以下几种：

- 在 /post/image 里放图片，然后复制到 /static/image 评价：麻烦

- 在（1）的基础上，写一个批处理，完成复制的任务；（因为之前写过的批处理：生成 public.cmd，只要在前面加上复制的命令就行） 评价：可行，但是不完美，可能出现文件权限问题

- 不管，就当瞎了，本地不看，直接看server实时渲染 评价：可行，但是太惨了

- 做一个 link，链接两个文件夹 评价：一劳永逸，可行。建立链接 cmd（管理员） 命令：

```
mklink /d "E:\Hugo\Sites\myblog\content\post\image" "E:\Hugo\Sites\myblog\static\image"
```

为了方便，我们希望在typora里粘贴的图片直接到image路径下，为此要做以下两步：

- 在markdown的文件头写入图片根目录，根目录为当前文件夹(`./`) ：`typora-root-url: ./`（也可以在格式—>图像—>设置图片根目录，选择 `\content\post` typora会自动会加入这行配置）

- 文件—>偏好设置—>图像，插入图片时**复制到指定路径** `./image`，应用规则**优先使用相对路径**

### 3、Git命令大全

[Git命令大全 - 简书 (jianshu.com)](https://www.jianshu.com/p/93318220cdce)

![github服务器图](/image/github服务器图.png)


---

> 作者: Winner  
> URL: https://Winner9696.github.io/%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2_windows_hugo/  

