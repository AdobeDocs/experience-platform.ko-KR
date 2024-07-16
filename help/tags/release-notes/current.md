---
title: 태그 및 이벤트 전달에 대한 릴리스 노트
description: Adobe Experience Platform의 태그 및 이벤트 게재에 대한 최신 릴리스 정보입니다.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 7%

---

# 태그 및 이벤트 전달에 대한 릴리스 노트

>[!IMPORTANT]
>
>태그 및 이벤트 전달 릴리스 정보를 앞으로 이동해도 이 페이지에는 더 이상 제공되지 않습니다. 자세한 태그 및 이벤트 전달 업데이트는 최신 [Adobe Experience Platform 릴리스 노트](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection)를 참조하십시오.

## 2023년 4월 26일

* **OAuth JWT 암호**: [OAuth JWT 암호](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html)을(를) 통해 고객은 Adobe 및 Google 서비스 토큰을 사용하여 이벤트 전달에서 서버 간 상호 작용을 지원할 수 있습니다.

다음 새 확장이 릴리스되었습니다.

* **[!DNL Pinterest Conversions API]확장**: [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 이벤트 전달 확장을 사용하면 Adobe Experience Platform Edge Network에서 캡처한 데이터를 활용하고 [!DNL Pinterest Conversions API]을(를) 사용하여 서버측 이벤트 형식으로 [!DNL Pinterest]에 보낼 수 있습니다.

## 2023년 3월 29일

**빠른 시작 워크플로(Beta)**

데이터 수집 홈 화면의 “시작하기” 아래에 있는 새로운 빠른 시작 워크플로에 액세스할 수 있습니다! 이제 고객이 공용 Beta으로 다음 워크플로우를 사용할 수 있습니다.
* **[메타 전환 API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: 이벤트 전달 고객은 몇 가지 간단한 단계만 거치면 광고 전환을 위해 서버측에서 메타로 이벤트 데이터를 빠르게 수집하고 전달할 수 있습니다.
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**: 고객은 몇 가지 간단한 단계만 거치면 Mobile SDK를 빠르게 구현하고 기본 모바일 이벤트의 유효성을 검사할 수 있습니다.

새로운 확장이 릴리스되었습니다.

* **[!DNL Braze]이벤트 전달 확장**: [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 이벤트 전달 확장을 사용하면 Adobe Experience Platform Edge Network에서 캡처한 데이터를 활용하고 [!DNL Braze] 사용자 추적 API를 사용하여 서버측 이벤트 형식으로 [!DNL Braze]에 보낼 수 있습니다.
* **[Epsilon Events API] 이벤트 전달 확장**: [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 확장을 사용하면 이벤트 전달을 사용하여 Adobe Experience Platform Edge Network에서 이벤트 정보를 캡처하고 [!DNL Epsilon] 이벤트 API를 사용하여 [!DNL Epsilon]에 보낼 수 있습니다.
* **[!DNL Mixpanel]이벤트 전달 확장**: [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 확장을 사용하면 이벤트 전달을 활용하여 Adobe Experience Platform Edge Network에서 이벤트 정보를 캡처하고 이벤트 추적 API를 사용하여 [!DNL Mixpanel]에 전송할 수 있습니다.

## 2023년 1월 25일

* **새 홈 화면**: 생산성을 간소화하는 유용한 온보딩 정보와 링크를 포함하도록 데이터 수집 UI의 홈 페이지가 업데이트되었습니다. 여기에는 다음 항목이 포함되어 있습니다.
   1. 시작을 위한 설명서 및 권장 워크플로
   1. 최근 속성, 규칙 및 데이터 요소
   1. 자주 사용하는 확장 기능
   1. 빠른 설치 기능을 통한 새로운 확장 기능 업데이트
* **이벤트 전달을 사용하여 [!DNL Google Ads]에 데이터 보내기**: 이제 이벤트 전달을 위해 [[!DNL Google Ads Enhanced Conversions] API 확장](../extensions/server/google-ads-enhanced-conversions/overview.md)을(를) 사용하여 [Google Oauth 2 비밀](../ui/event-forwarding/secrets.md#google-oauth2)과(와) 결합하여 서버측 데이터를 [!DNL Google Ads]에 실시간으로 안전하게 보낼 수 있습니다.

## 2022년 11월 23일 목요일

* 이벤트 전달을 위한 **[!DNL AWS]확장**: 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Amazon Web Services]([!DNL AWS])에게 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL AWS] 확장 개요](../../tags/extensions/server/aws/overview.md)를 참조하십시오.
* 이벤트 전달을 위한 **[!DNL Google Ads Enhanced Conversions]확장**: 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 변환 데이터를 [!DNL Google Ads]에 보낼 수 있습니다. 자세한 내용은 [[!DNL Google Ads Enhanced Conversions] 확장 개요](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)를 참조하십시오.
* 이벤트 전달을 위한 **[!DNL Microsoft Azure]확장**: 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Microsoft Azure]에 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL Microsoft Azure] 확장 개요](../../tags/extensions/server/azure/overview.md)를 참조하십시오.

## 2022년 10월 26일

* **데이터스트림에 대한 중요한 데이터 처리**: 이제 데이터스트림은 여러 플랫폼 기술을 활용하여 HIPAA(Health Insurance Portability and Accountability Act)와 같은 규정에 따라 중요한 데이터를 적절히 처리합니다. 자세한 내용은 [데이터 스트림에서 중요 데이터 처리](../../datastreams/overview.md#sensitive)에 대한 섹션을 참조하십시오.
* 이벤트 전달을 위한 **[!DNL Splunk]확장**: 이제 [이벤트 전달](../ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Splunk]에 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL Splunk] 확장 개요](../extensions/server/splunk/overview.md)를 참조하십시오.
* 이벤트 전달을 위한 **[!DNL Zendesk]확장**: 이제 [이벤트 전달](../ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Zendesk]에 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL Zendesk] 확장 개요](../extensions/server/zendesk/overview.md)를 참조하십시오.

## 2022년 9월 28일

* **Adobe Experience Platform 왼쪽 탐색 통합**: 이전에 데이터 수집 UI에만 있던 모든 기능(태그 및 이벤트 전달 포함)을 이제 Experience Platform UI의 왼쪽 탐색(**[!UICONTROL 데이터 수집]** 범주 아래)을 통해 사용할 수 있습니다. 이렇게 하면 Platform에서 데이터 수집 기능으로 작업할 때 UI 간을 전환할 필요가 없습니다.
* **태그 및 이벤트 전달의 사용자 속성**: 태그 및 이벤트 전달에서 사용 가능한 속성을 나열할 때 이제 나열된 각 속성이 마지막으로 업데이트된 시간과 업데이트 대상이 표시됩니다.
* 이벤트 전달을 위한 **[[!DNL Snap Conversions API] 확장](https://exchange.adobe.com/apps/ec/108550)**: 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Snapchat Conversions API]에 데이터를 보낼 수 있습니다. API 인증 및 사용 방법에 대한 자세한 내용은 [[!DNL Snapchat Marketing API] 설명서](https://marketingapi.snapchat.com/docs/conversion.html)를 참조하세요.

## 2022년 7월 27일

* 이제 Adobe Experience Platform 데이터 수집용 카드 아래에 있는 Adobe Admin Console을 통해 태그 및 이벤트 전달 기능에 대한 액세스를 관리합니다. 자세한 내용은 [데이터 수집 권한](../../collection/permissions.md)에 대한 안내서를 참조하십시오.
* Internet Explorer 10 및 11에 대한 지원은 [더 이상 사용되지 않음](../ie-deprecation.md)입니다.

## 2022년 6월 22일

새로운 확장이 릴리스되었습니다.

* [Google 데이터 레이어 태그 확장](../extensions/client/google-data-layer/overview.md): 태그 구현에서 Google 데이터 레이어를 사용할 수 있습니다.
* [Google 광고 향상된 전환 이벤트 전달 확장](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Google 광고 전환을 실시간으로 개선할 수 있습니다.
* [Mailchimp 이벤트 전달 확장](../extensions/server/mailchimp/overview.md): Mailchimp 마케팅 캠페인, 여정 또는 트랜잭션에 대한 이메일을 트리거할 수 있는 Mailchimp 마케팅 API에 이벤트를 보냅니다.