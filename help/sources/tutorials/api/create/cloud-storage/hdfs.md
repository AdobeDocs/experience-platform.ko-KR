---
keywords: Experience Platform;홈;인기 항목;Apache Hadoop 분산 파일 시스템;Apache hadoop;hdfs;HDFS
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Apache HDFS 기본 연결 만들기
type: Tutorial
description: Flow Service API를 사용하여 Apache Hadoop 분산 파일 시스템을 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다.
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# 만들기 [!DNL Apache] 를 사용하는 HDFS 기본 연결 [!DNL Flow Service] API

>[!NOTE]
>
>Apache HDFS 커넥터는 Beta 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블이 지정된 커넥터 사용에 대한 자세한 정보를 제공합니다.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Apache Hadoop Distributed File System] (이하 &quot;라고 한다)[!DNL HDFS]&quot;) 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL HDFS] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `url` | URL은에 연결하는 데 필요한 인증 매개 변수를 정의합니다. [!DNL HDFS] 익명으로 이 값을 얻는 방법에 대한 자세한 내용은 [이 [!DNL HDFS] 문서](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL AdWords] 은(는) `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL HDFS] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL HDFS]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.url` | 에 연결하는 데 필요한 인증 매개변수를 정의하는 URL [!DNL HDFS] 익명으로 |
| `connectionSpec.id` | 다음 [!DNL HDFS] 연결 사양 ID: `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**응답**

성공한 응답은 고유 식별자를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다(`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL HDFS] 을 사용한 연결 [!DNL Flow Service] API이며 연결의 고유 ID 값을 가져왔습니다. 다음 자습서에서 이 ID를 사용하여 다음 방법을 배울 수 있습니다 [흐름 서비스 API를 사용하여 서드파티 클라우드 스토리지 탐색](../../explore/cloud-storage.md).
