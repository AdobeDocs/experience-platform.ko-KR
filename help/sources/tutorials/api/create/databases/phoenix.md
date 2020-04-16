---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Flow Service API를 사용하여 Phoenix 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: c00edf487404e1d08bc86cb6692325f536964af6

---


# Flow Service API를 사용하여 Phoenix 커넥터 만들기

Flow Service는 Adobe Experience Platform에서 다양한 소스의 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 Flow Service API를 사용하여 Phoenix 데이터베이스를 Experience Platform에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Adobe Experience Platform을 사용하면 다양한 소스에서 데이터를 인제스트할 수 있을 뿐만 아니라 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 Flow Service API를 사용하여 Phoenix에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

Flow Service가 Phoenix와 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | Phoenix 서버의 IP 주소 또는 호스트 이름입니다. |
| `username` | Phoenix Server에 액세스하는 데 사용하는 사용자 이름입니다. |
| `password` | 사용자에 해당하는 암호입니다. |
| `port` | Phoenix 서버가 클라이언트 연결을 수신하는 데 사용하는 TCP 포트입니다. Azure HDInsights에 연결하는 경우 포트를 443으로 지정하십시오. |
| `httpPath` | Phoenix 서버에 해당하는 부분 URL. Azure HDInsights 클러스터를 사용하는 경우 /hbasephoenix0을 지정합니다. |
| `enableSsl` | 부울 값입니다. 서버에 대한 연결을 SSL을 사용하여 암호화할지 여부를 지정합니다. |
| `connectionSpec.id` | 연결을 만드는 데 필요한 고유 식별자입니다. Phoenix의 연결 사양 ID는 다음과 같습니다. `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

시작하는 방법에 대한 자세한 내용은 [이 Phoenix 문서를](https://python-phoenixdb.readthedocs.io/en/latest/api.html)참조하십시오.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../../../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

* 인증:베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Flow Service에 속하는 리소스를 비롯하여 Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 연결 만들기

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 여러 소스 커넥터를 만들어 다른 데이터를 가져오는 데 사용할 수 있으므로 Phoenix 계정당 하나의 연결만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

Phoenix 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. Phoenix의 연결 사양 ID는 `102706fb-a5cd-42ee-afe0-bc42f017ff43`입니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `auth.params.host` | Phoenix 서버 호스트입니다. |
| `auth.params.username` | Phoenix 연결과 연결된 사용자 이름입니다. |
| `auth.params.password` | Phoenix 연결과 관련된 암호입니다. |
| `auth.params.port` | Phoenix 연결에 대한 TCP 포트입니다. |
| `auth.params.httpPath` | Phoenix 연결에 대한 부분 http 경로입니다. |
| `auth.params.enableSsl` | 서버에 대한 연결이 SSL을 사용하여 암호화되는지 여부를 지정하는 부울 값입니다. |
| `connectionSpec.id` | Phoenix 연결 사양 ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`Adobe |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 다음 단계

이 자습서를 따라 Flow Service API를 사용하여 Phoenix 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서 Flow Service API를 사용하여 데이터베이스를 [탐색하는 방법을 배울 때 이 ID를 사용할 수 있습니다](../../explore/database-nosql.md).