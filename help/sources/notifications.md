---
keywords: Experience Platform;홈;인기 있는 주제; 알림
description: Adobe I/O Events을 구독하면 웹후크를 사용하여 소스 연결의 흐름 실행 상태에 대한 알림을 받을 수 있습니다. 이러한 알림에는 플로우 실행의 성공 또는 실행 실패에 기여한 오류에 대한 정보가 포함됩니다.
solution: Experience Platform
title: 플로우 실행 알림
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# 플로우 실행 알림

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)은(는) [!DNL Experience Platform] 내의 다양한 개별 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결 가능한 사용자 인터페이스와 RESTful API를 제공합니다.

Adobe I/O Events을 사용하면 이벤트를 구독하고 웹후크를 사용하여 플로우 실행 상태에 대한 알림을 받을 수 있습니다. 이러한 알림에는 플로우 실행의 성공 또는 실행 실패에 기여한 오류에 대한 정보가 포함됩니다.

이 문서에서는 이벤트를 구독하고, 웹후크를 등록하고, 플로우 실행 상태에 대한 정보가 포함된 알림을 받는 방법에 대한 단계를 제공합니다.

## 시작하기

이 자습서에서는 모니터링하려는 흐름이 실행되는 소스 연결을 이미 하나 이상 만들었다고 가정합니다. 아직 소스 연결을 구성하지 않은 경우 이 안내서로 돌아가기 전에 [소스 개요](./home.md)를 방문하여 원하는 소스를 구성하십시오.

또한 이 문서에서는 웹후크 및 웹후크를 한 응용 프로그램에서 다른 응용 프로그램으로 연결하는 방법에 대해 작업해야 합니다. Webhooks에 대한 소개는 [[!DNL I/O Events] 설명서](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md)를 참조하세요.

## 플로우 실행 알림에 대한 웹후크 등록

흐름 실행 알림을 받으려면 Adobe Developer Console을 사용하여 [!DNL Experience Platform] 통합에 웹후크를 등록해야 합니다.

이를 수행하는 방법에 대한 자세한 단계는 [[!DNL I/O Event] 알림 구독](../observability/alerts/subscribe.md)에 대한 자습서를 참조하십시오.

>[!IMPORTANT]
>
>구독 프로세스 중에 이벤트 공급자로 **[!UICONTROL 플랫폼 알림]**&#x200B;을(를) 선택하고 다음 이벤트 구독을 선택하십시오.
>
>* **[!UICONTROL Experience Platform Source의 흐름 실행 성공]**
>* **[!UICONTROL Experience Platform Source의 흐름 실행 실패]**

## 플로우 실행 알림 수신

Webhook이 연결되어 있고 이벤트 구독이 완료되면 Webhook 대시보드를 통해 흐름 실행 알림을 받을 수 있습니다.

알림은 실행된 수집 작업 수, 파일 크기 및 오류 등의 정보를 반환합니다. 알림은 플로우 실행과 연결된 페이로드도 JSON 형식으로 반환합니다. 응답 페이로드는 `sources_flow_run_success` 또는 `sources_flow_run_failure`(으)로 분류될 수 있습니다.

>[!IMPORTANT]
>
>흐름 만들기 프로세스 중에 부분 수집을 사용하도록 설정한 경우, 오류 수가 흐름 만들기 프로세스 중에 설정된 오류 임계값 백분율 미만인 경우에만 성공한 수집과 실패한 수집이 모두 포함된 흐름이 `sources_flow_run_success`로 표시됩니다. 성공한 흐름 실행에 오류가 포함되어 있으면 이러한 오류는 여전히 반환 페이로드의 일부로 포함됩니다.

### 성공

성공한 응답은 특정 흐름 실행의 특성을 정의하는 `metrics` 집합과 데이터 변환 방법을 설명하는 `activities`을(를) 반환합니다.

```json
{
  "event_id": "aec55616-1715-487f-8044-ba648cc8ffee",
  "event": {
    "createdAt": 1597213529158,
    "updatedAt": 1597213530760,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "7127a4f0-def8-11e9-83ce-e79494b1c2a5",
    "sandboxName": "prod",
    "imsOrgId": "{ORG_ID}",
    "id": "933cf9f4-cf01-4d75-bcf9-f4cf010d750a",
    "flowId": "1c6f1047-dcaf-48fe-af10-47dcaf08feaf",
    "providerRefId": "test1234",
    "etag": "\"5100ec97-0000-0200-0000-5f338b5b0000\"",
    "metrics": {
      "durationSummary": {
        "startedAtUTC": 1590512053,
        "completedAtUTC": 1590512053
      },
      "sizeSummary": {
        "inputBytes": 2048,
        "outputBytes": 1024
      },
      "recordSummary": {
        "inputRecordCount": 100,
        "outputRecordCount": 70
      },
      "fileSummary": {
        "inputFileCount": 10,
        "outputFileCount": 10
      },
      "statusSummary": {
        "status": "success"
      }
    },
    "activities": [
      {
        "id": "copyActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "startedAtUTC": 1590512053,
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 2048,
          "outputBytes": 1098
        },
        "recordSummary": {
          "inputRecordCount": 100,
          "outputRecordCount": 100
        },
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "adf/pipeline/id": "abcd",
            "adf/run/id": "1234"
          }
        },
        "sourceInfo": [
          {
            "id": "sourceConnectionId1",
            "type": "SourceConnection",
            "reference": {
              "type": "AdfRunId"
            }
          }
        ]
      },
      {
        "id": "promotionActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 1098,
          "outputBytes": 1024
        },
        "recordSummary": {},
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10,
          "extensions": {
            "manifest": {
              "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
            }
          }
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "batchId": "b1",
            "acp_request_id": "1234"
          }
        },
        "targetInfo": [
          {
            "id": "targetConnectionId1",
            "type": "TargetConnection",
            "reference": {
              "type": "batch"
            }
          }
        ]
      }
    ],
    "slaCreatedAt": 1597213531124,
    "processStartTime": 1597213531213,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "platform_notifications",
        "eventCode": "sources_flow_run_success"
      }
    },
    "transformedTime": 1597213531214
  }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `metrics` | 플로우 실행에서 데이터의 특성을 정의합니다. |
| `activities` | 데이터를 변환하기 위해 수행되는 다양한 단계 및 활동을 정의합니다. |
| `durationSummary` | 플로우 실행의 시작 및 종료 시간을 정의합니다. |
| `sizeSummary` | 데이터의 볼륨을 바이트 단위로 정의합니다. |
| `recordSummary` | 데이터의 레코드 수를 정의합니다. |
| `fileSummary` | 데이터의 파일 개수를 정의합니다. |
| `fileInfo` | 성공적으로 수집된 파일에 대한 개요로 이어지는 URL입니다. |
| `statusSummary` | 플로우 실행이 성공인지 실패인지를 정의합니다. |

### 실패

다음 응답은 복사된 데이터가 처리되면서 발생하는 오류와 함께 실패한 흐름 실행의 예입니다. 소스에서 데이터를 복사하는 동안 오류가 발생할 수도 있습니다. 실패한 흐름 실행에는 오류 및 설명을 포함하여 실행 실패의 원인이 된 오류에 대한 정보가 포함됩니다.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{ORG_ID}",
        "schema": {
          "name": "run-notification",
          "version": "1.0"
        },
        "provider": "FlowService",
        "_eventNotificationMeta": {
          "category": "Platform Notifications",
          "type": "sources_flow_run_failed"
        },
        "value": {
          "createdAt": 1597434147259,
          "updatedAt": 1597434157567,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "e49ebb00-d0fa-11e9-b164-ed6a398c8b35",
          "sandboxName": "prod",
          "imsOrgId": "{ORG_ID}",
          "id": "d9024c32-2174-4271-824c-322174627101",
          "flowId": "cf4fce79-8822-456d-8fce-798822556dc6",
          "etag": "\"0c003dbf-0000-0200-0000-5f36e92d0000\"",
          "metrics": {
            "durationSummary": {
              "startedAtUTC": 1597434147190
            },
            "sizeSummary": {
              "inputBytes": -1
            },
            "fileSummary": {
              "inputFileCount": -1
            },
            "statusSummary": {
              "status": "failed",
              "errors": [
                {
                  "code": "CONNECTOR-2001-500",
                  "message": "Error in processing (parsing, validation or transformation) the copied data."
                }
              ]
            }
          },
          "activities": [
            {
              "id": "promotionActivity",
              "updatedAtUTC": 1597434157529,
              "durationSummary": {
                "startedAtUTC": 1597434147190,
                "completedAtUTC": 1597434157212
              },
              "sizeSummary": {
                "inputBytes": -1
              },
              "recordSummary": {},
              "fileSummary": {
                "inputFileCount": -1,
                "extensions": {
                  "manifest": {
                    "fileInfo": "https://platform-stage.adobe.io/data/foundation/export/batches/6f6a900f-e40d-4f0e-9bb9-b614436c3465/meta?path=input_files"
                  }
                }
              },
              "statusSummary": {
                "status": "failed",
                "errors": [
                  {
                    "code": "CONNECTOR-2001-500",
                    "message": "Error in processing (parsing, validation or transformation) the copied data."
                  }
                ],
                "extensions": {
                  "errors": [
                    {
                      "code": "133",
                      "message": "We are unable to locate any files uploaded for this batch. Please upload files to ingest."
                    }
                  ]
                }
              },
              "targetInfo": [
                {
                  "id": "e88737aa-27b8-4795-8737-aa27b8f7959e",
                  "type": "TargetConnection",
                  "reference": {
                    "type": "Batch",
                    "ids": [
                      "6f6a900f-e40d-4f0e-9bb9-b614436c3465"
                    ]
                  }
                }
              ]
            }
          ]
        }
      }
    ]
  }
]
```

| 속성 | 설명 |
| ---------- | ----------- |
| `fileInfo` | 성공적으로 또는 성공적으로 수집되지 않은 파일에 대한 개요로 이어지는 URL입니다. |

>[!NOTE]
>
>오류 메시지에 대한 자세한 내용은 [부록](#errors)을 참조하세요.

## 다음 단계

이제 플로우 실행 상태에 대한 실시간 알림을 받을 수 있는 이벤트를 구독할 수 있습니다. 흐름 실행 및 소스에 대한 자세한 내용은 [소스 개요](./home.md)를 참조하세요.

## 부록

다음 섹션에서는 흐름 실행 알림 작업에 대한 추가 정보를 제공합니다.

### 오류 메시지 이해 {#errors}

소스에서 데이터를 복사하거나 복사된 데이터를 [!DNL Experience Platform]&#x200B;(으)로 처리하는 동안 수집 오류가 발생할 수 있습니다. 특정 오류에 대한 자세한 내용은 아래 표를 참조하십시오.

| 오류 | 설명 |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | 소스에서 데이터를 복사하는 동안 오류가 발생했습니다. |
| `CONNECTOR-2001-500` | 복사된 데이터를 [!DNL Experience Platform]&#x200B;(으)로 처리하는 동안 오류가 발생했습니다. 이 오류는 구문 분석, 유효성 검사 또는 변환과 관련된 것일 수 있습니다. |
