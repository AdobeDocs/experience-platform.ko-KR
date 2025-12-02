---
title: 데이터
description: 데이터 개체를 통해 XDM이 아닌 데이터를 Adobe으로 전송하는 방법에 대해 알아봅니다.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# `data`

`data` 개체를 사용하면 XDM 스키마와 일치하지 않는 Adobe에 페이로드를 보낼 수 있습니다. 이 메서드는 Adobe Analytics, Adobe Target 또는 Adobe Audience Manager으로 직접 데이터를 전송하는 경우와 같이, XDM이 아닌 시나리오에서 유용합니다. 데이터가 데이터 스트림에 도달하면 [데이터 준비 매핑](/help/data-prep/ui/mapping.md)을 사용하여 `data` 개체의 각 필드에 XDM 필드를 할당할 수 있습니다. Adobe에서 `data` 개체 내의 필드를 검색하도록 제품을 이미 구성한 경우 해당 데이터를 있는 그대로 데이터 스트림으로 보낼 수 있습니다.

>[!IMPORTANT]
>
>이 개체 내의 데이터에는 다음 작업 중 하나 이상이 있어야 합니다.
>
>* `data` 개체의 지정된 속성에서 데이터를 검색하도록 데이터 스트림의 서비스를 구성해야 합니다.
>* 지정된 속성은 데이터 준비를 사용하여 XDM 필드에 매핑되어야 합니다.
>
>지정된 속성이 XDM 필드에 매핑되지 않았거나 구성된 서비스에서 사용되지 않으면 해당 데이터가 영구적으로 손실됩니다.

`data` 개체를 `sendEvent` 명령의 매개 변수 내에서 JSON 개체의 일부로 설정하십시오. 데이터스트림에 매핑할 데이터의 경우 원하는 대로 이 개체를 구성할 수 있습니다. 특정 서비스에서 사용하는 데이터의 경우 개체 계층 구조가 서비스가 기대하는 것과 일치하는지 확인하십시오. 동일한 `data` 명령에 [`xdm`](xdm.md) 개체와 `sendEvent` 개체를 모두 포함할 수 있습니다.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Adobe Analytics에서 `data` 개체 사용 {#analytics}

Adobe Analytics에서 `data` 개체를 사용하여 XDM 스키마 없이 보고서 세트로 데이터를 보낼 수 있습니다. 변수는 AppMeasurement 변수와 동일한 구문을 사용하도록 구성되어 있으므로 웹 SDK에 대한 업그레이드 프로세스를 단순화합니다. 자세한 내용은 Adobe Analytics 구현 안내서의 [Adobe Analytics에 대한 데이터 개체 변수 매핑](https://experienceleague.adobe.com/ko/docs/analytics/implementation/aep-edge/data-var-mapping)을 참조하십시오.

## 웹 SDK 태그 확장을 사용하여 `data` 개체 사용

`data` 개체는 Web SDK 태그 확장을 사용할 때 [변수 데이터 요소](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)(으)로 사용할 수 있습니다.
