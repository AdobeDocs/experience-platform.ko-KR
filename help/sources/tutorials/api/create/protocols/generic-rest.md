---
keywords: Experience Platform;홈;인기 항목;일반 REST;일반 REST
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 일반 REST API 기본 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 일반 REST API를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 3%

---

# [!DNL Flow Service] API를 사용하여 일반 REST API 기본 연결 만들기

>[!NOTE]
>
>[!DNL Generic REST API] 원본이 Beta 버전입니다. 베타 레이블 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Generic REST API]에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Generic REST API]과(와) 연결하려면 선택한 인증 유형에 대해 올바른 자격 증명을 제공해야 합니다. [!DNL Generic REST API]은(는) OAuth 2 새로 고침 코드와 기본 인증을 모두 지원합니다. 지원되는 두 가지 인증 유형에 대한 자격 증명에 대한 자세한 내용은 다음 표를 참조하십시오.

#### OAuth 2 새로 고침 코드

| 자격 증명 | 설명 |
| --- | --- |
| `host` | 요청을 하는 소스의 호스트 URL입니다. 이 값은 필수이며 `requestParameterOverride`을(를) 사용하여 우회할 수 없습니다. |
| `authorizationTestUrl` | (선택 사항) 인증 테스트 URL은 기본 연결을 만들 때 자격 증명의 유효성을 검사하는 데 사용됩니다. 제공되지 않으면 소스 연결 생성 단계에서 자격 증명이 자동으로 확인됩니다. |
| `clientId` | (선택 사항) 사용자 계정과 연결된 클라이언트 ID. |
| `clientSecret` | (선택 사항) 사용자 계정과 연결된 클라이언트 암호입니다. |
| `accessToken` | 애플리케이션에 액세스하는 데 사용되는 기본 인증 자격 증명입니다. 액세스 토큰은 사용자 데이터의 특정 측면에 액세스하기 위한 애플리케이션의 인증을 나타냅니다. 이 값은 필수이며 `requestParameterOverride`을(를) 사용하여 우회할 수 없습니다. |
| `refreshToken` | (선택 사항) 액세스 토큰이 만료된 경우 새 액세스 토큰을 생성하는 데 사용되는 토큰입니다. |
| `expirationDate` | (선택 사항) 액세스 토큰의 만료 날짜를 정의하는 숨겨진 값입니다. |
| `accessTokenUrl` | (선택 사항) 액세스 토큰을 가져오는 데 사용되는 URL 엔드포인트입니다. |
| `requestParameterOverride` | (선택 사항) 재정의할 자격 증명 매개 변수를 지정할 수 있는 속성입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Generic REST API]의 연결 사양 ID는 `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`입니다. |

#### 기본 인증

| 자격 증명 | 설명 |
| --- | --- |
| `host` | 요청을 하는 소스의 호스트 URL입니다. |
| `username` | 사용자 계정에 해당하는 사용자 이름입니다. |
| `password` | 사용자 계정에 해당하는 암호입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Generic REST API]의 연결 사양 ID는 `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`입니다. |

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

[!DNL Generic REST API]은(는) 기본 인증과 OAuth 2 새로 고침 코드를 모두 지원합니다. 두 인증 유형 중 하나로 인증하는 방법에 대한 지침은 다음 예를 참조하십시오.

### OAuth 2 새로 고침 코드를 사용하여 [!DNL Generic REST API] 기본 연결 만들기

OAuth 2 새로 고침 코드를 사용하여 기본 연결 ID를 만들려면 OAuth 2 자격 증명을 제공하는 동안 `/connections` 끝점에 POST 요청을 합니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 [!DNL Generic REST API]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인하십시오. |
| `description` | (선택 사항) 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `connectionSpec.id` | [!DNL Generic REST API]에 연결된 연결 사양 ID입니다. 이 고정 ID는 `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`입니다. |
| `auth.specName` | Experience Platform에 소스를 인증하기 위해 사용하는 인증 유형입니다. |
| `auth.params.host` | [!DNL Generic REST API] 소스에 연결하는 데 사용되는 루트 URL입니다. |
| `auth.params.accessToken` | 소스 인증에 사용되는 해당 액세스 토큰입니다. OAuth 기반 인증에 필요합니다. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 연결을 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### 기본 인증을 사용하여 [!DNL Generic REST API] 기본 연결 만들기

기본 인증을 사용하여 [!DNL Generic REST API] 기본 연결을 만들려면 기본 인증 자격 증명을 제공하는 동안 [!DNL Flow Service] API의 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Generic REST API]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
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
| `connectionSpec.id` | [!DNL Generic REST API]에 연결된 연결 사양 ID입니다. 이 고정 ID는 `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`입니다. |
| `auth.specName` | 소스를 Experience Platform에 연결하는 데 사용하는 인증 유형입니다. |
| `auth.params.host` | [!DNL Generic REST API] 소스에 연결하는 데 사용되는 루트 URL입니다. |
| `auth.params.username` | [!DNL Generic REST API] 소스에 해당하는 사용자 이름입니다. 기본 인증에 필요합니다. |
| `auth.params.password` | [!DNL Generic REST API] 소스에 해당하는 암호입니다. 기본 인증에 필요합니다. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 기본 연결을 반환합니다. 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Generic REST API] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 프로토콜 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/protocols.md)
