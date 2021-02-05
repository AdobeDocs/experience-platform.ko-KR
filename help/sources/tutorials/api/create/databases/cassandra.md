---
keywords: Experience Platform;홈;인기 항목;Apache Cassandra;Cassandra;Cassandra
solution: Experience Platform
title: Flow Service API를 사용하여 Apache Cassandra 소스 연결 만들기
topic: overview
type: Tutorial
description: Flow Service API를 사용하여 Apache Cassandra를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---


# [!DNL Flow Service] API를 사용하여 [!DNL Apache Cassandra] 소스 연결 만들기

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집한 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 [!DNL Apache Cassandra](이하 &quot;Cassandra&quot;라 한다)을 [!DNL Experience Platform]에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 Cassandra에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Cassandra]에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | [!DNL Cassandra] 서버의 IP 주소 또는 호스트 이름입니다. |
| `port` | [!DNL Cassandra] 서버가 클라이언트 연결을 수신하는 데 사용하는 TCP 포트입니다. 기본 포트는 `9042`입니다. |
| `username` | 인증을 위해 [!DNL Cassandra] 서버에 연결하는 데 사용되는 사용자 이름입니다. |
| `password` | 인증을 위해 [!DNL Cassandra] 서버에 연결하는 암호입니다. |
| `connectionSpec.id` | 연결을 만드는 데 필요한 고유 식별자입니다. [!DNL Cassandra]에 대한 연결 사양 ID는 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`입니다. |

시작하는 방법에 대한 자세한 내용은 [이 Cassandra 문서](https://cassandra.apache.org/doc/latest/operating/security.html#authentication)를 참조하십시오.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증:Bearer `{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name:`{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형:`application/json`

## 연결 만들기

연결은 소스를 지정하며 해당 소스의 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 소스 커넥터를 만드는 데 사용할 수 있으므로 [!DNL Cassandra] 계정에는 커넥터가 하나만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

[!DNL Cassandra] 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. [!DNL Cassandra]에 대한 연결 사양 ID는 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`입니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.host` | [!DNL Cassandra] 서버의 IP 주소 또는 호스트 이름입니다. |
| `auth.params.port` | [!DNL Cassandra] 서버가 클라이언트 연결을 수신하는 데 사용하는 TCP 포트입니다. 기본 포트는 `9042`입니다. |
| `auth.params.username` | 인증을 위해 [!DNL Cassandra] 서버에 연결하는 데 사용되는 사용자 이름입니다. |
| `auth.params.password` | 인증을 위해 [!DNL Cassandra] 서버에 연결하는 암호입니다. |
| `connectionSpec.id` | [!DNL Cassandra] 연결 사양 ID:`a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 [!DNL Cassandra] 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서는 Flow Service API](../../explore/database-nosql.md)를 사용하여 [데이터베이스를 탐색하는 방법을 배울 때 이 ID를 사용할 수 있습니다.
