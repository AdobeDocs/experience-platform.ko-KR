---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;
title: (베타) Flow Service API를 사용하여 온디맨드 수집을 위한 흐름 실행 만들기
description: 이 자습서에서는 Flow Service API를 사용하여 온디맨드 수집에 대한 흐름 실행을 만드는 단계를 설명합니다
hide: true
hidefromtoc: true
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 24f16e315607a1076ff2efef129d9e97040a9500
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 1%

---

# (베타) [!DNL Flow Service] API

>[!IMPORTANT]
>
>온디맨드 수집은 현재 베타 버전이며 조직에서 아직 액세스할 수 없습니다. 이 설명서에 설명된 기능은 변경될 수 있습니다.

흐름 실행은 흐름 실행의 인스턴스를 나타냅니다. 예를 들어, 흐름이 오전 9:00, 오전 10:00 및 오전 11:00에 시간별로 실행되도록 예약된 경우, 흐름 실행의 세 인스턴스가 있습니다. 흐름 실행은 특정 조직에만 적용됩니다.

주문형 수집은 주어진 데이터 플로우에 대해 흐름 실행을 만드는 기능을 제공합니다. 이를 통해 사용자는 지정된 매개 변수를 기반으로 플로우 실행을 만들고 서비스 토큰 없이 수집 주기를 만들 수 있습니다.

이 자습서에서는 온디맨드 수집을 사용하고 을 사용하여 흐름 실행을 만드는 방법에 대해 설명합니다 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

>[!NOTE]
>
>흐름 실행을 만들려면 먼저 1회 수집으로 예약된 데이터 흐름의 흐름 ID가 있어야 합니다.

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../landing/api-guide.md).

## 테이블 기반 소스에 대해 흐름 실행 만들기

테이블 기반 소스에 대한 흐름을 생성하려면 [!DNL Flow Service] 실행을 생성할 흐름의 ID를 제공하고 시작 시간, 종료 시간 및 델타 열 값을 제공하는 동안 API를 생성합니다.

>[!TIP]
>
>테이블 기반 소스에는 다음과 같은 소스 카테고리가 포함됩니다. 광고, 분석, 동의 및 환경 설정, CRM, 고객 성공, 데이터베이스, 마케팅 자동화, 지불 및 프로토콜.

**API 형식**

```http
POST /runs/
```

**요청**

다음 요청은 흐름 ID에 대한 흐름 실행을 생성합니다 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>는 `deltaColumn` 첫 번째 흐름 실행을 생성할 때. 그 후에 `deltaColumn` 의 일부로 `copy` 흐름에서의 변형은 진리의 근원으로 간주될 것이다. 변경 시도 `deltaColumn` 흐름 실행 매개 변수를 통한 값은 오류가 발생합니다.

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
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `flowId` | 흐름 실행이 만들어질 흐름의 ID입니다. |
| `params.windowStartTime` | 데이터를 가져올 창의 시작 시간을 정의하는 정수입니다. 값은 unix 시간으로 표시됩니다. |
| `params.windowEndTime` | 데이터를 가져올 창의 종료 시간을 정의하는 정수입니다. 값은 unix 시간으로 표시됩니다. |
| `params.deltaColumn` | 델타 열은 데이터를 분할하고 새로 수집된 데이터를 내역 데이터에서 구분해야 합니다. |
| `params.deltaColumn.name` | 델타 열의 이름입니다. |

**응답**

성공적인 응답은 고유한 실행을 포함하여 새로 생성된 흐름 실행의 세부 사항을 반환합니다 `id`.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567",
        "deltaColumn": {
            "name": "DOB"
        }
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 새로 만든 흐름 실행의 ID입니다. 다음 안내서를 참조하십시오. [흐름 사양 검색](../api/collect/database-nosql.md#specs) 를 참조하십시오. |
| `createdAt` | 흐름 실행이 생성된 시점을 지정하는 unix 타임스탬프입니다. |
| `updatedAt` | 흐름 실행이 마지막으로 업데이트된 시기를 지정하는 unix 타임스탬프입니다. |
| `createdBy` | 흐름 실행을 생성한 사용자의 조직 ID입니다. |
| `updatedBy` | 흐름 실행을 마지막으로 업데이트한 사용자의 조직 ID입니다. |
| `createdClient` | 흐름 실행을 만든 응용 프로그램 클라이언트입니다. |
| `updatedClient` | 흐름 실행을 마지막으로 업데이트한 애플리케이션 클라이언트입니다. |
| `sandboxId` | 흐름 실행이 포함된 샌드박스의 ID입니다. |
| `sandboxName` | 흐름 실행이 포함된 샌드박스의 이름입니다. |
| `imsOrgId` | 조직 ID입니다. |
| `flowId` | 흐름 실행이 작성된 흐름의 ID입니다. |
| `params.windowStartTime` | 데이터를 가져올 창의 시작 시간을 정의하는 정수입니다. 값은 unix 시간으로 표시됩니다. |
| `params.windowEndTime` | 데이터를 가져올 창의 종료 시간을 정의하는 정수입니다. 값은 unix 시간으로 표시됩니다. |
| `params.deltaColumn` | 델타 열은 데이터를 분할하고 새로 수집된 데이터를 내역 데이터에서 구분해야 합니다. **참고**: 다음 `deltaColumn` 는 첫 번째 흐름 실행을 생성할 때만 필요합니다. |
| `params.deltaColumn.name` | 델타 열의 이름입니다. |
| `etag` | 흐름 실행의 리소스 버전입니다. |
| `metrics` | 이 속성은 흐름 실행에 대한 상태 요약을 표시합니다. |

## 파일 기반 소스에 대해 흐름 실행 만들기

파일 기반 소스에 대한 흐름을 만들려면 파일에 대한 POST 요청을 수행하십시오 [!DNL Flow Service] 시작 시간 및 종료 시간에 대한 값 및 실행을 만들 흐름의 ID를 제공하는 동안 API입니다.

>[!TIP]
>
>파일 기반 소스에는 모든 클라우드 스토리지 소스가 포함됩니다.

**API 형식**

```http
POST /runs/
```

**요청**

다음 요청은 흐름 ID에 대한 흐름 실행을 생성합니다 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

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
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `flowId` | 흐름 실행이 만들어질 흐름의 ID입니다. |
| `params.windowStartTime` | 데이터를 가져올 창의 시작 시간을 정의하는 정수입니다. 값은 unix 시간으로 표시됩니다. |
| `params.windowEndTime` | 데이터를 가져올 창의 종료 시간을 정의하는 정수입니다. 값은 unix 시간으로 표시됩니다. |

**응답**

성공적인 응답은 고유한 실행을 포함하여 새로 생성된 흐름 실행의 세부 사항을 반환합니다 `id`.


```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567"
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 새로 만든 흐름 실행의 ID입니다. 다음 안내서를 참조하십시오. [흐름 사양 검색](../api/collect/cloud-storage.md#specs) 파일 기반 실행 사양에 대한 자세한 정보. |
| `createdAt` | 흐름 실행이 생성된 시점을 지정하는 unix 타임스탬프입니다. |
| `updatedAt` | 흐름 실행이 마지막으로 업데이트된 시기를 지정하는 unix 타임스탬프입니다. |
| `createdBy` | 흐름 실행을 생성한 사용자의 조직 ID입니다. |
| `updatedBy` | 흐름 실행을 마지막으로 업데이트한 사용자의 조직 ID입니다. |
| `createdClient` | 흐름 실행을 만든 응용 프로그램 클라이언트입니다. |
| `updatedClient` | 흐름 실행을 마지막으로 업데이트한 애플리케이션 클라이언트입니다. |
| `sandboxId` | 흐름 실행이 포함된 샌드박스의 ID입니다. |
| `sandboxName` | 흐름 실행이 포함된 샌드박스의 이름입니다. |
| `imsOrgId` | 조직 ID입니다. |
| `flowId` | 흐름 실행이 작성된 흐름의 ID입니다. |
| `params.windowStartTime` | 데이터를 가져올 창의 시작 시간을 정의하는 정수입니다. 값은 unix 시간으로 표시됩니다. |
| `params.windowEndTime` | 데이터를 가져올 창의 종료 시간을 정의하는 정수입니다. 값은 unix 시간으로 표시됩니다. |
| `etag` | 흐름 실행의 리소스 버전입니다. |
| `metrics` | 이 속성은 흐름 실행에 대한 상태 요약을 표시합니다. |


## 흐름 실행 모니터링

흐름 실행이 만들어지면 이를 통해 수집되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. API를 사용하여 플로우 실행을 모니터링하려면 다음 자습서를 참조하십시오. [API에서 데이터 흐름 모니터링 ](./monitor.md). 플랫폼 UI를 사용하여 흐름 실행을 모니터링하려면 다음 안내서를 참조하십시오 [모니터링 대시보드를 사용하여 소스 데이터 흐름 모니터링](../../../dataflows/ui/monitor-sources.md).
