---
title: Adobe Experience Platform Web SDK Extension의 데이터 요소 유형
description: Adobe Experience Platform Web SDK 태그 확장에서 제공하는 다양한 데이터 요소 유형에 대해 알아봅니다.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 4caab19e1f58fc5cec5a3c56c43e47786d49c3dc
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 19%

---

# 데이터 요소 유형

[Adobe Experience Platform Web SDK 태그 확장](web-sdk-extension-configuration.md)에서 [작업 유형](action-types.md)을 설정한 후 데이터 요소 유형을 구성합니다.

이 페이지에서는 사용 가능한 데이터 요소 유형을 설명합니다.


## 이벤트 병합 ID

이 데이터 요소는 사용 시 이벤트 병합 ID를 제공합니다. 이 데이터 요소에는 구성이 필요하지 않습니다. 제공된 데이터 요소는 방문자가 페이지를 떠나거나 &quot;이벤트 병합 ID 재설정&quot; 작업 유형이 사용될 때까지 동일하게 유지됩니다.

## ID 맵

ID 맵을 사용하면 웹 페이지 방문자의 ID를 설정할 수 있습니다. ID 맵은 _phone_ 또는 _이메일_&#x200B;과 같은 네임스페이스로 구성되며, 각 네임스페이스에는 하나 이상의 식별자가 포함됩니다. 예를 들어 웹 사이트의 개인이 두 개의 전화 번호를 제공한 경우 휴대폰 네임스페이스에 두 개의 식별자가 있어야 합니다.

[!UICONTROL ID 맵] 데이터 요소에서 각 식별자에 대해 다음 정보 조각을 제공합니다.

* **[!UICONTROL ID]**: 방문자를 식별하는 값입니다. 예를 들어 식별자가 _phone_ 네임스페이스에 속하는 경우 [!UICONTROL ID]은 _555-555-5555_&#x200B;일 수 있습니다. 이 값은 일반적으로 JavaScript 변수 또는 페이지의 다른 일부 데이터에서 파생되므로 페이지 데이터를 참조하는 데이터 요소를 만든 다음 [!UICONTROL ID 맵] 데이터 요소 내의 [!UICONTROL ID] 필드에서 데이터 요소를 참조하는 것이 가장 좋습니다. 페이지에서 실행할 때 ID 값이 채워진 문자열이 아닌 경우 ID 맵에서 식별자가 자동으로 제거됩니다.
* **[!UICONTROL 인증됨 상태]**: 방문자의 인증 여부를 나타내는 선택 사항입니다.
* **[!UICONTROL 기본]**: 식별자를 개인의 기본 식별자로 사용해야 하는지 여부를 나타내는 선택 사항입니다. 기본 식별자로 표시된 식별자가 없으면 ECID가 기본 식별자로 사용됩니다.

ID 맵을 작성할 때 ECID를 제공해서는 안 됩니다. SDK를 사용할 때 ECID는 서버에서 자동으로 생성되어 ID 맵에 포함됩니다.

ID 맵 데이터 요소는 종종 [[!UICONTROL XDM 개체] 데이터 요소 유형](#xdm-object) 및 [[!UICONTROL 동의 설정 작업 유형](action-types.md#set-consent)과 함께 사용됩니다.]

[Adobe Experience Platform Identity 서비스](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ko)에 대해 자세히 알아보십시오.

![](./assets/identity-map-data-element.png)

## XDM 개체 {#xdm-object}

XDM 형식을 사용하여 데이터를 Adobe Experience Platform Web SDK에 보냅니다. XDM 개체 데이터 요소를 사용하면 데이터 형식을 보다 손쉽게 지정할 수 있습니다. 이 데이터 요소를 처음 열면 올바른 Adobe Experience Platform 샌드박스 및 스키마를 선택합니다. 스키마를 선택하면 쉽게 작성할 수 있는 스키마 구조가 표시됩니다.

![](./assets/XDM-object.png)

`web.webPageDetails.URL` 과 같은 스키마의 특정 필드를 열면 일부 항목이 자동으로 수집됩니다. 여러 항목이 자동으로 수집되지만 필요한 경우 덮어쓸 수 있습니다. 모든 값은 수동으로 채우거나 다른 데이터 요소를 사용할 수 있습니다.

>[!NOTE]
>
>수집하고자 하는 사항만 작성하십시오. 이 채워지지 않은 모든 것은 데이터가 솔루션으로 전송될 때 생략됩니다.
