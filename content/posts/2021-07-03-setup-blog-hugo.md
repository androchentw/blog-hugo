---
title: "Setup Blog Hugo"
date: 2021-07-03T20:51:44+08:00
author: androchentw
type: post
url: /2021/07/Setup-Blog-Hugo/
share_img: https://d33wubrfki0l68.cloudfront.net/c38c7334cc3f23585738e40334284fddcaf03d5e/2e17c/images/hugo-logo-wide.svg
categories:
  - Golang
  - Blog
  - Hugo
tags:
  - golang
  - hugo
---

## 1. Setup github page: project. 

* https://androchentw.github.io/blog-hugo

```sh
git clone https://github.com/androchentw/blog-hugo.git
```


## 2. Install Hugo

* https://gohugo.io/getting-started/quick-start/

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


## References

1. https://gohugo.io/hosting-and-deployment/hosting-on-github/
2. https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#user--organization-pages
3. https://blog.wu-boy.com/2021/05/migrate-wordpress-to-hugo/
4. https://milkmidi.medium.com/深入但不淺出-如何用-github-actions-自動發佈-gh-pages-8183464dfe84