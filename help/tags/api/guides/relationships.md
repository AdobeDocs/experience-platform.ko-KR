---
title: Reactor API의 관계
description: 각 리소스에 대한 관계 요구 사항을 포함하여 Reactor API에서 리소스 관계가 설정되는 방법을 알아봅니다.
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 10%

---

# Reactor API의 관계

Reactor API의 리소스는 서로 관련되어 있습니다. 이 문서에서는 API에서 리소스 관계가 설정되는 방식과 각 리소스 유형의 관계 요구 사항에 대한 개요를 제공합니다.

해당 리소스의 유형에 따라 일부 관계가 필요합니다. 필수 관계는 상위 리소스가 관계 없이 존재할 수 없음을 의미합니다. 다른 모든 관계는 선택 사항입니다.

필수 또는 선택 사항인지에 관계없이, 관련 리소스를 만들 때 시스템에서 관계를 자동으로 설정하거나 수동으로 만들어야 합니다. 관계를 수동으로 만드는 경우, 해당 리소스에 따라 가능한 두 가지 방법이 있습니다.

* [페이로드별로 만들기](#payload)
* [URL별 만들기](#url) (라이브러리 전용)

의 섹션을 참조하십시오. [관계 요구 사항](#requirements) 각 리소스 유형에 대한 호환 관계 목록 및 해당하는 경우 이러한 관계를 설정하는 데 필요한 방법을 설명합니다.

## 페이로드별 관계 만들기 {#payload}

처음 리소스를 만들 때 일부 관계를 수동으로 설정해야 합니다. 이를 수행하려면 다음을 제공해야 합니다 `relationship` 상위 리소스를 처음 만들 때 요청 페이로드에 있는 개체. 이러한 관계의 예는 다음과 같습니다.

* [데이터 요소 만들기](../endpoints/data-elements.md#create) 필요한 확장 사용
* [환경 만들기](../endpoints/environments.md#create) 필요한 호스트 관계 사용

**API 형식**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 리소스가 속한 속성의 ID입니다. |
| `{RESOURCE_TYPE}` | 만들 리소스 유형입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청으로 새 항목이 만들어집니다 `rule_component`, 관계 설정 `rules` 그리고 `extension`.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/rule_components \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EXa2865f4d14204fa094f247406424371b",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLd53598e3f1884e63bbc8e9c95e463dcf",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `relationships` | 페이로드별로 관계를 만들 때 제공해야 하는 개체입니다. 이 개체의 각 키는 특정 관계 유형을 나타냅니다. 위의 예에서 `extension` 및 `rules` 관계가 형성되고, 특히 `rule_components`. 서로 다른 리소스의 호환 관계 유형에 대한 자세한 내용은 [리소스별 관계 요구 사항](#relationship-requirements-by-resource). |
| `data` | 아래에 제공된 각 관계 유형 `relationship` 객체에는 다음이 포함되어야 합니다. `data` 속성을 참조하는 속성입니다 `id` 및 `type` 리소스 중에서 어떤 관계를 설정하고 있는지 확인합니다. 서식을 지정하여 같은 유형의 여러 리소스와 관계를 만들 수 있습니다 `data` 속성을 객체 배열로서 설정하고 각 객체는 `id` 및 `type` 해당 리소스 |
| `id` | 리소스의 고유 ID입니다. 각 `id` 형제와 함께 있어야 합니다 `type` 해당 리소스의 유형을 나타내는 속성입니다. |
| `type` | 동위 멤버가 참조하는 리소스 유형입니다. `id` 필드. 허용되는 값은 다음과 같습니다 `data_elements`, `rules`, `extensions`, 및 `environments`. |

{style=&quot;table-layout:auto&quot;}

## URL별 관계 만들기 {#url}

다른 리소스와 달리 라이브러리는 자신의 전용 리소스를 통해 관계를 구축합니다 `/relationship` 엔드포인트. 해당 예는 다음과 같습니다.

* [라이브러리에 확장, 데이터 요소 및 규칙 추가](../endpoints/libraries.md#add-resources)
* [환경에 라이브러리 할당](../endpoints/libraries.md#environment)

**API 형식**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 라이브러리가 속한 속성의 ID입니다. |
| `{LIBRARY_ID}` | 관계를 만들 라이브러리의 ID입니다. |
| `{RESOURCE_TYPE}` | 관계가 타깃팅하는 리소스의 유형입니다. 사용 가능한 값은 다음과 같습니다 `environment`, `data_elements`, `extensions`, 및 `rules`. |

**요청**

다음 요청에서는 `/relationships/environment` 브라우저가 환경과의 관계를 만들 수 있는 끝점입니다.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/libraries/LB10c1fd171cd347f19fcb8659a8d679ef/relationships/environment \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "id": "ENf395a477d2b24ad696d65b901055b9dc",
          "type": "environments",
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `data` | 를 참조하는 개체 `id` 및 `type` 관계를 위한 대상 리소스의 경로입니다. 같은 유형의 여러 리소스와 관계를 만드는 경우(예: `extensions` 및 `rules`), `data` 속성은 객체 배열로 포맷되어야 하며 각 객체에는 `id` 및 `type` 해당 리소스 |
| `id` | 리소스의 고유 ID입니다. 각 `id` 형제와 함께 있어야 합니다 `type` 해당 리소스의 유형을 나타내는 속성입니다. |
| `type` | 동위 멤버가 참조하는 리소스 유형입니다. `id` 필드. 허용되는 값은 다음과 같습니다 `data_elements`, `rules`, `extensions`, 및 `environments`. |

{style=&quot;table-layout:auto&quot;}

## 리소스별 관계 요구 사항 {#requirements}

다음 표에서는 각 리소스 유형에 대해 사용 가능한 관계, 해당 관계가 필요한지 여부 및 해당하는 경우 관계를 수동으로 생성하는 허용 방법에 대해 설명합니다.

>[!NOTE]
>
>관계가 페이로드 또는 URL에 의해 만들어져서 나열되지 않으면 시스템에 의해 자동으로 할당됩니다.

### 감사 이벤트

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 빌드

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 콜백

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 회사

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### 데이터 요소

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 환경

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 확장

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 호스트

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 라이브러리

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | ✓ |
| `data_elements` |  |  | ✓ |
| `extensions` |  |  | ✓ |
| `rules` |  |  | ✓ |
| `notes` |  |  |  |
| `upstream_library` | ✓ |  |  |
| `property` | ✓ |  |  |
| `last_build` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### 참고

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 속성

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### 규칙 구성 요소

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 규칙

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### 비밀

| 관계 | 필수 여부 | 페이로드별로 만들기 | URL별 만들기 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

