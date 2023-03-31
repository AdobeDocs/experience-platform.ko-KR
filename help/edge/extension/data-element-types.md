---
title: Adobe Experience Platform Web SDK Extension의 데이터 요소 유형
description: Adobe Experience Platform Web SDK 태그 확장에서 제공하는 다양한 데이터 요소 유형에 대해 알아봅니다.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 8%

---


# 데이터 요소 유형

을 설정한 후 [작업 유형](action-types.md) 에서 [Adobe Experience Platform 웹 SDK 태그 확장](web-sdk-extension-configuration.md), 데이터 요소 유형을 구성해야 합니다. 이 페이지에서는 사용 가능한 데이터 요소 유형을 설명합니다.

## 이벤트 병합 ID {#event-merge-id}

이 데이터 요소는 사용 시 이벤트 병합 ID를 제공합니다. 이 데이터 요소에는 구성이 필요하지 않습니다. 제공된 데이터 요소는 방문자가 페이지를 나갈 때까지 또는 **[!UICONTROL 이벤트 병합 ID 재설정]** 작업 유형이 사용됩니다.

## ID 맵 {#identity-map}

ID 맵을 사용하면 웹 페이지 방문자의 ID를 설정할 수 있습니다. ID 맵은 다음과 같은 네임스페이스로 구성됩니다 _phone_ 또는 _이메일_, 하나 이상의 식별자를 포함하는 각 네임스페이스에 대해 예를 들어 웹 사이트의 개인이 두 개의 전화 번호를 제공한 경우 휴대폰 네임스페이스에 두 개의 식별자가 있어야 합니다.

에서 [!UICONTROL ID 맵] 데이터 요소에서는 각 식별자에 대해 다음 정보를 제공합니다.

* **[!UICONTROL ID]**: 방문자를 식별하는 값입니다. 예를 들어, 식별자가 _phone_ namespace, [!UICONTROL ID] 아마 _555-555-5555_. 이 값은 일반적으로 JavaScript 변수 또는 페이지의 다른 일부 데이터에서 파생되므로 페이지 데이터를 참조하는 데이터 요소를 만든 다음, 페이지의 데이터 요소를 참조하는 것이 가장 좋습니다 [!UICONTROL ID] 내 필드 [!UICONTROL ID 맵] 데이터 요소를 생성하지 않습니다. 페이지에서 실행할 때 ID 값이 채워진 문자열이 아닌 경우 ID 맵에서 식별자가 자동으로 제거됩니다.
* **[!UICONTROL 인증됨 상태]**: 방문자의 인증 여부를 나타내는 선택 사항입니다.
* **[!UICONTROL 기본]**: 식별자를 개인의 기본 식별자로 사용해야 하는지 여부를 나타내는 선택 사항입니다. 기본 식별자로 표시된 식별자가 없으면 ECID가 기본 식별자로 사용됩니다.

![데이터 요소 편집 화면을 보여주는 UI 이미지.](./assets/identity-map-data-element.png)

를 제공해서는 안 됩니다 [!DNL ECID] id 맵을 작성할 때. SDK를 사용할 때 [!DNL ECID] 는 서버에서 자동으로 생성되며 id 맵에 포함됩니다.

ID 맵 데이터 요소는 종종 와 함께 사용됩니다 [[!UICONTROL XDM 개체] 데이터 요소 유형](#xdm-object) 그리고 [[!UICONTROL 동의 설정] 작업 유형](action-types.md#set-consent).

자세한 내용 [Adobe Experience Platform Identity 서비스](../../identity-service/home.md).

## XDM 개체 {#xdm-object}

XDM 개체 데이터 요소를 사용하면 데이터를 XDM에 쉽게 서식을 지정할 수 있습니다. 이 데이터 요소를 처음 열면 올바른 Adobe Experience Platform 샌드박스 및 스키마를 선택합니다. 스키마를 선택하면 쉽게 작성할 수 있는 스키마 구조가 표시됩니다.

![XDM 개체 구조를 보여주는 UI 이미지입니다.](assets/XDM-object.png)

다음과 같은 스키마의 특정 필드를 열 때 `web.webPageDetails.URL`, 일부 항목은 자동으로 수집됩니다. 여러 항목이 자동으로 수집되지만 필요한 경우 덮어쓸 수 있습니다. 모든 값은 수동으로 채우거나 다른 데이터 요소를 사용할 수 있습니다.

>[!NOTE]
>
>수집하고자 하는 사항만 작성하십시오. 이 채워지지 않은 모든 것은 데이터가 솔루션으로 전송될 때 생략됩니다.

## (베타) 변수 {#variable}

>[!IMPORTANT]
>
>현재 베타 기능이며 변경될 수 있습니다. 이후 버전에는 변경 사항이 포함될 수 있습니다.

XDM 개체를 만드는 또 다른 방법은 **[!UICONTROL 변수]** 데이터 요소를 생성하지 않습니다. XDM 개체 데이터 요소는 참조할 때(예: 내부) 만들어집니다 `sendEvent` 명령, **[!UICONTROL 변수]** 를 통해 데이터 요소를 업데이트할 수 있습니다. [!UICONTROL 변수 업데이트] 작업. 데이터 요소를 사용하려면 올바른 Adobe Experience Platform 샌드박스 및 스키마를 선택합니다.

![데이터 요소 만들기 화면을 보여주는 UI 이미지.](assets/variable-data-element.png)

이 데이터 요소를 만들면 [변수 업데이트](./action-types.md#update-variable) 데이터 요소를 수정하는 작업입니다. 그런 다음 이벤트 전송 내에서 XDM 옵션에 변수 데이터 요소를 사용합니다.

## 다음 단계 {#next-steps}

다음과 같은 특정 사용 사례에 대해 배웁니다. [ECID 액세스](accessing-the-ecid.md).
