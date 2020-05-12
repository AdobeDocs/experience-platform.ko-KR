---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Flow Service API를 사용하여 Azure Blob 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: 7ffe560f455973da3a37ad102fbb8cc5969d5043
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---


# Flow Service API를 사용하여 Azure Blob 커넥터 만들기

Flow Service는 Adobe Experience Platform에서 다양한 소스의 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 Flow Service API를 사용하여 Experience Platform을 Azure Blob(이하 &quot;Blob&quot;) 저장소에 연결하는 단계를 안내합니다.

경험 플랫폼에서 사용자 인터페이스를 사용하려는 경우 [Azure Blob 또는 Amazon S3 소스 커넥터 UI 자습서는](../../../ui/create/cloud-storage/blob-s3.md) 유사한 작업을 수행하기 위한 단계별 지침을 제공합니다.

## 시작하기

이 가이드에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md): Adobe Experience Platform을 사용하면 다양한 소스에서 데이터를 인제스트할 수 있으며, 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): 경험 플랫폼은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 Flow Service API를 사용하여 Blob 저장소에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

Flow Service가 Blob 저장소에 연결하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | Blob 저장소의 데이터에 액세스하는 데 필요한 연결 문자열입니다. |

시작하는 방법에 대한 자세한 내용은 [이 Azure Blob 문서를 참조하십시오](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string).

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 경험 플랫폼 문제 해결 안내서에서 예제 API 호출 [](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 읽기를 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를 완료해야 합니다](../../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 경험 플랫폼 API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증: 무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Flow Service에 속하는 리소스를 비롯하여 경험 플랫폼의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 연결 만들기

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 소스 커넥터를 만드는 데 사용할 수 있으므로 Blob 계정당 하나의 연결만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Blob Connection",
        "description": "Cnnection for an Azure Blob account",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.connectionString` | Blob 저장소의 연결 문자열입니다. |
| `connectionSpec.id` | Blob 저장소 연결 사양 ID: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 저장소를 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## 다음 단계

이 튜토리얼을 따라 API를 사용하여 Blob 연결을 만들고 응답 본문의 일부로 고유한 ID를 얻었습니다. 이 연결 ID를 사용하여 Flow Service API를 사용하여 클라우드 스토리지 [를](../../explore/cloud-storage.md) 탐색하거나 Flow Service API를 사용하여 [인제스트 쪽모이 세공 데이터를 생성할 수 있습니다](../../cloud-storage-parquet.md).