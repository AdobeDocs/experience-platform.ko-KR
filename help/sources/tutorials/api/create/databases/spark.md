---
keywords: Experience Platform;home;popular topics;Apache Spark;apache spark;Azure HDInsights
solution: Experience Platform
title: Flow Service API를 사용하여 Azure HDInsights 커넥터에서 Apache Spark 만들기
topic: overview
description: 이 자습서에서는 Flow Service API를 사용하여 Azure HDInsights(이하 "Spark"라 한다)의 Apache Spark를 Experience Platform에 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 5959d4344ec1c16542de045899ce74beb39a7bc4
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 2%

---


# API를 사용하여 [!DNL Apache Spark] HDInsights 커넥터 [!DNL Azure] 에 [!DNL Flow Service] 만들기

>[!NOTE]
>
>온 [!DNL Apache Spark] 커넥터 [!DNL Azure HDInsights] 가 베타에 있습니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../../../home.md#terms-and-conditions) 참조하십시오.

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집된 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 연결 단계 [!DNL Apache Spark] (이하 &quot; [!DNL Azure HDInsights] &quot;[!DNL Spark]이라 한다)를 단계별로 [!DNL Experience Platform]안내합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 API를 [!DNL Spark] 사용하기 위해 연결하기 위해 알아야 할 추가 정보를 [!DNL Flow Service] 제공합니다.

### 필요한 자격 증명 수집

연결 [!DNL Flow Service] 을 [!DNL Spark]하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 서버의 IP 주소 또는 [!DNL Spark] 호스트 이름입니다. |
| `username` | 서버에 액세스하는 데 사용하는 사용자 [!DNL Spark] 이름입니다. |
| `password` | 사용자에게 해당하는 암호입니다. |
| `connectionSpec.id` | 연결을 만드는 데 필요한 고유 식별자입니다. 에 대한 연결 사양 ID [!DNL Spark] 는 다음과 같습니다. `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

시작하는 방법에 대한 자세한 내용은 [이 Spark 문서를 참조하십시오](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

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

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 소스 커넥터를 만드는 데 사용할 수 있으므로 계정당 하나의 연결만 필요합니다. [!DNL Spark]

**API 형식**

```http
POST /connections
```

**요청**

연결을 만들려면 [!DNL Spark] 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. 에 대한 연결 사양 ID [!DNL Spark] 는 `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`입니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Spark test connection",
        "description": "A Spark test connection",
        "auth": {
            "specName": "HDInsights Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
            "version": "1.0"
        }
    }'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `auth.params.host` | The host of the [!DNL Spark] server. |
| `auth.params.username` | 연결과 연결된 사용자 [!DNL Spark] 이름입니다. |
| `auth.params.password` | 연결 관련 [!DNL Spark] 암호입니다. |
| `connectionSpec.id` | 연결 [!DNL Spark] 사양 ID: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## 다음 단계

이 튜토리얼을 따라 API를 사용하여 [!DNL Spark] 연결을 만들고 연결 [!DNL Flow Service] 의 고유 ID 값을 얻게 되었습니다. 다음 자습서에서는 Flow Service API를 사용하여 데이터베이스를 [탐색하는 방법을 배울 때 이 ID를 사용할 수 있습니다](../../explore/database-nosql.md).