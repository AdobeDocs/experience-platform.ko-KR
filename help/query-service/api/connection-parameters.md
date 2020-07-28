---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 쿼리 서비스 개발자 가이드
topic: connection parameters
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 1%

---


# 연결 매개 변수

## 샘플 API 호출

이제 사용할 헤더를 이해하므로 [!DNL Query Service] API에 대한 호출을 시작할 준비가 되었습니다. 다음 섹션에서는 [!DNL Query Service] API를 사용하여 수행할 수 있는 다양한 API 호출을 설명합니다. 각 호출에는 일반 API 형식, 필요한 헤더를 표시하는 샘플 요청 및 샘플 응답이 포함됩니다.

### 대화형 서비스에 대한 연결 매개 변수 요청

종단점에 GET 요청을 만들어 [대화형 서비스](../creating-queries/writing-queries.md) 사용을 위한 연결 매개 변수를 검색할 수 `/connection_parameters` 있습니다. 연결 매개 변수를 사용하여 대화형 서비스를 통해 연결하는 클라이언트에 대한 자세한 내용은 [쿼리 서비스 클라이언트에 대한 설명서를 참조하십시오](../clients/overview.md).

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
