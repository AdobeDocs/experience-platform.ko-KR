---
description: 이 페이지에서는 /testing/destinationInstance API 끝점을 사용하여 테스트 결과에 대한 전체 세부 정보를 보는 방법에 대해 설명합니다. 이 API 끝점은 흐름 서비스 API를 사용하여 데이터 흐름을 모니터링할 때 얻는 것과 동일한 결과를 반환합니다.
title: 자세한 활성화 결과 보기
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: 9ac6b075af3805da4dad0dd6442d026ae96ab5c7
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---

# 자세한 활성화 결과 보기 {#view-test-results}

## 개요 {#overview}

이 페이지에서는 `/testing/destinationInstance` API 끝점을 사용하여 파일 기반 대상 테스트 결과의 전체 세부 정보를 보는 방법에 대해 설명합니다.

이미 [대상을 테스트하고](file-based-destination-testing-api.md)유효한 API 응답을 받은 경우 대상이 올바르게 작동합니다.

활성화 흐름에 대한 자세한 정보를 보려면 아래 설명된 대로 [대상 테스트](file-based-destination-testing-api.md) 끝점 응답의 `results` 속성을 사용할 수 있습니다.

>[!NOTE]
>
>이 API 끝점은 [흐름 서비스 API](../../../api/update-destination-dataflows.md)를 사용하여 데이터 흐름을 모니터링할 때와 동일한 결과를 반환합니다.

## 시작하기 {#getting-started}

계속하기 전에 [시작 안내서](../../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 전제 조건 {#prerequisites}

`/testing/destinationInstance` 끝점을 사용하기 전에 다음 조건을 충족하는지 확인하십시오.

* Destination SDK을 통해 만든 기존 파일 기반 대상이 있으며 [대상 카탈로그](../../../ui/destinations-workspace.md)에서 볼 수 있습니다.
* Experience Platform UI에서 대상에 대한 활성화 흐름을 하나 이상 만들었습니다.
* API 요청을 성공적으로 수행하려면 테스트할 대상 인스턴스에 해당하는 대상 인스턴스 ID가 필요합니다. Platform UI에서 대상과의 연결을 검색할 때 API 호출에 사용해야 하는 대상 인스턴스 ID를 URL에서 가져옵니다.

  URL에서 대상 인스턴스 ID를 가져오는 방법을 보여 주는 ![UI 이미지.](../../assets/testing-api/get-destination-instance-id.png)
* 이전에 [대상 구성을 테스트하고](file-based-destination-testing-api.md) `results` 속성이 포함된 올바른 API 응답을 받았습니다. 이 `results` 값을 사용하여 대상을 추가로 테스트합니다.

## 자세한 대상 테스트 결과 보기 {#test-activation-results}

[대상 구성의 유효성을 검사했습니다](file-based-destination-testing-api.md). `authoring/testing/destinationInstance/` 끝점에 대한 GET 요청을 만들고 테스트 중인 대상의 대상 인스턴스 ID와 활성화된 대상의 흐름 실행 ID를 제공하여 자세한 활성화 결과를 볼 수 있습니다.

대상 테스트 호출의 [응답](file-based-destination-testing-api.md)에서 반환된 `results` 속성에서 사용해야 하는 전체 API URL을 찾을 수 있습니다.

**API 형식**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| 경로 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 샘플 프로필을 생성하고 있는 대상 인스턴스의 ID입니다. 이 ID를 얻는 방법에 대한 자세한 내용은 [필수 구성 요소](#prerequisites) 섹션을 참조하십시오. |

| 쿼리 문자열 매개 변수 | 설명 |
| -------- | ----------- |
| `flowRunIds` | 활성화된 대상자에 해당하는 흐름 실행 ID입니다. 대상 테스트 호출의 [응답](file-based-destination-testing-api.md)에서 반환된 `results` 속성에서 흐름 실행 ID를 찾을 수 있습니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=30d34875-e7ba-4520-ab6e-5705e01dfb16,86c00ad7-443c-459a-855d-0e8cbee43c4f,12305c58-42a9-4230-8fad-1661ee49cb70' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 활성화 흐름에 대한 전체 세부 정보가 포함됩니다. 데이터 흐름을 모니터링하기 위해 [흐름 서비스 API](../../../api/update-destination-dataflows.md)를 호출하여 동일한 응답을 얻을 수 있습니다.

```json
{
   "items":[
      {
         "id":"18efd5d2-40ae-4f5c-afd1-37a39a45183a",
         "flowId":"a02071ad-f3a4-496c-a2b1-468812301d5d",
         "flowSpec":{
            "id":"25473b67-0801-418a-ab49-ed74ebf88137",
            "version":"1.0"
         },
         "metrics":{
            "durationSummary":{
               "startedAtUTC":1646652235124,
               "completedAtUTC":1646652270439
            },
            "latencySummary":null,
            "sizeSummary":{
               "inputBytes":122,
               "outputBytes":122
            },
            "recordSummary":{
               "inputRecordCount":1,
               "outputRecordCount":1,
               "createdRecordCount":1,
               "skippedRecordCount":0,
               "sourceSummaries":[
                  {
                     "id":"76e4b969-9700-4557-8330-0a8390afbdde",
                     "entitySummaries":[
                        {
                           "inputRecordCount":1,
                           "skippedRecordCount":0,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ],
               "targetSummaries":[
                  {
                     "id":"b43607b6-0dca-43b3-a0bc-ecdea4fa6aa9",
                     "entitySummaries":[
                        {
                           "outputRecordCount":1,
                           "createdRecordCount":1,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ]
            },
            "fileSummary":{
               "inputFileCount":1,
               "outputFileCount":1
            },
            "statusSummary":{
               "status":"success"
            }
         },
         "activities":[
            {
               "id":"c4f238e3-7334-4933-8b56-64d7ea43ea54",
               "name":"Activation Batch XdmProcessor Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652235124,
                  "completedAtUTC":1646652255157
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "inputBytes":122,
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "inputFileCount":1,
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     "incremental.batchId":"",
                     "snapshot.batchId":"",
                     "snapshot.datasetId":"",
                     "incremental.datasetId":""
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            },
            {
               "id":"51d82b36-6b8f-11eb-9439-0242ac130002",
               "name":"Activation Batch Publisher Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652270326,
                  "completedAtUTC":1646652270439
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            }
         ],
         "predecessors":null
      }
   ],
   "_links":{
      
   }
}
```

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계

이제 이 문서를 읽고 파일 기반 대상 구성을 테스트하고 활성화 결과에 대한 전체 세부 정보를 확인하는 방법을 알 수 있습니다.

공개 대상을 만드는 경우 이제 [대상 구성을 제출](../../guides/submit-destination.md)하여 검토를 위해 Adobe에 액세스할 수 있습니다.
