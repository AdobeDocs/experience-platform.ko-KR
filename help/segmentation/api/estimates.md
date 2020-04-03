---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 예상
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7

---


# 예상

intro

- 특정 예상 작업의 결과 검색

## 시작하기

이 안내서에서 사용되는 API 끝점은 세그멘테이션 API의 일부입니다. 계속하기 전에 세그멘테이션 개발자 [안내서를](./getting-started.md)검토하십시오.

특히 세그멘테이션 개발자 안내서의 [시작 섹션은](./getting-started.md#getting-started) 관련 항목에 대한 링크, 문서에서 샘플 API 호출 읽기에 대한 안내, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 포함합니다.

## 특정 예상 작업의 결과 검색

GET 요청을 `/estimate` 끝점에 만들고 요청 경로에서 예상 작업의 `id` 값을 제공하여 특정 예상 작업의 세부 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /estimate/{PREVIEW_ID}
```

- `{PREVIEW_ID}`:검색할 예상 작업의 `id` 값.

**요청**

다음 요청은 특정 예상 작업의 결과를 가져옵니다.

//미리 보기 ID를 받아야 함

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/{PREVIEW_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 예상 작업의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
  "estimatedSize": 0,
  "numRowsToRead": 1,
  "state": "RESULT_READY",
  "profilesReadSoFar": 1,
  "standardError": 0,
  "error": {
    "description": "",
    "traceback": ""
  },
  "profilesMatchedSoFar": 0,
  "totalRows": 1,
  "confidenceInterval": "95%",
  "_links": {
    "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
  }
}
```

## 다음 단계

작업 결과 예측 방법을 알고 있으므로