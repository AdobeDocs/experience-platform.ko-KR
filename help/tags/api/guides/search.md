---
title: Reactor API에서 리소스 검색
description: Reactor API에서 리소스를 검색하는 방법을 알아봅니다.
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Reactor API에서 리소스 검색

Reactor API의 `/search` 종단점을 사용하면 저장된 리소스에 대해 구조화된 쿼리를 만들 수 있습니다. 이 문서에서는 다양한 일반적인 사용 사례에 대한 다양한 검색 쿼리의 예를 제공합니다.

>[!NOTE]
>
>이 안내서를 읽기 전에 [검색 끝점 안내서](../endpoints/search.md)에서 허용되는 쿼리 구문 및 기타 사용 지침에 대한 정보를 참조하십시오.

## 기본 쿼리 전략

다음 예에서는 API의 검색 기능을 사용하기 위한 몇 가지 기본 개념을 보여줍니다.

### 여러 필드에서 검색

필드 이름에 와일드카드를 사용하여 여러 필드에서 검색을 수행할 수 있습니다. 예를 들어 여러 속성 필드에서 검색하려면 `attributes.*` 을 필드 이름으로 사용하십시오.

```json
{
  "data" : {
    "query": {
      "attributes.*": {
        "value": "evar7"
      }
    }
  }
}
```

>[!IMPORTANT]
>
>일반적으로 검색 값은 검색되는 데이터 유형과 일치해야 합니다. 예를 들어 정수 필드에 대한 `evar7` 쿼리 값이 실패합니다. 여러 필드에서 검색할 때 쿼리 유형 요구 사항이 오류를 방지하기 위해 완화되지만 원치 않는 결과를 생성할 수 있습니다.

### 특정 리소스 유형에 대한 범위 쿼리

요청에서 `resource_types`을 제공하여 검색을 특정 리소스 유형으로 범위를 지정할 수 있습니다. 예를 들어 `data_elements` 및 `rule_components`에서 검색하려면 다음을 수행하십시오.

```json
{
  "data" : {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

### 응답 정렬

`sort` 속성을 사용하여 응답을 정렬할 수 있습니다. 예를 들어 `created_at` 을 기준으로 가장 최근의 순서로 정렬하려면 다음을 수행합니다.

```json
{
  "data" : {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "sort": [
      {
        "attributes.created_at": "desc"
      }
    ],
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

## 일반적인 검색 예

다음 예제에서는 추가적인 일반적인 검색 패턴을 보여 줍니다.

### 특정 이름을 갖는 모든 리소스

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.name": {
              "value": "Adobe"
            }
          }
        }
      }'
```

### &quot;evar7&quot;을 참조하는 모든 리소스

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.*": {
              "value": "evar7"
            }
          }
        }
      }'
```

### &quot;사용자 지정 코드&quot; 위임 유형의 데이터 요소

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.delegate_descriptor_id": {
              "value": "custom-code"
            }
          },
          "resource_types": ["data_elements"]
        }
      }'
```

### 특정 데이터 요소를 참조하는 규칙 구성 요소

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.settings": {
              "value": "myDataElement8"
            }
          },
          "resource_types": ["rule_components"]
        }
      }'
```

### 특정 속성의 규칙

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "relationships.property.data.id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          },
          "resource_types": ["rules"]
        }
      }'
```

### ID별로 리소스 찾기

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          }
        }
      }'
```

### &quot;OR&quot; 용어 논리를 사용하여 검색 수행

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.display_name": {
              "value": "My Rule Holiday Sale",
              "value_operator: "OR"
            }
          }
        }
      }'
```
