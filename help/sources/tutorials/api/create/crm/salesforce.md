---
title: 흐름 서비스 API를 사용하여 Salesforce을 Experience Platform에 연결
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Salesforce 계정에 연결하는 방법을 알아봅니다.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 56307d8457ba6d0046ad80a7c97405220aa6161c
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 2%

---

# [!DNL Salesforce] API를 사용하여 [!DNL Flow Service]을(를) Experience Platform에 연결

[!DNL Salesforce]API[[!DNL Flow Service] 를 사용하여 ](https://developer.adobe.com/experience-platform-apis/references/flow-service/) 소스 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## [!DNL Salesforce]에서 [!DNL Azure]을(를) Experience Platform에 연결 {#azure}

[!DNL Salesforce]에서 [!DNL Azure] 소스를 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하십시오.

### 필요한 자격 증명 수집

>[!WARNING]
>
>[!DNL Salesforce] 원본에 대한 기본 인증은 2026년 1월에 더 이상 사용되지 않습니다. 소스를 계속 사용하고 [!DNL Salesforce] 계정의 데이터를 Experience Platform으로 수집하려면 OAuth 2 클라이언트 자격 증명 인증으로 이동해야 합니다.

[!DNL Salesforce] 원본은 기본 인증과 OAuth2 클라이언트 자격 증명을 지원합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

기본 인증을 사용하여 [!DNL Salesforce] 계정을 [!DNL Flow Service]에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce] 원본 인스턴스의 URL입니다. `environmentUrl`의 형식은 `https://[domain].my.salesforce.com`입니다. |
| `username` | [!DNL Salesforce] 사용자 계정의 사용자 이름입니다. |
| `password` | [!DNL Salesforce] 사용자 계정의 암호입니다. |
| `securityToken` | [!DNL Salesforce] 사용자 계정의 보안 토큰입니다. |
| `apiVersion` | 선택 사항) 사용 중인 [!DNL Salesforce] 인스턴스의 REST API 버전입니다. API 버전의 값은 십진수로 형식을 지정해야 합니다. 예를 들어 API 버전 `52`을(를) 사용하는 경우 값을 `52.0`(으)로 입력해야 합니다. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Salesforce]의 연결 사양 ID는 `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`입니다. |

시작하기에 대한 자세한 내용은 [이 Salesforce 문서](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)를 참조하세요.

>[!TAB OAuth 2 클라이언트 자격 증명]

OAuth 2 클라이언트 자격 증명을 사용하여 [!DNL Salesforce] 계정을 [!DNL Flow Service]에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce] 원본 인스턴스의 URL입니다. `environmentUrl`의 형식은 `https://[domain].my.salesforce.com`입니다. |
| `clientId` | 클라이언트 ID는 OAuth2 인증의 일부로 클라이언트 암호와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Salesforce]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| `clientSecret` | 클라이언트 암호는 OAuth2 인증의 일부로 클라이언트 ID와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Salesforce]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| `apiVersion` | 사용 중인 [!DNL Salesforce] 인스턴스의 REST API 버전입니다. API 버전의 값은 십진수로 형식을 지정해야 합니다. 예를 들어 API 버전 `52`을(를) 사용하는 경우 값을 `52.0`(으)로 입력해야 합니다. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. 이 값은 OAuth2 클라이언트 자격 증명 인증에 필수입니다. |
| `includeDeletedObjects` | 일시 삭제된 레코드를 포함할지 여부를 결정하는 데 사용되는 부울 값입니다. true로 설정하면 일시 삭제된 레코드를 [!DNL Salesforce] 쿼리에 포함하고 계정에서 Experience Platform으로 수집할 수 있습니다. 구성을 지정하지 않으면 기본값은 `false`입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Salesforce]의 연결 사양 ID는 `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`입니다. |

[!DNL Salesforce]에 대한 OAuth 사용에 대한 자세한 내용은 OAuth 인증 흐름에 대한 [[!DNL Salesforce] 안내서](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)를 참조하십시오.

>[!ENDTABS]

### [!DNL Salesforce]의 Experience Platform에서 [!DNL Azure]에 대한 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결을 만들고 [!DNL Salesforce] 계정을 [!DNL Azure]의 Experience Platform에 연결하려면 `/connections` 끝점에 POST 요청을 만들고 요청 본문에 [!DNL Salesforce] 인증 자격 증명을 제공하십시오.

**API 형식**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 기본 인증]

+++요청

다음 요청은 기본 인증을 사용하여 [!DNL Salesforce]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.environmentUrl` | [!DNL Salesforce] 인스턴스의 URL. |
| `auth.params.username` | [!DNL Salesforce] 계정과 연결된 사용자 이름. |
| `auth.params.password` | [!DNL Salesforce] 계정과 연결된 암호입니다. |
| `auth.params.securityToken` | [!DNL Salesforce] 계정과 연결된 보안 토큰입니다. |
| `connectionSpec.id` | [!DNL Salesforce] 연결 사양 ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

+++

+++응답

성공적인 응답은 고유 ID와 함께 새로 생성된 기본 연결을 반환합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!TAB OAuth 2 클라이언트 자격 증명]

+++요청

다음 요청은 OAuth 2 클라이언트 자격 증명을 사용하여 [!DNL Salesforce]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using OAuth 2",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0",
            "includeDeletedObjects": true
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.environmentUrl` | [!DNL Salesforce] 인스턴스의 URL. |
| `auth.params.clientId` | [!DNL Salesforce] 계정과 연결된 클라이언트 ID입니다. |
| `auth.params.clientSecret` | [!DNL Salesforce] 계정과 연결된 클라이언트 암호입니다. |
| `auth.params.apiVersion` | 사용 중인 [!DNL Salesforce] 인스턴스의 REST API 버전입니다. |
| `auth.params.includeDeletedObjects` | 일시 삭제된 레코드를 포함할지 여부를 결정하는 데 사용되는 부울 값입니다. |
| `connectionSpec.id` | [!DNL Salesforce] 연결 사양 ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

+++


+++응답

성공적인 응답은 고유 ID와 함께 새로 생성된 기본 연결을 반환합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!ENDTABS]

## Amazon Web Services(AWS)의 Experience Platform에 [!DNL Salesforce] 연결 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../../../landing/multi-cloud.md)를 참조하세요.

[!DNL Salesforce] 소스를 AWS의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하십시오.

### 전제 조건

AWS의 Experience Platform에 연결할 수 있도록 [!DNL Salesforce] 계정을 설정하는 방법에 대한 자세한 내용은 [[!DNL Salesforce] 개요](../../../../connectors/crm/salesforce.md#aws)를 참조하십시오.

### AWS의 Experience Platform에서 [!DNL Salesforce]에 대한 기본 연결 만들기

기본 연결을 만들고 [!DNL Salesforce] 계정을 AWS의 Experience Platform에 연결하려면 `/connections` 끝점에 대한 POST 요청을 만들고 자격 증명에 적절한 값을 제공하십시오.

**API 형식**

```http
POST /connections
```

**요청**

+++요청을 보려면 선택

다음 요청은 AWS의 Experience Platform에서 [!DNL Salesforce] 소스에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account on AWS",
      "description": "ACME Salesforce account on AWS",
      "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params":
            "jwtToken": "{JWT_TOKEN},
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

[!DNL Salesforce] `jwtToken`을(를) 검색하는 방법에 대한 자세한 내용은 [AWS에서 Experience Platform에 연결하도록  [!DNL Salesforce] 소스를 설정하는 방법](../../../../connectors/crm/salesforce.md#aws)에 대한 안내서를 참조하십시오.

+++

**응답**

+++응답을 보려면 선택

성공적인 응답은 고유 ID와 함께 새로 생성된 기본 연결을 반환합니다.

```json
{
    "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

### 연결 상태 확인

연결 상태를 확인하려면 `/connections` 끝점에 대한 GET 요청을 만들고 만들기 단계에서 생성된 기본 연결 ID를 제공하십시오.

**API 형식**

```http
GET /connections
```

**요청**

+++요청을 보려면 선택

다음 요청은 기본 연결 ID `3e908d3f-c390-482b-9f44-43d3d4f2eb82`에 대한 정보를 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/3e908d3f-c390-482b-9f44-43d3d4f2eb82' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

>[!BEGINTABS]

>[!TAB 초기화 중]

+++응답 예를 보려면 선택

다음 응답은 `3e908d3f-c390-482b-9f44-43d3d4f2eb82` 상태에 있는 동안 기본 연결 ID `initializing`에 대한 정보를 표시합니다.

```json
{
  "items": [
    {
      "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
      "createdAt": 1736506325115,
      "updatedAt": 1736506325717,
      "createdBy": "acme@techacct.adobe.com",
      "updatedBy": "acme@techacct.adobe.com",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "JWT Token Auth Authentication E2E-1736506322",
      "description": "Base Connection for salesforce E2E",
      "connectionSpec": {
        "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
        "version": "1.0"
      },
      "state": "initializing",
      "auth": {
        "specName": "OAuth2 JWT Token Credential",
        "params": {
          "jwtToken": "{JWT_TOKEN}",
          "clientId": "{CLIENT_ID}",
          "clientSecret": "{CLIENT_SECRET}",
          "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      }
    }
  }
]
```

+++

>[!TAB 활성화됨]

+++응답 예를 보려면 선택

다음 응답은 `3e908d3f-c390-482b-9f44-43d3d4f2eb82` 상태에 있는 동안 기본 연결 ID `enabled`에 대한 정보를 표시합니다.

```json
{
  "items": [
      {
        "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
        "createdAt": 1736506325115,
        "updatedAt": 1736506413299,
        "createdBy": "acme@techacct.adobe.com",
        "updatedBy": "acme@AdobeID",
        "createdClient": "{CREATED_CLIENT}",
        "updatedClient": "acme",
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "imsOrgId": "{ORG_ID}",
        "name": "JWT Token Auth Authentication E2E-1736506322",
        "description": "Base Connection for salesforce E2E",
        "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
        },
        "state": "enabled",
        "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params": {
            "jwtToken": "{JWT_TOKEN}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}",
            "instanceUrl": "https://adb8-dev-ed.develop.my.salesforce.com",
            "orgId": "00DdL000001iPRxUAM"
          }
        },
        "version": "\"6d27f305-40be-41c3-97d4-a701827c34df\"",
        "etag": "\"6d27f305-40be-41c3-97d4-a701827c34df\""
    }
  ]
}
```

+++

>[!ENDTABS]

## 다음 단계

이 자습서에 따라 [!DNL Salesforce] API를 사용하여 [!DNL Flow Service] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 CRM 데이터를 Experience Platform으로 가져오는 데이터 흐름을 만듭니다.](../../collect/crm.md)
