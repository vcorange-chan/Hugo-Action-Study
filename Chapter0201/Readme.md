---
title: Readme.md
updated: 2022-10-07 10:30:41Z
created: 2022-10-06 21:04:37Z
latitude: 1.35537940
longitude: 103.86774440
altitude: 0.0000
---

# step1. 建立网站骨架
使用`hugo new site`命令，`yaml`格式，创建名为acme-corporation的网站骨架
```
hugo new site acme-corporation --format yaml
```

# step2. 认识文件结构
`hugo new`建立了六个文件夹
- archetypes : 包含内容(content)文件的模板。
- content : 包含网站内容。
- data : 包含存储结构，例如`YAML`,  `TOML`, `CSV`, 或者`JSON`文件。是网站的全局变量
- layouts : 覆盖主题的一部分。Hugo可灵活混搭主题页面、定制个性页面。此文件夹包含所有个性化主题。
- themes : 包含当前内容制作所用代码，可用Go模板语言写主题，亦可添加已有主题。
- config : 网站设计文件。包含网站初始数据例如：主题名称、主题参数。默认是一个`config.yaml`文件。Hugo支持一个配置文件分为多个配置文件之组合。
- static : 存储例如pdf、图片这样的静态内容。

除上述文件之外，通常还会遇到如下文件

- assets ： 放置网站全局所需之未处理的源代码。这些文件在编译中可执行。Hugo可重塑图像、包的大小，可缩小JavaScript文件，转化SCSS成CSS。
- public ：Hugo默认输出目录，即Hugo命令所生成的部署在CDN上的HTML。
- resources : Hugo在此文件夹中缓存数据处理时的大型操作。构建网站时，该文件中的数据应可重复使用，应有版本控制。例如图像处理结果。
- go.mod和go.sum ：Hugo模型以此同步独立项目。应版本控制。
- vendor : 存Hugo 模型引入的第三方依赖。
- node__modules, package.json, package-lock.json, package.hugo.json ： 用JavaScript生态关联整合Hugo。
- .github 和 netlify.toml ：用Github和Netlify服务关联Hugo。
- api : 定制化应用程序接口。 
---

# step3. 上传到github仓库
将`hugo new site` 命令生成的六个文件夹放入`acm-corporation/Chapter0201`目录下。
这个`acm-corporation` 目录下的内容做主支，每个章节的内容做分支。

由于git默认不上传空目录，因而在每个空目录下，填充`.gitkeep` 文件
```
New-Item   .gitkeep -type file
```
## 3.1. 将本地文件夹建立为github新仓库
### 3.1.0. 命令行建立仓库
适用于没有建立仓库的情况：
在`acm-corporation`目录下，初始化并建立仓库
```
git init
gh repo create
```
移动上下光标选择要执行的操作，注意选择：
```
Push an existing local repository to GitHub
? Add a remote? Yes
? What should the new remote be called? (origin) 
```
至此，新仓库建立完成。但此时仓库内空无一物，现将本地文件目录下的内容上传到仓库。
#### 3.1.0.1. 上传本地文件到仓库中
在已经建立远程连接的情况下（上文选项`? Add a remote? Yes`）
```
git add .
git commit -m "First commit"
```
这时候仓库内还没有主支，因此上传文件同时建立主支，主支名为master
```
git push --set-upstream origin master
```
### 3.1.1. 在github网站上建立仓库
如果已经通过github网站，建立了空仓库（没有任何文件），则如下命令：
```
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin 仓库URL
git push -u origin main
```
主支名为main
如果`git remote add origin` 后的仓库地址错了，可`git remote -v` 查看信息，然后`git remote remove origin` 删除错误的远程连接，重新连接。

## 3.2. 将当前子项目存档在分支中

进入当前项目`acme-corporation` 的子项目(章节Chapter0201)目录，现在要将这个Chapter0201存档在分支中。
`git remote -v ` 查看远程连接状态
`git status` 查看当前分支状态
`git branch` 查看分支列表
`git branch 分支名字` 新建分支
`git checkout 分支名字` 转到分支
上传文件到新分支
```
git init
git remote add origin 仓库URL
git branch Chapter0201
git checkout Chapter0201
git commit -m "commit 内容"
git push --set-upstream origin Chapter0201
```
