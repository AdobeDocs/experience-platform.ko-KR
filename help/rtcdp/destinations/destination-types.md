---
keywords: destinations;destination;destination types
title: 대상 유형 및 카테고리
seo-title: 대상 유형 및 카테고리
description: '실시간 고객 데이터 플랫폼에서 프로필/세그먼트 내보내기 대상은 이벤트 데이터를 캡처하고, 다른 데이터 소스와 결합하고, 세그멘테이션을 적용하고, 세그먼트 및 자격 있는 프로필을 대상에 내보냅니다. Experience Platform Launch 익스텐션은 원시 이벤트 데이터를 여러 유형의 대상으로 전달합니다. '
seo-description: 실시간 고객 데이터 플랫폼에서 프로필/세그먼트 내보내기 대상은 이벤트 데이터를 캡처하고, 다른 데이터 소스와 결합하고, 세그멘테이션을 적용하고, 세그먼트 및 자격 있는 프로필을 대상에 내보냅니다. Experience Platform Launch 익스텐션은 원시 이벤트 데이터를 여러 유형의 대상으로 전달합니다.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---


# 대상 유형 및 카테고리

실시간 고객 데이터 플랫폼 대상의 다양한 유형과 카테고리를 이해하려면 이 페이지를 참조하십시오.

## 대상 유형

실시간 고객 데이터 플랫폼에서는 연결과 익스텐션 등 두 가지 대상 유형을 구별합니다. 두 가지 연결 대상, 프로필 내보내기 대상 및 세그먼트 내보내기 대상이 있습니다.

![대상 유형](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### 연결 {#connections}

**[!UICONTROL 실시간 고객 데이터 플랫폼의 프로필 내보내기]** 및 **[!UICONTROL 세그먼트 내보내기]** 대상 [은 이벤트 데이터를 캡처하고, 다른 데이터 소스와 결합하여](/help/profile/home.md)실시간 고객 프로필을만들고, 세분화를 적용하며, 세그먼트 및 자격이 있는 프로필을 대상에 내보냅니다.

<br> 

#### 프로필 내보내기 대상

프로필 내보내기 대상은 프로필 및/또는 속성이 포함된 파일을 생성합니다. 이러한 대상은 종종 이메일 주소와 함께 원시 데이터를 기본 키로 사용합니다. 프로필 내보내기가 포함된 파일을 저장할 수 있는 [Amazon S3 클라우드 스토리지 대상의](/help/rtcdp/destinations/amazon-s3-destination.md) 예입니다.

#### 세그먼트 내보내기 대상

세그먼트 내보내기 대상은 대상 플랫폼에 자격을 부여받은 프로필 및 세그먼트를 보냅니다. 이러한 대상은 세그먼트 ID 또는 사용자 ID를 사용합니다. 이러한 유형의 목적지 [[!DNL Google Display & Video 360]](/help/rtcdp/destinations/google-dv360-destination.md) 또는 [[!DNL Google Ads]](/help/rtcdp/destinations/google-ads-destination.md) 와 같은 광고 목적지

#### 프로필 내보내기 및 세그먼트 내보내기 대상 - 비디오 개요

아래 비디오에서는 두 가지 유형의 대상에 대한 세부 사항을 살펴봅니다.

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### 확장 {#extensions}

Adobe 실시간 CDP는 Adobe Experience Platform Launch의 기능과 유연성을 활용하여 Adobe 실시간 CDP 인터페이스에 플랫폼 실행 확장 기능을 포함시킵니다.

>[!TIP]
>
>사용 사례 및 인터페이스에서 이를 찾는 방법 등 Adobe Experience Platform Launch 익스텐션에 대한 자세한 내용은 [Adobe Experience Platform Launch 익스텐션 개요를 참조하십시오](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

플랫폼 론치 익스텐션은 원시 이벤트 데이터를 여러 유형의 대상으로 전달합니다. 익스텐션을 대상의 **이벤트 전달** 유형으로 간주합니다. 이는 원시 이벤트 데이터만 전달하는 대상 플랫폼과의 단순한 통합 유형입니다. 이러한 예는 [Gainsight 개인화 확장](/help/rtcdp/destinations/gainsight-extension.md) 또는 [고객 확장의 확인 음보입니다](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md).

![다른 대상과 Experience Platform Launch 확장](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### 연결 및 확장 사용 시기

마케터는 연결과 확장 기능을 결합하여 사용 사례를 해결할 수 있습니다.

고객 연결은 정품 인증을 위해 중앙 관리 방식의 전체 고객 프로필 또는 고객 세그먼트를 활용해야 할 때 유용합니다. 예를 들어, 업로드된 CRM 데이터와 분석 시스템의 행동 데이터를 결합하는 경우 연결을 사용하여 해당 사용자에게 개인화된 메시지를 전달하기 전에 지정된 세그먼트에 대한 사용자의 자격을 얻게 됩니다.

익스텐션은 이벤트 데이터를 사용하여 작업을 트리거하거나 외부 환경에서 세그멘테이션을 수행하는 경우에 유용합니다. 예를 들어, 지정된 사용자에 대해 다른 데이터 소스에 연결하지 않고 외부 시스템으로 행동 데이터를 전달해야 하는 경우

<br> 

## 대상 카테고리

대상 카탈로그의 [연결 및 확장](https://platform.adobe.com/destination/catalog) 기능은&#x200B;**수행하는 마케팅 사용 사례에 따라 대상 범주(**&#x200B;광고 **, 스토리지**, 설문 조사 플랫폼 **,,**&#x200B;이메일 마케팅, 기타)별로 그룹화됩니다 ****. 각 카테고리와 각 카테고리에 포함된 대상에 대한 자세한 내용은 [대상 카탈로그 설명서를 참조하십시오](/help/rtcdp/destinations/destinations-catalog.md).

![대상 카테고리](/help/rtcdp/destinations/assets/destination-categories-menu.png)

