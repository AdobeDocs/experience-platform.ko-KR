---
keywords: Experience Platform;home;popular topics;Azure Data Lake Storage Gen2;azure data lake storage;Azure
solution: Experience Platform
title: Flow Service API를 사용하여 Azure Data Lake Storage Gen2 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 Experience Platform을 Azure Data Lake Storage Gen2(이하 "ADLS Gen2"라 한다)에 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 2%

---


# API를 사용하여 [!DNL Azure] Data Lake Storage Gen2 커넥터 [!DNL Flow Service] 만들기

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집된 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 Data Lake Storage Gen2(이하 &quot;ADLS Gen2&quot; [!DNL Experience Platform] )에 연결하는 [!DNL Azure] 단계를 안내합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 ADLS Gen2 소스 커넥터를 성공적으로 만들기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

ADLS Gen2 [!DNL Flow Service] 에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `url` | 주소 URL. |
| `servicePrincipalId` | 응용 프로그램의 클라이언트 ID입니다. |
| `servicePrincipalKey` | 응용 프로그램 키 |
| `tenant` | 응용 프로그램이 포함된 테넌트 정보. |

이러한 값에 대한 자세한 내용은 [이 ADLS Gen2 문서를 참조하십시오](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

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

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 여러 소스 커넥터를 만들어 다른 데이터를 가져올 수 있으므로 ADLS Gen2 계정당 하나의 연결만 필요합니다.

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
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.url` | ADLS Gen2 계정의 URL 끝점입니다. |
| `auth.params.servicePrincipalId` | ADLS Gen2 계정의 서비스 주체 ID. |
| `auth.params.servicePrincipalKey` | ADLS Gen2 계정의 서비스 주요 키입니다. |
| `auth.params.tenant` | ADLS Gen2 계정의 테넌트 정보입니다. |
| `connectionSpec.id` | ADLS Gen2 연결 사양 ID: `0ed90a81-07f4-4586-8190-b40eccef1c5a1`. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 다음 단계에서 클라우드 스토리지를 탐색하려면 이 ID가 필요합니다.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## 다음 단계

이 튜토리얼을 따라 API를 사용하는 ADLS Gen2 연결을 만들고 응답 본문의 일부로 고유 ID를 받았습니다. 이 연결 ID를 사용하여 Flow Service API를 사용하여 클라우드 스토리지 [를](../../explore/cloud-storage.md) 탐색하거나 Flow Service API를 사용하여 [인제스트 쪽모이 세공 데이터를 생성할 수 있습니다](../../cloud-storage-parquet.md).
