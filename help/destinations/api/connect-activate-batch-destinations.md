---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 배치 대상에 연결하고 데이터를 활성화합니다
description: 플로우 서비스 API를 사용하여 Experience Platform 시 일괄 클라우드 스토리지 또는 이메일 마케팅 대상을 만들고 데이터를 활성화하는 단계별 지침
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '3411'
ht-degree: 2%

---

# 파일 기반 이메일 마케팅 대상에 연결하고 플로우 서비스 API를 사용하여 데이터를 활성화합니다

>[!IMPORTANT]
> 
>* 대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다.
>
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다.
>
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}
>
>[액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 자습서에서는 흐름 서비스 API를 사용하여 파일 기반 [이메일 마케팅 대상](../catalog/email-marketing/overview.md)을(를) 만들고, 새로 만든 대상에 데이터 흐름을 만들고, CSV 파일을 통해 새로 만든 대상에 데이터를 내보내는 방법을 보여 줍니다.

>[!TIP]
> 
>흐름 서비스 API를 사용하여 클라우드 저장소 대상에 데이터를 활성화하는 방법을 알아보려면 [전용 API 튜토리얼](/help/destinations/api/activate-segments-file-based-destinations.md)을(를) 읽어 보십시오.

이 자습서에서는 모든 예에서 [!DNL Adobe Campaign] 대상을 사용하지만 파일 기반 이메일 마케팅 대상의 단계는 동일합니다.

![개요 - 대상을 만들고 대상을 활성화하는 단계](../assets/api/email-marketing/overview.png)

Platform 사용자 인터페이스를 사용하여 대상에 연결하고 데이터를 활성화하려면 [대상 연결](../ui/connect-destination.md) 및 [대상 데이터를 프로필 내보내기 대상 일괄 처리에 활성화](../ui/activate-batch-profile-destinations.md) 튜토리얼을 참조하십시오.

## 시작하기 {#get-started}

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md): [!DNL Adobe Experience Platform Segmentation Service]을(를) 사용하면 [!DNL Real-Time Customer Profile] 데이터에서 [!DNL Adobe Experience Platform]의 대상을 작성할 수 있습니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform]은(는) 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션은 Platform의 배치 대상으로 데이터를 활성화하기 위해 알아야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집 {#gather-required-credentials}

이 자습서의 단계를 완료하려면 대상을 연결하고 활성화하는 대상 유형에 따라 다음 자격 증명을 준비해야 합니다.

* [!DNL Amazon S3] 연결: `accessId`, `secretKey`
* [!DNL Adobe Campaign]에 대한 [!DNL Amazon S3] 연결: `accessId`, `secretKey`
* SFTP 연결의 경우: `domain`, `port`, `username`, `password` 또는 `sshKey`(FTP 위치에 대한 연결 메서드에 따라 다름)
* [!DNL Azure Blob]개 연결의 경우: `connectionString`

>[!NOTE]
>
>[!DNL Amazon S3] 연결에 대한 자격 증명 `accessId`, `secretKey`과(와) [!DNL Adobe Campaign]에 대한 [!DNL Amazon S3] 연결에 대한 `accessId`, `secretKey`이(가) 동일합니다.

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

### 필수 및 선택적 헤더에 대한 값 수집 {#gather-values-headers}

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api 키: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 리소스는 특정 가상 샌드박스로 격리될 수 있습니다. [!DNL Platform] API에 대한 요청에서 작업을 수행할 샌드박스의 이름과 ID를 지정할 수 있습니다. 이러한 매개 변수는 선택 사항입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

### API 참조 설명서 {#api-reference-documentation}

이 자습서에서 모든 API 작업에 대한 참조 설명서를 함께 찾을 수 있습니다. Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/)에서 [흐름 서비스 API 설명서를 참조하세요. 이 자습서와 API 참조 설명서를 동시에 사용하는 것이 좋습니다.

## 사용 가능한 대상 목록 가져오기 {#get-the-list-of-available-destinations}

![대상 단계 개요 1단계](../assets/api/batch-destination/step1.png)

첫 번째 단계로 데이터를 활성화할 대상을 결정해야 합니다. 먼저, 대상자를 연결하고 활성화할 수 있는 사용 가능한 대상 목록을 요청하는 호출을 수행합니다. `connectionSpecs` 끝점에 대해 다음 GET 요청을 수행하여 사용 가능한 대상 목록을 반환합니다.

**API 형식**

```http
GET /connectionSpecs
```

**요청**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**응답**

성공적인 응답에는 사용 가능한 대상 목록과 해당 고유 식별자(`id`)가 포함되어 있습니다. 사용할 대상의 값을 저장합니다. 이 값은 이후 단계에서 필수입니다. 예를 들어 대상자를 [!DNL Adobe Campaign]에 연결하여 전달하려면 응답에서 다음 코드 조각을 찾습니다.

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

아래 표에는 일반적으로 사용되는 배치 대상에 대한 연결 사양 ID가 포함되어 있습니다.

| 대상 | 연결 사양 ID |
---------|----------|
| [!DNL Adobe Campaign] | `0b23e41a-cb4a-4321-a78f-3b654f5d7d97` |
| [!DNL Oracle Eloqua] | `c1e44b6b-e7c8-404b-9031-58f0ef760604` |
| [!DNL Oracle Responsys] | `a5e28ddf-e265-426e-83a1-9d03a3a6822b` |
| [!DNL Salesforce Marketing Cloud] | `f599a5b3-60a7-4951-950a-cc4115c7ea27` |

{style="table-layout:auto"}

## [!DNL Experience Platform] 데이터에 연결 {#connect-to-your-experience-platform-data}

![대상 단계 개요 2단계](../assets/api/batch-destination/step2.png)

그런 다음 [!DNL Experience Platform] 데이터에 연결해야 프로필 데이터를 내보내고 원하는 대상에서 활성화할 수 있습니다. 이 단계는 아래에 설명된 두 개의 하위 단계로 구성됩니다.

1. 먼저 기본 연결을 설정하여 [!DNL Experience Platform]의 데이터에 대한 액세스 권한을 부여하는 호출을 수행해야 합니다.
2. 그런 다음 기본 연결 ID를 사용하여 [!DNL Experience Platform] 데이터에 대한 연결을 설정하는 *소스 연결*&#x200B;을 만드는 다른 호출을 수행합니다.

### [!DNL Experience Platform]의 데이터에 대한 액세스 권한 부여

**API 형식**

```http
POST /connections
```

**요청**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```

| 속성 | 설명 |
| --------- | ----------- |
| `name` | [!DNL Profile store] Experience Platform에 대한 기본 연결의 이름을 제공하십시오. |
| `description` | 선택적으로 기본 연결에 대한 설명을 제공할 수 있습니다. |
| `connectionSpec.id` | [Experience Platform 프로필 저장소](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`에 대한 연결 사양 ID를 사용하십시오. |

{style="table-layout:auto"}

**응답**

성공한 응답에는 기본 연결의 고유 식별자(`id`)가 포함되어 있습니다. 다음 단계에서 소스 연결을 만드는 데 필요한 대로 이 값을 저장합니다.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### [!DNL Experience Platform] 데이터에 연결 {#connect-to-platform-data}

**API 형식**

```http
POST /sourceConnections
```

**요청**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile store",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

| 속성 | 설명 |
| --------- | ----------- |
| `name` | [!DNL Profile store] Experience Platform에 대한 원본 연결의 이름을 제공하십시오. |
| `description` | 선택적으로 소스 연결에 대한 설명을 제공할 수 있습니다. |
| `connectionSpec.id` | [Experience Platform 프로필 저장소](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`에 대한 연결 사양 ID를 사용하십시오. |
| `baseConnectionId` | 이전 단계에서 얻은 기본 연결 ID를 사용합니다. |
| `data.format` | `CSV`은(는) 현재 지원되는 유일한 파일 내보내기 형식입니다. |

{style="table-layout:auto"}

**응답**

성공한 응답은 [!DNL Profile store]에 새로 만든 원본 연결에 대한 고유 식별자(`id`)를 반환합니다. 이를 통해 [!DNL Experience Platform] 데이터에 성공적으로 연결되었음을 확인할 수 있습니다. 이 값은 이후 단계에서 필요한 대로 저장하십시오.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```

## 배치 대상에 연결 {#connect-to-batch-destination}

![대상 단계 개요 3단계](../assets/api/batch-destination/step3.png)

이 단계에서는 원하는 배치 클라우드 스토리지 또는 이메일 마케팅 대상에 대한 연결을 설정합니다. 이 단계는 아래에 설명된 두 개의 하위 단계로 구성됩니다.

1. 먼저 기본 연결을 설정하여 대상 플랫폼에 대한 액세스 권한을 부여하는 호출을 수행해야 합니다.
2. 그런 다음 기본 연결 ID를 사용하여 저장소 계정에서 내보낼 데이터 파일의 위치와 내보낼 데이터 형식을 지정하는 *대상 연결*&#x200B;을(를) 만드는 다른 호출을 만듭니다.

### 배치 대상에 대한 액세스 권한 인증 {#authorize-access-to-batch-destination}

**API 형식**

```http
POST /connections
```

**요청**

아래 요청은 [!DNL Adobe Campaign] 대상에 대한 기본 연결을 설정합니다. 파일을 내보낼 저장소 위치([!DNL Amazon S3], SFTP, [!DNL Azure Blob])에 따라 적절한 `auth` 사양을 유지하고 다른 사양을 삭제합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "auth": {
        "specName": "S3",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }        
    "auth": {
        "specName": "Azure Blob",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }    
}'
```

지원되는 다른 일괄 처리 클라우드 스토리지 및 이메일 마케팅 대상에 연결하려면 아래의 예제 요청을 참조하십시오.

+++ [!DNL Amazon S3] 대상에 연결하는 예제 요청

아래 요청은 [!DNL Amazon S3] 대상에 대한 기본 연결을 설정합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Amazon S3",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "auth": {
        "specName": "Access Key",
        "params": {
            "s3AccessKey": "{AMAZON_S3_ACCESS_KEY}",
            "s3SecretKey": "{AMAZON_S3_SECRET_KEY}"
        }
    }
}'
```

+++

+++ [!DNL Azure Blob] 대상에 연결하는 예제 요청

아래 요청은 [!DNL Azure Blob] 대상에 대한 기본 연결을 설정합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Azure Blob",
    "description": "Summer advertising campaign",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "auth": {
        "specName": "ConnectionString",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }
}'
```

+++

+++ [!DNL Oracle Eloqua] 대상에 연결하는 예제 요청

아래 요청은 [!DNL Oracle Eloqua] 대상에 대한 기본 연결을 설정합니다. 파일을 내보낼 저장소 위치에 따라 적절한 `auth` 사양을 유지하고 다른 사양을 삭제합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Eloqua destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ [!DNL Oracle Responsys] 대상에 연결하는 예제 요청

아래 요청은 [!DNL Oracle Responsys] 대상에 대한 기본 연결을 설정합니다. 파일을 내보낼 저장소 위치에 따라 적절한 `auth` 사양을 유지하고 다른 사양을 삭제합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Responsys destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ [!DNL Salesforce Marketing Cloud] 대상에 연결하는 예제 요청

아래 요청은 [!DNL Salesforce Marketing Cloud] 대상에 대한 기본 연결을 설정합니다. 파일을 내보낼 저장소 위치에 따라 적절한 `auth` 사양을 유지하고 다른 사양을 삭제합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Salesforce Marketing Cloud",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ 암호 대상이 있는 SFTP에 대한 연결 요청 예

아래 요청은 SFTP 대상에 대한 기본 연결을 설정합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to SFTP with password",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
}'
```

+++

| 속성 | 설명 |
| --------- | ----------- |
| `name` | 배치 대상에 대한 기본 연결의 이름을 입력합니다. |
| `description` | 선택적으로 기본 연결에 대한 설명을 제공할 수 있습니다. |
| `connectionSpec.id` | 원하는 배치 대상에 대해 연결 사양 ID를 사용합니다. [사용 가능한 대상 목록 가져오기](#get-the-list-of-available-destinations) 단계에서 이 ID를 얻었습니다. |
| `auth.specname` | 대상의 인증 형식을 나타냅니다. 대상의 specName을 확인하려면 연결 사양 끝점](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec)에 대한 [GET 호출을 수행하여 원하는 대상의 연결 사양을 제공하십시오. 응답에서 매개 변수 `authSpec.name`을(를) 찾습니다. <br> 예를 들어 Adobe Campaign 대상의 경우 `S3`, `SFTP with Password` 또는 `SFTP with SSH Key` 중 하나를 사용할 수 있습니다. |
| `params` | 연결 중인 대상에 따라 서로 다른 필수 인증 매개 변수를 제공해야 합니다. Amazon S3 연결의 경우 Amazon S3 저장소 위치에 액세스 ID와 비밀 키를 제공해야 합니다. <br> 대상에 대한 필수 매개 변수를 확인하려면 연결 사양 끝점](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec)에 대한 [GET 호출을 수행하여 원하는 대상의 연결 사양을 제공하십시오. 응답에서 매개 변수 `authSpec.spec.required`을(를) 찾습니다. |

{style="table-layout:auto"}

**응답**

성공한 응답에는 기본 연결의 고유 식별자(`id`)가 포함되어 있습니다. 다음 단계에서 대상 연결을 만드는 데 필요한 대로 이 값을 저장합니다.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 저장소 위치 및 데이터 형식 지정 {#specify-storage-location-data-format}

[!DNL Adobe Experience Platform]은(는) 일괄 이메일 마케팅 및 클라우드 저장소 대상에 대한 데이터를 [!DNL CSV]개 파일 형태로 내보냅니다. 이 단계에서는 파일을 내보낼 저장소 위치의 경로를 결정할 수 있습니다.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform]은(는) 내보내기 파일을 파일당 5백만 개의 레코드(행)로 자동으로 분할합니다. 각 행은 하나의 프로필을 나타냅니다.
>
>분할 파일 이름에는 파일이 더 큰 내보내기의 일부임을 나타내는 숫자가 추가됩니다(예: `filename.csv`, `filename_2.csv`, `filename_3.csv`).

**API 형식**

```http
POST /targetConnections
```

**요청**

아래 요청은 [!DNL Adobe Campaign] 대상에 대한 대상 연결을 설정하여 내보낸 파일이 저장소 위치에 도달할 위치를 결정합니다. 파일을 내보낼 저장소 위치에 따라 적절한 `params` 사양을 유지하고 다른 사양을 삭제합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

지원되는 다른 일괄 처리 클라우드 스토리지 및 이메일 마케팅 대상에 대한 스토리지 위치를 설정하려면 아래 예제 요청을 참조하십시오.

+++ [!DNL Amazon S3] 대상에 대한 저장소 위치 설정 요청 예

아래 요청은 [!DNL Amazon S3] 대상에 대한 대상 연결을 설정하여 내보낸 파일이 저장소 위치에 도달할 위치를 결정합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Amazon S3",
    "description": "Connection to Amazon S3",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

+++

+++ [!DNL Azure Blob] 대상에 대한 저장소 위치 설정 요청 예

아래 요청은 [!DNL Azure Blob] 대상에 대한 대상 연결을 설정하여 내보낸 파일이 저장소 위치에 도달할 위치를 결정합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Azure Blob",
    "description": "Connection to Azure Blob",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

+++

+++ [!DNL Oracle Eloqua] 대상에 대한 저장소 위치 설정 요청 예

아래 요청은 [!DNL Oracle Eloqua] 대상에 대한 대상 연결을 설정하여 내보낸 파일이 저장소 위치에 도달할 위치를 결정합니다. 파일을 내보낼 저장소 위치에 따라 적절한 `params` 사양을 유지하고 다른 사양을 삭제합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Eloqua",
    "description": "Connection to Oracle Eloqua",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ [!DNL Oracle Responsys] 대상에 대한 저장소 위치 설정 요청 예

아래 요청은 [!DNL Oracle Responsys] 대상에 대한 대상 연결을 설정하여 내보낸 파일이 저장소 위치에 도달할 위치를 결정합니다. 파일을 내보낼 저장소 위치에 따라 적절한 `params` 사양을 유지하고 다른 사양을 삭제합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Responsys",
    "description": "Connection to Oracle Responsys",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ [!DNL Salesforce Marketing Cloud] 대상에 대한 저장소 위치 설정 요청 예

아래 요청은 [!DNL Salesforce Marketing Cloud] 대상에 대한 대상 연결을 설정하여 내보낸 파일이 저장소 위치에 도달할 위치를 결정합니다. 파일을 내보낼 저장소 위치에 따라 적절한 `params` 사양을 유지하고 다른 사양을 삭제합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Salesforce Marketing Cloud",
    "description": "Connection to Salesforce Marketing Cloud",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ SFTP 대상에 대한 저장소 위치 설정 요청 예

아래 요청은 SFTP 대상에 대한 대상 연결을 설정하여 내보낸 파일이 스토리지 위치에 도달할 위치를 결정합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for SFTP",
    "description": "Connection to SFTP",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
    }
}'
```

+++


| 속성 | 설명 |
| --------- | ----------- |
| `name` | 배치 대상에 대한 대상 연결의 이름을 입력합니다. |
| `description` | 필요한 경우 대상 연결에 대한 설명을 제공할 수 있습니다. |
| `baseConnectionId` | 위의 단계에서 생성한 기본 연결의 ID를 사용하십시오. |
| `connectionSpec.id` | 원하는 배치 대상에 대해 연결 사양 ID를 사용합니다. [사용 가능한 대상 목록 가져오기](#get-the-list-of-available-destinations) 단계에서 이 ID를 얻었습니다. |
| `params` | 연결할 대상에 따라 저장소 위치에 다른 필수 매개 변수를 제공해야 합니다. Amazon S3 연결의 경우 Amazon S3 저장소 위치에 액세스 ID와 비밀 키를 제공해야 합니다. <br> 대상에 대한 필수 매개 변수를 확인하려면 연결 사양 끝점](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec)에 대한 [GET 호출을 수행하여 원하는 대상의 연결 사양을 제공하십시오. 응답에서 매개 변수 `targetSpec.spec.required`을(를) 찾습니다. |
| `params.mode` | 대상에 대해 지원되는 모드에 따라 여기에 다른 값을 제공해야 합니다. 대상에 대한 필수 매개 변수를 확인하려면 연결 사양 엔드포인트](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec)에 대한 [GET 호출을 수행하여 원하는 대상의 연결 사양을 제공하십시오. 응답에서 매개 변수 `targetSpec.spec.properties.mode.enum`을(를) 찾아 원하는 모드를 선택하십시오. |
| `params.bucketName` | S3 연결의 경우 파일을 내보낼 버킷의 이름을 입력합니다. |
| `params.path` | S3 연결의 경우 파일을 내보낼 저장소 위치의 파일 경로를 제공합니다. |
| `params.format` | `CSV`은(는) 현재 지원되는 유일한 파일 내보내기 유형입니다. |

{style="table-layout:auto"}

**응답**

응답이 성공하면 배치 대상에 새로 만든 대상 연결에 대한 고유 식별자(`id`)가 반환됩니다. 이 값은 이후 단계에서 필요에 따라 저장합니다.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 데이터 흐름 만들기 {#create-dataflow}

![대상 단계 개요 4단계](../assets/api/batch-destination/step4.png)

이제 이전 단계에서 얻은 흐름 사양, 소스 연결 및 대상 연결 ID를 사용하여 [!DNL Experience Platform] 데이터와 데이터 파일을 내보낼 대상 간에 데이터 흐름을 만들 수 있습니다. 이 단계는 나중에 [!DNL Experience Platform]과(와) 원하는 대상 간에 데이터가 흐르는 파이프라인을 구성하는 것으로 생각하십시오.

데이터 흐름을 만들려면 페이로드 내에 아래에 언급된 값을 제공하면서 아래 표시된 대로 POST 요청을 수행합니다.

**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "activate audiences to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate audiences to Adobe Campaign",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ],
        "transformations": [
            {
                "name": "GeneralTransform",
                "params": {
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

| 속성 | 설명 |
| --------- | ----------- |
| `name` | 생성 중인 데이터 흐름의 이름을 입력합니다. |
| `description` | 선택적으로 데이터 흐름에 대한 설명을 제공할 수 있습니다. |
| `flowSpec.Id` | 연결할 배치 대상에 대해 흐름 사양 ID를 사용합니다. 흐름 사양 ID를 검색하려면 [흐름 사양 API 참조 설명서](https://www.adobe.io/experience-platform-apis/references/flow-service/#operation/retrieveFlowSpec)에 표시된 대로 `flowspecs` 끝점에 대해 GET 작업을 수행하십시오. 응답에서 `upsTo`을(를) 찾아 연결할 배치 대상의 해당 ID를 복사합니다. 예를 들어 Adobe Campaign의 경우 `upsToCampaign`을(를) 찾아 `id` 매개 변수를 복사합니다. |
| `sourceConnectionIds` | [Experience Platform 데이터에 연결](#connect-to-your-experience-platform-data) 단계에서 얻은 원본 연결 ID를 사용합니다. |
| `targetConnectionIds` | [일괄 처리 대상에 연결](#connect-to-batch-destination) 단계에서 얻은 대상 연결 ID를 사용하십시오. |
| `transformations` | 다음 단계에서는 이 섹션을 활성화할 대상 및 프로필 속성으로 채웁니다. |

아래 표에는 일반적으로 사용되는 배치 대상에 대한 흐름 사양 ID가 포함되어 있습니다.

| 대상 | 흐름 사양 ID |
---------|----------|
| 모든 클라우드 저장소 대상([!DNL Amazon S3], SFTP, [!DNL Azure Blob]) 및 [!DNL Oracle Eloqua] | `71471eba-b620-49e4-90fd-23f1fa0174d8` |
| [!DNL Oracle Responsys] | `51d675ce-e270-408d-91fc-22717bdf2148` |
| [!DNL Salesforce Marketing Cloud] | `493b2bd6-26e4-4167-ab3b-5e910bba44f0` |

**응답**

성공한 응답은 새로 만든 데이터 흐름의 ID(`id`) 및 `etag`을(를) 반환합니다. 다음 단계에서 필요한 대로 두 값을 모두 기록하여 대상을 활성화하고 데이터 파일을 내보냅니다.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 새 대상에 데이터 활성화 {#activate-data}

![대상 단계 개요 5단계](../assets/api/batch-destination/step5.png)

모든 연결 및 데이터 흐름을 만들었으므로 이제 프로필 데이터를 대상 플랫폼에 활성화할 수 있습니다. 이 단계에서는 대상으로 내보낼 대상과 프로필 속성을 선택합니다.

또한 내보낸 파일의 파일 이름 지정 형식과 [중복 제거 키](../ui/activate-batch-profile-destinations.md#mandatory-keys) 또는 [필수 특성](../ui/activate-batch-profile-destinations.md#mandatory-attributes)(으)로 사용할 특성을 결정할 수 있습니다. 이 단계에서는 데이터를 대상으로 전송하는 일정을 결정할 수도 있습니다.

새 대상에 대상을 활성화하려면 아래 예제와 유사한 JSON PATCH 작업을 수행해야 합니다. 한 번의 호출로 여러 대상과 프로필 속성을 활성화할 수 있습니다. JSON PATCH에 대한 자세한 내용은 [RFC 사양](https://tools.ietf.org/html/rfc6902)을 참조하세요.

**API 형식**

```http
PATCH /flows
```

**요청**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
    {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                } 
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "triggerType": "SCHEDULED",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                },   
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

| 속성 | 설명 |
| --------- | ----------- |
| `{DATAFLOW_ID}` | URL에서 이전 단계에서 생성한 데이터 흐름의 ID를 사용합니다. |
| `{ETAG}` | 이전 단계의 응답에서 `{ETAG}`을(를) 가져옵니다. [데이터 흐름 만들기](#create-dataflow). 이전 단계의 응답 형식에서 따옴표를 이스케이프 처리했습니다. 요청의 헤더에서 이스케이프되지 않은 값을 사용해야 합니다. 아래 예제를 참조하십시오. <br> <ul><li>응답 예: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>요청에 사용할 값: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> 데이터 흐름이 성공적으로 업데이트될 때마다 etag 값이 업데이트됩니다. |
| `{SEGMENT_ID}` | 이 대상으로 내보낼 대상 ID를 제공합니다. 활성화하려는 대상에 대해 대상 ID를 검색하려면 Experience Platform API 참조에서 [대상 정의 검색](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById)을 참조하십시오. |
| `{PROFILE_ATTRIBUTE}` | 예, `"person.lastName"` |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 `add`, `replace` 및 `remove`이(가) 포함됩니다. 데이터 흐름에 대상을 추가하려면 `add` 작업을 사용하십시오. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. 데이터 흐름에 대상을 추가할 때는 예제에 지정된 경로를 사용하십시오. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |
| `id` | 대상 데이터 흐름에 추가할 대상자의 ID를 지정합니다. |
| `name` | *선택 사항*. 대상 데이터 흐름에 추가할 대상자의 이름을 지정합니다. 이 필드는 필수가 아니므로 이름을 제공하지 않고 대상 데이터 흐름에 대상을 성공적으로 추가할 수 있습니다. |
| `filenameTemplate` | 이 필드는 대상으로 내보내는 파일의 파일 이름 형식을 결정합니다. <br> 다음 옵션을 사용할 수 있습니다. <br> <ul><li>`%DESTINATION_NAME%`: 필수입니다. 내보낸 파일에는 대상 이름이 포함되어 있습니다.</li><li>`%SEGMENT_ID%`: 필수입니다. 내보낸 파일에는 내보낸 대상자의 ID가 들어 있습니다.</li><li>`%SEGMENT_NAME%`: 선택 사항입니다. 내보낸 파일에는 내보낸 대상자의 이름이 포함됩니다.</li><li>`DATETIME(YYYYMMdd_HHmmss)` 또는 `%TIMESTAMP%`: 선택 사항입니다. 다음 두 옵션 중 하나를 선택하여 Experience Platform으로 생성된 시간을 파일에 포함합니다.</li><li>`custom-text`: 선택 사항입니다. 이 자리 표시자를 파일 이름 끝에 추가할 사용자 지정 텍스트로 바꿉니다.</li></ul> <br> 파일 이름 구성에 대한 자세한 내용은 일괄 처리 대상 활성화 자습서의 [파일 이름 구성](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 섹션을 참조하십시오. |
| `exportMode` | 필수. `"DAILY_FULL_EXPORT"` 또는 `"FIRST_FULL_THEN_INCREMENTAL"`을(를) 선택하십시오. 두 옵션에 대한 자세한 내용은 일괄 처리 대상 활성화 자습서에서 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)를 참조하십시오. |
| `startDate` | 대상자가 대상으로 프로필 내보내기를 시작할 날짜를 선택합니다. |
| `frequency` | 필수. <br> <ul><li>`"DAILY_FULL_EXPORT"` 내보내기 모드의 경우 `ONCE` 또는 `DAILY`을(를) 선택할 수 있습니다.</li><li>`"FIRST_FULL_THEN_INCREMENTAL"` 내보내기 모드의 경우 `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`을(를) 선택할 수 있습니다.</li></ul> |
| `triggerType` | *일괄 처리 대상*&#x200B;에만 해당. 이 필드는 `frequency` 선택기에서 `"DAILY_FULL_EXPORT"` 모드를 선택하는 경우에만 필요합니다. <br>은(는) 필수입니다. <br> <ul><li>매일 플랫폼 일괄 처리 세분화 작업이 완료된 후 즉시 활성화 작업을 실행하려면 `"AFTER_SEGMENT_EVAL"`을(를) 선택하십시오. 이렇게 하면 활성화 작업이 실행될 때 가장 최신 프로필을 대상으로 내보냅니다.</li><li>고정된 시간에 활성화 작업을 실행하려면 `"SCHEDULED"`을(를) 선택하십시오. 이렇게 하면 Experience Platform 프로필 데이터를 매일 동시에 내보낼 수 있지만 활성화 작업이 시작되기 전에 배치 세분화 작업이 완료되었는지 여부에 따라 내보내는 프로필이 최신 프로필이 아닐 수 있습니다. 이 옵션을 선택할 때는 일별 내보내기가 발생하는 시간을 UTC로 나타내려면 `startTime`도 추가해야 합니다.</li></ul> |
| `endDate` | *일괄 처리 대상*&#x200B;에만 해당. 이 필드는 Amazon S3, SFTP 또는 Azure Blob와 같은 배치 파일 내보내기 대상의 데이터 흐름에 대상을 추가할 때만 필요합니다. `"exportMode":"DAILY_FULL_EXPORT"` 및 `"frequency":"ONCE"`을(를) 선택할 때는 <br>을(를) 적용할 수 없습니다. <br> 대상 구성원의 대상 내보내기를 중지할 날짜를 설정합니다. |
| `startTime` | *일괄 처리 대상*&#x200B;에만 해당. 이 필드는 Amazon S3, SFTP 또는 Azure Blob와 같은 배치 파일 내보내기 대상의 데이터 흐름에 대상을 추가할 때만 필요합니다. <br>은(는) 필수입니다. 대상자의 멤버가 포함된 파일을 생성하여 대상으로 내보내야 하는 시간을 선택합니다. |

{style="table-layout:auto"}

>[!TIP]
>
> 내보낸 대상의 다양한 구성 요소(파일 이름 템플릿, 내보내기 시간 등)를 업데이트하는 방법은 [데이터 흐름에서 대상의 구성 요소 업데이트](/help/destinations/api/update-destination-dataflows.md#update-segment)를 참조하십시오.

**응답**

202 수락된 응답을 찾습니다. 응답 본문이 반환되지 않습니다. 요청이 올바른지 확인하려면 다음 단계인 [데이터 흐름 유효성 검사](#validate-dataflow)를 참조하세요.

## 데이터 흐름의 유효성 검사 {#validate-dataflow}

![대상 단계 개요 6단계](../assets/api/batch-destination/step6.png)

자습서의 마지막 단계에서는 대상 및 프로필 속성이 실제로 데이터 흐름에 올바르게 매핑되었는지 확인해야 합니다.

유효성을 검사하려면 다음 GET 요청을 수행하십시오.

**API 형식**

```http
GET /flows
```

**요청**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: 이전 단계의 데이터 흐름을 사용합니다.
* `{ETAG}`: 이전 단계의 etag를 사용합니다.

**응답**

반환된 응답에는 이전 단계에서 제출한 대상 및 프로필 특성이 `transformations` 매개 변수에 포함되어야 합니다. 응답의 샘플 `transformations` 매개 변수는 다음과 같습니다.

```json
"transformations":[
   {
      "name":"GeneralTransform",
      "params":{
         "profileSelectors":{
            "selectors":[
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"homeAddress.countryCode",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"homeAddress.countryCode",
                        "destination":"homeAddress.countryCode",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"homeAddress.countryCode",
                        "destinationXdmPath":"homeAddress.countryCode"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.firstName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.firstName",
                        "destination":"person.name.firstName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.firstName",
                        "destinationXdmPath":"person.name.firstName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.lastName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.lastName",
                        "destination":"person.name.lastName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.lastName",
                        "destinationXdmPath":"person.name.lastName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"personalEmail.address",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"personalEmail.address",
                        "destination":"personalEmail.address",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"personalEmail.address",
                        "destinationXdmPath":"personalEmail.address"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"segmentMembership.status",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"segmentMembership.status",
                        "destination":"segmentMembership.status",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"segmentMembership.status",
                        "destinationXdmPath":"segmentMembership.status"
                     }
                  }
               }
            ],
            "mandatoryFields":[
               "person.name.firstName",
               "person.name.lastName"
            ],
            "primaryFields":[
               {
                  "fieldType":"ATTRIBUTE",
                  "attributePath":"personalEmail.address"
               }
            ]
         },
         "segmentSelectors":{
            "selectors":[
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                     "name":"Interested in Mountain Biking",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"DAILY_FULL_EXPORT",
                     "schedule":{
                        "frequency":"ONCE",
                        "startDate":"2021-12-20",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               },
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"25768be6-ebd5-45cc-8913-12fb3f348613",
                     "name":"Loyalty Segment",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                     "schedule":{
                        "frequency":"EVERY_6_HOURS",
                        "startDate":"2021-12-22",
                        "endDate":"2021-12-31",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               }
            ]
         }
      }
   }
]
```

## API 오류 처리 {#api-error-handling}

이 자습서의 API 끝점은 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 오류 응답 해석에 대한 자세한 내용은 플랫폼 문제 해결 안내서의 [API 상태 코드](/help/landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](/help/landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계 {#next-steps}

이 자습서에 따라 선호하는 파일 기반 이메일 마케팅 대상 중 하나에 Platform을 연결하고 데이터 파일을 내보낼 각 대상에 대한 데이터 흐름을 설정했습니다. 이제 발신 데이터를 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례의 대상에서 사용할 수 있습니다. 흐름 서비스 API를 사용하여 기존 데이터 흐름을 편집하는 방법과 같은 자세한 내용은 다음 페이지를 참조하십시오.

* [대상 개요](../home.md)
* [대상 카탈로그 개요](../catalog/overview.md)
* [흐름 서비스 API를 사용하여 대상 데이터 흐름 업데이트](../api/update-destination-dataflows.md)
