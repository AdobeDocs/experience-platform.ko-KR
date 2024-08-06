---
title: 흐름 서비스 API를 사용하여 Salesforce 기본 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Salesforce 계정에 연결하는 방법에 대해 알아봅니다.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 5951b0f549c2fd2723945f8f4089d12f73b92e6c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Salesforce] 기본 연결 만들기

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Salesforce]에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Platform]을(를) [!DNL Salesforce] 계정에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

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

시작하는 방법에 대한 자세한 내용은 [이 Salesforce 문서](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)를 참조하십시오.

>[!TAB OAuth 2 클라이언트 자격 증명]

OAuth 2 클라이언트 자격 증명을 사용하여 [!DNL Salesforce] 계정을 [!DNL Flow Service]에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce] 원본 인스턴스의 URL입니다. `environmentUrl`의 형식은 `https://[domain].my.salesforce.com`입니다. |
| `clientId` | 클라이언트 ID는 OAuth2 인증의 일부로 클라이언트 암호와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Salesforce]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| `clientSecret` | 클라이언트 암호는 OAuth2 인증의 일부로 클라이언트 ID와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Salesforce]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| `apiVersion` | 사용 중인 [!DNL Salesforce] 인스턴스의 REST API 버전입니다. API 버전의 값은 십진수로 형식을 지정해야 합니다. 예를 들어 API 버전 `52`을(를) 사용하는 경우 값을 `52.0`(으)로 입력해야 합니다. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. 이 값은 OAuth2 클라이언트 자격 증명 인증에 필수입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Salesforce]의 연결 사양 ID는 `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`입니다. |

[!DNL Salesforce]에 대한 OAuth 사용에 대한 자세한 내용은 OAuth 인증 흐름에 대한 [[!DNL Salesforce] 안내서](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5)를 참조하십시오.

>[!ENDTABS]

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 끝점에 POST 요청을 하고 요청 본문에 [!DNL Salesforce] 인증 자격 증명을 제공하십시오.

**API 형식**

```http
POST /connections
```

**요청**

>[!BEGINTABS]

>[!TAB 기본 인증]

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

>[!TAB OAuth 2 클라이언트 자격 증명]

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
            "apiVersion": "60.0"
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
| `connectionSpec.id` | [!DNL Salesforce] 연결 사양 ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!ENDTABS]

**응답**

성공적인 응답은 고유 ID와 함께 새로 생성된 기본 연결을 반환합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Salesforce] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 CRM 데이터를 플랫폼으로 가져오는 데이터 흐름을 만듭니다.](../../collect/crm.md)
