---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 동의 API 끝점
description: Privacy Service API를 사용하여 Experience Cloud 애플리케이션에 대한 고객 동의 요청을 관리하는 방법에 대해 알아봅니다.
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# 동의 엔드포인트

특정 규정에서는 개인 데이터를 수집하기 전에 명시적인 고객 동의를 요구합니다. [!DNL Privacy Service] API의 `/consent` 끝점을 사용하면 고객 동의 요청을 처리하고 이를 개인 정보 보호 워크플로에 통합할 수 있습니다.

이 안내서를 사용하기 전에 아래 예제 API 호출에 제공된 필수 인증 헤더에 대한 정보는 [시작하기](./getting-started.md) 안내서를 참조하십시오.

## 고객 동의 요청 처리

동의 요청은 `/consent` 끝점에 대한 POST 요청을 통해 처리됩니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `optOutOfSale` | true로 설정하면 `entities` 아래에 제공된 사용자가 개인 데이터 판매 또는 공유를 거부하려고 함을 나타냅니다. |
| `entities` | 동의 요청이 적용되는 사용자를 나타내는 객체의 배열입니다. 각 개체에는 해당 네임스페이스와 개별 사용자를 일치시키기 위한 `namespace` 및 `values` 배열이 포함되어 있습니다. |
| `nameSpace` | `entities` 배열의 각 개체는 Privacy Service API에서 인식하는 [표준 ID 네임스페이스](./appendix.md#standard-namespaces) 중 하나를 포함해야 합니다. |
| `values` | 제공된 `nameSpace`에 해당하는 각 사용자에 대한 값의 배열입니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>[!DNL Privacy Service]에 보낼 고객 ID 값을 결정하는 방법에 대한 자세한 내용은 [ID 데이터 제공](../identity-data.md)에 대한 안내서를 참조하십시오.

**응답**

성공한 응답은 페이로드가 없는 HTTP 상태 202(허용됨)를 반환하며, 이는 요청이 [!DNL Privacy Service]에 의해 수락되었고 처리 중임을 나타냅니다.
