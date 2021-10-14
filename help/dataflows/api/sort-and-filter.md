---
title: Flow Service API의 응답 정렬 및 필터링
description: 이 자습서에서는 일부 고급 사용 사례를 포함하여 Flow Service API에서 쿼리 매개 변수를 사용하여 정렬 및 필터링하는 구문을 다룹니다.
source-git-commit: ccca81357bd7d7083abd3f395aa547c85ebf65fd
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 6%

---

# Flow Service API에서 응답 정렬 및 필터링

[Flow Service API](https://www.adobe.io/experience-platform-apis/references/flow-service/)에서 목록(GET) 요청을 수행할 때 쿼리 매개 변수를 사용하여 응답을 정렬 및 필터링할 수 있습니다. 이 안내서에서는 다양한 사용 사례에 이러한 매개 변수를 사용하는 방법에 대한 참조를 제공합니다.

## 정렬

`orderby` 쿼리 매개 변수를 사용하여 응답을 정렬할 수 있습니다. API에서 다음 리소스를 정렬할 수 있습니다.

* [연결](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [소스 연결](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Target 연결](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [흐름](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [실행](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

매개 변수를 사용하려면 해당 값을 정렬할 특정 속성(예: `?orderby=name`)으로 설정해야 합니다. 내림차순의 오름차순 또는 빼기 기호(`-`)를 사용하여 값을 앞에 추가할 수 있습니다. `+` 순서 지정 접두사가 제공되지 않으면 기본적으로 목록이 오름차순으로 정렬됩니다.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

&quot;and&quot; 기호(`&`)를 사용하여 정렬 매개 변수를 필터링 매개 변수와 결합할 수도 있습니다.

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## 필터링

키-값 표현식과 함께 `property` 매개 변수를 사용하여 응답을 필터링할 수 있습니다. 예를 들어 `?property=id==12345` 속성은 `id` 속성이 정확히 `12345`인 리소스만 반환합니다.

해당 속성의 유효한 경로가 알려진 한 필터링은 엔티티의 모든 속성에 일반적으로 적용할 수 있습니다.

>[!NOTE]
>
>속성이 배열 항목 내에 중첩된 경우 대괄호(`[]`)를 경로의 배열에 추가해야 합니다. 예제는 [배열 속성](#arrays)에서 필터링 섹션을 참조하십시오.

**소스 테이블 이름이 인 모든 소스 연결 반환  `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**특정 세그먼트 ID에 대한 모든 흐름 반환:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### 필터 결합

여러 `property` 필터가 &quot;and&quot; 문자(`&`)로 구분된 경우 쿼리에 포함할 수 있습니다. 필터를 결합할 때 AND 관계를 가정합니다. 즉, 엔티티가 응답에 포함되려면 모든 필터를 만족해야 합니다.

**세그먼트 ID에 대해 활성화된 모든 흐름 반환:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### 배열 속성에서 필터링 {#arrays}

배열 속성의 이름에 `[]`을 추가하여 배열 내의 항목의 속성을 기준으로 필터링할 수 있습니다.

**특정 소스 연결과 연결된 반환 흐름:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**특정 선택기 값 ID가 포함된 변환이 있는 반환 흐름:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**특정 값이 있는 열이 있는 소스 연결  `name` 반환:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**세그먼트 ID에서 필터링하여 대상에 대한 흐름 실행 ID를 조회합니다.**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

모든 필터링 쿼리는 `true` 값이 있는 `count` 쿼리 매개 변수와 함께 추가하여 결과 수를 반환할 수 있습니다. API 응답에는 필터링된 총 항목의 수를 나타내는 `count` 속성이 포함되어 있습니다. 필터링된 실제 항목은 이 호출에서 반환되지 않습니다.

**시스템에서 활성화된 흐름 수 반환:**

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

검색할 Flow Service 엔티티에 따라 필터링에 다른 속성을 사용할 수 있습니다. 아래 표는 필터링 사용 사례에 일반적으로 사용되는 각 리소스에 대한 루트 수준 필드를 분류합니다.

**`connectionSpec`**

| 속성 | 예 |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style=&quot;table-layout:auto&quot;}

**`flowSpec`**

| 속성 | 예 |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style=&quot;table-layout:auto&quot;}

**`connection`**

| 속성 | 예 |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style=&quot;table-layout:auto&quot;}

**`sourceConnection`**

| 속성 | 예 |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`targetConnection`**

| 속성 | 예 |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

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

{style=&quot;table-layout:auto&quot;}

**`run`**

| 속성 | 예 |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style=&quot;table-layout:auto&quot;}

## 다음 단계

이 안내서에서는 `orderby` 및 `property` 쿼리 매개 변수를 사용하여 Flow Service API에서 응답을 정렬 및 필터링하는 방법을 다룹니다. Platform에서 일반적인 워크플로우에 API를 사용하는 방법에 대한 단계별 안내서는 [sources](../../sources/home.md) 및 [대상](../../destinations/home.md) 설명서에 포함된 API 자습서를 참조하십시오.
