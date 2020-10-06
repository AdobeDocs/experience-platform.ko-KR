---
title: Adobe Experience Platform 릴리스 정보
description: 2020년 10월 Experience Platform 릴리스 노트
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 39668013723dcda332558b74cf72b5f93db04461
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 14%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜:2020년 10월**

- [데이터 준비](#data-prep)

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 XDM(Experience Data Model)을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| `is_set` 함수 위에 있어야 합니다 | 이 `is_set` 함수를 사용하면 소스 데이터 내에 속성이 있는지 확인할 수 있습니다. `is_set` 과 함께 사용하여 속성 `is_empty` 의 존재와 속성 내의 값 존재를 모두 확인할 수 있습니다. |
| `get_values` 함수 위에 있어야 합니다 | 이 `get_values` 함수를 사용하면 주어진 키에 대한 입력 맵에서 값을 가져올 수 있습니다. |

자세한 내용은 [데이터 준비 개요를 참조하십시오](../../data-prep/home.md).