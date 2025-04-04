---
title: 태그 및 이벤트 전달 릴리스 정보
description: Adobe Experience Platform의 태그 및 이벤트 전달에 대한 최신 릴리스 정보입니다.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 93%

---

# 태그 및 이벤트 전달 릴리스 정보

>[!IMPORTANT]
>
>앞으로 태그 및 이벤트 전달 릴리스 정보는 더 이상 이 페이지에 제공되지 않습니다. 태그 및 이벤트 전달 업데이트에 대한 자세한 내용은 [Adobe Experience Platform 릴리스 정보](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection)를 참조하십시오.

## 2023년 4월 26일

* **OAuth JWT Secret**: 고객은 [OAuth JWT Secret](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html)을 사용하여 Adobe 및 Google Service 토큰으로 이벤트 전달에서 서버 간 상호 작용을 지원할 수 있습니다.

새로 출시된 확장 기능은 다음과 같습니다.

* **[!DNL Pinterest Conversions API]extension**: [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 이벤트 전달 확장 기능을 사용하면 Adobe Experience Platform Edge Network에서 캡처된 데이터를 활용하여 [!DNL Pinterest Conversions API]를 통해 서버측 이벤트의 형태로 [!DNL Pinterest]로 전송할 수 있습니다

## 2023년 3월 29일

**빠른 시작 워크플로 (Beta)**

데이터 수집 홈 화면의 “시작하기” 아래에 있는 새로운 빠른 시작 워크플로에 액세스할 수 있습니다. 다음 워크플로는 현재 공개 Beta 버전으로 고객에게 제공됩니다.
* **[Meta Conversions API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: 이벤트 전달 고객은 Meta Conversions API를 위한 이벤트 데이터를 신속하게 수집하여 단 몇 번의 간단한 단계로 광고 전환을 위해 서버측에서 Meta로 전달할 수 있습니다.
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**: 고객은 몇 번의 간단한 단계로 Mobile SDK를 신속하게 구현하고 기본 모바일 이벤트의 유효성을 검사할 수 있습니다.

새로운 확장 기능이 출시되었습니다.

* **[!DNL Braze]이벤트 전달 확장 기능**: [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 이벤트 전달 확장 기능을 사용하면 Adobe Experience Platform Edge Network에서 캡처된 데이터를 활용하여 [!DNL Braze] 사용자 추적 API를 통해 서버측 이벤트의 형태로 [!DNL Braze]로 전송할 수 있습니다
* **[Epsilon 이벤트 API] 이벤트 전달 확장 기능**: [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 확장 기능을 사용하면 이벤트 전달을 통해 Adobe Experience Platform Edge Network의 이벤트 정보를 캡처하고 [!DNL Epsilon] 이벤트 API를 통해 [!DNL Epsilon]으로 전송할 수 있습니다
* **[!DNL Mixpanel]이벤트 전달 확장 기능**: [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 확장 기능을 사용하면 이벤트 전달을 통해 Adobe Experience Platform Edge Network의 이벤트 정보를 캡처하고 추적 이벤트 API를 통해 [!DNL Mixpanel]로 전송할 수 있습니다.

## 2023년 1월 25일

* **새로운 홈 화면**: 데이터 수집 UI의 홈 페이지가 업데이트되어 유용한 온보딩 정보와 생산성 간소화를 위한 링크가 포함되었습니다. 여기에는 다음 항목이 포함되어 있습니다.
   1. 시작을 위한 설명서 및 권장 워크플로
   1. 최근 속성, 규칙 및 데이터 요소
   1. 자주 사용하는 확장 기능
   1. 빠른 설치 기능을 통한 새로운 확장 기능 업데이트
* **이벤트 전달을 통해 데이터를 [!DNL Google Ads]로 전송**: 이제 [Google Oauth 2 Secret](../ui/event-forwarding/secrets.md#google-oauth2)과 함께 이벤트 전달을 위한 [[!DNL Google Ads Enhanced Conversions] API 확장 기능](../extensions/server/google-ads-enhanced-conversions/overview.md)을 사용하여 서버측 데이터를 [!DNL Google Ads]에 실시간으로 안전하게 전송할 수 있습니다.

## 2022년 11월 23일

* **[!DNL AWS]확장 기능을 통한 이벤트 전달**: 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장 기능을 통해 데이터를 [!DNL Amazon Web Services] ([!DNL AWS])로 전송할 수 있습니다. 자세한 내용은 [[!DNL AWS] 확장 기능 개요](../../tags/extensions/server/aws/overview.md)를 참조하십시오.
* **[!DNL Google Ads Enhanced Conversions]확장 기능을 통한 이벤트 전달**: 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장 기능을 통해 전환 데이터를 [!DNL Google Ads]로 전송할 수 있습니다. 자세한 내용은 [[!DNL Google Ads Enhanced Conversions] 확장 기능 개요](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)를 참조하십시오.
* **[!DNL Microsoft Azure]확장 기능을 통한 이벤트 전달**: 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장 기능을 통해 데이터를 [!DNL Microsoft Azure]로 전송할 수 있습니다. 자세한 내용은 [[!DNL Microsoft Azure] 확장 기능 개요](../../tags/extensions/server/azure/overview.md)를 참조하십시오.

## 2022년 10월 26일

* **데이터 스트림에 대한 중요한 데이터 처리**: 이제 데이터 스트림은 여러 Experience Platform 기술을 활용하여 HIPAA(Health Insurance Portability and Accountability Act)와 같은 규정에 따라 중요한 데이터를 적절히 처리합니다. 자세한 내용은 [데이터스트림의 민감한 데이터 처리](../../datastreams/overview.md#sensitive)에 대한 섹션을 참조하십시오.
* **[!DNL Splunk]확장 기능을 통한 이벤트 전달**: 이제 [이벤트 전달](../ui/event-forwarding/overview.md) 확장 기능을 통해 데이터를 [!DNL Splunk]로 전송할 수 있습니다. 자세한 내용은 [[!DNL Splunk] 확장 기능 개요](../extensions/server/splunk/overview.md)를 참조하십시오.
* **[!DNL Zendesk]확장 기능을 통한 이벤트 전달**: 이제 [이벤트 전달](../ui/event-forwarding/overview.md) 확장 기능을 통해 데이터를 [!DNL Zendesk]로 전송할 수 있습니다. 자세한 내용은 [[!DNL Zendesk] 확장 기능 개요](../extensions/server/zendesk/overview.md)를 참조하십시오.

## 2022년 9월 28일

* **Adobe Experience Platform 왼쪽 탐색 영역 통합**: 이전에 데이터 수집 UI에서만 사용할 수 있었던 모든 기능(태그 및 이벤트 전달 포함)을 이제 Experience Platform UI의 왼쪽 탐색 영역의 **[!UICONTROL 데이터 수집]** 범주 아래에서도 사용할 수 있습니다. 이렇게 하면 Experience Platform에서 데이터 수집 기능을 사용할 때 UI 간을 전환할 필요가 없습니다.
* **태그 및 이벤트 전달에서의 사용자 속성**: 태그 및 이벤트 전달에서 사용 가능한 속성을 나열할 때, 나열된 각 속성에는 마지막 업데이트 날짜와 업데이트한 사용자가 표시됩니다.
* **[[!DNL Snap Conversions API] 확장 기능](https://exchange.adobe.com/apps/ec/108550)을 통한 이벤트 전달**: 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장 기능을 통해 데이터를 [!DNL Snapchat Conversions API]로 전송할 수 있습니다. API 인증 및 사용 방법에 대한 자세한 내용은 이 [[!DNL Snapchat Marketing API] 설명서](https://marketingapi.snapchat.com/docs/conversion.html)를 참조하십시오.

## 2022년 7월 27일

* 태그 및 이벤트 전달 기능에 대한 액세스는 이제 Adobe Experience Platform 데이터 수집 카드 아래 Adobe Admin Console을 통해 관리됩니다. 자세한 내용은 [데이터 수집 권한](../../collection/permissions.md)에 대한 안내서를 참조하십시오.
* Internet Explorer 10 및 11은 [더 이상 지원되지 않습니다](../ie-deprecation.md).

## 2022년 6월 22일

새로운 확장 기능이 출시되었습니다.

* [Google 데이터 레이어 태그 확장 기능](../extensions/client/google-data-layer/overview.md): 태그 구현에서 Google 데이터 레이어를 사용할 수 있습니다.
* [Google Ads 향상된 전환 이벤트 전달 확장 기능](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): 실시간으로 Google Ads 전환을 개선할 수 있습니다.
* [Mailchimp 이벤트 전달 확장 기능](../extensions/server/mailchimp/overview.md): Mailchimp 마케팅 캠페인, 여정 또는 거래를 위한 이메일을 트리거할 수 있는 이벤트를 Mailchimp 마케팅 API로 전송합니다.