---
title: xdm
description: XDM 스키마 정렬 오브젝트를 통해 Adobe에 데이터를 전송하는 방법에 대해 알아봅니다.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# `xdm`

`xdm` 개체에 Adobe에 전송된 데이터 페이로드가 포함되어 있습니다. 이 오브젝트 내에 설정된 필드는 데이터 세트의 스키마에 정의된 요소에 직접 매핑됩니다.

Adobe Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다.

이 개체의 최대 제한은 32KB입니다.

## Web SDK 확장을 사용하여 XDM 개체 구성

**[!UICONTROL XDM]** 개체를 태그 규칙의 동작 내에서 설정합니다. [XDM 개체](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)는 다른 데이터 요소를 해당 XDM 필드에 매핑하는 직관적인 인터페이스를 제공합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 규칙]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL 작업]에서 기존 작업을 선택하거나 작업을 만드십시오.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 [!UICONTROL 작업 유형]을(를) **[!UICONTROL 이벤트 보내기]**(으)로 설정합니다.
1. **[!UICONTROL XDM]** 필드에 원하는 개체가 포함된 데이터 요소를 제공하십시오.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭한 다음 게시 워크플로우를 실행하십시오.

## 웹 SDK JavaScript 라이브러리를 사용하여 XDM 개체 구성

`sendEvent` 명령을 실행할 때 `xdm` 개체를 설정합니다. 이 개체의 계층 구조가 구성된 데이터 세트의 스키마와 일치하는지 확인하십시오. 동일한 `sendEvent` 명령에 `xdm` 개체와 [`data`](data.md) 개체를 모두 포함할 수 있습니다.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

다음 예제에서는 [Commerce 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/event/commerce-details.md)을 사용합니다.

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large field hat",
      },
      {
        "SKU":"HT104",
        "name":"Small field hat",
      }
    ]
  }
});
```
