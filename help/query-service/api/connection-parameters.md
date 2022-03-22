---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;api 안내서;연결 매개 변수;쿼리 서비스;
solution: Experience Platform
title: 연결 매개 변수 API 끝점
topic-legacy: connection parameters
description: /connection_parameters 종단점에 GET 요청을 수행하여 대화형 서비스를 사용하기 위한 연결 매개 변수를 검색할 수 있습니다.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: cff95575530e0db00d34ff1ea4c90e5422b6562d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# 연결 매개 변수 끝점

## 샘플 API 호출

다음 섹션에서는 를 사용하여 수행할 수 있는 API 호출을 안내합니다. [!DNL Query Service] API. 이 호출에는 일반 API 형식, 필수 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함되어 있습니다.

### 연결 매개 변수 요청

에 GET 요청을 수행하여 연결 매개 변수를 검색할 수 있습니다 `/connection_parameters` 엔드포인트. 대화형 서비스를 통해 연결하기 위해 연결 매개 변수를 사용하는 클라이언트에 대한 자세한 내용은 다음 문서를 참조하십시오. [쿼리 서비스 클라이언트](../clients/overview.md).

**API 형식**

```http
GET /connection_parameters
```

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 연결 매개 변수와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
