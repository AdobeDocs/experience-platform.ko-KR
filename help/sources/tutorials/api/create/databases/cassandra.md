---
keywords: Experience Platform;홈;인기 항목;Apache Cassandra;Cassandra;Cassandra
solution: Experience Platform
title: Flow Service API를 사용하여 Apache Cassandra 소스 연결 만들기
type: Tutorial
description: Flow Service API를 사용하여 Apache Cassandra를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---


# 만들기 [!DNL Apache Cassandra] 소스 연결 [!DNL Flow Service] API

[!DNL Flow Service] Adobe Experience Platform 내의 다양한 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스를 연결할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] 연결하는 단계를 안내하는 API [!DNL Apache Cassandra] (이하 &quot;카산드라&quot;라 한다)는 [!DNL Experience Platform].

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 를 사용하여 Cassandra에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다. [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 연결 [!DNL Cassandra]를 채울 때는 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 의 IP 주소 또는 호스트 이름 [!DNL Cassandra] server. |
| `port` | TCP 포트 [!DNL Cassandra] 서버는 을 사용하여 클라이언트 연결을 수신합니다. 기본 포트는 다음과 같습니다 `9042`. |
| `username` | 에 연결하는 데 사용되는 사용자 이름 [!DNL Cassandra] 인증을 위한 서버입니다. |
| `password` | 에 연결할 암호입니다 [!DNL Cassandra] 인증을 위한 서버입니다. |
| `connectionSpec.id` | 연결을 만드는 데 필요한 고유 식별자입니다. 에 대한 연결 사양 ID [!DNL Cassandra] is `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

시작하는 방법에 대한 자세한 내용은 [이 Cassandra 문서](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform]에 속했던 것 포함 [!DNL Flow Service]은 특정 가상 샌드박스로 구분됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

## 연결 만들기

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 커넥터는 하나만 필요합니다 [!DNL Cassandra] 계정을 사용하여 여러 소스 커넥터를 만들어 다른 데이터를 가져올 수 있습니다.

**API 형식**

```http
POST /connections
```

**요청**

을(를) 만들려면 [!DNL Cassandra] 연결 시 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. 에 대한 연결 사양 ID [!DNL Cassandra] is `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `auth.params.host` | 의 IP 주소 또는 호스트 이름 [!DNL Cassandra] server. |
| `auth.params.port` | TCP 포트 [!DNL Cassandra] 서버는 을 사용하여 클라이언트 연결을 수신합니다. 기본 포트는 다음과 같습니다 `9042`. |
| `auth.params.username` | 에 연결하는 데 사용되는 사용자 이름 [!DNL Cassandra] 인증을 위한 서버입니다. |
| `auth.params.password` | 에 연결할 암호입니다 [!DNL Cassandra] 인증을 위한 서버입니다. |
| `connectionSpec.id` | 다음 [!DNL Cassandra] 연결 사양 ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL Cassandra] 를 사용하여 연결 [!DNL Flow Service] API를 사용하고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서는 다음 ID를 사용하여 방법을 배울 수 있습니다 [흐름 서비스 API를 사용하여 데이터베이스 탐색](../../explore/database-nosql.md).
