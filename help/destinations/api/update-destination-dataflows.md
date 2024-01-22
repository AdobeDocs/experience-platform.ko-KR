---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;대상 데이터 흐름 업데이트
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 대상 데이터 흐름 업데이트
type: Tutorial
description: 이 튜토리얼에서는 대상 데이터 흐름을 업데이트하는 단계를 설명합니다. 흐름 서비스 API를 사용하여 데이터 흐름을 활성화 또는 비활성화하거나, 기본 정보를 업데이트하거나, 대상 및 속성을 추가 및 제거하는 방법을 알아봅니다.
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: c1d4a0586111d9cd8a66f4239f67f2f7e6ac8633
workflow-type: tm+mt
source-wordcount: '2404'
ht-degree: 3%

---

# 흐름 서비스 API를 사용하여 대상 데이터 흐름 업데이트

이 튜토리얼에서는 대상 데이터 흐름을 업데이트하는 단계를 설명합니다. 다음을 사용하여 데이터 흐름을 활성화 또는 비활성화하거나, 기본 정보를 업데이트하거나, 대상 및 속성을 추가 및 제거하는 방법에 대해 알아봅니다. [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Experience Platform UI를 사용하여 대상 데이터 흐름을 편집하는 방법에 대한 자세한 내용은 [활성화 플로우 편집](/help/destinations/ui/edit-activation.md).

## 시작하기 {#get-started}

이 자습서를 사용하려면 유효한 흐름 ID가 있어야 합니다. 유효한 흐름 ID가 없는 경우 [대상 카탈로그](../catalog/overview.md) 다음에 설명된 단계를 수행합니다. [대상에 연결](../ui/connect-destination.md) 및 [데이터 활성화](../ui/activation-overview.md) 이 자습서를 시도하기 전에.

>[!NOTE]
>
> 용어 *흐름* 및 *데이터 흐름* 는 이 자습서에서 서로 교환하여 사용할 수 있습니다. 이 자습서의 컨텍스트에서 은 동일한 의미를 갖습니다.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [대상](../home.md): [!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
* [샌드박스](../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 다음을 사용하여 데이터 흐름을 성공적으로 업데이트하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Flow Service] API.

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 참조하십시오.

### 필수 헤더에 대한 값 수집 {#gather-values-for-required-headers}

Platform API를 호출하려면 먼저 다음을 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더의 값이 제공됩니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform에 속한 리소스를 포함한 모든 리소스 [!DNL Flow Service]는 특정 가상 샌드박스로 분리됩니다. Platform API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>다음과 같은 경우 `x-sandbox-name` 헤더가 지정되지 않았습니다. 요청은에서 확인됩니다. `prod` 샌드박스.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 데이터 흐름 세부 정보 조회 {#look-up-dataflow-details}

대상 데이터 흐름을 업데이트하는 첫 번째 단계는 흐름 ID를 사용하여 데이터 흐름 세부 정보를 검색하는 것입니다. 에 GET 요청을 하여 기존 데이터 흐름의 현재 세부 정보를 볼 수 있습니다. `/flows` 엔드포인트.

**API 형식**

```http
GET /flows/{FLOW_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 고유 `id` 검색할 대상 데이터 흐름의 값입니다. |

**요청**

다음 요청은 플로우 ID와 관련된 정보를 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 버전, 고유 식별자( )를 포함하여 데이터 흐름의 현재 세부 정보를 반환합니다.`id`) 및 기타 관련 정보.

```json
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            {
               "name":"GeneralTransform",
               "params":{
                  "profileSelectors":{
                     "selectors":[
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"Email",
                              "operator":"EXISTS",
                              "identity":{
                                 "namespace":"Email"
                              },
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"Email",
                                 "destination":"Email",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"Email",
                                 "destinationXdmPath":"Email"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.firstName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.firstName",
                                 "destination":"person.name.firstName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.firstName",
                                 "destinationXdmPath":"person.name.firstName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.lastName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.lastName",
                                 "destination":"person.name.lastName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.lastName",
                                 "destinationXdmPath":"person.name.lastName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"personalEmail.address",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"personalEmail.address",
                                 "destination":"personalEmail.address",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"personalEmail.address",
                                 "destinationXdmPath":"personalEmail.address"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"segmentMembership.status",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"segmentMembership.status",
                                 "destination":"segmentMembership.status",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"segmentMembership.status",
                                 "destinationXdmPath":"segmentMembership.status"
                              }
                           }
                        }
                     ],
                     "mandatoryFields":[
                        "Email",
                        "person.name.firstName",
                        "person.name.lastName"
                     ],
                     "primaryFields":[
                        {
                           "identityNamespace":"Email",
                           "fieldType":"IDENTITY"
                        }
                     ]
                  },
                  "segmentSelectors":{
                     "selectors":[
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                              "name":"Interested in Mountain Biking",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"ONCE",
                                 "startDate":"2021-12-25",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"f52a3785-2e7c-40a7-8137-9be99af7794e",
                              "name":"Birth year 1970",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"6caa79b9-39e0-4c37-892b-5061cdca2377",
                              "name":"Account Leads",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
                              "name":"Batch export for autumn campaign",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"EVERY_6_HOURS",
                                 "startDate":"2022-01-05",
                                 "endDate":"2022-12-30",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        }
                     ]
                  }
               }
            }
         ]
      }
   ]
```

## 데이터 흐름 이름 및 설명 업데이트 {#update-dataflow}

데이터 흐름의 이름과 설명을 업데이트하려면에 대한 PATCH 요청을 수행합니다 [!DNL Flow Service] 흐름 ID, 버전 및 사용할 새 값을 제공하는 동안 API입니다.

>[!IMPORTANT]
>
>다음 `If-Match` PATCH 요청을 할 때 헤더가 필요합니다. 이 헤더의 값은 업데이트하려는 데이터 흐름의 고유 버전입니다. 데이터 흐름이 성공적으로 업데이트될 때마다 etag 값이 업데이트됩니다.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

다음 요청은 데이터 흐름의 이름과 설명을 업데이트합니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/name",
                "value": "2021/2022 winter campaign"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "ACME company holiday campaign for high fidelity customers and prospects"
            }
        ]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 흐름 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] 흐름 ID를 제공하는 동안 API입니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 데이터 흐름 활성화 또는 비활성화 {#enable-disable-dataflow}

활성화되면 데이터 흐름이 프로필을 대상으로 내보냅니다. 데이터 흐름은 기본적으로 활성화되어 있지만, 프로필 내보내기를 일시 중지하기 위해 비활성화할 수 있습니다.

에 POST 요청을 하여 기존 대상 데이터 흐름을 활성화하거나 비활성화할 수 있습니다. [!DNL Flow Service] 플로우를 업데이트할 API 및 제공 상태입니다.

**API 형식**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**요청**

다음 요청은 데이터 흐름의 상태를 활성화됨으로 업데이트합니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

다음 요청은 데이터 흐름의 상태를 비활성화로 업데이트합니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 흐름 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] 흐름 ID를 제공하는 동안 API입니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 데이터 흐름에 대상 추가 {#add-segment}

대상 데이터 흐름에 대상을 추가하려면 대상에 대한 PATCH 요청을 수행합니다 [!DNL Flow Service] 흐름 ID, 버전 및 추가하려는 대상을 제공하는 동안 API입니다.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

다음 요청은 기존 대상 데이터 흐름에 새 대상을 추가합니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"add",
      "path":"/transformations/0/params/segmentSelectors/selectors/-",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"2d79d0d8-724f-49fc-a09d-d1dec338c93c",
            "name":"Winter 2021/2022 campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%SEGMENT_NAME%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"DAILY_FULL_EXPORT",
            "schedule":{
               "startDate":"2022-01-05",
               "frequency":"DAILY",
               "triggerType": "AFTER_SEGMENT_EVAL",
               "endDate":"2022-03-10"
            }
         }
      }
   }
]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. 데이터 흐름에 대상을 추가하려면 `add` 작업. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. 데이터 흐름에 대상을 추가할 때는 예제에 지정된 경로를 사용하십시오. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |
| `id` | 대상 데이터 흐름에 추가할 대상자의 ID를 지정합니다. |
| `name` | **(선택 사항)**. 대상 데이터 흐름에 추가할 대상자의 이름을 지정합니다. 이 필드는 필수가 아니므로 이름을 제공하지 않고 대상 데이터 흐름에 대상을 성공적으로 추가할 수 있습니다. |
| `filenameTemplate` | 대상 *일괄 처리 대상* 만 해당. 이 필드는 Amazon S3, SFTP 또는 Azure Blob와 같은 배치 파일 내보내기 대상의 데이터 흐름에 대상을 추가할 때만 필요합니다. <br> 이 필드는 대상으로 내보내는 파일의 파일 이름 형식을 결정합니다. <br> 다음 옵션을 사용할 수 있습니다. <br> <ul><li>`%DESTINATION_NAME%`: 필수입니다. 내보낸 파일에는 대상 이름이 포함되어 있습니다.</li><li>`%SEGMENT_ID%`: 필수입니다. 내보낸 파일에는 내보낸 대상자의 ID가 들어 있습니다.</li><li>`%SEGMENT_NAME%`: **(선택 사항)**. 내보낸 파일에는 내보낸 대상자의 이름이 포함됩니다.</li><li>`DATETIME(YYYYMMdd_HHmmss)` 또는 `%TIMESTAMP%`: **(선택 사항)**. 다음 두 옵션 중 하나를 선택하여 Experience Platform으로 생성된 시간을 파일에 포함합니다.</li><li>`custom-text`: **(선택 사항)**. 이 자리 표시자를 파일 이름 끝에 추가할 사용자 지정 텍스트로 바꿉니다.</li></ul> <br> 파일 이름 구성에 대한 자세한 내용은 [파일 이름 구성](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 배치 대상 활성화 자습서의 섹션입니다. |
| `exportMode` | 대상 *일괄 처리 대상* 만 해당. 이 필드는 Amazon S3, SFTP 또는 Azure Blob와 같은 배치 파일 내보내기 대상의 데이터 흐름에 대상을 추가할 때만 필요합니다. <br> 필수. 선택 `"DAILY_FULL_EXPORT"` 또는 `"FIRST_FULL_THEN_INCREMENTAL"`. 두 옵션에 대한 자세한 내용은 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 배치 대상 활성화 자습서에서 다음을 수행합니다. |
| `startDate` | 대상자가 대상으로 프로필 내보내기를 시작할 날짜를 선택합니다. |
| `frequency` | 대상 *일괄 처리 대상* 만 해당. 이 필드는 Amazon S3, SFTP 또는 Azure Blob와 같은 배치 파일 내보내기 대상의 데이터 흐름에 대상을 추가할 때만 필요합니다. <br> 필수. <br> <ul><li>의 경우 `"DAILY_FULL_EXPORT"` 내보내기 모드에서 다음을 선택할 수 있습니다. `ONCE` 또는 `DAILY`.</li><li>의 경우 `"FIRST_FULL_THEN_INCREMENTAL"` 내보내기 모드에서 다음을 선택할 수 있습니다. `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | 대상 *일괄 처리 대상* 만 해당. 이 필드는 을(를) 선택할 때만 필요합니다. `"DAILY_FULL_EXPORT"` 의 모드 `frequency` 선택기. <br> 필수. <br> <ul><li>선택 `"AFTER_SEGMENT_EVAL"` 매일 플랫폼 일괄 처리 세분화 작업이 완료된 후 즉시 활성화 작업을 실행하도록 합니다. 이렇게 하면 활성화 작업이 실행될 때 가장 최신 프로필을 대상으로 내보냅니다.</li><li>선택 `"SCHEDULED"` 고정된 시간에 활성화 작업을 실행합니다. 이렇게 하면 Experience Platform 프로필 데이터를 매일 동시에 내보낼 수 있지만 활성화 작업이 시작되기 전에 배치 세분화 작업이 완료되었는지 여부에 따라 내보내는 프로필이 최신 프로필이 아닐 수 있습니다. 이 옵션을 선택할 때는 `startTime` 일별 내보내기가 발생하는 시간을 UTC로 표시합니다.</li></ul> |
| `endDate` | 대상 *일괄 처리 대상* 만 해당. 이 필드는 Amazon S3, SFTP 또는 Azure Blob와 같은 배치 파일 내보내기 대상의 데이터 흐름에 대상을 추가할 때만 필요합니다. <br> 선택 시 적용할 수 없음 `"exportMode":"DAILY_FULL_EXPORT"` 및 `"frequency":"ONCE"`. <br> 대상 구성원의 대상 내보내기를 중지할 날짜를 설정합니다. |
| `startTime` | 대상 *일괄 처리 대상* 만 해당. 이 필드는 Amazon S3, SFTP 또는 Azure Blob와 같은 배치 파일 내보내기 대상의 데이터 흐름에 대상을 추가할 때만 필요합니다. <br> 필수. 대상자의 멤버가 포함된 파일을 생성하여 대상으로 내보내야 하는 시간을 선택합니다. |

**응답**

성공적인 응답은 흐름 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] 흐름 ID를 제공하는 동안 API입니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 데이터 흐름에서 대상자 제거 {#remove-segment}

기존 대상 데이터 흐름에서 대상을 제거하려면 대상에 대한 PATCH 요청을 수행합니다 [!DNL Flow Service] 흐름 ID, 버전 및 제거할 대상자의 색인 선택기를 제공하는 동안 API입니다. 색인화 시작 위치: `0`. 예를 들어 아래 샘플 요청은 데이터 흐름에서 첫 번째 및 두 번째 대상을 제거합니다.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

다음 요청은 기존 대상 데이터 흐름에서 두 대상을 제거합니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
{
   "op":"remove",
   "path":"/transformations/0/params/segmentSelectors/selectors/0",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"/transformations/0/params/segmentSelectors/selectors/1",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
}
]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. 데이터 흐름에서 대상자를 제거하려면 `remove` 작업. |
| `path` | 대상 선택기의 색인에 따라 대상 데이터 흐름에서 제거해야 하는 기존 대상을 지정합니다. GET 데이터 흐름에서 대상자 순서를 검색하려면 `/flows` 엔드포인트 및 검사 `transformations.segmentSelectors` 속성. 데이터 흐름의 첫 번째 대상을 삭제하려면 `"path":"/transformations/0/params/segmentSelectors/selectors/0"`. |


**응답**

성공적인 응답은 흐름 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] 흐름 ID를 제공하는 동안 API입니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 데이터 흐름에서 대상의 구성 요소 업데이트 {#update-segment}

기존 대상 데이터 흐름에서 대상의 구성 요소를 업데이트할 수 있습니다. 예를 들어 내보내기 빈도를 변경하거나 파일 이름 템플릿을 편집할 수 있습니다. 이렇게 하려면 PATCH 요청을 [!DNL Flow Service] 플로우 ID, 버전 및 업데이트할 대상자의 색인 선택기를 제공하는 동안 API입니다. 색인화 시작 위치: `0`. 예를 들어 아래 요청은 데이터 흐름의 9번째 대상을 업데이트합니다.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

기존 대상 데이터 흐름에서 대상을 업데이트할 때에는 먼저 업데이트할 대상의 세부 정보를 검색하는 GET 작업을 수행해야 합니다. 그런 다음 업데이트하려는 필드뿐만 아니라 페이로드에 모든 대상 정보를 제공합니다. 아래 예에서는 파일 이름 템플릿 끝에 사용자 정의 텍스트가 추가되고 내보내기 일정 빈도가 6시간에서 12시간으로 업데이트됩니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"replace",
      "path":"/transformations/0/params/segmentSelectors/selectors/8",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
            "name":"Batch export for autumn campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
            "schedule":{
               "frequency":"EVERY_12_HOURS",
               "startDate":"2022-01-05",
               "endDate":"2022-01-30",
               "startTime":"20:00"
            },
            "createTime":"1640289901",
            "updateTime":"1640289901"
         }
      }
   }
]'
```

페이로드의 속성에 대한 설명은 섹션을 참조하십시오 [데이터 흐름에 대상 추가](#add-segment).


**응답**

성공적인 응답은 흐름 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] 흐름 ID를 제공하는 동안 API입니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

데이터 흐름에서 업데이트할 수 있는 대상 구성 요소의 추가 예는 아래 예를 참조하십시오.

## 대상자의 내보내기 모드를 예약됨에서 대상자 평가 후로 업데이트 {#update-export-mode}

+++ 대상자 내보내기가 지정된 시간에 매일 활성화되지 않고 플랫폼 일괄 처리 세분화 작업이 완료된 후 매일 활성화되도록 업데이트되는 예를 보려면 를 클릭합니다.

대상은 매일 16:00 UTC에 내보내집니다.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

매일 일괄 처리 세분화 작업이 완료된 후 대상자를 매일 내보냅니다.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "AFTER_SEGMENT_EVAL",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## 파일 이름에 추가 필드를 포함하도록 파일 이름 템플릿 업데이트 {#update-filename-template}

+++ 파일 이름에 추가 필드를 포함하도록 파일 이름 템플릿이 업데이트된 예를 보려면 클릭하십시오

내보낸 파일에는 대상 이름과 Experience Platform 대상 ID가 포함되어 있습니다

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

내보낸 파일에는 대상 이름, Experience Platform 대상 ID, Experience Platform에 의해 파일이 생성된 날짜와 시간, 파일 끝에 추가된 사용자 지정 텍스트가 포함되어 있습니다.


```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_%this is custom text%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## 데이터 흐름에 프로필 속성 추가 {#add-profile-attribute}

대상 데이터 흐름에 PATCH 속성을 추가하려면 [!DNL Flow Service] 플로우 ID, 버전 및 추가하려는 프로필 속성을 제공하는 동안 API입니다.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

다음 요청은 기존 대상 데이터 흐름에 새 프로필 속성을 추가합니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"add",
    "path":"/transformations/0/params/profileSelectors/selectors/-",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. 프로필 속성을 데이터 흐름에 추가하려면 `add` 작업. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. 데이터 흐름에 프로필 속성을 추가할 때는 예제에 지정된 경로를 사용하십시오. |
| `value.path` | 데이터 흐름에 추가할 프로필 속성의 값입니다. |

**응답**

성공적인 응답은 흐름 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] 흐름 ID를 제공하는 동안 API입니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 데이터 흐름에서 프로필 속성 제거 {#remove-profile-attribute}

PATCH 기존 대상 데이터 흐름에서 프로필 속성을 제거하려면 [!DNL Flow Service] 제거할 프로필 속성의 흐름 ID, 버전 및 색인 선택기를 제공하는 동안 API입니다. 색인화 시작 위치: `0`. 예를 들어 아래의 샘플 요청은 데이터 흐름에서 다섯 번째 프로필 속성을 제거합니다.


**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

다음 요청은 기존 대상 데이터 흐름에서 프로필 속성을 제거합니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"remove",
    "path":"/transformations/0/params/profileSelectors/selectors/4",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다. `add`, `replace`, 및 `remove`. 데이터 흐름에서 대상자를 제거하려면 `remove` 작업. |
| `path` | 대상 선택기의 색인에 따라 대상 데이터 흐름에서 제거해야 하는 기존 프로필 속성을 지정합니다. GET 데이터 흐름에서 프로필 속성 순서를 검색하려면 `/flows` 엔드포인트 및 검사 `transformations.profileSelectors` 속성. 데이터 흐름의 첫 번째 대상을 삭제하려면 `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**응답**

성공적인 응답은 흐름 ID와 업데이트된 etag를 반환합니다. 에 GET 요청을 하여 업데이트를 확인할 수 있습니다. [!DNL Flow Service] 흐름 ID를 제공하는 동안 API입니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## API 오류 처리 {#api-error-handling}

이 자습서의 API 끝점은 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](/help/landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](/help/landing/troubleshooting.md#request-header-errors) 오류 응답 해석에 대한 자세한 내용은 플랫폼 문제 해결 안내서를 참조하십시오.

## 다음 단계 {#next-steps}

이 자습서를 통해 다음을 사용하여 대상자 또는 프로필 속성을 추가 또는 제거하는 등, 대상 데이터 흐름의 다양한 구성 요소를 업데이트하는 방법을 배웠습니다 [!DNL Flow Service] API. 대상에 대한 자세한 내용은 [대상 개요](../home.md).
