---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: PQL 변환
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# PQL 변환

intro

- pql/text 및 pql/json에서 서식 변환

## 시작하기

이 안내서에서 사용되는 API 끝점은 세그멘테이션 API의 일부입니다. 계속하기 전에 세그멘테이션 개발자 [안내서를](./getting-started.md)검토하십시오.

특히 세그멘테이션 개발자 안내서의 [시작 섹션은](./getting-started.md#getting-started) 관련 항목에 대한 링크, 문서에서 샘플 API 호출 읽기에 대한 안내, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 포함합니다.

## pql/text 및 pql/json에서 서식 변환

**API 형식**

```http
POST /segment/conversion
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "People who ordered in the last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "ttlInDays": 60
}
 '
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 세그먼트 정의에 대한 고유한 이름입니다. |
| `expression.type` | 표현식 유형입니다. 그것은 `PQL` 또는 `ARL`일 수 있습니다. |
| `expression.format` | 표현식 형식입니다. 그것은 `pql/text` 또는 `pql/json`일 수 있습니다. |
| `expression.value` | 변환할 식의 쿼리 문자열입니다. |
| `schema.name` | 참조하는 스키마의 클래스 ID. |
| `ttlInDays` | TTL(Time to Live)을 나타내는 정수입니다. |

**응답**

성공적인 응답은 변환된 세그먼트에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## 다음 단계
