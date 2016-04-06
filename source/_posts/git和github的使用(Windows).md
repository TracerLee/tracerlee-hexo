---
title: git和github的使用(Windows)
date: 2016-04-03 02:33:09
tags: 工具
---

## 安装 [git](https://git-scm.com/download/win)

* Windows: 下载并安装[git](https://git-scm.com/download/win)
* 安装过程一直选择下一步即可，个性化需求可自行配置

## github配置

* $ git config --global user.name "Tracer Lee"
* $ git config --global user.email "example@example.com"
* 使用SSH连接方式
  * 按照[Generating an SSH key](https://help.github.com/articles/generating-an-ssh-key/)教程创建SSH key
* 克隆项目
  * $ git clone git@github.com:TracerLee/tracerlee.github.io.git
  * Warning: Permanently added the RSA host key for IP address '192.30.252.128' to the list of known hosts.
    fatal: Could not read from remote repository.
  * 出现警告后使用以下方式解决：
    * $ ssh -T git@github.com（不行就用这个：$ ssh -T -p 443 git@ssh.github.com）
    * 提示，输入yes，输入passphrase
  * 重新git clone，问题解决
* 修改，添加，提交
  * $ git add .
  * $ git commit -m "This is a message."
  * $ git push origin master