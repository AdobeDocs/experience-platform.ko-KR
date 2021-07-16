---
title: Reactor API의 페이지 매김 응답
description: Reactor API에서 리소스를 나열할 때 결과를 게시하는 방법을 알아봅니다.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Reactor API의 페이지 매김 응답

Reactor API에서 반환된 응답에 페이지 매김됩니다. 기본 페이지 크기는 25개의 요소입니다. 페이지 매김에 대한 자세한 내용은 API 응답 개체의 `meta.pagination `섹션에 나와 있습니다.

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

요청 경로에 `page` 쿼리 매개 변수를 포함하여 특정 페이지를 가져오고 페이지의 크기를 수정할 수 있습니다.

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

다양한 옵션을 함께 결합할 수 있습니다.

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
