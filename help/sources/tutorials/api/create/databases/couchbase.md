---
keywords: Experience Platform;홈;인기 항목;Couchbase;Couchbase
solution: Experience Platform
title: Flow Service API를 사용하여 Couchbase 연결 만들기
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Couchbase를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 625e3acf-fc27-44cf-b4e6-becf1d107ff2
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Couchbase] 기본 연결을 만듭니다

>[!NOTE]
>
>[!DNL Couchbase] 커넥터가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 를 참조하십시오.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)를 사용하여 [!DNL Couchbase]에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Couchbase]에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | [!DNL Couchbase] 인스턴스에 연결하는 데 사용되는 연결 문자열입니다. [!DNL Couchbase]에 대한 연결 문자열 패턴은 `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`입니다. 연결 문자열 가져오기에 대한 자세한 내용은 [이 Couchbase 문서](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)를 참조하십시오. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. [!DNL Couchbase]에 대한 연결 사양 ID는 `1fe283f6-9bec-11ea-bb37-0242ac130002`입니다. |

### 플랫폼 API 사용

플랫폼 API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 요청 매개 변수의 일부로 [!DNL Couchbase] 인증 자격 증명을 제공하는 동안 `/connections` 끝점에 POST 요청을 하십시오.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Couchbase]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Couchbase test connection",
        "description": "A test connection for a Couchbase source",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                    "connectionString": "Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];"
                }
        },
        "connectionSpec": {
            "id": "1fe283f6-9bec-11ea-bb37-0242ac130002",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `auth.params.connectionString` | [!DNL Couchbase] 계정에 연결하는 데 사용되는 연결 문자열입니다. 연결 문자열 패턴은 다음과 같습니다.`Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];` |
| `connectionSpec.id` | [!DNL Couchbase] 연결 사양 ID:`1fe283f6-9bec-11ea-bb37-0242ac130002`. |

**응답**

성공적인 응답은 해당 고유 식별자(`id`)를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "54997109-07b5-40b7-9971-0907b5a0b75a",
    "etag": "\"280168f5-0000-0200-0000-5ed72b230000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 [!DNL Couchbase] 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서는 [Flow Service API](../../explore/database-nosql.md)를 사용하여 데이터베이스를 탐색하는 방법을 배울 때 이 ID를 사용할 수 있습니다.
