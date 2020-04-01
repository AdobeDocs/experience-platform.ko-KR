---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: API를 사용하여 데이터 내보내기
topic: tutorial
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# API를 사용하여 프로필 데이터 내보내기

실시간 고객 프로파일을 사용하면 속성 데이터와 행동 데이터를 비롯한 다양한 소스에서 데이터를 취합하여 개별 고객에 대한 단일 뷰를 구축할 수 있습니다. 그런 다음 프로파일 내에서 사용할 수 있는 데이터를 데이터 세트에 내보내 추가로 처리할 수 있습니다. 이 자습서에서는 세그멘테이션 API를 사용하여 내보내기 작업을 만들고 관리하기 위한 단계별 [지침을 제공합니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

내보내기 작업을 만드는 것 외에도 프로필 액세스 API와 예상치를 사용하여 프로필 데이터에 액세스할 수도 있습니다. 이러한 다른 액세스 패턴에 [대한 자세한 내용은 프로필 액세스 API 자습서](../../profile/api/entities.md) 또는 에지 대상 및 예상 [](../../profile/api/edge-projections.md) 구성 자습서를참조하십시오.

## 시작하기

이 자습서에서는 프로필 데이터 작업과 관련된 다양한 Adobe Experience Platform 서비스에 대해 제대로 이해해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [실시간 고객 프로필](../../profile/home.md):다양한 소스의 데이터를 집계하여 실시간으로 통합된 고객 프로파일을 제공합니다.
- [Adobe Experience Platform 세그멘테이션 서비스](../home.md):실시간 고객 프로필 데이터를 통해 고객 세그먼트를 만들 수 있습니다.
- [XDM(Experience Data Model)](../../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [샌드박스](../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필수 헤더

또한 이 자습서에서는 플랫폼 API를 성공적으로 호출하려면 [인증 자습서를](../../tutorials/authentication.md) 완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 내보내기 작업 만들기

프로필 데이터를 내보내려면 먼저 데이터를 내보낼 데이터 세트를 만든 다음 새 내보내기 작업을 시작해야 합니다. 이러한 두 단계 모두 Experience Platform API를 사용하여 수행할 수 있으며, 이전 단계는 Catalog Service API를 사용하고, 이전 단계는 Real-time Customer Profile API를 사용하여 수행할 수 있습니다. 각 단계를 완료하기 위한 자세한 지침은 다음 섹션에 요약되어 있습니다.

- [대상 데이터 집합](#create-a-target-dataset) 만들기 - 내보낸 데이터를 저장할 데이터 집합을 만듭니다.
- [새 내보내기 작업](#initiate-export-job) 시작 - 데이터 세트를 XDM 개별 프로필 데이터로 채웁니다.

### 타겟 데이터 세트 만들기

프로필 데이터를 내보낼 때 먼저 대상 데이터 세트를 만들어야 합니다. 데이터 세트를 올바르게 구성하여 내보내기가 제대로 수행되도록 해야 합니다.

중요한 고려 사항 중 하나는 데이터 세트가 기반으로 하는 스키마입니다(`schemaRef.id` 아래 API 샘플 요청에서). 세그먼트를 내보내려면 데이터 집합이 XDM 개인 프로필 조합 스키마(`https://ns.adobe.com/xdm/context/profile__union`)를 기반으로 해야 합니다. 공용 스키마는 XDM 개별 프로필 클래스인 동일한 클래스를 공유하는 스키마 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다. 결합 보기 스키마에 대한 자세한 내용은 스키마 레지스트리 [개발자 안내서의](../../xdm/schema/composition.md#union)실시간 고객 프로필 섹션을 참조하십시오.

이 튜토리얼의 다음 단계에서는 카탈로그 API를 사용하여 XDM 개별 프로필 조합 스키마를 참조하는 데이터 세트를 만드는 방법에 대해 간략하게 설명합니다. 또한 Adobe Experience Platform 사용자 인터페이스를 사용하여 공용 스키마를 참조하는 데이터 집합을 만들 수 있습니다. UI를 사용하기 위한 단계는 [이 UI 튜토리얼에서 세그먼트](./create-dataset-export-segment.md) 내보내기를 위한 지침을 따르지만 여기에 적용할 수도 있습니다. 완료되면 이 튜토리얼로 돌아가 새 내보내기 작업을 [시작하는](#initiate-export-job)단계를 계속 진행할 수 있습니다.

이미 호환되는 데이터 세트가 있고 ID를 알고 있는 경우 새 내보내기 작업을 [시작하는](#initiate-export-job)단계로 직접 진행할 수 있습니다.

**API 형식**

```http
POST /dataSets
```

**요청**

다음 요청은 페이로드에 구성 매개 변수를 제공하여 새 데이터 세트를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        },
        "fileDescription": {
          "persisted": true,
          "containerFormat": "parquet",
          "format": "parquet"
        },
        "aspect": "production"
      }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 데이터 세트에 대한 설명 이름입니다. |
| `schemaRef.id` | 데이터 집합에 연결할 통합 보기(스키마)의 ID입니다. |
| `fileDescription.persisted` | 로 설정되면 `true`통합 보기에서 데이터 세트가 유지될 수 있도록 하는 부울 값입니다. |

**응답**

성공적인 응답은 새로 만든 데이터 세트에 대한 읽기 전용, 시스템 생성, 고유 ID가 포함된 배열을 반환합니다. 프로필 데이터를 성공적으로 내보내려면 제대로 구성된 데이터 집합 ID가 필요합니다.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 내보내기 작업 시작

결합 지속 데이터 세트를 가지고 있으면 실시간 고객 프로필 API의 `/export/jobs` 끝점에 대한 POST 요청을 만들고 요청 본문에 내보낼 데이터의 세부 정보를 제공하여 프로필 데이터를 데이터 세트에 유지하는 내보내기 작업을 만들 수 있습니다.

**API 형식**

```http
POST /export/jobs
```

**요청**

다음 요청은 페이로드에 구성 매개 변수를 제공하는 새 내보내기 작업을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `fields` | *(선택 사항)* 내보내기에 포함할 데이터 필드를 이 매개 변수에 제공된 필드로만 제한합니다. 세그먼트를 만들 때도 동일한 매개 변수를 사용할 수 있으므로 세그먼트의 필드가 이미 필터링되었을 수 있습니다. 이 값을 생략하면 내보낸 데이터에 모든 필드가 포함됩니다. |
| `mergePolicy` | *(선택 사항)* 내보낸 데이터를 제어하는 병합 정책을 지정합니다. 내보낼 세그먼트가 여러 개 있을 경우 이 매개 변수를 포함하십시오. 이 값을 생략하면 Export Service가 세그먼트에서 제공하는 병합 정책을 사용하게 됩니다. |
| `mergePolicy.id` | 병합 정책의 ID입니다. |
| `mergePolicy.version` | 사용할 병합 정책의 특정 버전입니다. 이 값을 생략하면 기본적으로 최신 버전이 사용됩니다. |
| `filter` | *(선택 사항)* 내보내기 전에 세그먼트에 적용할 다음 필터 중 하나 이상을 지정합니다. |
| `filter.segments` | *(선택 사항)* 내보낼 세그먼트를 지정합니다. 이 값을 생략하면 모든 프로필의 모든 데이터가 내보내집니다. 다음 필드를 포함하는 세그먼트 개체의 배열을 수락합니다.<ul><li>`segmentId`: **(사용하는 경우`segments`필수)** 내보낼 프로필에 대한 세그먼트 ID입니다.</li><li>`segmentNs` ( *선택 사항)* 주어진 세그먼트 `segmentID`네임스페이스입니다.</li><li>`status` ( *선택 사항)* 에 대한 상태 필터를 제공하는 문자열 `segmentID`배열입니다. 기본적으로 `status` 는 현재 시간에 세그먼트에 속하는 모든 프로파일을 나타내는 값을 `["realized", "existing"]` 가집니다. 가능한 값은 다음과 같습니다. `"realized"`및 `"existing"`를 `"exited"`참조하십시오.</br></br>자세한 내용은 세그먼트 [만들기 자습서를](./create-a-segment.md)참조하십시오.</li></ul> |
| `filter.segmentQualificationTime` | *(선택 사항)* 세그먼트 자격 조건 시간을 기반으로 필터링합니다. 시작 시간 및/또는 종료 시간을 제공할 수 있습니다. |
| `filter.segmentQualificationTime.startTime` | *(선택 사항)* 주어진 상태에 대한 세그먼트 ID에 대한 세그먼트 자격 시작 시간입니다. 제공되지 않으며 세그먼트 ID 자격에 대한 시작 시간에 필터가 없습니다. 타임스탬프는 RFC 3339 [형식으로 제공되어야 합니다](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(선택 사항)* 주어진 상태에 대한 세그먼트 ID에 대한 세그먼트 자격 종료 시간입니다. 제공되지 않으며 세그먼트 ID 자격 부여의 종료 시간에 필터가 없습니다. 타임스탬프는 RFC 3339 [형식으로 제공되어야 합니다](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp ` | *(선택 사항)* 내보낸 프로필을 이 타임스탬프 이후에 업데이트된 프로필만 포함하도록 제한합니다. 타임스탬프는 RFC 3339 [형식으로 제공되어야 합니다](https://tools.ietf.org/html/rfc3339) . <ul><li>`fromIngestTimestamp` for **profiles**, if provided:병합된 업데이트된 타임스탬프가 지정된 타임스탬프보다 큰 병합된 프로필을 모두 포함합니다. 피연산자를 `greater_than` 지원합니다.</li><li>`fromTimestamp` for **events**:이 타임스탬프 이후에 인제스트된 모든 이벤트는 결과 프로필 결과에 따라 내보내집니다. 이벤트 시간 자체가 아니라 이벤트에 대한 수집 시간입니다.</li> |
| `filter.emptyProfiles` | *(선택 사항)* 부울 값. 프로필에는 프로필 레코드, ExperienceEvent 레코드 또는 둘 다를 포함할 수 있습니다. 프로필 레코드가 없고 ExperienceEvent 레코드만 있는 프로필을 &quot;emptyProfiles&quot;라고 합니다. &quot;emptyProfiles&quot;를 포함하여 프로필 저장소에서 모든 프로필을 내보내려면 `emptyProfiles` 의 값을 `true`로 설정합니다. 로 `emptyProfiles` 설정하면 `false`저장소에 프로필 레코드가 있는 프로필만 내보내집니다. 기본적으로 속성이 포함되지 않은 경우 `emptyProfiles` 프로필 레코드가 포함된 프로파일만 내보내집니다. |
| `additionalFields.eventList` | *(선택 사항)* 다음 설정 중 하나 이상을 제공하여 하위 또는 관련 개체에 대해 내보낸 시계열 이벤트 필드를 제어합니다.<ul><li>`eventList.fields`:내보낼 필드를 제어합니다.</li><li>`eventList.filter`:관련 개체에서 포함된 결과를 제한하는 기준을 지정합니다. 내보내기에 필요한 최소 값(일반적으로 날짜)이 필요합니다.</li><li>`eventList.filter.fromIngestTimestamp`:제공된 타임스탬프 이후에 인제스트된 이벤트까지 시간 시리즈 이벤트를 필터링합니다. 이벤트 시간 자체가 아니라 이벤트에 대한 수집 시간입니다.</li></ul> |
| `destination` | **(필수)** 내보낸 데이터의 대상 정보:<ul><li>`destination.datasetId`:(필수) **** 데이터를 내보낼 데이터 집합의 ID입니다.</li><li>`destination.segmentPerBatch`:( *선택 사항)* 제공되지 않을 경우 기본적으로 를 사용하는 부울 값입니다 `false`. 값이 모든 세그먼트 ID를 단일 배치 ID로 `false` 내보냅니다. 한 세그먼트 ID를 하나의 배치 ID로 `true` 내보내는 값입니다. 값을 설정할 경우 일괄 내보내기 성능에 영향을 줄 `true` 수 있습니다.</li></ul> |
| `schema.name` | **(필수)** 데이터를 내보낼 데이터 세트와 연결된 스키마의 이름입니다. |

>[!NOTE] 관련 ExperienceEvent 데이터를 포함하지 않고 프로필 데이터만 내보내려면 요청에서 &quot;additionalFields&quot; 개체를 제거합니다.

**응답**

성공적인 응답은 요청에 지정된 대로 프로필 데이터로 채워진 데이터 세트를 반환합니다.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

요청에 포함되지 `destination.segmentPerBatch` 않았거나(없을 경우, 기본값이 `false`으로 설정됨), 또는 값이 로 설정된 경우 위의 응답에 있는 `false`개체에 `destination` 배열이 없고, 대신 아래에 표시된 것처럼 하나의 `batches` `batchId`배열만 포함됩니다. 이 단일 배치에는 모든 세그먼트 ID가 포함되는 반면 위의 응답에는 배치 ID당 단일 세그먼트 ID가 표시됩니다.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

## 모든 내보내기 작업 나열

특정 IMS에 대한 모든 내보내기 작업 목록을 `export/jobs` 끝점에 GET 요청을 수행하여 반환할 수 있습니다. 또한 요청은 쿼리 매개 변수를 `limit` 지원하며 `offset`아래와 같이 지원합니다.

**API 형식**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| 속성 | 설명 |
| -------- | ----------- |
| `limit` | 반환할 레코드 수를 지정합니다. |
| `offset` | 제공된 번호로 반환할 결과 페이지를 오프셋합니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

응답에는 IMS 조직에서 만든 내보내기 작업이 포함된 `records` 개체가 포함됩니다.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## 내보내기 진행 상태 모니터링

특정 내보내기 작업의 세부 사항을 보거나 진행 상태를 모니터링하려면 `/export/jobs` 종단점에 GET 요청을 만들고 내보내기 작업의 `id` 내용을 경로에 포함할 수 있습니다. 필드가 &quot;SUCCESS&quot; 값을 반환하면 내보내기 작업이 `status` 완료됩니다.

**API 형식**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 액세스하려는 내보내기 `id` 작업 |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `batchId` | 프로필 데이터를 읽을 때 조회 목적으로 사용할 성공적인 내보내기에서 생성된 배치의 식별자입니다. |

## 내보내기 작업 취소

Experience Platform을 사용하면 기존 내보내기 작업을 취소할 수 있습니다. 이 작업은 내보내기 작업이 완료되지 않았거나 처리 단계에 갇혀 있는지 등 여러 가지 이유로 유용할 수 있습니다. 내보내기 작업을 취소하려면 `/export/jobs` 끝점에 대한 DELETE 요청을 수행하고 요청 경로로 취소할 내보내기 작업의 `id` 내용을 포함할 수 있습니다.

**API 형식**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 액세스하려는 내보내기 `id` 작업 |

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

삭제 요청이 성공하면 HTTP 상태 204(콘텐츠 없음) 및 빈 응답 본문을 반환하며, 이는 취소 작업이 성공했음을 나타냅니다.

## 다음 단계

내보내기가 성공적으로 완료되면 Experience Platform의 Data Lake 내에서 데이터를 사용할 수 있습니다. 그런 다음 데이터 액세스 [API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) 사용하여 내보내기와 `batchId` 연결된 데이터를 사용하여 데이터에 액세스할 수 있습니다. 내보내기 크기에 따라 데이터가 청크 단위일 수 있으며 일괄 처리는 여러 파일로 구성될 수 있습니다.

데이터 액세스 API를 사용하여 배치 파일에 액세스하고 다운로드하는 방법에 대한 단계별 지침을 보려면 데이터 액세스 [자습서를](../../data-access/tutorials/dataset-data.md)따르십시오.

또한 Adobe Experience Platform 쿼리 서비스를 사용하여 성공적으로 내보낸 실시간 고객 프로필 데이터에 액세스할 수 있습니다. UI 또는 RESTful API를 사용하여 쿼리 서비스를 사용하여 데이터 레이크 내의 데이터에 대한 쿼리를 작성, 유효성 확인 및 실행할 수 있습니다.

대상 데이터를 쿼리하는 방법에 대한 자세한 내용은 쿼리 서비스 [설명서를](../../query-service/home.md)참조하십시오.