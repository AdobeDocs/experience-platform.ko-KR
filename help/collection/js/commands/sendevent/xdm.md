---
title: xdm
description: XDM 스키마 정렬 개체를 통해 Adobe으로 데이터를 전송하는 방법에 대해 알아봅니다.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# `xdm`

`xdm` 개체에 Adobe으로 전송된 데이터 페이로드가 포함되어 있습니다. 이 오브젝트 내에 설정된 필드는 데이터 세트의 스키마에 정의된 요소에 직접 매핑됩니다.

Adobe Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다.

`xdm` 명령을 실행할 때 `sendEvent` 개체를 설정합니다. 이 개체의 계층 구조가 구성된 데이터 세트의 스키마와 일치하는지 확인하십시오. 동일한 `xdm` 명령에 [`data`](data.md) 개체와 `sendEvent` 개체를 모두 포함할 수 있습니다.

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

## 웹 SDK 태그 확장을 사용하여 `xdm` 개체 사용

`xdm` 개체는 Web SDK 태그 확장을 사용할 때 [변수 데이터 요소](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) 또는 [XDM 개체 데이터 요소](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) 중 하나로 사용할 수 있습니다. Adobe 대부분의 경우 변수 데이터 요소를 사용하는 것이 좋습니다.
