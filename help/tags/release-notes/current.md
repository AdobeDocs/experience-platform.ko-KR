---
title: 태그 및 이벤트 전달에 대한 릴리스 노트
description: Adobe Experience Platform의 태그 및 이벤트 게재에 대한 최신 릴리스 정보입니다.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: c7f09da40d2ea84de6f21669bdda16c0175a63c1
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 4%

---

# 태그 및 이벤트 전달에 대한 릴리스 노트

## 2023년 4월 26일

* **OAuth JWT 암호**: [OAuth JWT 암호](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) 는 고객이 Adobe 및 Google 서비스 토큰을 사용하여 이벤트 전달에서 서버 간 상호 작용을 지원할 수 있도록 합니다.

다음 새 확장이 릴리스되었습니다.

* **[!DNL Pinterest Conversions API]확장**: [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 이벤트 전달 확장을 사용하면 Adobe Experience Platform Edge Network에 캡처된 데이터를 활용하여 로 전송할 수 있습니다. [!DNL Pinterest] 를 사용하는 서버측 이벤트 형식으로 [!DNL Pinterest Conversions API].

## 2023년 3월 29일

**Quick Stark 워크플로우(베타)**

데이터 수집 홈 화면의 &quot;시작하기&quot;에서 새 빠른 시작 워크플로우에 액세스합니다! 이제 다음 워크플로를 고객이 공개 베타로 사용할 수 있습니다.
* **[메타 전환 API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start)**: 이벤트 전달 고객은 몇 가지 간단한 단계만으로 광고 전환을 위해 서버측에서 메타로 이벤트 데이터를 빠르게 수집하고 전달할 수 있습니다.
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**: 고객은 몇 가지 간단한 단계만으로 Mobile SDK를 빠르게 구현하고 기본 모바일 이벤트를 확인할 수 있습니다.

새로운 확장이 릴리스되었습니다.

* **[!DNL Braze]이벤트 전달 확장**: [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 이벤트 전달 확장을 사용하면 Adobe Experience Platform Edge Network에 캡처된 데이터를 활용하여 로 전송할 수 있습니다. [!DNL Braze] 를 사용하는 서버측 이벤트 형식으로 [!DNL Braze] 사용자 추적 API.
* **[Epsilon Events API] 이벤트 전달 확장**: [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 확장을 사용하면 이벤트 전달을 활용하여 Adobe Experience Platform Edge Network에서 이벤트 정보를 캡처하여 로 전송할 수 있습니다. [!DNL Epsilon] 사용 [!DNL Epsilon] 이벤트 API.
* **[!DNL Mixpanel]이벤트 전달 확장**: [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 확장을 사용하면 이벤트 전달을 활용하여 Adobe Experience Platform Edge Network에서 이벤트 정보를 캡처하여 로 전송할 수 있습니다. [!DNL Mixpanel] 이벤트 추적 API 사용.

## 2023년 1월 25일

* **새 홈 화면**: 데이터 수집 UI의 홈 페이지가 생산성 효율화를 위한 유용한 온보딩 정보 및 링크를 포함하도록 업데이트되었습니다. 여기에는 다음 항목이 포함되어 있습니다.
   1. 시작하기 위한 설명서 및 권장 워크플로우
   1. 최근 속성, 규칙 및 데이터 요소
   1. 인기 있는 확장
   1. 빠른 설치 기능으로 새로운 확장 업데이트
* **데이터 보내기 대상 [!DNL Google Ads] 이벤트 전달 사용**: 이제 를 사용할 수 있습니다. [[!DNL Google Ads Enhanced Conversions] API 확장](../extensions/server/google-ads-enhanced-conversions/overview.md) 이벤트 전달용, 결합 [Google Oauth 2 비밀](../ui/event-forwarding/secrets.md#google-oauth2): 서버측 데이터를 로 안전하게 전송합니다. [!DNL Google Ads] 실시간으로.

## 2022년 11월 23일

* **[!DNL AWS]이벤트 전달을 위한 확장**: 이제 로 데이터를 전송할 수 있습니다. [!DNL Amazon Web Services] ([!DNL AWS]) 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장명. 다음을 참조하십시오. [[!DNL AWS] 확장 개요](../../tags/extensions/server/aws/overview.md) 추가 정보.
* **[!DNL Google Ads Enhanced Conversions]이벤트 전달을 위한 확장**: 이제 변환 데이터를 로 보낼 수 있습니다. [!DNL Google Ads] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장명. 다음을 참조하십시오. [[!DNL Google Ads Enhanced Conversions] 확장 개요](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 추가 정보.
* **[!DNL Microsoft Azure]이벤트 전달을 위한 확장**: 이제 로 데이터를 전송할 수 있습니다. [!DNL Microsoft Azure] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장명. 다음을 참조하십시오. [[!DNL Microsoft Azure] 확장 개요](../../tags/extensions/server/azure/overview.md) 추가 정보.

## 2022년 10월 26일

* **데이터스트림에 대한 중요한 데이터 처리**: 이제 데이터 스트림은 여러 플랫폼 기술을 활용하여 HIPAA(Health Insurance Portability and Accountability Act)와 같은 규정에 따라 중요한 데이터를 적절하게 처리합니다. 의 섹션을 참조하십시오. [데이터 스트림에서 중요 데이터 처리](../../edge/datastreams/overview.md#sensitive) 추가 정보.
* **[!DNL Splunk]이벤트 전달을 위한 확장**: 이제 로 데이터를 전송할 수 있습니다. [!DNL Splunk] 사용 [이벤트 전달](../ui/event-forwarding/overview.md) 확장명. 다음을 참조하십시오. [[!DNL Splunk] 확장 개요](../extensions/server/splunk/overview.md) 추가 정보.
* **[!DNL Zendesk]이벤트 전달을 위한 확장**: 이제 로 데이터를 전송할 수 있습니다. [!DNL Zendesk] 사용 [이벤트 전달](../ui/event-forwarding/overview.md) 확장명. 다음을 참조하십시오. [[!DNL Zendesk] 확장 개요](../extensions/server/zendesk/overview.md) 추가 정보.

## 2022년 9월 28일

* **Adobe Experience Platform 왼쪽 탐색 통합**: 이전에 데이터 수집 UI에만 있던 모든 기능(태그 및 이벤트 전달 포함)을 이제 Experience Platform UI의 범주 아래에 있는 왼쪽 탐색을 통해 사용할 수 있습니다 **[!UICONTROL 데이터 수집]**. 이렇게 하면 Platform에서 데이터 수집 기능으로 작업할 때 UI 간을 전환할 필요가 없습니다.
* **태그 및 이벤트 전달의 사용자 속성**: 태그 및 이벤트 전달에서 사용할 수 있는 속성을 나열할 때 이제 나열된 각 속성이 마지막으로 업데이트된 시간과 업데이트한 사람을 표시합니다.
* **[[!DNL Snap Conversions API] 확장](https://exchange.adobe.com/apps/ec/108550) 이벤트 전달용**: 이제 로 데이터를 전송할 수 있습니다. [!DNL Snapchat Conversions API] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장명. API 인증 및 사용 방법에 대한 자세한 내용은 다음을 참조하십시오. [[!DNL Snapchat Marketing API] 설명서](https://marketingapi.snapchat.com/docs/conversion.html).

## 2022년 7월 27일

* 이제 Adobe Experience Platform 데이터 수집용 카드 아래에 있는 Adobe Admin Console을 통해 태그 및 이벤트 전달 기능에 대한 액세스를 관리합니다. 다음 안내서를 참조하십시오 [데이터 수집 권한](../../collection/permissions.md) 추가 정보.
* Internet Explorer 10 및 11에 대한 지원은 다음과 같습니다 [더 이상 사용되지 않음](../ie-deprecation.md).

## 2022년 6월 22일

새로운 확장이 릴리스되었습니다.

* [Google 데이터 레이어 태그 확장](../extensions/client/google-data-layer/overview.md): 태그 구현에서 Google 데이터 레이어를 사용할 수 있습니다.
* [Google Ads Enhanced Conversion 이벤트 전달 확장](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Google 광고 전환을 실시간으로 향상시킬 수 있습니다.
* [Mailchimp 이벤트 전달 확장](../extensions/server/mailchimp/overview.md): Mailchimp 마케팅 캠페인, 여정 또는 트랜잭션에 대한 이메일을 트리거할 수 있는 이벤트를 Mailchimp Marketing API에 보냅니다.