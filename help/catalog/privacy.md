---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Data Lake의 개인 정보 요청 처리
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# Data Lake의 개인 정보 요청 처리

Adobe Experience Platform Privacy Service는 GDPR(General Data Protection Regulation) 및 CCPA(California Consumer Privacy Act)와 같은 개인 정보 보호 규정에 따라 고객의 개인 정보에 대한 액세스, 거부 또는 삭제를 처리합니다.

이 문서에서는 Data Lake에 저장된 고객 데이터의 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.

## 시작하기

이 안내서를 읽기 전에 다음 Experience Platform 서비스에 대한 충분한 지식이 있는 것이 좋습니다.

* [개인 정보 서비스](../privacy-service/home.md):Adobe Experience Cloud 애플리케이션에서 개인 데이터를 액세스, 판매 거부 또는 삭제하기 위한 고객 요청을 관리합니다.
* [카탈로그 서비스](home.md):Adobe Experience Platform의 데이터 위치 및 계열에 대한 기록 시스템 데이터 집합 메타데이터를 업데이트하는 데 사용할 수 있는 API를 제공합니다.
* [XDM(Experience Data Model) 시스템](../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

## 데이터 세트에 개인 정보 레이블 추가 {#privacy-labels}

데이터 세트에 대한 개인 정보 보호 요청에서 데이터 세트를 처리하려면 데이터 세트에 개인 정보 보호 레이블이 지정되어 있어야 합니다. 개인 정보 보호 레이블은 데이터 세트의 관련 스키마 내에서 개인 정보 요청으로 전송될 네임스페이스에 적용되는 필드를 나타냅니다.

이 섹션에서는 Data Lake 개인 정보 보호 요청에 사용하기 위해 데이터 세트에 개인 정보 레이블을 추가하는 방법을 설명합니다. 시작하려면 다음 데이터 세트를 고려하십시오.

```json
{
    "5d8e9cf5872f18164763f971": {
        "name": "Loyalty Members",
        "description": "Dataset for the Loyalty Members schema",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "loyalty_members"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "id": "5d8e9cf5872f18164763f971",
        "dule": {
            "identity": [],
            "contract": [
                "C2",
                "C5"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C5"
            ],
            "identifiability": [],
            "specialTypes": []
        },
        "version": "1.0.2",
        "created": 1569627381749,
        "updated": 1569880723282,
        "createdClient": "acp_ui_platform",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "viewId": "5d8e9cf5872f18164763f972",
        "aspect": "production",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/5d8e9cf5872f18164763f971/views/5d8e9cf5872f18164763f972/files",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [
                {
                    "path": "/properties/personalEmail/properties/address",
                    "identity": [
                        "I1"
                    ],
                    "contract": [],
                    "sensitive": [],
                    "contracts": [],
                    "identifiability": [
                        "I1"
                    ],
                    "specialTypes": []
                }
            ],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

데이터 세트에 대한 `schemaMetadata` 속성에 현재 비어 있는 `gdpr` 배열이 포함되어 있습니다. 데이터 세트에 개인 정보 레이블을 추가하려면 카탈로그 서비스 API에 대한 패치 요청을 사용하여 이 [배열을 업데이트해야 합니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

>[!NOTE] 배열의 이름은 `gdpr`지정되지만 레이블을 추가하면 GDPR 및 CPA 규정 모두에 대한 개인 정보 작업 요청이 허용됩니다.

**API 형식**

```http
PATCH /dataSets/{DATASET_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 업데이트할 데이터 집합의 `id` 값입니다. |

**요청**

이 예에서는 데이터 세트에 `personalEmail.address` 필드에 이메일 주소가 포함되어 있습니다. 이 필드가 Data Lake 개인 정보 요청의 식별자 역할을 하려면 등록되지 않은 네임스페이스를 사용하는 레이블을 해당 `gdpr` 배열에 추가해야 합니다.

다음 요청은 `personalEmail.address` 필드에 &quot;email_label&quot; 네임스페이스를 지정하는 개인 정보 레이블을 추가합니다.

>[!IMPORTANT] 데이터 세트 `schemaMetadata` 속성에서 PATCH 작업을 실행할 때는 요청 페이로드 내에 있는 기존 하위 속성을 복사해야 합니다. 페이로드에서 기존 값을 제외하면 데이터 세트에서 해당 값이 제거됩니다.

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/catalog/dataSets/5d8e9cf5872f18164763f971' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{ 
    "schemaMetadata": { 
      "primaryKey": [],
      "delta": [],
      "dule": [
        {
          "path": "/properties/personalEmail/properties/address",
          "identity": [
              "I1"
          ],
          "contract": [],
          "sensitive": [],
          "contracts": [],
          "identifiability": [
              "I1"
          ],
          "specialTypes": []
        }
      ],
      "gdpr": [
          {
              "namespace": ["email_label"],
              "path": "/properties/personalEmail/properties/address"
          }
      ]
  }'
```

| 속성 | 설명 |
| --- | --- |
| `namespace` | 에 지정된 필드와 연결할 네임스페이스를 나열하는 `path`배열입니다. 네임스페이스는 개인정보 보호 서비스 API에서 액세스 [또는 삭제 요청을](#submit) 제출할 때 개인 정보 관련 필드를 식별하는 데 사용됩니다. |
| `path` | 데이터 세트에 적용되는 데이터 집합의 관련 스키마 내의 필드 경로입니다 `namespace`. 이상적으로, 개인 정보 레이블은 &quot;리프&quot; 필드(하위 필드가 없는 필드)에만 적용되어야 합니다. |

**응답**

성공적인 응답은 페이로드에 제공된 데이터 세트의 ID와 함께 HTTP 상태 200(OK)을 반환합니다. ID를 사용하여 데이터 세트를 다시 검색하면 개인 정보 레이블이 추가되었음을 알 수 있습니다.

```json
[
    "@/dataSets/5d8e9cf5872f18164763f971"
]
```

### 중첩된 맵 유형 필드 레이블 지정

개인정보 표시를 지원하지 않는 중첩 맵 유형 필드에는 두 가지가 있습니다.

* 배열 유형 필드 내의 맵 유형 필드
* 다른 맵 유형 필드 내의 맵 유형 필드

위의 두 예 중 하나에 대한 개인 정보 작업 처리가 결국 실패합니다. 이러한 이유로, 중첩된 맵 유형 필드를 사용하여 개인 고객 데이터를 저장하지 않는 것이 좋습니다. 관련 소비자 ID는 `identityMap` 필드(자체 지도 유형 필드) 내에 데이터 형식이 아닌 데이터 형식으로 저장되어 레코드 기반 데이터 집합 또는 시간 시리즈 기반 데이터 집합의 `endUserID` 필드로 저장해야 합니다.

## 요청 제출 {#submit}

>[!NOTE] 이 섹션에서는 Data Lake에 대한 개인 정보 요청의 형식을 지정하는 방법에 대해 설명합니다. Adobe에서는 Privacy Service API [또는 Privacy Service](../privacy-service/api/getting-started.md) UI [문서를 검토하여 요청 페이로드에서 제출된 사용자 ID 데이터의 형식을 적절하게 지정하는 방법을 포함하여 개인 정보](../privacy-service/ui/overview.md) 보호 작업을 제출하는 방법에 대한 전체 단계를 수행하는 것이 좋습니다.

다음 섹션에서는 Privacy Service API 또는 UI를 사용하여 Data Lake에 대한 개인정보 보호 요청을 수행하는 방법에 대해 설명합니다.

### API 사용

API에서 작업 요청을 만들 `userIDs` 때 제공된 모든 작업은 해당 작업이 적용되는 데이터 저장소에 `namespace` 따라 특정 `type` 및 를 사용해야 합니다. Data Lake의 ID는 해당 `type` 값에 &quot;등록되지 않음&quot;을 사용하고 해당 데이터 세트에 추가된 `namespace` 개인 정보 레이블과 [](#privacy-labels) 일치하는 값을 사용해야 합니다.

또한 요청 페이로드 `include` 배열에는 요청이 수행되는 여러 데이터 저장소에 대한 제품 값이 포함되어야 합니다. Data Lake에 대한 요청을 할 때 배열에 &quot;aepDataLake&quot; 값이 포함되어야 합니다.

다음 요청은 등록되지 않은 &quot;email_label&quot; 네임스페이스를 사용하여 Data Lake에 대한 새 개인 정보 작업을 만듭니다. 또한 `include` 배열에 있는 Data Lake의 제품 값도 포함합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

### UI 사용

UI에서 작업 요청을 만들 때는 **DataLake** 및/또는 **Profiles에서** AEP Data _Lake 및/또는 Profile을 선택하여_ Data Lake 또는 실시간 고객 프로파일에 저장된 데이터에 대한 작업을 각각 처리해야 합니다.

<img src="images/privacy/product-value.png" width="450"><br>

## 요청 처리 삭제

Experience Platform이 개인 정보 보호 서비스에서 삭제 요청을 받으면, 플랫폼은 요청을 수신했으며 영향을 받는 데이터는 삭제하도록 표시되었음을 개인 정보 보호 서비스에 확인을 보냅니다. 그러면 7일 이내에 Data Lake에서 레코드가 제거됩니다. 이 7일 기간 동안 데이터는 소프트 삭제되므로 플랫폼 서비스에서 액세스할 수 없습니다.

향후 릴리스에서는 데이터가 물리적으로 삭제된 후 Platform은 개인 정보 보호 서비스에 확인을 보냅니다.

## 다음 단계

이 문서를 읽음으로써 Data Lake의 개인 정보 보호 요청 처리와 관련된 중요한 개념을 도입했습니다. ID 데이터 관리 및 개인 정보 보호 작업 생성 방법에 대한 이해를 높이려면 이 안내서 전체에서 제공된 설명서를 계속 읽는 것이 좋습니다.

프로필 스토어에 대한 개인정보 보호 요청을 처리하는 단계는 실시간 고객 [프로필에](../profile/privacy.md) 대한 개인정보 보호 요청 처리에 관한 문서를 참조하십시오.