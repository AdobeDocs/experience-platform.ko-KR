---
keywords: Experience Platform;홈;인기 항목;데이터 준비;데이터 준비;스트리밍;업데이트;스트리밍 업데이트
title: 데이터 준비를 사용하여 실시간 고객 프로필에 부분 행 업데이트 보내기
description: 데이터 준비를 사용하여 실시간 고객 프로필에 부분 행 업데이트를 보내는 방법을 알아봅니다.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---

# [!DNL Data Prep]을(를) 사용하여 [!DNL Real-Time Customer Profile]에 부분 행 업데이트 보내기

>[!IMPORTANT]
>
>* DCS 인렛을 통한 프로필 업데이트를 위한 XDM(Experience Data Model) 엔티티 업데이트 메시지(JSON PATCH 작업 포함) 수집은 더 이상 사용되지 않습니다. 이 안내서에 요약된 단계를 대신 따르십시오.
>
>* HTTP API 원본을 사용하여 [원시 데이터를 DCS 인렛으로 수집](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection)하고 필요한 데이터 매핑을 지정하여 프로필 업데이트를 위한 XDM 호환 메시지로 데이터를 변환할 수도 있습니다.
>
>* 스트리밍 업데이트에 배열을 사용하는 경우 명시적으로 `upsert_array_append` 또는 `upsert_array_replace`을(를) 사용하여 작업의 명확한 의도를 정의해야 합니다. 이러한 기능이 누락된 경우 오류가 발생할 수 있습니다.

단일 API 요청으로 새 ID 링크를 만들고 설정하는 동안 [!DNL Data Prep]에서 스트리밍 업데이트를 사용하여 [!DNL Real-Time Customer Profile] 데이터에 부분 행 업데이트를 보냅니다.

업데이트 스트리밍을 사용하면 수집 중에 해당 데이터를 [!DNL Real-Time Customer Profile]개의 PATCH 요청으로 변환하는 동안 데이터 형식을 유지할 수 있습니다. 제공한 입력을 기반으로 [!DNL Data Prep]을(를) 사용하면 단일 API 페이로드를 전송하고 데이터를 [!DNL Real-Time Customer Profile] PATCH 및 [!DNL Identity Service] CREATE 요청으로 변환할 수 있습니다.

[!DNL Data Prep]은(는) 헤더 매개 변수를 사용하여 삽입과 업데이트를 구별합니다. 업데이트를 사용하는 모든 행에는 헤더가 있어야 합니다. ID 설명자가 있거나 없는 업데이트를 사용할 수 있습니다. ID와 함께 업데이트를 사용하는 경우 [ID 데이터 집합 구성](#configure-the-identity-dataset)의 섹션에 설명된 구성 단계를 따라야 합니다. ID 없이 업데이트를 사용하는 경우 요청에 ID 구성을 제공할 필요가 없습니다. 자세한 내용은 [ID가 없는 업데이트 스트리밍](#payload-without-identity-configuration)의 섹션을 참조하십시오.

>[!NOTE]
>
>업데이트 기능을 활용하려면 데이터를 수집하는 동안 XDM 호환 구성을 끄고 [데이터 준비 매퍼](./ui/mapping.md)를 사용하여 들어오는 페이로드를 다시 매핑하는 것이 좋습니다.

이 문서에서는 [!DNL Data Prep]에서 업데이트를 스트리밍하는 방법에 대한 정보를 제공합니다.

## 시작하기

이 개요를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep]을(를) 통해 데이터 엔지니어는 데이터를 XDM(Experience Data Model)에 매핑하고, 변환하고, 유효성을 검사할 수 있습니다.
* [[!DNL Identity Service]](../identity-service/home.md): 장치 및 시스템 간에 ID를 연결하여 개별 고객 및 개별 고객의 행동을 더 잘 볼 수 있습니다.
* [실시간 고객 프로필](../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 실시간으로 통합된 고객 프로필을 제공합니다.
* [소스](../sources/home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.

## [!DNL Data Prep]에서 스트리밍 업데이트 사용 {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>다음 소스는 스트리밍 업데이트 사용을 지원합니다.<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### 높은 수준의 워크플로 스트리밍 업데이트

[!DNL Data Prep]의 스트리밍 업데이트는 다음과 같이 작동합니다.

* 먼저 [!DNL Profile] 사용에 대한 데이터 세트를 만들고 활성화해야 합니다. 자세한 내용은 [데이터 집합 활성화 [!DNL Profile]](../catalog/datasets/enable-for-profile.md)에 대한 안내서를 참조하십시오.
* 새 ID를 연결해야 하는 경우 [!DNL Profile] 데이터 세트와 동일한 스키마를 사용하여 **추가 데이터 세트를 만들어야 합니다**.
* 데이터 세트가 준비되면 들어오는 요청을 [!DNL Profile] 데이터 세트에 매핑할 데이터 흐름을 만들어야 합니다.
* 그런 다음 필요한 헤더를 포함하도록 수신 요청을 업데이트해야 합니다. 이러한 헤더는 다음을 정의합니다.
   * [!DNL Profile]&#x200B;(으)로 수행해야 하는 데이터 작업: `create`, `merge` 및 `delete`.
   * [!DNL Identity Service]&#x200B;(으)로 수행할 선택적 ID 작업: `create`.

### ID 데이터 세트 구성 {#configure-the-identity-dataset}

새 ID를 연결해야 하는 경우 수신 페이로드에서 추가 데이터 세트를 만들고 전달해야 합니다. ID 데이터 세트를 생성할 때 다음 요구 사항이 충족되는지 확인해야 합니다.

* ID 데이터 집합에는 [!DNL Profile] 데이터 집합과 연결된 스키마가 있어야 합니다. 스키마가 일치하지 않으면 시스템 동작이 일관되지 않을 수 있습니다.
* 그러나 ID 데이터 세트가 [!DNL Profile] 데이터 세트와 다른지 확인해야 합니다. 데이터 세트가 동일한 경우 데이터가 업데이트되지 않고 덮어쓰기됩니다.
* [!DNL Profile]에 대해 초기 데이터 세트를 활성화해야 하지만 [!DNL Profile]에 대해 ID 데이터 세트 **을(를) 활성화해서는 안 됩니다**. 그렇지 않으면 데이터가 업데이트되지 않고 덮어쓰기됩니다. 그러나 [!DNL Identity Service]에 대해 ID 데이터 세트 **을(를) 사용**&#x200B;해야 합니다.

#### ID 데이터 세트와 연결된 스키마의 필수 필드 {#identity-dataset-required-fileds}

스키마에 필수 필드가 포함된 경우 [!DNL Identity Service]이(가) ID만 받도록 하려면 데이터 집합의 유효성 검사를 억제해야 합니다. `acp_validationContext` 매개 변수에 `disabled` 값을 적용하여 유효성 검사를 표시하지 않을 수 있습니다. 아래 예를 참조하십시오.

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags": {
        "acp_validationContext": [
            "disabled"
        ],
        "unifiedProfile": [
            "enabled:false"
        ],
        "unifiedIdentity": [
            "enabled:true"
        ]
    }
}'
```

>[!TIP]
>
>ID 데이터 세트와 연결된 스키마에 필수 필드가 없는 경우 추가 구성을 수행할 필요가 없습니다.

## 들어오는 페이로드 구조

다음은 새 ID 링크를 설정하는 수신 페이로드 구조의 예를 보여 줍니다.

### ID 구성을 포함한 페이로드

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| 매개변수 | 설명 |
| --- | --- |
| `flowId` | 데이터 흐름을 식별하는 고유 ID입니다. 이 데이터 흐름 ID는 [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] 또는 [!DNL HTTP API]&#x200B;(으)로 만들어진 원본 연결에 해당해야 합니다. 이 데이터 흐름에는 [!DNL Profile]이(가) 활성화된 데이터 집합도 대상 데이터 집합으로 있어야 합니다. **참고**: [!DNL Profile] 사용 대상 데이터 집합의 ID가 `datasetId` 매개 변수로도 사용됩니다. |
| `imsOrgId` | 조직에 해당하는 ID입니다. |
| `datasetId` | 데이터 흐름의 [!DNL Profile] 사용 대상 데이터 세트의 ID입니다. **참고**: 이 ID는 데이터 흐름에서 찾은 [!DNL Profile] 사용 대상 데이터 세트 ID와 동일합니다. |
| `operations` | 이 매개 변수는 [!DNL Data Prep]이(가) 들어오는 요청을 기반으로 수행할 작업에 대해 간략하게 설명합니다. |
| `operations.data` | [!DNL Real-Time Customer Profile]에서 수행해야 하는 작업을 정의합니다. |
| `operations.identity` | [!DNL Identity Service]이(가) 데이터에 대해 허용하는 작업을 정의합니다. |
| `operations.identityDatasetId` | (선택 사항) 새 ID를 연결해야 하는 경우에만 필요한 ID 데이터 세트의 ID입니다. |

#### 지원되는 작업

[!DNL Real-Time Customer Profile]에서 다음 작업을 지원합니다.

| 작업 | 설명 |
| --- | --- | 
| `create` | 기본 작업입니다. [!DNL Real-Time Customer Profile]에 대한 XDM 엔터티 만들기 메서드를 생성합니다. |
| `merge` | [!DNL Real-Time Customer Profile]에 대한 XDM 엔터티 업데이트 메서드를 생성합니다. |
| `delete` | [!DNL Real-Time Customer Profile]에 대한 XDM 엔터티 삭제 메서드를 생성하고 [!DNL Profile store]에서 데이터를 영구적으로 제거합니다. |

[!DNL Identity Service]에서 다음 작업을 지원합니다.

| 작업 | 설명 |
| --- | --- |
| `create` | 이 매개변수에 대해 허용되는 작업입니다. `create`이(가) `operations.identity`의 값으로 전달되면 [!DNL Data Prep]이(가) [!DNL Identity Service]에 대한 XDM 엔터티 만들기 요청을 생성합니다. ID가 이미 존재하는 경우 ID는 무시됩니다. **참고:** `operations.identity`이(가) `create`(으)로 설정된 경우 `identityDatasetId`도 지정해야 합니다. [!DNL Data Prep] 구성 요소에서 내부적으로 생성한 XDM 엔터티 만들기 메시지가 이 데이터 세트 ID에 대해 생성됩니다. |

### ID 구성이 없는 페이로드 {#payload-without-identity-configuration}

새 ID를 연결할 필요가 없는 경우 작업에서 `identity` 및 `identityDatasetId` 매개 변수를 생략할 수 있습니다. [!DNL Real-Time Customer Profile]에만 데이터를 보내고 [!DNL Identity Service]을(를) 건너뜁니다. 예를 보려면 아래 페이로드를 참조하십시오.

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## 기본 ID 동적으로 전달

XDM 업데이트의 경우 [!DNL Profile]에 대해 스키마를 사용하도록 설정하고 기본 ID를 포함해야 합니다. 다음 두 가지 방법으로 XDM 스키마의 기본 ID를 지정할 수 있습니다.

* XDM 스키마에서 정적 필드를 기본 ID로 지정합니다.
* XDM 스키마의 ID 맵 필드 그룹을 통해 ID 필드 중 하나를 기본 ID로 지정합니다.

### XDM 스키마에서 정적 필드를 기본 ID 필드로 지정

아래 예에서 `state`, `homePhone.number` 및 기타 특성은 지정된 각각의 값으로 `sampleEmail@gmail.com`의 기본 ID를 사용하여 [!DNL Profile]에 업데이트됩니다. 그런 다음 스트리밍 [!DNL Data Prep] 구성 요소에서 XDM 엔티티 업데이트 메시지를 생성합니다. [!DNL Real-Time Customer Profile]에서 프로필 레코드를 업데이트할 XDM 업데이트 메시지를 확인합니다.

>[!NOTE]
>
>이 예제에서는 ID에 대해 정의된 작업이 없으므로 ID가 함께 연결되지 않습니다.

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### XDM 스키마의 ID 맵 필드 그룹을 통해 ID 필드 중 하나를 기본 ID로 지정

이 예제에서는 헤더에 `identity` 및 `identityDatasetId` 속성이 있는 `operations` 특성이 포함되어 있습니다. 이렇게 하면 데이터를 [!DNL Real-Time Customer Profile]과(와) 병합하고 ID를 [!DNL Identity Service]에 전달할 수 있습니다.

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## 알려진 제한 사항 및 주요 고려 사항

다음은 [!DNL Data Prep]을(를) 사용하여 업데이트를 스트리밍할 때 고려해야 할 알려진 제한 사항 목록을 간략하게 설명합니다.

* 부분 행 업데이트를 [!DNL Real-Time Customer Profile]&#x200B;(으)로 보낼 때만 스트리밍 업데이트 메서드를 사용해야 합니다. 데이터 레이크에서 부분 행 업데이트를 **사용하지 않음**&#x200B;합니다.
* 스트리밍 업데이트 메서드는 ID 업데이트, 바꾸기 및 제거를 지원하지 않습니다. 존재하지 않는 경우 새 ID가 생성됩니다. 따라서 `identity` 작업은 항상 만들도록 설정해야 합니다. ID가 이미 존재하는 경우 작업이 no-op입니다.
* 스트리밍 업데이트 방법은 현재 [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) 및 [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)을 지원하지 않습니다.

## 다음 단계

이 문서를 읽은 후에는 단일 API 요청으로 ID를 만들고 연결하는 동시에 [!DNL Data Prep]에서 업데이트를 스트리밍하여 [!DNL Real-Time Customer Profile] 데이터에 부분 행 업데이트를 전송하는 방법을 이해해야 합니다. 다른 [!DNL Data Prep] 기능에 대한 자세한 내용은 [[!DNL Data Prep] 개요](./home.md)를 참조하십시오. [!DNL Data Prep] API 내에서 매핑 세트를 사용하는 방법에 대해 알아보려면 [[!DNL Data Prep] 개발자 안내서](./api/overview.md)를 참조하십시오.
