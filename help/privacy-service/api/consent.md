---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 동의 API 끝점
description: Privacy Service API를 사용하여 Experience Cloud 애플리케이션에 대한 고객 동의 요청을 관리하는 방법을 알아봅니다.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 2%

---

# 동의 끝점

특정 규정에서는 개인 데이터를 수집하기 전에 명시적인 고객 동의를 필요로 합니다. 다음 `/consent` 의 엔드포인트 [!DNL Privacy Service] API를 사용하면 고객 동의 요청을 처리하고 개인 정보 보호 워크플로우에 통합할 수 있습니다.

이 안내서를 사용하기 전에 [시작하기](./getting-started.md) 아래의 예제 API 호출에 제공된 필수 인증 헤더에 대한 자세한 내용은 안내서 를 참조하십시오.

## 고객 동의 요청 처리

동의 요청은 POST에 요청하여 처리됩니다 `/consent` 엔드포인트.

**API 형식**

```http
POST /consent
```

**요청**

다음 요청은에서 제공하는 사용자 ID에 대한 새 동의 작업을 만듭니다 `entities` 배열입니다.

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
| `optOutOfSale` | 가 true로 설정되면 사용자가 `entities` 개인 데이터 판매 또는 공유를 옵트아웃하려고 합니다. |
| `entities` | 동의 요청이 적용되는 사용자를 나타내는 개체 배열입니다. 각 개체에는 `namespace` 그리고 `values` 개별 사용자를 해당 네임스페이스와 일치시킵니다. |
| `nameSpace` | 의 각 개체 `entities` 배열에는 다음 중 하나가 포함되어야 합니다 [표준 id 네임스페이스](./appendix.md#standard-namespaces) Privacy Service API에 의해 인식됩니다. |
| `values` | 제공된 와 해당하는 각 사용자의 값 배열입니다 `nameSpace`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>전송할 고객 ID 값을 결정하는 방법에 대한 자세한 내용 [!DNL Privacy Service]에 대해서는 안내서를 참조하십시오. [id 데이터 제공](../identity-data.md).

**응답**

성공적으로 응답하면 페이로드가 없는 HTTP 상태 202(허용됨)를 반환하여 요청이 수락되었음을 나타냅니다. [!DNL Privacy Service] 그리고 처리 중입니다.
