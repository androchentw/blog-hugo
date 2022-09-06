---
title: "自動化測試的 7 種類型"
url: /7-types-of-test-automation
# date: 2022-08-28T01:28:16+08:00
date: 2022-08-28T03:08:16+08:00
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

測試種類百百種, 你測的是哪一種? 該測的又是哪一種? 讓我們來一探究竟!
本文暫不討論為何要寫測試, 效益為何. 有興趣的朋友敬請期待下一篇文章 :P

一言以蔽之就是品質. 不測試的話就只是盲目地相信自己的程式碼永遠都會正常運作. 而這個信仰通常十分薄弱, 基本上都只是落入維運時 見一個修一個, 很難查 root cause 的惡性循環. 
細節就留待我最近邊學 TDD 時再來記錄囉~

### Challenges

* 測試初心者, 不確定該寫哪些測試才是有效的 (Effective & Efficient)

### Objectives

1. 瞭解自動化測試的類型與其定義
2. 建立測試範例程式碼, 結合 [python-playground]. 詳見 {{< ref . "content/python/2022-08-16-github-python-playground" >}}

### KRs

1. [x] 2022-08/E 初版完成。


<!--more-->

## Content

### Test Scenario 測試場景

在開始任何測試之前, 確立想要測試的場景、目標、範圍 (scenario, target, scope) 是非常重要的。

相關範例程式碼請參考 [python-playground] 的 [pgtest.py 與 sample/test/*.py](https://github.com/androchentw/python-playground/blob/main/sample/pgtest.py). 使用 [PyTest 開源測試框架](https://docs.pytest.org/en/7.1.x/).

### Types & Definitions 自動化測試的類型與其定義

這裡直接引用 [Atlassian - The different types of software testing](https://www.atlassian.com/continuous-delivery/software-testing/types-of-software-testing)

#### Unit tests 單元測試

* 測個別獨立的 methods & functions. 最基本常見的一種測試方式. 通常能在一秒內跑完.
* 適用場景: 基本邏輯檢查.
* 原文
  * Unit tests are very low level and close to the source of an application. They consist in testing **individual methods and functions** of the classes, components, or modules used by your software. Unit tests are generally quite cheap to automate and can run very quickly by a continuous integration server.

```py
# pgtest_sample_func.py
def equal(param1, param2):
    return param1 == param2

# test_equal.py
def test_equal():
    assert pgtest_sample_func.equal(1, 1) == True
    assert pgtest_sample_func.equal(-2, -2) == True
    assert pgtest_sample_func.equal("0", "0") == True
    assert pgtest_sample_func.equal(1e3, 1000) == True
    assert pgtest_sample_func.equal(1e-2, 0.01) == True
    assert pgtest_sample_func.equal(1.02e03, 1020) == True
```

#### Integration tests 整合測試

* 測試多個 module 放在一起時能正常運作. 常會需要串聯多個 services, 執行時間也會較長.
* 適用場景: 多個模組整合運作檢查.
* 原文
  * Integration tests verify that **different modules or services** used by your application work well together. For example, it can be testing the interaction with the database or making sure that microservices work together as expected. These types of tests are more expensive to run as they require multiple parts of the application to be up and running.

```py
# TODO multiple modules
def test_integration():
    assert False
```

#### Functional tests 功能測試

* 測試應用的 output 產出, 而非中間狀態. 
* 常與 integration tests 搞混. 差別是 functional test 關注的是 產品定義/要求的 "output 產出".
* 適用場景: 驗證 產品定義/要求的 output 如預期, 符合規格 (specification).
* 原文
  * Functional tests focus on the **business requirements** of an application. They only verify the **output** of an action and do not check the intermediate states of the system when performing that action.
  * There is sometimes a **confusion between integration tests and functional tests** as they both require multiple components to interact with each other. The difference is that an integration test may simply verify that you can query the database while a functional test would expect to get a specific value from the database as defined by the **product requirements**.

```py
# TODO: output of product requirements
def test_functional():
    assert False
```

#### End-to-end tests 端對端測試

* 仿照 user behavior 如何操作你的應用. 各種不同使用情境/操作流程. 
* 非常有用, 代價也很昂貴, 不易維護. 建議針對關鍵場景測試是否有重大改變.
* 適用場景: 測試 使用者操作流程.
* 原文
  * End-to-end testing **replicates a user behavior** with the software in a complete application environment. It verifies that various user flows work as expected and can be as simple as loading a web page or logging in or much more complex scenarios verifying email notifications, online payments, etc...
  * End-to-end tests are very useful, but they're **expensive** to perform and can be **hard to maintain** when they're automated. It is recommended to have a few key end-to-end tests and rely more on lower level types of testing (unit and integration tests) to be able to quickly identify **breaking changes**.

```py
# TODO: user behavior
def test_end_to_end():
    assert False
```

#### Acceptance testing 驗收測試

* 測試系統是否滿足業務需求. 可能包含效能測試. 屬於黑箱測試.
* 適用場景: 交付前, 正式測試系統/應用業務需求與設計規格.
* 原文
  * Acceptance tests are formal tests that verify if a **system satisfies business requirements**. They require the entire application to be running while testing and focus on replicating user behaviors. But they can also go further and measure the performance of the system and reject changes if certain goals are not met.

```py
# TODO: user behavior + performance meet specication and criteria
def test_acceptance():
    assert False
```

#### Performance testing 效能測試

* 測試系統效能符合預期. 可能包含一些平均/尖峰壓力測試, monkey testing 或甚至 Chaos engineering
* 適用場景: 測試系統 反應速度與穩定性.
* 原文
  * Performance tests evaluate how a system performs under a particular workload. These tests help to measure the **reliability, speed, scalability, and responsiveness** of an application. For instance, a performance test can observe *response times* when executing a high number of requests, or determine how a system behaves with a significant amount of data. It can determine if an application meets performance requirements, locate bottlenecks, measure stability during peak traffic, and more. 

```py
# TODO: test peek trafic 
def test_performance():
    assert False
```

#### Smoke testing 冒煙測試

* 測試主要功能運作正常. 旨在快速執行.
* 適用場景: 在新的部署環境中驗證一切如預期.
  * Smoke tests are basic tests that check the **basic functionality** of an application. They are meant to be quick to execute, and their goal is to give you the assurance that the **major features** of your system are working as expected.
  * Smoke tests can be useful right after a new build is made to decide whether or not you can run more expensive tests, or right after a deployment to make sure that they application is running properly in the **newly deployed environment**.

```py
# TODO: test basic functionality of major features in newly deployed environment
def test_smoke():
    assert False
```


## Murmur

* 2022-08-28: 測都測!


<!-- Link -->
[python-playground]: https://github.com/androchentw/python-playground
