---
title: Reactor API에서 응답 정렬
description: Reactor API에서 리소스를 나열할 때 결과를 필터링하는 방법을 알아봅니다.
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Reactor API에서 응답 정렬

Reactor API의 끝점을 나열하면 지정된 속성에 따라 반환된 리소스를 정렬할 수 있습니다. 요청 경로에 `sort` 매개 변수를 제공하여 응답의 정렬 순서를 구성할 수 있습니다.

## 오름차순 정렬

리소스를 속성별로 오름차순으로 정렬할 수 있습니다.
정렬할 기준 특성 및 `+` 접두사로 사용할 특성:

`GET /companies/:company_id/properties?sort=+name`

## 내림차순 정렬

리소스를 속성별로 내림차순으로 정렬할 수 있습니다.
정렬할 기준 특성 및 `-` 접두사로 사용할 특성:

`GET /companies/:company_id/properties?sort=-name`

## 여러 정렬

여러 값을 기준으로 정렬하려면 정렬 지시문을 쉼표로 구분하여 제공합니다
목록:

`GET /companies/:company_id/properties?sort=+name,-org_id`
