---
solution: Experience Platform
title: UI에서 XDM 스키마 내보내기
description: Adobe Experience Platform 사용자 인터페이스에서 기존 스키마를 다른 샌드박스 또는 조직으로 내보내는 방법을 알아봅니다.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 11%

---

# UI에서 XDM 스키마 내보내기 {#export-xdm-schemas-in-the-UI}

>[!CONTEXTUALHELP]
>id="platform_xdm_copyjsonstructure"
>title="JSON 구조 복사"
>abstract="JSON 구조를 클립보드에 복사하여 선택한 스키마에 대한 내보내기 페이로드를 생성합니다. 이 기능을 사용하여 스키마 라이브러리에 있는 모든 스키마의 세부 정보를 내보내십시오. 그런 다음 내보낸 JSON을 사용하여 스키마 및 관련 리소스를 다른 샌드박스 또는 조직으로 가져올 수 있습니다. 이를 통해 서로 다른 환경 간에 스키마를 간단하고 효율적인 방식으로 공유하고 재사용할 수 있습니다."

스키마 라이브러리 내의 모든 리소스는 조직 내의 특정 샌드박스에 포함됩니다. 경우에 따라 샌드박스와 조직 간에 XDM(Experience Data Model) 리소스를 공유할 수 있습니다.

이러한 요구를 해결하기 위해 Adobe Experience Platform UI의 [!UICONTROL 스키마] 작업 영역에서 스키마 라이브러리의 모든 스키마에 대한 내보내기 페이로드를 생성할 수 있습니다. 그런 다음 스키마(및 모든 종속 리소스)를 대상 샌드박스 및 조직으로 가져오기 위해 스키마 레지스트리 API 호출에 이 페이로드를 사용할 수 있습니다.

>[!NOTE]
>
>스키마 레지스트리 API를 사용하여 스키마 외에 클래스, 스키마 필드 그룹, 데이터 유형 등의 다른 리소스를 내보낼 수도 있습니다. 자세한 내용은 [끝점 내보내기 가이드](../api/export.md)를 참조하십시오.

## 전제 조건

Experience Platform UI를 사용하여 XDM 리소스를 내보낼 수 있지만 워크플로우를 완료하려면 스키마 레지스트리 API를 사용하여 해당 리소스를 다른 샌드박스 또는 조직으로 가져와야 합니다. 이 안내서를 따르기 전에 필수 인증 헤더에 대한 중요한 정보가 필요하면 [스키마 레지스트리 API 시작하기](../api/getting-started.md)에 대한 안내서를 참조하십시오.

## 내보내기 페이로드 생성 {#generate-export-payload}

내보내기 페이로드는 [!UICONTROL 찾아보기] 탭의 세부 정보 패널에서 Experience Platform UI를 생성하거나 스키마 편집기의 스키마 캔버스에서 직접 생성할 수 있습니다.

내보내기 페이로드를 생성하려면 왼쪽 탐색에서 **[!UICONTROL 스키마]**&#x200B;를 선택하십시오. [!UICONTROL 스키마] 작업 영역 내에서 내보낼 스키마의 행을 선택하여 오른쪽 사이드바에 스키마 세부 정보를 표시합니다.

>[!TIP]
>
>찾고 있는 XDM 리소스를 찾는 방법에 대한 자세한 내용은 [XDM 리소스 탐색](./explore.md)에 대한 안내서를 참조하십시오.

그런 다음 사용 가능한 옵션에서 **[!UICONTROL JSON 복사]** 아이콘(![복사 아이콘](/help/images/icons/copy.png))을 선택합니다.

![스키마 행과 [!UICONTROL JSON으로 복사]가 강조 표시된 스키마 작업 영역.](../images/ui/export/copy-json.png)

이렇게 하면 스키마 구조를 기반으로 생성된 클립보드에 JSON 페이로드가 복사됩니다. 위에 표시된 &quot;[!DNL Loyalty Members]&quot; 스키마의 경우 다음 JSON이 생성됩니다.

+++예제 JSON 페이로드를 확장하려면 선택

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty details",
    "type": "object",
    "description": "",
    "definitions": {
      "customFields": {
        "type": "object",
        "properties": {
          "_<XDM_TENANTID_PLACEHOLDER>": {
            "type": "object",
            "properties": {
              "loyalty": {
                "title": "Loyalty",
                "description": "",
                "type": "object",
                "isRequired": false,
                "required": [
                  
                ],
                "properties": {
                  "loyaltyId": {
                    "title": "Loyalty ID",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "string"
                  },
                  "memberSince": {
                    "title": "Member Since",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "format": "date",
                    "meta:xdmType": "date"
                  },
                  "points": {
                    "title": "Points",
                    "description": "",
                    "type": "integer",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "int"
                  },
                  "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
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
            "meta:xdmType": "object"
          }
        },
        "meta:xdmType": "object"
      }
    },
    "allOf": [
      {
        "$ref": "#/definitions/customFields",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
      
    ],
    "meta:xdmType": "object",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production"
  },
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/schemas/1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.schemas.1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Describes customers who are members of a loyalty program.",
    "allOf": [
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/mixins/profile-consents",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
      "https://ns.adobe.com/xdm/context/profile-person-details",
      "https://ns.adobe.com/xdm/context/profile-personal-details",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile",
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/mixins/profile-consents"
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production",
    "meta:immutableTags": [
      
    ]
  }
]
```

+++

스키마 편집기의 오른쪽 상단에서 [!UICONTROL 자세히]를 선택하여 페이로드를 복사할 수도 있습니다. 드롭다운 메뉴는 [!UICONTROL JSON 구조 복사] 및 [!UICONTROL 스키마 삭제]의 두 가지 옵션을 제공합니다.

>[!NOTE]
>
>프로필에 대해 활성화되거나 연결된 데이터 세트가 있는 스키마는 삭제할 수 없습니다.

![스키마 편집기 [!UICONTROL 자세히] 및 [!UICONTROL JSON에 복사]가 강조 표시되었습니다.](../images/ui/export/schema-editor-copy-json.png)

페이로드는 배열의 형태를 취하며, 각 배열 항목은 내보낼 사용자 정의 XDM 리소스를 나타내는 개체입니다. 위의 예에는 &quot;[!DNL Loyalty details]&quot; 사용자 지정 필드 그룹과 &quot;[!DNL Loyalty Members]&quot; 스키마가 포함되어 있습니다. 스키마에서 사용하는 모든 핵심 리소스는 모든 샌드박스 및 조직에서 사용할 수 있으므로 내보내기에 포함되지 않습니다.

조직의 테넌트 ID의 각 인스턴스는 페이로드에 `<XDM_TENANTID_PLACEHOLDER>`(으)로 표시됩니다. 이러한 자리 표시자는 다음 단계에서 스키마를 가져오는 위치에 따라 적절한 테넌트 ID 값으로 자동으로 대체됩니다.

## API를 사용하여 리소스 가져오기 {#import-resource-with-api}

스키마에 대한 내보내기 JSON을 복사한 후에는 스키마 레지스트리 API의 `/rpc/import` 끝점에 대한 POST 요청의 페이로드로 사용할 수 있습니다. 원하는 조직 및 샌드박스로 스키마를 보내는 호출을 구성하는 방법에 대한 자세한 내용은 [끝점 가져오기 안내서](../api/import.md)를 참조하십시오.

## 다음 단계

이 안내서를 따라 XDM 스키마를 다른 조직 또는 샌드박스로 내보냈습니다. [!UICONTROL 스키마] UI의 기능에 대한 자세한 내용은 [[!UICONTROL 스키마] UI 개요](./overview.md)를 참조하십시오.
