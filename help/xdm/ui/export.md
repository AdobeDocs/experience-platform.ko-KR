---
solution: Experience Platform
title: UI에서 XDM 스키마 내보내기
description: Adobe Experience Platform 사용자 인터페이스에서 기존 스키마를 다른 샌드박스 또는 조직으로 내보내는 방법을 알아봅니다.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: bed627b945c5392858bcc2dce18e9bbabe8bcdb6
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# UI에서 XDM 스키마 내보내기

스키마 라이브러리 내의 모든 리소스는 조직 내의 특정 샌드박스에 포함됩니다. 경우에 따라 샌드박스와 조직 간에 XDM(Experience Data Model) 리소스를 공유할 수 있습니다.

이러한 요구 사항을 해결하기 위해 [!UICONTROL 스키마] Adobe Experience Platform UI의 작업 영역에서는 스키마 라이브러리의 모든 스키마에 대한 내보내기 페이로드를 생성할 수 있습니다. 그런 다음 스키마(및 모든 종속 리소스)를 대상 샌드박스 및 조직으로 가져오기 위해 스키마 레지스트리 API 호출에 이 페이로드를 사용할 수 있습니다.

>[!NOTE]
>
>스키마 레지스트리 API를 사용하여 스키마 외에 클래스, 스키마 필드 그룹, 데이터 유형 등의 다른 리소스를 내보낼 수도 있습니다. 다음을 참조하십시오. [끝점 내보내기 안내서](../api/export.md) 추가 정보.

## 사전 요구 사항

Platform UI를 사용하여 XDM 리소스를 내보낼 수 있지만 워크플로우를 완료하려면 스키마 레지스트리 API를 사용하여 해당 리소스를 다른 샌드박스 또는 조직으로 가져와야 합니다. 다음 안내서를 참조하십시오. [스키마 레지스트리 API 시작하기](../api/getting-started.md) 이 안내서를 따르기 전에 필수 인증 헤더에 대한 중요 정보를 확인하십시오.

## 내보내기 페이로드 생성 {#generate-export-payload}

Platform UI에서 를 선택합니다. **[!UICONTROL 스키마]** 왼쪽 탐색. 다음 범위 내 [!UICONTROL 스키마] 작업 영역에서 내보낼 스키마의 행을 선택하여 오른쪽 사이드바에 스키마 세부 정보를 표시합니다.

>[!TIP]
>
>다음 안내서를 참조하십시오 [xdm 리소스 살펴보기](./explore.md) 찾고 있는 XDM 리소스를 찾는 방법에 대한 자세한 내용.

그런 다음 **[!UICONTROL JSON 복사]** 아이콘(![복사 아이콘](../images/ui/export/icon.png)사용 가능한 옵션에서 ).

![스키마 행 및 [!UICONTROL JSON으로 복사] 강조 표시됨.](../images/ui/export/copy-json.png)

이렇게 하면 스키마 구조를 기반으로 생성된 클립보드에 JSON 페이로드가 복사됩니다. 의 경우[!DNL Loyalty Members]&quot; 위에 표시된 스키마에서는 다음 JSON이 생성됩니다.

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

페이로드는 배열의 형태를 취하며, 각 배열 항목은 내보낼 사용자 정의 XDM 리소스를 나타내는 개체입니다. 위의 예에서[!DNL Loyalty details]&quot;사용자 정의 필드 그룹 및&quot;[!DNL Loyalty Members]&quot;스키마가 포함됩니다. 스키마에서 사용하는 모든 핵심 리소스는 모든 샌드박스 및 조직에서 사용할 수 있으므로 내보내기에 포함되지 않습니다.

조직의 테넌트 ID의 각 인스턴스는 로 표시됩니다. `<XDM_TENANTID_PLACEHOLDER>` 페이로드에서. 이러한 자리 표시자는 다음 단계에서 스키마를 가져오는 위치에 따라 적절한 테넌트 ID 값으로 자동으로 대체됩니다.

## API를 사용하여 리소스 가져오기

스키마에 대한 JSON 내보내기를 복사했으면 POST 요청에 대한 페이로드로 사용할 수 있습니다. `/rpc/import` 스키마 레지스트리 API의 끝점입니다. 다음을 참조하십시오. [끝점 가져오기 안내서](../api/import.md) 원하는 조직 및 샌드박스로 스키마를 전송하는 호출을 구성하는 방법에 대한 세부 정보.

## 다음 단계

이 안내서를 따라 XDM 스키마를 다른 조직 또는 샌드박스로 내보냈습니다. 의 기능에 대한 자세한 내용 [!UICONTROL 스키마] UI에서 다음을 참조하십시오 [[!UICONTROL 스키마] UI 개요](./overview.md).
