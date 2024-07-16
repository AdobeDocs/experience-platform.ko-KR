---
title: 흐름 서비스 API에서 응답 정렬 및 필터링
description: 이 자습서에서는 몇 가지 고급 사용 사례를 포함하여 흐름 서비스 API에서 쿼리 매개 변수를 사용하여 정렬하고 필터링하는 구문을 다룹니다.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: c7ff379b260edeef03f8b47f932ce9040eef3be2
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 2%

---

# 흐름 서비스 API에서 응답 정렬 및 필터링

[흐름 서비스 API](https://www.adobe.io/experience-platform-apis/references/flow-service/)에서 목록(GET) 요청을 수행할 때 쿼리 매개 변수를 사용하여 응답을 정렬하고 필터링할 수 있습니다. 이 안내서에서는 다양한 사용 사례에서 이러한 매개 변수를 사용하는 방법에 대한 참조를 제공합니다.

## 정렬

`orderby` 쿼리 매개 변수를 사용하여 응답을 정렬할 수 있습니다. API에서는 다음 리소스를 정렬할 수 있습니다.

* [연결](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Source 연결](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [대상 연결](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [흐름](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [실행](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

매개 변수를 사용하려면 해당 값을 정렬할 특정 속성(예: `?orderby=name`)으로 설정해야 합니다. 오름차순의 경우 더하기 기호(`+`)를 사용하고, 내림차순의 경우 빼기 기호(`-`)를 사용하여 값을 앞에 추가할 수 있습니다. 순서 지정 접두사가 제공되지 않으면 기본적으로 목록이 오름차순으로 정렬됩니다.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

&quot;and&quot; 기호(`&`)를 사용하여 정렬 매개 변수와 필터링 매개 변수를 결합할 수도 있습니다.

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## 필터링

키-값 식에 `property` 매개 변수를 사용하여 응답을 필터링할 수 있습니다. 예를 들어 `?property=id==12345`은(는) `id` 속성이 정확히 `12345`인 리소스만 반환합니다.

필터링은 해당 속성에 대한 유효한 경로가 알려져 있는 한 엔티티의 모든 속성에 일반적으로 적용할 수 있습니다.

>[!NOTE]
>
>속성이 배열 항목 내에 중첩되면 경로에 대괄호(`[]`)를 배열에 추가해야 합니다. 예를 보려면 [배열 속성 필터링](#arrays)에 대한 섹션을 참조하십시오.

**원본 테이블 이름이 `lead`인 모든 원본 연결을 반환합니다.**

```http
GET /sourceConnections?property=params.tableName==lead
```

**특정 세그먼트 ID에 대한 모든 흐름을 반환합니다.**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### 필터 결합

&quot;and&quot; 문자(`&`)로 구분된 경우 쿼리에 여러 `property` 필터를 포함할 수 있습니다. 필터를 결합할 때 AND 관계가 가정되는데, 이것은 엔티티가 응답에 포함되기 위해 모든 필터를 충족해야 함을 의미합니다.

**세그먼트 ID에 대해 활성화된 모든 흐름을 반환합니다.**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### 배열 속성 필터링 {#arrays}

배열 속성 이름에 `[]`을(를) 추가하여 배열 내의 항목 속성을 기준으로 필터링할 수 있습니다.

**특정 원본 연결과 연결된 흐름을 반환합니다.**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**특정 선택기 값 ID를 포함하는 변환이 있는 흐름을 반환합니다.**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**특정 `name` 값이 있는 열이 있는 원본 연결을 반환합니다.**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**세그먼트 ID를 필터링하여 대상에 대한 흐름 실행 ID를 조회합니다.**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

모든 필터링 쿼리에 `true` 값을 가진 `count` 쿼리 매개 변수를 추가하여 결과 수를 반환할 수 있습니다. API 응답에 `count` 속성이 포함되어 있습니다. 해당 값은 필터링된 총 항목 수를 나타냅니다. 이 호출에서는 실제 필터링된 항목이 반환되지 않습니다.

**시스템에서 활성화된 흐름 수를 반환합니다.**

```http
GET /flows?property=state==enabled&count=true
```

위의 쿼리에 대한 응답은 다음과 같습니다.

```json
{
  "count": 95
}
```

### 리소스별 필터링 가능한 속성

검색 중인 흐름 서비스 엔터티에 따라 필터링에 다른 속성을 사용할 수 있습니다. 아래 표는 필터링 사용 사례에 일반적으로 사용되는 각 리소스에 대한 루트 수준 필드를 설명합니다.

**`connectionSpec`**

| 속성 | 예 |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style="table-layout:auto"}

**`flowSpec`**

| 속성 | 예 |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| 속성 | 예 |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| 속성 | 예 |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| 속성 | 예 |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`flow`**

| 속성 | 예 |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style="table-layout:auto"}

**`run`**

| 속성 | 예 |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## 사용 사례 {#use-cases}

필터링 및 정렬을 사용하여 특정 커넥터에 대한 정보를 반환하거나 문제 디버깅을 지원하는 방법에 대한 몇 가지 특정 예를 보려면 이 섹션을 참조하십시오. Adobe에서 추가하려는 추가 사용 사례가 있는 경우 페이지의 **[!UICONTROL 자세한 피드백 옵션]**&#x200B;을 사용하여 요청을 제출하십시오.

**특정 대상에 대한 연결만 반환하도록 필터링**

필터를 사용하여 특정 대상에만 연결을 반환할 수 있습니다. 먼저 다음과 같이 `connectionSpecs` 끝점을 쿼리합니다.

```http
GET /connectionSpecs
```

그런 다음 `name` 매개 변수를 검사하여 원하는 `connectionSpec`을(를) 검색합니다. 예를 들어 `name` 매개 변수에서 Amazon Ads, Pega, SFTP 등을 검색합니다. 해당 `id`은(는) 다음 API 호출에서 검색할 수 있는 `connectionSpec`입니다.

예를 들어 Amazon S3 연결에 대한 기존 연결만 반환하도록 대상을 필터링할 수 있습니다.

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**대상으로만 데이터 흐름을 반환하도록 필터링**

`/flows` 끝점을 쿼리할 때 모든 원본 및 대상 데이터 흐름을 반환하는 대신 필터를 사용하여 데이터 흐름을 대상으로만 반환할 수 있습니다. 이렇게 하려면 다음과 같이 `isDestinationFlow`을(를) 쿼리 매개 변수로 사용합니다.

```http
GET /flows?property=inheritedAttributes.properties.isDestinationFlow==true
```

**특정 원본 또는 대상으로만 데이터 흐름을 반환하도록 필터링**

데이터 흐름을 필터링하여 특정 대상 또는 특정 소스에서만 데이터 흐름을 반환할 수 있습니다. 예를 들어 Amazon S3 연결에 대한 기존 연결만 반환하도록 대상을 필터링할 수 있습니다.

```http
GET /flows?property=inheritedAttributes.targetConnections[].connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**특정 기간 동안 데이터 흐름의 모든 실행을 가져오도록 필터링**

다음과 같이 데이터 흐름의 데이터 흐름 실행을 필터링하여 특정 시간 간격의 실행만 볼 수 있습니다.

```
GET /runs?property=flowId==<flow-id>&property=metrics.durationSummary.startedAtUTC>1593134665781&property=metrics.durationSummary.startedAtUTC<1653134665781
```

**실패한 데이터 흐름만 반환하도록 필터링**

디버깅 목적으로 아래와 같이 특정 소스 또는 대상 데이터 흐름에 대해 실패한 모든 데이터 흐름을 필터링하고 볼 수 있습니다.

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## 다음 단계

이 안내서에서는 `orderby` 및 `property` 쿼리 매개 변수를 사용하여 흐름 서비스 API에서 응답을 정렬하고 필터링하는 방법을 다룹니다. 플랫폼의 일반 워크플로에 API를 사용하는 방법에 대한 단계별 안내서는 [소스](../../sources/home.md) 및 [대상](../../destinations/home.md) 설명서에 포함된 API 튜토리얼을 참조하십시오.
