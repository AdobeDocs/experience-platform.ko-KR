---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Flow Service API를 사용하여 배치 대상에 연결하고 데이터를 활성화합니다
description: Flow Service API를 사용하여 Experience Platform에서 배치 클라우드 스토리지 또는 이메일 마케팅 대상을 만들고 데이터를 활성화하는 단계별 지침입니다
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '3420'
ht-degree: 2%

---

# Flow Service API를 사용하여 배치 대상에 연결하고 데이터를 활성화합니다

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions).
>
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions).
>
>다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 자습서에서는 Flow Service API를 사용하여 배치를 만드는 방법을 보여 줍니다 [클라우드 스토리지](../catalog/cloud-storage/overview.md) 또는 [이메일 마케팅 대상](../catalog/email-marketing/overview.md)를 채우기 위해 새로 만든 대상으로 데이터 흐름을 만들고 CSV 파일을 통해 새로 만든 대상으로 데이터를 내보냅니다.

이 자습서에서는 [!DNL Adobe Campaign] 대상에 포함되지만 단계는 모든 배치 클라우드 스토리지 및 이메일 마케팅 대상에 대해 동일합니다.

![개요 - 대상을 만들고 세그먼트를 활성화하는 절차](../assets/api/email-marketing/overview.png)

Platform 사용자 인터페이스를 사용하여 대상에 연결하고 데이터를 활성화하려면 를 참조하십시오. [대상 연결](../ui/connect-destination.md) 및 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../ui/activate-batch-profile-destinations.md) 튜토리얼.

## 시작하기 {#get-started}

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md): [!DNL Adobe Experience Platform Segmentation Service] 에서 세그먼트를 작성하고 대상을 생성할 수 있습니다. [!DNL Adobe Experience Platform] 다음 [!DNL Real-Time Customer Profile] 데이터.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 Platform에서 배치 대상으로 데이터를 활성화하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집 {#gather-required-credentials}

이 자습서의 단계를 완료하려면 세그먼트를 연결하고 활성화할 대상 유형에 따라 다음 자격 증명이 준비되어야 합니다.

* 대상 [!DNL Amazon S3] 연결: `accessId`, `secretKey`
* 대상 [!DNL Amazon S3] 연결 [!DNL Adobe Campaign]: `accessId`, `secretKey`
* SFTP 연결의 경우: `domain`, `port`, `username`, `password` 또는 `sshKey` (FTP 위치에 대한 연결 방법에 따라 다름)
* 대상 [!DNL Azure Blob] 연결: `connectionString`

>[!NOTE]
>
>자격 증명 `accessId`, `secretKey` 대상 [!DNL Amazon S3] 연결 및 `accessId`, `secretKey` 대상 [!DNL Amazon S3] 연결 [!DNL Adobe Campaign] 은 동일합니다.

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 및 선택적 헤더에 대한 값을 수집합니다 {#gather-values-headers}

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 분리할 수 있습니다. 요청에서 [!DNL Platform] API를 사용하여 작업을 수행할 샌드박스의 이름과 ID를 지정할 수 있습니다. 선택적 매개 변수입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Experience Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

### API 참조 설명서 {#api-reference-documentation}

이 자습서에서는 모든 API 작업에 대한 추가 참조 설명서를 찾을 수 있습니다. 자세한 내용은 [Adobe I/O에 대한 Flow Service API 설명서](https://www.adobe.io/experience-platform-apis/references/flow-service/). 이 자습서와 API 참조 설명서를 동시에 사용하는 것이 좋습니다.

## 사용 가능한 대상 목록 가져오기 {#get-the-list-of-available-destinations}

![대상 단계 개요 1단계](../assets/api/batch-destination/step1.png)

첫 번째 단계에서는 데이터를 활성화할 대상을 결정해야 합니다. 시작하려면 호출을 수행하여 세그먼트를 연결하고 활성화할 수 있는 사용 가능한 대상 목록을 요청합니다. 에 다음 GET 요청을 수행합니다. `connectionSpecs` 사용 가능한 대상 목록을 반환하는 끝점:

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

성공적인 응답에는 사용 가능한 대상 목록과 고유한 식별자(`id`). 추가 단계에서 필요하므로 사용할 대상의 값을 저장합니다. 예를 들어 세그먼트를 연결하고 [!DNL Adobe Campaign], 응답에서 다음 코드 조각을 찾습니다.

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

참조용으로 아래 표에는 일반적으로 사용되는 배치 대상에 대한 연결 사양 ID가 포함되어 있습니다.

| 대상 | 연결 사양 ID |
---------|----------|
| [!DNL Adobe Campaign] | `0b23e41a-cb4a-4321-a78f-3b654f5d7d97` |
| [!DNL Amazon S3] | `4890fc95-5a1f-4983-94bb-e060c08e3f81` |
| [!DNL Azure Blob] | `e258278b-a4cf-43ac-b158-4fa0ca0d948b` |
| [!DNL Oracle Eloqua] | `c1e44b6b-e7c8-404b-9031-58f0ef760604` |
| [!DNL Oracle Responsys] | `a5e28ddf-e265-426e-83a1-9d03a3a6822b` |
| [!DNL Salesforce Marketing Cloud] | `f599a5b3-60a7-4951-950a-cc4115c7ea27` |
| SFTP | `64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0` |

{style=&quot;table-layout:auto&quot;}

## 에 연결 [!DNL Experience Platform] 데이터 {#connect-to-your-experience-platform-data}

![대상 단계 개요 2단계](../assets/api/batch-destination/step2.png)

다음으로, [!DNL Experience Platform] 데이터, 즉 프로필 데이터를 내보내고 선호하는 대상에서 활성화할 수 있습니다. 이 작업은 아래에 설명된 두 가지 하위 단계로 구성됩니다.

1. 먼저 의 데이터에 대한 액세스를 승인하려면 호출을 수행해야 합니다 [!DNL Experience Platform]를 설정하는 것이 좋습니다.
2. 그런 다음 기본 연결 ID를 사용하여 를 만드는 다른 호출을 수행합니다 *소스 연결*: 에 대한 연결을 설정합니다. [!DNL Experience Platform] 데이터.

### 에서 데이터에 대한 액세스 권한 인증 [!DNL Experience Platform]

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
| `name` | Experience Platform에 대한 기본 연결의 이름을 제공합니다 [!DNL Profile Store]. |
| `description` | 기본 연결에 대한 설명을 제공할 수도 있습니다. |
| `connectionSpec.id` | 연결 사양 ID를 사용하여 [Experience Platform 프로필 저장소](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답에는 기본 연결의 고유 식별자(`id`). 다음 단계에서 필요에 따라 이 값을 저장하여 소스 연결을 만듭니다.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 에 연결 [!DNL Experience Platform] 데이터 {#connect-to-platform-data}

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
            "name": "Connecting to Profile Store",
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
| `name` | Experience Platform에 대한 소스 연결의 이름을 제공합니다 [!DNL Profile Store]. |
| `description` | 소스 연결에 대한 설명을 제공할 수 있습니다(선택적). |
| `connectionSpec.id` | 연결 사양 ID를 사용하여 [Experience Platform 프로필 저장소](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |
| `baseConnectionId` | 이전 단계에서 얻은 기본 연결 ID를 사용합니다. |
| `data.format` | `CSV` 는 현재 유일하게 지원되는 파일 내보내기 형식입니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 고유 식별자(`id`) 새로 만든 소스 연결용 [!DNL Profile Store]. 이 경우 [!DNL Experience Platform] 데이터. 이 값은 이후 단계에서 필요하므로 저장합니다.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```

## 배치 대상에 연결 {#connect-to-batch-destination}

![대상 단계 개요 3단계](../assets/api/batch-destination/step3.png)

이 단계에서는 원하는 배치 클라우드 스토리지 또는 이메일 마케팅 대상에 대한 연결을 설정합니다. 이 작업은 아래에 설명된 두 가지 하위 단계로 구성됩니다.

1. 먼저 기본 연결을 설정하여 대상 플랫폼에 대한 액세스를 승인하려면 호출을 수행해야 합니다.
2. 그런 다음 기본 연결 ID를 사용하여 *타겟 연결*: 내보낸 데이터 파일을 전달할 저장소 계정의 위치와 내보낼 데이터 형식을 지정합니다.

### 배치 대상에 대한 액세스 권한 인증 {#authorize-access-to-batch-destination}

**API 형식**

```http
POST /connections
```

**요청**

아래 요청은에 대한 기본 연결을 설정합니다. [!DNL Adobe Campaign] 대상. 파일을 내보낼 저장소 위치([!DNL Amazon S3], SFTP, [!DNL Azure Blob]), 적절하게 유지 `auth` 세부 항목을 지정하고 다른 항목은 삭제합니다.

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

지원되는 다른 배치 클라우드 스토리지 및 이메일 마케팅 대상에 연결하려면 아래 요청 예 를 참조하십시오.

+++ 연결 요청 예 [!DNL Amazon S3] 대상

아래 요청은에 대한 기본 연결을 설정합니다. [!DNL Amazon S3] 대상.

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

+++ 연결 요청 예 [!DNL Azure Blob] 대상

아래 요청은에 대한 기본 연결을 설정합니다. [!DNL Azure Blob] 대상.

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

+++ 연결 요청 예 [!DNL Oracle Eloqua] 대상

아래 요청은에 대한 기본 연결을 설정합니다. [!DNL Oracle Eloqua] 대상. 파일을 내보낼 저장소 위치에 따라 적절하게 유지합니다 `auth` 세부 항목을 지정하고 다른 항목은 삭제합니다.

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

+++ 연결 요청 예 [!DNL Oracle Responsys] 대상

아래 요청은에 대한 기본 연결을 설정합니다. [!DNL Oracle Responsys] 대상. 파일을 내보낼 저장소 위치에 따라 적절하게 유지합니다 `auth` 세부 항목을 지정하고 다른 항목은 삭제합니다.

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

+++ 연결 요청 예 [!DNL Salesforce Marketing Cloud] 대상

아래 요청은에 대한 기본 연결을 설정합니다. [!DNL Salesforce Marketing Cloud] 대상. 파일을 내보낼 저장소 위치에 따라 적절하게 유지합니다 `auth` 세부 항목을 지정하고 다른 항목은 삭제합니다.

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

+++ 암호 대상을 사용하여 SFTP에 연결하는 요청 예

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
| `description` | 기본 연결에 대한 설명을 제공할 수도 있습니다. |
| `connectionSpec.id` | 원하는 배치 대상에 연결 사양 ID를 사용합니다. 이 ID는 단계에서 가져왔습니다 [사용 가능한 대상 목록 가져오기](#get-the-list-of-available-destinations). |
| `auth.specname` | 대상에 대한 인증 형식을 나타냅니다. 대상에 대한 specName을 확인하려면 [연결 사양 끝점에 대한 GET 호출](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec): 원하는 대상의 연결 사양을 제공합니다. 매개 변수를 찾습니다 `authSpec.name` 을 반환합니다. <br> 예를 들어 Adobe Campaign 대상의 경우 다음 중 하나를 사용할 수 있습니다 `S3`, `SFTP with Password`, 또는 `SFTP with SSH Key`. |
| `params` | 연결하는 대상에 따라 다른 필수 인증 매개 변수를 제공해야 합니다. Amazon S3 연결의 경우 Amazon S3 저장소 위치에 액세스 ID 및 암호 키를 제공해야 합니다. <br> 대상에 필요한 매개 변수를 찾으려면 다음을 수행하십시오. [연결 사양 끝점에 대한 GET 호출](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec): 원하는 대상의 연결 사양을 제공합니다. 매개 변수를 찾습니다 `authSpec.spec.required` 을 반환합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답에는 기본 연결의 고유 식별자(`id`). 다음 단계에서 필요에 따라 이 값을 저장하여 대상 연결을 만듭니다.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 저장소 위치 및 데이터 형식 지정 {#specify-storage-location-data-format}

[!DNL Adobe Experience Platform] 배치 이메일 마케팅 및 클라우드 스토리지 대상에 대한 데이터를 다음과 같은 형태로 내보냅니다. [!DNL CSV] 파일. 이 단계에서는 파일을 내보낼 스토리지 위치의 경로를 확인할 수 있습니다.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] 에서는 내보내기 파일을 파일당 500만 개의 레코드(행)로 자동 분할합니다. 각 행은 하나의 프로필을 나타냅니다.
>
>파일 이름을 분할하면 파일이 더 큰 내보내기의 일부임을 나타내는 숫자가 추가됩니다. `filename.csv`, `filename_2.csv`, `filename_3.csv`.

**API 형식**

```http
POST /targetConnections
```

**요청**

아래 요청은 대상 연결을 설정합니다. [!DNL Adobe Campaign] 대상 - 내보낸 파일이 저장 위치에 도착하는 위치를 결정합니다. 파일을 내보낼 저장소 위치에 따라 적절하게 유지합니다 `params` 세부 항목을 지정하고 다른 항목은 삭제합니다.

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

지원되는 다른 배치 클라우드 스토리지 및 이메일 마케팅 대상에 대한 스토리지 위치를 설정하려면 아래 예제 요청 을 참조하십시오.

+++ 스토리지 위치 설정 요청 예 [!DNL Amazon S3] 대상

아래 요청은 대상 연결을 설정합니다. [!DNL Amazon S3] 대상 - 내보낸 파일이 저장 위치에 도착하는 위치를 결정합니다.

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

+++ 스토리지 위치 설정 요청 예 [!DNL Azure Blob] 대상

아래 요청은 대상 연결을 설정합니다. [!DNL Azure Blob] 대상 - 내보낸 파일이 저장 위치에 도착하는 위치를 결정합니다.

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

+++ 스토리지 위치 설정 요청 예 [!DNL Oracle Eloqua] 대상

아래 요청은 대상 연결을 설정합니다. [!DNL Oracle Eloqua] 대상 - 내보낸 파일이 저장 위치에 도착하는 위치를 결정합니다. 파일을 내보낼 저장소 위치에 따라 적절하게 유지합니다 `params` 세부 항목을 지정하고 다른 항목은 삭제합니다.

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

+++ 스토리지 위치 설정 요청 예 [!DNL Oracle Responsys] 대상

아래 요청은 대상 연결을 설정합니다. [!DNL Oracle Responsys] 대상 - 내보낸 파일이 저장 위치에 도착하는 위치를 결정합니다. 파일을 내보낼 저장소 위치에 따라 적절하게 유지합니다 `params` 세부 항목을 지정하고 다른 항목은 삭제합니다.

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

+++ 스토리지 위치 설정 요청 예 [!DNL Salesforce Marketing Cloud] 대상

아래 요청은 대상 연결을 설정합니다. [!DNL Salesforce Marketing Cloud] 대상 - 내보낸 파일이 저장 위치에 도착하는 위치를 결정합니다. 파일을 내보낼 저장소 위치에 따라 적절하게 유지합니다 `params` 세부 항목을 지정하고 다른 항목은 삭제합니다.

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

+++ SFTP 대상에 대한 저장소 위치 설정에 대한 요청 예

아래 요청은 SFTP 대상에 대한 타겟 연결을 설정하여 내보낸 파일이 저장소 위치에 도착하는 위치를 결정합니다.

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
| `description` | 선택적으로 대상 연결에 대한 설명을 제공할 수 있습니다. |
| `baseConnectionId` | 위의 단계에서 만든 기본 연결의 ID를 사용합니다. |
| `connectionSpec.id` | 원하는 배치 대상에 연결 사양 ID를 사용합니다. 이 ID는 단계에서 가져왔습니다 [사용 가능한 대상 목록 가져오기](#get-the-list-of-available-destinations). |
| `params` | 연결 중인 대상에 따라 스토리지 위치에 다른 필수 매개 변수를 제공해야 합니다. Amazon S3 연결의 경우 Amazon S3 저장소 위치에 액세스 ID 및 암호 키를 제공해야 합니다. <br> 대상에 필요한 매개 변수를 찾으려면 다음을 수행하십시오. [연결 사양 끝점에 대한 GET 호출](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec): 원하는 대상의 연결 사양을 제공합니다. 매개 변수를 찾습니다 `targetSpec.spec.required` 을 반환합니다. |
| `params.mode` | 대상에 대해 지원되는 모드에 따라 여기에서 다른 값을 제공해야 합니다. 대상에 필요한 매개 변수를 찾으려면 다음을 수행하십시오. [연결 사양 끝점에 대한 GET 호출](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec): 원하는 대상의 연결 사양을 제공합니다. 매개 변수를 찾습니다 `targetSpec.spec.properties.mode.enum` 응답에서 원하는 모드를 선택합니다. |
| `params.bucketName` | S3 연결의 경우 파일을 내보낼 버킷의 이름을 제공합니다. |
| `params.path` | S3 연결의 경우 파일을 내보낼 저장 위치에 파일 경로를 제공합니다. |
| `params.format` | `CSV` 는 현재 유일하게 지원되는 파일 내보내기 형식입니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 고유 식별자(`id`)를 배치 대상에 새로 만든 target 연결에 대해 사용할 수 있습니다. 이 값은 이후 단계에서 필요에 따라 저장합니다.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 데이터 흐름 만들기 {#create-dataflow}

![대상 단계 개요 4단계](../assets/api/batch-destination/step4.png)

이제 흐름 사양, 소스 연결 및 대상 연결 ID를 사용하여 [!DNL Experience Platform] 데이터 및 데이터 파일을 내보낼 대상 이 단계는 나중에 사이에 데이터가 흐르게 되는 파이프라인을 구성하는 것으로 생각해 보십시오 [!DNL Experience Platform] 및 원하는 대상을 선택합니다.

데이터 흐름을 만들려면 페이로드 내에서 아래에 언급된 값을 제공하면서 아래 표시된 대로 POST 요청을 수행하십시오.

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
   
        "name": "Activate segments to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate segments to Adobe Campaign",
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
| `name` | 만드는 데이터 흐름의 이름을 입력합니다. |
| `description` | 선택적으로 데이터 흐름의 설명을 제공할 수 있습니다. |
| `flowSpec.Id` | 연결하려는 배치 대상에 대한 흐름 사양 ID를 사용합니다. 흐름 사양 ID를 검색하려면 `flowspecs` 엔드포인트, 에 표시된 대로 [흐름 사양 API 참조 설명서](https://www.adobe.io/experience-platform-apis/references/flow-service/#operation/retrieveFlowSpec). 응답에서 `upsTo` 연결할 배치 대상의 해당 ID를 복사합니다. 예를 들어 Adobe Campaign의 경우 `upsToCampaign` 그리고 `id` 매개 변수. |
| `sourceConnectionIds` | 단계에서 얻은 소스 연결 ID를 사용합니다 [Experience Platform 데이터에 연결](#connect-to-your-experience-platform-data). |
| `targetConnectionIds` | 단계에서 얻은 대상 연결 ID를 사용합니다 [배치 대상에 연결](#connect-to-batch-destination). |
| `transformations` | 다음 단계에서는 활성화할 세그먼트 및 프로필 속성으로 이 섹션을 채웁니다. |

참조용으로 아래 표에는 일반적으로 사용되는 배치 대상에 대한 흐름 사양 ID가 포함되어 있습니다.

| 대상 | 흐름 사양 ID |
---------|----------|
| 모든 클라우드 스토리지 대상([!DNL Amazon S3], SFTP, [!DNL Azure Blob]) 및 [!DNL Oracle Eloqua] | `71471eba-b620-49e4-90fd-23f1fa0174d8` |
| [!DNL Oracle Responsys] | `51d675ce-e270-408d-91fc-22717bdf2148` |
| [!DNL Salesforce Marketing Cloud] | `493b2bd6-26e4-4167-ab3b-5e910bba44f0` |

**응답**

성공적인 응답은 ID(`id`)을 만들 수 있습니다 `etag`. 세그먼트를 활성화하고 데이터 파일을 내보내려면 다음 단계에서 필요한 대로 두 값을 모두 기록해 두십시오.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 새 대상에 데이터 활성화 {#activate-data}

![대상 단계 개요 5단계](../assets/api/batch-destination/step5.png)

이제 모든 연결 및 데이터 흐름을 만들었으므로 프로필 데이터를 대상 플랫폼에 활성화할 수 있습니다. 이 단계에서 대상으로 내보낼 세그먼트 및 프로필 속성을 선택합니다.

내보낸 파일의 파일 이름 지정 형식과 사용할 속성을 결정할 수도 있습니다 [중복 제거 키](../ui/activate-batch-profile-destinations.md#mandatory-keys) 또는 [필수 속성](../ui/activate-batch-profile-destinations.md#mandatory-attributes). 이 단계에서 대상으로 데이터를 보내는 일정을 결정할 수도 있습니다.

세그먼트를 새 대상에 활성화하려면 아래 예와 같이 JSON PATCH 작업을 수행해야 합니다. 한 번의 호출로 여러 세그먼트와 프로필 속성을 활성화할 수 있습니다. JSON PATCH에 대해 자세히 알아보려면 [RFC 사양](https://tools.ietf.org/html/rfc6902).

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
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
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
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
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
| `{DATAFLOW_ID}` | URL에서 이전 단계에서 만든 데이터 흐름의 ID를 사용합니다. |
| `{ETAG}` | 가져오기 `{ETAG}` 이전 단계의 응답에서 [데이터 흐름 만들기](#create-dataflow). 이전 단계의 응답 형식이 따옴표를 이스케이프 처리했습니다. 요청 헤더에 이스케이프 처리되지 않은 값을 사용해야 합니다. 아래 예를 참조하십시오. <br> <ul><li>응답 예: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>요청에 사용할 값: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> 태그 값은 데이터 흐름을 성공적으로 업데이트할 때마다 업데이트됩니다. |
| `{SEGMENT_ID}` | 이 대상으로 내보낼 세그먼트 ID를 제공합니다. 활성화할 세그먼트의 세그먼트 ID를 검색하려면 를 참조하십시오 [세그먼트 정의 검색](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) ( Experience Platform API 참조). |
| `{PROFILE_ATTRIBUTE}` | 예, `"person.lastName"` |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. 데이터 플로우에 세그먼트를 추가하려면 `add` 작업. |
| `path` | 업데이트할 흐름의 일부를 정의합니다. 데이터 플로우에 세그먼트를 추가할 때는 예제에 지정된 경로를 사용합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |
| `id` | 대상 데이터 플로우에 추가할 세그먼트의 ID를 지정합니다. |
| `name` | *선택 사항입니다*. 대상 데이터 플로우에 추가할 세그먼트 이름을 지정합니다. 이 필드는 필수가 아니므로 이름을 제공하지 않고 대상 데이터 플로우에 세그먼트를 성공적으로 추가할 수 있습니다. |
| `filenameTemplate` | 이 필드는 대상으로 내보내는 파일의 파일 이름 형식을 결정합니다. <br> 다음 옵션을 사용할 수 있습니다. <br> <ul><li>`%DESTINATION_NAME%`: 필수입니다. 내보낸 파일에 대상 이름이 포함되어 있습니다.</li><li>`%SEGMENT_ID%`: 필수입니다. 내보낸 파일에는 내보낸 세그먼트의 ID가 포함되어 있습니다.</li><li>`%SEGMENT_NAME%`: 선택 사항입니다. 내보낸 파일에 내보낸 세그먼트의 이름이 포함됩니다.</li><li>`DATETIME(YYYYMMdd_HHmmss)` 또는 `%TIMESTAMP%`: 선택 사항입니다. 파일에서 Experience Platform으로 생성되는 시간을 포함하려면 이 두 옵션 중 하나를 선택합니다.</li><li>`custom-text`: 선택 사항입니다. 이 자리 표시자를 파일 이름의 끝에 추가할 사용자 지정 텍스트로 바꿉니다.</li></ul> <br> 파일 이름 구성에 대한 자세한 내용은 [파일 이름 구성](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 섹션에 나열된 상태로 남아 있습니다. |
| `exportMode` | 필수입니다. `"DAILY_FULL_EXPORT"` 또는`"FIRST_FULL_THEN_INCREMENTAL"`를 선택합니다. 두 옵션에 대한 자세한 내용은 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 배치 대상 활성화 자습서에서 를 참조하십시오. |
| `startDate` | 세그먼트가 대상에 프로필 내보내기를 시작할 날짜를 선택합니다. |
| `frequency` | 필수입니다. <br> <ul><li>대상 `"DAILY_FULL_EXPORT"` 내보내기 모드, `ONCE` 또는 `DAILY`.</li><li>대상 `"FIRST_FULL_THEN_INCREMENTAL"` 내보내기 모드, `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | 대상 *배치 대상* 전용. 이 필드는 `"DAILY_FULL_EXPORT"` 모드 `frequency` 선택기. <br> 필수입니다. <br> <ul><li>선택 `"AFTER_SEGMENT_EVAL"` 을(를) 통해 일별 플랫폼 배치 세분화 작업이 완료된 후 즉시 활성화 작업을 실행할 수 있습니다. 이렇게 하면 활성화 작업이 실행될 때 최신 프로필을 대상으로 내보낼 수 있습니다.</li><li>선택 `"SCHEDULED"` 를 입력하여 고정된 시간에 활성화 작업을 실행합니다. 이렇게 하면 Experience Platform 프로필 데이터를 매일 동시에 내보낼 수 있지만, 내보내는 프로필은 활성화 작업이 시작되기 전에 배치 세그먼테이션 작업이 완료되었는지 여부에 따라 최신 프로필이 아닐 수 있습니다. 이 옵션을 선택할 때는 `startTime` 를 입력하여 일별 내보내기가 발생해야 하는 시간을 UTC로 나타냅니다.</li></ul> |
| `endDate` | 대상 *배치 대상* 전용. 이 필드는 Amazon S3, SFTP 또는 Azure Blob과 같은 배치 파일 내보내기 대상의 데이터 플로우에 세그먼트를 추가할 때만 필요합니다. <br> 선택할 때 해당 사항 없음 `"exportMode":"DAILY_FULL_EXPORT"` 및 `"frequency":"ONCE"`. <br> 세그먼트 구성원이 대상으로 내보내기를 중지하는 날짜를 설정합니다. |
| `startTime` | 대상 *배치 대상* 전용. 이 필드는 Amazon S3, SFTP 또는 Azure Blob과 같은 배치 파일 내보내기 대상의 데이터 플로우에 세그먼트를 추가할 때만 필요합니다. <br> 필수입니다. 세그먼트의 구성원이 포함된 파일을 생성하여 대상으로 내보내는 시간을 선택합니다. |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
> 자세한 내용은 [데이터 흐름에서 세그먼트의 구성 요소 업데이트](/help/destinations/api/update-destination-dataflows.md#update-segment) 내보낸 세그먼트의 다양한 구성 요소(파일 이름 템플릿, 내보내기 시간 등)를 업데이트하는 방법을 알아봅니다.

**응답**

202 수락된 응답을 찾습니다. 응답 본문이 반환되지 않습니다. 요청이 올바른지 확인하려면 다음 단계를 참조하십시오. [데이터 흐름 유효성 검사](#validate-dataflow).

## 데이터 흐름 유효성 검사 {#validate-dataflow}

![대상 단계 개요 6단계](../assets/api/batch-destination/step6.png)

자습서의 마지막 단계에서는 세그먼트 및 프로필 속성이 실제로 데이터 집합에 올바르게 매핑되었는지 확인해야 합니다.

유효성을 검사하려면 다음 GET 요청을 수행합니다.

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
* `{ETAG}`: 이전 단계의 태그를 사용합니다.

**응답**

반환된 응답에는 `transformations` 매개 변수 이전 단계에서 제출한 세그먼트 및 프로필 속성을 지정합니다. 샘플 `transformations` 응답의 매개 변수는 다음과 같을 수 있습니다.

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

이 자습서의 API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](/help/landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](/help/landing/troubleshooting.md#request-header-errors) 오류 응답 해석에 대한 자세한 내용은 플랫폼 문제 해결 가이드를 참조하십시오.

## 다음 단계 {#next-steps}

이 자습서를 따라 Platform을 기본 설정 배치 클라우드 스토리지 또는 이메일 마케팅 대상 중 하나에 연결하고 데이터 파일을 내보내기 위해 각 대상에 데이터 플로를 설정했습니다. 이제 보내는 데이터를 대상에 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 사용할 수 있습니다. Flow Service API를 사용하여 기존 데이터 흐름을 편집하는 방법 등 자세한 내용은 다음 페이지를 참조하십시오.

* [대상 개요](../home.md)
* [대상 카탈로그 개요](../catalog/overview.md)
* [Flow Service API를 사용하여 대상 데이터 흐름 업데이트](../api/update-destination-dataflows.md)
