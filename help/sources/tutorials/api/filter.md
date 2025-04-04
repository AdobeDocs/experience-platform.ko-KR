---
title: 흐름 서비스 API를 사용하여 Source에 대한 행 수준 데이터 필터링
description: 이 자습서에서는 흐름 서비스 API를 사용하여 소스 수준에서 데이터를 필터링하는 방법에 대한 단계를 다룹니다
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1823'
ht-degree: 4%

---

# [!DNL Flow Service] API를 사용하여 소스에 대한 행 수준 데이터 필터링

>[!AVAILABILITY]
>
>행 수준 데이터 필터링에 대한 지원은 현재 다음 소스에서만 사용할 수 있습니다.
>
>* [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)
>* [[!DNL Marketo Engage] 표준 활동](../../connectors/adobe-applications/marketo/marketo.md)

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 소스에 대한 행 수준 데이터를 필터링하는 방법에 대한 단계는 이 안내서를 참조하십시오.

## 시작하기

이 자습서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 잘 알고 있어야 합니다.

* [원본](../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 소스 데이터 필터링 {#filter-source-data}

다음은 소스에 대한 행 수준 데이터를 필터링하기 위해 수행해야 하는 단계입니다.

### 연결 사양 검색 {#retrieve-your-connection-specs}

소스에 대한 행 수준 데이터를 필터링하는 첫 번째 단계는 소스의 연결 사양을 검색하고 소스가 지원하는 연산자 및 언어를 결정하는 것입니다.

지정된 소스의 연결 사양을 검색하려면 [!DNL Flow Service] API의 `/connectionSpecs` 끝점에 대한 GET 요청을 만들고 소스의 속성 이름을 쿼리 매개 변수의 일부로 제공합니다.

**API 형식**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| 매개변수 | 설명 |
| --- | --- |
| `{QUERY_PARAMS}` | 결과를 필터링할 선택적 쿼리 매개 변수입니다. `name` 속성을 적용하고 검색에서 `"google-big-query"`을(를) 지정하여 [!DNL Google BigQuery] 연결 사양을 검색할 수 있습니다. |

+++요청

다음 요청은 [!DNL Google BigQuery]의 연결 사양을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++응답

성공한 응답은 지원되는 쿼리 언어 및 논리 연산자에 대한 정보를 포함하여 [!DNL Google BigQuery]의 상태 코드 200과 연결 사양을 반환합니다.

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

+++

#### 비교 연산자 {#comparison-operators}

| 연산자 | 설명 |
| --- | --- |
| `==` | 속성이 제공된 값과 동일한지 여부를 기준으로 필터링합니다. |
| `!=` | 속성이 제공된 값과 같지 않은지 여부로 필터링합니다. |
| `<` | 속성이 제공된 값보다 작은지 여부를 기준으로 필터링합니다. |
| `>` | 속성이 제공된 값보다 큰지 여부를 기준으로 필터링합니다. |
| `<=` | 속성이 제공된 값보다 작거나 같은지 여부를 기준으로 필터링합니다. |
| `>=` | 속성이 제공된 값보다 크거나 같은지 여부를 기준으로 필터링합니다. |
| `like` | 지정된 패턴을 검색하기 위해 `WHERE` 절에 사용되어 필터링합니다. |
| `in` | 속성이 지정된 범위 내에 있는지 여부를 기준으로 필터링합니다. |

{style="table-layout:auto"}

### 수집을 위한 필터링 조건 지정 {#specify-filtering-conditions-for-ingestion}

소스에서 지원하는 논리 연산자 및 쿼리 언어를 식별한 후에는 Profile Query Language(PQL)를 사용하여 소스 데이터에 적용할 필터링 조건을 지정할 수 있습니다.

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

### 데이터 미리 보기 {#preview-your-data}

`filters`을(를) 쿼리 매개 변수의 일부로 제공하고 [!DNL Base64]에서 PQL 입력 조건을 지정하는 동안 [!DNL Flow Service] API의 `/explore` 끝점에 GET 요청을 수행하여 데이터를 미리 볼 수 있습니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 소스의 기본 연결 ID입니다. |
| `{TABLE_PATH}` | 검사할 테이블의 경로 속성입니다. |
| `{FILTERS}` | [!DNL Base64]에 인코딩된 PQL 필터링 조건입니다. |

+++요청

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++응답

성공적인 응답은 데이터의 내용과 구조를 반환합니다.

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

+++

### 필터링된 데이터에 대한 소스 연결 만들기

소스 연결을 만들고 필터링된 데이터를 수집하려면 `/sourceConnections` 끝점에 대한 POST 요청을 만들고 요청 본문 매개 변수에 필터링 조건을 제공합니다.

**API 형식**

```http
POST /sourceConnections
```

+++요청

다음 요청은 `city` = `DDN`인 `test1.fasTestTable`에서 데이터를 수집하기 위한 원본 연결을 만듭니다.

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

+++

+++응답

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

+++

## [!DNL Marketo Engage]에 대한 활동 엔터티 필터링 {#filter-for-marketo}

[[!DNL Marketo Engage] 소스 커넥터](../../connectors/adobe-applications/marketo/marketo.md)를 사용할 때 행 수준 필터링을 사용하여 활동 엔터티를 필터링할 수 있습니다. 현재 활동 엔티티와 표준 활동 유형에 대해서만 필터링할 수 있습니다. 사용자 지정 활동은 [[!DNL Marketo] 필드 매핑](../../connectors/adobe-applications/mapping/marketo.md)에서 계속 관리됩니다.

### [!DNL Marketo] 표준 활동 유형 {#marketo-standard-activity-types}

다음 표에서는 [!DNL Marketo]의 표준 활동 유형에 대해 설명합니다. 이 표를 필터링 기준에 대한 참조로 사용하십시오.

| 활동 유형 ID | 활동 유형 이름 |
| --- | --- |
| 1 | 웹 페이지 방문 |
| 2 | 양식 작성 |
| 3 | 링크 클릭 |
| 6 | 이메일 보내기 |
| 7 | 이메일 전달됨 |
| 8 | 반송된 이메일 |
| 9 | 이메일 구독 취소 |
| 10 | 이메일 열기 |
| 11 | 이메일 클릭 |
| 12 | 새 잠재 고객 |
| 21 | 잠재 고객 전환 |
| 22 | 점수 변경 |
| 24 | 목록에 추가 |
| 25 | 목록에서 제거 |
| 27 | 가볍게 반송된 이메일 |
| 32 | 잠재 고객 병합 |
| 34 | 영업 기회에 추가 |
| 35 | 영업 기회에서 제거 |
| 36 | 영업 기회 업데이트 |
| 46 | 즐거운 순간 |
| 101 | 수익 단계 변경 |
| 104 | 진행 상태 변경 |
| 110 | Webhook 호출 |
| 113 | 양육에 추가 |
| 114 | 육성 추적 변경 |
| 115 | 육성 케이던스 변경 |

{style="table-layout:auto"}

[!DNL Marketo] 소스 커넥터를 사용할 때 표준 활동 엔터티를 필터링하려면 아래 단계를 따르십시오.

### 초안 데이터 흐름 만들기

먼저 [[!DNL Marketo] 데이터 흐름](../ui/create/adobe-applications/marketo.md)을 만들고 초안으로 저장합니다. 초안 데이터 흐름을 만드는 방법에 대한 자세한 단계는 다음 설명서를 참조하십시오.

* [UI를 사용하여 데이터 흐름을 초안으로 저장](../ui/draft.md)
* [API를 사용하여 데이터 흐름을 초안으로 저장](../api/draft.md)

### 데이터 흐름 ID 검색

초안 데이터 흐름이 있는 경우 해당 ID를 검색해야 합니다.

UI에서 소스 카탈로그로 이동한 다음 상단 헤더에서 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택합니다. 상태 열을 사용하여 초안 모드로 저장된 모든 데이터 흐름을 식별한 다음 데이터 흐름의 이름을 선택합니다. 그런 다음 오른쪽의 **[!UICONTROL 속성]** 패널을 사용하여 데이터 흐름 ID를 찾습니다.

### 데이터 흐름 세부 정보 검색

다음으로, 데이터 흐름 세부 정보, 특히 데이터 흐름과 연관된 소스 연결 ID를 검색해야 합니다. 데이터 흐름 세부 정보를 검색하려면 `/flows` 끝점에 GET 요청을 만들고 데이터 흐름 ID를 경로 매개 변수로 제공하십시오.

**API 형식**

```http
GET /flows/{FLOW_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{FLOW_ID}` | 검색할 데이터 흐름의 ID입니다. |

+++요청

다음 요청은 데이터 흐름 ID `a7e88a01-40f9-4ebf-80b2-0fc838ff82ef`에 대한 정보를 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++응답

성공한 응답은 해당 소스 및 타겟 연결에 대한 정보를 포함하여 데이터 흐름 세부 정보를 반환합니다. 데이터 흐름을 게시하려면 소스 및 타겟 연결 ID가 나중에 필요하므로 이 값을 적어 두어야 합니다.

```json {line-numbers="true" start-line="1" highlight="23, 26"}
{
    "items": [
        {
            "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "createdAt": 1728592929650,
            "updatedAt": 1728597187444,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "Marketo Engage Standard Activities ACME",
            "description": "",
            "flowSpec": {
                "id": "15f8402c-ba66-4626-b54c-9f8e54244d61",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "etag": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "sourceConnectionIds": [
                "56f7eb3a-b544-4eaa-b167-ef1711044c7a"
            ],
            "targetConnectionIds": [
                "7e53e6e8-b432-4134-bb29-21fc6e8532e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
                        "connectionSpec": {
                            "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "0137118b-373a-4c4e-847c-13a0abf73b33",
                            "connectionSpec": {
                                "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "isSampleDataflow": false,
                "errorDiagnosticsEnabled": true
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingVersion": 0,
                        "mappingId": "f6447514ef95482889fac1818972e285"
                    }
                }
            ],
            "runs": "/runs?property=flowId==a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "lastOperation": {
                "started": 1728592929650,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "2d7863d5-ca4d-4313-ac52-2603eaf2cdbe",
                "state": "success",
                "startedAtUTC": 1728594713537,
                "completedAtUTC": 1728597183080
            },
            "labels": [],
            "recordTypes": [
                {
                    "type": "experienceevent",
                    "extensions": {}
                }
            ]
        }
    ]
}
```

+++

### 소스 연결 세부 정보 검색

그런 다음 소스 연결 ID를 사용하고 `/sourceConnections` 끝점에 대한 GET 요청을 만들어 소스 연결 세부 정보를 검색합니다.

**API 형식**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | 검색할 소스 연결의 ID입니다. |

+++요청

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++응답

성공한 응답은 소스 연결의 세부 정보를 반환합니다. 소스 연결을 업데이트하려면 다음 단계에서 이 값이 필요하므로 버전을 참고하십시오.

```json {line-numbers="true" start-line="1" highlight="30"}
{
    "items": [
        {
            "id": "b85b895f-a289-42e9-8fe1-ae448ccc7e53",
            "createdAt": 1729634331185,
            "updatedAt": 1729634331185,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "New Source Connection - 2024-10-23T03:28:50+05:30",
            "description": "Source connection created from the workflow",
            "baseConnectionId": "fd9f7455-1e23-4831-9283-7717e20bee40",
            "state": "draft",
            "data": {
                "format": "tabular",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                "version": "1.0"
            },
            "params": {
                "columns": [],
                "tableName": "Activity"
            },
            "version": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "etag": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "fd9f7455-1e23-4831-9283-7717e20bee40",
                    "connectionSpec": {
                        "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                        "version": "1.0"
                    }
                }
            },
            "lastOperation": {
                "started": 1729634331185,
                "updated": 0,
                "operation": "draft_create"
            }
        }
    ]
}
```

+++

### 필터링 조건으로 소스 연결 업데이트

이제 소스 연결 ID와 해당 버전이 있으므로 표준 활동 유형을 지정하는 필터 조건으로 PATCH 요청을 수행할 수 있습니다.

소스 연결을 업데이트하려면 `/sourceConnections` 끝점에 PATCH 요청을 만들고 소스 연결 ID를 쿼리 매개 변수로 제공하십시오. 또한 `If-Match` 헤더 매개 변수를 해당 소스 연결 버전과 함께 제공해야 합니다.

>[!TIP]
>
>PATCH 요청을 수행할 때 `If-Match` 헤더가 필요합니다. 이 헤더의 값은 업데이트하려는 데이터 흐름의 고유한 버전/태그입니다. 버전/etag 값은 데이터 흐름이 성공적으로 업데이트될 때마다 업데이트됩니다.

**API 형식**

```http
PATCH /sourceConnections/{SOURCE_CONNECTION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | 업데이트하려는 소스 연결의 ID |

+++요청

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: {VERSION_HERE}'
  -d '
      {
        "op": "add",
        "path": "/params/filters",
        "value": {
            "type": "PQL",
            "format": "pql/json",
            "value": {
                "nodeType": "fnApply",
                "fnName": "in",
                "params": [
                    {
                        "nodeType": "fieldLookup",
                        "fieldName": "activityType"
                    },
                    {
                        "nodeType": "literal",
                        "value": [
                            "Change Status in Progression",
                            "Fill Out Form"
                        ]
                    }
                ]
            }
        }
    }'
```

+++

+++응답

성공적인 응답은 소스 연결 ID 및 etag(버전)를 반환합니다.

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"210068a6-0000-0200-0000-6718201b0000\""
}
```

+++

### 소스 연결 게시

이제 소스 연결이 필터링 조건으로 업데이트되어 초안 상태에서 이동하고 소스 연결을 게시할 수 있습니다. 이렇게 하려면 `/sourceConnections` 끝점에 POST를 요청하고 초안 원본 연결의 ID와 게시를 위한 작업 작업을 제공합니다.

**API 형식**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| 매개변수 | 설명 |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | 게시할 소스 연결의 ID입니다. |
| `op` | 쿼리된 소스 연결의 상태를 업데이트하는 작업 작업입니다. 초안 원본 연결을 게시하려면 `op`을(를) `publish`(으)로 설정하십시오. |

+++요청

다음 요청은 초안 소스 연결을 게시합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++응답

성공적인 응답은 소스 연결 ID 및 etag(버전)를 반환합니다.

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"9f007f7b-0000-0200-0000-670ef1150000\""
}
```

+++

### 대상 연결 게시

이전 단계와 마찬가지로 대상 연결도 게시해야 초안 데이터 흐름을 진행하고 게시할 수 있습니다. `/targetConnections` 끝점에 대한 POST 요청을 만들고 게시하려는 초안 대상 연결의 ID와 게시를 위한 작업 작업을 제공합니다.

**API 형식**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| 매개변수 | 설명 |
| --- | --- |
| `{TARGET_CONNECTION_ID}` | 게시하려는 타겟 연결의 ID입니다. |
| `op` | 쿼리된 대상 연결의 상태를 업데이트하는 작업 작업입니다. 초안 대상 연결을 게시하려면 `op`을(를) `publish`(으)로 설정하십시오. |

+++요청

다음 요청은 ID가 `7e53e6e8-b432-4134-bb29-21fc6e8532e5`인 대상 연결을 게시합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/7e53e6e8-b432-4134-bb29-21fc6e8532e5/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++응답

성공적인 응답은 게시된 타겟 연결에 대한 ID 및 해당 etag를 반환합니다.

```json
{
    "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++


### 데이터 흐름 게시

이제 소스 및 타겟 연결이 모두 게시된 상태에서 마지막 단계로 진행하여 데이터 흐름을 게시할 수 있습니다. 데이터 흐름을 게시하려면 `/flows` 끝점에 POST 요청을 만들고 게시할 데이터 흐름 ID와 작업 작업을 제공하십시오.

**API 형식**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| 매개변수 | 설명 |
| --- | --- |
| `{FLOW_ID}` | 게시할 데이터 흐름의 ID입니다. |
| `op` | 쿼리된 데이터 흐름의 상태를 업데이트하는 작업 작업입니다. 초안 데이터 흐름을 게시하려면 `op`을(를) `publish`(으)로 설정하십시오. |

+++요청

다음 요청은 초안 데이터 흐름을 게시합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++응답

성공적인 응답은 ID와 데이터 흐름의 해당 `etag`을(를) 반환합니다.

```json
{
  "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
  "etag": "\"4b0354b7-0000-0200-0000-6716ce1f0000\""
}
```

+++

Experience Platform UI를 사용하여 초안 데이터 흐름이 게시되었는지 확인할 수 있습니다. 소스 카탈로그의 데이터 흐름 페이지로 이동하고 데이터 흐름의 **[!UICONTROL 상태]**&#x200B;를 참조하십시오. 성공하면 이제 상태가 **활성화됨**(으)로 설정됩니다.

>[!TIP]
>
>* 필터링이 활성화된 데이터 흐름은 한 번만 다시 채워집니다. 필터링 기준에서 수행하는 의 모든 변경 사항(추가 또는 제거)은 증분 데이터에만 적용할 수 있습니다.
>* 새 활동 유형에 대한 내역 데이터를 수집해야 하는 경우 새 데이터 흐름을 만들고 필터 조건에 적절한 활동 유형을 사용하여 필터링 기준을 정의하는 것이 좋습니다.
>* 사용자 지정 활동 유형을 필터링할 수 없습니다.
>* 필터링된 데이터는 미리 볼 수 없습니다.

## 부록

이 섹션에서는 필터링에 대한 다양한 페이로드의 추가 예를 제공합니다.

### 단일 조건

조건이 하나만 필요한 시나리오의 경우 초기 `fnApply`을(를) 생략할 수 있습니다.

+++예를 보려면 선택

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

+++

### `in` 연산자 사용

`in` 연산자의 예제를 보려면 아래 샘플 페이로드를 참조하십시오.

+++예를 보려면 선택

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

+++

### `isNull` 연산자 사용

+++예를 보려면 선택

`isNull` 연산자의 예제를 보려면 아래 샘플 페이로드를 참조하십시오.

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

+++

### `NOT` 연산자 사용

`NOT` 연산자의 예제를 보려면 아래 샘플 페이로드를 참조하십시오.


+++예를 보려면 선택

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

+++

### 중첩된 조건이 있는 예

복잡한 중첩 조건의 예는 아래의 샘플 페이로드를 참조하십시오.

+++예를 보려면 선택

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

+++