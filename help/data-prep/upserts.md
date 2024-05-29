---
keywords: Experience Platform;홈;인기 항목;데이터 준비;데이터 준비;스트리밍;업데이트;스트리밍 업데이트
title: 데이터 준비를 사용하여 실시간 고객 프로필에 부분 행 업데이트 보내기
description: 데이터 준비를 사용하여 실시간 고객 프로필에 부분 행 업데이트를 보내는 방법을 알아봅니다.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 0%

---

# 부분 행 업데이트 보내기 대상 [!DNL Real-Time Customer Profile] 사용 [!DNL Data Prep]

>[!WARNING]
>
>DCS 인렛을 통한 프로필 업데이트를 위한 XDM(Experience Data Model) 엔티티 업데이트 메시지(JSON PATCH 작업 포함)에 대한 수집이 더 이상 사용되지 않습니다. 또는 다음을 수행할 수 있습니다. [원시 데이터를 DCS 인렛에 수집](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) 및 필요한 데이터 매핑을 지정하여 프로필 업데이트를 위한 XDM 호환 메시지로 데이터를 변환합니다.

에서 업데이트 스트리밍 [!DNL Data Prep] 부분 행 업데이트를 다음으로 보낼 수 있습니다. [!DNL Real-Time Customer Profile] 또한 단일 API 요청으로 새 ID 링크를 만들고 설정하는 동안 데이터가 수집됩니다.

업데이트를 스트리밍하면 해당 데이터를 로 번역하면서 데이터 형식을 유지할 수 있습니다 [!DNL Real-Time Customer Profile] 수집 중 PATCH 요청. 입력한 내용을 기반으로, [!DNL Data Prep] 을 사용하면 단일 API 페이로드를 전송하고 데이터를 두 페이로드로 번역할 수 있습니다 [!DNL Real-Time Customer Profile] PATCH 및 [!DNL Identity Service] 요청을 만듭니다.

>[!NOTE]
>
>업데이트 기능을 활용하려면 데이터 수집 중에 XDM 호환 구성을 끄고 를 사용하여 들어오는 페이로드를 다시 매핑하는 것이 좋습니다. [데이터 준비 매퍼](./ui/mapping.md).

이 문서는에서 업데이트를 스트리밍하는 방법에 대한 정보를 제공합니다 [!DNL Data Prep].

## 시작하기

이 개요를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] 데이터 엔지니어를 통해 XDM(Experience Data Model)과 데이터를 매핑, 변환 및 확인할 수 있습니다.
* [[!DNL Identity Service]](../identity-service/home.md): 디바이스와 시스템 간에 ID를 연결하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
* [실시간 고객 프로필](../profile/home.md): 여러 소스에서 집계한 데이터를 기반으로 통합 고객 프로필을 실시간으로 제공합니다.
* [소스](../sources/home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.

## 에서 스트리밍 업데이트 사용 [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>다음 소스는 스트리밍 업데이트 사용을 지원합니다.<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### 높은 수준의 워크플로 스트리밍 업데이트

에서 업데이트 스트리밍 [!DNL Data Prep] 는 다음과 같이 작동합니다.

* 먼저 데이터 세트를 만들고 활성화해야 합니다. [!DNL Profile] 소비. 다음 안내서를 참조하십시오 [데이터 세트 활성화 [!DNL Profile]](../catalog/datasets/enable-for-profile.md) 추가 정보.
* 새 ID를 연결해야 하는 경우 추가 데이터 세트도 만들어야 합니다 **동일한 스키마 사용** (으)로 [!DNL Profile] 데이터 세트.
* 데이터 세트가 준비되면 데이터 흐름을 만들어 수신 요청을 [!DNL Profile] 데이터 세트;
* 그런 다음 필요한 헤더를 포함하도록 수신 요청을 업데이트해야 합니다. 이러한 헤더는 다음을 정의합니다.
   * 를 수행해야 하는 데이터 작업입니다. [!DNL Profile]: `create`, `merge`, 및 `delete`.
   * 수행할 선택적 ID 작업 [!DNL Identity Service]: `create`.

### ID 데이터 세트 구성

새 ID를 연결해야 하는 경우 수신 페이로드에서 추가 데이터 세트를 만들고 전달해야 합니다. ID 데이터 세트를 생성할 때 다음 요구 사항이 충족되는지 확인해야 합니다.

* ID 데이터 세트에는 다음과 같이 연결된 스키마가 있어야 합니다. [!DNL Profile] 데이터 세트. 스키마가 일치하지 않으면 시스템 동작이 일관되지 않을 수 있습니다.
* 그러나 ID 데이터 세트가 [!DNL Profile] 데이터 세트. 데이터 세트가 동일한 경우 데이터가 업데이트되지 않고 덮어쓰기됩니다.
* 에 대해 초기 데이터 세트를 활성화해야 함 [!DNL Profile], id 데이터 세트 **활성화해서는 안 됨** 대상 [!DNL Profile]. 그렇지 않으면 데이터가 업데이트되지 않고 덮어쓰기됩니다. 그러나 ID 데이터 세트 **활성화해야 함** 대상 [!DNL Identity Service].

#### ID 데이터 세트와 연결된 스키마의 필수 필드 {#identity-dataset-required-fileds}

스키마에 필수 필드가 포함된 경우 활성화하려면 데이터 세트의 유효성 검사를 억제해야 합니다 [!DNL Identity Service] id만 받습니다. 다음을 적용하여 유효성 검사를 무시할 수 있습니다. `disabled` 에 대한 값 `acp_validationContext` 매개 변수. 아래 예를 참조하십시오.

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
| `flowId` | 데이터 흐름을 식별하는 고유 ID입니다. 이 데이터 흐름 ID는 로 만든 소스 연결에 해당해야 합니다. [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], 또는 [!DNL HTTP API]. 이 데이터 흐름에는 [!DNL Profile]-타겟 데이터 세트로 활성화된 데이터 세트. **참고**: 의 ID입니다 [!DNL Profile]-enabled target 데이터 세트는 `datasetId` 매개 변수. |
| `imsOrgId` | 조직에 해당하는 ID입니다. |
| `datasetId` | 의 ID [!DNL Profile]- 데이터 흐름의 대상 데이터 세트를 활성화했습니다. **참고**: 와 동일한 ID입니다. [!DNL Profile]-활성화된 대상 데이터 세트 ID가 데이터 흐름에 있습니다. |
| `operations` | 이 매개 변수는 다음과 같은 작업을 간략하게 설명합니다. [!DNL Data Prep] 은(는) 수신 요청을 기반으로 을(를) 수행합니다. |
| `operations.data` | 수행할 작업을 정의합니다. [!DNL Real-Time Customer Profile]. |
| `operations.identity` | 데이터에 대해 허용되는 작업을 다음 기준으로 정의합니다. [!DNL Identity Service]. |
| `operations.identityDatasetId` | (선택 사항) 새 ID를 연결해야 하는 경우에만 필요한 ID 데이터 세트의 ID입니다. |

#### 지원되는 작업

다음 작업은에서 지원됩니다. [!DNL Real-Time Customer Profile]:

| 작업 | 설명 |
| --- | --- | 
| `create` | 기본 작업입니다. 에 대한 XDM 엔티티 만들기 메서드를 생성합니다. [!DNL Real-Time Customer Profile]. |
| `merge` | 에 대한 XDM 엔티티 업데이트 메서드를 생성합니다. [!DNL Real-Time Customer Profile]. |
| `delete` | 에 대한 XDM 엔티티 삭제 메서드를 생성합니다. [!DNL Real-Time Customer Profile] 및 을(를) 통해 [!DNL Profile store]. |

다음 작업은에서 지원됩니다. [!DNL Identity Service]:

| 작업 | 설명 |
| --- | --- |
| `create` | 이 매개변수에 대해 허용되는 작업입니다. If `create` 의 값으로 전달됩니다. `operations.identity`, 그런 다음 [!DNL Data Prep] 에 대한 XDM 엔티티 만들기 요청을 생성합니다. [!DNL Identity Service]. ID가 이미 존재하는 경우 ID는 무시됩니다. **참고:** If `operations.identity` 이(가) (으)로 설정됨 `create`, 그런 다음 `identityDatasetId` 을(를) 지정해야 합니다. 에 의해 내부적으로 생성된 XDM 엔티티 생성 메시지 [!DNL Data Prep] 이 데이터 세트 id에 대한 구성 요소가 생성됩니다. |

### ID 구성이 없는 페이로드

새 ID를 연결할 필요가 없는 경우 `identity` 및 `identityDatasetId` 작업의 매개 변수. 이렇게 하면 데이터만 [!DNL Real-Time Customer Profile] 을 건너뛰고 [!DNL Identity Service]. 예를 보려면 아래 페이로드를 참조하십시오.

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

XDM 업데이트의 경우 스키마를 활성화해야 합니다. [!DNL Profile] 기본 id를 포함합니다. 다음 두 가지 방법으로 XDM 스키마의 기본 ID를 지정할 수 있습니다.

* XDM 스키마에서 정적 필드를 기본 ID로 지정합니다.
* XDM 스키마의 ID 맵 필드 그룹을 통해 ID 필드 중 하나를 기본 ID로 지정합니다.

### XDM 스키마에서 정적 필드를 기본 ID 필드로 지정

아래 예에서는 `state`, `homePhone.number` 및 기타 속성은 해당 지정된 값으로 다음에 업데이트됩니다. [!DNL Profile] 의 기본 ID 사용 `sampleEmail@gmail.com`. 그런 다음 XDM 엔티티 업데이트 메시지가 스트리밍에 의해 생성됩니다 [!DNL Data Prep] 구성 요소. [!DNL Real-Time Customer Profile] 그런 다음 프로필 레코드를 업데이트할 XDM 업데이트 메시지를 확인합니다.

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

이 예에서 헤더에는 `operations` 속성이 `identity` 및 `identityDatasetId` 속성. 이렇게 하면 데이터를 병합할 수 있습니다. [!DNL Real-Time Customer Profile] 및 로 전달될 ID에 대해서도 [!DNL Identity Service].

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

다음은 로 업데이트를 스트리밍할 때 고려할 알려진 제한 사항 목록을 간략하게 설명합니다. [!DNL Data Prep]:

* 부분 행 업데이트를 로 보낼 때만 스트리밍 업데이트 메서드를 사용해야 합니다. [!DNL Real-Time Customer Profile]. 부분 행 업데이트는 다음과 같습니다 **아님** 데이터 레이크에서 사용됨.
* 스트리밍 업데이트 메서드는 ID 업데이트, 바꾸기 및 제거를 지원하지 않습니다. 존재하지 않는 경우 새 ID가 생성됩니다. 따라서 `identity` 작업은 항상 만들도록 설정해야 합니다. ID가 이미 존재하는 경우 작업이 no-op입니다.
* 스트리밍 업데이트 방법은 현재 를 지원하지 않습니다. [Adobe Experience Platform 웹 SDK](/help/web-sdk/home.md) 및 [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/).

## 다음 단계

이제에서 업데이트를 스트리밍하는 방법을 이해할 수 있습니다 [!DNL Data Prep] 에 부분 행 업데이트를 보내려면 [!DNL Real-Time Customer Profile] 데이터를 캡처하는 동시에 단일 API 요청으로 ID를 만들고 연결합니다. 기타 정보 [!DNL Data Prep] 기능, 다음을 읽으십시오. [[!DNL Data Prep] 개요](./home.md). 내에서 매핑 세트를 사용하는 방법을 알아보려면 [!DNL Data Prep] API, 다음을 읽으십시오. [[!DNL Data Prep] 개발자 안내서](./api/overview.md).
