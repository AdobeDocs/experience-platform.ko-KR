---
keywords: 세분화; 세분화 rtcdp;실시간 고객 데이터 플랫폼 세그멘테이션
title: Real-time Customer Data Platform의 세그멘테이션 서비스
description: Adobe Real-Time Customer Data Platform은 Adobe Experience Platform을 기반으로 구축되었으며 많은 Experience Platform 서비스 및 기능을 사용합니다. 세그멘테이션 서비스를 사용하여 고객을 유사한 트레이트를 가진 작은 그룹으로 분할하여 맞춤 마케팅을 제공할 수 있습니다.
exl-id: 140667c0-e288-40c4-8c45-c275e348b84a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 4%

---

# [!DNL Segmentation Service] in [!DNL Real-Time Customer Data Platform]

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP)을 사용하면 여러 소스에서 데이터를 가져와 고객에게 통일되고 일관된 경험을 제공할 수 있습니다. 관련 개인화된 마케팅 캠페인을 제공하는 것은 [!DNL Segmentation Service]Adobe Experience Platform에 속해 있어야 합니다.

Real-Time CDP은 Adobe Experience Platform을 기반으로 구축되었으며, [!DNL Experience Platform] 서비스 및 기능. 사용 [!DNL Segmentation Service]를 사용하면 고객을 유사한 트레이트로 더 작은 그룹으로 분할하여 맞춤 마케팅을 제공할 수 있습니다.

## 세그먼테이션

세그먼테이션은 마케팅 가능한 사람 그룹을 고객 기반과 구분하기 위해 프로필 저장소의 프로필 하위 집합에 의해 공유되는 특정 속성 또는 동작을 정의하는 프로세스입니다. 예를 들어 &quot;운동화 구입을 잊으셨습니까?&quot;라는 이메일 캠페인에서 지난 30일 이내에 운동화 구매를 검색했지만 구매를 완료하지 않은 모든 사용자의 청중을 원할 수 있습니다. 다양한 세그먼트를 사용하여 다양한 대상에 집중하여 보다 맞춤형 마케팅 경험을 제공할 수 있습니다.

## [!DNL Segment Builder]

[!DNL Platform] 을(를) 사용하면 세그먼트를 쉽게 만들고 액세스할 수 있을 뿐만 아니라, 서로 다른 구성 요소를 사용하여 세그먼트를 더 규명할 수 있습니다. 세그먼트 빌더 사용 방법에 대한 자세한 내용은 [세그먼트 빌더 안내서](./segment-builder-guide.md).

## 고객 AI

Real-time Customer Data Platform에 포함된 고객 AI는 개별 수준에서 고객 예측을 생성할 수 있는 기능을 제공합니다.

영향력 있는 요소를 통해 Customer AI는 고객이 무엇을 할 수 있고 왜 하는지 알려 줄 수 있습니다. 또한 Customer AI 예측 및 인사이트를 통해 가장 적합한 오퍼 및 메시지를 제공하여 고객 경험을 개인화할 수 있습니다. 고객 AI는 다음을 지원할 수 있습니다.

* 더 강력한 세분화 및 타겟팅을 위해 정확도가 높은 고객 성향 모델을 제공합니다.
* 특정 고객 행동에 영향을 미치는 요소와 가능성을 파악합니다.
* 회사의 고유한 사용 사례 및 데이터에 대해 사용자 정의 가능한 옵션 제공.
* 이탈 및 전환과 같은 고객 성향 점수를 통해 실시간 고객 프로필 개선.
* 성향 점수에 대한 영향력 있는 요소로 고객 프로필 개선.
* 영향력 있는 요소 및 성향 점수를 기반으로 고객의 세그먼트 만들기

고객 AI는 **[!UICONTROL 서비스]** 아래의 탭 **[!UICONTROL Adobe 서비스]**.

![고객 AI 위치](../assets/overview/rtcdp-customer-ai.png)

### 고객 AI 시작하기

Customer AI를 시작하려면 다음을 수행해야 합니다 [데이터 준비 자습서](../../intelligent-services/data-preparation.md) 사용 사례에 따라 입력 스키마를 구성합니다. 이제 다음을 수행해야 합니다 [고객 AI 인스턴스 구성](../../intelligent-services/customer-ai/user-guide/configure.md). 인스턴스를 구성한 후 다음을 수행할 수 있는 모델이 생성됩니다 [인사이트 및 점수 보기](../../intelligent-services/customer-ai/user-guide/discover-insights.md). 모델에서 생성된 데이터를 사용하여 데이터 기반 활성화를 위한 세그먼트를 만들 수 있습니다.

Customer AI에 대해 자세히 알아보려면 [Customer AI 개요](../../intelligent-services/customer-ai/overview.md). 또한 다음 비디오에서는 고객 AI 가 AI 기반 자산으로 고객 프로필을 강화하고 고객 세분화와 타겟팅 활동을 강화하는 방법을 보여줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/40374/?quality=12&learn=on)


## 다음 단계

이 개요를 읽고 나면 이제 Real-Time CDP이 어떻게을 활용하는지를 이해해야 합니다 [!DNL Segmentation Service] 마케팅 캠페인의 사용자 지정 및 개인화를 개선하기 위해 에 대한 자세한 정보 [!DNL Segmentation Service]을(를) 참조하십시오. [세그먼테이션 설명서](../../segmentation/home.md).
