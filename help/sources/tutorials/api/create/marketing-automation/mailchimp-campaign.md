---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Mailchimp Campaign에 대한 데이터 흐름 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 MailChimp Campaign에 연결하는 방법을 알아봅니다.
exl-id: fd4821c7-6fe1-4cad-8e13-3549dbe0ce98
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 1%

---

# 다음에 대한 데이터 흐름 만들기 [!DNL Mailchimp Campaign] 흐름 서비스 API 사용

다음 자습서에서는 가져올 소스 연결 및 데이터 흐름을 만드는 단계를 안내합니다 [!DNL Mailchimp Campaign] 를 사용하여 데이터를 플랫폼에 전송 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 사전 요구 사항

연결하기 전에 [!DNL Mailchimp] oauth 2 새로 고침 코드를 사용하는 Adobe Experience Platform에 대해 먼저 액세스 토큰을 검색해야 합니다. [!DNL MailChimp.] 다음을 참조하십시오. [[!DNL Mailchimp] OAuth 2 안내서](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) 액세스 토큰 찾기에 대한 자세한 지침은 을 참조하십시오.

## 기본 연결 만들기 {#base-connection}

을(를) 검색한 후 [!DNL Mailchimp] 인증 자격 증명으로, 이제 가져올 데이터 흐름을 만드는 프로세스를 시작할 수 있습니다. [!DNL Mailchimp Campaign] 데이터를 플랫폼에 추가합니다. 데이터 흐름을 만드는 첫 번째 단계는 기본 연결을 만드는 것입니다.

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

[!DNL Mailchimp] 는 기본 인증과 OAuth 2 새로 고침 코드를 모두 지원합니다. 두 인증 유형 중 하나로 인증하는 방법에 대한 지침은 다음 예를 참조하십시오.

### 만들기 [!DNL Mailchimp] 기본 인증을 사용한 기본 연결

을(를) 만들려면 [!DNL Mailchimp] 기본 인증을 사용하여 기본 연결, POST 요청 `/connections` 엔드포인트 [!DNL Flow Service] 에 대한 자격 증명을 제공하는 동안 API `authorizationTestUrl`, `username`, 및 `password`.

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
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인하십시오. |
| `description` | (선택 사항) 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. 이 ID는 소스를 등록하고 를 통해 승인한 후에 검색할 수 있습니다. [!DNL Flow Service] API. |
| `auth.specName` | 소스를 플랫폼에 연결하는 데 사용하는 인증 유형입니다. |
| `auth.params.authorizationTestUrl` | (선택 사항) 인증 테스트 URL은 기본 연결을 만들 때 자격 증명의 유효성을 검사하는 데 사용됩니다. 제공되지 않으면 소스 연결 생성 단계에서 자격 증명이 자동으로 확인됩니다. |
| `auth.params.username` | 에 해당하는 사용자 이름 [!DNL Mailchimp] 계정입니다. 기본 인증에 필요합니다. |
| `auth.params.password` | 에 해당하는 암호 [!DNL Mailchimp] 계정입니다. 기본 인증에 필요합니다. |

**응답**

성공한 응답은 고유 연결 식별자를 포함하여 새로 만든 기본 연결을 반환합니다(`id`). 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

### 만들기 [!DNL Mailchimp] OAuth 2 새로 고침 코드를 사용한 기본 연결

을(를) 만들려면 [!DNL Mailchimp] POST OAuth 2 새로 고침 코드를 사용한 기본 연결에서 `/connections` 에 대한 자격 증명을 제공하는 도중 엔드포인트 `authorizationTestUrl`, 및 `accessToken`.

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
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인하십시오. |
| `description` | (선택 사항) 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. 이 ID는 [!DNL Flow Service] API. |
| `auth.specName` | Platform에 소스를 인증하기 위해 사용하는 인증 유형입니다. |
| `auth.params.authorizationTestUrl` | (선택 사항) 인증 테스트 URL은 기본 연결을 만들 때 자격 증명의 유효성을 검사하는 데 사용됩니다. 제공되지 않으면 소스 연결 생성 단계에서 자격 증명이 자동으로 확인됩니다. |
| `auth.params.accessToken` | 소스 인증에 사용되는 해당 액세스 토큰입니다. OAuth 기반 인증에 필요합니다. |

**응답**

성공한 응답은 고유 연결 식별자를 포함하여 새로 만든 기본 연결을 반환합니다(`id`). 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 소스 탐색 {#explore}

이전 단계에서 생성한 기본 연결 ID를 사용하여 GET 요청을 수행하여 파일 및 디렉터리를 탐색할 수 있습니다. 소스의 파일 구조 및 컨텐츠를 탐색하기 위해 GET 요청을 수행할 때 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 이전 단계에서 생성된 기본 연결 ID입니다. |
| `{OBJECT_TYPE}` | 탐색하려는 오브젝트의 유형입니다. REST 소스의 경우 이 값의 기본값은 `rest`. |
| `{OBJECT}` | 탐색하려는 오브젝트입니다. |
| `{FILE_TYPE}` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 해당 값은 탐색하려는 디렉터리의 경로를 나타냅니다. |
| `{PREVIEW}` | 연결 콘텐츠가 미리 보기를 지원하는지 여부를 정의하는 부울 값. |
| `{SOURCE_PARAMS}` | 의 base64로 인코딩된 문자열 `campaign_id`. |

>[!TIP]
>
>에 대해 허용된 형식 유형을 검색하려면 `{SOURCE_PARAMS}`, 전체를 인코딩해야 합니다. `campaignId` base64의 문자열 예를 들어, `{"campaignId": "c66a200cda"}` base64로 인코딩되는 값은 다음과 같습니다. `eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9`.

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

성공한 응답은 쿼리된 파일의 구조를 반환합니다.

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

에 POST 요청을 하여 소스 연결을 만들 수 있습니다. [!DNL Flow Service] API. 소스 연결은 연결 ID, 소스 데이터 파일에 대한 경로 및 연결 사양 ID로 구성됩니다.

소스 연결을 만들려면 데이터 형식 특성에 대한 열거형 값도 정의해야 합니다.

파일 기반 소스에 대해 다음 열거형 값을 사용하십시오.

| 데이터 형식 | 열거형 값 |
| ----------- | ---------- |
| 구분됨 | `delimited` |
| JSON | `json` |
| 쪽모이 세공 | `parquet` |

모든 테이블 기반 소스의 경우 값을 로 설정합니다. `tabular`.

**API 형식**

```https
POST /sourceConnections
```

**요청**

다음 요청은에 대한 소스 연결을 만듭니다. [!DNL Mailchimp]:

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
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회할 때 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `baseConnectionId` | 의 기본 연결 ID [!DNL Mailchimp]. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID. |
| `data.format` | 형식 [!DNL Mailchimp] 수집할 데이터. |
| `params.campaignId` | 다음 [!DNL Mailchimp] 캠페인 ID는 특정 [!DNL Mailchimp] campaign을 사용하면 목록/대상자에게 이메일을 보낼 수 있습니다. |

**응답**

성공적인 응답은 고유 식별자()를 반환합니다.`id`)을 참조하십시오. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
    "etag": "\"e205c206-0000-0200-0000-615b5c070000\""
}
```

## 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 플랫폼에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

에 대한 POST 요청을 수행하여 대상 XDM 스키마를 생성할 수 있습니다. [스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 다음 자습서를 참조하십시오. [api를 사용하여 스키마 만들기](../../../../../xdm/api/schemas.md).

### 타겟 데이터 세트 만들기 {#target-dataset}

에 대한 POST 요청을 수행하여 타겟 데이터 세트를 생성할 수 있습니다. [카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)페이로드 내에 대상 스키마의 ID를 제공합니다.

Target 데이터 세트를 만드는 방법에 대한 자세한 단계는 의 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](../../../../../catalog/api/create-dataset.md).

## 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 다음에 해당하는 고정 연결 사양 ID를 제공해야 합니다. [!DNL Data Lake]. 이 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마에 대한 고유 식별자, 대상 데이터 세트 및 연결 사양 ID가 있습니다. [!DNL Data Lake]. 이러한 식별자를 사용하여 다음을 사용하여 대상 연결을 만들 수 있습니다. [!DNL Flow Service] 인바운드 소스 데이터를 포함할 데이터 세트를 지정하는 API입니다.

**API 형식**

```https
POST /targetConnections
```

**요청**

다음 요청은에 대한 대상 연결을 만듭니다. [!DNL Mailchimp]:

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
| `name` | 대상 연결의 이름입니다. 대상 연결에 대한 정보를 찾을 때 사용할 수 있으므로 대상 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 대상 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 에 해당하는 연결 사양 ID [!DNL Data Lake]. 이 고정 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 형식 [!DNL Mailchimp] 플랫폼에 가져올 데이터입니다. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트 ID입니다. |


**응답**

성공적인 응답은 새 타겟 연결의 고유 식별자( )를 반환합니다.`id`). 이 ID는 이후 단계에서 필수입니다.

```json
{
    "id": "9463fe9c-027d-4347-a423-894fcd105647",
    "etag": "\"b902e822-0000-0200-0000-615b5c370000\""
}
```

>[!IMPORTANT]
>
>데이터 준비 기능은 현재 다음에 대해 지원되지 않습니다. [!DNL Mailchimp Campaign].

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

## 플로우 만들기 {#flow}

가져오기 위한 마지막 단계 [!DNL Mailchimp] 플랫폼으로 데이터를 보내는 것은 데이터 흐름을 만드는 것입니다. 이제 다음 필수 값이 준비되었습니다.

* [소스 연결 ID](#source-connection)
* [Target 연결 ID](#target-connection)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급된 값을 제공하면서 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

수집을 예약하려면 먼저 시작 시간 값을 에포크 시간(초)으로 설정해야 합니다. 그런 다음 빈도 값을 다음 다섯 가지 옵션 중 하나로 설정해야 합니다. `once`, `minute`, `hour`, `day`, 또는 `week`. 간격 값은 두 개의 연속 수집과 일회성 수집 생성 사이의 기간을 지정합니다(`once`) 간격을 설정할 필요가 없습니다. 다른 모든 주파수의 경우 간격 값이 보다 크거나 같게 설정되어야 합니다. `15`.


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
| `name` | 데이터 흐름의 이름입니다. 이 옵션을 사용하여 데이터 흐름에서 정보를 조회할 수 있으므로 데이터 흐름의 이름이 설명적인지 확인하십시오. |
| `description` | (선택 사항) 데이터 흐름에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `flowSpec.id` | 데이터 흐름을 만드는 데 필요한 흐름 사양 ID입니다. 이 고정 ID: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | 흐름 사양 ID의 해당 버전. 이 값의 기본값은 입니다. `1.0`. |
| `sourceConnectionIds` | 다음 [소스 연결 ID](#source-connection) 이전 단계에서 생성됩니다. |
| `targetConnectionIds` | 다음 [대상 연결 ID](#target-connection) 이전 단계에서 생성됩니다. |
| `scheduleParams.startTime` | 데이터의 첫 번째 수집이 시작되는 지정 시작 시간입니다. |
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. 허용되는 값은 다음과 같습니다. `once`, `minute`, `hour`, `day`, 또는 `week`. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 빈도를 로 설정하면 간격이 필요하지 않습니다. `once` 다음보다 크거나 같아야 합니다. `15` 다른 빈도 값의 경우. |

**응답**

성공적인 응답은 ID( )를 반환합니다.`id`)을 참조하십시오. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
    "id": "be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da",
    "etag": "\"7e010621-0000-0200-0000-615b5c9b0000\""
}
```

## 부록

다음 섹션에서는 데이터 흐름을 모니터링, 업데이트 및 삭제할 수 있는 단계에 대해 설명합니다.

### 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 데이터 흐름 모니터링](../../monitor.md).

### 데이터 흐름 업데이트

에 PATCH 요청을 하여 데이터 흐름의 이름, 설명, 실행 일정 및 관련 매핑 세트 등 세부 정보를 업데이트합니다. `/flows` 엔드포인트 [!DNL Flow Service] API, 데이터 흐름의 ID 제공. PATCH 요청을 할 때는 데이터 흐름의 고유한 값을 제공해야 합니다 `etag` 다음에서 `If-Match` 머리글입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 데이터 흐름 업데이트](../../update-dataflows.md).

### 계정 업데이트

에 대한 PATCH 요청을 수행하여 소스 계정의 이름, 설명 및 자격 증명을 업데이트합니다. [!DNL Flow Service] 기본 연결 ID를 쿼리 매개 변수로 제공하는 동안 API입니다. PATCH 요청을 할 때는 소스 계정의 고유한 이름을 제공해야 합니다 `etag` 다음에서 `If-Match` 머리글입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 계정 업데이트](../../update.md).

### 데이터 흐름 삭제

에 대한 DELETE 요청을 수행하여 데이터 흐름을 삭제합니다. [!DNL Flow Service] 쿼리 매개변수의 일부로 삭제할 데이터 흐름의 ID를 제공하는 동안 API입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 데이터 흐름 삭제](../../delete-dataflows.md).

### 계정 삭제

에 대한 DELETE 요청을 수행하여 계정을 삭제합니다. [!DNL Flow Service] 삭제할 계정의 기본 연결 ID를 제공하는 동안 API입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 계정 삭제](../../delete.md).