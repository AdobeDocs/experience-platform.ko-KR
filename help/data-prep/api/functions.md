---
keywords: Experience Platform;홈;인기 항목;데이터 준비;api 안내서;스키마;
title: 함수 API 끝점
description: 데이터 준비 API에서 "/functions" 끝점을 사용하여 매핑 표현식의 유효성을 검사하고 사용 가능한 매핑 세트 기능을 나열할 수 있습니다.
exl-id: dc24bfb4-2d96-4757-a610-0c2ee960d41d
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 2%

---

# 함수 엔드포인트

매핑 세트 기능을 사용하면 소스 및 대상 스키마 간에 데이터를 변환할 수 있습니다. `/languages/el` 끝점을 사용하여 표현식의 유효성을 검사하고 사용 가능한 모든 매핑 집합 함수의 목록을 가져올 수 있습니다.

## 표현식 유효성 검사

`/languages/el/validate` 끝점에 대한 POST 요청을 통해 현재 식이 유효한지 확인할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**응답**

성공적인 응답은 표현식의 유효성 검사 상태와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## 목록 매핑 집합 함수

`/languages/el/functions` 끝점에 대한 GET 요청을 통해 사용 가능한 모든 매핑 집합 함수 목록을 검색할 수 있습니다.

**API 형식**

```
GET /languages/el/functions
```

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 사용 가능한 모든 매핑 세트 함수 목록과 함께 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>이 응답은 공백으로 잘렸습니다.

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

## 목록 매핑 세트 연산자

`/languages/el/operators` 끝점에 대한 GET 요청을 통해 사용 가능한 모든 매핑 집합 연산자 목록을 검색할 수 있습니다.

**API 형식**

```
GET /languages/el/operators
```

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 사용 가능한 모든 매핑 세트 연산자 목록과 함께 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>이 응답은 공백으로 잘렸습니다.

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
