---
keywords: 세분화;세분화 rtcdp;실시간 고객 데이터 플랫폼 세분화
title: 실시간 고객 데이터 플랫폼의 세분화 서비스
seo-title: 실시간 고객 데이터 플랫폼의 세분화 서비스
description: 실시간 CDP는 Adobe Experience Platform을 기반으로 구축되어 많은 Experience Platform 서비스 및 기능을 활용합니다. 세그멘테이션 서비스를 사용하면 유사한 트레이트를 가진 작은 그룹으로 고객을 구분하여 맞춤 마케팅을 제공할 수 있습니다.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# [!DNL Segmentation Service] in [!DNL Real-time Customer Data Platform]

[!DNL Real-time Customer Data Platform] (실시간 CDP)를 사용하면 여러 소스에서 데이터를 가져와 고객에게 일관되고 일관된 경험을 제공할 수 있습니다. Adobe Experience Platform의 일부인 [!DNL Segmentation Service]을 사용하여 연관성 있는 개인화된 마케팅 캠페인을 제공할 수 있습니다.

실시간 CDP는 Adobe Experience Platform을 기반으로 구축되며, 많은 [!DNL Experience Platform] 서비스 및 기능을 활용합니다. [!DNL Segmentation Service]을 사용하면 고객을 유사한 트레이트가 있는 작은 그룹으로 나누어 맞춤 마케팅을 제공할 수 있습니다.

## 세그먼테이션

세그먼테이션은 프로필 하위 세트가 프로필 스토어와 공유한 특정 특성 또는 행동을 정의하여 마케팅 가능한 사람 그룹을 고객 기반과 구별하는 프로세스입니다. 예를 들어 &quot;운동화 구입을 잊으셨습니까?&quot;라는 이메일 캠페인에서는 지난 30일 이내에 운동화를 검색했지만 구매를 완료하지 않은 모든 사용자를 원할 수 있습니다. 세그먼트가 다른 경우 다양한 대상에 집중할 수 있으므로 보다 맞춤화된 마케팅 경험을 제공할 수 있습니다.

## [!DNL Segment Builder]

[!DNL Platform] 세그먼트를 쉽게 만들고 액세스할 수 있을 뿐만 아니라, 다양한 기본 요소를 사용하여 세그먼트를 더 세분화할 수 있습니다. 세그먼트 빌더 사용 방법에 대한 자세한 내용은 [세그먼트 빌더 안내서](./segment-builder-guide.md)를 참조하십시오.

## 고객 AI

실시간 고객 데이터 플랫폼에 포함되어 있는 고객 AI는 고객의 상황을 개별적으로 예측하는 방법을 제공합니다.

고객 AI는 영향력 있는 요소를 활용하여 고객의 관심사와 이유를 파악할 수 있습니다. 또한 고객 AI의 예측과 인사이트를 활용하여 최적의 제안과 메시지를 제공함으로써 고객 경험을 개인화할 수 있습니다. 고객 AI는 다음을 지원할 수 있습니다.

* 세그멘테이션 및 타깃팅을 강화할 수 있는 정확도가 높은 고객 성향 모델을 제공합니다.
* 특정 고객 행동의 영향력과 가능성을 파악합니다.
* 회사의 고유한 사용 사례 및 데이터에 대해 사용자 정의 가능한 옵션을 제공합니다.
* 고객 이탈률 및 전환율과 같은 고객 성향 점수를 통해 실시간 고객 프로파일 향상
* 고객 성향 점수를 위한 영향력 있는 요소를 통해 고객 프로파일을 향상시킬 수 있습니다.
* 영향력 있는 요인 및 성향 점수를 기반으로 고객 세그먼트 만들기

고객 AI는 **[!UICONTROL Adobe 서비스]**&#x200B;의 **[!UICONTROL 서비스]** 탭에 있습니다.

![고객 AI 위치](../assets/overview/rtcdp-customer-ai.png)

### 고객 AI 시작하기

고객 AI를 시작하려면 [데이터 사전 설정 자습서](../../intelligent-services/data-preparation.md)를 따르고 사용 사례에 따라 입력 스키마를 구성해야 합니다. 다음으로 [고객 AI 인스턴스](../../intelligent-services/customer-ai/user-guide/configure.md)를 구성해야 합니다. 인스턴스를 구성한 후 [인사이트와 점수](../../intelligent-services/customer-ai/user-guide/discover-insights.md)를 볼 수 있는 모델이 생성됩니다. 모델에서 생성된 데이터를 사용하여 데이터 기반 활성화를 위한 세그먼트를 만들 수 있습니다.

고객 AI에 대한 자세한 내용은 [고객 AI 개요](../../intelligent-services/customer-ai/overview.md)를 방문하여 시작하십시오. 또한 다음 비디오에서는 고객 AI가 어떻게 AI 기반 자산으로 고객 프로파일을 강화하고 고객 세분화와 타겟팅 활동을 강화하는지 보여줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/40374/?quality=12&learn=on)


## 다음 단계

이 개요를 본 후에는 실시간 CDP가 [!DNL Segmentation Service]을 활용하여 마케팅 캠페인의 맞춤화 및 개인화를 향상시키는 방법을 이해해야 합니다. [!DNL Segmentation Service]에 대한 자세한 내용은 [세그멘테이션 설명서](../../segmentation/home.md)를 참조하십시오.
