---
title: "開箱即用的 Python 專案結構與 PyTest"
url: /python-project-structure-with-pytest
# date: 2022-09-06T20:28:16+08:00
date: 2022-09-06T20:34:16+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - testing
share_img: https://i.imgur.com/Qe3Dzt6.png
series: testing
---

<img style="width:60%;" src="https://i.imgur.com/Qe3Dzt6.png">
<p align="center"><sub><sup>
  Photo by <a href="https://unsplash.com/@clemhlrdt?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Clément Hélardot</a> on <a href="https://unsplash.com/collections/SV-KO-htOoM/tech?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</sup></sub></p>

## Overview

### Challenges 現況 挑戰

* 該如何設計良好可擴充的 python 專案目錄結構? 有什麼 naming convention 嗎?

### Objectives 目標 效益

* 結合 PyTest 等各 Python Testing Framework, 研究並建立一個 Python Project 範本, 方便未來直接使用及擴充

### KRs 結果 解法

* [ ] 2022-09-09: 優化 [python-playground](https://github.com/androchentw/python-playground) 的目錄結構. 詳見 [Github - Python Playground](https://blog.androchen.tw/github-python-playground/)

<!--more-->

## 開箱即用

### Ref

* [Effective Python Testing With Pytest](https://realpython.com/pytest-python-testing/)
* [Project Structure with pytest | pylenium](https://docs.pylenium.io/getting-started/project-structure-with-pytest)

### PyTest hello world demo

下面是一個簡單的 PyTest 程式碼示例，用於測試一個名為 "hello()" 的函數，該函數應返回字符串 "Hello, world!"。

首先，建立一個名為 `hello.py` 的檔案，並在其中添加以下程式碼：

```py
def hello():  
return "Hello, world!"
```

接下來，建立一個名為 `test_hello.py` 的檔案，並在其中添加以下程式碼：

```py
import hello

def test_hello():  
assert hello.hello() == "Hello, world!"
```

在上面的程式碼中，我們匯入了前面寫的 `hello.py` 檔案，並測試了 `hello()` 函數的輸出。

最後，在終端機中運行以下命令，以執行 PyTest 測試：

```sh
pytest
```

如果測試成功，您應該會看到以下輸出：

```sh
$ pytest
= test session starts ==
platform linux-Python 3.8.5, pytest-6.1.1, py-1.9.0, pluggy-0.13.1
rootdir: /path/to/your/project
collected 1 item

test_hello.py .                                                        [100%]

1 passed in 0.01s =
```

這樣，您就成功地寫好了一個 PyTest 的 hello world 示例。您可以持續擴展測試程式碼，以滿足您的測試需求。

### Ref: 列出編輯時間超過 7 天的檔案

以 python script 列出 linux server 的 ~/download folder 下, 上一次編輯時間超過 7 天的檔案

```py
# 匯入 os 模組
import os

# 獲取當前時間
current_time = int(time.time())

# 獲取 7 天前的時間
seven_days_ago = current_time - 7 * 24 * 60 * 60

# 列出檔案
for file in os.listdir('~/download'):  
# 獲取檔案的最後修改時間  
last_modified_time = os.path.getmtime(file)

# 如果檔案的最後修改時間大於 7 天前的時間，則列出檔案  
if last_modified_time > seven_days_ago:  
print(file)
```

## Murmur

* 2022-09-06: 9 月就是測試月!
* 2022-12-10: 補上 ChatGPT 產生的答案 😆
