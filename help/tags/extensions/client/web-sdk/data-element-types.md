---
title: Adobe Experience Platform 웹 SDK 확장의 데이터 요소 유형
description: Adobe Experience Platform 웹 SDK 태그 확장에서 제공하는 다양한 데이터 요소 유형에 대해 알아봅니다.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: fbca8a47c500e89d82cf636e8cb639f2bb59c2e6
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---


# 데이터 요소 유형

[Adobe Experience Platform Web SDK 태그 확장](web-sdk-extension-configuration.md)에서 [작업 유형](action-types.md)을 설정한 후에는 데이터 요소 유형을 구성해야 합니다. 이 페이지에서는 사용 가능한 데이터 요소 유형에 대해 설명합니다.

## ID 맵 {#identity-map}

ID 맵을 사용하면 웹 페이지 방문자의 ID를 설정할 수 있습니다. ID 맵은 `CRMID`, `Phone` 또는 `Email`과(와) 같은 네임스페이스로 구성되며 각 네임스페이스에는 하나 이상의 식별자가 포함되어 있습니다. 예를 들어 웹 사이트의 개인이 두 개의 전화 번호를 제공한 경우 전화 네임스페이스에는 두 개의 식별자가 포함되어야 합니다.

[!UICONTROL ID 맵] 데이터 요소에서 각 식별자에 대해 다음 정보를 제공합니다.

* **[!UICONTROL ID]**: 방문자를 식별하는 값입니다. 예를 들어 식별자가 _phone_ 네임스페이스에 속하는 경우 [!UICONTROL ID]은(는) _555-555-5555_&#x200B;일 수 있습니다. 이 값은 일반적으로 JavaScript 변수 또는 페이지의 다른 데이터에서 파생되므로 페이지 데이터를 참조하는 데이터 요소를 만든 다음 [!UICONTROL ID 맵] 데이터 요소 내의 [!UICONTROL ID] 필드에 있는 데이터 요소를 참조하는 것이 좋습니다. 페이지에서 를 실행할 때 ID 값이 채워진 문자열이 아닌 경우 ID 맵에서 식별자가 자동으로 제거됩니다.
* **[!UICONTROL 인증됨 상태]**: 방문자가 인증되었는지 여부를 나타내는 선택입니다.
* **[!UICONTROL 기본]**: 식별자를 개인의 기본 식별자로 사용할지 여부를 나타내는 선택입니다. 기본 식별자로 표시된 식별자가 없으면 ECID가 기본 식별자로 사용됩니다.

![데이터 요소 편집 화면을 표시하는 UI 이미지입니다.](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe은 사용자를 나타내는 ID(예: `Luma CRM Id`)를 기본 ID로 보낼 것을 권장합니다.
>
>ID 맵에 사용자 식별자(예: `Luma CRM Id`)가 포함된 경우 사용자 식별자가 기본 식별자가 됩니다. 그렇지 않으면 `ECID`이(가) 기본 ID가 됩니다.

ID 맵을 작성할 때 [!DNL ECID]을(를) 제공해서는 안 됩니다. SDK를 사용하는 경우 [!DNL ECID]이(가) 서버에 자동으로 생성되고 ID 맵에 포함됩니다.

ID 맵 데이터 요소는 종종 [[!UICONTROL XDM 개체] 데이터 요소 유형](#xdm-object) 및 [[!UICONTROL 동의 설정] 작업 유형](action-types.md#set-consent)과 함께 사용됩니다.

[Adobe Experience Platform ID 서비스](../../../../identity-service/home.md)에 대해 자세히 알아보세요.

## XDM 개체 {#xdm-object}

XDM 개체 데이터 요소를 사용하면 데이터를 XDM으로 더 쉽게 포맷할 수 있습니다. 이 데이터 요소를 처음 열면 올바른 Adobe Experience Platform 샌드박스 및 스키마를 선택합니다. 스키마를 선택하면 스키마 구조가 표시되어 쉽게 작성할 수 있습니다.

![XDM 개체 구조를 보여 주는 UI 이미지입니다.](assets/XDM-object.png)

`web.webPageDetails.URL`과(와) 같은 스키마의 특정 필드를 열면 일부 항목이 자동으로 수집됩니다. 여러 항목이 자동으로 수집되지만 필요한 경우 덮어쓸 수 있습니다. 모든 값은 수동으로 채우거나 다른 데이터 요소를 사용할 수 있습니다.

>[!NOTE]
>
>수집하려는 정보만 입력하십시오. 작성되지 않은 내용은 데이터를 솔루션으로 보낼 때 생략됩니다.

## 변수 {#variable}

**[!UICONTROL 변수]** 데이터 요소를 사용하여 페이로드 개체를 만들 수 있습니다. [!UICONTROL XDM] 및 [!UICONTROL Data] 개체가 모두 지원됩니다.

* [!UICONTROL XDM]을(를) 선택한 경우 원하는 [!UICONTROL 샌드박스] 및 [!UICONTROL 스키마]를 선택하십시오.
* [!UICONTROL 데이터]를 선택하면 원하는 솔루션을 선택합니다. 사용 가능한 솔루션에는 [!UICONTROL Adobe Analytics] 및 [!UICONTROL Adobe Target]이(가) 있습니다.

![데이터 요소 옵션을 표시하는 태그 UI의 이미지](assets/variable-data-element.png)

이 데이터 요소를 만든 후 [변수 업데이트](./action-types.md#update-variable) 작업을 사용하여 수정할 수 있습니다. 준비가 되면 [이벤트 보내기](./action-types.md#send-event) 작업에 이 데이터 요소를 포함하여 데이터스트림으로 데이터를 보낼 수 있습니다.

## 미디어: 체감 품질 {#quality-experience}

**[!UICONTROL 체감 품질]** 데이터 요소는 스트리밍 미디어 이벤트를 Adobe Experience Platform으로 보낼 때 유용합니다. 미디어 세션을 만들 때 이 요소를 추가할 수 있으며 다음 미디어 이벤트에는 업데이트된 경험 품질 데이터가 포함됩니다.

![경험 데이터 요소 만들기 화면을 표시하는 UI 이미지입니다.](assets/qoe-data-element.png)

## 다음 단계 {#next-steps}

[ECID에 액세스](accessing-the-ecid.md)와 같은 특정 사용 사례에 대해 알아봅니다.
