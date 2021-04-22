---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 동의 API 끝점
topic-legacy: developer guide
description: Privacy Service API를 사용하여 Experience Cloud 응용 프로그램에 대한 고객 동의 요청을 관리하는 방법을 알아봅니다.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
translation-type: tm+mt
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 동의 끝점

특정 규정에는 개인 데이터를 수집하기 전에 명시적 고객의 동의를 요구합니다. [!DNL Privacy Service] API의 `/consent` 종단점을 사용하면 고객 동의 요청을 처리하고 이를 개인 정보 보호 워크플로우에 통합할 수 있습니다.

이 안내서를 사용하기 전에 아래의 예제 API 호출에 있는 필수 인증 헤더에 대한 자세한 내용은 [시작하기](./getting-started.md) 섹션을 참조하십시오.

## 고객 동의 요청 처리

동의 요청은 `/consent` 끝점에 POST 요청을 하여 처리됩니다.

**API 형식**

```http
POST /consent
```

**요청**

다음 요청은 `entities` 배열에 제공된 사용자 ID에 대한 새 동의 작업을 만듭니다.

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
| `optOutOfSale` | true로 설정된 경우 `entities`에 제공된 사용자가 개인 데이터의 판매 또는 공유를 거부하려고 함을 나타냅니다. |
| `entities` | 동의 요청이 적용되는 사용자를 나타내는 개체 배열입니다. 각 객체에는 해당 네임스페이스의 개별 사용자와 일치시키는 `namespace` 및 `values` 배열이 포함됩니다. |
| `nameSpace` | `entities` 배열의 각 개체는 Privacy Service API에서 인식하는 [표준 ID 네임스페이스](./appendix.md#standard-namespaces) 중 하나를 포함해야 합니다. |
| `values` | 제공된 `nameSpace`에 해당하는 각 사용자의 값 배열입니다. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>[!DNL Privacy Service]에 보낼 고객 ID 값을 결정하는 방법에 대한 자세한 내용은 [ID 데이터](../identity-data.md)를 제공하는 가이드를 참조하십시오.

**응답**

성공적인 응답은 페이로드가 없는 HTTP 상태 202(허용됨)를 반환하고, 요청이 [!DNL Privacy Service]에 의해 수락되고 처리 중임을 나타냅니다.
