---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Experience Platform API 기본 사항
description: 이 문서에서는 Experience Platform API와 관련된 몇 가지 기본 기술 및 구문에 대한 간략한 개요를 제공합니다.
role: Developer
feature: API
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# Experience Platform API 기본 사항

Adobe Experience Platform API는 JSON 기반 [!DNL Platform] 리소스를 효과적으로 관리하기 위해 이해해야 하는 몇 가지 기본 기술과 구문을 사용합니다. 이 문서에서는 이러한 기술에 대한 간략한 개요와 외부 설명서에 대한 링크를 제공합니다.

## JSON 포인터 {#json-pointer}

JSON 포인터는 JSON 문서 내의 특정 값을 식별하기 위한 표준화된 문자열 구문([RFC 6901](https://tools.ietf.org/html/rfc6901))입니다. JSON 포인터는 개체 키 또는 배열 인덱스를 지정하는 `/`자로 구분된 토큰 문자열이며 토큰은 문자열 또는 숫자일 수 있습니다. JSON 포인터 문자열은 이 문서의 뒷부분에 설명된 대로 [!DNL Platform] API에 대한 많은 PATCH 작업에 사용됩니다. JSON Pointer에 대한 자세한 내용은 [JSON Pointer 개요 설명서](https://rapidjson.org/md_doc_pointer.html)를 참조하세요.

### 예제 JSON 스키마 오브젝트

다음 JSON은 JSON 포인터 문자열을 사용하여 필드를 참조할 수 있는 간소화된 XDM 스키마를 나타냅니다. 사용자 지정 스키마 필드 그룹(예: `loyaltyLevel`)을 사용하여 추가된 모든 필드는 `_{TENANT_ID}` 개체 아래에 네임스페이스가 지정되지만 핵심 필드 그룹(예: `fullName`)을 사용하여 추가된 필드는 지정되지 않습니다.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### 스키마 오브젝트 기반 JSON 포인터 예

| JSON 포인터 | 다음으로 해결: |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (코어 필드 그룹에서 제공한 `fullName` 필드에 대한 참조를 반환합니다.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | 사용자 지정 필드 그룹에서 제공한 `loyaltyLevel` 필드에 대한 참조를 반환합니다. |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>[!DNL Experience Data Model](XDM) 설명자의 `xdm:sourceProperty` 및 `xdm:destinationProperty` 특성을 처리할 때 JSON 포인터 문자열에서 `properties` 키를 **제외**&#x200B;해야 합니다. 자세한 내용은 [설명자](../xdm/api/descriptors.md)의 [!DNL Schema Registry] API 개발자 안내서 하위 가이드를 참조하십시오.

## JSON 패치 {#json-patch}

[!DNL Platform] API에 대해 요청 페이로드에 JSON 패치 개체를 허용하는 많은 PATCH 작업이 있습니다. JSON 패치는 JSON 문서의 변경 내용을 설명하기 위한 표준화된 형식([RFC 6902](https://tools.ietf.org/html/rfc6902))입니다. 요청 본문에 전체 문서를 전송할 필요 없이 JSON에 대한 부분 업데이트를 정의할 수 있습니다.

### 예제 JSON 패치 오브젝트

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: 패치 작업의 유형입니다. JSON 패치가 여러 가지 다양한 작업 유형을 지원하지만 [!DNL Platform] API의 모든 PATCH 작업이 모든 작업 유형과 호환되는 것은 아닙니다. 사용 가능한 작업 유형은 다음과 같습니다.
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: 업데이트할 JSON 구조의 일부로, [JSON 포인터](#json-pointer) 표기법을 사용하여 식별됩니다.

`op`에 표시된 작업 유형에 따라 JSON 패치 개체에 추가 속성이 필요할 수 있습니다. 다른 JSON 패치 작업 및 필요한 구문에 대한 자세한 내용은 [JSON 패치 설명서](https://datatracker.ietf.org/doc/html/rfc6902)를 참조하십시오.

## JSON 스키마 {#json-schema}

JSON 스키마는 JSON 데이터의 구조를 설명하고 유효성을 검사하는 데 사용되는 형식입니다. [XDM(경험 데이터 모델)](../xdm/home.md)은(는) JSON 스키마 기능을 활용하여 수집된 고객 경험 데이터의 구조와 형식에 제한을 적용합니다. JSON 스키마에 대한 자세한 내용은 [공식 설명서](https://json-schema.org/)를 참조하세요.

## 다음 단계

이 문서에서는 [!DNL Experience Platform]에 대한 JSON 기반 리소스 관리와 관련된 일부 기술 및 구문을 소개했습니다. 모범 사례를 포함한 Platform API 작업에 대한 자세한 내용은 [시작 안내서](api-guide.md)를 참조하십시오. FAQ에 대한 답변은 [플랫폼 문제 해결 안내서](troubleshooting.md)를 참조하세요.
