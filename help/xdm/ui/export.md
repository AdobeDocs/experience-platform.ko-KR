---
solution: Experience Platform
title: UI에서 XDM 스키마 내보내기
description: Adobe Experience Platform 사용자 인터페이스에서 기존 스키마를 다른 샌드박스 또는 IMS 조직에 내보내는 방법을 알아봅니다.
topic: user guide
type: Tutorial
translation-type: tm+mt
source-git-commit: 8d6916890a94300dc68d018d56579df9616c177c
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# UI에서 XDM 스키마 내보내기

스키마 라이브러리 내의 모든 리소스는 IMS 조직 내의 특정 샌드박스에 포함됩니다. 샌드박스와 IMS 조직 간에 경험 데이터 모델(XDM) 리소스를 공유하는 경우도 있습니다.

이 요구 사항을 해결하기 위해 Adobe Experience Platform UI의 [!UICONTROL 스키마] 작업 영역을 사용하면 스키마 라이브러리 내의 모든 스키마에 대한 내보내기 페이로드를 생성할 수 있습니다. 그러면 이 페이로드를 스키마 레지스트리 API 호출에서 사용하여 스키마(및 모든 종속 리소스)를 대상 샌드박스 및 IMS 조직에 가져올 수 있습니다.

>[!NOTE]
>
>또한 스키마 레지스트리 API를 사용하여 클래스, 믹싱 및 데이터 유형을 비롯한 스키마 외에도 다른 리소스를 내보낼 수 있습니다. 자세한 내용은 [내보내기/가져오기 끝점](../api/export-import.md)의 안내서를 참조하십시오.

## 전제 조건

플랫폼 UI에서 XDM 리소스를 내보낼 수 있지만 스키마 레지스트리 API를 사용하여 해당 리소스를 다른 샌드박스 또는 IMS Organize로 가져와 워크플로우를 완료해야 합니다. 이 안내서를 참조하기 전에 스키마 레지스트리 API](../api/getting-started.md)에 대한 안내서를 참조하십시오.[

## 내보내기 페이로드 생성

플랫폼 UI의 왼쪽 탐색 영역에서 **[!UICONTROL 스키마]**&#x200B;를 선택합니다. [!UICONTROL 스키마] 작업 공간 내에서 내보낼 스키마를 찾아 [!DNL Schema Editor]에서 엽니다.

>[!TIP]
>
>원하는 XDM 리소스를 찾는 방법에 대한 자세한 내용은 [XDM 리소스](./explore.md)에 대한 가이드를 참조하십시오.

스키마를 연 후에는 캔버스 오른쪽 상단에 있는 **[!UICONTROL JSON 복사]** 아이콘(![아이콘 복사](../images/ui/export/icon.png))을 선택합니다.

![](../images/ui/export/copy-json.png)

스키마 구조에 따라 생성된 JSON 페이로드를 클립보드에 복사합니다. 위에 표시된 &quot;[!DNL Loyalty Members]&quot; 스키마에 대해 다음 JSON이 생성됩니다.

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

페이로드는 내보낼 사용자 지정 XDM 리소스를 나타내는 개체로서 각 배열 항목이 포함된 배열 형태를 취합니다. 위의 예에서 &quot;[!DNL Loyalty details]&quot; 사용자 정의 믹스인과 &quot;[!DNL Loyalty Members]&quot; 스키마가 포함됩니다. 스키마에서 사용되는 모든 핵심 리소스는 모든 샌드박스 및 IMS 조직에서 사용할 수 있으므로 내보내기에 포함되지 않습니다.

조직의 테넌트 ID의 각 인스턴스는 페이로드에서 `<XDM_TENANTID_PLACEHOLDER>`으로 나타납니다. 다음 단계에서 스키마를 가져오는 위치에 따라 이러한 자리 표시자는 해당 테넌트 ID 값으로 자동 대체됩니다.

## API를 사용하여 리소스 가져오기

스키마에 대한 내보내기 JSON을 복사했으면 스키마 레지스트리 API의 `/import` 끝점에 대한 POST 요청에 대한 페이로드로 사용할 수 있습니다. 원하는 IMS 조직 및 샌드박스로 스키마를 보내는 호출을 구성하는 방법에 대한 자세한 내용은 API](../api/export-import.md#import)의 [XDM 리소스 가져오기 섹션을 참조하십시오.

## 다음 단계

이 안내서를 따라 XDM 스키마를 다른 IMS 조직 또는 샌드박스로 성공적으로 내보냈습니다. [!UICONTROL 스키마] UI의 기능에 대한 자세한 내용은 [[!UICONTROL 스키마] UI 개요](./overview.md)를 참조하십시오.