---
title: Reactor API에서 응답 페이지 지정
description: Reactor API에서 리소스를 나열할 때 결과에 페이지를 매기는 방법을 알아봅니다.
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Reactor API에서 응답 페이지 지정

Reactor API에서 반환한 응답에는 페이지가 지정됩니다. 기본 페이지 크기는 25개 요소입니다. 페이지 매김에 대한 세부 사항은 다음에 보고됩니다. `meta.pagination `섹션( API 응답 개체):

```json
"meta": {
  "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 4,
      "total_count": 90
  }
}
```

특정 페이지를 가져올 수 있으며, 다음을 포함하여 페이지 크기를 수정할 수 있습니다. `page` 요청 경로의 쿼리 매개 변수입니다.

## 특정 페이지 검색

특정 페이지를 가져오려면 다음을 수행하십시오.

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## 페이지 크기 변경

페이지 크기를 변경하려면:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

서로 다른 옵션을 함께 결합할 수 있습니다.

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
