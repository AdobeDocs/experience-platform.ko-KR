---
keywords: Experience Platform;홈;인기 항목;Apache Cassandra;Apache Cassandra;Cassandra;Cassandra
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Apache Cassandra 소스 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Apache Cassandra를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다.
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---


# 만들기 [!DNL Apache Cassandra] 를 사용한 소스 연결 [!DNL Flow Service] API

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 개별 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결 가능한 사용자 인터페이스와 RESTful API를 제공합니다.

이 튜토리얼에서는 [!DNL Flow Service] 연결하는 단계를 안내하는 API [!DNL Apache Cassandra] (이하 &quot;카산드라&quot;라 함) [!DNL Experience Platform].

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 를 사용하여 Cassandra에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다. [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 연결 대상 [!DNL Cassandra], 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 의 IP 주소 또는 호스트 이름 [!DNL Cassandra] 서버입니다. |
| `port` | 이 작동하는 TCP 포트 [!DNL Cassandra] 서버는 를 사용하여 클라이언트 연결을 수신합니다. 기본 포트는 입니다. `9042`. |
| `username` | 에 연결하는 데 사용된 사용자 이름 [!DNL Cassandra] 인증용 서버입니다. |
| `password` | 에 연결할 암호 [!DNL Cassandra] 인증용 서버입니다. |
| `connectionSpec.id` | 연결을 만드는 데 필요한 고유 식별자입니다. 에 대한 연결 사양 ID [!DNL Cassandra] 은(는) `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

시작하기에 대한 자세한 내용은 을(를) 참조하십시오. [이 Cassandra 문서](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### 샘플 API 호출 읽기

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값 수집

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform], 다음에 속하는 항목 포함 [!DNL Flow Service]는 특정 가상 샌드박스로 분리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

## 연결 만들기

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 커넥터당 하나만 필요합니다. [!DNL Cassandra] 여러 소스 커넥터를 만들어 서로 다른 데이터를 가져오는 데 사용할 수 있는 계정

**API 형식**

```http
POST /connections
```

**요청**

를 만들려면 [!DNL Cassandra] 연결, 고유한 연결 사양 ID는 POST 요청의 일부로 제공해야 합니다. 에 대한 연결 사양 ID [!DNL Cassandra] 은(는) `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

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
| `auth.params.host` | 의 IP 주소 또는 호스트 이름 [!DNL Cassandra] 서버입니다. |
| `auth.params.port` | 이 작동하는 TCP 포트 [!DNL Cassandra] 서버는 를 사용하여 클라이언트 연결을 수신합니다. 기본 포트는 입니다. `9042`. |
| `auth.params.username` | 에 연결하는 데 사용된 사용자 이름 [!DNL Cassandra] 인증용 서버입니다. |
| `auth.params.password` | 에 연결할 암호 [!DNL Cassandra] 인증용 서버입니다. |
| `connectionSpec.id` | 다음 [!DNL Cassandra] 연결 사양 ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**응답**

성공한 응답은 고유 식별자를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다(`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Cassandra] 을 사용한 연결 [!DNL Flow Service] API이며 연결의 고유 ID 값을 가져왔습니다. 다음 자습서에서 이 ID를 사용하여 다음 방법을 배울 수 있습니다 [흐름 서비스 API를 사용하여 데이터베이스 탐색](../../explore/database-nosql.md).
