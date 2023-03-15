---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;흐름 서비스 API;소스;소스
title: 흐름 서비스 API를 사용하여 소스에 대한 행 수준 데이터 필터링
description: 이 자습서에서는 흐름 서비스 API를 사용하여 소스 수준에서 데이터를 필터링하는 방법에 대한 단계를 다룹니다
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# 를 사용하여 소스에 대한 행 수준 데이터 필터링 [!DNL Flow Service] API

>[!IMPORTANT]
>
>소스에 대한 행 수준 데이터 필터링 지원은 현재에만 사용할 수 있습니다. [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md) 및 [[!DNL Snowflake]](../../connectors/databases/snowflake.md) 소스.

이 자습서에서는 다음을 사용하여 소스에 대해 행 수준 데이터를 필터링하는 방법에 대한 단계를 제공합니다. [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 자습서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 잘 알고 있어야 합니다.

* [소스](../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../landing/api-guide.md).

## 소스 데이터 필터링

다음은 소스에 대한 행 수준 데이터를 필터링하기 위해 수행해야 하는 단계입니다.

### 연결 사양 조회

API를 사용하여 소스에 대한 행 수준 데이터를 필터링하려면 먼저 소스의 연결 사양 세부 정보를 검색하여 특정 소스가 지원하는 연산자 및 언어를 확인해야 합니다.

GET 지정된 소스의 연결 사양을 검색하려면 `/connectionSpecs` 의 엔드포인트 [!DNL Flow Service] 쿼리 매개변수의 일부로 소스의 속성 이름을 제공하는 동안 API입니다.

**API 형식**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMS}` | 결과를 필터링할 선택적 쿼리 매개 변수입니다. 다음을 검색할 수 있습니다. [!DNL Google BigQuery] 다음을 적용하여 연결 사양 `name` 속성 및 지정 `"google-big-query"` 을 클릭합니다. |

**요청**

다음 요청은 의 연결 사양을 검색합니다. [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 항목에 대한 연결 사양을 반환합니다. [!DNL Google BigQuery]지원되는 쿼리 언어 및 논리 연산자에 대한 정보를 포함합니다.

>[!NOTE]
>
>아래 API 응답은 간결성을 위해 잘립니다.

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| 속성 | 설명 |
| --- | --- |
| `attributes.filterAtSource.enabled` | 쿼리된 원본이 행 수준 데이터 필터링을 지원하는지 여부를 결정합니다. |
| `attributes.filterAtSource.queryLanguage` | 쿼리된 원본에서 지원하는 쿼리 언어를 결정합니다. |
| `attributes.filterAtSource.logicalOperators` | 소스에 대한 행 수준 데이터를 필터링하는 데 사용할 수 있는 논리 연산자를 결정합니다. |
| `attributes.filterAtSource.comparisonOperators` | 소스에 대해 행 수준 데이터를 필터링하는 데 사용할 수 있는 비교 연산자를 결정합니다. 비교 연산자에 대한 자세한 내용은 아래 표를 참조하십시오. |
| `attributes.filterAtSource.columnNameEscapeChar` | 열을 이스케이프 처리하는 데 사용할 문자를 결정합니다. |
| `attributes.filterAtSource.valueEscapeChar` | SQL 쿼리를 작성할 때 값을 묶는 방법을 결정합니다. |

{style="table-layout:auto"}

#### 비교 연산자

| 연산자 | 설명 |
| --- | --- |
| `==` | 속성이 제공된 값과 동일한지 여부를 기준으로 필터링합니다. |
| `!=` | 속성이 제공된 값과 같지 않은지 여부로 필터링합니다. |
| `<` | 속성이 제공된 값보다 작은지 여부를 기준으로 필터링합니다. |
| `>` | 속성이 제공된 값보다 큰지 여부를 기준으로 필터링합니다. |
| `<=` | 속성이 제공된 값보다 작거나 같은지 여부를 기준으로 필터링합니다. |
| `>=` | 속성이 제공된 값보다 크거나 같은지 여부를 기준으로 필터링합니다. |
| `like` | 에 사용되는 필터 `WHERE` 지정된 패턴을 검색하는 조건입니다. |
| `in` | 속성이 지정된 범위 내에 있는지 여부를 기준으로 필터링합니다. |

{style="table-layout:auto"}

### 수집을 위한 필터링 조건 지정

소스에서 지원하는 논리 연산자 및 쿼리 언어를 식별한 후에는 PQL(프로필 쿼리 언어)을 사용하여 소스 데이터에 적용할 필터링 조건을 지정할 수 있습니다.

아래 예에서는 매개 변수로 나열된 노드 유형에 대해 제공된 값과 동일한 선택 데이터에만 조건이 적용됩니다.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### 데이터 미리 보기

에 GET 요청을 하여 데이터를 미리 볼 수 있습니다. `/explore` 의 엔드포인트 [!DNL Flow Service] 제공하는 동안 API `filters` 를 쿼리 매개 변수의 일부로 사용하고에서 PQL 입력 조건을 지정합니다. [!DNL Base64].

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 소스의 기본 연결 ID입니다. |
| `{TABLE_PATH}` | 검사할 테이블의 경로 속성입니다. |
| `{FILTERS}` | 에 인코딩된 PQL 필터링 조건 [!DNL Base64]. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 요청은 다음 응답을 반환합니다.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

### 필터링된 데이터에 대한 소스 연결 만들기

POST 소스 연결을 만들고 필터링된 데이터를 수집하려면 `/sourceConnections` 필터링 조건을 본문 매개 변수의 일부로 제공하는 동안 끝점이 발생했습니다.

**API 형식**

```http
POST /sourceConnections
```

**요청**

다음 요청은 데이터를 수집할 소스 연결을 만듭니다 `test1.fasTestTable` 위치 `city` = `DDN`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

**응답**

성공적인 응답은 고유 식별자()를 반환합니다.`id`)을 참조하십시오.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## 부록

이 섹션에서는 필터링에 대한 다양한 페이로드의 추가 예를 제공합니다.

### 단일 조건

이니셜은 생략할 수 있습니다 `fnApply` 한 가지 조건만 필요한 시나리오의 경우.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

### 사용 `in` 연산자

연산자의 예는 아래 샘플 페이로드를 참조하십시오 `in`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

### 사용 `isNull` 연산자

연산자의 예는 아래 샘플 페이로드를 참조하십시오 `isNull`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

### 사용 `NOT` 연산자

연산자의 예는 아래 샘플 페이로드를 참조하십시오 `NOT`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

### 중첩된 조건이 있는 예

복잡한 중첩 조건의 예는 아래의 샘플 페이로드를 참조하십시오.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
