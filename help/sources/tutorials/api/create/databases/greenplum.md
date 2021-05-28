---
keywords: Experience Platform;홈;인기 항목;그린플럼;그린플럼
solution: Experience Platform
title: Flow Service API를 사용하여 GreenPlum 소스 연결 생성
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 GreenPlum을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: c4ce452a-b4c5-46ab-83ab-61b296c271d0
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 [!DNL GreenPlum] 소스 연결을 만듭니다

[!DNL Flow Service] Adobe Experience Platform 내의 다양한 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스를 연결할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 [!DNL GreenPlum]을 [!DNL Experience Platform]에 연결하는 단계를 안내합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL GreenPlum]에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | [!DNL GreenPlum] 인스턴스에 연결하는 데 사용되는 연결 문자열입니다. [!DNL GreenPlum]에 대한 연결 문자열 패턴은 `HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}`입니다. |
| `connectionSpec.id` | 연결을 만드는 데 필요한 식별자입니다. [!DNL GreenPlum]에 대한 고정 연결 사양 ID는 `37b6bf40-d318-4655-90be-5cd6f65d334b`입니다. |

연결 문자열 가져오기에 대한 자세한 내용은 [이 GreenPlum 문서](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn)를 참조하십시오.

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서에서 [예제 API 호출](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법 섹션을 참조하십시오.

### 필수 헤더에 대한 값을 수집합니다

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에 필요한 각 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 연결 만들기

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 소스 커넥터를 만드는 데 사용할 수 있으므로 [!DNL GreenPlum] 계정에는 하나의 커넥터만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

[!DNL GreenPlum] 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. [!DNL GreenPlum]에 대한 연결 사양 ID는 `37b6bf40-d318-4655-90be-5cd6f65d334b`입니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "GreenPlum test connection",
        "description": "A test connection for a GreenPlum source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "connectionString": "HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "37b6bf40-d318-4655-90be-5cd6f65d334b",
            "version": "1.0"
        }
    }'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `auth.params.connectionString` | [!DNL GreenPlum] 계정에 연결하는 데 사용되는 연결 문자열입니다. 연결 문자열 패턴은 다음과 같습니다.`HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | [!DNL GreenPlum] 연결 사양 ID:`37b6bf40-d318-4655-90be-5cd6f65d334b`. |

**응답**

성공적인 응답은 해당 고유 식별자(`id`)를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 [!DNL GreenPlum] 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서는 [Flow Service API](../../explore/database-nosql.md)를 사용하여 데이터베이스를 탐색하는 방법을 배울 때 이 ID를 사용할 수 있습니다.
