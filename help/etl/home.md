---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ETL 통합 만들기
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '4102'
ht-degree: 0%

---


# Adobe Experience Platform을 위한 ETL 통합 개발

ETL 통합 안내서에서는 데이터를 인제스트하고 고성능 보안 커넥터를 만드는 일반적인 단계를 간략하게 설명합니다 [!DNL Experience Platform] [!DNL Platform].


- [!DNL Catalog](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [!DNL Data Access](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [!DNL Data Ingestion](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [인증 및 인증 API](../tutorials/authentication.md)
- [!DNL Schema Registry](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

또한 이 안내서에는 ETL 커넥터를 디자인할 때 사용할 샘플 API 호출 및 각 서비스에 대한 개요를 제공하는 설명서로 연결되는 링크가 포함되어 있습니다. 또한 API를 보다 자세히 사용할 수 있습니다. [!DNL Experience Platform]

샘플 통합은 라이선스 버전 2.0 [!DNL GitHub] 의 [ETL 에코시스템 통합 참조 코드](https://github.com/adobe/acp-data-services-etl-reference) 를 통해 [!DNL Apache] 제공됩니다.

## 워크플로우

다음 워크플로우 다이어그램은 Adobe Experience Platform 구성 요소와 ETL 응용 프로그램 및 커넥터를 통합하는 고급 개요를 제공합니다.

![](images/etl.png)

## Adobe Experience Platform 구성 요소

ETL 커넥터 통합에 포함된 여러 Experience Platform 구성 요소가 있습니다. 다음 목록에는 몇 가지 주요 구성 요소 및 기능이 요약되어 있습니다.

- **Adobe Identity Management 시스템(IMS)** - Adobe 서비스에 대한 인증을 위한 프레임워크를 제공합니다.
- **IMS 조직** - 제품 및 서비스를 소유 또는 라이센스하고 회원에게 액세스를 허용할 수 있는 기업 실체입니다.
- **IMS 사용자** - IMS 조직의 구성원. 조직 대 사용자 관계는 여러 사람에게 적용됩니다.
- **[!DNL Sandbox]** - 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 [!DNL Platform] 인스턴스 가상 파티션
- **데이터 검색** - 인제스트 및 변형된 데이터의 메타데이터를 기록합니다 [!DNL Experience Platform].
- **[!DNL Data Access]** - 사용자에게 데이터에 액세스할 수 있는 인터페이스를 제공합니다 [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - API를 사용하여 데이터 [!DNL Experience Platform] 를 [!DNL Data Ingestion] 푸시합니다.
- **[!DNL Schema Registry]** - 사용할 데이터 구조를 설명하는 스키마를 정의하고 저장합니다 [!DNL Experience Platform].

## Getting started with [!DNL Experience Platform] APIs

다음 섹션에서는 API를 성공적으로 호출하기 위해 알아야 하거나 현재 보유하고 있는 추가 정보를 [!DNL Experience Platform] 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증: 무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

## 일반 사용자 흐름

먼저 ETL 사용자가 UI( [!DNL Experience Platform] 사용자 인터페이스)에 로그인하여 표준 커넥터 또는 푸시 서비스 커넥터를 사용하여 인제할 데이터 세트를 만듭니다.

사용자는 UI에서 데이터 집합 스키마를 선택하여 출력 데이터 집합을 만듭니다. 스키마 선택은 수집되는 데이터 유형(레코드 또는 시간 시리즈)에 따라 달라집니다 [!DNL Platform]. UI 내의 스키마 탭을 클릭하여 스키마를 지원하는 동작 유형을 포함하여 사용 가능한 모든 스키마를 볼 수 있습니다.

ETL 도구에서 사용자는 자격 증명을 사용하여 적절한 연결을 구성한 후 매핑 변형 디자인을 시작합니다. ETL 도구는 이미 [!DNL Experience Platform] 커넥터를 설치한 것으로 가정됩니다(이 통합 안내서에 정의되지 않은 프로세스).

샘플 ETL 도구 및 워크플로우의 목업은 [ETL 워크플로우에서 제공됩니다](./workflow.md). ETL 툴은 포맷에 따라 다를 수 있지만 대부분의 툴은 유사한 기능을 제공합니다.

>[!NOTE]
>
>ETL 커넥터는 데이터 및 오프셋을 인제스트할 날짜를 표시하는 타임스탬프 필터(즉, 데이터를 읽을 창)를 지정해야 합니다. ETL 도구는 이 UI 또는 기타 관련 UI에서 이러한 두 매개 변수를 사용하는 것을 지원해야 합니다. Adobe Experience Platform에서 이러한 매개 변수는 사용 가능한 날짜(있는 경우)나 데이터 세트의 일괄 처리 개체에 있는 캡처 날짜에 매핑됩니다.

### 데이터 집합 목록 보기

데이터 소스를 사용하여 매핑하면 해당 데이터를 사용하여 사용 가능한 모든 데이터 집합 목록을 가져올 수 있습니다 [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

사용 가능한 모든 데이터 집합(예: `GET /dataSets`). 응답 크기를 제한하는 쿼리 매개 변수를 포함하는 것이 좋습니다.

전체 __ 데이터 세트 정보가 요청되는 경우 응답 페이로드가 3GB를 초과할 수 있으므로 전반적인 성능이 저하될 수 있습니다. 따라서 쿼리 매개 변수를 사용하여 필요한 정보만 필터링하면 보다 효율적으로 [!DNL Catalog] 쿼리를 작성할 수 있습니다.

#### 목록 필터링

응답을 필터링할 때 앰퍼샌드(앰퍼샌드)로 매개 변수를 구분하여 단일 호출에서 여러 필터를 사용할 수`&`있습니다. 일부 쿼리 매개 변수는 아래의 샘플 요청에서 &quot;속성&quot; 필터와 같이 쉼표로 구분된 값 목록을 허용합니다.

[!DNL Catalog] 응답은 구성된 제한에 따라 자동으로 미터되지만, &quot;제한&quot; 쿼리 매개 변수를 사용하여 제약 조건을 사용자 정의하고 반환되는 개체 수를 제한할 수 있습니다. 사전 구성된 [!DNL Catalog] 응답 제한은 다음과 같습니다.

- 제한 매개 변수를 지정하지 않으면 응답 페이로드당 최대 개체 수는 20개입니다.
- 다른 모든 쿼리에 대한 전체 제한은 [!DNL Catalog] 100개 개체입니다.
- 데이터 집합 쿼리의 경우 속성 쿼리 매개 변수를 사용하여 observableSchema가 요청되면 반환되는 최대 데이터 집합 수는 20개입니다.
- 잘못된 한도 매개 변수(포함 `limit=0`)가 적절한 범위를 외곽선으로 하는 HTTP 400 오류를 충족했습니다.
- 제한이나 오프셋이 쿼리 매개 변수로 전달되면 헤더로 전달된 것보다 우선합니다.

쿼리 매개 변수는 [카탈로그 서비스 개요에서 자세히 다룹니다](../catalog/home.md).

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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

을(를) 호출하는 방법에 대한 자세한 예는 [카탈로그 서비스 개요를](../catalog/home.md) 참조하십시오 [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

**응답**

응답에는 쿼리 매개 변수에 지정된 &quot;name&quot;, &quot;description&quot; 및 &quot;schemaRef&quot;를 표시하는 세 개의 데이터 집합이`limit=3``properties` 포함됩니다.

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

### 데이터 집합 스키마 보기

데이터 집합의 &quot;schemaRef&quot; 속성에는 데이터 집합이 기반으로 하는 XDM 스키마를 참조하는 URI가 포함됩니다. XDM 스키마(&quot;schemaRef&quot;)는 데이터 세트에 사용할 수 있는 모든 _잠재적인_ 필드를 나타내며, _사용 중인_ 필드(&quot;observableSchema&quot; 참조)를나타냅니다.

XDM 스키마는 사용자가 작성될 수 있는 모든 필드 목록을 사용자에게 제공해야 할 때 사용하는 스키마입니다.

이전 응답 개체(`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`)의 첫 번째 &quot;schemaRef.id&quot; 값은 XDM 스키마를 가리키는 URI입니다 [!DNL Schema Registry]. API에 대한 조회(GET) 요청을 수행하여 스키마를 검색할 수 [!DNL Schema Registry] 있습니다.

>[!NOTE]
>
>&quot;schemaRef&quot; 속성은 더 이상 사용되지 않는 &quot;schema&quot; 속성을 대체합니다. 데이터 세트에 &quot;schemaRef&quot;가 없거나 값이 없는 경우 &quot;schema&quot; 속성이 있는지 확인해야 합니다. 이 작업은 이전 호출의 쿼리 매개 변수에서 &quot;schemaRef&quot;를 &quot;schema&quot;로 대체하여 수행할 수 `properties` 있습니다. &quot;스키마&quot; 속성에 대한 자세한 내용은 다음에 나오는 [데이터 세트 &quot;스키마&quot; 속성](#dataset-schema-property-deprecated---eol-2019-05-30) 섹션에서 확인할 수 있습니다.

**API 형식**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**요청**

요청에서는 스키마의 URL 인코딩 `id` URI(&quot;schemaRef.id&quot; 속성의 값)를 사용하고 Accept 헤더가 필요합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

응답 형식은 요청에서 전송된 수락 헤더 유형에 따라 달라집니다. 조회 요청도 수락 헤더에 `version` 포함되어야 합니다. 다음 표에서는 룩업에 대한 헤더 수락 개요를 제공합니다.

| 수락 | 설명 |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | 목록(GET) 요청, 제목, ID 및 버전 |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs 및 allOf resolved, 에는 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed+json; version={major version}` | $ref 및 allOf가 있는 Raw에는 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version={major version}` | $ref 및 allOf가 포함된 Raw, 제목 또는 설명 없음 |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs 및 all해결된 항목, 제목 또는 설명 없음 |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs 및 allOf resolved 설명자가 포함됨 |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` 및 `application/vnd.adobe.xed-full+json; version={major version}` 는 일반적으로 사용되는 [승인] 헤더입니다. `application/vnd.adobe.xed-id+json` 은 &quot;title&quot;, &quot;id&quot; 및 &quot;version&quot;만 반환하므로 [!DNL Schema Registry] 에 리소스를 나열하는 것이 좋습니다. `application/vnd.adobe.xed-full+json; version={major version}` 은 제목 및 설명뿐만 아니라 모든 필드(&quot;속성&quot; 아래에 중첩된)를 반환하므로 특정 리소스(&quot;id&quot;로 표시)를 보는 것이 좋습니다.

**응답**

반환되는 JSON 스키마는 구조 및 필드 수준 정보(&quot;type&quot;, &quot;format&quot;, &quot;minimum&quot;, &quot;maximum&quot; 등)를 설명합니다. JSON으로 정리되어 있는 데이터입니다. 통합(예: Portable or Scala)에 JSON이 아닌 일련화 형식을 사용하는 경우 [스키마 레지스트리 안내서에는 원하는 JSON 유형(&quot;meta:xdmType&quot;)과 해당 표현물을 다른 형식으로 보여 주는 표가 포함되어](../xdm/tutorials/create-schema-api.md) 있습니다.

이 표와 함께 개발자 안내서에는 [!DNL Schema Registry] API를 사용하여 수행할 수 있는 모든 호출의 심층 예가 [!DNL Schema Registry] 포함되어 있습니다.

### 데이터 집합 &quot;스키마&quot; 속성(더 이상 사용되지 않음 - EOL 2019-05-30)

데이터 세트에는 이제 더 이상 사용되지 않으며 이전 버전과의 호환성을 위해 일시적으로 사용할 수 있는 &quot;스키마&quot; 속성이 포함될 수 있습니다. 예를 들어, &quot;schema&quot;가 `properties` 쿼리 매개 변수에서 &quot;schemaRef&quot;로 대체된 경우 이전에 수행한 것과 유사한 목록(GET) 요청이 다음을 반환할 수 있습니다.

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

데이터 집합의 &quot;스키마&quot; 속성이 채워지는 경우 스키마가 더 이상 사용되지 않는 스키마이고, 지원되는 경우 ETL 커넥터는 끝점이 있는 &quot;스키마&quot; 속성 값(기존 스키마를 검색할 수 없는 종점 `/xdms` `/xdms` [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml))을 사용해야 합니다.

**API 형식**

```http
GET /catalog/{"schema" property without the "@"}
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>선택적 쿼리 매개 변수 `expansion=xdm`는 API가 참조되는 모든 스키마를 완전히 확장 및 인라인 포함하도록 지시합니다. 이 작업은 사용자에게 모든 잠재적인 필드 목록을 표시할 때 수행할 수 있습니다.

**응답**

데이터 집합 스키마 [보기](#view-dataset-schema)단계와 유사하게 응답에는 JSON으로 직렬화된 데이터의 구조 및 필드 수준 정보를 설명하는 JSON 스키마가 포함됩니다.

>[!NOTE]
>
>&quot;스키마&quot; 필드가 비어 있거나 완전히 없는 경우, 커넥터는 &quot;schemaRef&quot; 필드를 읽고 이전 단계에 표시된 [스키마 레지스트리 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) 를 사용하여 데이터 집합 스키마를 [확인해야 합니다](#view-dataset-schema).

### &quot;observableSchema&quot; 속성

데이터 집합의 &quot;observableSchema&quot; 속성에는 XDM 스키마 JSON의 JSON 구조와 일치하는 JSON 구조가 있습니다. &quot;observableSchema&quot;는 들어오는 입력 파일에 있는 필드를 포함합니다. 데이터를 쓸 때 [!DNL Experience Platform]사용자는 대상 스키마의 모든 필드를 사용할 필요가 없습니다. 대신 사용 중인 필드만 제공해야 합니다.

관측 가능한 스키마는 데이터를 읽거나 읽을 수 있는 필드 목록을 표시하는 데 사용할 스키마입니다.

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

### 데이터 미리 보기

ETL 애플리케이션은 데이터를 미리 볼 수 있는 기능(ETL 워크플로우의[&quot;그림 8&quot;](./workflow.md))을 제공할 수 있습니다. 데이터 액세스 API는 데이터를 미리 보기 위한 여러 옵션을 제공합니다.

데이터 액세스 API를 사용하여 데이터를 미리 보기 위한 단계별 지침을 비롯한 추가 정보는 [데이터 액세스 자습서에서 확인할 수 있습니다](../data-access/tutorials/dataset-data.md).

### &quot;속성&quot; 쿼리 매개 변수를 사용하여 데이터 세트 세부 사항 가져오기

데이터 집합 [목록을](#view-list-of-datasets)보기 위한 위의 단계에서와 같이 &quot;속성&quot; 쿼리 매개 변수를 사용하여 &quot;파일&quot;을 요청할 수 있습니다.

데이터 집합 및 사용 가능한 응답 필터 [를 쿼리하는](../catalog/home.md) 방법에 대한 자세한 내용은 카탈로그 서비스 개요를 참조할 수 있습니다.

**API 형식**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**응답**

응답에는 &quot;files&quot; 속성을 보여주는 하나의 데이터 세트(`limit=1`)가 포함됩니다.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### &quot;files&quot; 속성을 사용하여 데이터 세트 파일 나열

GET 요청을 사용하여 &quot;files&quot; 속성을 사용하여 파일 세부 사항을 가져올 수도 있습니다.

**API 형식**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**응답**

응답에는 데이터 집합 파일 ID 개체에 포함된 파일 세부 정보와 함께 데이터 집합 파일 ID를 최상위 속성으로 포함합니다.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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

이전 응답에서 반환되는 데이터 집합 파일 ID를 GET 요청에서 사용하여 [!DNL Data Access] API를 통해 더 많은 파일 세부 정보를 가져올 수 있습니다.

데이터 [액세스 개요에는](../data-access/home.md) API를 사용하는 방법에 대한 세부 사항이 [!DNL Data Access] 포함되어 있습니다.

**API 형식**

```http
GET /export/files/{DATASET_FILE_ID}
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
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

&quot;href&quot; 속성을 사용하여 [!DNL Data Access API](../data-access/home.md)

**API 형식**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

위의 요청에 대한 응답에는 파일의 내용 미리 보기가 포함됩니다.

자세한 요청 및 응답을 비롯한 [!DNL Data Access] API에 대한 자세한 내용은 [데이터 액세스 개요를 참조하십시오](../data-access/home.md).

### 데이터 세트에서 &quot;fileDescription&quot;을 가져옵니다.

변형된 데이터의 출력으로 대상 구성 요소인 데이터 엔지니어는 출력 데이터 세트(ETL 워크플로우에서[&quot;그림 12&quot;)를 선택합니다](workflow.md). XDM 스키마가 출력 데이터 세트와 연결되어 있습니다. 기록할 데이터는 데이터 검색 API에서 데이터 집합 엔티티의 &quot;fileDescription&quot; 속성으로 식별됩니다. 이 정보는 데이터 집합 ID(`{DATASET_ID}`)를 사용하여 가져올 수 있습니다. JSON 응답의 &quot;fileDescription&quot; 속성은 요청된 정보를 제공합니다.

**API 형식**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{DATASET_ID}` | 액세스하려는 데이터 세트의 `id` 값. |

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
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

데이터는 [!DNL Experience Platform] 데이터 통합 API [를 사용하도록 작성됩니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).  데이터 쓰기는 비동기 프로세스입니다. 데이터가 Adobe Experience Platform에 기록되면 데이터가 완전히 작성된 후에만 일괄 처리가 만들어지고 성공으로 표시됩니다.

in의 자료는 쪽모이 세공 마루 파일 형태로 작성해야 [!DNL Experience Platform] 한다.

## 실행 단계

실행이 시작되면 커넥터(소스 구성 요소에 정의됨)가 [!DNL Experience Platform] [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) 변환 프로세스는 특정 시간 범위의 데이터를 읽습니다. 내부적으로 소스 데이터 세트를 쿼리합니다. 쿼리하는 동안 매개 변수가 있는 시작 날짜(시간 시리즈 데이터 또는 증분 데이터를 위해 롤링)와 이러한 배치에 대한 데이터 집합 파일을 나열하고 해당 데이터 집합 파일에 대한 데이터 요청을 시작합니다.

### 변형 예

샘플 [ETL 변환](./transformations.md) 문서에는 ID 처리 및 데이터 형식 매핑을 비롯한 다양한 예제 변환이 포함되어 있습니다. 이러한 변형을 참조용으로 사용하십시오.

### 데이터 읽기 [!DNL Experience Platform]

이 [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)를 사용하여 지정된 시작 시간과 종료 시간 사이에 모든 배치를 가져와서 배치가 생성된 순서대로 정렬할 수 있습니다.

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

배치 필터링에 대한 자세한 내용은 [데이터 액세스 자습서를 참조하십시오](../data-access/tutorials/dataset-data.md).

### 일괄 파일 가져오기

찾고 있는 배치에 대한 ID가 있으면 (`{BATCH_ID}`) 을 통해 특정 배치에 속하는 파일 목록을 검색할 수 [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)있습니다.  자세한 내용은 [데이터 액세스 자습서를 참조하십시오](../data-access/tutorials/dataset-data.md).

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### 파일 ID를 사용하여 파일에 액세스

파일의 고유 ID(`{FILE_ID`)를 사용하여 파일 이름, 크기(바이트), 파일 다운로드 링크 등 파일의 특정 세부 정보에 액세스할 [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) 수 있습니다.

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

응답에서 단일 파일 또는 디렉토리를 가리킬 수 있습니다. 각 항목에 대한 세부 사항은 [데이터 액세스 자습서에서 확인할 수 있습니다](../data-access/tutorials/dataset-data.md).

### 파일 컨텐츠 액세스

특정 파일의 컨텐츠에 액세스하는 데 사용할 [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) 수 있습니다. 내용을 가져오기 위해 파일 ID를 사용하여 파일에 액세스할 때 반환되는 값 `_links.self.href` 을 사용하여 GET 요청이 수행됩니다.

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

이 요청에 대한 응답에는 파일의 내용이 포함되어 있습니다. 응답 페이지 매김에 대한 자세한 내용을 포함한 자세한 내용은 데이터 액세스 API [](../data-access/tutorials/dataset-data.md) 자습서를 참조하십시오.

### 스키마 준수 레코드 유효성 확인

데이터를 작성할 때 사용자는 XDM 스키마에 정의된 유효성 검사 규칙에 따라 데이터의 유효성을 검사하도록 선택할 수 있습니다. 스키마 유효성 검사에 대한 자세한 내용은 GitHub의 [ETL 에코시스템 통합 참조 코드에서 확인할 수 있습니다](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

에 있는 참조 구현을 사용 중인 경우 시스템 속성을 사용하여 이 구현 [!DNL GitHub](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)에서 스키마 유효성 검사를 활성화할 수 있습니다 `-DenableSchemaValidation=true`.

논리 XDM 유형에 대해 문자열 및 문자열 `minLength` 과 같은 속성 `maxlength` , 정수 `minimum` 등에 대해 유효성 검사 `maximum` 를 수행할 수 있습니다. 스키마 [레지스트리 API 개발자 안내서에는](../xdm/api/getting-started.md) XDM 유형 및 유효성 검사에 사용할 수 있는 속성에 대한 개요를 설명하는 표가 포함되어 있습니다.

>[!NOTE]
>
>다양한 `integer` 유형에 대해 제공되는 최소 및 최대 값은 유형이 지원할 수 있는 MIN 및 MAX 값이지만 이러한 값은 선택한 최소 및 최대 수에 더 제한될 수 있습니다.

### 일괄 처리 만들기

데이터가 처리되면 ETL 도구는 배치 처리 API를 [!DNL Experience Platform] 사용하여 데이터를 다시 [기록합니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml). 데이터를 데이터 세트에 추가하려면 먼저 묶음에 연결되어 있어야 하며, 나중에 특정 데이터 세트에 업로드됩니다.

**요청**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

샘플 요청 및 응답을 비롯한 일괄 처리 만들기에 대한 세부 사항은 [일괄 처리 처리 통합 개요에서 확인할 수 있습니다](../ingestion/batch-ingestion/overview.md).

### 데이터 세트에 쓰기

새 일괄 처리를 성공적으로 만든 후 파일을 특정 데이터 세트에 업로드할 수 있습니다. 여러 파일을 홍보할 때까지 일괄 게시할 수 있습니다. 작은 파일 업로드 API를 사용하여 _파일을 업로드할 수 있습니다_. 그러나 파일이 너무 크고 게이트웨이 제한이 초과된 경우 _대용량 파일 업로드 API를 사용할 수 있습니다_. 대용량 파일 업로드와 작은 파일 업로드를 모두 사용하는 방법에 대한 자세한 내용은 일괄 처리 [처리 통합 개요를 참조하십시오](../ingestion/batch-ingestion/overview.md).

**요청**

in의 자료는 쪽모이 세공 마루 파일 형태로 작성해야 [!DNL Experience Platform] 한다.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### 일괄 업로드 완료 표시

모든 파일이 배치에 업로드된 후 배치를 완료하도록 신호를 보낼 수 있습니다. 이렇게 하면 완료된 파일에 대해 [!DNL Catalog] &quot;DataSetFile&quot; 항목이 만들어지고 생성 배치와 연결됩니다. 그런 다음 일괄 처리 [!DNL Catalog] 가 성공으로 표시되어 사용 가능한 데이터를 인제스트하는 다운스트림 흐름을 트리거합니다.

데이터는 먼저 Adobe Experience Platform의 스테이징 위치에 도착한 다음 카탈로그 작성 및 확인 후 최종 위치로 이동됩니다. 모든 데이터가 영구 위치로 이동되면 일괄 처리는 성공한 것으로 표시됩니다.

**요청**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

성공하면 응답에서 HTTP 상태 200 OK를 반환하고 응답 본문은 비어 있게 됩니다.

ETL 도구는 데이터를 읽을 때 소스 데이터 집합의 타임스탬프를 기록합니다.

일정 또는 이벤트 호출과 같은 다음 변환 실행에서 ETL은 이전에 저장한 타임스탬프와 앞으로 진행되는 모든 데이터로부터 데이터를 요청하기 시작합니다.

### 마지막 배치 상태 가져오기

ETL 도구에서 새 작업을 실행하기 전에 마지막 배치가 성공적으로 완료되었는지 확인해야 합니다. 이 [!DNL Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) 는 관련 배치의 세부 사항을 제공하는 배치별 옵션을 제공합니다.

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**응답**

이전 배치 &quot;status&quot; 값이 아래와 같이 &quot;success&quot;인 경우 새 작업을 예약할 수 있습니다.

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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

### ID로 마지막 배치 상태 가져오기

을 사용하여 GET 요청을 실행하여 개별 배치 상태를 [!DNL Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) 검색할 수 있습니다 `{BATCH_ID}`. 사용한 ID는 일괄 처리를 만들 때 반환된 ID와 동일합니다. `{BATCH_ID}`

**요청**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**응답 - 성공**

다음 응답에는 &quot;성공&quot;이 표시됩니다.

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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

오류가 발생하는 경우 응답에서 &quot;오류&quot;를 추출하여 ETL 도구에서 오류 메시지로 표시할 수 있습니다.

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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

## 증분 데이터와 스냅샷 데이터 및 이벤트와 프로필 비교

데이터는 다음과 같이 2개의 행렬로 나타낼 수 있습니다.

| 증분 이벤트 | 증분 프로필 |
|-------------------------------|----------------------|
| 스냅샷 이벤트(발생 가능성이 낮음) | 스냅샷 프로필 |

이벤트 데이터는 일반적으로 각 행에 색인화된 타임스탬프 열이 있을 때 사용됩니다.

프로필 데이터는 일반적으로 데이터에 타임스탬프가 없고 각 행을 기본/복합 키로 식별할 수 있을 때 사용됩니다.

증분 데이터는 새로운/업데이트된 데이터만 시스템에 와서 데이터 세트의 현재 데이터에 추가됩니다.

스냅샷 데이터는 모든 데이터가 시스템에 들어와 데이터 세트에 있는 이전 데이터의 일부 또는 전체를 교체하는 경우입니다.

증분 이벤트의 경우 ETL 도구는 배치 엔티티의 사용 가능한 날짜/생성 날짜를 사용해야 합니다. 푸시 서비스의 경우 사용 가능한 날짜가 없으므로 일괄 작성/업데이트 날짜를 사용하여 증분을 표시합니다. 모든 증분 이벤트를 처리해야 합니다.

증분 프로파일의 경우 일괄 처리 엔티티의 생성/업데이트된 날짜를 사용합니다. 일반적으로 모든 증분 프로필 데이터를 처리해야 합니다.

데이터 크기 때문에 스냅샷 이벤트가 발생할 가능성이 매우 낮습니다. 하지만 이 작업이 필요한 경우 ETL 도구는 처리를 위해 마지막 일괄 처리만 선택해야 합니다.

스냅샷 프로필을 사용하는 경우 ETL 툴은 시스템에 도착한 데이터의 마지막 일괄 처리를 선택해야 합니다. 하지만 요구 사항이 변경 내용을 추적하는 경우 모든 배치가 처리됩니다. ETL 프로세스 내에서 중복 제거 처리를 통해 스토리지 비용을 절감할 수 있습니다.

## 일괄 재생 및 데이터 재처리

클라이언트가 지난 &#39;n&#39;일 동안 처리되는 ETL 데이터가 예상대로 발생하지 않았거나 소스 데이터 자체가 정확하지 않았을 수 있음을 발견한 경우 일괄 재생 및 데이터 재처리가 필요할 수 있습니다.

이를 위해 클라이언트의 데이터 관리자는 UI를 사용하여 손상된 데이터가 포함된 배치를 제거합니다. [!DNL Platform] 그런 다음 ETL을 다시 실행해야 하므로 올바른 데이터로 다시 채울 수 있습니다. 소스 자체에 손상된 데이터가 있는 경우 데이터 엔지니어/관리자는 소스 배치를 수정하고 데이터를 다시 인제스트해야 합니다(Adobe Experience Platform 또는 ETL 커넥터를 통해).

생성되는 데이터의 유형에 따라, 데이터 엔지니어는 하나의 일괄 처리 또는 특정 데이터 세트에서 모든 배치를 제거하는 것이 좋습니다. 지침에 따라 데이터가 제거/ [!DNL Experience Platform] 보관됩니다.

데이터를 삭제하는 ETL 기능이 중요할 가능성이 높습니다.

제거가 완료되면 클라이언트 관리자는 배치가 삭제되는 시점부터 핵심 서비스에 대한 처리를 다시 시작하도록 Adobe Experience Platform을 다시 구성해야 합니다.

## 동시 배치 처리

클라이언트의 재량에 따라 데이터 관리자/엔지니어는 특정 데이터 세트의 특성에 따라 순차적 방식 또는 동시 방식으로 데이터를 추출, 변형 및 로드할 수 있습니다. 또한 변환된 데이터로 클라이언트가 타깃팅하는 사용 사례를 기반으로 합니다.

예를 들어 클라이언트가 업데이트할 수 있는 지속성 저장소에 지속되고 이벤트의 시퀀스 또는 순서가 중요한 경우 클라이언트는 순차적 ETL 변형을 사용하여 작업을 엄격히 처리해야 할 수 있습니다.

다른 경우에는 지정된 타임스탬프를 사용하여 내부적으로 정렬되는 다운스트림 애플리케이션/프로세스에서 순서가 맞지 않는 데이터를 처리할 수 있습니다. 이러한 경우 병렬 ETL 변형을 사용하면 처리 시간을 향상시킬 수 있습니다.

소스 배치의 경우 클라이언트 환경 설정 및 소비자 제한에 따라 다시 달라집니다. 행의 리젠시/순서 없이 소스 데이터를 병렬로 선택할 수 있는 경우 변환 프로세스는 병렬 처리 수준이 높은 프로세스 배치를 만들 수 있습니다(주문 처리 범위를 기반으로 최적화). 그러나 변형이 타임스탬프 또는 변경 우선 순위 순서를 따라야 하는 경우 데이터 액세스 API 또는 ETL 도구 스케줄러/호출은 가능한 한 일괄 처리가 순서가 잘못되지 않도록 해야 합니다.

## 지연

지연은 입력 데이터가 아직 다운스트림 프로세스로 전송하기에 충분하지 않지만 향후 사용할 수 있는 프로세스입니다. 클라이언트는 향후 일치에 대한 데이터 창에 대한 개별 허용치를 결정하고, 데이터를 보관하고 다음 변환 실행에 재처리하기로 결정한 사항을 알리기 위해 데이터 창에 대한 개별 허용치를 결정합니다. 이러한 허용치를 향후 보존 기간 내에 농축하고 조정/통합할 수 있을 것입니다. 행이 충분히 처리되거나 투자를 계속하기에는 너무 오래된 것으로 간주될 때까지 이 사이클은 계속되고 있습니다. 모든 반복은 이전 반복에서 모든 지연된 데이터의 상위 집합인 지연된 데이터를 생성합니다.

Adobe Experience Platform은 현재 지연된 데이터를 식별하지 않으므로 클라이언트 구현은 ETL 및 데이터 세트 수동 구성을 사용하여 지연된 데이터를 유지하는 데 사용할 수 있는 소스 데이터 세트를 [!DNL Platform] 미러링하여 다른 데이터 세트를 만들어야 합니다. 이 경우 지연된 데이터는 스냅샷 데이터와 비슷합니다. ETL 변환을 실행할 때마다 소스 데이터가 지연된 데이터와 통합되고 처리를 위해 전송됩니다.

## 창로그

| 날짜 | 작업 | 설명 |
| ---- | ------ | ----------- |
| 2019-01-19 | 데이터 세트에서 &quot;필드&quot; 속성을 제거했습니다. | 이전에 데이터 집합에는 스키마의 복사본을 포함하는 &quot;필드&quot; 속성이 포함되었습니다. 이 기능은 더 이상 사용할 수 없습니다. &quot;fields&quot; 속성이 있으면 무시해야 하며 대신 &quot;observedSchema&quot; 또는 &quot;schemaRef&quot;가 사용됩니다. |
| 2019-03-15 | 데이터 세트에 &quot;schemaRef&quot; 속성이 추가되었습니다. | 데이터 집합의 &quot;schemaRef&quot; 속성에는 데이터 집합이 기반으로 하는 XDM 스키마를 참조하는 URI가 포함되어 있으며 데이터 집합에서 사용할 수 있는 모든 잠재적인 필드를 나타냅니다. |
| 2019-03-15 | 모든 최종 사용자 식별자는 &quot;identityMap&quot; 속성에 매핑됩니다. | &quot;identityMap&quot;은 CRM ID, ECID 또는 로열티 프로그램 ID와 같은 주체의 모든 고유 식별자를 캡슐화합니다. 이 맵은 각 최종 사용자에 대해 단일 ID 그래프를 형성하면서 대상의 모든 알려진 및 익명 ID를 해결하는 데 사용됩니다 [!DNL Identity Service](../identity-service/home.md) . |
| 2019-05-30 | 데이터 세트에서 EOL 및 &quot;스키마&quot; 속성 제거 | 데이터 집합 &quot;스키마&quot; 속성은 API에서 더 이상 사용되지 않는 끝점을 사용하여 스키마에 대한 참조 링크를 `/xdms` [!DNL Catalog] 제공했습니다. 새 [!DNL Schema Registry] API에서 참조되는 스키마의 &quot;id&quot;, &quot;version&quot; 및 &quot;contentType&quot;을 제공하는 &quot;schemaRef&quot;로 대체되었습니다. |