---
keywords: Experience Platform;사용자 인터페이스;UI;대시보드;대시보드;프로필;세그먼트;대상;라이센스 사용
title: UI에서 플랫폼 대시보드 수정
description: '이 안내서에서는 조직의 Adobe Experience Platform 데이터가 대시보드 내에 표시되는 방식을 사용자 지정하기 위한 단계별 지침을 제공합니다. '
topic-legacy: guide
exl-id: 75e4aea7-b521-434d-9cd5-32a00d00550d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# (베타) 대시보드 {#modify-dashboards} 수정

>[!IMPORTANT]
>
>대시보드 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform 유저 인터페이스(UI) 내에서 여러 대시보드를 사용하여 조직의 데이터를 보고 상호 작용할 수 있습니다. 대시보드에 표시되는 기본 위젯과 지표는 개별 사용자 수준에서 조정하여 기본 데이터를 표시하고 같은 조직의 사용자 간에 위젯을 만들고 공유할 수 있습니다.

이 안내서에서는 플랫폼 UI의 [!UICONTROL Profiles], [!UICONTROL Segments] 및 [!UICONTROL Destinations] 대시보드에 대시보드 데이터가 표시되는 방식을 사용자 지정하기 위한 단계별 지침을 제공합니다.

>[!NOTE]
>
>라이센스 사용 대시보드에 표시되는 위젯을 사용자 지정할 수 없습니다. 이 고유 대시보드에 대한 자세한 내용은 [라이센스 사용 대시보드 설명서](guides/license-usage.md)를 참조하십시오.

## 시작하기

모든 대시보드(예: [!UICONTROL Profiles] 대시보드)에서 기존 위젯의 크기를 조정하고 순서를 변경하려면 **[!UICONTROL Modify dashboard]**&#x200B;을 선택할 수 있습니다.

![](images/customization/modify-dashboard.png)

## 위젯 순서 변경

대시보드를 수정하려면 위젯 제목을 선택하고 위젯을 원하는 순서로 드래그하여 놓아 위젯의 순서를 변경할 수 있습니다. 이 예에서, **[!UICONTROL Profiles by identity namespace]** 위젯이 맨 위 행으로 이동되고 이제 두 번째 행에 [!UICONTROL Profile Count] 위젯이 표시됩니다.

![](images/customization/move-widget.png)

## 위젯 크기 조정

위젯(`⌟`)의 오른쪽 하단에 있는 각도 기호를 선택하고 위젯을 원하는 크기로 드래그하여 위젯의 크기를 조정할 수도 있습니다. 이 예에서 **[!UICONTROL Profiles by identity namespace]** 위젯의 크기가 전체 상단 행을 채우도록 조정되어 다른 위젯을 두 번째 행으로 자동으로 이동합니다. 위젯이 커짐에 따라 수평 축이 조정되어 보다 세부 증분을 제공하는 방법을 확인합니다.

>[!NOTE]
>
>위젯의 크기가 조정되면 주변 위젯의 위치가 동적으로 변경됩니다. 이로 인해 일부 위젯이 추가 행으로 이동될 수 있으므로 모든 위젯을 보려면 스크롤해야 합니다.

![](images/customization/resize-widget.png)

## 대시보드 업데이트 저장

위젯 이동 및 크기 조정을 완료한 후 **[!UICONTROL Save]**&#x200B;을 선택하여 변경 내용을 저장하고 기본 대시보드 보기로 돌아갑니다. 변경 사항을 유지하지 않으려면 **[!UICONTROL Cancel]**&#x200B;을 선택하여 대시보드를 재설정하고 기본 대시보드 보기로 돌아갑니다.

![](images/customization/save-changes.png)

## 위젯 라이브러리

위젯의 크기 조정 및 순서 변경 외에도 [!UICONTROL Profiles] 및 [!UICONTROL Segments] 대시보드에서 **[!UICONTROL Widget library]**&#x200B;를 사용하여 위젯을 표시하거나 만들 위젯을 더 선택할 수 있습니다.

[!UICONTROL Widget library]에 액세스하여 작업하는 방법에 대한 단계별 지침은 [widget library guide](widget-library.md)를 참조하십시오.

## 다음 단계

이 문서를 읽은 후 대시보드 수정 기능을 사용하여 위젯의 순서를 변경하고 크기를 조정하여 대시보드 보기를 사용자 지정하는 방법을 알아보았습니다. 대시보드에 위젯을 만들고 추가하는 방법에 대해 알아보려면 [위젯 라이브러리 안내서](widget-library.md)를 참조하십시오.
