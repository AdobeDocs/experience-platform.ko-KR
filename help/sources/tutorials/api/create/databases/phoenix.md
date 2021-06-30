---
keywords: Experience Platform;홈;인기 주제;피닉스;피닉스
solution: Experience Platform
title: Flow Service API를 사용하여 Phoenix Base Connection 생성
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Phoenix 데이터베이스를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Phoenix] 기본 연결을 만듭니다

>[!NOTE]
>
>[!DNL Phoenix] 커넥터가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 를 참조하십시오.

[!DNL Flow Service] Adobe Experience Platform 내의 다양한 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스를 연결할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 [!DNL Phoenix] 데이터베이스를 [!DNL Experience Platform]에 연결하는 단계를 안내합니다.

## 시작

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Phoenix]에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이 [!DNL Phoenix]과 연결하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | [!DNL Phoenix] 서버의 IP 주소 또는 호스트 이름입니다. |
| `username` | [!DNL Phoenix] 서버에 액세스하는 데 사용하는 사용자 이름입니다. |
| `password` | 사용자에 해당하는 암호입니다. |
| `port` | [!DNL Phoenix] 서버가 클라이언트 연결을 수신 대기하는 데 사용하는 TCP 포트입니다. [!DNL Azure] HDInsights에 연결하는 경우 포트를 443으로 지정합니다. |
| `httpPath` | [!DNL Phoenix] 서버에 해당하는 부분 URL입니다. [!DNL Azure] HDInsights 클러스터를 사용하는 경우 /hbasepaenix0을 지정합니다. |
| `enableSsl` | 부울 값. 서버에 대한 연결이 SSL을 사용하여 암호화되는지 여부를 지정합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. [!DNL Phoenix]에 대한 연결 사양 ID는 다음과 같습니다.`102706fb-a5cd-42ee-afe0-bc42f017ff43` |

시작하는 방법에 대한 자세한 내용은 [이 Phoenix 문서](https://python-phoenixdb.readthedocs.io/en/latest/api.html)를 참조하십시오.

### 플랫폼 API 사용

플랫폼 API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 요청 매개 변수의 일부로 [!DNL Phoenix] 인증 자격 증명을 제공하는 동안 `/connections` 끝점에 POST 요청을 하십시오.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Phoenix]에 대한 기본 연결을 만듭니다.

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
| `auth.params.host` | [!DNL Phoenix] 서버의 호스트입니다. |
| `auth.params.username` | [!DNL Phoenix] 연결에 연결된 사용자 이름입니다. |
| `auth.params.password` | [!DNL Phoenix] 연결에 연결된 암호입니다. |
| `auth.params.port` | [!DNL Phoenix] 연결에 대한 TCP 포트입니다. |
| `auth.params.httpPath` | [!DNL Phoenix] 연결에 대한 부분 http 경로입니다. |
| `auth.params.enableSsl` | 서버에 대한 연결이 SSL을 사용하여 암호화되는지 여부를 지정하는 부울 값입니다. |
| `connectionSpec.id` | [!DNL Phoenix] 연결 사양 ID:`102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**응답**

성공적인 응답은 해당 고유 식별자(`id`)를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 [!DNL Phoenix] 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서는 [Flow Service API](../../explore/database-nosql.md)를 사용하여 데이터베이스를 탐색하는 방법을 배울 때 이 ID를 사용할 수 있습니다.
