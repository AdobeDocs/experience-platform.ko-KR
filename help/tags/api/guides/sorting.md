---
title: Reactor API에서 응답 정렬
description: Reactor API에서 리소스를 나열할 때 결과를 필터링하는 방법을 알아봅니다.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Reactor API에서 응답 정렬

Reactor API에서 끝점을 나열하면 지정된 특성에 따라 반환된 리소스를 정렬할 수 있습니다. 요청 경로에 `sort` 매개 변수를 제공하여 응답의 정렬 순서를 구성할 수 있습니다.

## 오름차순 정렬

리소스는
정렬할 속성의 다음 `+` 를 사용하여 사전 고정합니다.

`GET /companies/:company_id/properties?sort=+name`

## 내림차순 정렬

리소스는
정렬할 속성의 다음 `-` 를 사용하여 사전 고정합니다.

`GET /companies/:company_id/properties?sort=-name`

## 여러 정렬

여러 값으로 정렬하려면 정렬 지시어를 쉼표로 구분하여 입력합니다
목록:

`GET /companies/:company_id/properties?sort=+name,-org_id`
