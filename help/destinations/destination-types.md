---
keywords: 대상;대상;대상 유형
title: 대상 유형 및 범주
description: Adobe Experience Platform의 다양한 유형과 범주에 대해 알아봅니다.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: ba5a539603da656117c95d19c9e989ef0e252f82
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# 대상 유형 및 범주

Adobe Experience Platform 대상의 다양한 유형과 범주를 이해하려면 이 페이지를 참조하십시오.

## 대상 유형 {#destination-types}

Adobe Experience Platform에서는 서로 다른 대상 유형(연결, 데이터 세트 내보내기 및 확장)을 구별합니다. 여러 유형의 연결 대상이 있으므로 데이터를 API 기반 대상으로 내보낼 수 있습니다.

마지막으로, 대상 카탈로그의 모든 조직에서 사용할 수 있는 공개 대상과 Real-Time CDP Ultimate 고객이 특정 내보내기 사용 사례를 충족하기 위해 만들 수 있는 비공개 대상을 연결할 수도 있습니다.

![대상 다이어그램 유형.](./assets/destination-types/types-of-destinations-no-highlight.png)

## 연결 {#connections}

**[!UICONTROL 프로필 내보내기]**, **[!UICONTROL 스트리밍 대상 내보내기]**, 및 **[!DNL Edge Personalization]** Adobe Experience Platform의 대상은 이벤트 데이터를 캡처하고 다른 데이터 소스와 결합하여 [실시간 고객 프로필](../profile/home.md)을 클릭하고, 세그멘테이션을 적용하고 대상 및 자격을 갖춘 프로필을 대상으로 내보냅니다.

## 프로필 내보내기 대상 {#profile-export}

프로필 내보내기 대상은 원시 데이터를 수신하며, 이때 기본 키는 이메일 주소입니다. Experience Platform은 현재 두 가지 유형의 프로필 내보내기 대상을 지원합니다.

* [스트리밍 프로필 내보내기 대상(엔터프라이즈 대상)](#streaming-profile-export)
* [배치(파일 기반) 대상](#file-based)

### 스트리밍 프로필 내보내기 대상(엔터프라이즈 대상) {#streaming-profile-export}

>[!IMPORTANT]
>
>엔터프라이즈 대상 또는 스트리밍 프로필 내보내기 대상은 다음 경우에 사용할 수 있습니다. [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 고객만 해당.

Enterprise 대상 Data Connectors를 사용하여 데이터 동기화, 분석 및 추가적인 프로필 보강 사용 사례를 위해 내부 시스템 또는 다른 서드파티 시스템에 거의 실시간으로 Adobe Real-time Customer Data Platform 프로필을 제공합니다.

이러한 대상은 대상자 및 프로필 데이터를 Experience Platform 데이터 스트림으로 수신합니다.

엔터프라이즈 대상에는 다음이 포함됩니다.

* [HTTP API 대상](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure 이벤트 허브](catalog/cloud-storage/azure-event-hubs.md)

### 배치(파일 기반) 대상 {#file-based}

파일 기반 대상 수신 `.csv` 프로필 및/또는 속성을 포함하는 파일입니다. [Amazon](catalog/cloud-storage/amazon-s3.md) 는 프로필 내보내기가 포함된 파일을 내보낼 수 있는 대상의 예입니다.

## 스트리밍 대상자 내보내기 대상 {#streaming-destinations}

대상자 내보내기 대상은 Experience Platform 대상자 데이터를 받습니다. 이러한 대상은 대상 ID 또는 사용자 ID를 사용합니다. 광고 및 소셜 대상 [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md), 또는 [Facebook](catalog/social/facebook.md) 는 이러한 대상의 예입니다.

## Edge 개인화 대상 {#edge-personalization-destinations}

Experience Platform의 Edge 개인화 대상은 다음과 같습니다 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 및 [사용자 지정 개인화 대상](/help/destinations/catalog/personalization/custom-personalization.md). 이러한 대상을 사용하면 고객에 대해 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화할 수 있습니다.

방법 자세히 알아보기 [동일 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성](/help/destinations/ui/activate-edge-personalization-destinations.md).

## 프로필 내보내기 및 대상자 내보내기 대상 - 비디오 개요 {#video}

아래 비디오에서는 두 가지 유형의 대상에 대한 자세한 내용을 소개합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 데이터 세트 내보내기 대상 {#dataset-export-destinations}

대상 카탈로그의 일부 클라우드 스토리지 대상이 데이터 세트 내보내기를 지원합니다. 이러한 대상을 사용하여 원시 데이터 세트를 클라우드 스토리지 위치로 내보냅니다.

방법 자세히 알아보기 [데이터 세트 내보내기](/help/destinations/ui/export-datasets.md).

## 확장 {#extensions}

플랫폼은 태그 관리의 강력한 기능과 유연성을 활용하므로 UI에서 태그 확장을 구성할 수 있습니다.

>[!TIP]
>
>사용 사례 및 인터페이스에서 태그 확장을 찾는 방법을 포함하여 태그 확장에 대한 자세한 내용은 [태그 확장 개요](./catalog/launch-extensions/overview.md).

태그 확장은 원시 이벤트 데이터를 여러 유형의 대상으로 전달합니다. 확장을 다음으로 고려: **이벤트 전달** 대상 유형. 이는 원시 이벤트 데이터만 전달하는 대상 플랫폼과의 통합 유형입니다. 예를 들면 다음과 같습니다. [Gainsight 개인화 확장](./catalog/personalization/gainsight.md) 또는 [고객의 소리 확장 확인](./catalog/voice/confirmit-digital-feedback.md).

![다른 대상과 비교한 태그 확장](./assets/common/launch-and-other-destinations.png)

## 연결 및 확장을 사용해야 하는 경우 {#when-to-use}

마케터는 연결과 확장을 함께 사용하여 사용 사례를 해결할 수 있습니다.

연결은 활성화를 위해 전체 중앙 집중식 고객 프로필 또는 고객 대상을 활용해야 할 때 유용합니다. 예를 들어, 업로드된 CRM 데이터와 Analytics 시스템의 행동 데이터를 결합하여 해당 사용자에게 개인화된 메시지를 전달하기 전에 사용자를 특정 대상에 맞게 자격을 부여하는 경우 연결을 사용하십시오.

확장은 이벤트 데이터를 사용하여 작업을 트리거하거나 외부 환경에서 세그멘테이션을 수행할 때 유용합니다. 예를 들어, 지정된 사용자에 대해 파일의 다른 데이터 소스에 조인되지 않고 동작 데이터를 외부 시스템으로 전달해야 하는 경우,

## 대상 범주 {#categories}

의 연결 및 확장 [대상 카탈로그](https://platform.adobe.com/destination/catalog) 대상 범주별로 그룹화됩니다(**광고**, **클라우드 스토리지**, **설문 조사 플랫폼**, **이메일 마케팅**, 등)는 달성에 도움이 되는 마케팅 활동에 따라 달라집니다. 각 범주와 각 범주에 포함된 대상에 대한 자세한 내용은 [대상 카탈로그 설명서](./catalog/overview.md).

![카탈로그 페이지에서 강조 표시된 대상 카테고리입니다.](./assets/destination-types/destination-categories-menu.png)
