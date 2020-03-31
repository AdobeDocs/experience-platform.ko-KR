---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: API를 사용하여 의사 결정 서비스 런타임 사용
topic: tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# API를 사용하여 의사 결정 서비스 런타임 사용

이 문서에서는 Adobe Experience Platform API를 사용하여 의사 결정 서비스의 런타임 서비스를 사용하는 방법에 대한 자습서를 제공합니다.

## 시작하기

이 자습서에서는 의사 결정 및 고객 경험 동안 제공할 다음 최고의 제안을 결정하는 데 관련된 경험 플랫폼 서비스를 제대로 이해해야 합니다. 이 자습서를 시작하기 전에 다음 사항에 대한 설명서를 검토하십시오.

- [의사 결정 서비스](./../home.md):오퍼를 추가 및 제거하고 고객 경험 중에 표시할 최적의 알고리즘을 선택할 수 있는 프레임워크를 제공합니다.
- [XDM(Experience Data Model)](../../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [PQL(프로필 쿼리 언어)](../../segmentation/pql/overview.md):PQL은 규칙 및 필터를 정의하는 데 사용됩니다.
- [API를 사용하여 의사 결정 개체 및 규칙 관리](./entities.md):의사 결정 서비스 런타임을 사용하기 전에 관련 엔티티를 설정해야 합니다.

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

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../tutorials/authentication.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

런타임 요청에도 필요합니다.

- x-request-id: `{UUID}`

>[!NOTE] UUID 형식의 `UUID` 문자열로서, 전역적으로 고유하며, 다른 API 호출에 재사용할 수 없습니다.

의사 결정 서비스는 서로 관련된 여러 비즈니스 개체에 의해 제어됩니다. 모든 비즈니스 객체는 플랫폼의 비즈니스 객체 저장소인 XDM 핵심 객체 저장소에 저장됩니다. 이 저장소의 주요 기능은 API가 비즈니스 객체 유형과 수직이라는 것입니다. API 끝점의 리소스 유형을 나타내는 POST, GET, PUT, PATCH 또는 DELETE API를 사용하는 대신, 6개의 일반 끝점만 있지만 이러한 모호성이 필요할 때 개체의 유형을 나타내는 매개 변수를 수락하거나 반환합니다. 스키마는 저장소에 등록되어 있어야 하지만, 저장소가 열려 있는 객체 유형 집합에서 사용할 수 있다는 점을 넘어

모든 XDM 코어 개체 저장소 API의 끝점 경로는 다음으로 `https://platform.adobe.io/data/core/ode/`시작합니다.

끝점 다음의 첫 번째 경로 요소는 `containerId`입니다. 이 식별자는 XDM 코어 개체 저장소 루트 끝점을 통해 `GET https://platform.adobe.io/data/core/xcore/`얻습니다.

## 의사 결정 모델 작성

비즈니스 논리 엔티티 활성화는 자동으로 지속적으로 이루어집니다. 새 옵션이 저장소에 저장되고 &quot;승인됨&quot;으로 표시된 즉시 사용 가능한 옵션 세트를 포함하는 후보자가 됩니다. 결정 규칙이 업데이트되면 규칙 세트가 다시 조합되어 런타임 실행을 위해 준비됩니다. 이 자동 활성화 단계에서는 런타임 컨텍스트에 종속되지 않는 비즈니스 논리로 정의된 모든 제한을 평가합니다. 이 활성화 단계의 결과는 Decision Service 런타임에서 사용할 수 있는 캐시에 전송됩니다.

### 배치, 필터 및 라이프사이클 상태의 효과

오퍼는 지속적으로 생성되거나, 오퍼의 라이프사이클 상태가 변경되거나, 새로운 컨텐츠 표현을 가져올 수 있습니다. 활동의 오퍼 필터는 태그 세트가 업데이트된 오퍼를 변경하거나 일치시키거나 필터링할 수 있습니다. 이 프로세스는 상당히 관련이 있을 수 있으며 애플리케이션 및 서비스는 활동의 결과 후보 세트가 무엇인지 알아야 합니다. 의사 결정 런타임은 승인되지 않은 오퍼를 필터링하거나, 오퍼 필터와 일치하지 않거나, 활동에 의해 참조되는 배치에 대한 표현이 없는 오퍼를 필터링하는 API를 제공합니다.

**요청**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**응답**

매개 변수는 URL에서 반복할 `activityId` 수 있으며 하나의 요청에서 최대 30개의 다른 활동 참조를 지정할 수 있습니다. 이 응답은 설정 결과로 발생하는 예기치 않은 상황을 파악하는 데 유용하며 다음과 같습니다.

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

개체가 업데이트되는 시간과 API 응답이 활동-오퍼 매핑을 반영하는 시간 사이에 몇 초 정도의 지연이 있습니다. 각 객체의 수정은 응답에 제공되므로 클라이언트가 반영되지 않은 객체에 대한 업데이트가 있는지 확인할 수 있습니다.

### 진단 API 및 문제 해결

활동, 오퍼 및 자격 조건 규칙은 의사 결정 서비스 런타임에서 사용하는 내부 형식(런타임 오퍼 카탈로그)으로 컴파일됩니다. 컴파일은 객체가 저장되고 링크가 XDM 코어 객체 리포지토리에 설정되었을 때 수행되는 검사에서 포착되지 않은 오류를 감지할 수 있습니다.

진단 API가 제공되어 해당 단계에서 발생한 컴파일 오류를 입수하고 규칙과 활동이 마지막으로 다시 컴파일된 시기에 대한 정보를 얻는 데 오류가 없는 경우.

**요청**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

이 API 호출에 대한 유일한 매개 변수는 `containerId`입니다. 그 결과 해당 컨테이너에서 의사 결정 규칙, 오퍼, 활동 또는 오퍼 필터가 수정된 모든 클라이언트의 모든 업데이트가 표시됩니다. 개체가 업데이트되는 시간과 컴파일이 끝난 시간 사이에 몇 초 정도의 지연이 있습니다. 마지막 업데이트 타임스탬프와 모든 오류는 진단 호출에 대한 응답으로 반환됩니다.

**응답**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## REST API 호출을 사용하여 의사 결정 실행

REST API는 조직에서 사용자를 위해 설정한 규칙, 모델 및 제한 사항을 기반으로 한 다음 최상의 경험을 얻기 위해 플랫폼 위에서 실행되는 응용 프로그램을 위한 경로 중 하나입니다. 응용 프로그램은 프로필의 ID(프로필 ID 및 ID 네임스페이스) 중 하나를 보냅니다. 의사 결정 서비스가 프로필을 조회하고 이 정보는 비즈니스 논리를 적용하는 데 사용됩니다. 추가 컨텍스트 데이터는 요청에 전달될 수 있으며 비즈니스 규칙에 지정된 경우 데이터에 포함시켜 결정을 내릴 수 있습니다.

최대 30개의 활동에 대한 결정을 한 번에 요청하여 애플리케이션의 성능을 향상시킬 수 있습니다. 활동의 URI는 동일한 요청에서 전달됩니다. REST API는 동기적이며, 제약 조건을 충족하지 않는 개인화 옵션이 없을 경우 이러한 모든 활동에 대해 제안된 옵션이나 대체 옵션을 반환합니다.

두 개의 다른 활동들이 그들의 &quot;최고&quot;와 같은 옵션을 생각해낼 수 있다. 작성된 경험을 반복하지 않도록 하기 위해 기본적으로 의사 결정 서비스는 동일한 요청에서 참조되는 활동 간을 조정합니다. 중재는 각 활동에 대해 최상위 N개 옵션이 고려되지만 해당 활동에 대해 두 번 이상 옵션이 제안되지 않음을 의미합니다. 두 활동이 가장 순위가 같은 옵션을 갖는 경우 두 번째 최상의 선택 또는 세 번째 최상의 선택 등을 사용할 수 있습니다. 이러한 중복 제거 규칙은 어떤 활동에서도 폴백 옵션을 사용해야 한다는 것을 방지합니다.

결정 요청에는 POST 요청의 해당 본문에 대한 인수가 포함되어 있습니다. 본문은 JSON `Content-Type` 헤더 값으로 형식이 지정됩니다. `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

현재 지원되는 요청 스키마와 버전은 `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`입니다. 나중에 추가 요청 스키마 또는 버전이 제공됩니다.

**요청**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** - 이 옵션 속성의 값이 true로 설정되면 결정 요청이 제한 조건을 따르지만 실제로 카운터에 표시되지 않습니다. 호출자가 프로파일로 제안을 표시하지 않을 것이라는 예상입니다. 의사 결정 서비스는 이 제안을 공식 XDM 의사 결정 이벤트로 기록하지 않으며 보고 데이터 세트에 나타나지 않습니다. 이 속성의 기본값은 false이며, 속성을 생략하면 테스트 실행으로 간주되지 않으므로 최종 사용자에게 표시됩니다.
- **`xdm:validateContextData`** - 이 선택적 속성은 컨텍스트 데이터의 유효성 검사를 켜거나 끕니다. 유효성 검사를 활성화한 경우 제공된 각 컨텍스트 데이터 항목에 대해 XDM 레지스트리에서 스키마( `@type` 필드를 기반으로 함)를 가져오게 되고 해당 `xdm:data` 개체에 대해 유효성 검사가 수행됩니다.

이 스키마당 요청에는 오퍼 활동, 프로필 ID 및 컨텍스트 데이터 항목의 배열을 참조하는 URI 배열이 포함됩니다.

- **`xdm:offerActivities`** - 이 필수 속성은 각 항목에 오퍼 활동에 대한 데이터가 포함된 객체의 배열입니다. 오퍼 활동에는 다음 속성이 있습니다.
   - **`xdm:offerActivity`** - 활동의 고유 식별자(URI)입니다. 오퍼 활동의 `@id` 속성 값입니다.
- **`xdm:identityMap`** - XDM 스키마를 따르는 JSON 개체를 보유하는 필수 속성입니다 `https://ns.adobe.com/xdm/context/identitymap`. 이 속성은 키가 ID 네임스페이스 코드이고 값이 지정된 네임스페이스의 최종 사용자 식별자 목록입니다. 만약 m.
- **`xdm:contextData`** - 스키마에 대한 참조로 설명된 항목이 포함된 선택적 속성입니다. 배열의 각 컨텍스트 데이터 항목에는 다음 속성이 있어야 합니다.
   - **`@type`** - 이 항목에 있는 개체의 XDM 스키마를 참조하는 필수 속성입니다.
   - **`xdm:data`** - 속성에 지정된 XDM 스키마당 개체 속성을 포함하는 필수 `@type` 속성입니다.

## 의사 결정 요청의 동적 컨텍스트 데이터

이전 섹션에서는 XDM 개체를 의사 결정 요청으로 전달하는 방법을 설명했습니다. 다음은 이러한 컨텍스트 객체 배열의 예입니다.

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

스키마는 조직에서 만들었어야 합니다. 스키마 구성에 대한 자세한 내용은 스키마 편집기 [자습서를 참조하십시오](../../xdm/tutorials/create-schema-ui.md). 스키마가 네임스페이스에 `https://ns.adobe.com/{TENANT_ID}/schemas`있습니다.

스키마 [레지스트리 API 개발자 안내서는](../../xdm/tutorials/create-schema-api.md) 프로그래밍 방식으로 스키마에 액세스할 수 있는 방법과 개발자가 테넌트 ID와 스키마의 숫자 식별자를 얻는 방법에 대해 설명합니다. 버전 번호는 필수이며 스키마 레지스트리 API에서도 제공됩니다.

조직에서 정의한 스키마에는 일반적으로 테넌트 네임스페이스 문자열이라고도 `_{TENANT_ID}`하는 루트 속성이 있습니다.
전역 스키마 구성 요소(_`https://ns.adobe.com/xdm/context/product` )에서 사용되는 속성에는 네임스페이스 접두어가 `xdm:`있습니다. 이 경우 조직 정의 속성이 해당 데이터 형식으로 `productDetails` 생성되었습니다. 테넌트 속성이 테넌트 네임스페이스 다음에 명명된 속성에 중첩되는 동안 전역적으로 사용할 수 있는 데이터 형식은 예약된 접두사를 사용하여 속성 이름 충돌을 `xdm:` 방지합니다.

여러 데이터 개체를 `xdm:contextData` 속성에 나열할 수 있습니다. 각 개체는 `@type` 속성을 통해 해당 형식을 식별해야 합니다.
컨텍스트 데이터 개체의 값은 PQL 표현식에서 사용할 수 있습니다(예: 자격 조건). 컨텍스트 데이터 개체는 특수 경로 참조 표현식을 통해 해결되어야 합니다 `@{schemaId}`. 이 참조 표현식 다음에 나오는 표현식은 데이터 개체의 속성에 액세스하는 일반 경로 표현식입니다.

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

위의 예에서, 변수는 `p` = `@type` `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`로 표시된 개체 배열을 반복하고 있습니다.

PQL 구문은 속성 이름에 접두사를 사용하지 않습니다. 기본적으로 전역 속성은 `xdm:` 접두사 없이 참조됩니다. 조직에서 정의하는 속성은 테넌트 네임스페이스(변수에 의해 표시된 예제)의 **추가** 속성 내에 중첩됩니다 `{TENANT_ID}`. 사용자 정의 속성을 직접 참조할 수 있도록 변수는 추가 중첩 속성을 참조하는 경로의 결과에 `p` 바인딩됩니다.

## 프로필 레코드 사용

프로필 및 경험 이벤트 엔티티에 대한 모든 레코드는 이미 프로필 저장소에서 관리됩니다. 하나 이상의 프로필 ID를 요청에 전달하면 해당 ID에 대한 프로필이 식별되어 스토어에서 검색됩니다. 그런 다음 의사 결정 규칙 및 의사 결정 전략에 의해 평가된 모델에 데이터를 자동으로 사용할 수 있습니다.

프로필 및 경험 레코드를 검색하려면 기본 병합 정책이 적용됩니다.
프로필 레코드를 플랫폼 데이터에 업로드한 후 프로필 레코드를 조회할 때까지 약간의 지연이 있습니다. 스트리밍 API를 통해 프로필 및 경험 레코드를 인제스트하는 경우에도 몇 초 후에 프로필 및 경험 이벤트 데이터를 평가하는 결정 규칙을 평가하는 데 데이터를 사용할 수 있습니다.