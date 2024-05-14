---
title: 데이터
description: 데이터 개체를 통해 XDM이 아닌 데이터를 Adobe으로 보내는 방법을 알아봅니다.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# `data`

다음 `data` 개체를 사용하면 XDM 스키마와 일치하지 않는 Adobe에 페이로드를 보낼 수 있습니다. 이 메서드는 Adobe Analytics, Adobe Target 또는 Adobe Audience Manager으로 직접 데이터를 전송하는 경우와 같이, XDM이 아닌 시나리오에서 유용합니다. 데이터가 데이터 스트림에 도달하면 [데이터 준비 매핑](/help/data-prep/ui/mapping.md) 의 각 필드에 XDM 필드를 할당하려면 `data` 개체.

>[!IMPORTANT]
>
>이 개체 내의 데이터에는 다음 작업 중 하나 이상이 있어야 합니다.
>
>* 데이터스트림의 특정 속성에서 데이터를 검색하도록 데이터스트림의 서비스를 구성해야 합니다. `data` 개체.
>* 지정된 속성은 데이터 준비를 사용하여 XDM 필드에 매핑되어야 합니다.
>
>지정된 속성이 XDM 필드에 매핑되지 않았거나 구성된 서비스에서 사용되지 않으면 해당 데이터가 영구적으로 손실됩니다.

## 사용 `data` Web SDK 태그 확장을 통한 개체 {#tag-extension}

에 데이터 요소를 제공합니다. **[!UICONTROL 데이터]** 태그 규칙 작업 내의 필드

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 작업]를 클릭하고 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL 이벤트 보내기]**.
1. 에서 원하는 개체가 포함된 데이터 요소를 제공합니다. **[!UICONTROL 데이터]** 필드.
1. 클릭 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

## 사용 `data` 웹 SDK JavaScript 라이브러리를 통한 개체 {#library}

설정 `data` 의 매개 변수 내에서 JSON 개체의 일부로 개체 `sendEvent` 명령입니다. 데이터스트림에 매핑할 데이터의 경우 원하는 대로 이 개체를 구성할 수 있습니다. 특정 서비스에서 사용하는 데이터의 경우 개체 계층 구조가 서비스가 기대하는 것과 일치하는지 확인하십시오. 다음 두 가지를 모두 포함할 수 있습니다. `data` 오브젝트 및 [`xdm`](xdm.md) 같은 오브젝트 `sendEvent` 명령입니다.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## 사용 `data` Adobe Analytics이 있는 오브젝트 {#analytics}

다음을 사용할 수 있습니다. `data` XDM 스키마 없이 보고서 세트로 데이터를 전송할 Adobe Analytics 포함 개체입니다. 변수는 와 동일한 구문을 사용하도록 구성됩니다. [!DNL AppMeasurement] 변수를 사용하여 Web SDK에 대한 업그레이드 프로세스를 간소화합니다. 다음을 참조하십시오 [Adobe Analytics에 대한 데이터 개체 변수 매핑](https://experienceleague.adobe.com/ko/docs/analytics/implementation/aep-edge/data-var-mapping) 자세한 내용은 Adobe Analytics 구현 안내서 를 참조하십시오.
