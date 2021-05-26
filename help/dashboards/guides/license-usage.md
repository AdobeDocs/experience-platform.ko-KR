---
keywords: Experience Platform;사용자 인터페이스;UI;사용자 지정;라이선스 사용 대시보드;대시보드;라이선스 사용;권한;소비
title: 라이선스 사용 대시보드
description: Adobe Experience Platform에서는 조직의 라이선스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 47c4113d45b0101a761fa7d703013609e8729dbb
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 0%

---

# 라이선스 사용 대시보드 {#license-usage-dashboard}

Adobe Experience Platform UI(사용자 인터페이스)는 일별 스냅샷 중에 캡처된 대로 조직의 라이선스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 라이선스 사용 대시보드에 액세스하고 작업하는 방법을 간략하게 설명하고 대시보드에 표시되는 시각화에 대한 자세한 정보를 제공합니다.

플랫폼 UI에 대한 일반적인 개요는 [Experience Platform UI 안내서](../../landing/ui-guide.md)를 참조하십시오.

## 라이선스 사용 대시보드 데이터

라이센스 사용량 대시보드는 Experience Platform에 대한 조직의 라이선스 관련 데이터의 스냅샷을 표시합니다. 대시보드의 데이터는 스냅샷을 가져온 특정 시점의 데이터와 동일하게 표시됩니다. 즉, 스냅샷은 데이터의 근사 또는 샘플이 아니며, 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅샷을 생성하기 때문에 데이터가 변경된 사항이나 업데이트는 다음 스냅샷을 가져올 때까지 대시보드에 반영되지 않습니다.

## 라이선스 사용 대시보드 탐색

플랫폼 UI 내의 라이선스 사용 대시보드로 이동하려면 왼쪽 레일에서 **[!UICONTROL 라이선스 사용량]** 을 선택합니다. 대시보드가 표시되는 **[!UICONTROL 개요]** 탭이 열립니다.

>[!NOTE]
>
>라이센스 사용 대시보드는 기본적으로 활성화되지 않습니다. 대시보드를 보려면 사용자에게 &quot;라이선스 사용 대시보드 보기&quot; 권한이 부여되어야 합니다. 라이센스 사용 대시보드를 보기 위한 액세스 권한을 부여하는 단계는 [대시보드 권한 안내서](../permissions.md)를 참조하십시오.

![](../images/license-usage/dashboard-overview.png)

### 샌드박스 선택

대시보드에서 볼 샌드박스를 선택하려면 [!UICONTROL 프로덕션] 또는 [!UICONTROL 개발]을 선택합니다. 선택한 샌드박스는 샌드박스 이름 옆에 있는 라디오 단추로 표시됩니다.

샌드박스에 대한 소비 보고는 동일한 유형의 모든 샌드박스에 대해 누적됩니다. 즉, [!UICONTROL 프로덕션] 또는 [!UICONTROL 개발]을 선택하면 각각 모든 프로덕션 또는 개발 샌드박스에 대한 사용량 보고서가 제공됩니다.

![](../images/license-usage/select-sandbox.png)

>[!WARNING]
>
>라이선스 사용량 대시보드를 볼 수 있는 권한은 샌드박스 수준에서 지정해야 합니다. 즉, 대시보드를 볼 수 있는 권한을 각 개별 샌드박스에 추가해야 합니다. 이 제한은 향후 릴리스에서 해결될 예정입니다. 그 동안에는 다음 해결 방법을 사용할 수 있습니다.
>
>1. Adobe Admin Console에서 제품 프로필을 만듭니다.
>2. 샌드박스 카테고리의 권한 아래에서 라이선스 사용 대시보드에서 보려는 모든 샌드박스를 추가합니다.
>3. 사용자 대시보드 권한 카테고리에서 &quot;라이선스 사용 대시보드 보기&quot; 권한을 추가합니다.


### 날짜 범위 선택

샌드박스를 선택한 후 날짜 범위 드롭다운을 사용하여 대시보드에 표시할 기간을 선택할 수 있습니다. 최근 30일의 기본값을 포함하여 여러 옵션을 사용할 수 있습니다.

![](../images/license-usage/select-date-range.png)

**[!UICONTROL 사용자 지정 날짜]**&#x200B;를 선택하여 표시되는 기간을 선택할 수도 있습니다.

![](../images/license-usage/select-custom-date.png)

## 위젯

라이선스 사용량 대시보드는 위젯으로 구성되며, 조직의 라이선스 사용과 관련된 중요한 정보를 제공하는 읽기 전용 지표를 표시합니다. 표시되는 지표는 조직의 특정 라이센스에 따라 다릅니다( [사용 가능한 지표](#available-metrics) 섹션 참조).

각 위젯은 조직의 실제 수치를 조직의 라이센스에서 사용할 수 있는 총수와 비교하는 선 그래프를 보여주며 총 사용량의 백분율을 제공합니다.

![](../images/license-usage/widgets.png)

## 사용 가능한 지표

라이선스 사용량 대시보드 는 4개의 주요 지표에 대해 보고되며 후속 릴리스에서 추가할 지표가 더 있습니다. 사용 가능한 지표는 아래에 나와 있습니다.

>[!NOTE]
>
>사용 가능한 지표 중 세 개가 현재 베타 버전입니다.

* [!UICONTROL 대응 가능 대상]
* [!UICONTROL 평균 프로필 품질] (베타)
* [!UICONTROL 세그먼테이션 비율당 스캔한 데이터] (베타)
* [!UICONTROL 총 소비 스토리지] (베타)

>[!WARNING]
>
>[!UICONTROL 총 소비된 저장소] 지표의 알려진 제한 사항:배치 데이터를 삭제할 때 해당 배치는 데이터 복구 사용 사례를 지원하기 위해 7일 동안 소프트 삭제 상태로 배치됩니다. 7일 후 일괄 처리가 하드 삭제 상태로 이동됩니다. 총 소비된 스토리지에 대한 보고에서는 일괄 처리가 하드 삭제 상태가 될 때까지 트렌드 차트에 변경 사항이 반영되지 않습니다. 이 문제는 향후 릴리스에서 해결됩니다.

이러한 지표의 가용성과 이러한 각 지표의 구체적인 정의는 조직이 구입한 라이센스에 따라 다릅니다. 각 지표에 대한 자세한 정의는 해당 제품 설명 설명서를 참조하십시오.

| 라이선스 | 제품 설명 |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, 앱 서비스 및 Intelligent Services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT 고객 데이터 플랫폼:OD</li><li>RT 고객 데이터 플랫폼:POD - 10M</li><li>RT 고객 데이터 플랫폼:OD PRFL에서 50M까지</li></ul> | [실시간 고객 데이터 플랫폼](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD 활성화</li><li>AEP:OD 활성화 PRFL - 10M</li><li>AEP:OD 활성화 PRFL 최대 50M</li></ul> | [Adobe Experience Platform 활성화](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

>[!WARNING]
>
>라이선스 사용량 대시보드는 조직에 제공된 최신 라이센스에 대해서만 보고합니다. 조직에 대해 제공된 최신 라이센스가 위의 표에 표시되지 않으면 라이센스 사용 대시보드가 제대로 표시되지 않을 수 있습니다. 한 조직의 추가 라이센스와 여러 라이센스에 대한 지원은 향후 릴리스에 제공될 예정입니다.

## 다음 단계

이 문서를 읽은 후 라이선스 사용 대시보드를 찾아 볼 샌드박스를 선택할 수 있습니다. 또한 조직에서 구입한 라이센스에 따라 조직의 사용 가능한 지표에 대한 자세한 정보를 찾을 수 있습니다.

Experience Platform UI에서 사용할 수 있는 다른 기능에 대한 자세한 내용은 [플랫폼 UI 안내서](../../landing/ui-guide.md)를 참조하십시오.
