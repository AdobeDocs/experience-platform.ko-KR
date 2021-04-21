---
keywords: Experience Platform;홈;인기 항목;Azure;azure blob;blob;Blob
solution: Experience Platform
title: Flow Service API를 사용하여 Azure Blob 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Azure Blob에 Adobe Experience Platform을 연결하는 방법을 알아봅니다.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Azure Blob] 소스 연결 만들기

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)을 사용하여 [!DNL Azure Blob](이하 &quot;물방울&quot;이라 한다)을 Adobe Experience Platform에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Blob] 소스 연결을 성공적으로 만들기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Blob] 저장소에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | Experience Platform에 대해 [!DNL Blob]을(를) 인증하는 데 필요한 인증 정보를 포함하는 문자열입니다. [!DNL Blob] 연결 문자열 패턴은 다음과 같습니다.`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. 연결 문자열에 대한 자세한 내용은 [연결 문자열 구성](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)의 이 [!DNL Blob] 문서를 참조하십시오. |
| `sasUri` | 대체 인증 유형으로 사용하여 [!DNL Blob] 계정을 연결할 수 있는 공유 액세스 서명 URI입니다. [!DNL Blob] SAS URI 패턴은 다음과 같습니다.`https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 자세한 내용은 [공유 액세스 서명 URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)에 있는 이 [!DNL Blob] 문서를 참조하십시오. |
| `connectionSpec.id` | 연결을 만드는 데 필요한 고유 식별자입니다. [!DNL Blob]에 대한 연결 사양 ID는 다음과 같습니다.`4c10e202-c428-4796-9208-5f1f5732b1cf` |

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 호출 예](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 연결 만들기

연결은 소스를 지정하며 해당 소스의 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 데이터 흐름을 만드는 데 사용할 수 있으므로 [!DNL Blob] 계정당 하나의 연결만 필요합니다.

### 연결 문자열 기반 인증을 사용하여 [!DNL Blob] 연결 만들기

연결 문자열 기반 인증을 사용하여 [!DNL Blob] 연결을 만들려면 [!DNL Blob] `connectionString`을(를) 제공하는 동안 [!DNL Flow Service] API에 POST 요청을 하십시오.

**API 형식**

```http
POST /connections
```

**요청**

[!DNL Blob] 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. [!DNL Blob]에 대한 연결 사양 ID는 `4c10e202-c428-4796-9208-5f1f5732b1cf`입니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob connection using connectionString",
        "description": "Azure Blob connection using connectionString",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
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
| `auth.params.connectionString` | Blob 저장소의 데이터에 액세스하는 데 필요한 연결 문자열입니다. Blob 연결 문자열 패턴은 다음과 같습니다.`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Blob 저장소 연결 사양 ID는 다음과 같습니다.`4c10e202-c428-4796-9208-5f1f5732b1cf` |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 저장소를 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### 공유 액세스 서명 URI를 사용하여 [!DNL Blob] 연결 만들기

SAS(Shared Access Signature) URI를 사용하면 [!DNL Blob] 계정에 대한 보안 위임 인증을 허용합니다. SAS 기반 인증을 통해 특정 리소스에 대한 규정 및 권한, 시작 및 만료 날짜를 설정할 수 있으므로 SAS를 사용하여 액세스 수준이 다른 인증 자격 증명을 만들 수 있습니다.

공유 액세스 서명 URI를 사용하여 [!DNL Blob] 연결을 만들려면 [!DNL Blob] `sasUri`에 대한 값을 제공하는 동안 [!DNL Flow Service] API에 POST 요청을 하십시오.

**API 형식**

```http
POST /connections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob source connection using SAS URI",
        "description": "Azure Blob source connection using SAS URI",
        "auth": {
            "specName": "SasURIAuthentication",
            "params": {
                "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>"
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
| `auth.params.connectionString` | [!DNL Blob] 저장소의 데이터에 액세스하는 데 필요한 SAS URI입니다. [!DNL Blob] SAS URI 패턴은 다음과 같습니다.`https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | [!DNL Blob] 스토리지 연결 사양 ID:`4c10e202-c428-4796-9208-5f1f5732b1cf` |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 저장소를 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## 다음 단계

이 자습서를 따라 API를 사용하여 [!DNL Blob] 연결을 만들고 고유한 ID를 응답 본문의 일부로 받았습니다. 이 연결 ID를 Flow Service API](../../explore/cloud-storage.md) 또는 [인제스트 Portable 데이터를 사용하여 [클라우드 스토리지 탐색에 사용할 수 있습니다. Flow Service API](../../cloud-storage-parquet.md)
