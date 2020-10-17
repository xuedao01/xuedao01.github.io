---
title: 建站之 Hexo博客备份到Github分支
date: 2020-09-30 22:00:01
tags: 
	- Hexo
	- 建站
	- 博客
---

将hexo生成的静态博客部署到Github Pages的同时，备份hexo根目录文件到Github。

<!--more-->

## 备份

1. 创建仓库[xuedao01.github.io](https://github.com/xuedao01/xuedao01.github.io)，如果同名仓库之前已经创建，请将之前的仓库改名，新建的仓库必须是username.github.io；

2. 将刚刚创建的新仓库 `clone` 至本地，将之前的 hexo 文件夹中的 _config.yml、themes/、source/、scaffolds/、package.json 和 .gitignore 复制至 xuedao01.github.io 文件夹；

   ```
   git clone https://github.com/xuedao01/xuedao01.github.io.git
   ```

3. 将 themes/next/（我用的是 NexT 主题）中的 `.git/` 删除，否则无法将主题文件夹 push；

4. 在 xudao01.github.io 文件夹执行 `npm install` 和 `npm install hexo-deployer-git`（这里分支应该显示为 hexo）；

   ```
   cd xuedao01.github.io
   git checkout -b hexo

   npm install
   npm install hexo-deployer-git
   ```

5. 执行 `git add`、`git commit -m ""`、`git push origin hexo` 来提交 hexo 网站源文件；

   ```
   git add .
   git commit -m ""
   git commit -m "first commit"
   git push origin hexo
   ```

   > 此时Github上应只有hexo分支，且hexo为默认分支（default）。

6. 执行 `hexo g -d` 生成静态网页部署至 Github 上。

   ```
   hexo d -g
   hexo new post "Hexo备份到Github分支上"
   ```

   > 此时Github有两个分支 master + hexo ，且hexo仍为默认分支；xuedao01.github.io可以正常访问。

缺点（暂未解决）：_post里的.md文件直接用Typora编辑无法保存，只能写好再复制进来。





## 修改

在本地对博客修改（包括修改主题样式、发布新文章等）后：

1. 依次执行 `git add`、`git commit -m ""` 和 `git push origin hexo` 来提交 hexo 网站源文件；
2. 执行 `hexo g -d` 生成静态网页部署至 Github 上。

即重复备份的 7-8 步骤，以上两步没有严格的顺序。

## 恢复

重装电脑后，或者在其它电脑上想修改博客：

1. 安装 git；
2. 安装 Nodejs 和 npm；
3. 使用 `git clone git#github.com:WincerChan/WincerChan.github.io.git` 将仓库拷贝至本地；
4. 在文件夹内执行以下命令 `npm install hexo-cli -g`、`npm install`、`npm install hexo-deployer-git`。

## 附录

这里稍作说明：

### 添加 ssh-keys

1. 在终端下运行：`ssh-keygen -t rsa -C "yourname#email.com"`，一路回车；
2. 会在 .ssh 目录生成 `id_rsa`、`id_rsa.pub` 两个文件，这就是密钥对，id_rsa 是私钥，千万不能泄漏出去；
3. 登录 Github，打开「Settings」–>「SSH and GPG keys」，然后点击「new SSH key」，填上任意 Title，在 Key 文本框里粘贴公钥 `id_rsa.pub` 文件的内容，注意不要粘贴成 `id_rsa`，最后点击「Add SSH Key」。

### hexo 的源文件

这里说一下步骤 4 为什么只需要拷贝 6 个，而不需要全部：

1. `_config.yml`站点的配置文件，需要拷贝；
2. `themes/`主题文件夹，需要拷贝；
3. `source` 博客文章的 .md 文件，需要拷贝；
4. `scaffolds/` 文章的模板，需要拷贝；
5. `package.json` 安装包的名称，需要拷贝；
6. `.gitignore` 限定在 push 时哪些文件可以忽略，需要拷贝；
7. `.git/` 主题和站点都有，标志这是一个 git 项目，不需要拷贝；
8. `node_modules/` 是安装包的目录，在执行 `npm install` 的时候会重新生成，不需要拷贝；
9. `public` 是 `hexo g` 生成的静态网页，不需要拷贝；
10. `.deploy_git` 同上，`hexo g` 也会生成，不需要拷贝；
11. `db.json`文件，不需要拷贝。

其实不需要拷贝的文件正是 `.gitignore` 中所忽略的。



------

方法全部来自wincerchen大佬：https://blog.itswincer.com/posts/7efd2818/ ，本文只作记录，方便自己用。
