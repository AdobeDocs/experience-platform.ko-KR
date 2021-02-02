---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: Adobe Experience Platform API 기본 사항
topic: getting started
description: 이 문서에서는 Experience Platform API와 관련된 일부 기본 기술 및 구문에 대한 간단한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---


# Adobe Experience Platform API 기본 사항

Adobe Experience Platform API는 JSON 기반 [!DNL Platform] 리소스를 효과적으로 관리하기 위해 이해해야 하는 몇 가지 기본 기술 및 구문을 사용합니다. 이 문서에서는 이러한 기술에 대한 간단한 개요와 자세한 내용을 살펴보려면 외부 문서에 대한 링크를 제공합니다.

## JSON 포인터 {#json-pointer}

JSON 포인터는 JSON 문서 내의 특정 값을 식별하기 위한 표준 문자열 구문([RFC 6901](https://tools.ietf.org/html/rfc6901))입니다. JSON 포인터는 개체 키 또는 배열 인덱스를 지정하는 `/` 문자로 구분된 토큰의 문자열이며, 토큰은 문자열 또는 숫자일 수 있습니다. JSON 포인터 문자열은 이 문서의 후반부에 있는 설명에 따라 [!DNL Platform] API에 대한 많은 PATCH 작업에 사용됩니다. JSON 포인터에 대한 자세한 내용은 [JSON 포인터 개요 설명서](https://rapidjson.org/md_doc_pointer.html)를 참조하십시오.

### JSON 스키마 개체 예

다음 JSON은 JSON 포인터 문자열을 사용하여 필드를 참조할 수 있는 간소화된 XDM 스키마를 나타냅니다. 사용자 정의 믹싱(예: `loyaltyLevel`)을 사용하여 추가된 모든 필드는 `_{TENANT_ID}` 개체 아래에 이름이 지정되지만, 핵심 믹싱(예: `fullName`)을 사용하여 추가된 필드는 지정되지 않습니다.

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

### 스키마 개체를 기반으로 하는 JSON 포인터 예

| JSON 포인터 | 해결 대상 |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | 코어 믹싱에서 제공하는 `fullName` 필드에 대한 참조를 반환합니다. |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | 사용자 정의 믹싱에서 제공하는 `loyaltyLevel` 필드에 대한 참조를 반환합니다. |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>`xdm:sourceProperty` 및 [!DNL Experience Data Model](XDM) 설명자의 `xdm:destinationProperty` 특성을 처리할 때 `properties` 키는 JSON 포인터 문자열에서 **excluded**&#x200B;이어야 합니다. 자세한 내용은 [설명자](../xdm/api/descriptors.md)의 [!DNL Schema Registry] API 개발자 안내서 하위 안내서를 참조하십시오.

## JSON 패치 {#json-patch}

요청 페이로드를 위해 JSON 패치 개체를 허용하는 [!DNL Platform] API에 대해 많은 PATCH 작업이 있습니다. JSON 패치는 JSON 문서의 변경 내용을 설명하는 표준 형식([RFC 6902](https://tools.ietf.org/html/rfc6902))입니다. 이렇게 하면 전체 문서를 요청 본문에 보내지 않고도 JSON에 대한 부분 업데이트를 정의할 수 있습니다.

### JSON 패치 개체 예

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:패치 작업의 유형입니다. JSON 패치는 여러 가지 작업 유형을 지원하지만 [!DNL Platform] API의 모든 PATCH 작업은 모든 작업 유형과 호환되지 않습니다. 사용 가능한 작업 유형은 다음과 같습니다.
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:업데이트할 JSON 구조의 일부를  [JSON ](#json-pointer) 표기법을 사용하여 식별합니다.

`op`에 지정된 작업 유형에 따라 JSON 패치 객체에는 추가 속성이 필요할 수 있습니다. 다양한 JSON 패치 작업 및 필요한 구문에 대한 자세한 내용은 [JSON 패치 문서](http://jsonpatch.com/)를 참조하십시오.

## JSON 스키마

JSON 스키마는 JSON 데이터의 구조를 설명하고 확인하는 데 사용되는 형식입니다. [XDM(Experience Data Model)은 JSON 스키마 기능을 ](../xdm/home.md) 활용하여 인제스트된 고객 경험 데이터의 구조와 형식에 대한 제약 사항을 적용합니다. JSON 스키마에 대한 자세한 내용은 [공식 설명서](https://json-schema.org/)를 참조하십시오.

## 다음 단계

이 문서에서는 [!DNL Experience Platform]에 대한 JSON 기반 리소스 관리와 관련된 기술 및 구문을 소개합니다. 모범 사례 및 FAQ 답변 등 [!DNL Platform] API 작업에 대한 자세한 내용은 [플랫폼 문제 해결 안내서](troubleshooting.md)를 참조하십시오.