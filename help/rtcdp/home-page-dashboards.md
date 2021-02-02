---
keywords: 지표 개요;rcdp 지표 개요
title: 실시간 고객 데이터 플랫폼 홈 페이지 및 대시보드
seo-title: 실시간 고객 데이터 플랫폼 홈 페이지 및 대시보드
description: 대시보드, 홈페이지 및 Adobe Experience Platform의 최초 사용자 경험
seo-description: 대시보드, 홈페이지 및 Adobe Experience Platform의 최초 사용자 경험
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 4%

---


# [!DNL Real-time Customer Data Platform] 지표 개요

측정 지표 대시보드가 포함된 실시간 고객 데이터 플랫폼(실시간 CDP) 홈 페이지는 실시간 CDP에 로그인할 때 나타납니다.

홈 페이지는 지표 카드가 표시되는 위치 중 하나입니다. 실시간 CDP는 경험 전반에 측정 카드를 제공합니다. 이러한 지표는 시스템의 데이터, 프로필 및 세그먼트 대상에 대해 알려줍니다.

![image](assets/home.png)

실시간 CDP에 로그인할 때 시스템에 데이터가 없으면 홈 페이지의 대시보드가 나타나지 않습니다. 이 경우 홈 페이지에서 처음 사용자 경험을 위한 학습 자료를 제공합니다. 즉, 데이터가 수집되면, 즉 <!--sources-->데이터 세트, 프로필, 세그먼트 및 대상이 만들어지고 데이터가 시스템에 유입되므로 대시보드는 자동으로 업데이트되어 해당 데이터<!-- in metric cards-->에 대한 정보를 표시합니다.

## 홈 페이지 대시보드 보기

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

대시보드는<!-- two areas.-->으로 분할됩니다.

* **** 리더보드는 대시보드 맨 위에 있습니다. 리드 보드는 시스템에 있는 데이터 세트, 프로필, 세그먼트 및 대상의 수를 보여줍니다.

   ![이미지](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **최근** 는 시스템에 추가된 최근 데이터 세트, 소스, 세그먼트 및 대상을 5개 나열합니다.

   ![이미지](assets/recent.png)

실시간 고객 데이터 플랫폼의 다른 부분에서는 프로파일 및 세그먼트 등의 추가 지표를 사용할 수 있습니다.

### 데이터 세트

**[!UICONTROL 데이터 집합]** 카운터는 시스템의 데이터 집합 수와 [!DNL Platform]의 데이터 양을 표시합니다. 이 카운터는 데이터 세트를 만들 때 업데이트됩니다.

데이터 집합에 대한 자세한 내용은 [데이터 집합 개요](../catalog/datasets/overview.md)를 참조하십시오.

### 프로필

**[!UICONTROL Profiles]** 개수는 [!DNL Real-time Customer Profile]에 프로필이 있는 총 사용자 수를 보여줍니다. 프로필 조각은 포함되지 않습니다. 전체 주소 지정 가능한 대상입니다.

이 개수는 통합 프로필의 병합 정책 구성에 설정된 기본 [병합 정책](profile/merge-policies.md)을 사용합니다.

프로파일 수는 24시간마다 한 번씩 업데이트됩니다.

프로파일에 대한 자세한 내용은 실시간 CDP](profile/profile-overview.md)에서 고객의 통합 보기를 참조하십시오.[

### 세그먼트

**[!UICONTROL 세그먼트]** 는 조직에 대해 만들어진 총 세그먼트 수를 보여줍니다. 이 숫자는 새 세그먼트를 만들 때 업데이트됩니다.

세그먼트에 대한 자세한 내용은 [세그멘테이션 서비스 개요](segmentation/segmentation-overview.md)를 참조하십시오.

### 대상

**[!UICONTROL 대상]** 은 조직에 대해 만든 총 대상 수를 보여줍니다. 이 번호는 새 대상이 생성될 때 업데이트됩니다.

대상에 대한 자세한 내용은 [대상 개요](destinations/overview.md)를 참조하십시오.

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### 최근 데이터 세트

**[!UICONTROL 최근 데이터 집합]** 카드는 조직 내에서 가장 최근 데이터 집합 5개를 표시합니다. 이 목록은 새 데이터 세트를 만들 때 업데이트됩니다.

해당 항목에 대한 세부 사항을 볼 데이터 집합을 선택하거나 데이터 집합 목록을 보려면 **[!UICONTROL 모두 보기]**&#x200B;를 선택합니다. 여기에서 자세한 내용을 보려면 특정 소스를 선택할 수 있습니다.

데이터 집합에 대한 자세한 내용은 [데이터 집합 개요](../catalog/datasets/overview.md)를 참조하십시오.

### 최근 소스

**[!UICONTROL 최근 소스]** 지표 카드는 조직 내에서 가장 최근 소스 5개를 보여줍니다. 이 목록은 새 소스를 만들 때 업데이트됩니다.

해당 항목에 대한 세부 사항을 보려면 소스를 선택하고 소스 목록을 보려면 **[!UICONTROL 모두 보기]**. 여기에서 자세한 내용을 보려면 특정 소스를 선택할 수 있습니다.

소스에 대한 자세한 내용은 [소스 개요](sources/sources-overview.md)를 참조하십시오.

### 최근 세그먼트

**[!UICONTROL 최근 세그먼트]** 지표 카드는 조직 내에서 만들어진 가장 최근 세그먼트 5개를 보여줍니다. 이 목록은 새 세그먼트를 만들 때 업데이트됩니다.

해당 항목에 대한 세부 사항을 보려면 세그먼트를 선택하고, 추가 세그먼트에 대한 정보를 보려면 **[!UICONTROL 모두 보기]**.

세그먼트에 대한 자세한 내용은 [세그멘테이션 서비스 개요](segmentation/segmentation-overview.md)를 참조하십시오.

### 최근 대상

**[!UICONTROL 최근 대상]** 지표 카드는 조직 내에서 가장 최근 5개의 대상을 보여줍니다. 이 목록은 새 대상을 만들 때 업데이트됩니다.

해당 항목에 대한 세부 정보를 보려면 대상을 선택하고, 추가 대상에 대한 정보를 보려면 **[!UICONTROL 모두 보기]**&#x200B;를 선택합니다.

대상에 대한 자세한 내용은 [대상 개요](destinations/overview.md)를 참조하십시오.
