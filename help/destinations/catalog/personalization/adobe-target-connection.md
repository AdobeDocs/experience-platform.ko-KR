---
keywords: target 개인화; 대상; experience platform target 대상;adobe target 대상
title: Adobe Target 연결
description: Adobe Target은 웹 사이트, 모바일 앱 등에서 모든 인바운드 고객 상호 작용에 실시간 AI 기반의 개인화 및 실험 기능을 제공하는 애플리케이션입니다.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 61a3a05466eca30ba08fcaf32a3f00e0ca49f325
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Adobe Target 연결 {#adobe-target-connection}

## 개요 {#overview}

Adobe Target은 웹 사이트, 모바일 앱 등에서 모든 인바운드 고객 상호 작용에 실시간 AI 기반의 개인화 및 실험 기능을 제공하는 애플리케이션입니다.

Adobe Target은 Adobe Experience Platform의 개인화 연결입니다.

## 전제 조건 {#prerequisites}

이 통합은 [Adobe Experience Platform Web SDK](../../../edge/home.md). 이 대상을 사용하려면 이 SDK를 사용해야 합니다.

## 내보내기 유형 {#export-type}

**프로필 요청** - Adobe Target 대상에 매핑된 모든 세그먼트를 단일 프로필에 대해 요청하고 있습니다.

## 사용 사례 {#use-cases}

**홈 페이지 배너 개인화**

홈 대여 및 판매 회사는 Adobe Experience Platform의 고객 세그먼트 자격에 따라 배너를 사용하여 홈 페이지를 개인화하려고 합니다. 회사는 개인화된 경험을 제공해야 하는 대상을 선택하고, Target 오퍼에 대한 타깃팅 기준으로 Adobe Target에 보낼 수 있습니다.

## 대상에 연결 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="데이터 스트림 ID 기본 정보"
>abstract="이 옵션은 페이지에 대한 응답에 세그먼트를 포함할 데이터 수집 데이터 스트림을 결정합니다. 드롭다운 메뉴에는 대상 구성이 활성화된 데이터 세트만 표시됩니다. 대상을 구성하려면 먼저 데이터 스트림을 구성해야 합니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="데이터 스트림을 구성하는 방법을 알아봅니다."

>[!IMPORTANT]
>
>만들기 전 [!DNL Adobe Target] connection에 대한 안내서를 읽어 보는 것이 좋습니다 [동일한 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성](../../ui/configure-personalization-destinations.md). 이 안내서에서는 여러 Experience Platform 구성 요소에서 동일한 페이지 및 다음 페이지 개인화 사용 사례에 필요한 구성 단계를 안내합니다.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

Adobe Experience Platform은 회사의 Adobe Target 인스턴스에 자동으로 연결됩니다. 인증이 필요하지 않습니다.

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **이름**: 이 대상의 기본 이름을 입력합니다.
* **설명**: 대상에 대한 설명을 입력합니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
* **데이터 스트림 ID**: 이에 따라 페이지에 대한 응답에 세그먼트를 포함할 데이터 수집 데이터 스트림을 결정합니다. 드롭다운 메뉴에는 대상 구성이 활성화된 데이터 세트만 표시됩니다. 자세한 내용은 [데이터 스트림 구성](../../../edge/fundamentals/datastreams.md) 자세한 내용

## 세그먼트를 이 대상에 활성화 {#activate}

읽기 [프로필 요청 대상에 프로필 및 세그먼트 활성화](../../ui/activate-profile-request-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 내보낸 데이터 {#exported-data}

Adobe Target은 Adobe Experience Platform Edge Network에서 프로필 데이터를 읽으므로 데이터를 내보내지 않습니다.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 읽기 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
