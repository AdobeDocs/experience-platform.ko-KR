---
keywords: Experience Platform;사용자 인터페이스;사용자 인터페이스;사용자 정의;라이센스 사용 대시보드;대시보드;라이센스 사용;자격 부여;소비
title: 라이센스 사용 대시보드
description: Adobe Experience Platform은 조직의 라이선스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 084aaa315f694d696abee7f078be3a121111f6cc
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---


# (베타) [!UICONTROL 라이센스 사용] 대시보드 {#license-usage-dashboard}

>[!IMPORTANT]
>
>이 문서에 설명된 대시보드 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform 사용자 인터페이스(UI)는 일일 스냅샷 중에 캡처된 조직의 라이센스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 라이선스 사용 대시보드에 액세스하고 작업하는 방법에 대해 설명하고 대시보드에 표시되는 시각화에 대한 자세한 정보를 제공합니다.

플랫폼 UI에 대한 일반적인 개요는 [Experience Platform UI 안내서](../../landing/ui-guide.md)를 참조하십시오.

## 라이선스 사용 대시보드 데이터

라이센스 사용 대시보드에는 Experience Platform에 대한 조직의 라이센스 관련 데이터 스냅샷이 표시됩니다. 대시보드의 데이터는 스냅샷을 촬영한 특정 시점에 나타나는 것과 동일하게 표시됩니다. 즉, 스냅숏은 데이터에 대한 근사 또는 샘플이 아니며 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅숏을 만든 이후 데이터에 대한 변경 사항이나 업데이트는 다음 스냅샷을 촬영하기 전까지 대시보드에 반영되지 않습니다.

## 라이선스 사용 대시보드 살펴보기

플랫폼 UI 내의 라이센스 사용 대시보드로 이동하려면 왼쪽 레일에서 **[!UICONTROL 라이선스 사용량]**&#x200B;을 선택합니다. 대시보드가 표시되는 **[!UICONTROL 개요]** 탭으로 열립니다.

![](../images/license-usage/dashboard-overview.png)

### 샌드박스 선택

대시보드에서 볼 샌드박스를 선택하려면 [!UICONTROL 프로덕션] 또는 [!UICONTROL 개발]을 선택합니다. 선택한 샌드박스는 샌드박스 이름 옆에 있는 라디오 버튼으로 표시됩니다.

>[!NOTE]
>
>샌드박스에 대한 소비 보고는 동일한 유형의 모든 샌드박스에 대해 누적됩니다. 즉, [!UICONTROL 프로덕션] 또는 [!UICONTROL 개발]을 선택하면 모든 프로덕션 또는 개발 샌드박스에 대해 각각 보고합니다.

![](../images/license-usage/select-sandbox.png)

### 날짜 범위 선택

샌드박스를 선택한 후 날짜 범위 드롭다운을 사용하여 대시보드에 표시할 기간을 선택할 수 있습니다. 다음 3가지 옵션을 사용할 수 있습니다.[!UICONTROL 최근 30일], [!UICONTROL 최근 90일] 및 [!UICONTROL 지난 12개월] 최근 30일은 기본적으로 선택됩니다.

![](../images/license-usage/select-date-range.png)

### 위젯 및 지표

라이선스 사용량 대시보드는 위젯으로 구성되어 있으며, 조직의 라이선스 사용과 관련된 중요 정보를 제공하는 읽기 전용 지표가 표시됩니다. 이러한 위젯에 대한 자세한 내용은 이 안내서의 사용 가능한 위젯 섹션을 참조하십시오.

## 사용 가능한 위젯 {#available-widgets}

Experience Platform은 현재 라이선스 사용을 시각화하는 데 사용할 수 있는 하나의 위젯을 제공하므로 더 많은 위젯이 곧 릴리스됩니다.

### [!UICONTROL 대응 가능 고객] {#addressable-audiences}

결정(비공개) 그래프 알고리즘을 사용하여 현재 모든 데이터 세트에서 프로필 조각을 결합하기 위해 시스템 생성 병합 정책을 적용한 후 **[!UICONTROL 대응 가능 대상]** 위젯은 프로필 데이터 저장소 내의 병합된 프로필의 총 수를 표시합니다.

조각 및 병합된 프로파일에 대한 자세한 내용은 [프로필 개요](../../profile/home.md)의 *프로필 조각과 병합된 프로필* 섹션을 읽으십시오.

>[!NOTE]
>
>이 지표를 계산하는 데 사용되는 병합 정책은 Experience Platform에 의해 생성되며 편집할 수 없거나 다른 병합 정책을 선택할 수 없습니다. 이 시스템에서 생성한 병합 정책은 [!DNL Profile] 대시보드에서 [!UICONTROL 대상 크기]을 계산하는 데 사용되는 기본 병합 정책과 동일하지 않으므로 [!UICONTROL 라이선스 사용량] 및 [!DNL Profile] 대시보드의 대상 수가 정확히 동일하지는 않습니다.

![](../images/license-usage/addressable-audiences.png)

## 다음 단계

이 문서를 따르면 이제 라이선스 사용 대시보드를 찾아 볼 샌드박스를 선택할 수 있습니다. 사용 가능한 위젯에 표시되는 지표도 이해해야 합니다. Experience Platform UI에 대한 자세한 내용은 [플랫폼 UI 안내서](../../landing/ui-guide.md)를 참조하십시오.