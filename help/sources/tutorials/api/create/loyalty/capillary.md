---
title: 흐름 서비스 API를 사용하여 Capillary를 Experience Platform에 연결
description: API를 사용하여 Capillary를 Experience Platform에 연결하는 방법을 알아봅니다.
badge: Beta
exl-id: 763792d0-d5dc-40ac-b86a-6a0d26463b71
source-git-commit: 91d6206c6ce387fde365fa72dc79ca79fc0e46fa
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 2%

---

# [!DNL Capillary Streaming Events] API를 사용하여 [!DNL Flow Service]을(를) Experience Platform에 연결

>[!AVAILABILITY]
>
>[!DNL Capillary Streaming Events] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 소스 개요에서 [약관](../../../../home.md#terms-and-conditions)을 참조하십시오.

[!DNL Capillary Streaming Events] 및 [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Capillary] 계정의 데이터를 Adobe Experience Platform으로 스트리밍하는 방법에 대해 알아보려면 이 안내서를 읽어 보십시오.

## 시작

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL Capillary Streaming Events] 개요](../../../../connectors/loyalty/capillary.md)를 읽어 보십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작하기](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

>[!BEGINSHADEBOX]

## 개발자 프로세스 체크리스트

1. 스키마 레지스트리를 사용하여 대상 **XDM(Experience Data Model) 스키마**&#x200B;를 만들거나 선택하십시오. 이 XDM 스키마를 사용하여 카탈로그 서비스에서 **데이터 집합을 만들기**&#x200B;하세요.
2. **자격 증명을 저장하려면**&#x200B;기본 연결[!DNL Capillary]을 만드십시오.
3. **에 바인딩할**&#x200B;소스 연결`baseConnectionId`을(를) 만듭니다.
4. 데이터가 데이터 레이크에 도달하는지 확인하려면 **대상 연결**&#x200B;을 만드십시오.
5. 데이터 준비를 사용하여 [!DNL Capillary] 소스 필드를 올바른 XDM 필드에 매핑하는 매핑을 만드십시오.
6. `sourceConnectionId`, `targetConnectionId` 및 `mappingID`을(를) 사용하여 데이터 흐름 만들기
7. 단일 샘플 프로필/트랜잭션 이벤트로 테스트하여 데이터 흐름을 확인하십시오.

>[!ENDSHADEBOX]

## 기본 연결 만들기 {#base-connection}

기본 연결은 자격 증명과 연결 세부 정보를 유지합니다. [!DNL Capillary]에 대한 기본 연결을 만들려면 `/connections` API의 [!DNL Flow Service] 끝점에 대한 POST 요청을 만들고 요청 본문에 [!DNL Capillary] 자격 증명을 제공하십시오.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Capillary]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary base connection",
    "description": "Base connection to authenticate the [!DNL Capillary] source.",
    "connectionSpec": {
      "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
      "version": "1.0"
    },
    "auth": {
      "specName": "OAuth generic-rest-connector",
      "params": {
        "clientId": "{CLIENT_ID}",
        "clientSecret": "{CLIENT_SECRET}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    }
  }'
```

**응답**

```
A successful response returns the newly created base connection, including its unique connection identifier (id). This ID is required to explore your source's file structure and contents in the next step.

{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### 소스 연결 만들기

원본 연결을 만들려면 기본 연결 ID를 제공하는 동안 `/sourceConnections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```http
POST /flowservice/sourceConnections
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Capillary Streaming",
      "description": "Capillary Streaming",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
          "version": "1.0"
      }
    }'
```

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 생성된 소스 연결에 대한 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

### 스키마 구성

>[!BEGINTABS]

>[!TAB 프로필 수집]

프로필에는 ID 및 충성도 속성이 포함되어 있습니다. [!DNL Capillary] 프로필 스키마를 기반으로 하는 예제에 대한 다음 페이로드를 확인합니다. 이 스키마를 구성하고 XDM 개인 프로필에 매핑할 수 있습니다.

**요청**

```json
{
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john.doe@capillarytech.com",
        "primary": true
      }
    ]
  },
  "loyalty": {
    "tier": "gold",
    "points": 1250,
    "lifetimePoints": 122,
    "expiredPoints": 12,
    "pointsRedeemed": 500,
    "program": "loyalty program name",
    "status": "active"
  }
}
```

**응답**

```json
{
  "id": "8c19f1c3-4b91-47cd-8cb5-b152a93f7349",
  "status": "success",
  "message": "Profile record ingested successfully"
}
```

>[!TAB 트랜잭션 수집]

거래는 상거래 활동을 캡처합니다. [!DNL Capillary] 이벤트 스키마를 기반으로 하는 예제에 대한 다음 페이로드를 확인합니다. 이 스키마를 구성하고 XDM 경험 이벤트에 매핑할 수 있습니다.

**요청**

```json
{
  "_id": "T0001",
  "timestamp": "2025-07-14T12:00:00-06:00",
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john@capillarytech.com",
        "primary": true
      }
    ]
  },
  "commerce": {
    "commerceScope": {
      "storeCode": "HSR"
    },
    "order": {
      "priceTotal": 90
    }
  },
  "productLineItems": [
    {
      "SKU": "sku_01",
      "quantity": 1,
      "priceTotal": 100,
      "name": "Kitkat",
      "discountAmount": 10
    }
  ]
}
```

**응답**

```json
{
  "id": "T0001",
  "status": "success",
  "message": "Transaction event ingested successfully"
}
```

>[!ENDTABS]

<!--### Supported Events

The [!DNL Capillary] source supports the following events:

* `pointsIssued`
* `tierDowngraded`
* `tierUpgraded`
* `pointsExpiryChange`
* `pointsExpired`
* `transactionUpdated`
* `customerAdded`
* `tierDowngradeReminder`
* `promotionEarned`
* `pointsExpiryReminder`
* `pointsRedeemed`
* `transactionAdded`
* `tierRenewed`
* `customerUpdated`-->

### 이전 데이터 마이그레이션

과거 충성도 및 거래 데이터를 Experience Platform으로 가져올 수 있습니다. 데이터를 [!DNL Capillary]에서 구조화된 CSV 파일로 내보내고 [!DNL SFTP]을(를) 사용하여 안전하게 전송한 다음 Experience Platform 데이터 세트로 수집하면 됩니다. 초기 마이그레이션 후에는 이벤트 기반 커넥터를 통해 데이터가 실시간으로 최신 상태로 유지됩니다.

### 대상 XDM 스키마 만들기 {#target-schema}

XDM(경험 데이터 모델) 스키마는 Experience Platform 내에서 고객 경험 데이터를 구성하고 설명하는 표준화된 방법을 제공합니다. 소스 데이터를 Experience Platform에 수집하려면 먼저 수집하려는 데이터의 구조와 유형을 정의하는 대상 XDM 스키마를 만들어야 합니다. 이 스키마는 수집된 데이터가 위치할 Experience Platform 데이터 세트에 대한 블루프린트 역할을 합니다.

[스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)에 대한 POST 요청을 수행하여 대상 XDM 스키마를 만들 수 있습니다. 대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 다음 안내서를 참조하십시오.

* [API를 사용하여 스키마를 만듭니다](../../../../../xdm/api/schemas.md).
* [UI를 사용하여 스키마를 만듭니다](../../../../../xdm/tutorials/create-schema-ui.md).

만든 후에는 대상 데이터 세트 및 매핑에 대상 XDM 스키마 `$id`이(가) 필요합니다.

## 타겟 데이터 세트 만들기 {#target-dataset}

데이터 집합은 일반적으로 열(스키마) 및 행(필드)이 있는 테이블처럼 구성된 데이터 수집을 위한 저장 및 관리 구성입니다. Experience Platform에 성공적으로 수집된 데이터는 데이터 세트로 데이터 레이크 내에 저장됩니다. 이 단계에서는 새 데이터 세트를 만들거나 기존 데이터 세트를 사용할 수 있습니다.

페이로드 내에 대상 스키마의 ID를 제공하면서 [카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/)에 대한 POST 요청을 하여 대상 데이터 집합을 만들 수 있습니다. 대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../../../catalog/api/create-dataset.md)에 대한 안내서를 참조하십시오.


## 대상 연결 만들기 {#target}

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크와 연결된 고정 연결 사양 ID를 제공해야 합니다. 이 연결 사양 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`입니다.

**API 형식**

```http
POST /targetConnections
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Capillary Target Connection",
      "description": "Capillary Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

### 매핑 만들기 {#mapping}

그런 다음 소스 데이터를 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑합니다. 매핑을 만들려면 `mappingSets`API[[!DNL Data Prep] 의 ](https://developer.adobe.com/experience-platform-apis/references/data-prep/) 끝점에 대한 POST 요청을 만듭니다. 대상 XDM 스키마 ID와 만들려는 매핑 세트에 대한 세부 사항을 포함합니다.

다음과 같이 모세관 필드를 해당 XDM 스키마 필드에 매핑합니다.

| 소스 스키마 | 대상 스키마 |
|------------------------------|-------------------------------|
| `identityMap.email.id` | `xdm:identityMap.email[0].id` |
| `loyalty.points` | `xdm:loyalty.points` |
| `loyalty.tier` | `xdm:loyalty.tier` |
| `commerce.order.priceTotal` | `xdm:commerce.order.priceTotal` |
| `productLineItems.SKU` | `xdm:productListItems.SKU` |

>[!TIP]
>
>데이터를 매핑할 준비가 되면 [ 및 ](../../../../images/tutorials/create/capillary/mappings.zip)데이터 준비로 파일 가져오기[!DNL Capillary]에 대한 [이벤트 및 프로필 매핑](../../../../../data-prep/ui/mapping.md#import-mapping)을 다운로드할 수 있습니다.

### 데이터 흐름 만들기 {#flow}

소스 연결, 매핑 및 대상 연결을 만든 후 데이터를 [!DNL Capillary]에서 Experience Platform으로 이동하도록 데이터 흐름을 구성할 수 있습니다.

일반적인 데이터 흐름은 다음과 같습니다.

* **프로필 데이터 흐름**: [!DNL Capillary] 프로필 데이터를 XDM 개별 프로필 데이터 세트에 수집합니다.
* **트랜잭션 데이터 흐름**: [!DNL Capillary] 트랜잭션 데이터를 XDM ExperienceEvent 데이터 세트로 수집합니다.

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary dataflow",
    "description": "Capillary → Experience Platform dataflow",
    "flowSpec": {
      "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "version": "1.0"
    },
    "sourceConnectionIds": "{SOURCE_CONNECTION_ID}",
    "targetConnectionIds": "{TARGET_CONNECTION_ID}",
    "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "{MAPPING_ID}",
          "mappingVersion": "0"
        }
      }
    ],
    "scheduleParams": {
      "startTime": "1625040887",
      "frequency": "minute",
      "interval": 15
    }
  }'
```

>[!NOTE]
>
>`startTime`은(는) UNIX Epoch 초입니다.

**응답**

성공적인 응답은 해당 데이터 흐름 ID와 함께 데이터 흐름을 반환합니다.

```json
{
  "id": "92f11b8c-0a9f-45a9-8239-60b4e8430a88",
  "status": "enabled",
  "message": "Dataflow created successfully"
}
```

## 오류 처리

커넥터에는 다음 시나리오에 대한 강력한 오류 처리가 포함되어 있습니다.

* **인증 오류**: 인증이 실패하면 Adobe 자격 증명을 자동으로 새로 고칩니다.
* **속도 제한 오류**: API 속도 제한에 도달하면 지수 백오프를 사용하여 다시 시도를 구현합니다.
* **네트워크 오류**: 네트워크 요청에 실패한 로그 및 다시 시도.
* **데이터 유효성 검사 오류**: 수동 검토 및 해결에 대해 잘못된 페이로드를 기록합니다.

모든 오류는 문제 해결 및 디버깅을 용이하게 하기 위해 오류 유형, 타임스탬프, 요청 페이로드 및 Adobe API 응답과 같은 세부 정보로 기록됩니다.

## 연결 테스트

아래 단계에 따라 연결을 테스트하기 위해 수행할 수 있는 단계를 알아보십시오.

* `/connections/{BASE_CONNECTION_ID}`에 GET을 요청하고 기본 연결 ID를 제공하여 기본 연결이 있는지 확인하십시오. 이 단계에서는 기본 연결 상태가 `active`(으)로 설정되어 있는지 확인할 수도 있습니다.
* `/flowservice/sourceConnections/{SOURCE_CONNECTION_ID}`에 GET을 요청하고 원본 연결 ID를 제공하여 원본 연결을 확인하세요.
* 스트리밍 끝점 URL을 사용하여 샘플 프로필 페이로드를 보냅니다(프로필 수집 JSON 사용).
* Experience Platform UI에서 데이터 세트로 이동하고 데이터 세트에 대한 쿼리를 실행하여 레코드를 확인합니다.
* 데이터 준비 로그를 사용하여 오류를 검사합니다.
* 지원 티켓을 열어야 하는 경우, 다음 사항이 있는지 확인하십시오.
   * 경로 페이로드
   * 응답 본문
   * Request-id
   * 타임스탬프
   * 리소스 ID.

## 부록

추가 작업에 대한 안내서는 다음 설명서를 참조하십시오

* [데이터 흐름 모니터링](../../../../../dataflows/ui/monitor-sources.md)
* [데이터 흐름 업데이트](../../../ui/update-dataflows.md)
* [데이터 흐름 삭제](../../../ui/delete.md)
* [소스 계정 업데이트](../../../ui/update.md)
