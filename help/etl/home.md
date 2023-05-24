---
keywords: Experience Platform;홈;인기 항목;ETL;etl;etl 통합;ETL 통합
solution: Experience Platform
title: Adobe Experience Platform용 ETL 통합 개발
description: ETL 통합 안내서에서는 데이터를 플랫폼에 Experience Platform 및 수집할 수 있는 고성능 보안 커넥터를 만드는 일반적인 단계를 간략하게 설명합니다.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '4081'
ht-degree: 1%

---

# Adobe Experience Platform용 ETL 통합 개발

ETL 통합 안내서에서는 다음을 위한 고성능, 보안 커넥터를 만드는 일반적인 단계를 간략하게 설명합니다. [!DNL Experience Platform] 및 데이터 수집 대상 [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Experience Platform API에 대한 인증 및 인증](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

이 안내서에는 ETL 커넥터를 디자인할 때 사용할 샘플 API 호출과 각 ETL 커넥터를 간략하게 설명하는 설명서 링크도 포함되어 있습니다 [!DNL Experience Platform] 서비스 및 해당 API 사용에 대해 자세히 알아보십시오.

샘플 통합은에서 사용할 수 있습니다. [!DNL GitHub] 를 통해 [ETL 에코시스템 통합 참조 코드](https://github.com/adobe/acp-data-services-etl-reference) 다음 아래에 [!DNL Apache] 라이선스 버전 2.0.

## 워크플로

다음 워크플로우 다이어그램은 Adobe Experience Platform 구성 요소와 ETL 애플리케이션 및 커넥터의 통합에 대한 높은 수준의 개요를 제공합니다.

![](images/etl.png)

## Adobe Experience Platform 구성 요소

ETL 커넥터 통합과 관련된 여러 Experience Platform 구성 요소가 있습니다. 다음 목록에서는 몇 가지 주요 구성 요소 및 기능에 대해 간략히 설명합니다.

- **Adobe Identity Management 시스템(IMS)** - Adobe 서비스에 대한 인증을 위한 프레임워크를 제공합니다.
- **IMS 조직** - 제품 및 서비스를 소유 또는 라이선스할 수 있고 해당 구성원에 대한 액세스를 허용할 수 있는 법인
- **IMS 사용자** - IMS 조직의 구성원. 조직 대 사용자 관계는 다대다수입니다.
- **[!DNL Sandbox]** - 단일 가상 파티션 [!DNL Platform] 예를 들어 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 됩니다.
- **데이터 검색** - 수집 및 변환된 데이터의 메타데이터 기록 [!DNL Experience Platform].
- **[!DNL Data Access]** - 사용자가에서 데이터에 액세스할 수 있는 인터페이스를 제공합니다. [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - 데이터를 로 푸시 [!DNL Experience Platform] 포함 [!DNL Data Ingestion] API.
- **[!DNL Schema Registry]** - 사용할 데이터 구조를 설명하는 스키마를 정의하고 저장합니다. [!DNL Experience Platform].

## 시작하기 [!DNL Experience Platform] API

다음 섹션에서는 을 성공적으로 호출하기 위해 알고 있거나 보유하고 있어야 하는 추가 정보를 제공합니다. [!DNL Experience Platform] API.

### 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값 수집

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

## 일반 사용자 흐름

시작하려면 ETL 사용자가 [!DNL Experience Platform] UI(사용자 인터페이스) 및 표준 커넥터 또는 푸시 서비스 커넥터를 사용하여 수집할 데이터 세트를 만듭니다.

UI에서 사용자는 데이터 세트 스키마를 선택하여 출력 데이터 세트를 만듭니다. 스키마의 선택은 수집하는 데이터 유형(레코드 또는 시계열)에 따라 다릅니다 [!DNL Platform]. UI 내의 스키마 탭을 클릭하면 스키마가 지원하는 동작 유형을 포함하여 사용 가능한 모든 스키마를 볼 수 있습니다.

ETL 도구에서 사용자는 자격 증명을 사용하여 적절한 연결을 구성한 후 매핑 변형 디자인을 시작합니다. ETL 도구는 이미 다음과 같은 기능이 있다고 가정합니다. [!DNL Experience Platform] 설치된 커넥터(이 통합 안내서에 정의되지 않은 프로세스)

샘플 ETL 도구 및 워크플로에 대한 모크업이 [ETL 워크플로우](./workflow.md). ETL 도구는 형식이 다를 수 있지만 대부분의 경우 유사한 기능을 제공합니다.

>[!NOTE]
>
>ETL 커넥터는 데이터 및 오프셋을 수집할 날짜를 표시하는 타임스탬프 필터를 지정해야 합니다(예: 데이터를 읽을 창입니다). ETL 도구는 이 UI 또는 다른 관련 UI에서 이러한 두 매개 변수를 사용할 수 있도록 지원해야 합니다. Adobe Experience Platform에서 이러한 매개 변수는 사용 가능한 날짜(있는 경우) 또는 데이터 세트의 배치 개체에 있는 캡처된 날짜에 매핑됩니다.

### 데이터 세트 목록 보기

매핑에 데이터 소스를 사용하여 사용 가능한 모든 데이터 세트 목록을 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

사용 가능한 모든 데이터 세트를 보기 위해 단일 API 요청을 실행할 수 있습니다(예: `GET /dataSets`)를 설정하는 것이 좋습니다. 여기서 가장 좋은 방법은 응답의 크기를 제한하는 쿼리 매개 변수를 포함하는 것입니다.

전체 데이터 세트 정보가 요청되는 경우 응답 페이로드의 크기가 3GB를 초과할 수 있으므로 전체 성능이 저하될 수 있습니다. 따라서 쿼리 매개 변수를 사용하여 필요한 정보만 필터링하면 [!DNL Catalog] 쿼리의 효율성이 향상됩니다.

#### 목록 필터링

응답을 필터링할 때 앰퍼샌드( )로 매개 변수를 분리하여 단일 호출에 여러 필터를 사용할 수 있습니다.`&`). 일부 쿼리 매개 변수는 아래 샘플 요청의 &quot;속성&quot; 필터와 같이, 쉼표로 구분된 값 목록을 허용합니다.

[!DNL Catalog] 응답은 구성된 제한에 따라 자동으로 측정되지만, &quot;limit&quot; 쿼리 매개 변수를 사용하여 제약 조건을 사용자 지정하고 반환되는 개체 수를 제한할 수 있습니다. 사전 구성됨 [!DNL Catalog] 응답 제한:

- 제한 매개 변수를 지정하지 않으면 응답 페이로드당 최대 개체 수는 20개입니다.
- 다른 모든 항목에 대한 전역 제한 [!DNL Catalog] 쿼리는 100개의 개체입니다.
- 데이터 세트 쿼리의 경우 속성 쿼리 매개 변수를 사용하여 observableSchema가 요청되면 반환되는 최대 데이터 세트 수는 20개입니다.
- 잘못된 제한 매개변수(포함) `limit=0`)에는 적절한 범위를 윤곽선으로 표시하는 HTTP 400 오류가 표시됩니다.
- 제한이나 오프셋이 쿼리 매개 변수로 전달되면 헤더로 전달된 것보다 우선합니다.

쿼리 매개변수에 대해서는 다음에서 자세히 설명합니다. [카탈로그 서비스 개요](../catalog/home.md).

**API 형식**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

다음을 참조하십시오. [카탈로그 서비스 개요](../catalog/home.md) 을 호출하는 방법에 대한 자세한 예는 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**응답**

응답에는 3개(`limit=3`)에 표시된 대로 &quot;name&quot;, &quot;description&quot; 및 &quot;schemaRef&quot;를 보여주는 데이터 세트 `properties` 쿼리 매개 변수.

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### 데이터 세트 스키마 보기

데이터 세트의 &quot;schemaRef&quot; 속성은 데이터 세트가 기반으로 하는 XDM 스키마를 참조하는 URI를 포함합니다. XDM 스키마(&quot;schemaRef&quot;)는 데이터 세트에서 사용할 수 있는 모든 잠재적 필드를 나타내며 사용 중인 필드일 필요는 없습니다(아래 &quot;observableSchema&quot; 참조).

XDM 스키마는 쓸 수 있는 모든 사용 가능한 필드 목록을 사용자에게 제시해야 할 때 사용하는 스키마입니다.

이전 응답 개체의 첫 번째 &quot;schemaRef.id&quot; 값(`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`)는에서 특정 XDM 스키마를 가리키는 URI입니다 [!DNL Schema Registry]. 스키마에 대한 조회(GET) 요청을 수행하여 스키마를 검색할 수 있습니다. [!DNL Schema Registry] API.

>[!NOTE]
>
>이제 더 이상 사용되지 않는 &quot;schema&quot; 속성을 &quot;schemaRef&quot; 속성으로 바꿉니다. 데이터 세트에 &quot;schemaRef&quot;가 없거나 값을 포함하지 않으면 &quot;schema&quot; 속성이 있는지 확인해야 합니다. 이 작업은 의 &quot;schemaRef&quot;를 &quot;schema&quot;로 교체하여 수행할 수 있습니다. `properties` 이전 호출의 쿼리 매개 변수입니다. &quot;스키마&quot; 속성에 대한 자세한 내용은 [데이터 세트 &quot;스키마&quot; 속성](#dataset-schema-property-deprecated---eol-2019-05-30) 다음 섹션.

**API 형식**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**요청**

요청은 인코딩된 URL을 사용합니다 `id` 스키마(&quot;schemaRef.id&quot; 특성 값)의 URI이며 Accept 헤더가 필요합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

응답 형식은 요청에서 전송된 Accept 헤더 유형에 따라 다릅니다. 조회 요청에는 `version` Accept 헤더에 포함됩니다. 다음 표에서는 조회에 사용 가능한 Accept 헤더를 간략하게 설명합니다.

| Accept | 설명 |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | (GET) 요청, 제목, ID 및 버전 나열 |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs 및 allOf resolved, 제목 및 설명 포함 |
| `application/vnd.adobe.xed+json; version={major version}` | $ref 및 allOf가 있는 Raw에 제목 및 설명이 있음 |
| `application/vnd.adobe.xed-notext+json; version={major version}` | $ref 및 allOf가 있는 Raw, 제목 또는 설명 없음 |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs 및 allOf resolved, 제목 또는 설명 없음 |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs 및 allOf 해결됨, 설명자가 포함됨 |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` 및 `application/vnd.adobe.xed-full+json; version={major version}` 는 가장 일반적으로 사용되는 Accept 헤더입니다. `application/vnd.adobe.xed-id+json` 는에서 리소스를 나열하는 데 선호됩니다. [!DNL Schema Registry] 따라서 &quot;title&quot;, &quot;id&quot; 및 &quot;version&quot;만 반환됩니다. `application/vnd.adobe.xed-full+json; version={major version}` 는 제목 및 설명뿐만 아니라 모든 필드(&quot;속성&quot; 아래에 중첩된)를 반환하므로 특정 리소스(&quot;id&quot;로 표시)를 보는 데 선호됩니다.

**응답**

반환되는 JSON 스키마는 구조 및 필드 수준 정보(&quot;type&quot;, &quot;format&quot;, &quot;minimum&quot;, &quot;maximum&quot; 등)를 설명합니다. JSON으로 일련화된 데이터의. 수집에 JSON 이외의 직렬화 형식을 사용하는 경우(예: Parquet 또는 Scala), [스키마 레지스트리 안내서](../xdm/tutorials/create-schema-api.md) 에는 원하는 JSON 유형(&quot;meta:xdmType&quot;) 및 해당 표현을 다른 형식으로 표시하는 테이블이 포함되어 있습니다.

이 테이블과 함께 [!DNL Schema Registry] 개발자 안내서에는 를 사용하여 수행할 수 있는 모든 호출에 대한 심층적인 예가 포함되어 있습니다. [!DNL Schema Registry] API.

### 데이터 세트 &quot;스키마&quot; 속성(더 이상 사용되지 않음 - EOL 2019-05-30)

데이터 세트에는 이제 더 이상 사용되지 않으며 이전 버전과의 호환성을 위해 일시적으로 사용할 수 있는 &quot;스키마&quot; 속성이 포함될 수 있습니다. 예를 들어 이전에 수행한 요청과 유사한 목록(GET) 요청이 있습니다. 여기서 &quot;schema&quot;는 의 &quot;schemaRef&quot;로 대체되었습니다. `properties` 쿼리 매개 변수에서 다음을 반환할 수 있습니다.

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

데이터 세트의 &quot;schema&quot; 속성이 채워지면 스키마가 더 이상 사용되지 않음을 나타냅니다 `/xdms` 스키마 및 지원되는 경우 ETL 커넥터는 &quot;스키마&quot; 속성의 값을 `/xdms` 끝점(에서 더 이상 사용되지 않는 끝점) [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/))을 클릭하여 기존 스키마를 검색합니다.

**API 형식**

```http
GET /catalog/{"schema" property without the "@"}
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>선택적 쿼리 매개 변수, `expansion=xdm`는 API에 참조된 모든 스키마를 완전히 확장 및 인라인하도록 알려줍니다. 모든 잠재적 필드 목록을 사용자에게 제공할 때 이 작업을 수행할 수 있습니다.

**응답**

의 단계와 유사합니다. [데이터 세트 스키마 보기](#view-dataset-schema), 응답에는 JSON으로 직렬화된 데이터의 구조 및 필드 수준 정보를 설명하는 JSON 스키마가 포함되어 있습니다.

>[!NOTE]
>
>&quot;스키마&quot; 필드가 비어 있거나 완전히 없는 경우 커넥터는 &quot;schemaRef&quot; 필드를 읽고 다음을 사용해야 합니다. [스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) 의 이전 단계에 표시된 대로 [데이터 세트 스키마 보기](#view-dataset-schema).

### &quot;observableSchema&quot; 속성

데이터 세트의 &quot;observableSchema&quot; 속성에는 XDM 스키마 JSON의 구조와 일치하는 JSON 구조가 있습니다. &quot;observableSchema&quot;에는 들어오는 입력 파일에 있었던 필드가 포함되어 있습니다. 에 데이터를 쓸 때 [!DNL Experience Platform]: 사용자가 대상 스키마의 모든 필드를 사용할 필요는 없습니다. 대신 사용 중인 필드만 제공해야 합니다.

관찰 가능한 스키마는 데이터를 읽거나 읽기/매핑할 수 있는 필드 목록을 표시할 때 사용할 스키마입니다.

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### 데이터 미리보기

ETL 애플리케이션은 데이터를 미리 볼 수 있는 기능을 제공할 수 있습니다([ETL 워크플로의 &quot;그림 8&quot;](./workflow.md)). 데이터 액세스 API는 데이터를 미리 볼 수 있는 몇 가지 옵션을 제공합니다.

데이터 액세스 API를 사용하여 데이터를 미리 보기 위한 단계별 지침을 비롯한 추가 정보는 [데이터 액세스 자습서](../data-access/tutorials/dataset-data.md).

### &quot;속성&quot; 쿼리 매개 변수를 사용하여 데이터 세트 세부 정보 가져오기

위의 단계에 표시된 대로 [데이터 세트 목록 보기](#view-list-of-datasets), &quot;properties&quot; 쿼리 매개 변수를 사용하여 &quot;files&quot;를 요청할 수 있습니다.

다음을 참조하십시오. [카탈로그 서비스 개요](../catalog/home.md) 데이터 세트 쿼리 및 사용 가능한 응답 필터에 대한 자세한 정보.

**API 형식**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**응답**

응답에는 하나의 데이터 세트(`limit=1`) &quot;files&quot; 속성을 표시합니다.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### &quot;files&quot; 속성을 사용하여 데이터 세트 파일 나열

GET 요청을 사용하여 &quot;files&quot; 속성을 사용하여 파일 세부 정보를 가져올 수도 있습니다.

**API 형식**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**응답**

응답에는 데이터 세트 파일 ID가 최상위 속성으로 포함되며, 파일 세부 정보는 데이터 세트 파일 ID 개체 내에 포함됩니다.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### 파일 세부 정보 가져오기

이전 응답에서 반환된 데이터 세트 파일 ID는 GET 요청에서 를 통해 추가 파일 세부 정보를 가져오는 데 사용할 수 있습니다. [!DNL Data Access] API.

다음 [데이터 액세스 개요](../data-access/home.md) 사용 방법에 대한 세부 정보를 포함합니다. [!DNL Data Access] API.

**API 형식**

```http
GET /export/files/{DATASET_FILE_ID}
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**응답**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### 파일 데이터 미리 보기

&quot;href&quot; 속성을 사용하여 를 통해 미리보기 데이터를 가져올 수 있습니다. [[!DNL Data Access API]](../data-access/home.md).

**API 형식**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

위의 요청에 대한 응답에는 파일 내용의 미리보기가 포함됩니다.

다음에 대한 추가 정보: [!DNL Data Access] 자세한 요청 및 응답을 포함한 API는 [데이터 액세스 개요](../data-access/home.md).

### 데이터 세트에서 &quot;fileDescription&quot; 가져오기

대상 구성 요소는 변환된 데이터의 출력으로, 데이터 엔지니어는 출력 데이터 세트 를 선택합니다([ETL 워크플로우의 &quot;그림 12&quot;](workflow.md)). XDM 스키마는 출력 데이터 세트와 연결됩니다. 기록할 데이터는 데이터 검색 API에서 데이터 세트 엔티티의 &quot;fileDescription&quot; 속성으로 식별됩니다. 이 정보는 데이터 세트 ID( )를 사용하여 가져올 수 있습니다.`{DATASET_ID}`). JSON 응답의 &quot;fileDescription&quot; 속성은 요청된 정보를 제공합니다.

**API 형식**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{DATASET_ID}` | 다음 `id` 액세스하려는 데이터 세트의 값입니다. |

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**응답**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

데이터가 다음에 기록됩니다. [!DNL Experience Platform] 사용 [일괄 처리 수집 API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  데이터 쓰기는 비동기 프로세스입니다. 데이터가 Adobe Experience Platform에 기록되면 데이터가 완전히 기록된 후에만 배치가 만들어지고 성공으로 표시됩니다.

데이터 입력 [!DNL Experience Platform] Parquet 파일 형식으로 작성해야 합니다.

## 실행 단계

실행이 시작되면 커넥터(소스 구성 요소에 정의된 대로)가 의 데이터를 읽습니다. [!DNL Experience Platform] 사용 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). 변환 프로세스는 특정 시간 범위 동안의 데이터를 읽게 됩니다. 내부적으로 소스 데이터 세트의 배치를 쿼리합니다. 쿼리하는 동안 매개 변수가 있는(시계열 데이터 또는 증분 데이터에 대한 롤링) 시작 날짜를 사용하고 이러한 배치에 대한 데이터 세트 파일을 나열하고 해당 데이터 세트 파일에 대한 데이터 요청을 시작합니다.

### 예제 변형

다음 [샘플 ETL 변형](./transformations.md) 문서에는 id 처리 및 데이터 유형 매핑을 포함한 많은 예제 변형이 포함되어 있습니다. 이러한 변환을 참조에 사용하십시오.

### 데이터 읽기 [!DNL Experience Platform]

사용 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/), 지정된 시작 시간과 종료 시간 사이의 모든 배치를 가져오고, 만들어진 순서대로 정렬할 수 있습니다.

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

일괄 처리 필터링에 대한 자세한 내용은 [데이터 액세스 자습서](../data-access/tutorials/dataset-data.md).

### 배치에서 파일 가져오기

배치에 대한 ID가 있는 경우 (`{BATCH_ID}`)를 통해 특정 배치에 속한 파일 목록을 검색할 수 있습니다. [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  자세한 내용은 [[!DNL Data Access] 튜토리얼](../data-access/tutorials/dataset-data.md).

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### 파일 ID를 사용하여 파일 액세스

파일의 고유 ID 사용(`{FILE_ID`), [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 는 파일 이름, 크기(바이트) 및 다운로드 링크를 포함하여 파일의 특정 세부 정보에 액세스하는 데 사용할 수 있습니다.

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

응답이 단일 파일 또는 디렉토리를 가리킬 수 있습니다. 각각에 대한 자세한 내용은 [[!DNL Data Access] 튜토리얼](../data-access/tutorials/dataset-data.md).

### 파일 컨텐츠 액세스

다음 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 를 사용하여 특정 파일의 내용에 액세스할 수 있습니다. 콘텐츠를 가져오려면에 대해 반환된 값을 사용하여 GET 요청이 수행됩니다 `_links.self.href` 파일 ID를 사용하여 파일에 액세스할 때.

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

이 요청에 대한 응답에는 파일의 내용이 포함됩니다. 응답 페이지 매김에 대한 세부 사항을 포함한 자세한 내용은 [데이터 액세스 API를 통해 데이터를 쿼리하는 방법](../data-access/tutorials/dataset-data.md) 튜토리얼.

### 스키마 규정 준수에 대한 레코드 유효성 검사

데이터가 작성될 때 사용자는 XDM 스키마에 정의된 유효성 검사 규칙에 따라 데이터의 유효성을 검사하도록 선택할 수 있습니다. 스키마 유효성 검사에 대한 자세한 내용은 [의 ETL 생태계 통합 참조 코드 [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

에 있는 참조 구현을 사용하는 경우 [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), 시스템 속성을 사용하여 이 구현에서 스키마 유효성 검사를 켤 수 있습니다 `-DenableSchemaValidation=true`.

논리적 XDM 유형에 대해 다음과 같은 속성을 사용하여 유효성 검사를 수행할 수 있습니다. `minLength` 및 `maxlength` 문자열의 경우 `minimum` 및 `maximum` 정수 등에 사용됩니다. 다음 [스키마 레지스트리 API 개발자 안내서](../xdm/api/getting-started.md) 유효성 검사에 사용할 수 있는 XDM 유형 및 속성을 대략적으로 보여 주는 표를 포함합니다.

>[!NOTE]
>
>다양한 용도로 제공된 최소값 및 최대값 `integer` 유형은 유형이 지원할 수 있는 MIN 및 MAX 값이지만 이러한 값은 선택한 최소 및 최대값으로 추가로 제한될 수 있습니다.

### 일괄 처리 만들기

데이터가 처리되면 ETL 툴은 데이터를에 다시 기록합니다 [!DNL Experience Platform] 사용 [일괄 처리 수집 API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). 데이터를 데이터 세트에 추가하려면 먼저 나중에 특정 데이터 세트에 업로드되는 배치에 연결해야 합니다.

**요청**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

샘플 요청 및 응답을 포함하여 배치를 만들기 위한 세부 사항은 [일괄 처리 수집 개요](../ingestion/batch-ingestion/overview.md).

### 데이터 세트에 쓰기

새 배치를 성공적으로 만든 후 파일을 특정 데이터 세트에 업로드할 수 있습니다. 승격될 때까지 배치에 여러 파일을 게시할 수 있습니다. Small File Upload API를 사용하여 파일을 업로드할 수 있습니다. 그러나 파일이 너무 크고 게이트웨이 제한이 초과된 경우 Large File Upload API를 사용할 수 있습니다. 대용량 및 소규모 파일 업로드 사용에 대한 자세한 내용은 [일괄 처리 수집 개요](../ingestion/batch-ingestion/overview.md).

**요청**

데이터 입력 [!DNL Experience Platform] Parquet 파일 형식으로 작성해야 합니다.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### 일괄 업로드 완료 표시

모든 파일이 배치에 업로드되면 배치를 완료하라는 신호를 보낼 수 있습니다. 이렇게 하면 [!DNL Catalog] 완료된 파일에 대해 &quot;DataSetFile&quot; 항목이 생성되고 배치 생성과 연결됩니다. 다음 [!DNL Catalog] 그런 다음 배치가 성공으로 표시되며, 이는 다운스트림 흐름을 트리거하여 사용 가능한 데이터를 수집합니다.

데이터는 먼저 Adobe Experience Platform의 스테이징 위치에 도착한 다음, 카탈로그 작성 및 유효성 검사 후 최종 위치로 이동됩니다. 모든 데이터가 영구 위치로 이동되면 배치가 성공한 것으로 표시됩니다.

**요청**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

성공하면 응답은 HTTP 상태 200 OK를 반환하고 응답 본문은 비어 있습니다.

ETL 도구는 데이터를 읽을 때 소스 데이터 세트의 타임스탬프를 기억해야 합니다.

다음 변환 실행에서, 일정 또는 이벤트 호출에 의해 발생할 수 있으므로, ETL은 이전에 저장된 타임스탬프에서 데이터 요청을 시작하고 앞으로 모든 데이터를 요청합니다.

### 마지막 배치 상태 가져오기

ETL 도구에서 새 작업을 실행하기 전에 마지막 배치가 성공적으로 완료되었는지 확인해야 합니다. 다음 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 관련 배치의 세부 정보를 제공하는 배치별 옵션을 제공합니다.

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**응답**

이전 배치 &quot;상태&quot; 값이 아래와 같이 &quot;성공&quot;인 경우 새 작업을 예약할 수 있습니다.

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### ID별 마지막 배치 상태 가져오기

다음을 통해 개별 배치 상태를 검색할 수 있습니다. [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 를 사용하여 GET 요청 발행 `{BATCH_ID}`. 다음 `{BATCH_ID}` 는 배치가 생성될 때 반환된 ID와 동일합니다.

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**응답 - 성공**

다음 응답은 &quot;성공&quot;을 보여 줍니다.

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**응답 - 실패**

오류가 발생한 경우 응답에서 &quot;오류&quot;를 추출하여 ETL 도구에 오류 메시지로 표시될 수 있습니다.

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## 증분 및 스냅샷 데이터, 이벤트 및 프로필 비교

데이터는 다음과 같이 2x2 행렬로 나타낼 수 있습니다.

| 증분 이벤트 | 증분 프로필 |
|-------------------------------|----------------------|
| 스냅샷 이벤트(가능성 낮음) | 스냅샷 프로필 |

이벤트 데이터는 일반적으로 각 행에 색인화된 타임스탬프 열이 있는 경우에 사용됩니다.

프로필 데이터는 일반적으로 데이터에 타임스탬프가 없고 각 행을 기본/복합 키로 식별할 수 있는 경우에 사용됩니다.

증분 데이터는 새 데이터 또는 업데이트된 데이터만 시스템으로 들어와 데이터 세트의 현재 데이터에 추가합니다.

스냅샷 데이터는 모든 데이터가 시스템으로 유입되어 데이터 세트의 일부 또는 모든 이전 데이터를 대체하는 경우입니다.

증분 이벤트의 경우 ETL 도구는 배치 엔티티의 사용 가능한 날짜/생성 날짜를 사용해야 합니다. 푸시 서비스의 경우 사용 가능한 날짜가 표시되지 않으므로 도구에서는 표시 증분을 위해 일괄적으로 생성/업데이트된 날짜를 사용합니다. 모든 증분 이벤트 일괄 처리를 처리해야 합니다.

증분 프로필의 경우 ETL 도구는 배치 엔티티의 생성/업데이트 날짜를 사용합니다. 일반적으로 증분 프로필 데이터의 모든 배치를 처리해야 합니다.

스냅샷 이벤트는 데이터의 엄청난 크기로 인해 발생할 가능성이 매우 낮습니다. 그러나 이 작업이 필요한 경우 ETL 도구는 처리를 위해 마지막 배치만 선택해야 합니다.

스냅샷 프로필을 사용하는 경우 ETL 도구는 시스템에 도착한 데이터의 마지막 배치를 선택해야 합니다. 그러나 변경 사항의 버전을 추적해야 하는 경우에는 모든 일괄 처리를 처리해야 합니다. ETL 프로세스 내에서 데이터 중복 제거 처리를 수행하면 스토리지 비용을 제어하는 데 도움이 됩니다.

## 일괄 재생 및 데이터 재처리

클라이언트가 지난 &#39;n&#39;일 동안 ETL 처리 중인 데이터가 예상대로 발생하지 않았거나 소스 데이터 자체가 올바르지 않을 수 있음을 발견한 경우 배치 재생 및 데이터 재처리가 필요할 수 있습니다.

이를 위해 클라이언트의 데이터 관리자는 [!DNL Platform] 손상된 데이터가 포함된 배치를 제거하는 UI. 그런 다음 ETL을 다시 실행해야 하므로 올바른 데이터로 다시 채워집니다. 소스 자체에 손상된 데이터가 있는 경우 데이터 엔지니어/관리자는 소스 배치를 수정하고 데이터를 다시 수집해야 합니다(Adobe Experience Platform 또는 ETL 커넥터를 통해).

생성되는 데이터 유형에 따라 특정 데이터 세트에서 단일 배치 또는 모든 배치를 제거하는 것은 데이터 엔지니어의 선택입니다. 다음과같이 데이터가 제거/보관됩니다. [!DNL Experience Platform] 지침.

데이터를 제거하는 ETL 기능이 중요해질 가능성이 높은 시나리오입니다.

제거가 완료되면 클라이언트 관리자는 일괄 처리가 삭제된 시점부터 핵심 서비스에 대한 처리를 다시 시작하도록 Adobe Experience Platform을 다시 구성해야 합니다.

## 일괄 처리 동시 실행

데이터 관리자/엔지니어는 클라이언트의 판단에 따라 특정 데이터 세트의 특성에 따라 순차적 또는 동시 방식으로 데이터를 추출, 변환 및 로드하기로 결정할 수 있습니다. 이는 또한 클라이언트가 변환된 데이터로 타겟팅하는 사용 사례를 기반으로 합니다.

예를 들어, 클라이언트가 업데이트할 수 있는 지속성 저장소에 지속되고 있고 이벤트의 시퀀스 또는 순서가 중요한 경우, 클라이언트는 순차적 ETL 변환으로 작업을 엄격하게 처리해야 할 수 있습니다.

다른 경우, 잘못된 데이터는 지정된 타임스탬프를 사용하여 내부적으로 정렬하는 다운스트림 애플리케이션/프로세스에 의해 처리될 수 있습니다. 그러한 경우들에서, 병렬 ETL 변환들은 프로세싱 시간들을 개선시키기 위해 실행 가능할 수도 있다.

소스 배치의 경우 클라이언트 기본 설정 및 소비자 제한 사항에 따라 다시 달라집니다. 행의 리젠시/순서에 관계없이 소스 데이터를 동시에 선택할 수 있는 경우 변환 프로세스는 병렬도가 더 높은 프로세스 배치를 생성할 수 있습니다(무순서 처리를 기반으로 한 최적화). 그러나 변환에서 타임스탬프를 적용하거나 우선 순위 순서를 변경해야 하는 경우 데이터 액세스 API 또는 ETL 도구 스케줄러/호출은 가능한 경우 배치가 잘못된 순서로 처리되지 않도록 해야 합니다.

## 지연

지연은 입력 데이터가 아직 다운스트림 프로세스로 전송될 만큼 완전하지 않은 프로세스이지만 향후 사용할 수 있습니다. 고객은 향후 일치를 위한 데이터 윈도우에 대한 개별 허용 오차와 처리 비용을 결정하여 데이터를 보류하고 다음 변환 실행에서 재처리하기로 결정했음을 알려 보존 기간 내에서 향후 시간에 보강하고 조정/결합할 수 있게 됩니다. 이 주기는 행이 충분히 처리되거나 투자가 지속되기에는 부실 하다고 판단될 때까지 지속됩니다. 모든 반복은 이전 반복에서 모든 지연된 데이터의 상위 집합인 지연된 데이터를 생성합니다.

Adobe Experience Platform은 현재 지연된 데이터를 식별하지 않으므로 클라이언트 구현은에서 다른 데이터 세트를 만들려면 ETL 및 데이터 세트 수동 구성을 사용해야 합니다. [!DNL Platform] 지연된 데이터를 유지하는 데 사용할 수 있는 소스 데이터 세트 미러링 이 경우 지연된 데이터는 스냅샷 데이터와 비슷합니다. ETL 변환을 실행할 때마다 소스 데이터가 지연된 데이터와 결합되고 처리를 위해 전송됩니다.

## 변경 로그

| 날짜 | 작업 | 설명 |
| ---- | ------ | ----------- |
| 2019-01-19 | 데이터 세트에서 &quot;fields&quot; 속성 제거됨 | 이전에 데이터 세트에는 스키마 사본이 포함된 &quot;필드&quot; 속성이 포함되었습니다. 이 기능은 더 이상 사용해서는 안 됩니다. &quot;fields&quot; 속성을 찾으면 이를 무시하고 대신 &quot;observedSchema&quot; 또는 &quot;schemaRef&quot;를 사용해야 합니다. |
| 2019-03-15 | 데이터 세트에 &quot;schemaRef&quot; 속성 추가됨 | 데이터 세트의 &quot;schemaRef&quot; 속성은 데이터 세트가 기반으로 하는 XDM 스키마를 참조하는 URI를 포함하며 데이터 세트에서 사용할 수 있는 모든 잠재적 필드를 나타냅니다. |
| 2019-03-15 | 모든 최종 사용자 식별자는 &quot;identityMap&quot; 속성에 매핑됩니다. | identityMap은 CRM ID, ECID 또는 고객 충성도 프로그램 ID와 같은 주체의 모든 고유 식별자를 캡슐화하는 것입니다. 이 지도는 다음 사용자가 사용합니다. [[!DNL Identity Service]](../identity-service/home.md) 주체의 모든 알려진 id와 익명의 id를 해결하려면 각 최종 사용자에 대해 단일 id 그래프를 만듭니다. |
| 2019-05-30 | 데이터 세트에서 &quot;스키마&quot; 속성 EOL 및 제거 | 데이터 세트 &quot;schema&quot; 속성은 더 이상 사용되지 않는 항목을 사용하여 스키마에 대한 참조 링크를 제공했습니다 `/xdms` 의 엔드포인트 [!DNL Catalog] API. 이 은(는) 새 항목에서 참조한 대로 스키마의 &quot;id&quot;, &quot;version&quot; 및 &quot;contentType&quot;을 제공하는 &quot;schemaRef&quot;로 대체되었습니다. [!DNL Schema Registry] API. |
