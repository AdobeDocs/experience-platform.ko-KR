---
keywords: metrics overview; rtcdp metrics overview
title: 실시간 고객 데이터 플랫폼 홈 페이지 및 대시보드
seo-title: 실시간 고객 데이터 플랫폼 홈 페이지 및 대시보드
description: 대시보드, 홈페이지 및 Adobe Experience Platform의 최초 사용자 경험
seo-description: 대시보드, 홈페이지 및 Adobe Experience Platform의 최초 사용자 경험
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 4%

---


# [!DNL Real-time Customer Data Platform] 지표 개요

측정 지표 대시보드가 포함된 실시간 고객 데이터 플랫폼(실시간 CDP) 홈 페이지는 실시간 CDP에 로그인할 때 나타납니다.

홈 페이지는 지표 카드가 표시되는 곳 중 하나입니다. 실시간 CDP는 고객 경험 전반에서 측정 카드를 제공합니다. 이러한 지표는 시스템의 데이터, 프로필 및 세그먼트 대상에 대해 알려줍니다.

![image](assets/home.png)

실시간 CDP에 로그인할 때 시스템에 데이터가 없으면 홈 페이지의 대시보드가 나타나지 않습니다. 이 경우 홈 페이지에서 처음 사용자 경험을 위한 학습 자료를 제공합니다. 데이터가 수집되면 즉, <!--sources-->데이터 세트, 프로필, 세그먼트 및 대상이 만들어지고 데이터가 시스템에 유입되므로 대시보드는 자동으로 업데이트되어 해당 데이터에 대한 정보를 표시합니다<!-- in metric cards-->.

## 홈 페이지 대시보드 보기

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

대시보드는 다음과 같이 구분됩니다<!-- two areas.-->.

* **리더보드는** 대시보드 맨 위에 있습니다. 리드 보드는 시스템의 데이터 집합, 프로필, 세그먼트 및 대상 수를 보여줍니다.

   ![image](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **최근 항목에는** 시스템에 추가된 최근 데이터 세트, 소스, 세그먼트 및 대상 5개가 나열됩니다.

   ![image](assets/recent.png)

프로필 및 세그먼트 등의 추가 지표는 실시간 고객 데이터 플랫폼의 다른 부분에서 사용할 수 있습니다.

### 데이터 세트

데이터 **[!UICONTROL 집합]** 카운터는 시스템의 데이터 집합 수와 데이터의 양을 표시합니다 [!DNL Platform]. 이 카운터는 데이터 세트를 만들 때 업데이트됩니다.

데이터 세트에 대한 자세한 내용은 [데이터 집합 개요를 참조하십시오](../catalog/datasets/overview.md).

### 프로필

프로필 **** 수는 프로필에 있는 총 사람 수를 보여줍니다 [!DNL Real-time Customer Profile]. 프로필 조각은 포함되지 않습니다. 전체 주소 지정 가능 고객입니다.

이 계산에서는 통합 프로필의 병합 정책 구성에 설정된 대로 기본 [병합 정책을](profile/merge-policies.md) 사용합니다.

프로파일 수는 24시간마다 한 번씩 업데이트됩니다.

프로파일에 대한 자세한 내용은 실시간 [CDP에서 고객의 전체 상황을 참조하십시오](profile/profile-overview.md).

### 세그먼트

**[!UICONTROL 세그먼트는]** 조직에 대해 생성된 총 세그먼트 수를 보여줍니다. 이 숫자는 새 세그먼트가 생성될 때 업데이트됩니다.

세그먼트에 대한 자세한 내용은 세그멘테이션 [서비스 개요를 참조하십시오](segmentation/segmentation-overview.md).

### 대상

**[!UICONTROL 대상은]** 조직에 대해 만들어진 총 대상 수를 보여줍니다. 이 번호는 새 대상이 생성될 때 업데이트됩니다.

대상에 대한 자세한 내용은 대상 [개요를 참조하십시오](destinations/overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Click **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Click **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Click **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### 최근 데이터 집합

최근 데이터 **[!UICONTROL 집합]** 카드는 조직 내에서 생성된 가장 최근 데이터 집합 5개를 보여줍니다. 이 목록은 새 데이터 세트를 만들 때 업데이트됩니다.

데이터 세트를 클릭하여 해당 항목에 대한 세부 사항을 보거나 데이터 집합 목록을 **[!UICONTROL 보려면 모두]** 보기를 클릭합니다. 여기에서 자세한 내용을 보려면 특정 소스를 클릭하면 됩니다.

데이터 세트에 대한 자세한 내용은 [데이터 집합 개요를 참조하십시오](../catalog/datasets/overview.md).

### 최근 소스

최근 **[!UICONTROL 소스]** 지표 카드는 조직 내에서 만들어진 가장 최근 5개의 소스를 보여줍니다. 이 목록은 새 소스를 만들 때 업데이트됩니다.

소스를 클릭하여 해당 항목에 대한 세부 사항을 보거나 소스 목록을 **[!UICONTROL 보려면 모두]** 보기를 클릭합니다. 여기에서 자세한 내용을 보려면 특정 소스를 클릭하면 됩니다.

소스에 대한 자세한 내용은 소스 [개요를 참조하십시오](sources/sources-overview.md).

### 최근 세그먼트

최근 **[!UICONTROL 세그먼트]** 지표 카드는 조직 내에서 만들어진 가장 최근 5개의 세그먼트를 보여줍니다. 이 목록은 새 세그먼트를 만들면 업데이트됩니다.

세그먼트를 클릭하여 해당 항목에 대한 세부 사항을 보거나 추가 세그먼트에 대한 정보를 **[!UICONTROL 보려면 모두]** 보기를 클릭합니다.

세그먼트에 대한 자세한 내용은 세그멘테이션 [서비스 개요를 참조하십시오](segmentation/segmentation-overview.md).

### 최근 대상

최근 **[!UICONTROL 대상]** 지표 카드는 조직 내에서 만들어진 가장 최근 5개의 대상을 보여줍니다. 이 목록은 새 대상을 만들 때 업데이트됩니다.

대상을 클릭하여 해당 항목에 대한 세부 사항을 보거나, **[!UICONTROL 추가 대상에 대한 정보를 보려면 모두]** 보기를 클릭합니다.

대상에 대한 자세한 내용은 대상 [개요를 참조하십시오](destinations/overview.md).
