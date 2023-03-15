---
title: Reactor API에서 리소스 검색
description: Reactor API에서 리소스를 검색하는 방법을 알아봅니다.
exl-id: cb594e60-3e24-457e-bfb3-78ec84d3e39a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Reactor API에서 리소스 검색

다음 `/search` reactor API의 끝점을 사용하면 저장된 리소스에 대해 구조화된 쿼리를 만들 수 있습니다. 이 문서에서는 다양한 일반적인 사용 사례에 대한 다양한 검색 쿼리의 예를 제공합니다.

>[!NOTE]
>
>이 안내서를 읽기 전에 다음을 참조하십시오. [검색 끝점 안내서](../endpoints/search.md) 허용되는 쿼리 구문 및 기타 사용 지침에 대한 정보입니다.

## 기본 쿼리 전략

다음 예에서는 API의 검색 기능 사용에 대한 몇 가지 기본 개념을 보여 줍니다.

### 여러 필드 검색

필드 이름에 와일드카드를 사용하여 여러 필드에서 검색을 수행할 수 있습니다. 예를 들어 여러 속성 필드를 검색하려면 `attributes.*` 를 필드 이름으로 사용하십시오.

```json
{
  "data": {
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
>일반적으로 검색 값은 검색 중인 데이터 유형과 일치해야 합니다. 예를 들어 쿼리 값 `evar7` 정수 필드에 대해 오류가 발생합니다. 여러 필드에서 검색할 때 오류를 방지하기 위해 쿼리 유형 요구 사항을 완화하지만 원하지 않는 결과가 발생할 수 있습니다.

### 특정 리소스 유형으로 쿼리 범위 지정

다음을 입력하여 특정 리소스 유형으로 검색 범위를 지정할 수 있습니다. `resource_types` 요청에서. 예를 들어 을 사용하여 검색할 수 있습니다 `data_elements`, 및 `rule_components`:

```json
{
  "data": {
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

다음 `sort` 속성을 사용하여 응답을 정렬할 수 있습니다. 예를 들어 다음 기준으로 정렬하려면 `created_at` 최신 버전 먼저:

```json
{
  "data": {
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

다음 예제에서는 일반적인 추가 검색 패턴을 보여 줍니다.

### 특정 이름을 가진 모든 리소스

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "relationships.property.data.id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          },
          "resource_types": ["rules"]
        }
      }'
```

### ID로 리소스 찾기

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "query": {
            "attributes.display_name": {
              "value": "My Rule Holiday Sale",
              "value_operator: "OR"
            }
          }
        }
      }'
```
