---
title: 데이터 스트림 구성 설정
description: 웹 SDK 태그 확장을 사용하여에 데이터를 전송하도록 데이터 스트림을 구성합니다.
exl-id: 2d2504c6-b3f9-4e7b-aff4-a8d8d6c4e3dd
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---

# 데이터 스트림 구성 설정 {#datastreams}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_datastreams"
>title="데이터스트림"
>abstract="필수 여부. 데이터를 전송할 Edge Network 내의 데이터 스트림을 설정합니다."

이 구성 섹션에서는 데이터를 보낼 [데이터스트림](/help/datastreams/overview.md)을(를) 결정할 수 있습니다. **Edge Network으로 전송되는 모든 데이터에 데이터 스트림 ID가 필요합니다.**

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. **[!UICONTROL Datastreams]** 섹션까지 아래로 스크롤합니다.

![태그 UI에서 웹 SDK 태그 확장의 데이터 스트림 설정을 보여 주는 이미지](../assets/web-sdk-ext-datastreams.png)

데이터 스트림을 선택할 때 각 [환경](/help/tags/ui/publishing/environments.md)([!UICONTROL Development], [!UICONTROL Staging] 및 [!UICONTROL Production])에 대해 그렇게 할 수 있습니다. 이러한 필드는 개발, 스테이징 및 프로덕션 환경 간에 전송된 데이터를 분리하려는 경우 유용합니다. 이렇게 하면 각 환경에 올바른 태그 로더를 설치하는 한 잘못된 데이터 스트림에 데이터를 보내는 데 걱정할 필요가 없는 편리한 워크플로우를 사용할 수 있습니다.

다음 방법 중 하나를 사용하여 데이터 스트림 ID를 채울 수 있습니다.

* **[!UICONTROL Choose from list]**: 각 환경에는 두 개의 드롭다운 메뉴가 포함되어 있으므로 선택한 환경에 대한 샌드박스 및 데이터스트림을 선택할 수 있습니다. 각 드롭다운 메뉴의 값은 각 [샌드박스](/help/datastreams/overview.md) 내에서 구성된 [데이터스트림](/help/sandboxes/ui/overview.md)에 따라 다릅니다.

* **[!UICONTROL Enter values]**: 드롭다운 메뉴를 사용하여 원하는 데이터 스트림을 선택하는 대신 원하는 데이터 스트림 ID를 직접 수동으로 지정할 수 있습니다. 각 환경에서는 데이터 스트림 ID를 직접 입력하거나 [데이터 요소](/help/tags/ui/managing-resources/data-elements.md)를 사용하여 이 필드를 채울 수 있습니다.
