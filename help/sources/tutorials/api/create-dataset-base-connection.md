---
keywords: Experience Platform;홈;인기 항목;데이터 집합 연결 흐름 서비스;흐름 서비스;흐름 서비스 연결
solution: Experience Platform
title: Flow Service API를 사용하여 Adobe Experience Platform 데이터 세트 기본 연결 만들기
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform에 대한 데이터 세트 기본 연결을 만드는 방법을 알아봅니다.
exl-id: 5e829f4a-954b-4011-a003-c42c7a0d5617
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Experience Platform] 데이터 집합 기본 연결을 만듭니다.

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집한 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

제3자 소스의 데이터를 [!DNL Platform]에 연결하려면 먼저 데이터 세트 기본 연결을 설정해야 합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 데이터 세트 기본 연결을 만드는 단계를 안내합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [XDM(경험 데이터 모델) 시스템](../../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   * [스키마 컴포지션의 기본 사항](../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   * [스키마 레지스트리 개발자 안내서](../../../xdm/api/getting-started.md):스키마 레지스트리 API에 대한 호출을 성공적으로 수행하기 위해 알아야 하는 중요한 정보를 포함합니다. 여기에는 `{TENANT_ID}`, &quot;컨테이너&quot; 개념 및 요청 수행에 필요한 머리글이 포함됩니다(수락 헤더와 가능한 값에 특히 유의함).
* [카탈로그 서비스](../../../catalog/home.md):카탈로그는 데이터 위치 및 내부 연결을 위한 레코드 시스템입니다 [!DNL Experience Platform].
* [일괄 처리](../../../ingestion/batch-ingestion/overview.md):일괄 처리 통합 API를 사용하면 데이터를 Experience Platform에 일괄 파일로 통합할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 Data Lake에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 연결 사양 조회

데이터 집합 기본 연결을 만드는 첫 번째 단계는 [!DNL Flow Service] 내에서 연결 사양 집합을 가져오는 것입니다.

**API 형식**

사용 가능한 각 소스에는 인증 요구 사항과 같은 커넥터 속성을 설명하는 고유한 연결 사양이 있습니다. GET 요청을 수행하고 쿼리 매개 변수를 사용하여 데이터 세트 기본 연결에 대한 연결 사양을 조회할 수 있습니다.

쿼리 매개 변수 없이 GET 요청을 보내면 사용 가능한 모든 소스에 대한 연결 사양이 반환됩니다. `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` 쿼리를 포함하여 데이터 집합 기본 연결에 대한 정보를 가져올 수 있습니다.

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**요청**

다음 요청은 데이터 집합 기본 연결에 대한 연결 사양을 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 기본 연결을 만드는 데 필요한 연결 사양 및 고유 식별자(`id`)가 반환됩니다.

```json
{
    "items": [
        {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "name": "{NAME}",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "targetSpec": {
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "dataSetId": {
                            "type": "string"
                        }
                    },
                    "required": [
                        "dataSetId"
                    ]
                }
            },
            "attributes": {
                "category": "{CATEGORY}"
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## 데이터 집합 기본 연결 만들기

기본 연결은 소스를 지정하며 해당 소스의 자격 증명을 포함합니다. 여러 소스 커넥터를 만들어 서로 다른 데이터를 가져오는 데 사용할 수 있으므로 데이터 세트 기본 연결은 하나만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataset Base Connection",
        "description": "Dataset Base Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| ------------- | --------------- |
| `connectionSpec.id` | 이전 단계에서 접속 사양 `id`이 검색되었습니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다. 이 ID는 대상 연결을 만들고 타사 소스 커넥터에서 데이터를 인제스트하는 데 필요합니다.

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 데이터 세트 기본 연결 연결을 만들고 연결의 고유 ID 값을 받았습니다. 이 기본 연결을 사용하여 대상 연결을 만들 수 있습니다. 다음 자습서에서는 사용 중인 소스 커넥터의 범주에 따라 대상 연결을 만드는 단계를 안내합니다.

* [클라우드 스토리지](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [고객 성공 사례](./collect/customer-success.md)
* [데이터베이스](./collect/database-nosql.md)
