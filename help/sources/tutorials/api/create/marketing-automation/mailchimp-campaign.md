---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: Flow Service API를 사용하여 Mailchimp Campaign에 대한 데이터 흐름 만들기
topic-legacy: tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 MailChimp Campaign에 연결하는 방법을 알아봅니다.
exl-id: fd4821c7-6fe1-4cad-8e13-3549dbe0ce98
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 2%

---

# 데이터 흐름 만들기 [!DNL Mailchimp Campaign] 흐름 서비스 API 사용

다음 자습서에서는 가져올 소스 연결 및 데이터 흐름을 만드는 단계를 안내합니다 [!DNL Mailchimp Campaign] 데이터를 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 전제 조건

연결하기 전에 [!DNL Mailchimp] OAuth 2 새로 고침 코드를 사용하여 Adobe Experience Platform에 액세스하려면 먼저 액세스 토큰을 검색해야 합니다 [!DNL MailChimp.] 자세한 내용은 [[!DNL Mailchimp] OAuth 2 안내서](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) 액세스 토큰 찾기에 대한 자세한 지침

## 기본 연결 만들기 {#base-connection}

을 검색한 후 [!DNL Mailchimp] 이제 데이터 흐름을 만드는 프로세스를 시작하여 다음을 가져올 수 있습니다 [!DNL Mailchimp Campaign] Platform으로 데이터를 전송할 수 있습니다. 데이터 흐름을 만드는 첫 번째 단계는 기본 연결을 만드는 것입니다.

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

[!DNL Mailchimp] 에서는 기본 인증 및 OAuth 2 새로 고침 코드를 모두 지원합니다. 두 인증 유형을 인증하는 방법에 대한 지침은 다음 예를 참조하십시오.

### 만들기 [!DNL Mailchimp] 기본 인증을 사용한 기본 연결

을(를) 만들려면 [!DNL Mailchimp] 기본 인증을 사용하여 기본 연결에서 `/connections` 끝점 [!DNL Flow Service] 에 대한 자격 증명을 제공하는 동안 API `host`, `authorizationTestUrl`, `username`, 및 `password`.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with basic authentication",
      "description": "Mailchimp Campaign base connection with basic authentication",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인합니다. |
| `description` | (선택 사항) 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. 이 ID는 소스를 등록하고 [!DNL Flow Service] API. |
| `auth.specName` | 소스를 Platform에 연결하는 데 사용하는 인증 유형입니다. |
| `auth.params.host` | 연결하는 데 사용되는 루트 URL입니다 [!DNL Mailchimp] API. 루트 URL의 형식은 다음과 같습니다 `https://{DC}.api.mailchimp.com`, 위치 `{DC}` 계정에 해당하는 데이터 센터를 나타냅니다. |
| `auth.params.authorizationTestUrl` | (선택 사항) 기본 연결을 만들 때 인증 테스트 URL을 사용하여 자격 증명을 확인합니다. 지정하지 않으면 소스 연결 생성 단계 동안 자격 증명이 자동으로 선택됩니다. |
| `auth.params.username` | 사용자 이름과 일치하는 사용자 이름 [!DNL Mailchimp] 계정이 필요합니다. 기본 인증에 필요합니다. |
| `auth.params.password` | 사용자의 [!DNL Mailchimp] 계정이 필요합니다. 기본 인증에 필요합니다. |

**응답**

성공적인 응답은 해당 고유 연결 식별자(`id`). 이 ID는 다음 단계에서 소스의 파일 구조와 컨텐츠를 탐색하는 데 필요합니다.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

### 만들기 [!DNL Mailchimp] OAuth 2 새로 고침 코드를 사용한 기본 연결

을(를) 만들려면 [!DNL Mailchimp] OAuth 2 새로 고침 코드를 사용하여 기본 연결에 대해 POST 요청을 수행하십시오 `/connections` 에 대한 자격 증명을 제공하는 중 끝점입니다. `host`, `authorizationTestUrl`, 및 `accessToken`.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with OAuth 2 refresh code",
      "description": "Mailchimp Campaign base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인합니다. |
| `description` | (선택 사항) 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. 이 ID는 [!DNL Flow Service] API. |
| `auth.specName` | Platform에 소스를 인증하는 데 사용하는 인증 유형입니다. |
| `auth.params.host` | 연결하는 데 사용되는 루트 URL입니다 [!DNL Mailchimp] API. 루트 URL의 형식은 다음과 같습니다 `https://{DC}.api.mailchimp.com`, 위치 `{DC}` 계정에 해당하는 데이터 센터를 나타냅니다. |
| `auth.params.authorizationTestUrl` | (선택 사항) 기본 연결을 만들 때 인증 테스트 URL을 사용하여 자격 증명을 확인합니다. 지정하지 않으면 소스 연결 생성 단계 동안 자격 증명이 자동으로 선택됩니다. |
| `auth.params.accessToken` | 소스를 인증하는 데 사용되는 해당 액세스 토큰. OAuth 기반 인증에 필요합니다. |

**응답**

성공적인 응답은 해당 고유 연결 식별자(`id`). 이 ID는 다음 단계에서 소스의 파일 구조와 컨텐츠를 탐색하는 데 필요합니다.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 소스 탐색 {#explore}

이전 단계에서 생성한 기본 연결 ID를 사용하여 GET 요청을 수행하여 파일 및 디렉토리를 탐색할 수 있습니다. GET 요청을 수행하여 소스의 파일 구조 및 컨텐츠를 탐색할 때는 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 이전 단계에서 생성된 기본 연결 ID입니다. |
| `{OBJECT_TYPE}` | 탐색할 객체의 유형입니다. REST 소스의 경우 이 값의 기본값은 입니다. `rest`. |
| `{OBJECT}` | 탐색할 객체입니다. |
| `{FILE_TYPE}` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 이 값은 탐색할 디렉토리의 경로를 나타냅니다. |
| `{PREVIEW}` | 연결의 내용이 미리 보기를 지원하는지 여부를 정의하는 부울 값입니다. |
| `{SOURCE_PARAMS}` | 기본 64로 인코딩된 문자열의 `campaign_id`. |

>[!TIP]
>
>에 대해 허용되는 형식 유형을 검색하려면 `{SOURCE_PARAMS}`를 인코딩해야 전체 `campaignId` base64의 문자열입니다. 예, `{"campaignId": "c66a200cda"}` base64에서 인코딩은 다음과 같습니다. `eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9`.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&objectType={OBJECT_TYPE}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 쿼리된 파일의 구조를 반환합니다.

```json
{
    "data": [
        {
            "emails": [
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "cff65fb4c5f5828666ad846443720efd",
                    "email_address": "kendall2134@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "a16b82774b211afaf60902d1afd8abc5",
                    "email_address": "logan9935890967@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
            ]
        }
    ]    
}
```

## 소스 연결 만들기 {#source-connection}

에 POST 요청을 수행하여 소스 연결을 만들 수 있습니다 [!DNL Flow Service] API. 소스 연결은 연결 ID, 소스 데이터 파일의 경로 및 연결 사양 ID로 구성됩니다.

소스 연결을 만들려면 데이터 형식 속성에 대한 열거형 값도 정의해야 합니다.

파일 기반 소스에 대해 다음 열거형 값을 사용하십시오.

| 데이터 형식 | 열거형 값 |
| ----------- | ---------- |
| 구분 기호 | `delimited` |
| JSON | `json` |
| 쪽모이 세공 | `parquet` |

모든 테이블 기반 소스의 경우 값을 `tabular`.

**API 형식**

```https
POST /sourceConnections
```

**요청**

다음 요청은에 대한 소스 연결을 만듭니다 [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest campaign ID",
      "description": "MailChimp Campaign source connection to ingest campaign ID",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "campaignId": "c66a200cda"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `baseConnectionId` | 의 기본 연결 ID입니다. [!DNL Mailchimp]. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID입니다. |
| `data.format` | 의 형식 [!DNL Mailchimp] 수집할 데이터입니다. |
| `params.campaignId` | 다음 [!DNL Mailchimp] 캠페인 ID가 특정 [!DNL Mailchimp] campaign을 통해 목록/대상자에게 이메일을 보낼 수 있습니다. |

**응답**

성공적인 응답은 고유 식별자(`id`) 내의 아무 곳에나 삽입할 수 있습니다. 이 ID는 이후 단계에서 데이터 흐름을 만드는 데 필요합니다.

```json
{
    "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
    "etag": "\"e205c206-0000-0200-0000-615b5c070000\""
}
```

## 대상 XDM 스키마 만들기 {#target-schema}

Platform에서 소스 데이터를 사용하려면 필요에 따라 소스 데이터를 구조화하기 위해 대상 스키마를 만들어야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

대상 XDM 스키마는에 대한 POST 요청을 수행하여 만들 수 있습니다 [스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

대상 XDM 스키마를 만드는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오 [api를 사용하여 스키마 만들기](../../../../../xdm/api/schemas.md).

### 대상 데이터 세트 만들기 {#target-dataset}

에 대한 POST 요청을 수행하여 대상 데이터 세트를 만들 수 있습니다 [카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)페이로드 내에 대상 스키마의 ID를 제공하는 것이 좋습니다.

대상 데이터 세트를 만드는 방법에 대한 자세한 단계는 다음 사항에 대한 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](../../../../../catalog/api/create-dataset.md).

## 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 ID가 [!DNL Data Lake]. 이 ID는 다음과 같습니다. `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마에서 대상 데이터 세트와 연결 사양 ID에 대한 고유 식별자가 있습니다 [!DNL Data Lake]. 이러한 식별자를 사용하여 [!DNL Flow Service] 인바운드 소스 데이터를 포함할 데이터 세트를 지정하는 API입니다.

**API 형식**

```https
POST /targetConnections
```

**요청**

다음 요청은에 대한 대상 연결을 만듭니다 [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Campaign target connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6155e3a9bd13651949515f14"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 대상 연결의 이름입니다. 대상 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 대상 연결의 이름이 설명적인지 확인합니다. |
| `description` | Target 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 에 해당하는 연결 사양 ID [!DNL Data Lake]. 이 고정 ID는 다음과 같습니다. `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 의 형식 [!DNL Mailchimp] Platform으로 가져올 데이터입니다. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트 ID입니다. |


**응답**

성공적인 응답은 새 대상 연결의 고유 식별자(`id`). 이 ID는 이후 단계에서 필요합니다.

```json
{
    "id": "9463fe9c-027d-4347-a423-894fcd105647",
    "etag": "\"b902e822-0000-0200-0000-615b5c370000\""
}
```

>[!IMPORTANT]
>
>데이터 준비 함수는 현재 지원되지 않습니다 [!DNL Mailchimp Campaign].

<!--
## Create a mapping {#mapping}

In order for the source data to be ingested into a target dataset, it must first be mapped to the target schema that the target dataset adheres to. This is achieved by performing a POST request to Conversion Service with data mappings defined within the request payload.

**API format**

```http
POST /conversion/mappingSets
```

**Request**

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
      "xdmSchema": "_{TENANT_ID}.schemas.570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
      "xdmVersion": "1.0",
      "mappings": [
      {
        "destinationXdmPath": "person.name.firstName",
        "sourceAttribute": "merge_fields.FNAME",
        "identity": false,
        "version": 0
      },
      {
        "destinationXdmPath": "person.name.lastName",
        "sourceAttribute": "merge_fields.LNAME",
        "identity": false,
        "version": 0
      }
    ]
  }'
```

| Property | Description |
| --- | --- |
| `xdmSchema` | The ID of the [target XDM schema](#target-schema) generated in an earlier step. |
| `mappings.destinationXdmPath` | The destination XDM path where the source attribute is being mapped to. |
| `mappings.sourceAttribute` | The source attribute that needs to be mapped to a destination XDM path. |
| `mappings.identity` | A boolean value that designates whether the mapping set will be marked for [!DNL Identity Service]. |

**Response**

A successful response returns details of the newly created mapping including its unique identifier (`id`). This value is required in a later step to create a dataflow.

```json
{
    "id": "5a365b23962d4653b9d9be25832ee5b4",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

--->

## 흐름 만들기 {#flow}

마지막 단계는 [!DNL Mailchimp] Platform에 데이터를 보내는 것은 데이터 흐름을 만드는 것입니다. 현재까지는 다음 필수 값이 준비되었습니다.

* [소스 연결 ID](#source-connection)
* [Target 연결 ID](#target-connection)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에서 이전에 언급된 값을 제공하는 동안 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

수집을 예약하려면 먼저 시작 시간 값을 초 단위로 설정해야 합니다. 그런 다음 빈도 값을 다섯 가지 옵션 중 하나로 설정해야 합니다. `once`, `minute`, `hour`, `day`, 또는 `week`. 간격 값은 두 개의 연속 섭취 사이의 기간을 지정하고 1회 수집(`once`)에는 간격을 설정할 필요가 없습니다. 다른 모든 주파수의 경우 간격 값을 같거나 그 이상으로 설정해야 합니다 `15`.


**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Campaign dataflow",
      "description": "MailChimp Campaign dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "d6557bf1-7347-415f-964c-9316bd4cbf56"
      ],
      "targetConnectionIds": [
          "9463fe9c-027d-4347-a423-894fcd105647"
      ],
      "scheduleParams": {
          "startTime": "1632809759",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 데이터 흐름의 이름입니다. 데이터 흐름에서 정보를 조회하는 데 사용할 수 있으므로 데이터 흐름의 이름이 설명적인지 확인합니다. |
| `description` | (선택 사항) 데이터 집합에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `flowSpec.id` | 데이터 흐름을 만드는 데 필요한 흐름 사양 ID입니다. 이 고정 ID는 다음과 같습니다. `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | 흐름 사양 ID의 해당 버전입니다. 이 값의 기본값은 입니다. `1.0`. |
| `sourceConnectionIds` | 다음 [소스 연결 ID](#source-connection) 이전 단계에서 생성된 . |
| `targetConnectionIds` | 다음 [target 연결 ID](#target-connection) 이전 단계에서 생성된 . |
| `scheduleParams.startTime` | 데이터의 첫 번째 수집이 시작되는 경우의 지정된 시작 시간입니다. |
| `scheduleParams.frequency` | 데이터 흐름에서 데이터를 수집하는 빈도입니다. 허용되는 값은 다음과 같습니다. `once`, `minute`, `hour`, `day`, 또는 `week`. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 빈도가 로 설정된 경우 간격이 필요하지 않습니다 `once` 및 보다 크거나 같아야 합니다. `15` 다른 주파수 값에 사용할 수 있습니다. |

**응답**

성공적인 응답은 ID(`id`)을 만들 수 있습니다. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
    "id": "be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da",
    "etag": "\"7e010621-0000-0200-0000-615b5c9b0000\""
}
```

## 데이터 흐름 모니터링

데이터 흐름을 만든 후에는 데이터 흐름을 통해 수집 중인 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다.

**API 형식**

```http
GET /runs?property=flowId=={FLOW_ID}
```

**요청**

다음 요청은 기존 데이터 흐름의 사양을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 생성 날짜, 소스 및 대상 연결에 대한 정보, 흐름 실행의 고유 식별자(`id`).

```json
{
    "items": [
        {
            "id": "209812ad-7bef-430c-b5b2-a648aae72094",
            "createdAt": 1633044829955,
            "updatedAt": 1633044838006,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "MailChimp Campaign dataflow",
            "description": "MailChimp Campaign dataflow",
            "flowSpec": {
                "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "etag": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "sourceConnectionIds": [
                "d6557bf1-7347-415f-964c-9316bd4cbf56"
            ],
            "targetConnectionIds": [
                "9463fe9c-027d-4347-a423-894fcd105647"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
                        "connectionSpec": {
                            "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "9601747c-6874-4c02-bb00-5732a8c43086",
                            "connectionSpec": {
                                "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "9463fe9c-027d-4347-a423-894fcd105647",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1633377385",
                "frequency": "minute",
                "interval": 15
            },
            "runs": "/flows/be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da/runs",
            "lastOperation": {
                "started": 1633377421476,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "84f95788-3e83-4ce0-8e45-c0a89117c6f1",
                "state": "failed",
                "startedAtUTC": 1633377445979,
                "completedAtUTC": 1633377487082
            }
        }
    ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `items` | 특정 흐름 실행과 연결된 메타데이터의 단일 페이로드를 포함합니다. |
| `id` | 데이터 흐름과 해당하는 ID를 표시합니다. |
| `state` | 데이터 흐름의 현재 상태를 표시합니다. |
| `inheritedAttributes` | 해당 기본, 소스 및 타겟 연결에 대한 ID와 같이 흐름을 정의하는 속성을 포함합니다. |
| `scheduleParams` | 데이터 흐름의 수집 일정(예: 시작 시간(epoch 시간), 빈도 및 간격)에 대한 정보를 포함합니다. |
| `transformations` | 데이터 집합에 적용되는 변형 속성에 대한 정보를 포함합니다. |
| `runs` | 흐름의 해당 실행 ID를 표시합니다. 이 ID를 사용하여 특정 흐름 실행을 모니터링할 수 있습니다. |

## 데이터 흐름 업데이트

데이터 흐름의 실행 일정, 이름 및 설명을 업데이트하려면 [!DNL Flow Service] 플로우 ID, 버전 및 사용할 새 일정을 제공하는 API입니다.

>[!IMPORTANT]
>
>다음 `If-Match` PATCH 요청을 만들 때는 헤더가 필요합니다. 이 헤더의 값은 업데이트할 연결의 고유한 버전입니다.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

다음 요청은 흐름 실행 일정과 데이터 흐름의 이름과 설명을 업데이트합니다.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "2e01f11d-0000-0200-0000-615649660000"' \
  -d '[
          {
              "op": "replace",
              "path": "/scheduleParams/frequency",
              "value": "day"
          },
          {
              "op": "replace",
              "path": "/name",
              "value": "MailChimp Campaign Dataflow 2.0"
          },
          {
              "op": "replace",
              "path": "/description",
              "value": "MailChimp Campaign Dataflow Updated"
          }
      ]'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 매개 변수의 경로입니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 플로우 ID와 업데이트된 태그를 반환합니다. 에 GET 요청을 수행하여 업데이트를 확인할 수 있습니다 [!DNL Flow Service] 흐름 ID를 제공하는 동안 API를 사용하여 규칙 세트를 단순화하는 것이 좋습니다.

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 데이터 흐름 삭제

기존 흐름 ID를 사용하는 경우, [!DNL Flow Service] API.

**API 형식**

```http
DELETE /flows/{FLOW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 고유 `id` 삭제할 데이터 흐름 값입니다. |

**요청**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다. 데이터 플로우에 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. API가 HTTP 404(찾을 수 없음) 오류를 반환하여 데이터 흐름이 삭제되었음을 나타냅니다.

## 연결 업데이트

연결의 이름, 설명 및 자격 증명을 업데이트하려면 [!DNL Flow Service] 기본 연결 ID, 버전 및 사용할 새 정보를 제공하는 동안 API입니다.

>[!IMPORTANT]
>
>다음 `If-Match` PATCH 요청을 만들 때는 헤더가 필요합니다. 이 헤더의 값은 업데이트할 연결의 고유한 버전입니다.

**API 형식**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 고유 `id` 업데이트할 연결의 값입니다. |

**요청**

다음 요청에서는 연결을 업데이트할 새 이름 및 설명과 새 자격 증명 세트를 제공합니다.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: 4000cff7-0000-0200-0000-6154bad60000' \
  -d '[
      {
          "op": "replace",
          "path": "/auth/params",
          "value": {
              "username": "mailchimp-member-activity-user",
              "password": "{NEW_PASSWORD}"
          }
      },
      {
          "op": "replace",
          "path": "/name",
          "value": "MailChimp Campaign Connection 2.0"
      },
      {
          "op": "add",
          "path": "/description",
          "value": "Updated MailChimp Campaign Connection"
      }
  ]'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `op` | 연결을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 매개 변수의 경로입니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 기본 연결 ID와 업데이트된 태그를 반환합니다. 에 GET 요청을 수행하여 업데이트를 확인할 수 있습니다 [!DNL Flow Service] API, 연결 ID를 제공하는 동안

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 연결 삭제

기존 기본 연결 ID가 있는 경우, 다음에 대한 DELETE 요청을 수행합니다 [!DNL Flow Service] API.

**API 형식**

```http
DELETE /connections/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 고유 `id` 삭제할 기본 연결 값입니다. |

**요청**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다.

연결에 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다.
