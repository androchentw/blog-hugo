---
draft: true
title: "DAMA DMBOK2 Data Quality"
url: /dama-dmbok2-data-quality
# date: 2022-12-11T18:28:16+08:00
date: 2022-12-11T19:08:16+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - python
  - data-quality
share_img: https://i.imgur.com/Qe3Dzt6.png
series: data-quality
---

<img style="width:60%;" src="https://i.imgur.com/Qe3Dzt6.png">
<p align="center"><sub><sup>
  Photo by <a href="https://unsplash.com/@clemhlrdt?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Clément Hélardot</a> on <a href="https://unsplash.com/collections/SV-KO-htOoM/tech?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</sup></sub></p>

## Overview

### Challenges

*

### Objectives

1.

### KRs

1. [ ] 2022-08/E 初版完成。



## Content

以 python 實作一段 DAMA DMBOK 2nd 的資料品質驗證 "数据完整性指标"

```py
def check_data_quality(data):  
  # 定义数据质量指标  
  quality_indicators = {  
    "completeness": 0.0,  
    "consistency": 0.0,  
    "accuracy": 0.0,  
    "timeliness": 0.0  
  }

  quality_indicators["completeness"] = check_data_completeness(data)
  quality_indicators["consistency"] = check_data_consistency(data)
  quality_indicators["accuracy"] = check_data_accuracy(data, reference_data)
  quality_indicators["timeliness"] = check_data_timeliness(data, reference_date)

  return quality_indicators
```

```py
def check_data_completeness(data):  
  # 定义数据完整性指标  
  completeness_indicator = 0.0
  # 统计缺失值的数量  
  num_missing_values = data.isnull().sum().sum()
  # 计算完整性指标  
  completeness_indicator = 1 - (num_missing_values / data.size)
  return completeness_indicator

def check_data_consistency(data):  
  # 定义数据一致性指标  
  consistency_indicator = 0.0

  # 检查数据的每一列，统计相同值的数量  
  for col in data.columns:  
  value_counts = data[col].value_counts()  
  max_count = value_counts.max()  
  total_count = value_counts.sum()  
  consistency_indicator += max_count / total_count

  # 计算平均值作为数据一致性指标  
  consistency_indicator /= len(data.columns)
  return consistency_indicator

def check_data_accuracy(data, reference_data):  
  # 定义数据准确性指标  
  accuracy_indicator = 0.0
  # 计算数据的相似度，可以使用编辑距离或 Jaccard 系数等方法  
  accuracy_indicator = calculate_similarity(data, reference_data)
  return accuracy_indicator

def check_data_timeliness(data, reference_date):  
  # 定义数据时效性指标  
  timeliness_indicator = 0.0
  # 统计时间字段的数据  
  time_col = data["time"]
  # 计算时间字段数据的最大值和最小值  
  max_time = time_col.max()  
  min_time = time_col.min()
  # 计算时效性指标  
  timeliness_indicator = (reference_date - min_time) / (max_time - min_time)
  return timeliness_indicator
```

## Murmur

* 2022-12-11: ChatGPT... 比我還懂 😂

<!-- Link -->
