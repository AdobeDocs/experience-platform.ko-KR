---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: API를 사용하여 의사 결정 서비스 엔티티 관리
topic: tutorial
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# API를 사용하여 의사 결정 개체 및 규칙 관리

이 문서에서는 Adobe Experience Platform API를 사용하여 의사 결정 서비스의 비즈니스 업체와 작업하기 위한 자습서를 제공합니다.

이 자습서에는 두 가지 부분이 있습니다.

- 비즈니스 객체를 관리하기 위한 일반 저장소 API는 [첫 번째 부분에서](#managing-repository-entities-using-apis)도입되었습니다. 이러한 API는 **모든** 유형의 비즈니스 객체에 대한 작성, 읽기, 업데이트, 삭제 및 검색 기능을 제공한다는 점에서 일반적입니다. 일반 API 모델에 대해 설명하고 HAL(Hypertext Application Language)과의 관계에 대해 설명합니다.

- 저장소 API에 대한 지식을 적용하는 [두 번째](#creating-and-managing-offer-decisioning-entities-using-apis) 부분은 저장소 API를 통해 관리되는 비즈니스 개체에 중점을 둡니다. 동일한 API가 적용되면 활동 및 비즈니스 규칙과 같은 두 개의 서로 다른 개체를 관리하는 것에만 차이점이 있을 뿐 아니라 관리되는 개체의 유형을 나타내는 필요한 헤더 값이 적용됩니다.

## 시작하기

이 자습서에서는 Experience Platform 서비스 및 API 규칙에 대한 작업 이해를 필요로 합니다. 플랫폼 저장소는 비즈니스 객체와 다양한 유형의 메타데이터를 저장하기 위해 다른 여러 플랫폼 서비스에서 사용하는 서비스입니다. 이러한 객체를 관리하고 쿼리하여 여러 런타임 서비스에서 사용할 수 있는 안전하고 유연한 방법을 제공합니다. 의사 결정 서비스는 이러한 서비스 중 하나입니다. 이 자습서를 시작하기 전에 다음 사항에 대한 설명서를 검토하십시오.

- [XDM(Experience Data Model)](../../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [의사 결정 서비스](./../home.md):경험 의사 결정(일반)에 사용되는 개념과 구성 요소, 특히 오퍼 결정에 대해 설명합니다. 고객 경험 중에 표시할 최상의 옵션을 선택하는 데 사용되는 전략을 보여줍니다.
- [PQL(프로필 쿼리 언어)](../../segmentation/pql/overview.md):PQL은 XDM 인스턴스 위에 표현식을 작성할 수 있는 강력한 언어입니다. PQL은 의사 결정 규칙을 정의하는 데 사용됩니다.

다음 섹션에서는 플랫폼 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 저장소 API 규칙

의사 결정 서비스는 서로 관련된 여러 비즈니스 개체에 의해 제어됩니다. 모든 비즈니스 객체는 플랫폼의 비즈니스 객체 저장소에 저장됩니다. 이 저장소의 주요 기능은 API가 비즈니스 객체 유형과 수직이라는 것입니다. API 끝점의 리소스 유형을 나타내는 POST, GET, PUT, PATCH 또는 DELETE API를 사용하는 대신, 6개의 일반 끝점만 있지만 이러한 모호성이 필요할 때 개체의 유형을 나타내는 매개 변수를 수락하거나 반환합니다. 스키마는 저장소에 등록되어 있어야 하지만, 저장소가 열려 있는 객체 유형 집합에서 사용할 수 있다는 점을 넘어

위에 나열된 헤더 외에, 저장소 개체를 생성, 읽기, 업데이트, 삭제 및 쿼리할 API에는 다음 규칙이 있습니다.

- 모든 리포지토리 API에 대한 끝점 경로는 다음으로 `https://platform.adobe.io/data/core/xcore/`시작합니다.

API 페이로드 형식은 `Accept` 또는 `Content-Type` 헤더와 협상됩니다. 다음 표에 따라 `Accept` 또는 `Content-Type` 헤더의 메시지 형식이 {FORMAT} `application/vnd.adobe.platform.xcore.{FORMAT}+json` 의 값이 특정 저장소 API 요청 또는 응답 메시지에 종속되는 값으로 표시됩니다.

| 형식 변형 | 요청 또는 응답 엔티티에 대한 설명 |
| --- | --- |
| 매개 변수<br>뒤에 `schema={schemaId}` | 이 메시지에는 형식 매개 변수 스키마로 표시된 JSON 스키마로 설명된 인스턴스가 포함되어 있습니다. 인스턴스는 JSON 속성으로 래핑됩니다 `_instance`. 응답 페이로드의 다른 최상위 등록 정보는 모든 리소스에 사용할 수 있는 저장소 정보를 지정합니다.  HAL 형식을 준수하는 메시지에는 HAL 형식의 참조가 들어 있는 `_links` 속성이 있습니다. |
| `patch.hal` | 이 메시지에는 패치할 인스턴스가 HAL을 준수한다고 가정하고 있는 JSON 패치 페이로드가 포함되어 있습니다. 즉, 인스턴스의 자체 인스턴스 속성뿐만 아니라 인스턴스의 HAL 링크도 패치할 수 있습니다. 클라이언트에서 속성을 업데이트할 수 있는 제한 사항이 있습니다. |
| `home.hal` | 이 메시지에는 보관소의 홈 문서 리소스의 JSON 형식 표현이 포함되어 있습니다. |
| xdm.receipt | 이 메시지에는 만들기, 업데이트(전체 및 패치) 또는 삭제 작업에 대한 JSON 형식 응답이 포함되어 있습니다. 영수증에는 ETag 형식의 인스턴스 개정을 나타내는 제어 데이터가 포함됩니다. |

각 **형식 변형의** 사용은 특정 API에 따라 다릅니다.

| API | Content-Type 헤더 | 헤더 수락 |
| --- | --- | --- |
| 인스턴스 만들기 <br/>컨테이너 만들기 | `hal`<br/>스키마 매개 변수 | `xdm.receipt` |
| InstanceUpdate<br/>컨테이너 업데이트 | `hal`<br/>스키마 매개 변수 | `xdm.receipt` |
| 패치 인스턴스 | `patch.hal` | `xdm.receipt` |
| 인스턴스<br/>삭제컨테이너 삭제 | N/A | `xdm.receipt` |
| InstanceRead<br/>컨테이너 읽기 | N/A | `hal` with `schema` parameter |
| 목록<br/>인스턴스목록 컨테이너 | N/A | `hal` 특수 `schema` 매개 변수 사용 `https://ns.adobe.com/experience/xcore/hal/results` |
| 검색 인스턴스 | N/A | hal with special parameter `schema``https://ns.adobe.com/experience/xcore/hal/results` |
| 보고서 루트 읽기 | N/A | `home.hal` |

컨테이너 만들기, 업데이트 및 읽기 API의 경우 형식 매개 변수 스키마에 값이 `https://ns.adobe.com/experience/xcore/container`있습니다.

`ContainerId` 는 인스턴스 API의 첫 번째 경로 매개 변수입니다. 모든 사업체는 컨테이너라고 하는 곳에 상주합니다. 컨테이너는 서로 다른 걱정을 분리시키는 격리 메커니즘입니다. 저장소 인스턴스 API의 첫 번째 경로 요소는 `containerId`입니다. 식별자는 호출자가 액세스할 수 있는 컨테이너 목록에서 가져옵니다. 예를 들어 컨테이너에서 인스턴스를 만드는 API는 `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`입니다.

액세스 가능한 컨테이너 목록은 표준 헤더를 사용하여 HTTP GET 요청과 함께 저장소 루트 끝점 &quot;/&quot;을(를) 호출하여 가져옵니다.

## 컨테이너에 대한 액세스 관리

관리자는 비슷한 주체, 리소스, 액세스 권한을 프로필에 그룹화할 수 있습니다. 이렇게 하면 관리 부담이 줄어들고 Adobe의 Admin [Console UI에서 지원됩니다](https://adminconsole.adobe.com). 프로필을 만들고 사용자를 할당하려면 조직에서 Adobe Experience Platform 및 오퍼의 제품 관리자여야 합니다.

한 번에 특정 권한과 일치하는 제품 프로필을 만든 다음 해당 프로필에 사용자를 추가하는 것만으로 충분합니다. 프로필은 권한을 부여받은 그룹 역할을 하며 해당 그룹의 모든 실제 사용자 또는 기술 사용자는 이러한 권한을 상속받습니다.

### 사용자 및 통합에 액세스할 수 있는 컨테이너 목록

관리자가 일반 사용자에 대한 컨테이너에 대한 액세스 권한을 부여하거나 통합을 수행하면 해당 컨테이너가 저장소의 이른바 &quot;홈&quot; 목록에 표시됩니다. 이 목록은 호출자가 액세스할 수 있는 모든 컨테이너의 하위 집합이므로 다른 사용자 또는 통합에 대해 다를 수 있습니다. 컨테이너 목록은 제품 컨텍스트에 대한 연관성을 기준으로 필터링할 수 있습니다. 필터 매개 변수가 호출되고 `product` 반복될 수 있습니다. 두 개 이상의 제품 컨텍스트 필터가 제공되면 해당 제품 컨텍스트와 연결된 컨테이너의 조합이 반환됩니다. 단일 컨테이너를 여러 제품 컨텍스트에 연결할 수 있습니다.

플랫폼 의사 결정 서비스 컨테이너의 컨텍스트가 현재 `dma_offers`있습니다.

>[!NOTE] 플랫폼 의사 결정 컨테이너의 컨텍스트가 곧 `acp`변경됩니다. 필터링은 선택 사항이지만, 필터링 기준은 향후 릴리스에 대해서만 편집해야 `dma_offers` 합니다. 이러한 변경 사항을 준비하기 위해 클라이언트는 필터를 사용하지 않거나 두 제품 컨텍스트를 모두 필터로 적용해야 합니다.

**요청**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**응답**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

결과 항목에 `instanceId` 나열된 내용을 확인합니다. 이 매개 변수는 API에서 일반 비즈니스 개체를 읽고 조작하는 데 사용됩니다. `containerId`

목록은 액세스 권한에 따라 사용자에 대해 이미 필터링되지만 속성 쿼리를 통해 필터링할 수 있습니다.

## 엔티티 관리를 위한 일반 API

### 인스턴스 만들기

저장소에서 새 인스턴스를 만드는 API는 `containerId` 경로 매개 변수를 사용하며 스키마 매개 변수를 사용하여 `Content-Type` 헤더에 있는 인스턴스의 유형을 식별합니다.

인스턴스 속성은 `_instance` 속성에 래핑된 페이로드에서 제공됩니다. 인스턴스 속성은 지정된 스키마 식별자가 있는 JSON 스키마에 대해 유효해야 합니다.

HAL `_links` 속성이 있어야 하지만 비어 있을 수 있습니다. 즉, 이 인스턴스에 대해 사용자 지정 링크가 정의되지 않습니다.

**요청**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**응답**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

응답에는 방금 만든 개체의 instanceId가 포함됩니다. 이 instanceId는 변경할 수 없으며, 항상 저장소에 의해 지정되며 전체적으로 고유합니다. 이 값은 실제 식별자 역할을 합니다.

또한 스키마에 이러한 속성이 있는 경우 응답 페이로드의 `@id` 속성에서 URI(Universal Resource Identifier)가 반환됩니다. 각 인스턴스에는 인스턴스의 URI 및 기본 키로 사용되는 속성이 있어야 합니다. 이 식별자는 다른 인스턴스에서 다른 유형을 포함하여 새 인스턴스와 관계를 형성하는 데 사용됩니다. 현재 릴리스에서는 URI가 저장소에 의해 생성되며 `@id` 속성에 포함됩니다. 이후 버전에서는 이 규칙을 완화하여 클라이언트가 자신의 URI 값을 관리하고 이 규칙이 포함된 속성의 이름을 지정할 수 있습니다.

이러한 URI는 URL이 아니며 리소스를 직접 검색하는 방법을 제공하지 않습니다. 이러한 측면을 나타내기 위해 URI에는 검색 프로토콜을 지정하지 않는 URI 체계가 접두사로 사용됩니다. 하지만 URI를 사용하여 쿼리를 사용하여 인스턴스를 조회할 수 있습니다.

REST 응답에는 방금 만든 인스턴스를 검색하는 데 사용할 수 있는 URL 구성 요소가 포함된 위치 헤더가 있습니다. 이 구성 요소는 상대 URI 참조이며 저장소의 기본 URI에 적용해야 합니다. 기본 URI가 `Content-Base` 헤더에서 반환됩니다.

이 `repo:etag` 속성은 인스턴스의 개정을 지정합니다. 이 값은 일관성을 유지하기 위해 업데이트 작업에 사용할 수 있습니다. HTTP 헤더를 `If-Match` 사용하여 실수로 덮어쓸 수 있는 인스턴스에 다른 변경 사항이 없도록 PUT 또는 PATCH API 호출에 조건을 추가할 수 있습니다. 이 `repo:etag` 값은 모든 만들기, 읽기, 업데이트, 삭제 및 쿼리 호출과 함께 반환됩니다. 이 값은 RFC7232 섹션 ` If-Match` 3.1 [](https://tools.ietf.org/html/rfc7232#section-3.1)헤더의 값으로 사용됩니다.

나머지 속성은 인스턴스를 만들고 마지막으로 수정하는 데 사용한 계정 및 API 키를 나타냅니다. 이 호출에 의해 인스턴스가 생성되었으므로 각 값은 요청의 값입니다.

### ID로 인스턴스 조회

Create 호출과 함께 반환된 위치 헤더의 URL을 사용하면 애플리케이션에서 인스턴스를 찾을 수 있습니다.

**요청**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE] 경로 매개 변수로 `instanceId` 제공되지만, 가능한 경우, 경로 자체를 생성하지 말고 목록 및 검색 작업에 포함된 인스턴스에 대한 링크를 따라가야 합니다. 자세한 내용은 ‎ 섹션 6.4.4 및 ‎ 6.4.6을 참조하십시오.

**응답**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

인스턴스의 JSON 속성은 `_instance` 속성으로 둘러싸여 있고 다른 루트 레벨 속성은 인스턴스에 대한 메타데이터를 보유합니다.

이 리소스에는 JSON 스키마 ID의 배열도 포함되어 있습니다. 이 배열은 이 인스턴스의 유효성을 검사하는 JSON 스키마를 나타냅니다.

각 인스턴스에는 IANA 등록 자체 관계(RFC5988에 정의됨)에 해당하는 관계 유형 자아 [방식의 HAL 링크가 포함되어]있습니다.

**인스턴스의 최신 개정 테스트**

인스턴스의 현재 `eTag` 값이 응답과 함께 반환되어 클라이언트가 인스턴스에 대해 조건부 작업을 발행할 수 있으므로 동일한 리소스 상태를 다시 검색하지 않도록 하거나 클라이언트의 지식 없이도 이후 개정 값을 덮어쓰지 않도록 할 수 있습니다.

조회 API를 사용하여 클라이언트는 `If-None-Match` 헤더 매개 변수를 지정할 수 있습니다. 이 표준 HTTP 매개 변수 RFC2616 [의 정의를 참조하십시오]. 클라이언트가 지정하는 엔티티 태그 값은 업데이트, 읽기, 목록 또는 검색 API 호출에서 최신 응답으로 받은 값입니다. 이 `etag` 값은 클라이언트에 불투명해야 하며 따옴표로 둘러싸인 문자열로 지정해야 합니다.

**요청**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

The repository API will respond with the tag given인스턴스의 마지막 개정판이 지정된 경우 리포지토리 API는 304 Not Modified 상태로 응답합니다.

### 스키마 인스턴스 목록 - 정렬 및 페이징

클라이언트는 만들고 있는 인스턴스를 추적할 수 없으므로 실제 instanceId로 클라이언트에 액세스할 수 없습니다. 인스턴스 읽기 API를 사용하는 것은 예외입니다. 또한 클라이언트는 다른 클라이언트가 만든 인스턴스를 알지 못합니다.

보다 일반적인 액세스 패턴은 모든 인스턴스 집합을 통해 페이지를 표시합니다.

**요청**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**응답**

응답은 `{schemaId}` 지정된 항목에 따라 다릅니다. &quot;https<span></span>://ns.adobe.com/experience/offer-management/offer-activity&amp;id=xcore:offer-activity:fa24f9e8fc15c73&quot;의 경우 응답은 다음과 같습니다.

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE] 결과에는 지정된 스키마 또는 이 목록의 첫 번째 페이지에 대한 인스턴스가 포함됩니다. 인스턴스는 두 개 이상의 스키마를 따를 수 있으므로 두 개 이상의 목록에 표시될 수 있습니다.

페이지 리소스는 일시적이며 읽기 전용입니다.업데이트하거나 삭제할 수 없습니다. 페이징 모델은 클라이언트별로 상태를 유지하지 않고 장시간 동안 큰 목록의 하위 세트에 대한 임의 액세스를 제공합니다.

이러한 방식으로 페이지별로 인스턴스 목록에 액세스하려면 해당 인스턴스 목록에 의해 열거된 항목 위에 안정된 정렬을 정의할 수 있어야 합니다. &quot;안정적&quot;이라고 해서 인스턴스가 미리 결정된 페이지에 나타나는 것은 아닙니다. 사실, 속성 P에 따라 인스턴스를 정렬하여 페이지 순서를 지정하고 클라이언트가 이 속성 P를 업데이트하면 다른 클라이언트가 목록을 페이징 처리하는 동안 다른 페이지에서 이 인스턴스에 다시 도달할 수 있습니다. 즉, 모델은 더 많은 현재 결과를 반환하는 것을 선호합니다.

하지만 정렬 순서가 수정할 수 없는 속성을 기반으로 하는 경우 &quot;안정적&quot; 정렬 순서는 페이지 시작 시 존재했던 모든 인스턴스에 도달할 수 있도록 보장합니다(페이지가 도달할 때까지 삭제되지 않는 경우). 이 정렬 순서가 단조롭게 증가하는 속성에 있으면 페이징 작업이 시작된 후 생성된 인스턴스에도 도달합니다.

클라이언트는 원하는 페이지 크기에 대한 힌트를 제공할 수 있지만 반환되는 페이지에 더 많은 인스턴스 수를 제공하는 것은 전적으로 보관소에만 있습니다. 안정적인 순서를 보장하려면 정렬 속성의 값이 페이지 경계 간에 다르도록 페이지에서 항목을 추가하거나 제거해야 합니다. 이렇게 하면 다음 페이지에 마지막 페이지의 일부 항목이 다시 포함되지 않거나 최악의 시나리오에서 각 페이지에 있는 동일한 항목으로 인해 중단됩니다.

페이징 기능은 다음 매개 변수에 의해 제어됩니다.

- **`orderBy`**:인스턴스 목록이 정렬되는 기준으로 쉼표로 구분된 순서가 지정된 속성 목록을 포함합니다. 첫 번째 속성은 기본 정렬에 사용되고 두 번째 속성은 기본 정렬의 연결을 확인하는 데 사용됩니다. 인스턴스당 고유한 값이 있는 속성을 지정하면 연결이 불가능하며 각 항목 뒤에 페이지 나누기가 발생할 수 있습니다. 속성 이름 앞에 오름차순 또는 해당 속성에 의한 내림차순 순서를 `+` 나타내는 `-` 접두사가 붙을 수 있습니다. 속성 이름 접두사가 없는 경우 결과가 오름차순으로 정렬됩니다. 요청에 이 지정되지 `orderBy` 않으면 저장소가 대신 실제 instanceId 속성을 사용합니다.
- **`start`**:클라이언트는 시작 매개 변수를 사용하여 검색할 페이지를 정의합니다. 시작 매개 변수는 원하는 페이지의 시작을 결정합니다. 응답에는 `orderBy` 속성 값이 지정된 값보다 (오름차순) 엄격하게 크거나, 지정된 값보다 (내림차순) 정확히 작음(내림차순)인 인스턴스로 시작하는 인스턴스가 포함됩니다. 쿼리 매개 변수가 지정되지 않으면, 이 매개 변수는 가능한 첫 번째 인스턴스 식별자 앞에 정렬되는 instanceId 값으로 기본 설정되며, 따라서 이 값은 첫 번째 페이지에서 생략됩니다.
- **`limit`**:지정된 요청에 대해 반환해야 하는 최대 항목 수에 대한 힌트로 양의 정수를 지정합니다. 시작 매개 변수의 안정적인 작업을 제공해야 하는 필요에 따라 실제 응답 크기가 작거나 클 수 있습니다

### 필터링 목록

목록 결과를 필터링할 수 있으며 페이징 메커니즘과는 독립적으로 수행할 수 있습니다. 필터는 목록 순서에서 인스턴스를 건너뛰거나 지정된 조건을 충족하는 인스턴스만 포함하도록 명시적으로 요청합니다. 클라이언트는 속성 표현식을 필터로 사용하거나 인스턴스의 기본 키 값으로 사용할 URI 목록을 지정할 수 있습니다.

- **`property`**:속성 이름 경로 뒤에 비교 연산자 뒤에 값이 들어 있습니다. <br/>
반환된 인스턴스 목록에는 표현식이 true로 평가되는 인스턴스가 포함되어 있습니다. 예를 들어 인스턴스에 페이로드 속성이 `status` 있고 가능한 값이 `draft``approved`있다고 가정하면 쿼리 매개 변수는 상태가 승인된 인스턴스만 `archived` `deleted` `property=_instance.status==approved` 반환합니다. <br/>
<br/>
지정된 값과 비교할 속성은 경로로 식별됩니다. 개별 경로 구성 요소는 다음과 같이 '.'로 구분됩니다.'_instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1'<br/>

문자열, 숫자 또는 날짜/시간 값이 있는 속성의 경우 허용되는 연산자는 다음과 같습니다. `==`및 `!=`, `<``<=`, `>` 그리고 `>=`를 선택합니다. 또한 문자열 값이 있는 속성의 경우 연산자를 사용할 `~` 수 있습니다. 연산자는 정규 표현식에 따라 지정된 속성과 일치합니다. `~` 속성의 문자열 값은 필터링된 결과에 포함할 엔티티의 **전체** 표현식과 일치해야 합니다. 예를 들어, 속성 값 `cars` 내의 아무 위치에서나 문자열을 찾으려면 정규 표현식이 있어야 합니다 `.*cars.*`. 행간 또는 후행 `.*``cars`없이, 각 항목으로 시작하거나 끝나는 속성 값이 있는 엔티티만 일치합니다. 연산자의 `~` 경우 문자 비교가 대/소문자를 구분하지 않습니다. 다른 모든 연산자의 경우 대소문자를 구분합니다.<br/><br/>
인스턴스 페이로드 속성만 필터 표현식에 사용할 수 있습니다. 둘러싸기 속성은 같은 방식으로 비교됩니다(예: `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`Adobe <br/>
쿼리<br/>매개 변수를 `property` 반복하여 여러 필터 조건이 적용되도록 할 수 있습니다. 예를 들어 특정 날짜 이후에 특정 날짜 이전에 마지막으로 수정된 모든 인스턴스를 반환합니다. 이러한 식의 값은 URL로 인코딩되어야 합니다. 표현식이 제공되지 않고 속성 이름이 나열되는 경우 해당 이름의 속성이 있는 항목만 나열됩니다.<br/>
<br/>

- **`id`**:경우에 따라 목록을 인스턴스의 URI로 필터링해야 합니다. 쿼리 매개 변수를 사용하여 하나의 인스턴스를 필터링할 수 있지만 둘 이상의 인스턴스를 얻으려면 요청에 URI 목록을 지정할 수 있습니다. `property` 매개 `id` 변수가 반복되고 각 항목은 하나의 URI 값을 지정합니다. `id={URI_1}&id={URI_2},…` URI 값은 URL로 인코딩되어야 합니다.

페이지 지정 결과는 특수 MIME `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`형식으로 반환됩니다.

**요청**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**응답**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

응답에는 이 페이지의 결과 수와 방금 반환된 페이지로 시작하는 필터링된 목록의 총 항목 수를 나타내는 두 속성 옆에 있는 JSON 속성 결과 내의 결과 항목 목록이 포함되어 있습니다.

### 전체 텍스트 검색 및 구조화된 쿼리

클라이언트가 문자열 속성에 포함된 용어별로 보다 복잡한 필터 조건 및 검색 인스턴스를 제공하려는 경우 저장소가 보다 강력한 검색 API를 제공합니다.

**요청**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

이 API를 통해 클라이언트는 페이지 및 목록 API의 필터링 매개 변수 외에도 전체 텍스트 및 부울 쿼리 매개 변수를 추가할 수 있습니다.

전체 텍스트 검색은 다음 매개 변수로 제어됩니다.

- **`q`**:인스턴스의 문자열 속성과 일치하기 전에 표준화된 공백으로 구분된 용어 목록이 들어 있습니다. 용어 및 해당 용어 역시 표준화되므로 문자열 속성을 분석합니다. 검색 쿼리는 `q` 매개 변수에 지정된 용어 중 하나 이상을 일치시킵니다. 문자 +, -, =, &amp;&amp;,||, >, &lt;,!, (,), {, }, [,]^, &quot;, ~, *, ?, :, / 는 쿼리 문자열 내에서 단어 경계를 결정하는 특별한 의미를 가지며, 문자와 일치해야 하는 토큰에 표시될 때 백슬래시로 이스케이프해야 합니다. 쿼리 문자열은 정확한 문자열 일치와 특수 문자를 escape하기 위해 큰따옴표로 묶을 수 있습니다.
- **`field`**:검색어를 속성의 하위 집합과 일치시켜야 하는 경우 필드 매개 변수는 해당 속성의 경로를 나타낼 수 있습니다. 매개 변수를 반복하여 일치시킬 속성을 두 개 이상 지정할 수 있습니다.
- **`qop`**:검색의 일치 동작을 수정하는 데 사용되는 컨트롤 매개 변수를 포함합니다. 매개 변수가 로 설정된 경우 모든 검색어가 일치해야 하고 매개 변수가 없거나 해당 값이 로 설정된 경우 또는 어떤 검색어도 일치할 수 있습니다.

### 인스턴스 업데이트 및 패치

인스턴스를 업데이트하려면 클라이언트가 한 번에 전체 속성 목록을 덮어쓰거나 JSON PATCH 요청을 사용하여 목록을 포함한 개별 속성 값을 조작할 수 있습니다.

두 경우 모두 요청의 URL이 실제 인스턴스에 대한 경로를 지정하며 두 경우 모두 [만들기 작업에서](#create-instances)반환된 JSON 영수증 페이로드가 응답됩니다. 클라이언트는 가급적이면 이 개체에 대한 이전 API 호출에서 받은 `Location` 헤더 또는 HAL 링크를 이 API에 대한 전체 URL 경로로 사용해야 합니다. 이렇게 할 수 없는 경우 클라이언트는 `containerId` 및 에서 URL을 구성할 수 `instanceId`있습니다.

**요청** (PUT)

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**요청** (패치)

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

PATCH 요청은 지침을 적용한 다음 결과 엔티티가 스키마와 PUT 요청과 동일한 엔티티 및 참조 무결성 규칙에 대해 유효한지 확인합니다.

**속성 값 편집 제어**

다음 주석을 사용하여 작성 및/또는 업데이트 시 속성이 설정되지 않도록 할 수 있습니다.

- **`"meta:usereditable"`**:부울 - 사용자 또는 기술 계정 액세스 토큰을 사용하여 호출자를 식별하는 사용자 에이전트로부터 요청이 생성되면, 주석으로 연결된 속성이 페이로드에 `"meta:usereditable": false` 있으면 안 됩니다. 이러한 경우 현재 설정된 값과 다른 값을 가질 수 없습니다. 값이 다른 경우 업데이트 또는 패치 요청이 거부되고 상태 422 처리 취소 가능 엔티티가 반환됩니다.
- **`"meta:immutable"`**:부울 - 로 주석을 단 속성은 설정한 후에는 변경할 수 `"meta:immutable": true` 없습니다. 이는 최종 사용자의 요청, 기술 계정 통합 또는 특별 서비스에 적용됩니다.

**동시 업데이트 테스트**

여러 클라이언트가 동시에 인스턴스를 업데이트하려고 시도하는 조건이 있습니다. 저장소는 중앙 트랜잭션 관리 없이 컴퓨팅 노드 클러스터에서 작동합니다. 한 클라이언트가 다른 클라이언트에서 동시에 작성된 인스턴스를 쓰는 것을 방지하기 위해 클라이언트는 조건부 업데이트 또는 패치 요청을 사용할 수 있습니다. 헤더에 `etag` 문자열을 지정하면 첫 번째 요청만 성공하고 같은 `If-Match` `etag` 값을 사용하는 다른 클라이언트의 후속 요청만 실패하는지 확인합니다. 인스턴스가 수정될 때마다 값이 `etag` 변경됩니다. 클라이언트는 인스턴스를 검색하여 최신 `etag` 값을 얻은 다음 업데이트를 시도하는 여러 클라이언트 중 하나만 해당 값으로 성공할 수 있습니다. 다른 클라이언트는 409 충돌 메시지와 함께 거부됩니다.

### 인스턴스 삭제

인스턴스는 DELETE 호출로 삭제할 수 있습니다. 클라이언트는 이를 위한 이전 API 호출에서 수신한 `Location` 헤더 또는 HAL 링크를 전체 URL 경로로 사용해야 합니다. 이것이 불가능한 경우 클라이언트는 URL을 `containerId` 및 실제 URL에서 구성할 수 `instanceId`있습니다.

**요청**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**응답**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

삭제 요청을 받으면 저장소가 모든 스키마의 다른 인스턴스를 확인하지만 삭제할 인스턴스를 계속 참조합니다. 고가용성 시스템에서 참조 무결성을 즉시 확인할 수 없습니다. 외래 키 관계가 정의된 경우 비동기적으로 검사가 수행됩니다. 이렇게 하면 삭제 요청 결과에 대한 응답이 약간 지연됩니다. 이러한 검사가 수행되면 즉시 응답에는 202 수락됨 상태와 `Location` 헤더에서 삭제 작업의 결과를 확인하는 링크가 포함됩니다. 그러면 클라이언트는 해당 링크를 통해 결과를 확인해야 합니다.

삭제할 인스턴스를 참조하는 인스턴스가 발견되면 삭제 작업이 거부됩니다. 다른 외래 키 참조가 검색되지 않으면 삭제가 완료됩니다. 결과가 아직 결정되지 않은 경우 응답에 동일한 `Location` 헤더를 가진 다른 202 수락 응답으로 확인되고 클라이언트에게 계속 확인하도록 요청합니다. 결과가 결정되면 응답에 200개의 확인 상태와 응답의 페이로드에는 원래 삭제 요청의 결과가 포함됩니다. 200 확인 응답은 결과가 알려졌음을 의미하며 응답 본문에는 삭제 요청의 확인 또는 거부가 포함됩니다.

## 오퍼 및 하위 구성 요소 만들기

이전 섹션에서 설명한 API는 모든 유형의 비즈니스 객체에 일관되게 적용됩니다. 오퍼를 만들고 활동을 만드는 것은 JSON 스키마를 따르는 요청의 JSON 페이로드인 JSON 스키마를 설명하는 `content-type` 헤더가 될 것이라는 것과 같은 유일한 차이입니다. 따라서 다음 섹션은 해당 스키마와 스키마 간의 관계에만 초점을 맞춰야 합니다.

API를 컨텐츠 유형과 함께 사용할 `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`때 인스턴스의 자체 속성이 `_instance` 있는 속성 옆에 `_links` 포함됩니다. 모든 인스턴스가 표시되는 일반 형식이 됩니다.

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE] 간단히 설명하자면, 모든 JSON 조각에서 인스턴스 속성만 설명되며 필요한 경우에만 둘러싸기 속성 및 _links 섹션이 표시됩니다.

### 일반 오퍼 속성

오퍼는 의사 결정 옵션 유형이며 오퍼의 JSON 스키마는 각 옵션 인스턴스에 포함할 표준 옵션 속성을 상속합니다.

- **`@id`** - 기본 키이고 다른 개체의 옵션을 참조하는 데 사용되는 각 옵션의 고유 식별자입니다. 이 속성은 인스턴스가 생성될 때 지정되며, 변경할 수 없으며 편집할 수 없습니다.
- **`xdm:name`** - 모든 옵션에는 검색 및 표시 용도로 사용되는 이름이 있습니다. 이름을 변경할 수 없으며 인스턴스를 고유하게 식별하는 데 사용할 수 없습니다. 이름은 자유롭게 선택할 수 있지만 오퍼 인스턴스 전체에서 고유해야 합니다.

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 이 `schemaId` 매개 변수는 `https://ns.adobe.com/experience/offer-management/personalized-offer` 또는 오퍼가 폴백 오퍼인 `https://ns.adobe.com/experience/offer-management/fallback-offer` 경우에 사용해야 합니다.

각 오퍼 인스턴스에는 해당 인스턴스에만 특화된 선택적 속성 세트가 있을 수 있습니다. 오퍼마다 해당 속성에 대해 다른 키가 있을 수 있지만 값은 문자열이어야 합니다. 이러한 속성은 의사 결정 및 세그멘테이션 규칙에 사용할 수 있습니다. 또한 메시지를 사용자 정의할 수 있도록 정해진 환경을 구성할 수 있습니다.

### 오퍼 라이프사이클

모든 옵션이 따르는 간단한 상태 전환 흐름이 있습니다. 초안 상태에서 시작하여 준비가 되면 상태가 승인됨으로 설정됩니다. 종료 날짜가 지나면 보관된 상태로 이동할 수 있습니다. 그 상태에서, 그것들은 다시 드래프팅 상태로 옮겨서 삭제하거나 재사용할 수 있습니다.

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** - 이 속성은 인스턴스의 라이프사이클 관리에 사용됩니다. 이 값은 오퍼가 아직 건설 중인지(값 = 초안), 런타임에서 일반적으로 간주할 수 있는지(값 = 승인됨), 더 이상 사용하지 않아야 하는지(값 = 아카이브) 여부를 나타내는 데 사용되는 워크플로우 상태를 나타냅니다.

인스턴스에 대한 간단한 PATCH 작업은 일반적으로 `xdm:status` 속성을 조작하는 데 사용됩니다.

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 이 `schemaId` 매개 변수는 `https://ns.adobe.com/experience/offer-management/personalized-offer` 또는 오퍼가 폴백 오퍼인 `https://ns.adobe.com/experience/offer-management/fallback-offer` 경우에 사용해야 합니다.

### 표현 및 배치

오퍼는 컨텐츠 표현이 있는 결정 옵션입니다. 결정을 하면 옵션이 선택되고 해당 식별자는 제공해야 하는 배치에 대한 컨텐츠 또는 컨텐츠 참조를 가져오는 데 사용됩니다. 오퍼에는 둘 이상의 표현이 있을 수 있지만 각 오퍼에는 다른 배치 참조가 있어야 합니다. 이렇게 하면 지정된 배치를 통해 표현이 모호하게 결정될 수 있습니다.
의사 결정 작업 중에, 배치는 활동 개체와 함께 결정됩니다. 참조로 배치되는 표현이 없는 오퍼는 선택 항목 목록에서 자동으로 제거됩니다.

표현을 오퍼에 추가하려면 배치 인스턴스가 있어야 합니다. 이러한 인스턴스는 스키마 식별자를`https://ns.adobe.com/experience/offer-management/offer-placement`만듭니다.

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 이 `schemaId` 매개 변수는 `https://ns.adobe.com/experience/offer-management/personalized-offer` 또는 오퍼가 폴백 오퍼인 `https://ns.adobe.com/experience/offer-management/fallback-offer` 경우에 사용해야 합니다.

배치 **인스턴스는** 다음 속성을 가질 수 있습니다.

- **`xdm:name`** - 인간 상호 작용 및 사용자 인터페이스에서 배치의 지정된 이름을 포함합니다.
- **`xdm:description`** - 이 배치의 컨텐츠가 전체 메시지 전달에 사용되는 방법에 대해 사람이 읽을 수 있는 의도를 전달하는 데 사용됩니다. 전달 채널에서 새 배치를 정의할 때 컨텐츠 작성자가 그에 따라 컨텐츠를 만들거나 선택할 수 있도록 이 속성에 추가 정보를 추가할 수 있습니다. 이러한 지침은 공식적으로 해석되거나 시행되지 않습니다. 이 재산은 단지 의도를 전달하기 위한 장소일 뿐이다.
- **`xdm:channel`** - 채널의 URI입니다. 채널은 동적 컨텐츠가 전달될 위치를 나타냅니다. 채널 제약 조건은 오퍼를 사용할 위치뿐만 아니라 경험에 사용되는 컨텐츠 편집기 또는 유효성 검사기를 결정하는 데에도 사용됩니다.
- **`xdm:componentType`** - 이 배치에 설명된 위치에 표시할 수 있는 컨텐츠의 모델 식별자(예: URI)입니다. 구성 요소 유형은 다음과 같습니다.이미지 링크, html 또는 일반 텍스트. 각 구성 요소 유형은 컨텐츠 항목에 있을 수 있는 특정 속성 집합(모델)을 의미할 수 있습니다. 구성 요소 유형 목록을 확장할 수 있습니다. 사전 정의된 구성 요소 유형 값은 다음과 같이 세 가지가 있습니다.
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`**, 이 배치에 필요한 구성 요소의 미디어 유형에 대한 제한입니다. 다른 이미지 포맷과 같은 하나의 구성 요소 유형에 두 개 이상의 미디어 유형이 있을 수 있습니다.

**오퍼의** 표시 항목은 배열 속성에 개체 구조를 갖습니다 `xdm:representations`. 각 항목에는 다음 속성이 있을 수 있습니다.

- **`xdm:placement`** - 이 속성에는 배치 인스턴스에 대한 참조가 포함되어 있습니다. 오퍼에 표현을 추가하면 값이 확인됩니다. 해당 URI가 있는 배치 인스턴스가 존재해야 하며 삭제됨으로 표시되어서는 안 됩니다. 또한, 오퍼 인스턴스에 배치 참조에 대해 동일한 값을 가진 두 개의 표현이 없도록 검사가 수행됩니다.
- **`xdm:components`** - 컨텐츠 구성 요소는 특정 오퍼 표현과 연관된 조각입니다. 이러한 조각은 나중에 최종 사용자 경험을 구성하는 데 사용됩니다. 의사 결정 서비스 자체만으로는 전체 최종 사용자 경험이 작성되지는 않습니다. 다음 속성은 모든 구성 요소 모델의 일부입니다.
   - **`@type`** - 이 속성은 구성 요소 유형을 식별합니다. 이 개념의 다른 이름은 컨텐츠 조각 모델입니다. 구성 `@type` 요소의 URI는 최종 사용자 경험을 취합하는 응용 프로그램 또는 서비스에 의해 정의된 모델의 URI입니다.
   - **`repo:id`** - 이 속성에는 자산이 저장되는 저장소에 있는 구성 요소의 기본 리소스에 대한 전역으로 고유하고 변경할 수 없는 식별자가 포함됩니다.
   - **`repo:name`** - 이 속성에는 보관소의 자산에 대해 사람이 읽을 수 있는 이름이 포함되어 있습니다. 이 이름은 사용자가 정의하며 고유하도록 보장되지 않습니다.
   - **`repo:resolveURL`** - 이 속성에는 컨텐츠 저장소에서 자산을 읽을 수 있는 고유한 리소스 로케이터가 포함되어 있습니다. 이렇게 하면 클라이언트가 어떤 API를 호출할지 이해하지 않아도 에셋을 보다 쉽게 얻을 수 있습니다. URL은 자산의 기본 리소스의 바이트를 반환합니다.
   - **`dc:format`** - 이 속성은 Dublin Core Metadata Initiative에서 제공됩니다. 이 포맷은 리소스를 표시하거나 작동하기 위해 필요한 소프트웨어, 하드웨어 또는 기타 장비를 결정하는 데 사용될 수 있습니다. 제어된 단어(예: 컴퓨터 미디어 형식을 정의하는 인터넷 미디어 유형 목록)에서 값을 선택하는 것이 좋습니다.
   - **`dc:language`** - 이 속성은 리소스의 언어 또는 언어를 포함합니다. 언어는 IETF RFC 3066에 정의된 언어 코드에 지정됩니다.

속성에 표현되는 사전 정의된 구성 요소 유형은 세 가지가 `@type` 있습니다.

- https<span></span>://ns.adobe.com/experience/offer-management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-text
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-html

속성 값에 따라 `@type` 추가 속성이 `xdm:components` 포함됩니다.

- **`xdm:linkURL`** - 구성 요소가 이미지 링크일 때 표시됩니다. 이 속성에는 이미지와 연관된 링크가 포함되며 최종 사용자가 오퍼 컨텐츠와 상호 작용할 때 `user-agent` 탐색됩니다.
- **`xdm:copyline`** - 구성 요소가 텍스트일 때 사용됩니다. 텍스트 에셋을 참조하는 것 외에도, 예를 들어 서식이 있는 긴 양식 텍스트 오퍼의 경우 짧은 텍스트 문자열을 xdm:copyline 속성에 직접 저장할 수 있습니다.

클라이언트는 추가 속성을 사용하여 컨텍스트 처리 지침을 설정하고 평가할 수 있습니다. 예를 들어 오퍼 UI 라이브러리 클라이언트는 다음 선택적 속성을 추가하여 표시를 보다 쉽게 처리합니다.

- 배열의 각 항목 내부에 오퍼 라이브러리 UI 클라이언트가 다음 속성을 추가합니다. `xdm:components` 이러한 속성은 UI에 미치는 영향을 이해하지 않고 삭제하거나 조작해서는 안 됩니다.
   - **`offerui:previewThumbnail`** - 오퍼 라이브러리 UI에서 에셋 렌더링을 표시하는 데 사용하는 선택적 속성입니다. 이 변환은 자산 자체와 다릅니다. 예를 들어 컨텐츠는 HTML일 수 있고 변환은 비트맵 이미지이며 표현물의 근사치만 표시합니다. 이(낮은 품질) 변환은 오퍼의 표시 블록 내에 표시됩니다.

오퍼 인스턴스의 PATCH 작업 예는 표현을 조작하는 방법을 보여줍니다.

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 이 `schemaId` 매개 변수는 `https://ns.adobe.com/experience/offer-management/personalized-offer` 또는 오퍼가 폴백 오퍼인 `https://ns.adobe.com/experience/offer-management/fallback-offer` 경우에 사용해야 합니다.

속성이 `xdm:representations` 아직 없으면 PATCH 작업이 실패할 수 있습니다. 이 경우 위의 추가 작업 앞에 `xdm:representations` 배열을 만드는 다른 추가 작업 또는 단일 추가 작업이 배열을 직접 설정할 수 있습니다.
설명된 스키마 및 속성은 모든 오퍼 유형, 개인화 오퍼와 폴백 오퍼에 사용됩니다. 개인화 오퍼의 측면을 설명하는 제한 및 결정 규칙에 대한 다음 두 가지 섹션.

## 오퍼 제한 설정

### 달력 제한

일반적으로 의사 결정 옵션은 달력 제한 역할을 하는 시작 및 종료 날짜와 시간을 지정할 수 있습니다. 속성은 속성에 `xdm:selectionConstraint`포함됩니다.

- **`xdm:startDate`** - 이 속성은 시작 날짜와 시간을 나타냅니다. 이 값은 RFC 3339 규칙에 따라 형식이 지정된 문자열(예: 다음 타임스탬프)입니다.&quot;2019-06-13T11:21:23.356Z&quot;
시작 날짜 및 시간에 도달하지 않은 의사 결정 옵션은 의사 결정에서 아직 적격한 것으로 간주되지 않습니다.
- **`xdm:endDate`** - 이 속성은 종료 날짜와 시간을 나타냅니다. 이 값은 RFC 3339 규칙에 따라 형식이 지정된 문자열(예: 다음 타임스탬프)입니다.&quot;2019-07-13T11:00:00.000Z&quot;종료 날짜 및 시간이 지난 의사 결정 옵션이 더 이상 의사 결정 프로세스에서 적용되지 않습니다.

달력 제약 조건은 다음과 같은 PATCH 호출을 사용하여 변경할 수 있습니다.

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 매개 `schemaId` 변수는 반드시 사용해야 합니다 `https://ns.adobe.com/experience/offer-management/personalized-offer`. 폴백 오퍼에는 제한이 없습니다.

### 제한 적용

매핑 제약은 클릭 매개 변수를 정의하는 결정 옵션의 구성 요소입니다. 캡처한 작업은 개별 프로필뿐만 아니라 모든 프로필에 대해 옵션을 제안할 수 있는 횟수를 제한하는 프로세스입니다. 속성에는 1보다 크거나 같아야 하는 정수 값이 있습니다. 속성은 속성 내에 중첩됩니다 `xdm:cappingConstraint`.

- **`xdm:globalCap`** - 글로벌 CAP는 오퍼를 전체적으로 제안 횟수에 대한 제한을 의미합니다.
- **`xdm:profileCap`** - 프로필 끝은 특정 프로필에 오퍼를 제안할 수 있는 횟수에 대한 제한입니다.

개인화 오퍼에 대한 설정 또는 변경은 다음 PATCH 호출을 사용하여 수행할 수 있습니다.

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 매개 `schemaId` 변수는 반드시 사용해야 합니다 `https://ns.adobe.com/experience/offer-management/personalized-offer`. 폴백 오퍼에는 제한이 없습니다.

매핑 값을 제거하려면 작업 &quot;추가&quot;가 작업 &quot;제거&quot;로 대체됩니다. 매핑 값은 개별적으로 존재하며 개별적으로 설정하거나 제거할 수도 있습니다.

### 자격 조건

의사 결정 프로세스에서 조건부로 오퍼를 선택할 수 있습니다. 개인화 오퍼에 자격 규칙에 대한 참조가 있으면, 주어진 프로필에 대해 오퍼 개체가 고려되도록 규칙의 조건이 true로 평가되어야 합니다. 자격 조건 규칙은 의사 결정 옵션과 별도로 생성 및 관리되며, 동일한 규칙을 여러 개인화 오퍼에서 참조할 수 있습니다.

규칙에 대한 참조가 속성에 포함됩니다 `xdm:selectionConstraint`.

- **`xdm:eligibilityRule`** - 이 속성은 자격 조건 규칙에 대한 참조를 보유합니다. 값은 스키마https://ns.adobe.com/experience/offer-management/eligibility-rule `@id` 의 인스턴스입니다.

PATCH 작업을 통해 규칙을 추가 및 삭제할 수도 있습니다.

```
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 매개 `schemaId` 변수는 반드시 사용해야 합니다 `https://ns.adobe.com/experience/offer-management/personalized-offer`. 폴백 오퍼에는 제한이 없습니다.

자격 조건 규칙은 달력 제약 조건과 함께 `xdm:selectionConstraint` 속성에 포함됩니다. 패치 작업에서 전체 `SelectionConstraint` 속성을 제거하려고 하면 안 됩니다.

## 오퍼 우선 순위 설정

적격한 결정 옵션은 지정된 프로필에 가장 적합한 옵션을 결정하기 위해 등급이 지정됩니다. 등급을 지원하고 다른 메커니즘으로 등급을 결정할 수 없는 경우 기본값을 제공하기 위해 각 개인화 오퍼에 대해 기본 우선 순위를 설정할 수 있습니다.
기본 우선 순위는 속성에 `xdm:rank`포함됩니다.

- **`xdm:priority`** - 이 속성은 알려진 프로필 특정 등급 순서가 없는 경우 한 오퍼가 다른 오퍼에서 선택되는 기본 순서를 나타냅니다. 우선 순위 값을 비교한 후 두 개 이상의 개인화 오퍼가 여전히 연결되어 있는 경우, 임의로 선택되고 제안 제안에서 사용됩니다. 이 속성의 값은 0보다 크거나 같은 정수여야 합니다.

기본 우선 순위 조정은 다음 PATCH 호출을 사용하여 수행할 수 있습니다.

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 매개 `schemaId` 변수는 반드시 사용해야 합니다 `https://ns.adobe.com/experience/offer-management/personalized-offer`. 폴백 오퍼에는 등급 속성이 없습니다.

## 의사 결정 규칙 관리

자격 규칙에는 주어진 결정 옵션이 해당 프로필에 적합한지를 결정하기 위해 평가되는 조건이 있습니다. 하나 이상의 결정 옵션에 규칙을 첨부하면 이 옵션에 대해 규칙이 true로 평가되어야 이 사용자에게 고려됩니다. 규칙에는 프로필 속성에 대한 테스트가 포함될 수 있고, 이 프로필에 대한 경험 이벤트와 관련된 표현식을 평가할 수 있으며, 의사 결정 요청에 전달된 컨텍스트 데이터를 포함할 수 있습니다. 예를 들어, 조건을 다음과 같이 설명할 수 있습니다.

> &quot;엘리트 자격을 가진 개인들을 포함하여, 현 비행기의 비행번호를 가지고 있는 지난 6개월 동안 세 번 비행기를 탔습니다.&quot;

인스턴스는 스키마 identifierhttps://ns.adobe.com/experience/offer-management/eligibility-rule으로 만들어집니다. 만들기 또는 업데이트 호출에 대한 `_instance` 속성은 다음과 같습니다.

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 매개 `schemaId` 변수는 반드시 사용해야 합니다 `https://ns.adobe.com/experience/offer-management/eligibility-rule`.

규칙 조건 속성의 값에 PQL 표현식이 포함되어 있습니다. 컨텍스트 데이터는 특수 경로 식 @{schemaID}을 통해 참조됩니다.

규칙은 경험 플랫폼의 세그먼트에 맞게 자연스럽게 정렬되며, 종종 규칙은 프로필의 `segmentMembership` 속성을 테스트하여 세그먼트의 의도를 재사용합니다. 이 `segmentMembership` 속성에는 이미 평가된 세그먼트 조건의 결과가 포함되어 있습니다. 이를 통해 조직은 도메인 특정 대상을 한 번 정의하고 이름을 지정하고 조건을 한 번 평가할 수 있습니다.

## 오퍼 컬렉션 관리

### 태그 및 태그 지정 오퍼 만들기

각 컬렉션에서 적용할 필터 조건을 정의하는 컬렉션에서 오퍼를 구성할 수 있습니다. 현재 컬렉션의 필터 식에는 다음 두 가지 양식 중 하나를 사용할 수 있습니다.

1. 오퍼의 `@id` 매개 변수는 컬렉션에 있을 오퍼의 식별자 목록에 있는 매개 변수와 일치해야 합니다. 이 필터는 단순히 컬렉션의 오퍼의 URI를 열거한 것입니다.
2. 오퍼에는 태그 참조 목록이 있고 컬렉션의 필터는 태그 목록으로 구성됩니다. 오퍼는 다음 경우에 컬렉션에 있습니다.\
   a.오퍼의 태그 중 하나와 일치하는 필터의 태그\
   b.모든 필터의 태그가 오퍼 태그 중 하나와 일치합니다.

태그는 인스턴스를 연결할 수 있는 간단한 인스턴스입니다. 이러한 인스턴스는 이름을 사용하여 자체적으로 인스턴스로서 표시됩니다. 사용자 인터페이스에서 보다 쉽게 표시하려면 인스턴스 간에 이름이 고유해야 합니다.

태그 개체는 결정 옵션(오퍼) 간의 분류를 설정하는 데 사용됩니다. 태그는 많은 오퍼로 연결할 수 있으며 오퍼에는 많은 태그 참조가 있을 수 있습니다. 오퍼 카테고리는 주어진 태그 인스턴스 집합과 관련된 모든 오퍼를 참조하여 설정됩니다.

태그 인스턴스는 스키마 identifierhttps://ns.adobe.com/experience/offer-management/tag으로 만들어집니다. 만들기 또는 업데이트 호출에 대한 `_instance` 속성은 다음과 같습니다.

```json
{
  "xdm:name": "credit card"
} 
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 매개 `schemaId` 변수는 반드시 사용해야 합니다 `https://ns.adobe.com/experience/offer-management/tag`.


다음과 같은 태그 참조 목록을 사용하여 오퍼 인스턴스를 만들 수 있습니다.

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

또는 오퍼를 패치하여 태그 목록을 변경할 수 있습니다.

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

두 경우 모두 전체 cURL [구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치를 참조하십시오. 매개 `schemaId` 변수는 반드시 사용해야 합니다 `https://ns.adobe.com/experience/offer-management/personalized-offer`.

추가 작업이 성공하려면 `xdm:tags` 속성이 이미 있어야 합니다. 인스턴스에 태그가 없습니다. 패치 작업에서 먼저 배열 속성을 추가한 다음 해당 배열에 태그 참조를 추가할 수 있습니다.

### 오퍼 컬렉션에 대한 필터 정의

필터 인스턴스는 스키마 identifierhttps://ns.adobe.com/experience/offer-management/offer-filter으로 만들어집니다. 만들기 또는 업데이트 호출에 대한 `_instance` 속성은 다음과 같습니다.

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 매개 `schemaId` 변수는 반드시 사용해야 합니다 `https://ns.adobe.com/experience/offer-management/offer-filter`.

- **`xdm:filterType`** - 이 속성은 필터를 태그를 사용하여 설정할지 또는 ID로 오퍼를 직접 참조할지를 나타냅니다. 필터를 사용하여 태그를 사용하도록 설정하면 필터 유형이 모든 태그가 특정 오퍼의 태그와 일치해야 하는지 또는 주어진 태그 중 하나라도 필터의 자격을 갖추기에 충분한지 여부를 추가로 표시할 수 있습니다. 이 enum 속성의 유효한 값은 다음과 같습니다.
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** - 속성에는 의 값에 따라 인스턴스 또는 태그 인스턴스에 대한 참조인 URI의 배열이 포함됩니다 `xdm:filterType`..

다음 호출에서는 오퍼가 직접 참조되는 경우에 대비해 만들기 또는 업데이트 호출에 대한 `_instance` 속성이 어떻게 표시되는지를 보여 줍니다.

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## 활동 관리

오퍼 활동은 의사 결정 프로세스를 제어하는 데 사용됩니다. 이 보고서는 전체 인벤토리에 적용된 오퍼 필터를 지정하여 주제/카테고리별로 오퍼를 좁히고, 예약 공간에 맞는 오퍼로 재고를 좁히고, 결합된 제약 조건이 모든 사용 가능한 개인화 옵션(오퍼)의 자격을 박탈할 경우 대체 옵션을 지정합니다.

활동 인스턴스는 스키마 식별자를`https://ns.adobe.com/experience/offer-management/offer-activity`사용하여 만들어집니다. 만들기 또는 업데이트 호출에 대한 `_instance` 속성은 다음과 같습니다.

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 매개 `schemaId` 변수는 반드시 사용해야 합니다 `https://ns.adobe.com/experience/offer-management/offer-activity`.

- **`xdm:name`** - 이 필수 속성은 활동 이름을 포함합니다. 이 이름은 다양한 사용자 인터페이스에 표시됩니다.
- **`xdm:status`** - 이 속성은 인스턴스의 라이프사이클 관리에 사용됩니다. 이 값은 활동이 아직 건설 중인지를 나타내는 데 사용되는 워크플로우 상태(값 = 초안)를 나타내며, 일반적으로 런타임(값 = 라이브)에 의해 고려되거나 더 이상 사용하지 않아야 하는 경우(값 = 아카이브)를 나타냅니다.
- **`xdm:placement`** - 의사 결정이 이 활동의 컨텍스트로 만들어질 때 재고에 적용되는 오퍼 배치에 대한 참조를 포함하는 필수 속성입니다. 값은 사용되는 오퍼 배치의 URI(`@id`)입니다.
- **`xdm:filter`** - 이 활동의 컨텍스트에서 결정을 내릴 때 인벤토리에 적용되는 오퍼 필터에 대한 참조를 포함하는 필수 속성입니다. 값은 사용되는 오퍼 필터의 URI(`@id`)입니다.
- **`xdm:fallback`** - 폴백 오퍼에 대한 참조를 포함하는 필수 속성입니다. 이 활동에 대한 의사 결정이 개인화 오퍼를 제한하지 않는 경우 폴백 오퍼가 사용됩니다. 값은 폴백 오퍼 인스턴스의 URI(`@id`)입니다.

### 폴백 오퍼 관리

활동 인스턴스를 만들려면 먼저 활동의 배치에 적합한 폴백 오퍼가 있어야 합니다. 폴백 오퍼 인스턴스는 스키마 식별자를`https://ns.adobe.com/experience/offer-management/fallback-offer`사용하여 만들어집니다. 만들기 또는 업데이트 호출에 대한 `_instance` 속성은 개인화 오퍼에 있는 것과 동일한 일반 속성을 포함하지만 다른 제약 조건을 가질 수 없습니다.

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

전체 [cURL 구문에 대한 인스턴스](#updating-and-patching-instances) 업데이트 및 패치 적용을 참조하십시오. 매개 `schemaId` 변수는 반드시 사용해야 합니다 `https://ns.adobe.com/experience/offer-management/fallback-offer`.

