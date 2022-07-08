---
description: 이 페이지에서는 /testing/destinationInstance API 엔드포인트를 사용하여 테스트 결과의 전체 세부 사항을 보는 방법에 대해 설명합니다. 이 API 종단점은 Flow Service API를 사용하여 데이터 흐름을 모니터링할 때 얻을 것과 동일한 결과를 반환합니다.
title: 자세한 활성화 결과 보기
source-git-commit: 5b62203113dd55dad8adeb96cbcc2d46b3420c3a
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---


# 자세한 활성화 결과 보기 {#view-test-results}

## 개요 {#overview}

이 페이지에서는 를 사용하는 방법을 설명합니다. `/testing/destinationInstance` 파일 기반 대상 테스트 결과의 전체 세부 사항을 보는 API 엔드포인트.

이미 [대상을 테스트했습니다.](file-based-destination-testing-api.md) 유효한 API 응답을 수신했습니다. 대상이 올바르게 작동합니다.

활성화 흐름에 대한 자세한 정보를 보려면 `results` 속성 [대상 테스트](file-based-destination-testing-api.md) 아래에 자세히 설명된 대로 엔드포인트 응답.

>[!NOTE]
>
>이 API 종단점은 를 사용할 때와 동일한 결과를 반환합니다 [Flow Service API](../api/update-destination-dataflows.md) 데이터 흐름을 모니터링하려면 다음을 수행하십시오.

## 시작하기 {#getting-started}

계속하기 전에 [시작 안내서](./getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 전제 조건 {#prerequisites}

를 사용하기 전에 `/testing/destinationInstance` endpoint, 다음 조건을 충족하는지 확인하십시오.

* Destination SDK을 통해 만든 기존 파일 기반 대상이 있으며 [대상 카탈로그](../ui/destinations-workspace.md).
* Experience Platform UI에서 대상에 대해 하나 이상의 활성화 흐름을 만들었습니다.
* API 요청을 성공적으로 수행하려면 테스트할 대상 인스턴스에 해당하는 대상 인스턴스 ID가 필요합니다. Platform UI에서 대상과의 연결을 검색할 때 URL에서 API 호출에 사용해야 하는 대상 인스턴스 ID를 가져옵니다.

   ![URL에서 대상 인스턴스 ID를 가져오는 방법을 보여주는 UI 이미지입니다.](assets/get-destination-instance-id.png)
* 이전에 [대상 구성을 테스트했습니다.](file-based-destination-testing-api.md), 및 가 다음을 포함한 유효한 API 응답을 수신했습니다. `results` 속성을 사용합니다. 다음 항목을 사용합니다 `results` 값을 사용하여 대상을 추가로 테스트할 수 있습니다.

## 자세한 대상 테스트 결과 보기 {#test-activation-results}

한번 드시면 [대상 구성을 검증했습니다.](file-based-destination-testing-api.md)에 대한 GET 요청을 수행하여 세부 활성화 결과를 볼 수 있습니다. `authoring/testing/destinationInstance/` 테스트할 대상의 대상 인스턴스 ID와 활성화된 세그먼트의 흐름 실행 ID를 제공하는 종단점입니다.

사용해야 하는 전체 API URL을 `results` 에서 반환된 속성 [대상 테스트 호출 응답](file-based-destination-testing-api.md).

**API 형식**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| 경로 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 샘플 프로필을 생성하는 대상 인스턴스의 ID입니다. 자세한 내용은 [전제 조건](#prerequisites) 섹션을 참조하십시오. |

| 쿼리 문자열 매개 변수 | 설명 |
| -------- | ----------- |
| `flowRunIds` | 활성화된 세그먼트에 해당하는 흐름 실행 ID입니다. 흐름 실행 ID는 `results` 에서 반환된 속성 [대상 테스트 호출 응답](file-based-destination-testing-api.md). |

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

응답에는 활성화 흐름의 전체 세부 정보가 포함되어 있습니다. 를 호출하여 동일한 응답을 얻을 수 있습니다 [Flow Service API](../api/update-destination-dataflows.md) 데이터 흐름을 모니터링하려면 다음을 수행하십시오.

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

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 파일 기반 대상 구성을 테스트하고 활성화 결과의 전체 세부 사항을 확인하는 방법을 알 수 있습니다.

이제 공개 대상을 만드는 경우 [대상 구성 제출](../destination-sdk/submit-destination.md) Adobe을 참조하십시오.
