---
keywords: Experience Platform;홈;인기 항목;소스;API;탐색;흐름 서비스
title: 흐름 서비스 API를 사용하여 테이블 형식 소스 탐색
description: 이 자습서에서는 흐름 서비스 API를 사용하여 테이블 기반 소스의 컨텐츠와 구조를 살펴봅니다.
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: 3bdeec8284873b8d9368f833b24e9922ed489019
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 2%

---

# 다음을 사용하여 데이터 테이블 탐색 [!DNL Flow Service] API

이 자습서에서는 를 사용하여 데이터 테이블의 구조와 컨텐츠를 탐색하고 미리 보는 방법에 대한 단계를 제공합니다 [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
> 데이터 테이블을 탐색하려면 테이블 형식 소스에 대한 유효한 기본 연결 ID가 이미 있어야 합니다. 이 ID가 없는 경우 테이블 형식 소스에 대한 기본 연결 ID를 만드는 방법에 대한 단계를 알려면 다음 튜토리얼을 참조하십시오. <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[고객 성공](../../../home.md#customer-success)</li><li>[데이터베이스](../../../home.md#database)</li><li>[전자 상거래](../../../home.md#ecommerce)</li><li>[마케팅 자동화](../../../home.md#marketing-automation)</li><li>[결제](../../../home.md#payments)</li><li>[프로토콜](../../../home.md#protocols)</li></ul>

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../landing/api-guide.md).

## 데이터 테이블 탐색

에 GET 요청을 하여 데이터 테이블의 구조에 대한 정보를 검색할 수 있습니다. [!DNL Flow Service] 소스의 기본 연결 ID를 제공하는 동안 API입니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 소스의 기본 연결 ID입니다. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 소스의 테이블 배열을 반환합니다. Platform으로 가져올 테이블을 찾아 기록해 두십시오. `path` 속성을 다음 단계에서 제공해야 구조를 검사할 수 있습니다.

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## 표 구조 Inspect

GET 데이터 테이블의 내용을 검사하려면 [!DNL Flow Service] 쿼리 매개 변수로 테이블의 경로를 지정하는 동안 API입니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 소스의 기본 연결 ID입니다. |
| `{TABLE_PATH}` | 검사할 테이블의 경로 속성입니다. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 테이블의 내용과 구조에 대한 정보를 반환합니다. 각 테이블 열에 대한 세부 사항은 의 요소 내에 있습니다. `columns` 배열입니다.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "TestID",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Name",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## 다음 단계

이 자습서를 따라 데이터 테이블의 구조 및 내용에 대한 정보를 수집했습니다. 또한 Platform으로 수집하려는 표의 경로를 검색했습니다. 이 정보를 사용하여 소스 연결 및 데이터 흐름을 만들어 데이터를 플랫폼으로 가져올 수 있습니다. 를 사용하여 소스 연결 및 데이터 흐름을 만드는 방법에 대한 특정 단계는 다음 자습서를 참조하십시오 [!DNL Flow Service] API:

* [광고 소스](../collect/advertising.md)
* [CRM 소스](../collect/crm.md)
* [고객 성공 소스](../collect/customer-success.md)
* [데이터베이스 소스](../collect/database-nosql.md)
* [전자 상거래 소스](../collect/ecommerce.md)
* [마케팅 자동화 소스](../collect/marketing-automation.md)
* [결제 소스](../collect/payments.md)
* [프로토콜 소스](../collect/protocols.md)
