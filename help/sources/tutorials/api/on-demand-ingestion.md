---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;
title: 흐름 서비스 API를 사용하여 온디맨드 수집에 대한 흐름 실행 만들기
description: 흐름 서비스 API를 사용하여 온디맨드 수집을 위한 흐름 실행을 만드는 방법을 알아봅니다
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 온디맨드 수집에 대한 흐름 실행을 만듭니다.

흐름 실행은 흐름 실행의 인스턴스를 나타냅니다. 예를 들어 흐름이 매시간 오전 9:00, 오전 10:00 및 오전 11:00에 실행되도록 예약되어 있는 경우 세 개의 흐름 실행 인스턴스가 생깁니다. 플로우 실행은 특정 조직에만 해당됩니다.

온디맨드 수집은 주어진 데이터 흐름에 대해 실행되는 흐름을 만들 수 있는 기능을 제공합니다. 이를 통해 사용자는 서비스 토큰 없이 주어진 매개 변수를 기반으로 흐름 실행을 만들고 수집 주기를 만들 수 있습니다. 온디맨드 수집에 대한 지원은 배치 출처에 대해서만 사용할 수 있습니다.

이 자습서에서는 온디맨드 수집을 사용하고 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 흐름 실행을 만드는 방법에 대한 단계를 다룹니다.

## 시작하기

>[!NOTE]
>
>플로우 실행을 만들려면 먼저 1회 수집으로 예약된 데이터 흐름의 플로우 ID가 있어야 합니다.

이 자습서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 잘 알고 있어야 합니다.

* [원본](../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 테이블 기반 소스에 대한 흐름 실행 만들기

테이블 기반 소스에 대한 흐름을 만들려면 실행을 만들 흐름의 ID와 시작 시간, 종료 시간 및 델타 열에 대한 값을 제공하면서 [!DNL Flow Service] API에 대한 POST 요청을 만듭니다.

>[!TIP]
>
>테이블 기반 소스에는 광고, 분석, 동의 및 환경 설정, CRM, 고객 성공, 데이터베이스, 마케팅 자동화, 결제 및 프로토콜과 같은 소스 카테고리가 포함됩니다.

**API 형식**

```http
POST /runs/
```

**요청**

다음 요청은 흐름 ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`에 대한 흐름 실행을 만듭니다.

>[!NOTE]
>
>첫 번째 흐름 실행을 만들 때만 `deltaColumn`을(를) 제공하면 됩니다. 그 후 `deltaColumn`은(는) 흐름에서 `copy` 변환의 일부로 패치되며 진실의 소스로 처리됩니다. 흐름 실행 매개 변수를 통해 `deltaColumn` 값을 변경하려고 하면 오류가 발생합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| 매개변수 | 설명 |
| --- | --- |
| `flowId` | 플로우 실행을 생성할 플로우의 ID입니다. |
| `params.startTime` | 온디맨드 플로우 실행이 시작될 예약된 시간입니다. 이 값은 unix 시간으로 표시됩니다. |
| `params.windowStartTime` | 데이터를 검색할 가장 빠른 날짜 및 시간입니다. 이 값은 unix 시간으로 표시됩니다. |
| `params.windowEndTime` | 데이터를 검색할 날짜 및 시간입니다. 이 값은 unix 시간으로 표시됩니다. |
| `params.deltaColumn` | 델타 열은 데이터를 분할하고 새로 수집된 데이터를 기록 데이터와 구분하는 데 필요합니다. **참고**: `deltaColumn`은(는) 첫 번째 흐름 실행을 만들 때만 필요합니다. |
| `params.deltaColumn.name` | 델타 열의 이름입니다. |

**응답**

응답이 성공하면 고유한 실행 `id`을(를) 포함하여 새로 만든 흐름 실행의 세부 정보가 반환됩니다.

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 새로 생성된 플로우 실행의 ID입니다. 테이블 기반 실행 사양에 대한 자세한 내용은 [흐름 사양 검색](../api/collect/database-nosql.md#specs)에 대한 안내서를 참조하십시오. |
| `etag` | 흐름 실행의 리소스 버전입니다. |

<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

## 파일 기반 소스에 대한 흐름 실행 만들기

파일 기반 소스에 대한 흐름을 만들려면 실행할 흐름의 ID와 시작 시간 및 종료 시간에 대한 값을 제공하면서 [!DNL Flow Service] API에 대한 POST 요청을 만듭니다.

>[!TIP]
>
>파일 기반 소스에는 모든 클라우드 스토리지 소스가 포함됩니다.

**API 형식**

```http
POST /runs/
```

**요청**

다음 요청은 흐름 ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`에 대한 흐름 실행을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| 매개변수 | 설명 |
| --- | --- |
| `flowId` | 플로우 실행을 생성할 플로우의 ID입니다. |
| `params.startTime` | 온디맨드 플로우 실행이 시작될 예약된 시간입니다. 이 값은 unix 시간으로 표시됩니다. |
| `params.windowStartTime` | 데이터를 검색할 가장 빠른 날짜 및 시간입니다. 이 값은 unix 시간으로 표시됩니다. |
| `params.windowEndTime` | 데이터를 검색할 날짜 및 시간입니다. 이 값은 unix 시간으로 표시됩니다. |

**응답**

응답이 성공하면 고유한 실행 `id`을(를) 포함하여 새로 만든 흐름 실행의 세부 정보가 반환됩니다.


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 새로 생성된 플로우 실행의 ID입니다. 테이블 기반 실행 사양에 대한 자세한 내용은 [흐름 사양 검색](../api/collect/database-nosql.md#specs)에 대한 안내서를 참조하십시오. |
| `etag` | 흐름 실행의 리소스 버전입니다. |

## 플로우 실행 모니터링

플로우 실행이 생성되면 플로우 실행을 통해 수집되는 데이터를 모니터링하여 플로우 실행, 완료 상태 및 오류에 대한 정보를 확인할 수 있습니다. API를 사용하여 흐름 실행을 모니터링하려면 [API의 데이터 흐름 모니터링](./monitor.md)에 대한 자습서를 참조하십시오. Experience Platform UI를 사용하여 플로우 실행을 모니터링하려면 [모니터링 대시보드를 사용하여 소스 데이터 흐름 모니터링](../../../dataflows/ui/monitor-sources.md)에 대한 안내서를 참조하십시오.
