---
keywords: Experience Platform;홈;인기 항목;데이터 준비;데이터 준비;스트리밍;업로드;스트리밍 업그레이드
title: 데이터 준비를 사용하여 프로필 서비스에 부분 행 업데이트 보내기
description: 이 문서에서는 데이터 준비를 사용하여 프로필 서비스에 부분 행 업데이트를 보내는 방법에 대한 정보를 제공합니다.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: cc3ecbd8544839246d54f72b894ad27e850c0c90
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---

# 부분 행 업데이트를 로 보내기 [!DNL Profile Service] 사용 [!DNL Data Prep]

의 스트리밍 업데이트 [!DNL Data Prep] 부분 행 업데이트를 [!DNL Profile Service] 또한 단일 API 요청으로 새 id 링크를 만들고 설정하는 동안 데이터를 생성할 수 있습니다.

스트리밍 업사이트를 통해 해당 데이터를 로 번역하는 동안 데이터 형식을 유지할 수 있습니다 [!DNL Profile Service] PATCH 요청 을 수집 중입니다. 입력한 내용에 따라 [!DNL Data Prep] 단일 API 페이로드를 전송하고 데이터를 두 API 모두로 변환할 수 있습니다 [!DNL Profile Service] PATCH 및 [!DNL Identity Service] 요청을 만듭니다.

이 문서에서는 의 업스트림을 스트리밍하는 방법에 대한 정보를 제공합니다 [!DNL Data Prep].

## 시작하기

이 개요를 사용하려면 다음 Adobe Experience Platform 구성 요소를 이해할 수 있어야 합니다.

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.
* [[!DNL Identity Service]](../identity-service/home.md): 여러 장치와 시스템에서 ID를 브리징하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
* [실시간 고객 프로필](../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 실시간으로 통합 고객 프로필을 제공합니다.
* [소스](../sources/home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.

## 에서 스트리밍 업데이트 사용 [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>다음 소스는 스트리밍 업스트림 사용을 지원합니다.<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### 스트리밍 업스트림 고급 워크플로우

의 스트리밍 업데이트 [!DNL Data Prep] 는 다음과 같이 작동합니다.

* 먼저 데이터 세트를 만들고 활성화해야 합니다 [!DNL Profile] 소비. 다음 안내서를 참조하십시오. [데이터 집합 활성화 [!DNL Profile]](../catalog/datasets/enable-for-profile.md) 추가 정보
* 새 ID를 연결해야 하는 경우 추가 데이터 집합도 만들어야 합니다 **동일한 스키마 사용** 로서의 [!DNL Profile] 데이터 세트;
* 데이터 세트가 준비되면 들어오는 요청을 데이터 흐름을 만들어 [!DNL Profile] 데이터 세트;
* 다음으로, 필요한 헤더를 포함하도록 수신 요청을 업데이트해야 합니다. 이러한 헤더는 다음을 정의합니다.
   * 을 사용하여 수행해야 하는 데이터 작업 [!DNL Profile]: `create`, `merge`, 및 `delete`;
   * 사용할 선택적 ID 작업 [!DNL Identity Service]: `create`.

### ID 데이터 세트 구성

새 ID를 연결해야 하는 경우 들어오는 페이로드에서 추가 데이터 세트를 만들고 전달해야 합니다. ID 데이터 세트를 만들 때 다음 요구 사항이 충족되는지 확인해야 합니다.

* ID 데이터 세트에는 와(과) 연결된 스키마가 있어야 합니다. [!DNL Profile] 데이터 세트. 스키마가 일치하지 않으면 시스템 동작이 일관되지 않을 수 있습니다.
* 그러나 ID 데이터 세트가 [!DNL Profile] 데이터 세트. 데이터 세트가 동일한 경우 업데이트된 대신 데이터를 덮어씁니다.
* 반면에 초기 데이터 세트에 대해 를 활성화해야 합니다 [!DNL Profile], id 데이터 세트 **다음을 해서는 안 됩니다** 다음 기간 동안 활성화됨 [!DNL Profile]. 그렇지 않으면 업데이트된 대신 데이터를 덮어씁니다.

#### ID 데이터 세트와 연결된 스키마의 필수 필드 {#identity-dataset-required-fileds}

스키마에 필수 필드가 포함되어 있는 경우, 활성화하려면 데이터 집합에 대한 유효성 검사를 억제해야 합니다 [!DNL Identity Service] ID만 수신 를 적용하여 유효성 검사를 억제할 수 있습니다 `disabled` 값 `acp_validationContext` 매개 변수. 아래 예를 참조하십시오.

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags":{
        "acp_validationContext": ["disabled"]
        }
}'
```

>[!TIP]
>
>ID 데이터 세트와 연결된 스키마에 필수 필드가 없는 경우 추가 구성을 수행하지 않아도 됩니다.

## 들어오는 페이로드 구조

다음은 새 ID 링크를 설정하는 들어오는 페이로드 구조의 예를 표시합니다.

### ID 구성이 있는 페이로드

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

| 매개 변수 | 설명 |
| --- | --- |
| `flowId` | 데이터 흐름을 식별하는 고유 ID입니다. 이 데이터 흐름 ID는 [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], 또는 [!DNL HTTP API]. 이 데이터 흐름에는 [!DNL Profile]-활성화된 데이터 세트를 target 데이터 세트로 사용합니다. **참고**: 의 ID입니다 [!DNL Profile]-활성화된 target 데이터 집합도 `datasetId` 매개 변수. |
| `imsOrgId` | 조직에 해당하는 ID입니다. |
| `datasetId` | 의 ID입니다 [!DNL Profile]-데이터 흐름의 대상 데이터 집합을 활성화했습니다. **참고**: ID와 동일합니다 [!DNL Profile]-활성화된 target 데이터 세트 ID가 데이터 플로우에 있습니다. |
| `operations` | 이 매개 변수는 [!DNL Data Prep] 은 들어오는 요청을 기반으로 합니다. |
| `operations.data` | 에서 수행해야 하는 작업을 정의합니다 [!DNL Profile Service]. |
| `operations.identity` | 데이터에서 허용되는 작업을 [!DNL Identity Service]. |
| `operations.identityDatasetId` | (선택 사항) 새 ID를 연결해야 하는 경우에만 필요한 ID 데이터 세트의 ID입니다. |

#### 지원되는 작업

다음 작업은 [!DNL Profile Service]:

| 작업 | 설명 |
| --- | --- | 
| `create` | 기본 작업입니다. 이에 대한 XDM 엔티티 생성 방법이 생성됩니다 [!DNL Profile Service]. |
| `merge` | 이에 대한 XDM 엔티티 업데이트 방법이 생성됩니다 [!DNL Profile Service]. |
| `delete` | 이에 대한 XDM 엔티티 삭제 방법이 생성됩니다 [!DNL Profile Service] 에서 데이터를 영구적으로 제거 [!DNL Profile Store]. |

다음 작업은 [!DNL Identity Service]:

| 작업 | 설명 |
| --- | --- |
| `create` | 이 매개 변수에 대해 허용되는 유일한 작업입니다. If `create` 에 대한 값으로 전달됩니다. `operations.identity`, 그런 다음 [!DNL Data Prep] 에 대한 XDM 엔티티 생성 요청을 생성합니다. [!DNL Identity Service]. ID가 이미 있으면 ID가 무시됩니다. **참고:** If `operations.identity` 가 로 설정되어 있습니다. `create`, 그런 다음 `identityDatasetId` 을 지정해야 합니다. XDM 엔티티가 내부적으로 생성된 메시지를 만듭니다. [!DNL Data Prep] 이 데이터 세트 id에 대한 구성 요소가 생성됩니다. |

### ID 구성이 없는 페이로드

새 ID를 연결할 필요가 없는 경우 `identity` 및 `identityDatasetId` 매개 변수를 사용하여 작업할 수 있습니다. 이렇게 하면 데이터만 [!DNL Profile Service] 및 는 를 건너뜁니다. [!DNL Identity Service]. 예를 보려면 아래 페이로드를 참조하십시오.

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

## 기본 ID를 동적으로 전달

XDM 업데이트의 경우 스키마를 [!DNL Profile] 에는 기본 ID가 들어 있습니다. XDM 스키마의 기본 ID를 두 가지 방법으로 지정할 수 있습니다.

* 정적 필드를 XDM 스키마의 기본 ID로 지정합니다.
* XDM 스키마의 ID 맵 필드 그룹을 통해 ID 필드 중 하나를 기본 ID로 지정합니다.

### 정적 필드를 XDM 스키마의 기본 ID 필드로 지정합니다

아래 예에서는 `state`, `homePhone.number` 및 다른 속성은 지정된 값과 함께 [!DNL Profile] 의 `sampleEmail@gmail.com`. 그런 다음 스트리밍에 의해 XDM 엔티티 업데이트 메시지가 생성됩니다 [!DNL Data Prep] 구성 요소. [!DNL Profile Service] 그런 다음 XDM 업데이트 메시지가 프로필 레코드를 업데이트하는지 확인합니다.

>[!NOTE]
>
>이 예에서 ID에 대해 정의된 작업이 없으므로 ID가 함께 연결되어 있지 않습니다.

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

### XDM 스키마의 ID 맵 필드 그룹을 통해 ID 필드 중 하나를 기본 ID로 지정합니다

이 예에서 헤더에는 `operations` 속성을 `identity` 및 `identityDatasetId` 속성을 사용합니다. 이렇게 하면 데이터를 [!DNL Profile Service] 그리고 또한 [!DNL Identity Service].

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

다음은 업데이트를 스트리밍할 때 고려해야 하는 알려진 제한 사항 목록을 간략하게 설명합니다 [!DNL Data Prep]:

* 스트리밍 업데이트 메서드는 부분 행 업데이트를 [!DNL Profile Service]. 부분 행 업데이트는 다음과 같습니다 **not** data lake에서 소비합니다.
* 스트리밍 업데이트 메서드는 ID 업데이트, 교체 및 제거를 지원하지 않습니다. 새 ID가 없는 경우 만들어집니다. 따라서 `identity` 작업은 항상 생성하도록 설정해야 합니다. ID가 이미 존재하는 경우 작업은 작업이 아닙니다.
* 스트리밍 업데이트 메서드는 현재 기본 단일 값 속성(예: 정수, 날짜, 타임스탬프 및 문자열)과 개체만 지원합니다.
* 현재 스트리밍 업데이트 메서드가 지원되지 않습니다 [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=en) 및 [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/).

## 다음 단계

이 문서를 읽은 후에는 업스트림을 스트리밍하는 방법을 이해할 수 있어야 합니다 [!DNL Data Prep] 부분 행 업데이트를 로 보내려면 [!DNL Profile Service] 데이터를 생성할 수도 있고 단일 API 요청으로 id를 생성 및 연결할 수도 있습니다. 기타 정보 [!DNL Data Prep] 기능, [[!DNL Data Prep] 개요](./home.md). 내에서 매핑 세트를 사용하는 방법을 알아보려면 [!DNL Data Prep] API입니다. [[!DNL Data Prep] 개발자 안내서](./api/overview.md).
