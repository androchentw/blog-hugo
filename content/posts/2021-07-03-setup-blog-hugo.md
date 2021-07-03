---
title: "Setup Blog Hugo"
url: /setup-blog-hugo
date: 2021-07-03T20:51:44+08:00
author: androchentw
type: post
categories:
  - Dev
tags:
  - blog
share_img: https://d33wubrfki0l68.cloudfront.net/c38c7334cc3f23585738e40334284fddcaf03d5e/2e17c/images/hugo-logo-wide.svg
---

## 1. Setup github page: project. 

```sh
git clone https://github.com/androchentw/blog-hugo.git
```


## 2. Install Hugo

* [Hugo - Quick Start](https://gohugo.io/getting-started/quick-start/)
* [Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

```sh
brew install hugo
hugo new site blog-hugo
cd blog-hugo
git submodule add https://github.com/appleboy/blog-theme.git themes/beautifulhugo
echo 'theme = "beautifulhugo"' >> config.toml

hugo new posts/hello_world.md

# to preview at http://localhost:1313/
hugo server -D	

# to build static page
hugo -D
```

# 3. Setup GitHub Action

* [深入但不淺出，如何用 github actions 自動發佈 gh-pages](https://milkmidi.medium.com/深入但不淺出-如何用-github-actions-自動發佈-gh-pages-8183464dfe84)
* [從零開始: 用github pages 上傳靜態網站](https://medium.com/進擊的-git-git-git/從零開始-用github-pages-上傳靜態網站-fa2ae83e6276)
[About GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#user--organization-pages)


## References

1. [將部落格從 Wordpress 轉換到 Hugo](https://blog.wu-boy.com/2021/05/migrate-wordpress-to-hugo/)
2. [ghostToHugo](https://dwmkerr.com/migrating-from-ghost-to-hugo/)
3. [Hugo - Front Matter](https://gohugo.io/content-management/front-matter/)
4. [Hugo - Archetypes](https://gohugo.io/content-management/archetypes/)
5. [Hugo - URL Management](https://gohugo.io/content-management/urls/)
