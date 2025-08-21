---
title: 흐름 서비스 API를 사용하여 Azure Blob 저장소를 Experience Platform에 연결
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Azure Blob에 연결하는 방법을 알아봅니다.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 8e932a25026bef2b785cfddfb8b668b1dd47eb0d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 3%

---

# API를 사용하여 [!DNL Azure Blob Storage]을(를) Experience Platform에 연결

[!DNL Azure Blobg Storage]API[[!DNL Flow Service] 를 사용하여 ](https://developer.adobe.com/experience-platform-apis/references/flow-service/) 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL Azure Blob Storage] 개요](../../../../connectors/cloud-storage/blob.md#authentication)를 읽어 보십시오.

## [!DNL Azure Blob Storage] 계정을 Experience Platform에 연결 {#connect}

[!DNL Azure Blob Storage] 계정을 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하세요.

### 기본 연결 만들기

>[!NOTE]
>
>만든 후에는 [!DNL Azure Blob Storage] 기본 연결의 인증 유형을 변경할 수 없습니다. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.

기본 연결은 소스를 Experience Platform에 연결하여 인증 세부 정보, 연결 상태 및 고유 ID를 저장합니다. 이 ID를 사용하여 소스 파일을 검색하고 데이터 유형 및 형식을 포함하여 수집할 특정 항목을 식별합니다.

다음 인증 유형을 사용하여 [!DNL Azure Blob Storage] 계정을 Experience Platform에 연결할 수 있습니다.

* **계정 키 인증**: 저장소 계정의 액세스 키를 사용하여 인증하고 [!DNL Azure Blob Storage] 계정에 연결합니다.
* **SAS(공유 액세스 서명)**: SAS URI를 사용하여 [!DNL Azure Blob Storage] 계정의 리소스에 위임되고 제한된 시간 제한 액세스를 제공합니다.
* **서비스 사용자 기반 인증**: Azure Active Directory(AAD) 서비스 사용자(클라이언트 ID 및 암호)를 사용하여 Azure Blob 저장소 계정을 안전하게 인증합니다.

**API 형식**

```https
POST /connections
```

기본 연결 ID를 만들려면 `/connections` 끝점에 POST를 요청하고 인증 자격 증명을 요청 매개 변수의 일부로 제공합니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

계정 키 인증을 사용하려면 `connectionString`, `container` 및 `folderPath`에 대한 값을 제공하십시오.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage connection using connectingString",
    "description": "Azure Blob Storage connection using connectionString",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| 매개변수 | 설명 |
| --- | --- |
| `connectionString` | [!DNL Azure Blob Storage] 계정에 대한 연결 문자열입니다. 연결 문자열 패턴은 `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net`입니다. |
| `container` | 데이터 파일이 저장된 [!DNL Azure Blob Storage] 컨테이너의 이름입니다. |
| `folderPath` | 파일이 있는 지정된 컨테이너 내의 경로입니다. |
| `connectionSpec.id` | [!DNL Azure Blob Storage] 소스의 연결 사양 ID입니다. 이 ID는 `4c10e202-c428-4796-9208-5f1f5732b1cf`(으)로 수정되었습니다. |

>[!TAB 공유 액세스 서명]

공유 액세스 서명을 사용하려면 `sasUri`, `container` 및 `folderPath`에 대한 값을 제공하십시오.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using SAS URI",
    "description": "Azure Blob Storage source connection using SAS URI",
    "auth": {
      "specName": "SAS URI Authentication",
      "params": {
        "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| 매개변수 | 설명 |
| --- | --- |
| `sasUri` | 계정을 연결하는 데 대체 인증 유형으로 사용할 수 있는 공유 액세스 서명 URI입니다. SAS URI 패턴: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. |
| `container` | 데이터 파일이 저장된 [!DNL Azure Blob Storage] 컨테이너의 이름입니다. |
| `folderPath` | 파일이 있는 지정된 컨테이너 내의 경로입니다. |
| `connectionSpec.id` | [!DNL Azure Blob Storage] 소스의 연결 사양 ID입니다. 이 ID는 `4c10e202-c428-4796-9208-5f1f5732b1cf`(으)로 수정되었습니다. |

>[!TAB 서비스 사용자 기반 인증]

서비스 사용자 기반 인증을 통해 연결하려면 `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` 및 `folderPath`에 대한 값을 제공하십시오.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using service principal based authentication",
    "description": "Azure Blob Storage source connection using service principal based authentication",
    "auth": {
      "specName": "Service Principal Based Authentication",
      "params": {
        "serviceEndpoint": "{SERVICE_ENDPOINT}",
        "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
        "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
        "accountKind": "{ACCOUNT_KIND}",
        "tenant": "{TENANT}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| 매개변수 | 설명 |
| --- | --- |
| `serviceEndpoint` | [!DNL Azure Blob Storage] 계정의 끝점 URL입니다. 일반적으로 형식은 `https://{ACCOUNT_NAME}.blob.core.windows.net`입니다. |
| `servicePrincipalId` | 인증에 사용되는 Azure Active Directory(AAD) 서비스 사용자의 클라이언트/응용 프로그램 ID입니다. |
| `servicePrincipalKey` | Azure 서비스 주체와 연결된 클라이언트 암호 또는 암호입니다. |
| `accountKind` | [!DNL Azure Blob Storage] 계정의 형식입니다. 일반적인 값에는 `Storage`(일반 목적 V1), `StorageV2`(일반 목적 V2), `BlobStorage` 및 `BlockBlobStorage`이(가) 포함됩니다. |
| `tenant` | 서비스 주체가 등록된 Azure Active Directory(AAD) 테넌트 ID입니다. |
| `container` | 데이터 파일이 저장된 [!DNL Azure Blob Storage] 컨테이너의 이름입니다. |
| `folderPath` | 파일이 있는 지정된 컨테이너 내의 경로입니다. |
| `connectionSpec.id` | [!DNL Azure Blob Storage] 소스의 연결 사양 ID입니다. 이 ID는 `4c10e202-c428-4796-9208-5f1f5732b1cf`(으)로 수정되었습니다. |

>[!ENDTABS]

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다. 다음 단계에서 소스 연결을 만들려면 이 ID가 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```



## 다음 단계

이 자습서에 따라 API를 사용하여 [!DNL Blob] 연결을 만들었고 고유 ID를 응답 본문의 일부로 가져왔습니다. 이 연결 ID를 사용하여 [흐름 서비스 API를 사용하여 클라우드 저장소 탐색](../../explore/cloud-storage.md)할 수 있습니다.
