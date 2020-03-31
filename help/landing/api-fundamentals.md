---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform API 기본 사항
topic: getting started
translation-type: tm+mt
source-git-commit: c94f065a5d56ac495dd2d541531aaec94c187612

---


# Adobe Experience Platform API 기본 사항

Adobe Experience Platform API 파섹 이 문서에서는 이러한 기술에 대한 간략한 개요와 자세한 내용은 외부 문서에 대한 링크를 제공합니다.

## JSON 포인터 {#json-pointer}

JSON Pointer는 JSON 문서 내의 특정[값을 식별하기 위한 표준화된 문자열 구문(RFC](https://tools.ietf.org/html/rfc6901)6901)입니다. JSON 포인터는 `/` 문자로 구분된 토큰 문자열로서, 개체 키 또는 배열 인덱스를 지정하며, 토큰은 문자열 또는 숫자일 수 있습니다. JSON 포인터 문자열은 이 문서의 후반부에 설명된 대로 플랫폼 API에 대한 많은 패치 작업에서 사용됩니다. JSON 포인터에 대한 자세한 내용은 JSON 포인터 [개요 설명서를](https://rapidjson.org/md_doc_pointer.html)참조하십시오.

### JSON 스키마 개체 예

```json
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "description": "The current loyalty program level to which the individual member belongs.",
                            "type": "string",
                            "enum": [
                                "platinum",
                                "gold",
                                "silver",
                                "bronze"
                            ],
                            "meta:enum": {
                                "platinum": "Platinum",
                                "gold": "Gold",
                                "silver": "Silver",
                                "bronze": "Bronze"
                            },
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    }
}
```

### 스키마 개체를 기반으로 하는 JSON 포인터 예

| JSON 포인터 | 해결 방법 |
|--- | ---|
| `"/title"` | &quot;충성도 회원 세부 정보&quot; |
| `"/definitions/loyalty"` | (개체의 내용을 `loyalty` 반환합니다.) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!Note]
>XDM(Experience Data Model) 설명자의 `xdm:sourceProperty` 및 `xdm:destinationProperty` 특성을 처리할 때 `properties` 모든 키를 JSON 포인터 문자열에서 **제외해야** 합니다. 자세한 내용은 스키마 레지스트리 API 개발자 가이드 [설명자에](../xdm/api/descriptors.md) 대한 하위 안내서를 참조하십시오.

## JSON 패치

요청 페이로드에 대해 JSON 패치 개체를 허용하는 플랫폼 API에 대한 많은 PATCH 작업이 있습니다. JSON 패치는 JSON 문서의 변경 사항을[설명하는 표준 형식(RFC](https://tools.ietf.org/html/rfc6902)6902)입니다. 전체 문서를 요청 본문에 보내지 않고도 JSON에 대한 부분 업데이트를 정의할 수 있습니다.

### JSON 패치 개체 예

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:패치 작업의 유형입니다. JSON 패치는 여러 가지 작업 유형을 지원하지만 플랫폼 API의 일부 PATCH 작업은 모든 작업 유형과 호환되지 않습니다. 사용 가능한 작업 유형은 다음과 같습니다.
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:JSON 포인터 표기법을 사용하여 식별되는 업데이트 JSON 구조의 [일부](#json-pointer) .

에 지정된 작업 유형에 따라 JSON 패치 `op`개체에 추가 속성이 필요할 수 있습니다. 다양한 JSON 패치 작업 및 필요한 구문에 대한 자세한 내용은 JSON 패치 [설명서를](http://jsonpatch.com/)참조하십시오.

## JSON 스키마

JSON 스키마는 JSON 데이터의 구조를 설명하고 확인하는 데 사용되는 포맷입니다. [XDM(Experience Data Model)](../xdm/home.md) 은 JSON 스키마 기능을 활용하여 인제스트된 고객 경험 데이터의 구조와 형식에 대한 제약 사항을 적용합니다. JSON 스키마에 대한 자세한 내용은 [공식 설명서를](https://json-schema.org/)참조하십시오.

## 다음 단계

이 문서에서는 Experience Platform용 JSON 기반 리소스 관리와 관련된 기술 및 구문 일부를 소개합니다. 우수 사례, FAQ 등 플랫폼 API 작업에 대한 자세한 내용은 플랫폼 문제 해결 [안내서를](troubleshooting.md)참조하십시오.