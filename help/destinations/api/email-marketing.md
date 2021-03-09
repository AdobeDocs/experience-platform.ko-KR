---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 이메일 마케팅 대상에 연결하고 Flow Service API를 사용하여 데이터를 활성화합니다
description: 이 문서에서는 Adobe Experience Platform API를 사용하여 이메일 마케팅 대상을 만드는 방법에 대해 설명합니다
topic: 자습서
type: 튜토리얼
translation-type: tm+mt
source-git-commit: 32cb198bcf2c142b50c4b7a60282f0c923be06b1
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 1%

---


# 이메일 마케팅 대상에 연결하고 Flow Service API를 사용하여 데이터를 활성화합니다

이 자습서에서는 API 호출을 사용하여 Adobe Experience Platform 데이터에 연결하고, [이메일 마케팅 대상](../catalog/email-marketing/overview.md)을 만들고, 데이터 흐름을 새로 만든 대상에 만들고, 데이터를 새로 만든 대상에 활성화하는 방법을 보여 줍니다.

이 자습서에서는 모든 예에서 Adobe Campaign 대상을 사용하지만, 이 단계는 모든 이메일 마케팅 대상에 대해 동일합니다.

![개요 - 대상을 만들고 세그먼트를 활성화하는 절차](../assets/api/email-marketing/overview.png)

플랫폼의 사용자 인터페이스를 사용하여 대상을 연결하고 데이터를 활성화하려면 [대상 연결](../ui/connect-destination.md) 및 [프로필 및 세그먼트를 대상](../ui/activate-destinations.md) 튜토리얼로 활성화를 참조하십시오.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] 은 데이터 위치 및 내부 계열에 대한 기록 시스템입니다 [!DNL Experience Platform].
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 플랫폼의 이메일 마케팅 대상으로 데이터를 활성화하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

이 자습서의 단계를 완료하려면 세그먼트를 연결하고 활성화할 대상 유형에 따라 다음 자격 증명이 준비되어야 합니다.

* 이메일 마케팅 플랫폼에 대한 [!DNL Amazon] S3 연결의 경우:`accessId`, `secretKey`
* 이메일 마케팅 플랫폼에 대한 SFTP 연결의 경우:`domain`, `port`, `username`, `password` 또는 `ssh key`(FTP 위치에 대한 연결 방법에 따라 다름)

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 및 선택적 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증:Bearer `{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]의 리소스는 특정 가상 샌드박스로 분리할 수 있습니다. [!DNL Platform] API에 대한 요청에서 작업이 수행될 샌드박스의 이름과 ID를 지정할 수 있습니다. 선택적 매개 변수입니다.

* x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

### Swagger 설명서

이 자습서에서는 Swagger에서 모든 API 호출에 대한 참조 설명서를 찾을 수 있습니다. Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)에 대한 [Flow Service API 설명서를 참조하십시오. 이 자습서와 Swagger 설명서 페이지를 동시에 사용하는 것이 좋습니다.

## 사용 가능한 대상 목록 {#get-the-list-of-available-destinations} 가져오기

![대상 단계 개요 단계 1](../assets/api/email-marketing/step1.png)

첫 번째 단계로 데이터를 활성화할 이메일 마케팅 대상을 결정해야 합니다. 먼저 세그먼트를 연결하고 활성화할 수 있는 사용 가능한 대상 목록을 요청하는 호출을 수행하십시오. 사용 가능한 대상 목록을 반환하려면 `connectionSpecs` 끝점에 다음 GET 요청을 수행하십시오.

**API 형식**

```http
GET /connectionSpecs
```

**요청**

<!--

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \    
    -H 'Content-Type: application/json' \
```

-->

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**응답**

성공적인 응답에는 사용 가능한 대상 및 고유 식별자(`id`) 목록이 포함됩니다. 추가 단계에서 필요하므로 사용할 대상의 값을 저장합니다. 예를 들어 세그먼트를 연결하고 Adobe Campaign에 제공하려는 경우 응답에서 다음 코드 조각을 찾습니다.

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## [!DNL Experience Platform] 데이터 {#connect-to-your-experience-platform-data}에 연결

![대상 단계 개요 단계 2](../assets/api/email-marketing/step2.png)

다음으로 프로필 데이터를 내보내고 원하는 대상에서 활성화할 수 있도록 [!DNL Experience Platform] 데이터에 연결해야 합니다. 이것은 아래에 설명된 두 가지 하위 단계로 구성됩니다.

1. 먼저 기본 연결을 설정하여 [!DNL Experience Platform]에서 데이터에 대한 액세스를 인증하기 위한 호출을 수행해야 합니다.
2. 그런 다음 기본 연결 ID를 사용하여 소스 연결을 만드는 다른 호출을 수행하여 [!DNL Experience Platform] 데이터에 대한 연결을 설정합니다.


### [!DNL Experience Platform]에서 데이터에 대한 액세스 권한 부여

**API 형식**

```http
POST /connections
```

**요청**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            }
           }'
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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


* `{CONNECTION_SPEC_ID}`:통합 프로필 서비스에 연결 사양 ID 사용 -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**응답**

성공적인 응답에는 기본 연결의 고유 식별자(`id`)가 포함됩니다. 소스 연결을 만들기 위해 다음 단계에서 필요에 따라 이 값을 저장합니다.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### [!DNL Experience Platform] 데이터 {#connect-to-platform-data}에 연결

**API 형식**

```http
POST /sourceConnections
```

**요청**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
  "name": "Connecting to Unified Profile Service",
  "description": "Optional",
  "baseConnectionId": "{BASE_CONNECTION_ID}",
  "connectionSpec": {
    "id": "{CONNECTION_SPEC}",
    "version": "1.0"
  },
  "data": {
    "format": "CSV",
    "schema": null
  }
  }
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
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

* `{BASE_CONNECTION_ID}`:이전 단계에서 얻은 ID를 사용합니다.
* `{CONNECTION_SPEC_ID}`:연결 사양 ID를  [!DNL Unified Profile Service] - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**응답**

성공적으로 응답하면 새로 만든 소스 연결이 [!DNL Unified Profile Service]에 대한 고유 식별자(`id`)가 반환됩니다. 그러면 [!DNL Experience Platform] 데이터에 성공적으로 연결되었음을 확인합니다. 이 값은 이후 단계에서 필요에 따라 저장합니다.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 이메일 마케팅 대상 {#connect-to-email-marketing-destination}에 연결

![대상 단계 개요 단계 3](../assets/api/email-marketing/step3.png)

이 단계에서 원하는 이메일 마케팅 대상에 대한 연결을 설정합니다. 이것은 아래에 설명된 두 가지 하위 단계로 구성됩니다.

1. 먼저 기본 연결을 설정하여 이메일 서비스 공급자에 대한 액세스를 인증하는 호출을 수행해야 합니다.
2. 그런 다음 기본 연결 ID를 사용하여 대상 연결을 만드는 다른 호출을 수행합니다. 이 호출은 내보낸 데이터를 전달할 저장소 계정의 위치 및 내보낼 데이터의 형식을 지정합니다.

### 이메일 마케팅 대상에 대한 액세스 권한 부여

**API 형식**

```http
POST /connections
```

**요청**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "S3 Connection for Adobe Campaign",
            "description": "ACME company holiday campaign",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            },
            "auth": {
                "specName": "{S3 or SFTP}",
                "params": {
                    "accessId": "{ACCESS_ID}",
                    "secretKey": "{SECRET_KEY}"
                }
            }
           }'
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{S3 or SFTP}",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
}'
```

* `{CONNECTION_SPEC_ID}`:사용 가능한 대상 목록  [가져오기 단계에서 얻은 연결 사양 ID를 사용합니다](#get-the-list-of-available-destinations).
* `{S3 or SFTP}`:이 대상에 대해 원하는 연결 유형을 입력합니다. [대상 카탈로그](../catalog/overview.md)에서 원하는 대상으로 스크롤하여 S3 및/또는 SFTP 연결 유형이 지원되는지 확인합니다.
* `{ACCESS_ID}`:사용자의  [!DNL Amazon] S3 스토리지 위치에 대한 액세스 ID.
* `{SECRET_KEY}`:S3 저장 위치에 대한  [!DNL Amazon] 비밀 키.

**응답**

성공적인 응답에는 기본 연결의 고유 식별자(`id`)가 포함됩니다. 대상 연결을 만들기 위해 다음 단계에서 필요에 따라 이 값을 저장합니다.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 저장소 위치 및 데이터 형식 지정

[!DNL Adobe Experience Platform] 이메일 마케팅 및 클라우드 스토리지 대상에 대한 데이터를  [!DNL CSV] 파일 형식으로 내보냅니다.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] 내보내기 파일을 파일당 5백만 개의 레코드(행)로 자동으로 분할합니다. 각 행은 하나의 프로파일을 나타냅니다.
>
>분할된 파일 이름에 파일이 더 큰 내보내기의 일부임을 나타내는 숫자가 추가됩니다.`filename.csv`, `filename_2.csv`, `filename_3.csv`.

**API 형식**

```http
POST /targetConnections
```

**요청**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \    
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
   "baseConnectionId": "{BASE_CONNECTION_ID}",
   "name": "TargetConnection for Adobe Campaign",
   "data": {
       "format": "CSV",
       "schema": {
           "id": "1.0",
           "version": "1.0"
       },
    "connectionSpec": {
    "id": "{CONNECTION_SPEC_ID}",
    "version": "1.0"
   },
   "params": {
       "mode": "S3",
       "bucketName": "{BUCKETNAME}",
       "path": "{FILEPATH}"
    }
    }
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
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
        "bucketName": "{BUCKETNAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

* `{BASE_CONNECTION_ID}`:위 단계에서 얻은 기본 연결 ID를 사용합니다.
* `{CONNECTION_SPEC_ID}`:사용 가능한 대상 목록  [가져오기 단계에서 얻은 연결 사양을 사용합니다](#get-the-list-of-available-destinations).
* `{BUCKETNAME}`:S3  [!DNL Amazon] 버킷으로, Platform은 데이터 내보내기를 저장합니다.
* `{FILEPATH}`:Platform에서 데이터 내보내기를  [!DNL Amazon] 저장할 S3 버킷 디렉토리의 경로입니다.

**응답**

성공적인 응답은 이메일 마케팅 대상에 새로 만든 대상 연결에 대한 고유 식별자(`id`)를 반환합니다. 이 값은 이후 단계에서 필요에 따라 저장합니다.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 데이터 흐름 만들기

![대상 단계 개요 단계 4](../assets/api/email-marketing/step4.png)

이전 단계에서 얻은 ID를 사용하여 이제 데이터를 활성화할 대상과 [!DNL Experience Platform] 데이터 사이에 데이터 흐름을 만들 수 있습니다. 이 단계를 파이프라인을 구성하는 것으로 생각해 보십시오. 이 단계는 나중에 데이터가 [!DNL Experience Platform]과 원하는 대상 사이에 진행될 수 있습니다.

데이터 흐름을 만들려면 아래에 표시된 대로 POST 요청을 수행하고 페이로드 내에 아래 언급된 값을 제공합니다.

데이터 흐름을 만들려면 다음 POST 요청을 수행하십시오.

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
-H 'x-gw-ims-org-id: {IMS_ORG}' \
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

* `{FLOW_SPEC_ID}`:연결할 이메일 마케팅 대상에 대한 흐름을 사용합니다. 흐름 사양을 가져오려면 `flowspecs` 끝점에서 GET 작업을 수행하십시오. Swagger 설명서 참조:https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs을 참조하십시오. 응답에서 `upsTo`을 검색하여 연결할 이메일 마케팅 대상의 해당 ID를 복사합니다. 예를 들어 Adobe Campaign의 경우 `upsToCampaign`을 찾고 `id` 매개 변수를 복사합니다.
* `{SOURCE_CONNECTION_ID}`:Experience Platform 연결 단계에서 얻은 소스 연결 ID [를 사용합니다](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`:이메일 마케팅 대상에 대한  [연결 단계에서 얻은 대상 연결 ID를 사용합니다](#connect-to-email-marketing-destination).

**응답**

성공적인 응답은 새로 만든 데이터 흐름의 ID(`id`) 및 `etag`을 반환합니다. 두 값을 모두 적어 둡니다. 를 클릭하여 세그먼트를 활성화합니다.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 새 대상에 데이터 활성화

![대상 단계 개요 단계 5](../assets/api/email-marketing/step5.png)

모든 연결과 데이터 흐름을 만들었으므로 이제 프로필 데이터를 이메일 마케팅 플랫폼으로 활성화할 수 있습니다. 이 단계에서 대상으로 보내는 세그먼트 및 프로필 속성을 선택하고 데이터를 예약하고 대상에 보낼 수 있습니다.

세그먼트를 새 대상에 활성화하려면 아래 예와 유사한 JSON PATCH 작업을 수행해야 합니다. 한 번의 클릭으로 여러 세그먼트 및 프로필 속성을 활성화할 수 있습니다. JSON PATCH에 대한 자세한 내용은 [RFC 사양](https://tools.ietf.org/html/rfc6902)을 참조하십시오.

**API 형식**

```http
PATCH /flows
```

**요청**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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
                "id": "{SEGMENT_ID}"
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
                "id": "{SEGMENT_ID}"
            }
        }
    },
        {
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "operator": "EXISTS",
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

* `{DATAFLOW_ID}`:이전 단계에서 얻은 데이터 흐름을 사용합니다.
* `{ETAG}`:이전 단계에서 얻은 태그를 사용합니다.
* `{SEGMENT_ID}`:이 대상으로 내보낼 세그먼트 ID를 제공합니다. 활성화할 세그먼트에 대한 세그먼트 ID를 검색하려면 **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**&#x200B;으로 이동하여 왼쪽 탐색 메뉴에서 **[!UICONTROL 세그멘테이션 서비스 API]**&#x200B;를 선택하고 **[!UICONTROL 세그먼트 정의]**&#x200B;에서 `GET /segment/definitions` 작업을 찾습니다.
* `{PROFILE_ATTRIBUTE}`: 예, `"person.lastName"`

**응답**

202 OK 응답을 찾습니다. 응답 본문이 반환되지 않습니다. 요청이 올바른지 확인하려면 다음 단계인 데이터 흐름 유효성 검사를 참조하십시오.

## 데이터 흐름 확인

![대상 단계 개요 단계 6](../assets/api/email-marketing/step6.png)

자습서의 마지막 단계로, 세그먼트와 프로필 속성이 실제로 데이터 흐름에 올바르게 매핑되었는지 확인해야 합니다.

유효성을 확인하려면 다음 GET 요청을 수행하십시오.

**API 형식**

```http
GET /flows
```

**요청**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`:이전 단계의 데이터 흐름을 사용합니다.
* `{ETAG}`:이전 단계의 태그를 사용합니다.

**응답**

반환된 응답에는 이전 단계에서 제출한 세그먼트 및 프로필 속성이 `transformations` 매개 변수에 포함되어야 합니다. 응답의 샘플 `transformations` 매개 변수는 다음과 같습니다.

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                "selectors": []
            },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

## 다음 단계

이 자습서를 따라 선호하는 이메일 마케팅 대상 중 하나에 플랫폼을 연결했고 각 대상에 데이터 흐름을 설정합니다. 이제 이메일 캠페인, 타깃팅된 광고 및 기타 많은 사용 사례에 대해 보내는 데이터를 대상에서 사용할 수 있습니다. 자세한 내용은 다음 페이지를 참조하십시오.

* [대상 개요](../home.md)
* [대상 카탈로그 개요](../catalog/overview.md)