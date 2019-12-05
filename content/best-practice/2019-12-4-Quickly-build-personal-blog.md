---
title: Hexo + Serverless Framework，简单三步搭建你的个人博客
description: 简单三步，即可通过 Serverless Website 组件快速构建一个 Serverless Hexo 站点。
date: 2019-12-05
thumbnail: https://main.qcloudimg.com/raw/15052bcfdb9cd73bb65b2037a63fa412.png
authors:
  - liujiang
authorslink:
  - https://github.com/tinafangkunding
---

很多人都想拥有自己的个人博客，还得看起来漂亮、酷酷的。尤其对开发者来说，不仅可以分享技术（装）心得（逼），面试的时候还能成为加分。这里介绍两款好用的神器，不用忙前（前端）忙后（后端），简单 3min 即可搞定，本文免费分享给大家。

> PS：不会写代码？没有备案的域名？没有服务器？在这里，这些都不是事儿！

# 工具介绍
**[Serverless Framework](https://github.com/serverless/serverless)**：Serverless Framework 是业界非常受欢迎的无服务器应用框架，开发者无需关心底层资源即可部署完整可用的 Serverless 应用架构。

**[Hexo](https://hexo.io/zh-cn/)**：Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

# 快速开始
 [Serverless Framework](https://github.com/serverless/serverless) 提供了丰富的 [Component](https://github.com/serverless/components) 供用户搭建各种形态的 Serverless 应用。本文将演示通过 [Serverless Website Component](https://github.com/serverless-components/tencent-website) 快速构建一个 Serverless Hexo 站点。
 
  <iframe width="670px" height="442px"  src="//player.bilibili.com/player.html?aid=78057816&cid=133519858&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

[English Version Docs ](https://github.com/tinafangkunding/serverless-hexo/blob/master/README_EN.md)>>: Build a serverless hexo website with serverless website component

1. 安装
2. 配置
3. 部署

## 安装
安装前提：
- [Node.js](https://nodejs.org/en/)（Node.js 版本需不低于 8.6，建议使用 Node.js 10.0 及以上版本）
- [Git](https://git-scm.com/)

如未安装上述应用程序，可以参考[安装说明](https://hexo.io/zh-cn/docs/)。

开始安装 Serverless Framework 和 Hexo。

- 安装 Serverless Framework CLI

```
$ npm install -g serverless
```

- 安装 Hexo

```
$ npm install -g hexo-cli
```

安装 Hexo 完成后，执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```
$ hexo init hexo   # 生成hexo目录
$ cd hexo
$ npm install
```

新建完成后，`hexo` 文件夹的目录如下：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

可以通过 `hexo g` 命令生成静态页面

```
hexo g   # generate
```

> 注：如果希望在本地查看效果，也可以运行下列命令，通过浏览器访问 `localhost:4000` 查看页面效果。

```
hexo s   # server
```

## 配置

在项目目录下，创建 `serverless.yml` 文件，在其中进行如下配置

```yaml
$ touch serverless.yml
# serverless.ymlmyWebsite:
  component: "@serverless/tencent-website"inputs:
    code:
      src: ./hexo/public # Upload static files generated by HEXOindex: index.htmlerror: index.htmlregion: ap-guangzhoubucketName: my-bucket
```

配置完成后，文件目录如下：

```
.
├── .serverless
├── hexo
|   ├── public
|   ├── ...
|   ├── _config.yml
|   ├── ...
|   └── source
└── serverless.yml
```

## 部署
通过 `sls` 命令进行部署，并可以添加 `--debug` 参数查看部署过程中的信息。

如您的账号未登陆或注册腾讯云，您可以直接通过微信扫描命令行中的二维码进行授权登陆和注册。

```
PS serverless --debug

  DEBUG ─ Resolving the template's static variables.
  DEBUG ─ Collecting components from the template.
  DEBUG ─ Downloading any NPM components found in the template.
  DEBUG ─ Analyzing the template's components dependencies.
  DEBUG ─ Creating the template's components graph.
  DEBUG ─ Syncing template state.
  DEBUG ─ Executing the template's components graph.
  DEBUG ─ Starting Website Component.

Please scan QR code login from wechat
Wait login...
Login successful for TencentCloud
  DEBUG ─ Preparing website Tencent COS bucket my-bucket-1250000000.
  DEBUG ─ Deploying "my-bucket-1250000000" bucket in the "ap-guangzhou" region.
  DEBUG ─ "my-bucket-1250000000" bucket was successfully deployed to the "ap-guangzhou" region.
  DEBUG ─ Setting ACL for "my-bucket-1250000000" bucket in the "ap-guangzhou" region.
  DEBUG ─ Ensuring no CORS are set for "my-bucket-1250000000" bucket in the "ap-guangzhou" region.
  DEBUG ─ Ensuring no Tags are set for "my-bucket-1250000000" bucket in the "ap-guangzhou" region.
  DEBUG ─ Configuring bucket my-bucket-1250000000 for website hosting.
  DEBUG ─ Uploading website files from D:\hexotina\localhexo\public to bucket my-bucket-1250000000.
  DEBUG ─ Starting upload to bucket my-bucket-1250000000 in region ap-guangzhou
  DEBUG ─ Uploading directory D:\hexotina\localhexo\public to bucket my-bucket-1250000000
  DEBUG ─ Website deployed successfully to URL: https://my-bucket-1250000000.cos-website.ap-guangzhou.myqcloud.com.

  myWebsite:
    url: https://my-bucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
    env:

  13s » myWebsite » done
```

访问命令行输出的 website url，即可查看属于自己的 Serverless Hexo 站点。

![](https://main.qcloudimg.com/raw/168a86cf7747ce1cfa1dbb8b730d2f75.png)

> 注：如果希望更新 `hexo` 站点中的文章，需要在本地重新运行 `hexo g` 进行生成静态页面，再运行 `serverless` 就可以直接更新到页面啦~

[具体可参考完整模板仓库](https://github.com/tinafangkunding/serverless-hexo)

# 写在最后

本文只是简单展示了如何利用 Serverless Framework 创建一个个人博客，Hexo 拥有丰富的插件系统，大家可以基于 Serverless Framework 和 Hexo 开发更多个性化功能如自定义 Themes、博文置顶、添加小图标等。这两个工具结合使用，开发方便部署快捷，非常适合初入门或者想要快速搭建静态网站的同学。