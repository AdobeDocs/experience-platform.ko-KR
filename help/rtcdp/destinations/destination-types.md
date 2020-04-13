---
title: 대상 유형 및 카테고리
seo-title: 대상 유형 및 카테고리
description: 'Adobe 실시간 고객 데이터 플랫폼에서 프로필/세그먼트 내보내기 대상은 이벤트 데이터를 캡처하고, 다른 데이터 소스와 결합하고, 세그멘테이션을 적용하며, 세그먼트와 적격한 프로필을 대상에 내보냅니다. 익스텐션을 실행하면 원시 이벤트 데이터가 여러 유형의 대상으로 전달됩니다. '
seo-description: Adobe 실시간 고객 데이터 플랫폼에서 프로필/세그먼트 내보내기 대상은 이벤트 데이터를 캡처하고, 다른 데이터 소스와 결합하고, 세그멘테이션을 적용하며, 세그먼트와 적격한 프로필을 대상에 내보냅니다. 익스텐션을 실행하면 원시 이벤트 데이터가 여러 유형의 대상으로 전달됩니다.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# 대상 유형 및 카테고리

Adobe 실시간 고객 데이터 플랫폼 대상의 다양한 유형과 카테고리를 이해하려면 이 페이지를 참조하십시오.

## 대상 유형

Adobe는 실시간 고객 데이터 플랫폼에서 연결과 확장이라는 두 가지 대상 유형을 구별합니다. 연결 대상 유형에는 프로필 내보내기 대상 및 세그먼트 내보내기 대상의 두 가지가 있습니다.

![대상 유형](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### 연결

**프로파일 내보내기** 및 **세그먼트 내보내기** Adobe 실시간 고객 데이터 플랫폼의 대상: 이벤트 데이터를 캡처하고, 다른 데이터 소스와 결합하여 [실시간 고객 프로파일을](https://docs.adobe.com/content/help/en/experience-platform/profile/home.html)만들고, 세그먼테이션을 적용하며, 세그먼트와 자격이 있는 프로파일을 대상에 내보낼 수 있습니다.

<br> 

#### 프로필 내보내기 대상

프로필 내보내기 대상은 프로필 및/또는 속성이 포함된 파일을 생성합니다. 이러한 대상은 종종 이메일 주소와 함께 원시 데이터를 사용합니다. Amazon [S3 클라우드 스토리지 대상은](/help/rtcdp/destinations/amazon-s3-destination.md) 프로필 내보내기가 포함된 파일을 저장할 수 있는 대상의 예입니다.

#### 세그먼트 내보내기 대상

세그먼트 내보내기 대상은 대상 플랫폼에 자격이 있는 프로필과 세그먼트를 보냅니다. 이러한 대상은 세그먼트 ID 또는 사용자 ID를 사용합니다. Google Display &amp; Video [360](/help/rtcdp/destinations/google-dv360-destination.md) 또는 Google [Ads와 같은](/help/rtcdp/destinations/google-ads-destination.md) 광고 대상은 이러한 유형의 대상입니다.

#### 프로필 내보내기 및 세그먼트 내보내기 대상 - 비디오 개요

아래 비디오에서는 두 가지 유형의 대상에 대한 세부 사항을 살펴봅니다.

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### 확장

Adobe Real-time CDP는 Adobe Experience Platform Launch의 강력하고 유연한 기능을 활용하여 Launch 익스텐션을 Adobe 실시간 CDP 인터페이스에 포함시킵니다.

익스텐션을 실행하면 원시 이벤트 데이터가 여러 유형의 대상으로 전달됩니다. 확장을 대상의 **이벤트 전달** 유형으로 간주합니다. 이는 원시 이벤트 데이터만 전달하는 대상 플랫폼과의 단순한 통합 유형입니다. 이러한 예는 Gainsight [개인화 확장](/help/rtcdp/destinations/gainsight-extension.md) 또는 [고객 확장의](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Confirmation Voice입니다.

Experience Platform Launch 확장 기능에 대한 자세한 내용은 Launch [확장 개요를](/help/rtcdp/destinations/experience-platform-launch-extensions.md)참조하십시오.


![다른 대상과 비교하여 경험 플랫폼 실행 확장](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### 연결 및 확장 기능 사용 시기

마케터는 연결과 확장 기능을 결합하여 사용 사례를 해결할 수 있습니다.

전체 중앙 관리 고객 프로파일 또는 고객 세그먼트를 활성화하여 사용해야 하는 경우 연결이 유용합니다. 예를 들어, 업로드된 CRM 데이터와 함께 분석 시스템의 행동 데이터를 결합하는 경우 연결을 사용하여 해당 사용자에게 개인화된 메시지를 전달하기 전에 해당 세그먼트에 대한 사용자를 검증합니다.

익스텐션은 이벤트 데이터를 사용하여 작업을 트리거하거나 외부 환경에서 세그멘테이션을 수행하는 경우에 유용합니다. 예를 들어, 지정된 사용자에 대해 다른 데이터 소스에 연결하지 않고 외부 시스템으로 행동 데이터를 전달해야 하는 경우

<br> 

## 대상 카테고리

대상 카탈로그의 [대상 및 대상은](https://platform.adobe.com/destination/catalog) 대상에 따라&#x200B;**분류됩니다(**&#x200B;대상 카탈로그의 **대상 및**&#x200B;대상 카테고리 **, 설문 조사 플랫폼,**&#x200B;설문 조사 플랫폼, 이메일 마케팅, 확장 등 **)**. 각 카테고리 및 각 카테고리에 포함된 대상에 대한 자세한 내용은 대상 [카탈로그 설명서를](/help/rtcdp/destinations/destinations-catalog.md)참조하십시오.

![대상 카테고리](/help/rtcdp/destinations/assets/destination-categories.png)

