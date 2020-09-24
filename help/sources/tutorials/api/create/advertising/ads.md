---
keywords: Experience Platform;home;popular topics;google adwords;Google AdWords;adwords
solution: Experience Platform
title: Flow Service API를 사용하여 Google AdWords 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 Experience Platform을 Google AdWords에 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 1%

---


# API를 [!DNL Google AdWords] 사용하여 커넥터 [!DNL Flow Service] 만들기

>[!NOTE]
>
>커넥터의 [!DNL Google AdWords] 베타입니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../../../home.md#terms-and-conditions) 참조하십시오.

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집된 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 연결 단계 [!DNL Experience Platform] 를 안내합니다 [!DNL Google AdWords].

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 광고에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

AdWords [!DNL Flow Service] 와 연결하려면 다음 연결 속성에 값을 제공해야 합니다.

| **자격 증명** | **설명** |
| -------------- | --------------- |
| 클라이언트 고객 ID | AdWords 계정의 클라이언트 고객 ID. |
| 개발자 토큰 | 관리자 계정과 연결된 개발자 토큰입니다. |
| 토큰 새로 고침 | AdWords에 대한 액세스 권한 [!DNL Google] 을 인증하기 위해 얻은 새로 고침 토큰입니다. |
| 클라이언트 ID | 새로 고침 토큰을 획득하는 데 사용되는 [!DNL Google] 응용 프로그램의 클라이언트 ID입니다. |
| 클라이언트 암호 | 새로 고침 토큰을 획득하는 데 [!DNL Google] 사용되는 응용 프로그램의 클라이언트 암호입니다. |
| 연결 사양 ID | 연결을 만드는 데 필요한 고유 식별자입니다. 에 대한 연결 사양 ID [!DNL Google AdWords] 는 다음과 같습니다. `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

이러한 값에 대한 자세한 내용은 이 [Google AdWords 문서를 참조하십시오](https://developers.google.com/adwords/api/docs/guides/authentication).

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증:무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Flow Service]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 연결 만들기

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 소스 커넥터를 만드는 데 사용할 수 있으므로 계정당 하나의 연결만 필요합니다. [!DNL Google AdWords]

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 페이로드에서 제공하는 속성으로 구성된 새 AdWords 연결을 만듭니다.


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `auth.params.clientCustomerID` | 계정의 클라이언트 고객 ID입니다 [!DNL AdWords] . |
| `auth.params.developerToken` | 계정의 개발자 [!DNL AdWords] 토큰입니다. |
| `auth.params.refreshToken` | 계정의 새로 고침 [!DNL AdWords] 토큰입니다. |
| `auth.params.clientID` | 계정의 클라이언트 [!DNL AdWords] ID. |
| `auth.params.clientSecret` | 귀하의 [!DNL AdWords] 계정의 클라이언트 비밀입니다. |
| `connectionSpec.id` | 연결 [!DNL Google AdWords] 사양 ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 다음 단계

이 튜토리얼을 따라 API를 사용하여 [!DNL Google AdWords] 연결을 만들고 연결 [!DNL Flow Service] 의 고유 ID 값을 얻게 되었습니다. 다음 자습서에서는 Flow Service API를 사용하여 광고 시스템을 [탐색하는 방법을 학습하면서 이 ID를 사용할 수 있습니다](../../explore/advertising.md).
