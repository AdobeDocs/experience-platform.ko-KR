---
keywords: Experience Platform;홈;인기 항목;모니터 데이터 흐름 서비스 api;흐름 서비스
solution: Experience Platform
title: Flow Service API를 사용하여 데이터 흐름 모니터링
topic-legacy: overview
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 완벽성, 오류 및 지표에 대한 흐름 실행 데이터를 모니터링하는 단계를 설명합니다.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Flow Service API를 사용하여 데이터 흐름 모니터링

Adobe Experience Platform은 [!DNL Platform] 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있도록 허용합니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등 다양한 소스의 데이터를 인제스트할 수 있습니다. 또한 Experience Platform을 통해 외부 파트너에게 데이터를 활성화할 수 있습니다.

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집한 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스 및 대상을 연결할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)을(를) 사용하여 완료, 오류 및 지표에 대한 흐름 실행 데이터를 모니터링하는 단계를 설명합니다.

## 시작하기

이 자습서에서는 올바른 데이터 흐름 ID 값을 가져야 합니다. 유효한 데이터 흐름 ID가 없는 경우 [소스 개요](../../sources/home.md) 또는 [대상 개요](../../destinations/catalog/overview.md)에서 원하는 커넥터를 선택하고 이 튜토리얼을 시작하기 전에 설명한 단계를 따르십시오.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 자세히 알아야 합니다.

- [대상](../../destinations/home.md):대상은 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 많은 사용 사례를 위해 플랫폼에서 데이터를 원활하게 활성화할 수 있도록 하는 일반적으로 사용되는 애플리케이션과의 사전 구축된 통합입니다.
- [소스](../../sources/home.md): [!DNL Experience Platform] 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 흐름 실행을 성공적으로 모니터링하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

- `Content-Type: application/json`

## 흐름 실행 모니터링

데이터 흐름을 만들었으면 [!DNL Flow Service] API에 GET 요청을 수행합니다.

**API 형식**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 모니터링할 데이터 플로의 고유한 `id` 값입니다. |

**요청**

다음 요청은 기존 데이터 흐름 사양을 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 작성 날짜, 소스 및 대상 연결과 흐름 실행의 고유 식별자(`id`)에 대한 정보를 포함하여 흐름 실행에 대한 세부 정보를 반환합니다.

```json
{
    "items": [
        {
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{IMS_ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `items` | 특정 흐름 실행과 연관된 메타데이터의 단일 페이로드를 포함합니다. |
| `metrics` | 흐름 실행 데이터의 특성입니다. |
| `activities` | 데이터가 변형되는 방식을 표시합니다. |
| `durationSummary` | 흐름 실행의 시작 및 종료 시간입니다. |
| `sizeSummary` | 데이터의 볼륨(바이트)입니다. |
| `recordSummary` | 데이터의 레코드 수입니다. |
| `fileSummary` | 데이터의 파일 카운트입니다. |
| `fileSummary.extensions` | 활동과 관련된 정보를 포함합니다. 예를 들어 `manifest`은 &quot;홍보 활동&quot;의 일부이므로 `extensions` 개체에 포함됩니다. |
| `statusSummary` | 흐름 실행이 성공인지 실패인지 표시합니다. |

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 데이터 플로에서 지표 및 오류 정보를 검색했습니다. 이제 통합 일정에 따라 데이터 흐름을 계속 모니터링하여 상태 및 수집 비율을 추적할 수 있습니다. 소스의 데이터 흐름 모니터링 방법에 대한 자세한 내용은 사용자 인터페이스](../ui/monitor-sources.md) 자습서를 사용하여 소스의 데이터 흐름 모니터링을 참조하십시오. [ 대상에 대한 데이터 흐름 모니터링 방법에 대한 자세한 내용은 사용자 인터페이스](../ui/monitor-destinations.md) 튜토리얼을 사용하여 대상의 데이터 흐름 모니터링을 참조하십시오.[
