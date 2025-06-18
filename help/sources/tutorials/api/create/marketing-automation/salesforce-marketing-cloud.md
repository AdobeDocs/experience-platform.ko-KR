---
title: 흐름 서비스 API를 사용하여 Salesforce Marketing Cloud을 Experience Platform에 연결
description: API를 사용하여 Salesforce Marketing Cloud 계정을 Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud] 원본은 2026년 1월에 사용되지 않습니다. 대안으로 새로운 정보원이 올해 말 공개될 것이다. 새 소스가 릴리스되면 2026년 1월 말 이전에 새 계정 연결 및 데이터 흐름을 생성하여 새 소스로 마이그레이션할 계획이어야 합니다.

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Salesforce Marketing Cloud] 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Azure Synapse Analytics]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.


### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Salesforce Marketing Cloud]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL Salesforce Marketing Cloud] 인증 개요](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md)를 읽어 보십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작하기](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## [!DNL Azure]에서 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결

기본 연결을 만들고 [!DNL Salesforce Marketing Cloud] 계정을 [!DNL Azure]의 Experience Platform에 연결하는 방법을 알아보려면 다음을 참조하세요.

### 기본 연결 만들기 {#azure-base}

>[!IMPORTANT]
>
>사용자 지정 개체 수집은 현재 [!DNL Salesforce Marketing Cloud] 원본 통합에서 지원되지 않습니다.

**기본 연결**&#x200B;은(는) 소스 시스템을 Adobe Experience Platform에 연결하는 키 정보를 저장합니다. 여기에는 다음 항목이 포함되어 있습니다.

* 소스의 인증 자격 증명
* 현재 연결 상태
* 고유 **기본 연결 ID**

**기본 연결 ID**&#x200B;을(를) 사용하면 소스에서 파일을 탐색하고 탐색할 수 있으므로 데이터 형식 및 형식과 함께 수집할 항목을 식별하는 데 도움이 됩니다.

기본 연결 ID를 만들려면 요청 매개 변수에 [!DNL Salesforce Marketing Cloud] 인증 자격 증명을 포함하여 `/connections` 끝점에 POST 요청을 보냅니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Salesforce Marketing Cloud]에 대한 기본 연결을 만듭니다.

+++예제 요청 보기

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for Azure",
    "description": "Salesforce Marketing Cloud base connection for Azure",
    "auth": {
      "specName": "Client-Id-Secret Based Authentication",
      "params": {
        "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst",
        "clientId": "acme-salesforce-marketing-cloud",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.host` |
| `auth.params.clientId` | [!DNL Salesforce Marketing Cloud] 응용 프로그램과 연결된 클라이언트 ID입니다. |
| `auth.params.clientSecret` | [!DNL Salesforce Marketing Cloud] 응용 프로그램과 연결된 클라이언트 암호입니다. |
| `connectionSpec.id` | [!DNL Salesforce Marketing Cloud] 연결 사양 ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

+++

+++예제 응답 보기

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

## Amazon Web Services에서 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../../../landing/multi-cloud.md)를 참조하세요.

[!DNL Salesforce Marketing Cloud] 계정을 AWS의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하십시오.

### 기본 연결 만들기 {#aws-base}

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Salesforce Service Cloud]이(가) AWS의 Experience Platform에 연결할 수 있는 기본 연결을 만듭니다.

+++요청 보기 예

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for AWS",
    "description": "Salesforce Marketing Cloud base connection for AWS",
    "auth": {
      "specName": "OAuth2 Client Credential",
      "params": {
        "subdomain": "mc563885gzs27c5t9-63k636ttgm",
        "clientId": "3a1b2c3d4e5f67890123456789abcdef",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

+++

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다.

+++응답 보기 예

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


## [!DNL Salesforce Marketing Cloud] 데이터에 대한 데이터 흐름 만들기

[!DNL Salesforce Marketing Cloud] 계정을 연결했으므로 이제 [데이터 흐름을 만들고 마케팅 자동화 공급자에서 Experience Platform으로 데이터를 수집](../../collect/marketing-automation.md)할 수 있습니다.