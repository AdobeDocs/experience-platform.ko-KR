---
keywords: 대상;대상;대상 유형
title: 대상 유형 및 카테고리
description: Adobe Experience Platform의 다양한 대상 유형 및 카테고리에 대해 알아봅니다.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---

# 대상 유형 및 카테고리

Adobe Experience Platform 대상의 다양한 유형과 카테고리를 이해하려면 이 페이지를 읽으십시오.

## 대상 유형 {#destination-types}

Adobe Experience Platform에서는 연결과 확장의 두 대상 유형을 구별합니다. 연결 대상의 두 가지 유형인 프로필 내보내기 대상과 세그먼트 내보내기 대상이 있습니다.

![대상 유형](./assets/destination-types/types-of-destinations.png)

## 연결 {#connections}

**[!UICONTROL 프로필 내보내기]**, **[!UICONTROL 스트리밍 세그먼트 내보내기]**, 및 **[!DNL Edge Personalization]** Adobe Experience Platform의 대상 캡처 이벤트 데이터를 대상으로 하여 다른 데이터 소스와 결합하여 양식을 구성합니다 [실시간 고객 프로필](../profile/home.md), 세그먼테이션을 적용하고 세그먼트와 자격을 갖춘 프로필을 대상으로 내보냅니다.

## 프로필 내보내기 대상 {#profile-export}

프로필 내보내기 대상은 원시 데이터를 받게 되며, 종종 이메일 주소를 기본 키로 사용합니다. Experience Platform은 현재 두 가지 유형의 프로필 내보내기 대상을 지원합니다.

* [스트리밍 프로필 내보내기 대상(엔터프라이즈 대상)](#streaming-profile-export)
* [배치(파일 기반) 대상](#file-based)

### 스트리밍 프로필 내보내기 대상(엔터프라이즈 대상) {#streaming-profile-export}

>[!IMPORTANT]
>
>엔터프라이즈 대상 또는 스트리밍 프로필 내보내기 대상을 사용할 수 있습니다 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 고객에게만 해당됩니다.

엔터프라이즈 대상 Data Connectors를 사용하여 내부 시스템 또는 기타 타사 시스템에 Adobe Real-time Customer Data Platform 프로필을 실시간으로 전달하여 데이터 동기화, 분석 및 추가적인 프로필 보강 사용 사례를 제공합니다.

이러한 대상은 Experience Platform 데이터 스트림으로 세그먼트 및 프로필 데이터를 받습니다.

엔터프라이즈 대상:

* [HTTP API 대상](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure 이벤트 허브](catalog/cloud-storage/azure-event-hubs.md)

### 배치(파일 기반) 대상 {#file-based}

파일 기반 대상 수신 `.csv` 프로필 및/또는 속성을 포함하는 파일. [Amazon S3](catalog/cloud-storage/amazon-s3.md) 은 프로필 내보내기가 포함된 파일을 내보낼 수 있는 대상의 예입니다.

## 스트리밍 세그먼트 내보내기 대상 {#streaming-destinations}

세그먼트 내보내기 대상이 Experience Platform 세그먼트 데이터를 받습니다. 이러한 대상은 세그먼트 ID 또는 사용자 ID를 사용합니다. 광고 및 다음과 같은 소셜 대상 [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md), 또는 [Facebook](catalog/social/facebook.md) 은 그러한 대상의 예시입니다.

## Edge 개인화 대상 {#edge-personalization-destinations}

Experience Platform의 Edge 개인화 대상은 다음과 같습니다 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 그리고 [사용자 지정 개인화 대상](/help/destinations/catalog/personalization/custom-personalization.md). 이러한 대상을 사용하여 고객에 대해 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화할 수 있습니다.

방법 알아보기 [동일한 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성](/help/destinations/ui/configure-personalization-destinations.md).

## 프로필 내보내기 및 세그먼트 내보내기 대상 - 비디오 개요 {#video}

아래 비디오에서는 두 가지 유형의 대상의 세부기간을 안내합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 확장 {#extensions}

Platform은 태그 관리의 힘과 유연성을 활용하여 UI에서 태그 확장을 구성할 수 있습니다.

>[!TIP]
>
>사용 사례 및 인터페이스에서 태그 확장을 찾는 방법을 비롯한 태그 확장에 대한 자세한 내용은 [태그 확장 개요](./catalog/launch-extensions/overview.md).

태그 확장은 원시 이벤트 데이터를 여러 유형의 대상에 전달합니다. 확장을 **이벤트 전달** 대상 유형입니다. 이는 원시 이벤트 데이터만 전달하는 대상 플랫폼과의 단순한 통합 유형입니다. 그 예는 다음과 같습니다 [Gainsight 개인화 확장](./catalog/personalization/gainsight.md) 또는 [고객 확장의 음성 확인](./catalog/voice/confirmit-digital-feedback.md).

![다른 대상과 비교하여 태그 확장](./assets/common/launch-and-other-destinations.png)

## 연결 및 확장을 사용해야 하는 경우 {#when-to-use}

마케터는 연결과 확장의 조합을 사용하여 사용 사례를 처리할 수 있습니다.

연결은 전체 중앙 집중식 고객 프로필 또는 활성화를 위해 고객 세그먼트를 활용해야 할 때 유용합니다. 예를 들어, 업로드된 CRM 데이터와 분석 시스템의 행동 데이터를 결합하여 해당 사용자에게 개인화된 메시지를 전달하기 전에 해당 세그먼트에 대한 사용자의 자격을 부여하는 경우 연결을 사용합니다.

확장은 이벤트 데이터를 사용하여 작업을 트리거하거나 외부 환경에서 세그멘테이션을 수행할 때 유용합니다. 예를 들어, 지정된 사용자에 대해 파일의 다른 데이터 소스에 가입하지 않고 동작 데이터를 외부 시스템으로 전달해야 하는 경우.

## 대상 카테고리 {#categories}

의 연결 및 확장 [대상 카탈로그](https://platform.adobe.com/destination/catalog) 대상 카테고리별로 그룹화됩니다(**광고**, **클라우드 스토리지**, **설문 조사 플랫폼**, **이메일 마케팅**&#x200B;등)을 사용할 수 있습니다. 각 카테고리와 각 카테고리에 포함된 대상에 대한 자세한 내용은 [대상 카탈로그 설명서](./catalog/overview.md).

![대상 카테고리](./assets/destination-types/destination-categories-menu.png)
