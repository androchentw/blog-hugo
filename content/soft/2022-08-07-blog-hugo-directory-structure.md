---
title: "深入瞭解 Hugo Blog 目錄結構"
url: /blog-hugo-directory-structure
# date: 2022-08-07T11:36:16+08:00
date: 2022-08-07T11:36:16+08:00
author: androchentw
type: post
categories:
  - tech
tags:
  - tech
  - blog
  - hugo
share_img: https://d33wubrfki0l68.cloudfront.net/c38c7334cc3f23585738e40334284fddcaf03d5e/2e17c/images/hugo-logo-wide.svg
series: blog
---

<img style="width:40%;" src="https://d33wubrfki0l68.cloudfront.net/c38c7334cc3f23585738e40334284fddcaf03d5e/2e17c/images/hugo-logo-wide.svg">

## Overview

### Challenges

1. 隨著 blog post 越來越多, content/posts 下的 md 會越來越多, 想要好好整理一個大分類, 方便後續文章管理

### Objectives

1. 建立 content/posts 分類 folder structure, 並與 series 相對應

### KRs

1. 2022-08-07 分類所有 blog posts

<!--more-->

## Content

### 實戰: 調整目錄結構

* [Directory Structure](https://gohugo.io/getting-started/directory-structure/)
  * All content for your website will live inside this directory. Each top-level folder in Hugo is considered a content section. 
  * For example, if your site has three main sections—blog, articles, and tutorials—you will have three directories at content/blog, content/articles, and content/tutorials. Hugo uses sections to assign default content types.
      ```
      .
      ├── archetypes
      ├── config.toml
      ├── content
      ├── data
      ├── layouts
      ├── static
      └── themes
      ```

* [Content Types](https://gohugo.io/content-management/types/)
  * Hugo is built around content organized in sections. 
  * A content type is a way to organize your content. 
  * 善用 [Archetypes](https://gohugo.io/content-management/archetypes/) 幫你快速產生文章範本
    * Archetypes are templates used when creating new content.
* [Content Sections](https://gohugo.io/content-management/sections/)
  * Hugo generates a section tree that matches your content.
  * A Section is a collection of pages that gets defined based on the organization structure under the content/ directory.
  * [Nested Sections](https://gohugo.io/content-management/sections/#nested-sections) 
  * 實際上就是直接在 `content` 底下開資料夾, 並且加入 `_index.md` 就可以了!
    ```
    content
    └── blog        <-- Section, because first-level dir under content/
        ├── funny-cats
        │   ├── mypost.md
        │   └── kittens         <-- Section, because contains _index.md
        │       └── _index.md
        └── tech                <-- Section, because contains _index.md
            └── _index.md
    ```

* `config.toml`
  * [mainSections](https://gohugo.io/functions/where/#mainsections)
  * 我們要在 config.toml 新增 menu.main, 讓他能在 navigation bar 顯現
    ```
    [[menu.main]]
      name = "Tech"
      pre = '<i class="fas fa-laptop-code fa-lg"></i>'
      url = "/tech/"
      weight = 1
    ```
  * [Taxonomies](https://gohugo.io/content-management/taxonomies/)
    * Hugo includes support for user-defined taxonomies.
    * Hugo includes support for user-defined groupings of content called taxonomies. Taxonomies are classifications of logical relationships between content.

### Other Reference: 深入瞭解 Hugo 設計

* [Content Organization](https://gohugo.io/content-management/organization/)
  * Hugo assumes that the same structure that works to organize your source content is used to organize the rendered site.
  * The illustration shows three bundles. Note that the home page bundle cannot contain other content pages, although other files (images etc.) are allowed.

  <img style="width:40%;" src="https://d33wubrfki0l68.cloudfront.net/e78d19184b20fb7869c1fbf9af205be3a241f874/45ef3/content-management/organization/1-featured-content-bundles_hu911524202ff4753624ea0b303cf97415_34394_300x0_resize_catmullrom_3.png">

      ```
      .
      └── content
          └── about
          |   └── index.md  // <- https://example.com/about/
          ├── posts
          |   ├── firstpost.md   // <- https://example.com/posts/firstpost/
          |   ├── happy
          |   |   └── ness.md  // <- https://example.com/posts/happy/ness/
          |   └── secondpost.md  // <- https://example.com/posts/secondpost/
          └── quote
              ├── first.md       // <- https://example.com/quote/first/
              └── second.md      // <- https://example.com/quote/second/
      ```

* [Page Bundles](https://gohugo.io/content-management/page-bundles/#branch-bundles)
  * [Branch Bundles](https://gohugo.io/content-management/page-bundles/#branch-bundles)
    * A Branch Bundle is any directory at any hierarchy within the `content/` directory, that contains at least an `_index.md` file.
    ```
    content/
    ├── branch-bundle-1
    │   ├── branch-content1.md
    │   ├── branch-content2.md
    │   ├── image1.jpg
    │   ├── image2.png
    │   └── _index.md
    └── branch-bundle-2
        ├── _index.md
        └── a-leaf-bundle
            └── index.md
    ```

## Conclusion

實際會動到的 code

1. 創建 `content/` 下的 folder, 並加上 `_index.md`. git commit - [feat: add sections](https://github.com/androchentw/blog-hugo/commit/8ea46f265bc3b84c299ba150539ab5ad84432f2f)
2. 調整 `config.toml`, 使之顯示在 nav bar. git commit - [feat: rearrange order weight of nav bar](https://github.com/androchentw/blog-hugo/commit/b5a218edd758a93c836895621ac742dc723b3064) 

### Discussion


### Ref


## Murmur

* 2022-08-07 整理癖...

