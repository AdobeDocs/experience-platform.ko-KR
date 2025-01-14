---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Mailchimp Campaign에 대한 데이터 흐름 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 MailChimp Campaign에 연결하는 방법을 알아봅니다.
exl-id: fd4821c7-6fe1-4cad-8e13-3549dbe0ce98
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 1%

---

# 흐름 서비스 API를 사용하여 [!DNL Mailchimp Campaign]에 대한 데이터 흐름 만들기

다음 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Mailchimp Campaign] 데이터를 플랫폼으로 가져오기 위한 소스 연결 및 데이터 흐름을 만드는 단계를 안내합니다.

## 전제 조건

OAuth 2 새로 고침 코드를 사용하여 [!DNL Mailchimp]을(를) Adobe Experience Platform에 연결하려면 먼저 [!DNL MailChimp.]에 대한 액세스 토큰을 검색해야 합니다. 액세스 토큰을 찾는 방법에 대한 자세한 지침은 [[!DNL Mailchimp] OAuth 2 안내서](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/)를 참조하십시오.

## 기본 연결 만들기 {#base-connection}

[!DNL Mailchimp] 인증 자격 증명을 검색했으면 이제 데이터 흐름을 만드는 프로세스를 시작하여 [!DNL Mailchimp Campaign] 데이터를 플랫폼으로 가져올 수 있습니다. 데이터 흐름을 만드는 첫 번째 단계는 기본 연결을 만드는 것입니다.

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

[!DNL Mailchimp]은(는) 기본 인증과 OAuth 2 새로 고침 코드를 모두 지원합니다. 두 인증 유형 중 하나로 인증하는 방법에 대한 지침은 다음 예를 참조하십시오.

### 기본 인증을 사용하여 [!DNL Mailchimp] 기본 연결 만들기

기본 인증을 사용하여 [!DNL Mailchimp] 기본 연결을 만들려면 `authorizationTestUrl`, `username` 및 `password`에 대한 자격 증명을 제공하는 동안 [!DNL Flow Service] API의 `/connections` 끝점에 POST 요청을 하십시오.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Mailchimp]에 대한 기본 연결을 만듭니다.

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
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. 이 ID는 [!DNL Flow Service] API를 통해 소스를 등록 및 승인한 후에 검색할 수 있습니다. |
| `auth.specName` | 소스를 플랫폼에 연결하는 데 사용하는 인증 유형입니다. |
| `auth.params.authorizationTestUrl` | (선택 사항) 인증 테스트 URL은 기본 연결을 만들 때 자격 증명의 유효성을 검사하는 데 사용됩니다. 제공되지 않으면 소스 연결 생성 단계에서 자격 증명이 자동으로 확인됩니다. |
| `auth.params.username` | [!DNL Mailchimp] 계정에 해당하는 사용자 이름. 기본 인증에 필요합니다. |
| `auth.params.password` | [!DNL Mailchimp] 계정에 해당하는 암호입니다. 기본 인증에 필요합니다. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 기본 연결을 반환합니다. 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

### OAuth 2 새로 고침 코드를 사용하여 [!DNL Mailchimp] 기본 연결 만들기

OAuth 2 새로 고침 코드를 사용하여 [!DNL Mailchimp] 기본 연결을 만들려면 `authorizationTestUrl` 및 `accessToken`에 대한 자격 증명을 제공하는 동안 `/connections` 끝점에 POST 요청을 하십시오.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Mailchimp]에 대한 기본 연결을 만듭니다.

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
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. 이 ID는 [!DNL Flow Service] API를 사용하여 소스를 등록한 후에 검색할 수 있습니다. |
| `auth.specName` | Platform에 소스를 인증하기 위해 사용하는 인증 유형입니다. |
| `auth.params.authorizationTestUrl` | (선택 사항) 인증 테스트 URL은 기본 연결을 만들 때 자격 증명의 유효성을 검사하는 데 사용됩니다. 제공되지 않으면 소스 연결 생성 단계에서 자격 증명이 자동으로 확인됩니다. |
| `auth.params.accessToken` | 소스 인증에 사용되는 해당 액세스 토큰입니다. OAuth 기반 인증에 필요합니다. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 기본 연결을 반환합니다. 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

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
| `{OBJECT_TYPE}` | 탐색하려는 오브젝트의 유형입니다. REST 원본의 경우 이 값은 기본적으로 `rest`(으)로 설정됩니다. |
| `{OBJECT}` | 탐색하려는 오브젝트입니다. |
| `{FILE_TYPE}` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 해당 값은 탐색하려는 디렉터리의 경로를 나타냅니다. |
| `{PREVIEW}` | 연결 콘텐츠가 미리 보기를 지원하는지 여부를 정의하는 부울 값. |
| `{SOURCE_PARAMS}` | `campaign_id`의 base64로 인코딩된 문자열입니다. |

>[!TIP]
>
>`{SOURCE_PARAMS}`에 대해 허용되는 형식 유형을 검색하려면 base64에서 전체 `campaignId` 문자열을 인코딩해야 합니다. 예를 들어 base64에서 인코딩된 `{"campaignId": "c66a200cda"}`은(는) `eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9`과(와) 같습니다.

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

[!DNL Flow Service] API에 대한 POST 요청을 수행하여 소스 연결을 만들 수 있습니다. 소스 연결은 연결 ID, 소스 데이터 파일에 대한 경로 및 연결 사양 ID로 구성됩니다.

소스 연결을 만들려면 데이터 형식 특성에 대한 열거형 값도 정의해야 합니다.

파일 기반 소스에 대해 다음 열거형 값을 사용하십시오.

| 데이터 형식 | 열거형 값 |
| ----------- | ---------- |
| 구분됨 | `delimited` |
| JSON | `json` |
| 쪽모이 세공 | `parquet` |

모든 테이블 기반 원본의 경우 값을 `tabular`(으)로 설정하십시오.

**API 형식**

```https
POST /sourceConnections
```

**요청**

다음 요청은 [!DNL Mailchimp]에 대한 소스 연결을 만듭니다.

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
| `baseConnectionId` | [!DNL Mailchimp]의 기본 연결 ID. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID. |
| `data.format` | 수집할 [!DNL Mailchimp] 데이터의 형식입니다. |
| `params.campaignId` | [!DNL Mailchimp] 캠페인 ID는 특정 [!DNL Mailchimp] 캠페인을 식별하므로 목록/대상자에게 이메일을 보낼 수 있습니다. |

**응답**

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
    "etag": "\"e205c206-0000-0200-0000-615b5c070000\""
}
```

## 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 플랫폼에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

[스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)에 대한 POST 요청을 수행하여 대상 XDM 스키마를 만들 수 있습니다.

대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 [API를 사용하여 스키마 만들기](../../../../../xdm/api/schemas.md)에 대한 자습서를 참조하십시오.

### 타겟 데이터 세트 만들기 {#target-dataset}

[카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/)에 대한 POST 요청을 수행하고 페이로드 내에 대상 스키마의 ID를 제공하여 대상 데이터 집합을 만들 수 있습니다.

대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../../../catalog/api/create-dataset.md)에 대한 자습서를 참조하십시오.

## 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 [!DNL Data Lake]에 해당하는 고정 연결 사양 ID를 제공해야 합니다. 이 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마에 대한 고유 식별자, 대상 데이터 세트 및 [!DNL Data Lake]에 대한 연결 사양 ID가 있습니다. 이러한 식별자를 사용하여 [!DNL Flow Service] API를 사용하여 대상 연결을 만들어 인바운드 원본 데이터를 포함할 데이터 집합을 지정할 수 있습니다.

**API 형식**

```https
POST /targetConnections
```

**요청**

다음 요청은 [!DNL Mailchimp]에 대한 대상 연결을 만듭니다.

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
| `connectionSpec.id` | [!DNL Data Lake]에 해당하는 연결 사양 ID입니다. 이 고정 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`입니다. |
| `data.format` | 플랫폼으로 가져올 [!DNL Mailchimp] 데이터의 형식입니다. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트 ID입니다. |


**응답**

응답이 성공하면 새 대상 연결의 고유 식별자(`id`)가 반환됩니다. 이 ID는 이후 단계에서 필수입니다.

```json
{
    "id": "9463fe9c-027d-4347-a423-894fcd105647",
    "etag": "\"b902e822-0000-0200-0000-615b5c370000\""
}
```

>[!IMPORTANT]
>
>데이터 준비 기능은 현재 [!DNL Mailchimp Campaign]에 대해 지원되지 않습니다.

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

[!DNL Mailchimp] 데이터를 플랫폼으로 가져오는 마지막 단계는 데이터 흐름을 만드는 것입니다. 이제 다음 필수 값이 준비되었습니다.

* [Source 연결 ID](#source-connection)
* [대상 연결 ID](#target-connection)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급된 값을 제공하면서 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

수집을 예약하려면 먼저 시작 시간 값을 에포크 시간(초)으로 설정해야 합니다. 그런 다음 빈도 값을 `once`, `minute`, `hour`, `day` 또는 `week` 옵션 중 하나로 설정해야 합니다. 간격 값은 두 개의 연속 수집 사이의 기간을 지정하며 1회 수집(`once`)을 만들 때 간격을 설정할 필요가 없습니다. 다른 모든 주파수의 경우 간격 값을 `15`보다 크거나 같게 설정해야 합니다.


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
| `flowSpec.id` | 데이터 흐름을 만드는 데 필요한 흐름 사양 ID입니다. 이 고정 ID는 `6499120c-0b15-42dc-936e-847ea3c24d72`입니다. |
| `flowSpec.version` | 흐름 사양 ID의 해당 버전. 이 값은 기본적으로 `1.0`입니다. |
| `sourceConnectionIds` | 이전 단계에서 생성된 [소스 연결 ID](#source-connection)입니다. |
| `targetConnectionIds` | 이전 단계에서 생성된 [대상 연결 ID](#target-connection)입니다. |
| `scheduleParams.startTime` | 데이터의 첫 번째 수집이 시작될 때 지정된 시작 시간입니다. |
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. 허용되는 값은 `once`, `minute`, `hour`, `day` 또는 `week`입니다. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 빈도가 `once`(으)로 설정된 경우 간격이 필요하지 않으며 다른 빈도 값의 경우 `15`보다 크거나 같아야 합니다. |

**응답**

성공한 응답은 새로 만든 데이터 흐름의 ID(`id`)를 반환합니다. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
    "id": "be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da",
    "etag": "\"7e010621-0000-0200-0000-615b5c9b0000\""
}
```

## 부록

다음 섹션에서는 데이터 흐름을 모니터링, 업데이트 및 삭제할 수 있는 단계에 대해 설명합니다.

### 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 전체 API 예제는 [API를 사용하여 소스 데이터 흐름 모니터링](../../monitor.md)에 대한 안내서를 참조하십시오.

### 데이터 흐름 업데이트

데이터 흐름의 ID를 제공하면서 [!DNL Flow Service] API의 `/flows` 끝점에 PATCH 요청을 하여 데이터 흐름의 이름, 설명, 실행 일정 및 관련 매핑 세트와 같은 데이터 흐름의 세부 정보를 업데이트합니다. PATCH 요청을 할 때 `If-Match` 헤더에 데이터 흐름의 고유한 `etag`을(를) 제공해야 합니다. 전체 API 예제는 [API를 사용하여 소스 데이터 흐름을 업데이트하는 방법](../../update-dataflows.md)에 대한 안내서를 참조하십시오.

### 계정 업데이트

기본 연결 ID를 쿼리 매개 변수로 제공하면서 [!DNL Flow Service] API에 대한 PATCH 요청을 수행하여 소스 계정의 이름, 설명 및 자격 증명을 업데이트합니다. PATCH 요청을 할 때는 `If-Match` 헤더에 원본 계정의 고유 `etag`을(를) 제공해야 합니다. 전체 API 예제는 [API를 사용하여 소스 계정을 업데이트하는 방법](../../update.md)에 대한 안내서를 참조하십시오.

### 데이터 흐름 삭제

쿼리 매개 변수의 일부로 삭제할 데이터 흐름의 ID를 제공하면서 [!DNL Flow Service] API에 대한 DELETE 요청을 수행하여 데이터 흐름을 삭제하십시오. 전체 API 예제는 [API를 사용하여 데이터 흐름 삭제](../../delete-dataflows.md)에 대한 안내서를 참조하십시오.

### 계정 삭제

삭제할 계정의 기본 연결 ID를 제공하는 동안 [!DNL Flow Service] API에 대한 DELETE 요청을 수행하여 계정을 삭제합니다. 전체 API 예제는 [API를 사용하여 소스 계정 삭제](../../delete.md)에 대한 안내서를 참조하십시오.