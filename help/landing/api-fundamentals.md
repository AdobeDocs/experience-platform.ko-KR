---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Experience Platform API 기본 사항
description: 이 문서에서는 Experience Platform API와 관련된 몇 가지 기본 기술 및 구문에 대한 간략한 개요를 제공합니다.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# Experience Platform API 기본 사항

Adobe Experience Platform API는 JSON 기반을 효과적으로 관리하기 위해 이해해야 하는 몇 가지 기본 기술 및 구문을 사용합니다 [!DNL Platform] 리소스. 이 문서에서는 이러한 기술에 대한 간략한 개요와 외부 설명서에 대한 링크를 제공합니다.

## JSON 포인터 {#json-pointer}

JSON 포인터는 표준화된 문자열 구문([RFC 6901](https://tools.ietf.org/html/rfc6901))를 사용하여 JSON 문서 내에서 특정 값을 식별할 수 있습니다. JSON 포인터는 토큰으로 구분된 문자열입니다. `/` 개체 키 또는 배열 인덱스를 지정하는 문자 및 토큰은 문자열 또는 숫자일 수 있습니다. JSON 포인터 문자열은 의 다양한 PATCH 작업에 사용됩니다. [!DNL Platform] 이 문서의 뒷부분에 설명되어 있는 API입니다. JSON Pointer에 대한 자세한 내용은 [JSON Pointer 개요 설명서](https://rapidjson.org/md_doc_pointer.html).

### 예제 JSON 스키마 오브젝트

다음 JSON은 JSON 포인터 문자열을 사용하여 필드를 참조할 수 있는 간소화된 XDM 스키마를 나타냅니다. 사용자 정의 스키마 필드 그룹을 사용하여 추가된 모든 필드(예: `loyaltyLevel`) 아래에 네임스페이스가 지정됨 `_{TENANT_ID}` 개체와 달리 핵심 필드 그룹을 사용하여 추가된 필드(예: `fullName`)은(는) 아닙니다.

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
| `"/properties/person/properties/name/properties/fullName"` | (에 대한 참조를 반환합니다. `fullName` 필드, 코어 필드 그룹에서 제공) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (에 대한 참조를 반환합니다. `loyaltyLevel` 필드, 사용자 정의 필드 그룹에서 제공) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>을(를) 처리할 때 `xdm:sourceProperty` 및 `xdm:destinationProperty` 속성 [!DNL Experience Data Model] (XDM) 설명자, 모두 `properties` 키는 다음과 같아야 합니다. **제외됨** json 포인터 문자열에서. 다음을 참조하십시오. [!DNL Schema Registry] 에 대한 API 개발자 안내서 하위 안내서 [설명자](../xdm/api/descriptors.md) 추가 정보.

## JSON 패치 {#json-patch}

다음에 대한 많은 PATCH 작업이 있습니다. [!DNL Platform] 요청 페이로드에 대해 JSON 패치 개체를 허용하는 API입니다. JSON 패치는 표준화된 형식입니다([RFC 6902](https://tools.ietf.org/html/rfc6902))를 참조하십시오. 요청 본문에 전체 문서를 전송할 필요 없이 JSON에 대한 부분 업데이트를 정의할 수 있습니다.

### 예제 JSON 패치 오브젝트

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: 패치 작업 유형입니다. JSON 패치는 여러 가지 작업 유형을 지원하지만 의 일부 PATCH 작업만 지원합니다. [!DNL Platform] API는 모든 작업 유형과 호환됩니다. 사용 가능한 작업 유형은 다음과 같습니다.
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: 를 사용하여 식별하여 업데이트할 JSON 구조의 부분입니다. [JSON 포인터](#json-pointer) 표기법.

에 표시된 작업 유형에 따라 `op`, JSON 패치 객체에는 추가 속성이 필요할 수 있습니다. 다양한 JSON 패치 작업 및 필요한 구문에 대한 자세한 내용은 다음을 참조하십시오. [JSON 패치 설명서](https://datatracker.ietf.org/doc/html/rfc6902).

## JSON 스키마 {#json-schema}

JSON 스키마는 JSON 데이터의 구조를 설명하고 유효성을 검사하는 데 사용되는 형식입니다. [경험 데이터 모델(XDM)](../xdm/home.md) 는 JSON 스키마 기능을 활용하여 수집된 고객 경험 데이터의 구조 및 형식에 제한을 적용합니다. JSON 스키마에 대한 자세한 내용은 [공식 문서](https://json-schema.org/).

## 다음 단계

이 문서에서는 JSON 기반 리소스 관리와 관련된 기술 및 구문 을 소개합니다. [!DNL Experience Platform]. 다음을 참조하십시오. [시작 안내서](api-guide.md) 모범 사례를 포함하여 Platform API 작업에 대한 자세한 내용을 알아보십시오. FAQ에 대한 답변은 다음을 참조하십시오. [플랫폼 문제 해결 안내서](troubleshooting.md).
