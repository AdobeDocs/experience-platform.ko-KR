---
keywords: Experience Platform;홈;매퍼;매핑 세트;매핑;
solution: Experience Platform
title: 매핑 세트 개요
description: Adobe Experience Platform 데이터 준비와 함께 매핑 세트를 사용하는 방법을 알아봅니다.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# 매핑 세트 개요

매핑 세트는 데이터를 한 스키마에서 다른 스키마로 변환하는 매핑 세트입니다. 이 문서에서는 입력 스키마, 출력 스키마 및 매핑을 포함하여 매핑 세트를 구성하는 방법에 대한 정보를 제공합니다.

## 시작하기

이 개요를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

- [데이터 준비](./home.md): 데이터 준비를 통해 데이터 엔지니어는 XDM(Experience Data Model)과 데이터를 매핑, 변환 및 확인할 수 있습니다.
- [데이터 흐름](../dataflows/home.md): 데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 데이터 흐름은 서로 다른 서비스에 걸쳐 구성되어 데이터를 소스 커넥터에서 대상 데이터 세트로 이동하는 데 도움이 됩니다. [!DNL Identity] 및 [!DNL Profile], 및 까지 [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): 데이터를 전송할 수 있는 방법 [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.

## 매핑 세트 구문

매핑 세트는 ID, 이름, 입력 스키마, 출력 스키마 및 연결된 매핑 목록으로 구성됩니다.

다음 JSON은 일반적인 매핑 세트의 예입니다.

```json
{
    "id": "cbb0da769faa48fcb29e026a924ba29d",
    "name": "Demo Mapping Set",
    "inputSchema": {
        "id": "a167ff2947ff447ebd8bcf7ef6756232",
        "version": 0
    },
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/6dd1768be928c36d58ad4897219bb52d491671f966084bc0",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "Id",
            "destination": "_id",
            "name": "Id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "FirstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "LastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 매핑 세트에 대한 고유 식별자. |
| `name` | 매핑 세트의 이름입니다. |
| `inputSchema` | 들어오는 데이터에 대한 XDM 스키마. |
| `outputSchema` | 입력 데이터가 따라야 할 XDM 스키마가 변환됩니다. |
| `mappings` | 소스 스키마에서 대상 스키마로의 필드 간 매핑 배열입니다. |
| `sourceType` | 나열된 각 매핑에 대해 `sourceType` 속성은 매핑될 소스의 유형을 나타냅니다. 다음 중 하나일 수 있습니다. `ATTRIBUTE`, `STATIC`, 또는 `EXPRESSION`: <ul><li> `ATTRIBUTE` 소스 경로에 있는 모든 값에 사용됩니다. </li><li>`STATIC` 대상 경로에 삽입된 값에 사용됩니다. 이 값은 일정하게 유지되며 소스 스키마의 영향을 받지 않습니다.</li><li> `EXPRESSION` 는 런타임 중에 확인되는 표현식에 사용됩니다. 사용 가능한 표현식 목록은 [매핑 함수 안내서](./functions.md).</li> </ul> |
| `source` | 나열된 각 매핑에 대해 `source` 속성은 매핑할 필드를 나타냅니다. 소스를 구성하는 방법에 대한 자세한 내용은 [소스 섹션](#sources). |
| `destination` | 나열된 각 매핑에 대해 `destination` 속성은 필드 또는 필드의 경로를 나타내며, 여기서 값은 `source` 필드가 배치됩니다. 대상을 구성하는 방법에 대한 자세한 내용은 [대상 섹션](#destination). |
| `mappings.name` | (*선택 사항*) 매핑의 이름입니다. |
| `mappings.description` | (*선택 사항*) 매핑에 대한 설명입니다. |

## 매핑 소스 구성

매핑에서 `source` 는 필드, 표현식 또는 정적 값일 수 있습니다. 주어진 소스 유형을 기반으로 다양한 방법으로 값을 추출할 수 있다.

### 열 형식 데이터의 필드

CSV 파일과 같은 열 형식 데이터의 필드를 매핑할 때 `ATTRIBUTE` 소스 유형. 필드에 `.` 이름 내에서 `\` 값을 이스케이프 처리합니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

**샘플 CSV 파일:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**샘플 매핑**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**변환된 데이터**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 중첩된 데이터의 필드

JSON 파일과 같은 중첩된 데이터의 필드를 매핑할 때 다음을 사용합니다. `ATTRIBUTE` 소스 유형. 필드에 `.` 이름 내에서 `\` 값을 이스케이프 처리합니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

**샘플 JSON 파일**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**샘플 매핑**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**변환된 데이터**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 배열 내 필드

배열 내의 필드를 매핑할 때 인덱스를 사용하여 특정 값을 검색할 수 있습니다. 이렇게 하려면 `ATTRIBUTE` 소스 유형 및 매핑할 값의 색인. 이 매핑의 예는 아래에서 찾을 수 있습니다.

**샘플 JSON 파일**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**샘플 매핑**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**변환된 데이터**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### 배열에서 배열 또는 개체에서 개체로

사용 `ATTRIBUTE` 소스 유형을 사용하면 배열 또는 객체를 객체에 직접 매핑할 수도 있습니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

**샘플 JSON 파일**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**샘플 매핑**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**변환된 데이터**

```json
{
    "pi": {
        "emailList": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

### 스토리지 시스템에서 반복 작업

사용 `ATTRIBUTE` 소스 유형에서는 배열을 반복적으로 루프하고 와일드카드 인덱스(`[*]`). 이 매핑의 예는 아래에서 찾을 수 있습니다.

**샘플 JSON 파일**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**샘플 매핑**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**변환된 데이터**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

### 상수 값

상수 또는 정적 값을 매핑하려면 `STATIC` 소스 유형.  사용 시 `STATIC` 소스 유형, `source` 에 지정할 하드 코딩된 값을 나타냅니다. `destination`. 이 매핑의 예는 아래에서 찾을 수 있습니다.

**샘플 JSON 파일**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**샘플 매핑**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**변환된 데이터**

```json
{
    "userType:": "CUSTOMER"
}
```

### 표현식

표현식을 매핑하려면 `EXPRESSION` 소스 유형. 허용되는 함수 목록은 [매핑 함수 안내서](./functions.md). 사용 시 `EXPRESSION` 소스 유형, `source` 은 해결할 함수를 나타냅니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

**샘플 JSON 파일**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**샘플 매핑**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**변환된 데이터**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## 매핑 대상 구성

매핑에서 `destination` 은 값에서 값을 추출하는 위치입니다. `source` 을(를) 삽입합니다.

### 루트 수준의 필드

을(를) 매핑하려는 경우 `source` 값을 변환된 데이터의 루트 수준으로 지정하려면 아래 예를 따르십시오.

**샘플 JSON 파일**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**샘플 매핑**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**변환된 데이터**

```json
{
    "name": "John Smith"
}
```

### 중첩된 필드

을(를) 매핑하려는 경우 `source` 변환된 데이터의 중첩 필드에 대한 값은 아래 예를 참조하십시오.

**샘플 JSON 파일**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**샘플 매핑**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**변환된 데이터**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 특정 배열 인덱스의 필드

을(를) 매핑하려는 경우 `source` 값이 변환된 데이터의 배열에서 특정 인덱스에 지정되면 아래 예를 따르십시오.

**샘플 JSON 파일**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**샘플 매핑**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**변환된 데이터**

```json
{
    "piList": ["John Smith"]
}
```

### 반복적 배열 작업

배열을 반복적으로 루프하고 값을 대상에 매핑하려면 와일드카드 인덱스(`[*]`). 이에 대한 예는 아래에서 확인할 수 있습니다.

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**샘플 매핑**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**변환된 데이터**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

## 다음 단계

이 문서를 읽은 후에는 매핑 세트 내에서 개별 매핑을 구성하는 방법을 포함하여 매핑 세트가 구성되는 방법을 이해해야 합니다. 다른 데이터 준비 기능에 대한 자세한 내용은 [데이터 준비 개요](./home.md). 데이터 준비 API 내에서 매핑 세트를 사용하는 방법에 대해 알아보려면 다음을 참조하십시오. [데이터 준비 개발자 안내서](./api/overview.md).
