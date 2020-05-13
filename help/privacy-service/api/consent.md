---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 동의
topic: developer guide
translation-type: tm+mt
source-git-commit: a3178ab54a7ab5eacd6c5f605b8bd894779f9e85
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 1%

---


# 동의

개인 데이터를 수집하기 전에 명시적인 고객 동의를 요구하는 규정도 있었다. 개인 정보 서비스 API의 `/consent` 종단점을 사용하면 고객 동의 요청을 처리하고 개인 정보 보호 워크플로우에 통합할 수 있습니다.

이 안내서를 사용하기 전에 아래의 예제 API 호출에 제시된 필수 인증 헤더에 대한 [정보는 시작하기](./getting-started.md) 섹션을 참조하십시오.

## 고객 동의 요청 처리

종단점에 POST 요청을 작성하여 동의 요청이 `/consent` 처리됩니다.

**API 형식**

```http
POST /consent
```

**요청**

다음 요청은 배열에 제공된 사용자 ID에 대한 새 동의 작업을 `entities` 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| 속성 | 설명 |
| --- | --- |
| `optOutOfSale` | true로 설정된 경우 제공된 사용자가 개인 데이터 판매 또는 공유를 `entities` 거부하려고 함을 나타냅니다. |
| `entities` | 동의 요청이 적용되는 사용자를 나타내는 개체 배열. 각 개체에는 해당 네임스페이스와 개별 사용자 `namespace` 를 일치시킬 수 `values` 있는 하나의 배열 및 배열이 포함됩니다. |
| `nameSpace` | 배열의 각 개체는 `entities` Privacy Service API에서 인식하는 [표준 ID 네임스페이스](./appendix.md#standard-namespaces) 중 하나를 포함해야 합니다. |
| `values` | 제공된 값과 일치하는 각 사용자에 대한 값 배열 `nameSpace`. |

>[!NOTE] 개인정보 보호 서비스로 전송할 고객 ID 값을 결정하는 방법에 대한 자세한 내용은 ID 데이터 [제공 가이드를 참조하십시오](../identity-data.md).

**응답**

성공적인 응답은 페이로드가 없는 HTTP 상태 202(허용됨)를 반환하여 개인 정보 보호 서비스에서 요청을 수락했으며 처리 중임을 나타냅니다.