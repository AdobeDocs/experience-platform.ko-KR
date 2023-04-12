---
title: 프로필 끝점
description: Reactor API에서 /profiles 종단점을 호출하는 방법을 알아봅니다.
exl-id: d0434098-f49a-45f3-9772-488bd3c134aa
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%

---

# 프로필 끝점

Reactor API에서 프로필은 Adobe Experience Platform 사용자를 나타냅니다. Reactor API는 자체 사용자 및 권한 데이터베이스를 유지 관리하지 않고 대신 에서 관리하는 Adobe ID에 의존합니다 [Adobe의 IMS(ID 관리 시스템)](https://helpx.adobe.com/kr/enterprise/using/identity.html).

프로필에는 자신이 속한 모든 조직, 각 조직 내에 속한 제품 프로필 및 각 제품 프로필에서 가지고 있는 권한을 포함하여 로그인한 사용자에 대한 모든 정보가 포함됩니다.

## 시작하기

이 안내서에 사용된 엔드포인트는 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 계속하기 전에 [시작 안내서](../getting-started.md) 를 참조하십시오.

## 현재 프로필 검색 {#lookup}

에 GET 요청을 수행하여 현재 로그인한 프로필의 세부 사항을 검색할 수 있습니다 `/profile` 엔드포인트.

**API 형식**

```http
GET /profile
```

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 프로필의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{ORG_1}": {
          "name": "Example organization A",
          "admin": true,
          "active": true,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_audiencemanager_int",
            "dma_tartan",
            "dma_dtm",
            "dma_reactor",
            "dma_auditor"
          ],
          "tenant_id": "{TENANT_ID_1}"
        },
        "{ORG_2}": {
          "name": "Example organization B",
          "admin": false,
          "active": false,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_reactor",
            "dma_auditor",
            "dma_tartan"
          ],
          "tenant_id": "{TENANT_ID_2}"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/profile"
    },
    "meta": {
      "rights": [
        "manage_companies"
      ]
    }
  }
}
```
