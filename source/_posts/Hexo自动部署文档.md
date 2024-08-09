---
title: Actions实现Hexo个人博客在GIthubPages上的自动部署
date: 2024-08-08
updated: 
tags:  ["Hexo","GIthubPages","GIthubActions"]
categories: 部署
keywords:
description:
top_img:
comments:
cover:
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
abcjs:

---

# 本地部署Hexo并进行配置

## 安装

> 详情参考：[文档 | Hexo](https://hexo.io/zh-cn/docs/)

- Git

- Node.js

- Hexo

```
    $ npm install -g hexo-cli //全局安装
    $ npm install hexo //局部安装
    
```

## Hexo初始化

- 新建文件夹初始化Hexo框架

```
hexo init
```

- 清除部署缓存并开启本地服务 

```
hexo clean
    hexo server
    //访问localhost:4000可以看到hexo的helloWorld博客界面
    hexo clean
    hexo server
    //访问localhost:4000可以看到hexo的helloWorld博客界面
```




## 主题

### 下载

- 从github上拉取或者通过NPM下载

```
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
    
    npm i hexo-theme-butterfly
    //放置到目录下的theme文件夹中
```
- 修改 hexo 配置文件`_config.yml`

```yaml
    theme:主题名称
```

- **！！！记得删除.git文件不然无法push到gihub中**



### 配置

> 参考文档：[Butterfly 安裝文檔(一) 快速開始 | Butterfly](https://butterfly.js.org/posts/21cfbf15/)

- 一般配置_config.yml文件



# GIthubPages挂载

## 创建仓库

- 仓库名必须是：你的用户名.github.io

## Hexo一键部署

- 安装 [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)。

```
$ npm install hexo-deployer-git --save
```

- 编辑 **_config.yml** （示例值如下所示）：

```yaml
deploy:
  type: git
  repo: <repository url> # 创建的仓库远程连接
  branch: gh_pages # 注意分支名，要与之后的actions中配置相对应，最好就用这个
```

```
  //博客根目录执行
  hexo clean //清除旧的部署文件
  hexo deploy //一键部署
```

- 等待GithubActions执行结束

- 进入仓库Setteings查看Pages

  - 可以看到分支gh_pages已经挂载到Pages上
  - 点击https://你的用户名.github.io/可以访问到博客



# Actions实现自动化挂载

## 创建工作流

- 在根目录的.github文件夹中创建workflows文件夹

- 在workflows文件夹中创建page.yml(名称无所谓）

- 编写部署流程：
```yaml
    name: Pages
    
    # 触发器、分支
    on:
      push:
        branches:
          - master  # default branch
    jobs:
      # 子任务
      pages:
        runs-on: ubuntu-latest # 定运行所需要的虚拟机环境                     1
        permissions:
          contents: write
        steps:
          - uses: actions/checkout@v2
            # with:
            #   submodules: true
            #   fetch-depth: 0
          # 每个name表示一个步骤:step
          - name: Use Node.js 16.x
            uses: actions/setup-node@v2
            with:
              node-version: '18.19.0' # 自己正在使用的node版本即可            2
          - name: 安装 Hexo
            run: |
              export TZ='Asia/Shanghai'
              npm install hexo-cli -g
          - name: 缓存 Hexo                   #                            3 
            id: cache-npm
            uses: actions/cache@v3
            env:
              cache-name: cache-node-modules
            with:
              path: node_modules
              key: ${{ runner.os }}-build-${{ env.cache-name }}-${{ hashFiles('**/package-lock.json') }}
              restore-keys: |
                ${{ runner.os }}-build-${{ env.cache-name }}-
                ${{ runner.os }}-build-
                ${{ runner.os }}-
          - name: 安装依赖                     #                            4
            if: ${{ steps.cache-npm.outputs.cache-hit != 'true' }}
            run: |
              npm install --save
          - name: 查看插件
            run: |
              npm ls --depth 0
              
          - name: 生成静态文件                  #                            5
            run: |
              hexo clean
              hexo generate
    
          - name: Deploy                     #                             6
            uses: peaceiris/actions-gh-pages@v3 
            with:
              deploy_key: ${{ secrets.ACTIONS_DEPLOY_KEY  }}
              user_name: heaven
              user_email: heaven@163.com
              # 获取提交文章源码时的commit message，作为发布gh-pages分支的信息
              commit_message: ${{ github.event.head_commit.message }}
              full_commit_message: ${{ github.event.head_commit.message }}
              github_token: ${{ secrets.GITHUB_TOKEN }}
              # GITHUB_TOKEN不是个人访问令牌，GitHub Actions 运行器会自动创建一个GITHUB_TOKEN密钥
              # 以在您的工作流程中进行身份验证。因此，您无需任何配置即可立即开始部署
              publish_dir: ./public
              allow_empty_commit: true # 允许空提交
          # Use the output from the `deploy` step(use for test action)
          - name: Get the output
            run: |
              echo "${{ steps.deploy.outputs.notify }}"
```



## 部署密钥

### 获取

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key

1. Open Git Bash.

2. Paste the text below, replacing the email used in the example with your GitHub email address.

```shell
   ssh-keygen -t ed25519 -C "your_email@example.com"
```

   **Note:** If you are using a legacy system that doesn't support the Ed25519 algorithm, use:

```shell
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

​	3. 得到id_ed25519.pub（公钥）和id_ed25519（私钥）两个文件

### 配置

- 仓库Settings
- Deploy keys
  - 配置公钥
- Secrets and variables
  - actions
  - New repository secret
    - 配置私钥

- ！！！！ 全部复制粘贴，保持完整

## push到该仓库的一个新建分支

### 等待Actions部署完毕

### 访问https://你的用户名.github.io/
