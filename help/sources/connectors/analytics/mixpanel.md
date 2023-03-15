---
keywords: Experience Platform;홈;인기 있는 주제;
title: (베타) Mixpanel 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Mixpanel을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: e44f6d5bb2fd891a3e3b3c5e4aed68e8d4687b53
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (베타) [!DNL Mixpanel]

>[!NOTE]
>
>다음 [!DNL Mixpanel] 소스는 베타 버전입니다. 다음을 참조하십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 분석 애플리케이션에서 데이터를 수집하는 기능을 지원합니다. Analytics 공급자에 대한 지원은 다음과 같습니다 [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) 는 사용자가 디지털 제품과 상호 작용하는 방법에 대한 데이터를 캡처할 수 있도록 해주는 제품 분석 도구입니다. Mixpanel을 사용하면 몇 번의 클릭만으로 데이터를 쿼리하고 시각화할 수 있는 간단한 대화형 보고서로 이 제품 데이터를 분석할 수 있습니다.

소스는 [Mixpanel 이벤트 내보내기 API > 다운로드](https://developer.mixpanel.com/reference/raw-event-export) 내에서 수신 및 저장되는 이벤트 데이터를 다운로드하려면 [!DNL Mixpanel], 모든 이벤트 속성(포함) `distinct_id`) 이벤트를 Experience Platform에 전송한 정확한 타임스탬프입니다. Mixpanel은 인증 메커니즘으로 전달자 토큰을 사용하여 Mixpanel 이벤트 내보내기 API와 통신합니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 다음을 참조하십시오. [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지 를 참조하십시오.

## 인증 [!DNL Mixpanel] account

이 섹션에서는 계정을 인증하고 을(를) 가져오기 위해 완료해야 하는 사전 요구 사항에 대해 설명합니다. [!DNL Mixpanel] 데이터를 플랫폼에 추가합니다.

를 만들려면 [!DNL Mixpanel] 소스 연결 및 데이터 흐름입니다. 먼저 유효해야 합니다. [!DNL Mixpanel] 계정입니다. 유효하지 않은 경우 [!DNL Mixpanel] 계정, 다음 참조 [Mixpanel 레지스터](https://mixpanel.com/register/) 페이지를 통해 계정을 만드십시오.

을(를) 정상적으로 생성하면 [!DNL Mixpanel] 계정, 다음으로 이동 [!DNL Project Details] 의 탭 [!DNL Project Seettings] 페이지의 [!DNL Mixpanel] 프로젝트 ID를 검색하고 시간대를 구성하는 UI입니다.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

다음으로 이동 [!DNL Service Accounts] 의 탭 [!DNL Project Settings] 페이지의 [!DNL Mixpanel] 서비스 계정 자격 증명을 검색할 UI입니다.

>[!TIP]
>
>모범 사례를 위해 다음과 같은 서비스 계정을 선택합니다. [만료되지 않음](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Mixpanel 서비스 계정](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

마지막으로 플랫폼을 만듭니다. [스키마](../../../xdm/schema/composition.md) 다음에 필요합니다. [!DNL Mixpanel Event Export API]. 스키마에 필요한 매핑에 대한 자세한 내용은 [만들기 [!DNL Mixpanel] UI의 소스 연결](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![스키마 만들기](../../images/tutorials/create/mixpanel-export-events/schema.png)

## 연결 [!DNL Mixpanel] API를 사용하여 플랫폼으로

아래 설명서는 연결 방법에 대한 정보를 제공합니다 [!DNL Mixpanel] API 또는 사용자 인터페이스를 사용하여 Platform으로

* [소스 연결 및 데이터 흐름 만들기 [!DNL Mixpanel] 흐름 서비스 API 사용](../../tutorials/api/create/analytics/mixpanel.md)

## 연결 [!DNL Mixpanel] UI를 사용하여 플랫폼에 연결

* [만들기 [!DNL Mixpanel] UI의 소스 연결](../../tutorials/ui/create/analytics/mixpanel.md)
* [UI에서 고객 성공 소스 연결에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/analytics.md)
