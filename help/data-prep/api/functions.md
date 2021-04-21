---
keywords: Experience Platform;홈;인기 항목;데이터 준비;api 안내서;스키마;home;popular topics;data prepare;api guide;schemas;
solution: Experience Platform
title: 스키마 API 끝점
topic-legacy: schemas
description: Adobe Experience Platform API의 '/functions' 끝점을 사용하여 매핑 표현식과 사용 가능한 매핑 집합 함수를 확인할 수 있습니다.
exl-id: dc24bfb4-2d96-4757-a610-0c2ee960d41d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 2%

---

# 함수 끝점

매핑 집합 함수를 사용하면 소스 및 대상 스키마 간에 데이터를 변형할 수 있습니다. `/languages/el` 끝점을 사용하여 표현식의 유효성을 확인하고 사용 가능한 모든 매핑 집합 함수 목록을 가져올 수 있습니다.

## 표현식 유효성 검사

`/languages/el/validate` 끝점에 POST 요청을 함으로써 현재 표현식이 유효한지 확인할 수 있습니다.

**API 형식**

```
POST /languages/el/validate
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**응답**

성공적인 응답은 표현식의 유효성 검사 상태로 HTTP 상태 200을 반환합니다.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## 목록 매핑 집합 함수

`/languages/el/functions` 끝점에 GET 요청을 함으로써 사용할 수 있는 모든 매핑 집합 함수 목록을 검색할 수 있습니다.

**API 형식**

```
GET /languages/el/functions
```

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 사용 가능한 모든 매핑 집합 함수 목록이 포함된 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>이 응답은 공간에 대해 잘렸습니다.

```json
[
    {
        "category": "Date / Time",
        "function": "date",
        "description": "Function that converts date string into a ZonedDateTime object.",
        "syntax": "ZonedDateTime date(String, String, ZonedDateTime)",
        "returns": "Returns the date object that is formatted in given format or a default date if the expression evaluates to a null date.",
        "returnType": "java.time.ZonedDateTime",
        "example": "",
        "result": "",
        "params": [],
        "since": 1
    },
    {
        "category": "Hierarchies - Arrays",
        "function": "first",
        "description": "Function to retrieve the first element of the given array.",
        "syntax": "T first(T...)",
        "returns": "The first element or null if the array is null or empty.",
        "returnType": "java.lang.Object",
        "example": "first(\"1\", \"2\", \"3\")",
        "result": "\"1\"",
        "params": [
            {
                "name": "values",
                "description": "Zero or more arguments",
                "type": "object",
                "dataType": "[Ljava.lang.Object;",
                "position": 1
            }
        ],
        "since": 1
    }
]
```

## 목록 매핑 집합 연산자

`/languages/el/operators` 종단점에 GET 요청을 함으로써 사용할 수 있는 모든 매핑 집합 연산자 목록을 검색할 수 있습니다.

**API 형식**

```
GET /languages/el/operators
```

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 사용 가능한 모든 매핑 집합 연산자 목록이 있는 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>이 응답은 공간에 대해 잘렸습니다.

```json
[
    {
        "operatorSymbol": "+",
        "methodName": "add",
        "numberOfOperands": 2,
        "description": "Simple arithmetic addition",
        "example": "1 + 2"
    },
    {
        "operatorSymbol": "/",
        "methodName": "divide",
        "numberOfOperands": 2,
        "description": "Simple arithmetic division",
        "example": "1 / 2"
    },
    {
        "operatorSymbol": "~",
        "methodName": "complement",
        "numberOfOperands": 1,
        "description": "The usual ~ operator is used, e.g.\n~33\n, ~0010 0001 = 1101 1110 = -34.",
        "example": "~44"
    },
    {
        "operatorSymbol": "-",
        "methodName": "negate",
        "numberOfOperands": 1,
        "description": "The unary - operator is used. For example\n-12",
        "example": "-12"
    },
    {
        "operatorSymbol": "!",
        "methodName": "not",
        "numberOfOperands": 1,
        "description": "The usual ! operator can be used as well as the word not, e.g.\n!cond1\nand\nnot cond1\nare equivalent",
        "example": "!cond1"
    }
]
```
