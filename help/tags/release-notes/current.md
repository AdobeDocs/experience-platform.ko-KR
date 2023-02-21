---
title: 태그 및 이벤트 전달을 위한 릴리스 노트
description: Adobe Experience Platform의 태그 및 이벤트 전달에 대한 최신 릴리스 정보입니다.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 2b11fb87523c777d5c2d855e97a4af78a8483abe
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 5%

---

# 태그 및 이벤트 전달에 대한 릴리스 노트

## 2023년 1월 25일

* **새 홈 화면**: 데이터 수집 UI의 홈 페이지가 생산성을 간소화하기 위해 유용한 온보딩 정보 및 링크를 포함하도록 업데이트되었습니다. 여기에는 다음 항목이 포함되어 있습니다.
   1. 시작하는 설명서 및 권장 워크플로우
   1. 최근 속성, 규칙 및 데이터 요소
   1. 인기 있는 확장
   1. 빠른 설치 기능으로 새로운 확장 업데이트
* **에 데이터 보내기 [!DNL Google Ads] 이벤트 전달 사용**: 이제 를 사용할 수 있습니다 [[!DNL Google Ads Enhanced Conversions] API 확장](../extensions/server/google-ads-enhanced-conversions/overview.md) 이벤트 전달에 대해 다음을 결합합니다. [Google Oauth 2 비밀](../ui/event-forwarding/secrets.md#google-oauth2)으로 데이터를 안전하게 [!DNL Google Ads] 실시간으로

## 2022년 11월 23일

* **[!DNL AWS]이벤트 전달을 위한 확장**: 이제 데이터를에 보낼 수 있습니다 [!DNL Amazon Web Services] ([!DNL AWS]) 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장. 자세한 내용은 [[!DNL AWS] 확장 개요](../../tags/extensions/server/aws/overview.md) 추가 정보.
* **[!DNL Google Ads Enhanced Conversions]이벤트 전달을 위한 확장**: 이제 변환 데이터를에 보낼 수 있습니다 [!DNL Google Ads] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장. 자세한 내용은 [[!DNL Google Ads Enhanced Conversions] 확장 개요](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 추가 정보.
* **[!DNL Microsoft Azure]이벤트 전달을 위한 확장**: 이제 데이터를에 보낼 수 있습니다 [!DNL Microsoft Azure] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장. 자세한 내용은 [[!DNL Microsoft Azure] 확장 개요](../../tags/extensions/server/azure/overview.md) 추가 정보.

## 2022년 10월 26일

* **데이터 세트에 대한 중요 데이터 처리**: 이제 데이터 저장소는 여러 플랫폼 기술을 활용하여 HIPAA(Health Insurance Portability and Accountability Act)와 같은 규정에 따라 적용되는 중요한 데이터를 적절하게 처리합니다. 의 섹션을 참조하십시오. [datstreams의 sendstive 데이터 처리](../../edge/datastreams/overview.md#sensitive) 추가 정보.
* **[!DNL Splunk]이벤트 전달을 위한 확장**: 이제 데이터를에 보낼 수 있습니다 [!DNL Splunk] 사용 [이벤트 전달](../ui/event-forwarding/overview.md) 확장. 자세한 내용은 [[!DNL Splunk] 확장 개요](../extensions/server/splunk/overview.md) 추가 정보.
* **[!DNL Zendesk]이벤트 전달을 위한 확장**: 이제 데이터를에 보낼 수 있습니다 [!DNL Zendesk] 사용 [이벤트 전달](../ui/event-forwarding/overview.md) 확장. 자세한 내용은 [[!DNL Zendesk] 확장 개요](../extensions/server/zendesk/overview.md) 추가 정보.

## 2022년 9월 28일

* **Adobe Experience Platform 왼쪽 탐색 통합**: 데이터 수집 UI에 대해 이전에 배타적이었던 모든 기능(태그 및 이벤트 전달 포함)은 이제 Experience Platform UI의 카테고리 아래에 있는 왼쪽 탐색 기능을 통해 사용할 수도 있습니다 **[!UICONTROL 데이터 수집]**. 따라서 Platform에서 데이터 수집 기능을 사용할 때 UI 간을 전환할 필요가 없습니다.
* **태그 및 이벤트 전달의 사용자 속성**: 태그 및 이벤트 전달에서 사용 가능한 속성을 나열할 때 이제 나열된 각 속성에 마지막으로 업데이트된 시간과 해당 속성의 소유자가 표시됩니다.
* **[[!DNL Snap Conversions API] 확장](https://exchange.adobe.com/apps/ec/108550) 이벤트 전달을 위한**: 이제 데이터를 [!DNL Snapchat Conversions API] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장. API를 인증하고 사용하는 방법에 대한 자세한 내용은 [[!DNL Snapchat Marketing API] 설명서](https://marketingapi.snapchat.com/docs/conversion.html).

## 2022년 7월 27일

* 태그 및 이벤트 전달 기능에 대한 액세스는 이제 Adobe Experience Platform 데이터 수집용 카드에서 Adobe Admin Console을 통해 관리됩니다. 다음 안내서를 참조하십시오. [데이터 수집 권한](../../collection/permissions.md) 추가 정보.
* Internet Explorer 10 및 11에 대한 지원이 제공되었습니다 [사용되지 않음](../ie-deprecation.md).

## 2022년 6월 22일

새로운 확장이 릴리스되었습니다.

* [Google 데이터 레이어 태그 확장](../extensions/client/google-data-layer/overview.md): 태그 구현에서 Google 데이터 계층을 사용할 수 있습니다.
* [Google 광고 향상된 전환 이벤트 전달 확장](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Google 광고 전환을 실시간으로 향상시킬 수 있습니다.
* [메일 침팬지 이벤트 전달 확장](../extensions/server/mailchimp/overview.md): Mailchimp 마케팅 캠페인, 여정 또는 트랜잭션에 대한 이메일을 트리거할 수 있는 Mailchimp 마케팅 API에 이벤트를 보냅니다.