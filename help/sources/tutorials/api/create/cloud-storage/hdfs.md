---
keywords: Experience Platform;홈;인기 항목;Apache Hadoop 분산 파일 시스템;Apache hadoop;hdfs;HDFS
solution: Experience Platform
title: Flow Service API를 사용하여 Apache HDFS 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 Apache Hadoop Distributed File System(이하 "HDFS"라 한다)을 Experience Platform에 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---


# [!DNL Flow Service] API를 사용하여 [!DNL Apache] HDFS 커넥터 만들기

>[!NOTE]
>
>Apache HDFS 커넥터가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

[!DNL Flow Service] 는 다양한 소스의 고객 데이터를 수집 및 중앙화하여 Adobe Experience Platform으로 가져오는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서는 [!DNL Flow Service] API를 사용하여 Apache Hadoop 배포 파일 시스템(이하 &quot;HDFS&quot;라 한다)을 [!DNL Experience Platform]에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 HDFS에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `url` | URL은 HDFS에 익명으로 연결하는 데 필요한 인증 매개 변수를 정의합니다. 이 값을 얻는 방법에 대한 자세한 내용은 [이 HDFS 문서](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)를 참조하십시오. |
| `connectionSpec.id` | 연결을 만드는 데 필요한 식별자입니다. HDFS에 대한 고정 연결 사양 ID는 `54e221aa-d342-4707-bcff-7a4bceef0001`입니다. |

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 연결 만들기

연결은 소스를 지정하며 해당 소스의 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 소스 커넥터를 만드는 데 사용할 수 있으므로 HDFS 계정당 하나의 연결만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 페이로드에서 제공하는 속성으로 구성된 새 HDFS 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `auth.params.url` | HDFS에 익명으로 연결하는 데 필요한 인증 매개 변수를 정의하는 URL |
| `connectionSpec.id` | HDFS 연결 사양 ID:`54e221aa-d342-4707-bcff-7a4bceef0001`. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 HDFS 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서는 흐름 서비스 API](../../explore/cloud-storage.md)를 사용하여 [타사 클라우드 스토리지를 탐색하는 방법을 배울 때 이 ID를 사용할 수 있습니다.
