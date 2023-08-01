---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 설명서 셀프서비스 템플릿
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 YOURSOURCE에 연결하는 방법을 알아봅니다.
exl-id: c6927a71-3721-461e-9752-8ebc0b7b1cca
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '2139'
ht-degree: 1%

---

# 만들기 *소스* 을 사용한 연결 [!DNL Flow Service] API

*이 템플릿을 진행할 때 이탤릭체로 된 모든 단락을 바꾸거나 삭제합니다(이 단락부터 시작).*

*페이지 상단에 있는 메타데이터(제목 및 설명)를 업데이트하여 시작합니다. 이 페이지에서 DNL의 모든 인스턴스를 무시하십시오. 이것은 기계 번역 프로세스가 페이지를 지원하는 여러 언어로 올바르게 번역할 수 있도록 도와주는 태그입니다. 문서를 제출하면 문서에 태그를 추가하겠습니다.*

## 개요

*고객에게 제공하는 가치를 포함하여 회사에 대한 간략한 개요를 제공하십시오. 자세히 읽어보려면 제품 설명서 홈페이지에 대한 링크를 포함하십시오.*

>[!IMPORTANT]
>
>이 소스 커넥터 및 설명서 페이지는 *YourSource* 팀. 문의 사항이나 업데이트 요청은 다음 주소로 직접 문의하십시오. *업데이트를 위해 연락할 수 있는 링크 또는 이메일 주소 삽입*.

## 사전 요구 사항

*이 섹션에서 Adobe Experience Platform 사용자 인터페이스에서 소스 설정을 시작하기 전에 고객이 알아야 할 사항에 대한 정보를 추가합니다. 이 작업은 다음에 대해 수행할 수 있습니다.*

* *허용 목록에 추가 필요*
* *이메일 해시 요구 사항*
* *귀하 측의 계정 세부 사항*
* *플랫폼에 연결하기 위한 API 키를 얻는 방법*

### 필요한 자격 증명 수집

연결하려면 *소스* Experience Platform을 수행하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| *자격 증명 1* | *여기에서 소스의 인증 자격 증명에 대한 간단한 설명을 추가하십시오.* | *여기에 소스의 인증 자격 증명의 예를 추가하십시오.* |
| *자격 증명 2* | *여기에서 소스의 인증 자격 증명에 대한 간단한 설명을 추가하십시오.* | *여기에 소스의 인증 자격 증명의 예를 추가하십시오.* |
| *자격 증명 3* | *여기에서 소스의 인증 자격 증명에 대한 간단한 설명을 추가하십시오.* | *여기에 소스의 인증 자격 증명의 예를 추가하십시오.* |

이러한 자격 증명에 대한 자세한 내용은 *소스* 인증 문서. *여기에 플랫폼의 인증 설명서에 대한 링크를 추가하십시오.*.

## 연결 *소스* 를 사용하여 플랫폼으로 [!DNL Flow Service] API

다음 튜토리얼에서는 다음을 만드는 단계를 설명합니다. *소스* 소스 연결 및 가져올 데이터 흐름 만들기 *소스* 를 사용하여 데이터를 플랫폼에 전송 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### 기본 연결 만들기 {#base-connection}

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 *소스* 요청 본문의 일부인 인증 자격 증명입니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. *소스*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} base connection",
        "description": "{YOURSOURCE} base connection to authenticate to Platform",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "auth": {
            "specName": "OAuth generic-rest-connector",
            "params": {
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}",
                "expirationDate": "{EXPIRATION_DATE}"
            }
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. 이 ID는 소스를 등록하고 를 통해 승인한 후에 검색할 수 있습니다. [!DNL Flow Service] API. |
| `auth.specName` | Platform에 소스를 인증하기 위해 사용하는 인증 유형입니다. |
| `auth.params.` | 소스 인증에 필요한 자격 증명을 포함합니다. |

**응답**

성공한 응답은 고유 연결 식별자를 포함하여 새로 만든 기본 연결을 반환합니다(`id`). 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### 소스 탐색 {#explore}

이전 단계에서 생성한 기본 연결 ID를 사용하여 GET 요청을 수행하여 파일 및 디렉터리를 탐색할 수 있습니다.
다음 호출을 사용하여 가져올 파일의 경로를 찾습니다 [!DNL Platform]:

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

소스의 파일 구조 및 컨텐츠를 탐색하기 위해 GET 요청을 수행할 때 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.


| 매개변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 이전 단계에서 생성된 기본 연결 ID입니다. |
| `objectType=rest` | 탐색하려는 오브젝트의 유형입니다. 현재 이 값은 항상 로 설정됩니다. `rest`. |
| `{OBJECT}` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 해당 값은 탐색하려는 디렉터리의 경로를 나타냅니다. |
| `fileType=json` | Platform으로 가져올 파일의 파일 유형입니다. 현재, `json` 는 유일하게 지원되는 파일 유형입니다. |
| `{PREVIEW}` | 연결 콘텐츠가 미리 보기를 지원하는지 여부를 정의하는 부울 값. |
| `{SOURCE_PARAMS}` | Platform으로 가져올 소스 파일의 매개 변수를 정의합니다. 에 대해 허용된 형식 유형을 검색하려면 `{SOURCE_PARAMS}`, 전체를 인코딩해야 합니다. `list_id` base64의 문자열 아래 예에서는 `"list_id": "10c097ca71"` base64로 인코딩되는 값은 다음과 같습니다. `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`. |


**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 쿼리된 파일의 구조를 반환합니다.

```json
{
  "data": [
    {
      "members": [
        {
          "id": "cff65fb4c5f5828666ad846443720efd",
          "email_address": "roykent@gmail.com",
          "unique_email_id": "72c758cbf1",
          "full_name": "Roy Kent",
          "web_id": 547094062,
          "email_type": "html",
          "status": "subscribed",
          "merge_fields": {
            "FNAME": "Roy",
            "LNAME": "Kent",
            "ADDRESS": {
              "addr1": "",
              "addr2": "",
              "city": "Richmond",
              "state": "Virginia",
              "zip": "",
              "country": "US"
            },
            "PHONE": "",
            "BIRTHDAY": ""
          },
          "stats": {
            "avg_open_rate": 0,
            "avg_click_rate": 0
          },
          "ip_signup": "",
          "timestamp_signup": "",
          "ip_opt": "103.43.112.97",
          "timestamp_opt": "2021-06-01T15:31:36+00:00",
          "member_rating": 2,
          "last_changed": "2021-06-01T15:31:36+00:00",
          "language": "",
          "vip": false,
          "email_client": "",
          "location": {
            "latitude": 0,
            "longitude": 0,
            "gmtoff": 0,
            "dstoff": 0,
            "country_code": "",
            "timezone": ""
          },
          "source": "Admin Add",
          "tags_count": 0,
          "tags": [
             
          ],
          "list_id": "10c097ca71"
        }
      ],
      "list_id": "10c097ca71",
      "total_items": 2,
      "_links": [
        {
          "rel": "self",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
          "method": "GET",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
          "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
        },
        {
          "rel": "parent",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71",
          "method": "GET",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
        },
        {
          "rel": "create",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
          "method": "POST",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
          "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/POST.json"
        }
      ]
    }
  ]
}
```

### 소스 연결 만들기 {#source-connection}

에 POST 요청을 하여 소스 연결을 만들 수 있습니다. [!DNL Flow Service] API. 소스 연결은 연결 ID, 소스 데이터 파일에 대한 경로 및 연결 사양 ID로 구성됩니다.

**API 형식**

```https
POST /sourceConnections
```

**요청**

다음 요청은에 대한 소스 연결을 만듭니다. *소스*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Source Connection",
        "description": "{YOURSOURCE} Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "server": "us6",
            "listId": "10c097ca71"
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회할 때 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `baseConnectionId` | 의 기본 연결 ID *소스*. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID. |
| `data.format` | 형식 *소스* 수집할 데이터. 현재 지원되는 데이터 형식은 `json`. |

**응답**

성공적인 응답은 고유 식별자()를 반환합니다.`id`)을 참조하십시오. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 플랫폼에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

에 대한 POST 요청을 수행하여 대상 XDM 스키마를 생성할 수 있습니다. [스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 다음 자습서를 참조하십시오. [api를 사용하여 스키마 만들기](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### 타겟 데이터 세트 만들기 {#target-dataset}

에 대한 POST 요청을 수행하여 타겟 데이터 세트를 생성할 수 있습니다. [카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)페이로드 내에 대상 스키마의 ID를 제공합니다.

Target 데이터 세트를 만드는 방법에 대한 자세한 단계는 의 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터를 저장할 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 다음에 해당하는 고정 연결 사양 ID를 제공해야 합니다. [!DNL Data Lake]. 이 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마에 대한 고유 식별자, 대상 데이터 세트 및 연결 사양 ID가 있습니다. [!DNL Data Lake]. 이러한 식별자를 사용하여 다음을 사용하여 대상 연결을 만들 수 있습니다. [!DNL Flow Service] 인바운드 소스 데이터를 포함할 데이터 세트를 지정하는 API입니다.

**API 형식**

```https
POST /targetConnections
```

**요청**

다음 요청은에 대한 대상 연결을 만듭니다. *소스*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Target Connection",
        "description": "{YOURSOURCE} Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "5ef4551c52e054191a61a99f"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 대상 연결의 이름입니다. 대상 연결에 대한 정보를 찾을 때 사용할 수 있으므로 대상 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 대상 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 에 해당하는 연결 사양 ID [!DNL Data Lake]. 이 고정 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 형식 *소스* 플랫폼에 가져올 데이터입니다. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트 ID입니다. |


**응답**

성공적인 응답은 새 타겟 연결의 고유 식별자( )를 반환합니다.`id`). 이 ID는 이후 단계에서 필수입니다.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### 매핑 만들기 {#mapping}

소스 데이터를 타겟 데이터 세트에 수집하려면 먼저 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑해야 합니다. 이에 대한 POST 요청을 수행함으로써 수행됩니다. [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) (요청 페이로드 내에 정의된 데이터 매핑 포함)

**API 형식**

```http
POST /conversion/mappingSets
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| 속성 | 설명 |
| --- | --- |
| `xdmSchema` | 의 ID [대상 XDM 스키마](#target-schema) 이전 단계에서 생성됩니다. |
| `mappings.destinationXdmPath` | 소스 속성이 매핑되는 대상 XDM 경로. |
| `mappings.sourceAttribute` | 대상 XDM 경로에 매핑해야 하는 소스 속성입니다. |
| `mappings.identity` | 매핑 세트를 다음에 대해 표시할지 여부를 지정하는 부울 값 [!DNL Identity Service]. |

**응답**

성공적인 응답은 고유한 식별자( )를 포함하여 새로 생성된 매핑의 세부 정보를 반환합니다.`id`). 이 값은 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 플로우 만들기 {#flow}

데이터 가져오기를 위한 마지막 단계 *소스* 를 플랫폼으로 가져와서 데이터 흐름을 만듭니다. 이제 다음 필수 값이 준비되었습니다.

* [소스 연결 ID](#source-connection)
* [Target 연결 ID](#target-connection)
* [ID 매핑](#mapping)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급된 값을 제공하면서 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

수집을 예약하려면 먼저 시작 시간 값을 에포크 시간(초)으로 설정해야 합니다. 그런 다음 빈도 값을 다음 다섯 가지 옵션 중 하나로 설정해야 합니다. `once`, `minute`, `hour`, `day`, 또는 `week`. 간격 값은 두 개의 연속 수집 사이의 기간을 지정하지만, 일회성 수집을 만들 때는 간격을 설정할 필요가 없습니다. 다른 모든 주파수의 경우 간격 값이 보다 크거나 같게 설정되어야 합니다. `15`.


**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} dataflow",
        "description": "{YOURSOURCE} dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "246d052c-da4a-494a-937f-a0d17b1c6cf5"
        ],
        "targetConnectionIds": [
            "7c96c827-3ffd-460c-a573-e9558f72f263"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1625040887",
            "frequency": "minute",
            "interval": 15
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 데이터 흐름의 이름입니다. 이 옵션을 사용하여 데이터 흐름에서 정보를 조회할 수 있으므로 데이터 흐름의 이름이 설명적인지 확인하십시오. |
| `description` | 데이터 흐름에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `flowSpec.id` | 데이터 흐름을 만드는 데 필요한 흐름 사양 ID입니다. 이 고정 ID: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | 흐름 사양 ID의 해당 버전. 이 값의 기본값은 입니다. `1.0`. |
| `sourceConnectionIds` | 다음 [소스 연결 ID](#source-connection) 이전 단계에서 생성됩니다. |
| `targetConnectionIds` | 다음 [대상 연결 ID](#target-connection) 이전 단계에서 생성됩니다. |
| `transformations` | 이 속성에는 데이터에 적용하는 데 필요한 다양한 변형이 포함되어 있습니다. 이 속성은 XDM 규격이 아닌 데이터를 Platform으로 가져올 때 필요합니다. |
| `transformations.name` | 변환에 지정된 이름입니다. |
| `transformations.params.mappingId` | 다음 [매핑 ID](#mapping) 이전 단계에서 생성됩니다. |
| `transformations.params.mappingVersion` | 매핑 ID의 해당 버전. 이 값의 기본값은 입니다. `0`. |
| `scheduleParams.startTime` | 이 속성은 데이터 흐름의 수집 예약에 대한 정보를 포함합니다. |
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. 허용되는 값은 다음과 같습니다. `once`, `minute`, `hour`, `day`, 또는 `week`. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 빈도를 로 설정하면 간격이 필요하지 않습니다. `once` 다음보다 크거나 같아야 합니다. `15` 다른 빈도 값의 경우. |

**응답**

성공적인 응답은 ID( )를 반환합니다.`id`)을 참조하십시오. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## 부록

다음 섹션에서는 데이터 흐름을 모니터링, 업데이트 및 삭제할 수 있는 단계에 대해 설명합니다.

### 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 데이터 흐름 모니터링](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### 데이터 흐름 업데이트

에 PATCH 요청을 하여 데이터 흐름의 이름, 설명, 실행 일정 및 관련 매핑 세트 등 세부 정보를 업데이트합니다. `/flows` 엔드포인트 [!DNL Flow Service] API, 데이터 흐름의 ID 제공. PATCH 요청을 할 때는 데이터 흐름의 고유한 값을 제공해야 합니다 `etag` 다음에서 `If-Match` 머리글입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 데이터 흐름 업데이트](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 계정 업데이트

에 대한 PATCH 요청을 수행하여 소스 계정의 이름, 설명 및 자격 증명을 업데이트합니다. [!DNL Flow Service] 기본 연결 ID를 쿼리 매개 변수로 제공하는 동안 API입니다. PATCH 요청을 할 때는 소스 계정의 고유한 이름을 제공해야 합니다 `etag` 다음에서 `If-Match` 머리글입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 계정 업데이트](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### 데이터 흐름 삭제

에 대한 DELETE 요청을 수행하여 데이터 흐름을 삭제합니다. [!DNL Flow Service] 쿼리 매개변수의 일부로 삭제할 데이터 흐름의 ID를 제공하는 동안 API입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 데이터 흐름 삭제](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### 계정 삭제

에 대한 DELETE 요청을 수행하여 계정을 삭제합니다. [!DNL Flow Service] 삭제할 계정의 기본 연결 ID를 제공하는 동안 API입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 계정 삭제](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).