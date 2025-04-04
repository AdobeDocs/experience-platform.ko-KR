---
title: 흐름 서비스 API를 사용하여 Salesforce 서비스 Cloud Source 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Salesforce 서비스 클라우드에 연결하는 방법을 알아봅니다.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Salesforce Service Cloud] 소스 연결 만들기

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Salesforce Service Cloud]에 대한 기본 연결을 만드는 방법을 알아보려면 이 자습서를 읽어 보십시오.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Salesforce Service Cloud]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Salesforce Service Cloud] 원본은 기본 인증과 OAuth2 클라이언트 자격 증명을 지원합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

기본 인증을 사용하여 [!DNL Salesforce Service Cloud] 계정을 [!DNL Flow Service]에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce Service Cloud] 원본 인스턴스의 URL입니다. |
| `username` | [!DNL Salesforce Service Cloud] 사용자 계정의 사용자 이름입니다. |
| `password` | [!DNL Salesforce Service Cloud] 사용자 계정의 암호입니다. |
| `securityToken` | [!DNL Salesforce Service Cloud] 사용자 계정의 보안 토큰입니다. |
| `apiVersion` | (선택 사항) 사용 중인 [!DNL Salesforce Service Cloud] 인스턴스의 REST API 버전입니다. API 버전의 값은 십진수로 형식을 지정해야 합니다. 예를 들어 API 버전 `52`을(를) 사용하는 경우 값을 `52.0`(으)로 입력해야 합니다. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Salesforce Service Cloud]의 연결 사양 ID는 `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`입니다. |

시작하기에 대한 자세한 내용은 [이 Salesforce 문서](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)를 참조하세요.

>[!TAB OAuth 2 클라이언트 자격 증명]

OAuth 2 클라이언트 자격 증명을 사용하여 [!DNL Salesforce Service Cloud] 계정을 [!DNL Flow Service]에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce Service Cloud] 원본 인스턴스의 URL입니다. |
| `clientId` | 클라이언트 ID는 OAuth2 인증의 일부로 클라이언트 암호와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Salesforce Service Cloud]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| `clientSecret` | 클라이언트 암호는 OAuth2 인증의 일부로 클라이언트 ID와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Salesforce Service Cloud]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| `apiVersion` | 사용 중인 [!DNL Salesforce Service Cloud] 인스턴스의 REST API 버전입니다. API 버전의 값은 십진수로 형식을 지정해야 합니다. 예를 들어 API 버전 `52`을(를) 사용하는 경우 값을 `52.0`(으)로 입력해야 합니다. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. 이 값은 OAuth2 클라이언트 자격 증명 인증에 필수입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Salesforce Service Cloud]의 연결 사양 ID는 `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`입니다. |

[!DNL Salesforce Service Cloud]에 대한 OAuth 사용에 대한 자세한 내용은 OAuth 인증 흐름에 대한 [[!DNL Salesforce Service Cloud] 안내서](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5)를 참조하십시오.

>[!ENDTABS]

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Salesforce Service Cloud] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```http
POST /connections
```

**요청**

>[!BEGINTABS]

>[!TAB 기본 인증]

다음 요청은 기본 인증을 사용하여 [!DNL Salesforce Service Cloud]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (basic auth)",
      "description": "Salesforce Service Cloud account for ACME data (basic auth)",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce-service-cloud",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| 매개변수 | 설명 |
| ---| --- |
| `auth.params.environmentUrl` | [!DNL Salesforce Service Cloud] 인스턴스의 URL. |
| `auth.params.username` | [!DNL Salesforce Service Cloud] 계정과 연결된 사용자 이름. |
| `auth.params.password` | [!DNL Salesforce Service Cloud] 계정과 연결된 암호입니다. |
| `auth.params.securityToken` | [!DNL Salesforce Service Cloud] 계정과 연결된 보안 토큰입니다. |
| `connectionSpec.id` | [!DNL Salesforce Service Cloud] 연결 사양 ID: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB OAuth2 클라이언트 자격 증명]

다음 요청은 OAuth 2 클라이언트 자격 증명을 사용하여 [!DNL Salesforce Service Cloud]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
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
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.environmentUrl` | [!DNL Salesforce Service Cloud] 인스턴스의 URL. |
| `auth.params.clientId` | [!DNL Salesforce Service Cloud] 계정과 연결된 클라이언트 ID입니다. |
| `auth.params.clientSecret` | [!DNL Salesforce Service Cloud] 계정과 연결된 클라이언트 암호입니다. |
| `auth.params.apiVersion` | 사용 중인 [!DNL Salesforce Service Cloud] 인스턴스의 REST API 버전입니다. |
| `connectionSpec.id` | [!DNL Salesforce Service Cloud] 연결 사양 ID: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

>[!ENDTABS]

**응답**

성공적인 응답은 고유 ID와 함께 새로 생성된 기본 연결을 반환합니다.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Salesforce Service Cloud] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 고객 성공 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/customer-success.md)
