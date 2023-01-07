---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Experience Platform API 기본 사항
description: 이 문서에서는 Experience Platform API와 관련된 일부 기본 기술 및 구문에 대한 간략한 개요를 제공합니다.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# Experience Platform API 기본 사항

Adobe Experience Platform API는 JSON 기반의 을 효과적으로 관리하기 위해 알고 있어야 하는 몇 가지 기본 기술 및 구문을 사용합니다 [!DNL Platform] 리소스 를 참조하십시오. 이 문서에서는 이러한 기술에 대한 간략한 개요와 자세한 내용을 보려면 외부 설명서 링크를 제공합니다.

## JSON 포인터 {#json-pointer}

JSON 포인터는 표준화된 문자열 구문([RFC 6901](https://tools.ietf.org/html/rfc6901)) JSON 문서 내에서 특정 값을 식별하는 데 사용됩니다. JSON 포인터는 로 구분된 토큰 문자열입니다 `/` 개체 키 또는 배열 인덱스를 지정하고 토큰은 문자열 또는 숫자일 수 있는 문자입니다. JSON 포인터 문자열은 [!DNL Platform] 이 문서의 뒷부분에 설명된 대로 API를 참조하십시오. JSON 포인터에 대한 자세한 내용은 [JSON 포인터 개요 설명서](https://rapidjson.org/md_doc_pointer.html).

### JSON 스키마 객체 예

다음 JSON은 JSON 포인터 문자열을 사용하여 필드를 참조할 수 있는 간소화된 XDM 스키마를 나타냅니다. 사용자 지정 스키마 필드 그룹(예: `loyaltyLevel`)은 `_{TENANT_ID}` 객체 와 달리, 핵심 필드 그룹(예: `fullName`)가 아닙니다.

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

### 스키마 개체를 기반으로 한 JSON 포인터 예

| JSON 포인터 | 해결 대상 |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (에 대한 참조 반환 `fullName` 필드(핵심 필드 그룹에서 제공) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (에 대한 참조 반환 `loyaltyLevel` 필드(사용자 지정 필드 그룹에서 제공) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>를 처리할 때 `xdm:sourceProperty` 및 `xdm:destinationProperty` 속성 [!DNL Experience Data Model] (XDM) 설명자, `properties` 키가 있어야 합니다. **제외** 를 반환합니다. 자세한 내용은 [!DNL Schema Registry] API 개발자 안내서 하위 안내서 [설명자](../xdm/api/descriptors.md) 추가 정보.

## JSON 패치 {#json-patch}

에는 많은 PATCH 작업이 있습니다 [!DNL Platform] 요청 페이로드에 대해 JSON 패치 개체를 허용하는 API입니다. JSON 패치는 표준화된 형식([RFC 6902](https://tools.ietf.org/html/rfc6902)) JSON 문서의 변경 사항을 설명하는 데 사용됩니다. 요청 본문에 전체 문서를 보낼 필요 없이 JSON에 대한 부분 업데이트를 정의할 수 있습니다.

### 예제 JSON Patch 개체

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: 패치 작업의 유형입니다. 반면 JSON 패치는 의 일부 다른 작업 유형을 지원하지만, 일부 PATCH 작업은에서 지원하지 않습니다 [!DNL Platform] API는 모든 작업 유형과 호환됩니다. 사용 가능한 작업 유형은 다음과 같습니다.
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: 업데이트할 JSON 구조의 일부이며, 를 사용하여 식별됩니다 [JSON 포인터](#json-pointer) 표기법.

에 표시된 작업 유형에 따라 `op`, JSON 패치 객체에는 추가 속성이 필요할 수 있습니다. 다양한 JSON 패치 작업 및 필요한 구문에 대한 자세한 내용은 [JSON 패치 설명서](https://datatracker.ietf.org/doc/html/rfc6902).

## JSON 스키마 {#json-schema}

JSON 스키마는 JSON 데이터 구조를 설명하고 유효성을 검사하는 데 사용되는 형식입니다. [XDM(경험 데이터 모델)](../xdm/home.md) 은 JSON 스키마 기능을 활용하여 수집된 고객 경험 데이터의 구조 및 형식에 제한을 적용합니다. JSON 스키마에 대한 자세한 내용은 다음을 참조하십시오. [공식 문서](https://json-schema.org/).

## 다음 단계

이 문서에서는 [!DNL Experience Platform]. 자세한 내용은 [시작 안내서](api-guide.md) 를 참조하십시오. 자주 묻는 질문에 대한 답변은 [플랫폼 문제 해결 안내서](troubleshooting.md).
