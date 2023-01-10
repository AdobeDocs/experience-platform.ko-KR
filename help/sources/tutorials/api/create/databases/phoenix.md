---
keywords: Experience Platform;홈;인기 주제;피닉스;피닉스
solution: Experience Platform
title: Flow Service API를 사용하여 Phoenix Base Connection 생성
type: Tutorial
description: Flow Service API를 사용하여 Phoenix 데이터베이스를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# 만들기 [!DNL Phoenix] 기본 연결 [!DNL Flow Service] API

>[!NOTE]
>
>다음 [!DNL Phoenix] 커넥터가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 커넥터 사용에 대한 자세한 정보.

[!DNL Flow Service] Adobe Experience Platform 내의 다양한 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스를 연결할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] 연결 단계를 안내하는 API [!DNL Phoenix] 데이터베이스 대상 [!DNL Experience Platform].

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Phoenix] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 연결 [!DNL Phoenix]를 채울 때는 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 의 IP 주소 또는 호스트 이름 [!DNL Phoenix] server. |
| `username` | 액세스하는 데 사용하는 사용자 이름 [!DNL Phoenix] 서버. |
| `password` | 사용자에 해당하는 암호입니다. |
| `port` | TCP 포트 [!DNL Phoenix] 서버는 을 사용하여 클라이언트 연결을 수신합니다. 에 연결하는 경우 [!DNL Azure] HDInsights를 443으로 지정합니다. |
| `httpPath` | 에 해당하는 부분 URL [!DNL Phoenix] server. /hbasepaenix0(사용 시) 지정 [!DNL Azure] HDInsights 클러스터. |
| `enableSsl` | 부울 값. 서버에 대한 연결이 SSL을 사용하여 암호화되는지 여부를 지정합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 에 대한 연결 사양 ID [!DNL Phoenix] is: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

시작하는 방법에 대한 자세한 내용은 [이 피닉스 문서](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 제공하는 동안 엔드포인트 [!DNL Phoenix] 요청 매개 변수의 일부로 인증 자격 증명.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Phoenix]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}",
            "port": {PORT},
            "httpPath": "{PATH}",
            "enableSsl": {SSL}
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
| `auth.params.host` | 의 호스트 [!DNL Phoenix] server. |
| `auth.params.username` | 사용자 이름과 연결된 사용자 이름 [!DNL Phoenix] 연결. |
| `auth.params.password` | 와 연결된 암호 [!DNL Phoenix] 연결. |
| `auth.params.port` | 사용자의 TCP 포트 [!DNL Phoenix] 연결. |
| `auth.params.httpPath` | 에 대한 부분 http 경로 [!DNL Phoenix] 연결. |
| `auth.params.enableSsl` | 서버에 대한 연결이 SSL을 사용하여 암호화되는지 여부를 지정하는 부울 값입니다. |
| `connectionSpec.id` | 다음 [!DNL Phoenix] 연결 사양 ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL Phoenix] 기본 연결 [!DNL Flow Service] API. 다음 자습서에서는 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 컨텐츠를 탐색합니다. [!DNL Flow Service] API](../../explore/tabular.md)
* [데이터 흐름을 만들어 [!DNL Flow Service] API](../../collect/database-nosql.md)
