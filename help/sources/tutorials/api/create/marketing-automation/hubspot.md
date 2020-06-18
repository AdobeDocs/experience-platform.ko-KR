---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Flow Service API를 사용하여 HubSpot 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---


# Flow Service API를 사용하여 HubSpot 커넥터 만들기

>[!NOTE]
>HubSpot 커넥터가 베타에 있습니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../../../home.md#terms-and-conditions) 참조하십시오.

Flow Service는 Adobe Experience Platform 내의 다양한 소스에서 수집한 고객 데이터를 중앙에서 수집하고 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 Flow Service API를 사용하여 Experience Platform을 HubSpot에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드는 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 Platform 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 Flow Service API를 사용하여 HubSpot에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

Flow Service가 HubSpot에 연결하려면 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 클라이언트 ID | HubSpot 응용 프로그램과 연결된 클라이언트 ID. |
| 클라이언트 암호 | HubSpot 응용 프로그램과 연결된 클라이언트 암호입니다. |
| 액세스 토큰 | OAuth 통합을 처음 인증할 때 얻은 액세스 토큰입니다. |
| 토큰 새로 고침 | OAuth 통합을 처음 인증할 때 얻은 새로 고침 토큰입니다. |
| 연결 사양 ID | 연결을 만드는 데 필요한 고유 식별자입니다. HubSpot의 연결 사양 ID는 다음과 같습니다. `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

시작하는 방법에 대한 자세한 내용은 이 [HubSpot 문서를 참조하십시오](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 예제 API 호출 [](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 읽기 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

Platform API를 호출하려면 먼저 [인증 자습서를 완료해야 합니다](../../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증: 무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

흐름 서비스에 속하는 리소스를 포함하여 Experience Platform의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. Platform API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 연결 만들기

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 여러 소스 커넥터를 만들어 다른 데이터를 가져올 수 있으므로 HubSpot 계정당 하나의 연결만 필요합니다.

**API 형식**

```https
POST /connections
```

**요청**

HubSpot 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. HubSpot의 연결 사양 ID입니다 `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.clientId` | HubSpot 응용 프로그램과 연결된 클라이언트 ID. |
| `auth.params.clientSecret` | HubSpot 응용 프로그램과 연결된 클라이언트 암호입니다. |
| `auth.params.accessToken` | OAuth 통합을 처음 인증할 때 얻은 액세스 토큰입니다. |
| `auth.params.refreshToken` | OAuth 통합을 처음 인증할 때 얻은 새로 고침 토큰입니다. |

**응답**

성공적인 응답은 API의 고유 식별자(`id`)를 포함하여 새로 만든 API에 대한 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

이 자습서를 따라 Flow Service API를 사용하여 HubSpot 연결을 만들고 연결의 고유 ID 값을 받았습니다. Flow Service API를 사용하여 마케팅 자동화 시스템을 [탐색하는 방법을 배울 때 다음 자습서에서 이 연결 ID를 사용할 수 있습니다](../../explore/marketing-automation.md).