---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 미리 보기
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# 개발자 가이드 미리 보기

intro

- 새 미리 보기 만들기
- 특정 미리 보기 결과 검색
- 특정 미리 보기 취소 또는 삭제

## 시작하기

이 안내서에서 사용되는 API 끝점은 세그멘테이션 API의 일부입니다. 계속하기 전에 세그멘테이션 개발자 [안내서를](./getting-started.md)검토하십시오.

특히 세그멘테이션 개발자 안내서의 [시작 섹션은](./getting-started.md#getting-started) 관련 항목에 대한 링크, 문서에서 샘플 API 호출 읽기에 대한 안내, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 포함합니다.

## 새 미리 보기 만들기

종단점에 POST 요청을 만들어 새 미리 보기를 만들 수 `/preview` 있습니다.

**API 형식**

```http
POST /preview
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
  "predicateType": "pql/text",
  "predicateModel": "_xdm.context.profile",
  "graphType": "pdg"
}
 '
```

본문 정보

**응답**

성공적인 응답은 새로 만든 미리 보기에 대한 세부 정보와 함께 HTTP 상태 201(만들어짐)을 반환합니다.

```json
{
  "state": "NEW",
  "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
  "previewQueryStatus": "NEW",
  "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
  "previewExecutionId": 0
}
```

응답 정보, x-location이 없습니다.

## 특정 미리 보기 결과 검색

종단점에 GET 요청을 만들고 요청 경로에서 미리 보기의 `/preview` `id` 값을 제공하여 특정 미리 보기에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}`:검색할 미리 보기의 `id` 값입니다.

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 미리 보기에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
  "state": "RESULT_READY",
  "page": {
    "offset": 0,
    "size": 0
  },
  "results": [],
  "link": {
    "nextPage": ""
  },
  "previewSampledResultsCount": 0
}
```

## 특정 미리 보기 취소 또는 삭제

종단점에 DELETE 요청을 만들고 요청 경로에 미리 보기 `/preview` `id` 값을 제공하여 특정 미리 보기를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}` 삭제할 미리 보기 `id` 값입니다.

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 200을 반환합니다.

```json
{
  "status": true,
  "message": "KILLED"
}
```

## 다음 단계
