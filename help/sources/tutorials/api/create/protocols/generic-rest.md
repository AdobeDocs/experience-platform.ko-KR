---
keywords: Experience Platform;홈;인기 항목;일반 REST;일반 REST
solution: Experience Platform
title: Flow Service API를 사용하여 일반 REST API 기본 연결 만들기
type: Tutorial
description: Flow Service API를 사용하여 일반 REST API를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# 를 사용하여 일반 REST API 기본 연결 만들기 [!DNL Flow Service] API

>[!NOTE]
>
>다음 [!DNL Generic REST API] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 커넥터 사용에 대한 자세한 정보.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음에 대한 기본 연결을 만드는 단계를 안내합니다 [!DNL Generic REST API] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 연결 [!DNL Generic REST API]를 선택한 인증 유형에 유효한 자격 증명을 제공해야 합니다. [!DNL Generic REST API] 은 OAuth 2 새로 고침 코드 및 기본 인증을 모두 지원합니다. 지원되는 두 가지 인증 유형에 대한 자격 증명에 대한 자세한 내용은 다음 표를 참조하십시오.

#### OAuth 2 새로 고침 코드

| 자격 증명 | 설명 |
| --- | --- |
| `host` | 요청을 하는 소스의 호스트 URL입니다. 이 값은 필수이며 를 사용하여 우회할 수 없습니다 `requestParameterOverride`. |
| `authorizationTestUrl` | (선택 사항) 기본 연결을 만들 때 인증 테스트 URL을 사용하여 자격 증명을 확인합니다. 지정하지 않으면 소스 연결 생성 단계 동안 자격 증명이 자동으로 선택됩니다. |
| `clientId` | (선택 사항) 사용자 계정과 연결된 클라이언트 ID입니다. |
| `clientSecret` | (선택 사항) 사용자 계정과 연결된 클라이언트 암호입니다. |
| `accessToken` | 응용 프로그램에 액세스하는 데 사용되는 기본 인증 자격 증명입니다. 액세스 토큰은 사용자 데이터의 특정 측면에 액세스할 수 있도록 애플리케이션의 인증을 나타냅니다. 이 값은 필수이며 를 사용하여 우회할 수 없습니다 `requestParameterOverride`. |
| `refreshToken` | (선택 사항) 액세스 토큰이 만료되었을 때 새 액세스 토큰을 생성하는 데 사용되는 토큰입니다. |
| `expirationDate` | (선택 사항) 액세스 토큰의 만료 날짜를 정의하는 숨겨진 값입니다. |
| `accessTokenUrl` | (선택 사항) 액세스 토큰을 가져오는 데 사용되는 URL 끝점입니다. |
| `requestParameterOverride` | (선택 사항) 재정의할 자격 증명 매개 변수를 지정할 수 있는 속성입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 에 대한 연결 사양 ID [!DNL Generic REST API] is: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### 기본 인증

| 자격 증명 | 설명 |
| --- | --- |
| `host` | 요청을 하는 소스의 호스트 URL입니다. |
| `username` | 사용자 계정에 해당하는 사용자 이름입니다. |
| `password` | 사용자 계정에 해당하는 암호입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 에 대한 연결 사양 ID [!DNL Generic REST API] is: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

[!DNL Generic REST API] 에서는 기본 인증 및 OAuth 2 새로 고침 코드를 모두 지원합니다. 두 인증 유형을 인증하는 방법에 대한 지침은 다음 예를 참조하십시오.

### 만들기 [!DNL Generic REST API] OAuth 2 새로 고침 코드를 사용한 기본 연결

OAuth 2 새로 고침 코드를 사용하여 기본 연결 ID를 만들려면 `/connections` OAuth 2 자격 증명을 제공하는 중 끝점입니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Generic REST API]:

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
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인합니다. |
| `description` | (선택 사항) 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `connectionSpec.id` | 연결된 연결 사양 ID [!DNL Generic REST API]. 이 고정 ID는 다음과 같습니다. `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Platform에 소스를 인증하는 데 사용하는 인증 유형입니다. |
| `auth.params.host` | 에 연결하는 데 사용되는 루트 URL입니다 [!DNL Generic REST API] 소스. |
| `auth.params.accessToken` | 소스를 인증하는 데 사용되는 해당 액세스 토큰. OAuth 기반 인증에 필요합니다. |

**응답**

성공적인 응답은 해당 고유 연결 식별자(`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### 만들기 [!DNL Generic REST API] 기본 인증을 사용한 기본 연결

을(를) 만들려면 [!DNL Generic REST API] 기본 인증을 사용하여 기본 연결에서 `/connections` 끝점 [!DNL Flow Service] 기본 인증 자격 증명을 제공하는 동안 API입니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Generic REST API]:

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
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인합니다. |
| `description` | (선택 사항) 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `connectionSpec.id` | 연결된 연결 사양 ID [!DNL Generic REST API]. 이 고정 ID는 다음과 같습니다. `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | 소스를 Platform에 연결하는 데 사용하는 인증 유형입니다. |
| `auth.params.host` | 에 연결하는 데 사용되는 루트 URL입니다 [!DNL Generic REST API] 소스. |
| `auth.params.username` | 사용자 이름과 일치하는 사용자 이름 [!DNL Generic REST API] 소스. 기본 인증에 필요합니다. |
| `auth.params.password` | 사용자의 [!DNL Generic REST API] 소스. 기본 인증에 필요합니다. |

**응답**

성공적인 응답은 해당 고유 연결 식별자(`id`). 이 ID는 다음 단계에서 소스의 파일 구조와 컨텐츠를 탐색하는 데 필요합니다.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL Generic REST API] 기본 연결 [!DNL Flow Service] API. 다음 자습서에서는 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 컨텐츠를 탐색합니다. [!DNL Flow Service] API](../../explore/tabular.md)
* [데이터 흐름을 만들어 [!DNL Flow Service] API](../../collect/protocols.md)
