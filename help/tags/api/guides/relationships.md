---
title: Reactor API의 관계
description: 각 리소스에 대한 관계 요구 사항을 포함하여 Reactor API에서 리소스 관계를 설정하는 방법에 대해 알아봅니다.
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 6%

---

# Reactor API의 관계

Reactor API의 리소스는 서로 관련이 있는 경우가 많습니다. 이 문서에서는 API에서 리소스 관계가 설정되는 방식과 각 리소스 유형의 관계 요구 사항에 대한 개요를 제공합니다.

해당 리소스의 유형에 따라 몇 가지 관계가 필요합니다. 필수 관계는 상위 리소스가 관계 없이 존재할 수 없음을 의미합니다. 다른 모든 관계는 선택 사항입니다.

필수 또는 선택 사항인지 여부에 관계없이 관계는 관련 리소스가 생성될 때 시스템에 의해 자동으로 설정되거나 수동으로 생성되어야 합니다. 수동으로 관계를 만드는 경우 해당 리소스에 따라 두 가지 방법이 있습니다.

* [페이로드로 만들기](#payload)
* [URL로 만들기](#url) (라이브러리만 해당)

의 섹션을 참조하십시오. [관계 요구 사항](#requirements) 각 리소스 유형에 대해 호환되는 관계 목록 및 해당되는 경우 해당 관계를 설정하는 데 필요한 메서드를 참조하십시오.

## 페이로드로 관계 만들기 {#payload}

리소스를 처음 만들 때 일부 관계를 수동으로 설정해야 합니다. 이를 수행하려면 다음을 제공해야 합니다. `relationship` 상위 리소스를 처음 만들 때 요청 페이로드의 개체입니다. 이러한 관계의 예는 다음과 같습니다.

* [데이터 요소 만들기](../endpoints/data-elements.md#create) 필요한 확장 기능 포함
* [환경 만들기](../endpoints/environments.md#create) 필수 호스트 관계 사용

**API 형식**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| 매개변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 리소스가 속한 속성의 ID입니다. |
| `{RESOURCE_TYPE}` | 만들 리소스의 유형입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 새 를 만듭니다 `rule_component`, 와 관계 설정 `rules` 및 `extension`.

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
| `relationships` | 페이로드로 관계를 만들 때 제공해야 하는 개체입니다. 이 개체의 각 키는 특정 관계 유형을 나타냅니다. 위의 예에서, `extension` 및 `rules` 관계는 다음과 같이 설정됩니다. `rule_components`. 다른 리소스에 대해 호환되는 관계 유형에 대한 자세한 내용은 [자원별 관계 요구 사항](#relationship-requirements-by-resource). |
| `data` | 아래에 제공된 각 관계 유형 `relationship` 객체에는 다음이 포함되어야 합니다: `data` 속성, 참조 `id` 및 `type` 을(를) 통해 관계를 설정하고 있습니다. 형식을 지정하여 동일한 유형의 여러 리소스와 관계를 만들 수 있습니다. `data` 속성을 객체의 배열로 사용하며 각 객체에는 `id` 및 `type` 적용 가능한 리소스 |
| `id` | 리소스의 고유 ID입니다. 각 `id` 형제자매와 동반해야 합니다. `type` 속성, 해당 리소스의 유형을 나타냅니다. |
| `type` | 형제 자매가 참조하는 리소스의 유형 `id` 필드. 허용되는 값은 다음과 같습니다 `data_elements`, `rules`, `extensions`, 및 `environments`. |

{style="table-layout:auto"}

## URL로 관계 만들기 {#url}

도서관은 다른 자원과 달리 자신의 전용 자원을 통해 관계를 구축한다 `/relationship` 엔드포인트. 해당 예는 다음과 같습니다.

* [라이브러리에 확장, 데이터 요소 및 규칙 추가](../endpoints/libraries.md#add-resources)
* [환경에 라이브러리 할당](../endpoints/libraries.md#environment)

**API 형식**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 매개변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 라이브러리가 속한 속성의 ID입니다. |
| `{LIBRARY_ID}` | 관계를 만들 라이브러리의 ID입니다. |
| `{RESOURCE_TYPE}` | 관계가 타겟팅하는 리소스의 유형입니다. 사용 가능한 값은 다음과 같습니다 `environment`, `data_elements`, `extensions`, 및 `rules`. |

**요청**

다음 요청은 `/relationships/environment` 환경과의 관계를 만드는 라이브러리의 종단점입니다.

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
| `data` | 를 참조하는 개체 `id` 및 `type` 관계의 대상 리소스. 동일한 유형의 여러 리소스로 관계를 만드는 경우(예: `extensions` 및 `rules`), `data` 속성은 개체의 배열로 형식화되어야 하며, 각 개체에는 `id` 및 `type` 적용 가능한 리소스 |
| `id` | 리소스의 고유 ID입니다. 각 `id` 형제자매와 동반해야 합니다. `type` 속성, 해당 리소스의 유형을 나타냅니다. |
| `type` | 형제 자매가 참조하는 리소스의 유형 `id` 필드. 허용되는 값은 다음과 같습니다 `data_elements`, `rules`, `extensions`, 및 `environments`. |

{style="table-layout:auto"}

## 자원별 관계 요구 사항 {#requirements}

다음 표에서는 각 리소스 유형에 사용할 수 있는 관계, 해당 관계가 필요한지 여부 및 해당되는 경우 관계를 수동으로 만들 수 있는 허용 방법에 대해 설명합니다.

>[!NOTE]
>
>관계가 페이로드 또는 URL로 생성된 것으로 나열되지 않으면 시스템에서 관계를 자동으로 지정합니다.

### 이벤트 감사

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ 덧신 |  |  |
| `entity` | ✓ |  |  |

{style="table-layout:auto"}

### 빌드

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 콜백

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 회사

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style="table-layout:auto"}

### 데이터 요소

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### 환경

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 확장

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### 호스트

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 라이브러리

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
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

{style="table-layout:auto"}

### 참고

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style="table-layout:auto"}

### 속성

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style="table-layout:auto"}

### 규칙 구성 요소

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style="table-layout:auto"}

### 규칙

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### 비밀

| 관계 | 필수 여부 | 페이로드로 만들기 | URL로 만들기 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

