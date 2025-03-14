---
title: 대상에 대한 잠재 고객 활성화
type: Tutorial
description: 잠재 고객을 대상으로 활성화하는 방법을 알아봅니다
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 13%

---

# 잠재 고객 대상자 활성화

>[!AVAILABILITY]
>
>이 기능은 Real-Time CDP Prime 및 Ultimate 패키지를 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

이 문서에서는 Adobe Experience Platform에서 선호하는 대상으로 [잠재 고객](/help/segmentation/types/prospect-audiences.md)을(를) 내보내는 데 필요한 워크플로에 대해 설명합니다.

## 지원되는 대상 {#supported-destinations}

**[!UICONTROL 연결]** > **[!UICONTROL 대상]**(으)로 이동한 다음 **[!UICONTROL 카탈로그]** 탭을 선택합니다. **[!UICONTROL 데이터 형식]** 필터를 사용하고 **[!UICONTROL 잠재 고객]**&#x200B;을 선택하여 잠재 고객 대상의 활성화를 지원하는 대상을 확인하십시오. 현재 Prospect Audiences 내보내기는 클라우드 스토리지 대상에서만 사용할 수 있습니다.

잠재 고객을 지원하는 ![대상.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## 전제 조건 {#prerequisites}

* 다운스트림 대상으로 활성화하려면 먼저 [잠재 고객 프로필](/help/profile/ui/prospect-profile.md)을 수집하고 [잠재 고객 대상](/help/segmentation/types/prospect-audiences.md)을 만들어야 합니다.
* 대상에 잠재 고객을 활성화하려면 대상에 성공적으로 연결해야 합니다. 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)(으)로 이동하여 지원되는 대상을 탐색하고 사용할 대상을 구성합니다. 자세한 내용은 [대상에 연결](./connect-destination.md)에 대한 UI 자습서를 참조하십시오.

### 필요한 권한 {#permissions}

잠재 고객을 활성화하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

잠재 고객을 활성화하는 데 필요한 권한이 있는지 확인하려면 대상 카탈로그를 확인하십시오. 대상에 **[!UICONTROL Activate]** 컨트롤이 있으면 적절한 사용 권한이 있습니다.

## 대상 선택 {#select-destination}

지침에 따라 데이터 세트를 내보낼 수 있는 대상을 선택합니다.

1. **[!UICONTROL 연결 > 대상]**(으)로 이동하여 **[!UICONTROL 카탈로그]** 탭을 선택합니다.

   ![카탈로그 컨트롤이 강조 표시된 대상 카탈로그 탭.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. 데이터 세트를 내보내려는 대상에 해당하는 카드에서 **[!UICONTROL 활성화]**&#x200B;를 선택합니다.

>[!TIP]
>
>프로필 대상을 내보낼 수 있는 대상은 카드 오른쪽 상단에 아래에 강조 표시된 대상과 유사한 아이콘으로 표시되거나, 데이터 유형 필터를 사용하여 [페이지에 더 위에 표시된 대로 잠재 대상을 내보낼 수 있는 대상만 표시할 수 있습니다](#supported-destinations).

![강조 표시된 프로필 대상을 내보낼 수 있는 Amazon S3 대상 페이지입니다.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. **[!UICONTROL 데이터 형식 잠재 고객]**&#x200B;을 선택한 후 데이터 집합을 내보내려는 대상 연결을 선택하고 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

>[!TIP]
> 
>잠재 고객을 활성화하기 위해 새 대상을 설정하려면 **[!UICONTROL 새 대상 구성]**&#x200B;을 선택하여 [대상에 연결](/help/destinations/ui/connect-destination.md) 워크플로우를 트리거하십시오.

![잠재 고객 컨트롤이 강조 표시된 대상 활성화 워크플로우입니다.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. [내보낼 프로필 대상을 선택](#select-profile-audiences)하려면 다음 섹션으로 이동하십시오.

## 잠재 고객 선택 {#select-prospect-audiences}

잠재 고객 이름 왼쪽에 있는 확인란을 사용하여 대상으로 내보낼 대상을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을(를) 선택합니다. 이 보기에는 Prospect 대상만 표시되고 다른 대상은 표시되지 않습니다.

![내보낼 잠재 고객을 선택할 수 있는 대상 선택 단계를 표시하는 데이터 세트 내보내기 워크플로우입니다.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## 예약 및 다음 단계

잠재 고객을 내보내기 위한 활성화 워크플로의 나머지 부분에 대해서는 파일 기반 대상으로 데이터 활성화에 대한 자습서를 참조하십시오. [대상자 내보내기 예약 단계](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)에서 계속합니다.

>[!NOTE]
>
>예약 단계에서 잠재 고객 활성화 워크플로를 사용하면 [전체 파일을 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)만 가능합니다. 증분 파일 내보내기는 지원되지 않습니다.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## 파트너 데이터 지원을 통해 달성한 기타 사용 사례 {#other-use-cases}

Real-Time CDP에서 파트너 데이터 지원을 통해 활성화된 추가 사용 사례를 살펴보십시오.

* [신뢰할 수 있는 데이터 파트너의 속성으로 자사 프로필을 보완](/help/rtcdp/partner-data/supplement-first-party-profiles.md)하여 데이터 기반을 개선하고 고객층에 대한 새로운 인사이트를 얻고 대상자 최적화를 개선합니다.
* Real-Time CDP에서 서드파티 데이터 지원을 사용하여 [데이터 파트너의 잠재 고객 프로필로 프로필 기반을 확장하고 데이터 파트너와 협력하여 신규 고객에게 도달하거나 확보할 수 있습니다](/help/rtcdp/partner-data/prospecting.md).
* [방문에서 사용자 인증을 받지 않았거나 브랜드에 대한 이전 기록이 없는 상태에서 온사이트 경험을 개인화하기 위해 파트너 지원 인식을 활용합니다](/help/rtcdp/partner-data/onsite-personalization.md).
