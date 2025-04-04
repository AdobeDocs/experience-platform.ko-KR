---
keywords: Experience Platform;홈;매퍼;매핑 세트;매핑;
solution: Experience Platform
title: 매핑 세트 개요
description: Adobe Experience Platform 데이터 준비와 함께 매핑 세트를 사용하는 방법을 알아봅니다.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# 매핑 세트 개요

매핑 세트는 데이터를 한 스키마에서 다른 스키마로 변환하는 매핑 세트입니다. 이 문서에서는 입력 스키마, 출력 스키마 및 매핑을 포함하여 매핑 세트를 구성하는 방법에 대한 정보를 제공합니다.

## 시작하기

이 개요를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

- [데이터 준비](./home.md): 데이터 준비를 통해 데이터 엔지니어는 데이터를 XDM(Experience Data Model)에 매핑하고, 변환하고, 유효성을 검사할 수 있습니다.
- [데이터 흐름](../dataflows/home.md): 데이터 흐름은 Experience Platform에서 데이터를 이동하는 데이터 작업을 나타냅니다. 데이터 흐름은 여러 서비스에 걸쳐 구성되어 있으므로 데이터를 소스 커넥터에서 대상 데이터 세트로, [!DNL Identity] 및 [!DNL Profile], [!DNL Destinations]&#x200B;(으)로 이동하는 데 도움이 됩니다.
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): 데이터를 [!DNL Experience Platform]에 보낼 수 있는 메서드입니다.
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

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
| `sourceType` | 나열된 각 매핑에 대해 해당 `sourceType` 특성은 매핑할 원본 형식을 나타냅니다. `ATTRIBUTE`, `STATIC` 또는 `EXPRESSION` 중 하나일 수 있습니다. <ul><li> `ATTRIBUTE`은(는) 원본 경로에 있는 모든 값에 사용됩니다. </li><li>`STATIC`은(는) 대상 경로에 삽입된 값에 사용됩니다. 이 값은 일정하게 유지되며 소스 스키마의 영향을 받지 않습니다.</li><li> `EXPRESSION`은(는) 런타임 중에 확인되는 식에 사용됩니다. 사용 가능한 식 목록은 [매핑 함수 안내서](./functions.md)에서 찾을 수 있습니다.</li> </ul> |
| `source` | 나열된 각 매핑에 대해 `source` 특성은 매핑할 필드를 나타냅니다. 소스를 구성하는 방법에 대한 자세한 내용은 [소스 개요](../sources/home.md)에서 확인할 수 있습니다. |
| `destination` | 나열된 각 매핑에 대해 `destination` 특성은 필드 또는 필드에 대한 경로를 나타내며, 여기에서 `source` 필드에서 추출된 값이 배치됩니다. 대상을 구성하는 방법에 대한 자세한 내용은 [대상 개요](../destinations/home.md)에서 확인할 수 있습니다. |
| `mappings.name` | (*선택 사항*) 매핑의 이름입니다. |
| `mappings.description` | (*선택 사항*) 매핑에 대한 설명입니다. |

## 매핑 소스 구성

매핑에서 `source`은(는) 필드, 식 또는 정적 값일 수 있습니다. 주어진 소스 유형을 기반으로 다양한 방법으로 값을 추출할 수 있다.

### 열 형식 데이터의 필드

CSV 파일과 같은 열 형식 데이터의 필드를 매핑할 때 `ATTRIBUTE` 소스 형식을 사용하십시오. 필드에 이름 안에 `.`이(가) 있으면 `\`을(를) 사용하여 값을 이스케이프 처리합니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

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

JSON 파일과 같은 중첩 데이터의 필드를 매핑할 때 `ATTRIBUTE` 소스 유형을 사용하십시오. 필드에 이름 안에 `.`이(가) 있으면 `\`을(를) 사용하여 값을 이스케이프 처리합니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

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

배열 내의 필드를 매핑할 때 인덱스를 사용하여 특정 값을 검색할 수 있습니다. 이렇게 하려면 `ATTRIBUTE` 원본 형식과 매핑할 값의 인덱스를 사용합니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

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

`ATTRIBUTE` 소스 형식을 사용하여 배열을 배열에 직접 매핑하거나 개체를 개체에 직접 매핑할 수도 있습니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

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

`ATTRIBUTE` 소스 형식을 사용하여 배열을 반복적으로 루프하고 와일드카드 인덱스(`[*]`)를 사용하여 대상 스키마에 매핑할 수 있습니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

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

상수 또는 정적 값을 매핑하려면 `STATIC` 원본 형식을 사용하십시오.  `STATIC` 소스 형식을 사용하는 경우 `source`은(는) `destination`에 할당할 하드 코딩된 값을 나타냅니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

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

식을 매핑하려면 `EXPRESSION` 원본 형식을 사용합니다. 허용되는 함수 목록은 [매핑 함수 안내서](./functions.md)에서 찾을 수 있습니다. `EXPRESSION` 소스 형식을 사용하는 경우 `source`은(는) 확인하려는 함수를 나타냅니다. 이 매핑의 예는 아래에서 찾을 수 있습니다.

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

매핑에서 `destination`은(는) `source`에서 추출된 값이 삽입되는 위치입니다.

### 루트 수준의 필드

`source` 값을 변환된 데이터의 루트 수준에 매핑하려면 아래 예를 따르십시오.

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

`source` 값을 변환된 데이터의 중첩 필드에 매핑하려면 아래 예를 따르십시오.

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

`source` 값을 변환된 데이터의 배열에 있는 특정 인덱스에 매핑하려면 아래 예를 따르십시오.

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

배열을 반복하여 값을 대상으로 매핑하려면 와일드카드 인덱스(`[*]`)를 사용할 수 있습니다. 이에 대한 예는 아래에서 확인할 수 있습니다.

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

이 문서를 읽은 후에는 매핑 세트 내에서 개별 매핑을 구성하는 방법을 포함하여 매핑 세트가 구성되는 방법을 이해해야 합니다. 다른 데이터 준비 기능에 대한 자세한 내용은 [데이터 준비 개요](./home.md)를 참조하십시오. 데이터 준비 API에서 매핑 세트를 사용하는 방법에 대해 알아보려면 [데이터 준비 개발자 안내서](./api/overview.md)를 읽어 보십시오.
