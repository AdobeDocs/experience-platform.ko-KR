---
keywords: Experience Platform;홈;인기 항목;대상 관리자 소스 커넥터;Audience Manager;대상 관리자 커넥터
solution: Experience Platform
title: UI에서 Adobe Audience Manager 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: 이 자습서에서는 사용자 인터페이스를 사용하여 Consumer Experience Event 데이터를 Platform으로 가져오기 위한 Adobe Audience Manager용 소스 커넥터를 만드는 단계를 안내합니다.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# UI에서 Adobe Audience Manager 소스 연결 만들기

이 자습서에서는 사용자 인터페이스를 사용하여 Consumer Experience Event 데이터를 Platform으로 가져오기 위해 Adobe Audience Manager용 소스 커넥터를 만드는 단계를 안내합니다.

## Adobe Audience Manager을 사용하여 소스 연결 만들기

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL Sources]**&#x200B;를 선택하여 [!UICONTROL Sources] 작업 영역에 액세스합니다. [!UICONTROL Catalog] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

[!UICONTROL Adobe applications] 범주에서 **[!UICONTROL Adobe Audience Manager]**&#x200B;을 선택한 다음 **[!UICONTROL Configure]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/aam/catalog.png)

트레이트, 세그먼트 및 데이터를 탐색 및 선택할 수 있는 대화형 인터페이스를 제공하는 [!UICONTROL Select traits and segments] 단계가 나타납니다.

* 인터페이스의 왼쪽 패널에는 [!UICONTROL Select traits and segments] 옵션과 사용 가능한 모든 세그먼트의 계층 디렉토리가 포함됩니다.
* 인터페이스의 오른쪽 절반을 사용하면 선택한 세그먼트와 상호 작용하고 사용하려는 특정 데이터를 선택할 수 있습니다.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

사용 가능한 세그먼트를 탐색하려면 [!UICONTROL All Segments] 패널에서 액세스할 폴더를 선택합니다. 폴더를 선택하면 폴더의 계층을 트래버스할 수 있으며 필터링할 세그먼트 목록을 제공합니다.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

사용하려는 세그먼트를 식별하여 선택하면 선택한 항목의 목록을 표시하는 새 패널이 오른쪽에 표시됩니다. 다른 폴더에 계속 액세스하고 연결에 대해 다른 세그먼트를 선택할 수 있습니다. 세그먼트를 더 선택하면 오른쪽의 패널이 업데이트됩니다.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

또는 **[!UICONTROL Select all segments]** 및 **[!UICONTROL Select all traits]** 상자를 선택할 수 있습니다. 모든 세그먼트를 선택하면 Audience Manager 세그먼트가 플랫폼에 이동되고 모든 트레이트를 선택하면 Audience Manager의 자사 트레이트가 모두 활성화됩니다.

완료되면 **[!UICONTROL Next]** 선택

![모든 세그먼트](../../../../images/tutorials/create/aam/all-segments.png)

[!UICONTROL Review] 단계가 나타나 선택한 트레이트와 세그먼트를 플랫폼에 연결하기 전에 검토할 수 있습니다. 세부 사항은 다음 카테고리 내에서 그룹화됩니다.

* **[!UICONTROL Connection]**:소스 플랫폼과 연결 상태를 표시합니다.
* **[!UICONTROL Selected data]**:선택한 세그먼트 수와 활성화된 트레이트의 수를 표시합니다.

![검토](../../../../images/tutorials/create/aam/review.png)

데이터 흐름을 검토했으면 **[!UICONTROL Finish]**&#x200B;을 선택하고 데이터 흐름을 만드는 데 약간의 시간이 소요됩니다.

## 다음 단계

Audience Manager 데이터 흐름 기능이 활성화되면 들어오는 데이터를 실시간 고객 프로필로 자동으로 인제스트됩니다. 이제 이 수신 데이터를 활용하고 플랫폼 세그멘테이션 서비스를 사용하여 고객 세그먼트를 만들 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../../../../profile/home.md)
* [세그멘테이션 서비스 개요](../../../../../segmentation/home.md)
