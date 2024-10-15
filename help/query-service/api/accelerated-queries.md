---
title: 가속화된 쿼리 끝점
description: 상태 비저장 방식으로 쿼리 가속 저장소에 액세스하여 집계된 데이터를 기반으로 결과를 빠르게 반환하는 방법을 알아봅니다. 이 문서에서는 쿼리 서비스 가속 쿼리 끝점에 대한 샘플 HTTP 요청 및 응답을 제공합니다.
role: Developer
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# 가속화된 쿼리 끝점

Data Distiller SKU의 일부로 [쿼리 서비스 API](https://developer.adobe.com/experience-platform-apis/references/query-service/)를 사용하면 상태 비저장 쿼리를 가속 스토어에 만들 수 있습니다. 반환된 결과는 집계된 데이터를 기반으로 합니다. 결과의 지연 시간이 줄어 보다 대화식 정보 교환이 가능합니다. 가속화된 쿼리 API는 [사용자 정의 대시보드](../../dashboards/standard-dashboards.md)를 제공하는 데에도 사용됩니다.

이 안내서를 계속하기 전에 쿼리 서비스 API를 성공적으로 사용하려면 [쿼리 서비스 API 안내서](./getting-started.md)를 읽고 이해했는지 확인하십시오.

## 시작하기

Data Distiller SKU는 쿼리 가속 스토어를 사용해야 합니다. Data Distiller SKU와 관련된 [패키징](../packaging.md) 및 [보호 기능](../guardrails.md#query-accelerated-store), [라이선스](../data-distiller/license-usage.md) 설명서를 참조하십시오. Data Distiller SKU가 없는 경우 Adobe 고객 서비스 담당자에게 자세한 내용을 문의하십시오.

다음 섹션에서는 쿼리 서비스 API를 통해 상태 비저장 방식으로 쿼리 가속 저장소에 액세스하는 데 필요한 API 호출에 대해 자세히 설명합니다. 각 호출에는 일반 API 형식, 필요한 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함됩니다.

## 가속화된 쿼리 실행 {#run-accelerated-query}

가속화된 쿼리를 실행하려면 `/accelerated-queries` 끝점에 POST을 요청하세요. 쿼리가 요청 페이로드에 직접 포함되거나 템플릿 ID로 참조됩니다.

**API 형식**

```shell
POST /accelerated-queries
```

### 요청

>[!IMPORTANT]
>
>`/accelerated-queries` 끝점에 대한 요청에는 SQL 문이나 템플릿 ID가 필요하지만 둘 다 필요하지는 않습니다. 요청에서 두 을(를) 모두 제출하면 오류가 발생합니다.

다음 요청은 요청 본문의 SQL 쿼리를 가속 저장소로 제출합니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "sql": "SELECT * FROM accounts;",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

이 대체 요청은 요청 본문의 템플릿 ID를 가속 저장소로 제출합니다. 해당 템플릿의 SQL을 사용하여 가속화된 저장소를 쿼리합니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "templateId": "5d8228e7-4200-e3de-11e9-7f27416c5f0d",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

| 속성 | 설명 |
|---|---|
| `dbName` | 가속화된 쿼리를 만드는 데이터베이스의 이름입니다. `dbName`의 값은 `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}` 형식을 사용해야 합니다. 제공된 데이터베이스가 가속화된 저장소 내에 있어야 합니다. 그렇지 않으면 요청에서 오류가 발생합니다. 또한 `dbName`의 `x-sandbox-name` 헤더와 샌드박스 이름이 동일한 샌드박스를 참조하는지 확인해야 합니다. |
| `sql` | SQL 문 문자열입니다. 허용되는 최대 크기는 1000000자입니다. |
| `templateId` | `/templates` 끝점에 대한 POST 요청이 수행될 때 만들어져 템플릿으로 저장되는 쿼리의 고유 식별자입니다. |
| `name` | 가속화된 쿼리에 대한 사람 친화적인 수사적 이름(선택 사항)입니다. |
| `description` | 다른 사용자가 쿼리의 목적을 이해할 수 있도록 쿼리의 의도에 대한 선택적 주석입니다. 허용되는 최대 크기는 1000바이트입니다. |

**응답**

성공한 응답은 쿼리에서 만든 임시 스키마와 함께 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>다음 응답은 간결성을 위해 잘렸습니다.

```json
{
  "queryId": "315a0a66-0fbb-4810-bc30-484cea5e0f1e",
  "resultsMeta": {
    "_adhoc": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
                "Units": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_name_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_code": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_name": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_aggregation_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Value": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Year": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_category": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_ANZSIC06": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                }
            }
        }
    },
  "results": [
     {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H26",
            "Variable_name": "Fixed tangible assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "282",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H27",
            "Variable_name": "Additions to fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "35",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H28",
            "Variable_name": "Disposals of fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "9",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        ...
    ],
  "request": {
    "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
    "sql": "SELECT * FROM accounts;",
    "name": "Sample Accelerated Query",
    "description": "A sample of an accelerated query."
  }
}
```

| 속성 | 설명 |
|---|---|
| `queryId` | 생성된 쿼리의 ID 값입니다. |
| `resultsMeta` | 이 개체에는 결과에 반환되는 각 열의 메타데이터가 포함되어 있으므로 사용자가 각 열의 이름과 유형을 알 수 있습니다. |
| `resultsMeta._adhoc` | 단일 데이터 세트에서만 사용할 수 있도록 네임스페이스가 지정된 필드가 있는 임시 경험 데이터 모델(XDM) 스키마. |
| `resultsMeta._adhoc.type` | Ad Hoc 스키마의 데이터 유형입니다. |
| `resultsMeta._adhoc.meta:xdmType` | XDM 필드 유형에 대해 시스템에서 생성한 값입니다. 사용 가능한 형식에 대한 자세한 내용은 [사용 가능한 XDM 형식](../../xdm/tutorials/custom-fields-api.md)에 대한 설명서를 참조하십시오. |
| `resultsMeta._adhoc.properties` | 쿼리된 데이터 세트의 열 이름입니다. |
| `resultsMeta._adhoc.results` | 쿼리된 데이터 세트의 행 이름입니다. 반환된 각 열이 반영됩니다. |
