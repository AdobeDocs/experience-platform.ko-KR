---
keywords: 대상;대상;대상 유형
title: 대상 유형 및 카테고리
seo-title: 대상 유형 및 카테고리
description: Adobe Experience Platform의 다양한 대상 유형과 카테고리에 대해 알아봅니다.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# 대상 유형 및 카테고리

Adobe Experience Platform 대상의 다양한 유형과 카테고리를 이해하려면 이 페이지를 참조하십시오.

## 대상 유형

Adobe Experience Platform에서는 연결과 확장이라는 두 가지 대상 유형을 구별합니다. 연결 대상 유형인 프로필 내보내기 대상 및 세그먼트 내보내기 대상이 2개 있습니다.

![대상 유형](./assets/destination-types/types-of-destinations.png)

## 연결 {#connections}

**[!UICONTROL Profile Export]** Adobe Experience Platform **[!UICONTROL Segment Export]** 의 대상(Destination)은 이벤트 데이터를 캡처하고 다른 데이터 소스와 결합하여  [실시간 고객 프로파일을 만들고 세그멘테이션을 적용하며 세그먼트 및 자격이 있는 프로파일을 대상에 내보낼 수 있습니다](../profile/home.md).

## 프로필 내보내기 대상

프로필 내보내기 대상은 프로필 및/또는 속성이 포함된 파일을 생성합니다. 이러한 대상은 원시 데이터를 사용하며, 이메일 주소를 기본 키로 사용합니다. [Amazon S3 클라우드 스토리지 대상](./catalog/cloud-storage/amazon-s3.md)은 프로필 내보내기가 포함된 파일을 저장할 수 있는 대상의 예입니다.

## 세그먼트 내보내기 대상

세그먼트 내보내기 대상은 대상 플랫폼에 자격이 있는 프로필 및 세그먼트를 보냅니다. 이러한 대상은 세그먼트 ID 또는 사용자 ID를 사용합니다. 이러한 유형의 대상은 [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) 또는 [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md)과 같은 광고 대상입니다.

## 프로필 내보내기 및 세그먼트 내보내기 대상 - 비디오 개요

아래 비디오에서는 두 가지 유형의 대상에 대한 세부 사항을 살펴봅니다.

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 확장 {#extensions}

Platform(플랫폼)은 Adobe Experience Platform Launch의 강력하고 유연한 기능을 활용하여 플랫폼 인터페이스에 Platform launch 확장을 포함합니다.

>[!TIP]
>
>사용 사례 및 인터페이스에서 이러한 확장 기능을 찾는 방법을 포함한 Adobe Experience Platform Launch 확장 기능에 대한 자세한 내용은 [Adobe Experience Platform Launch 확장 개요](./catalog/launch-extensions/overview.md)를 참조하십시오.

platform launch 익스텐션은 원시 이벤트 데이터를 여러 유형의 대상으로 전달합니다. 확장을 대상의 **이벤트 전달** 유형으로 생각해 보십시오. 이는 원시 이벤트 데이터만 전달하는 대상 플랫폼과의 단순한 통합 유형입니다. 이러한 예로는 [Gainsight 개인화 확장](./catalog/personalization/gainsight.md) 또는 고객 확장](./catalog/voice/confirmit-digital-feedback.md)의 [확인 음성이 있습니다.

![다른 대상과 Experience Platform Launch 확장](./assets/common/launch-and-other-destinations.png)

## 연결 및 확장 사용 시기

마케터는 연결과 확장 기능을 결합하여 사용 사례를 해결할 수 있습니다.

정품 인증을 위해 전체 중앙 관리 방식의 고객 프로필 또는 고객 세그먼트를 활용해야 하는 경우 연결이 유용합니다. 예를 들어, 업로드된 CRM 데이터와 함께 분석 시스템의 행동 데이터를 결합하는 경우 연결을 사용하여 해당 사용자에게 개인화된 메시지를 전달하기 전에 지정된 세그먼트에 대한 사용자를 자격을 얻게 됩니다.

익스텐션은 이벤트 데이터를 사용하여 작업을 트리거하거나 외부 환경에서 세그멘테이션을 수행하는 경우에 유용합니다. 예를 들어, 지정된 사용자에 대해 다른 데이터 소스에 가입하지 않고 외부 시스템으로 행동 데이터를 전달해야 하는 경우

## 대상 카테고리

[대상 카탈로그](https://platform.adobe.com/destination/catalog)의 연결 및 확장은 사용자가 수행하는 마케팅 작업에 따라 대상 카테고리(**광고**, **클라우드 스토리지**, **설문 조사 플랫폼**, **이메일 마케팅** 등)별로 그룹화됩니다. 각 카테고리와 각 카테고리에 포함된 대상에 대한 자세한 내용은 [대상 카탈로그 설명서](./catalog/overview.md)를 참조하십시오.

![대상 카테고리](./assets/destination-types/destination-categories-menu.png)

