---
keywords: Experience Platform;home;popular topics; notifications
description: Adobe I/O 이벤트를 사용하면 이벤트를 구독하고 웹 후크를 사용하여 흐름 실행 상태와 관련된 알림을 받을 수 있습니다. 이러한 알림에는 흐름 실행의 성공 또는 실행에 실패한 오류에 대한 정보가 포함됩니다.
solution: Experience Platform
title: 흐름 실행 알림
topic: overview
translation-type: tm+mt
source-git-commit: b5b785d8415c15e3acb9e1155811a66c51477717
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---


# 흐름 실행 알림

Adobe Experience Platform은 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있도록 허용합니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등 다양한 소스의 데이터를 인제스트할 수 있습니다.

[[!DNL Adobe Experience Platform 흐름 서비스]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) 는 다양한 서로 다른 소스에서 고객 데이터를 수집하고 관리하는 데 사용됩니다 [!DNL Platform]. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

Adobe I/O 이벤트를 사용하면 이벤트를 구독하고 웹 후크를 사용하여 흐름 실행 상태와 관련된 알림을 받을 수 있습니다. 이러한 알림에는 흐름 실행의 성공 또는 실행에 실패한 오류에 대한 정보가 포함됩니다.

이 문서에서는 이벤트 가입, 웹 후크 등록 및 흐름 실행 상태에 대한 정보가 포함된 알림 수신 방법에 대해 설명합니다.

## 시작하기

이 문서는 다음 Adobe Experience Platform 구성 요소에 대한 작업 이해를 필요로 합니다.

* [[!DNL 경험 데이터 모델(XDM) 시스템]](../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
* [[!DNL 실시간 고객 프로필]](../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Adobe Experience Platform 데이터 처리]](../ingestion/home.md): [!DNL Data Ingestion] 는 이러한 소스의 데이터를 [!DNL Platform] 인제스트하는 여러 메서드와 다운스트림 [!DNL Data Lake] [!DNL Platform] 서비스에서 사용하기 위해 데이터가 내부에서 유지되는 방식을 나타냅니다.

또한 이 문서를 사용하려면 웹 후크에 대한 작업 내용과 한 응용 프로그램에서 다른 응용 프로그램으로 웹후크를 연결하는 방법을 이해해야 합니다. 웹 후크에 대한 자세한 내용은 다음 [설명서를](https://requestbin.com/blog/working-with-webhooks/) 참조하십시오.

## 웹 후크 등록

흐름 실행 상태에 대한 알림을 받으려면 고유한 웹 후크 URL을 이벤트 등록 세부 정보의 일부로 지정하여 웹 후크를 등록해야 합니다. 웹 후크를 구독에 연결하려면 [!DNL I/O Events] 웹 후크 서비스 [](https://webhook.site/) 를 방문하여 제공된 고유한 URL을 복사하십시오.

![웹 후크](./images/notifications/webhook-url.png)

## 이벤트 구독

고유한 웹 후크 URL을 얻으면 [Adobe I/O 이벤트로](https://www.adobe.io/apis/experienceplatform/events.html) 이동하여 [데이터 수집 알림](../ingestion/quality/subscribe-events.md) 문서에 설명된 단계에 따라 이벤트 구독을 시작합니다.

>[!IMPORTANT]
>구독 프로세스 동안 이벤트 제공자로 [!DNL Platform] 알림을 선택하고 다음 이벤트 구독을 선택하십시오.
>
>* **[!UICONTROL Experience Platform 소스의 흐름 실행 성공]**
>* **[!UICONTROL Experience Platform 소스의 흐름 실행 실패]**

>
>
웹 후크 주소를 제공하라는 메시지가 표시되면 이전에 획득한 웹 후크 URL을 사용합니다.

## 흐름 실행 알림 받기

웹후크가 연결되고 이벤트 구독이 완료되면 웹 후크 대시보드를 통해 흐름 실행 알림을 받을 수 있습니다.

알림은 처리 작업 실행 수, 파일 크기 및 오류와 같은 정보를 반환합니다. 또한 알림은 흐름 실행과 관련된 페이로드를 JSON 형식으로 반환합니다. 응답 페이로드를 `sources_flow_run_success` 또는 `sources_flow_run_failure`로 분류할 수 있습니다.

>[!IMPORTANT]
>흐름 생성 프로세스 중에 부분 처리가 활성화되면, 성공 및 실패한 입고를 모두 포함하는 흐름은 흐름 생성 프로세스 동안 오류 임계값 백분율 설정 아래에 있는 `sources_flow_run_success` 경우에만 표시됩니다. 성공적인 흐름 실행에 오류가 있는 경우 이러한 오류는 여전히 반환 페이로드의 일부로 포함됩니다.

### 성공

성공적인 응답은 특정 흐름 실행의 특성을 `metrics` 정의하고 데이터가 변형되는 방법을 `activities` 대략적으로 설명하는 집합을 반환합니다.

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
    "imsOrgId": "{IMS_ORG}",
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
              "fileInfo": "https://platform-int.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
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
        "imsOrgId": "{IMS_ORG}",
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
| `metrics` | 흐름 실행 데이터의 특성을 정의합니다. |
| `activities` | 데이터를 변형하기 위해 수행되는 다양한 단계 및 활동을 정의합니다. |
| `durationSummary` | 흐름 실행의 시작 및 종료 시간을 정의합니다. |
| `sizeSummary` | 데이터의 볼륨(바이트)을 정의합니다. |
| `recordSummary` | 데이터의 레코드 개수를 정의합니다. |
| `fileSummary` | 데이터의 파일 개수를 정의합니다. |
| `fileInfo` | 인제스트된 파일의 개요를 표시하는 URL. |
| `statusSummary` | 흐름 실행이 성공인지 실패인지 여부를 정의합니다. |

### 실패

다음 응답은 복사된 데이터가 처리될 때 발생하는 오류와 함께 실패한 흐름 실행의 예입니다. 소스에서 데이터를 복사하는 동안에도 오류가 발생할 수 있습니다. 실패한 흐름 실행에는 오류 및 설명을 포함하여 실행 실패에 기여한 오류에 대한 정보가 포함됩니다.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{IMS_ORG}",
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
          "imsOrgId": "{IMS_ORG}",
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
| `fileInfo` | 성공적으로 인제스트된 파일과 실패한 파일의 개요를 표시하는 URL입니다. |

>[!NOTE]
>오류 메시지에 대한 자세한 내용은 [부록을](#errors) 참조하십시오.

## 다음 단계

이제 흐름 실행 상태에 대한 실시간 알림을 수신할 수 있는 이벤트를 구독할 수 있습니다. 흐름 실행 및 소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](./home.md).

## 부록

다음 섹션에서는 흐름 실행 알림 작업에 대한 추가 정보를 제공합니다.

### 오류 메시지 이해 {#errors}

데이터가 소스에서 복사되거나 복사된 데이터가 처리되는 경우 처리 오류가 발생할 수 있습니다 [!DNL Platform]. 특정 오류에 대한 자세한 내용은 아래 표를 참조하십시오.

| 오류 | 설명 |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | 소스에서 데이터를 복사하는 동안 오류가 발생했습니다. |
| `CONNECTOR-2001-500` | 복사한 데이터를 처리하는 동안 오류가 발생했습니다 [!DNL Platform]. 구문 분석, 유효성 검사 또는 변환과 관련하여 이 오류가 발생할 수 있습니다. |
