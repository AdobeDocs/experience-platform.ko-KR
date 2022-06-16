---
keywords: Experience Platform;홈;인기 있는 주제
title: (베타) Mixpanel 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Mixpanel을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: e7a5e20721f5826ca1f4520b4a27d261eed1e4df
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (베타) [!DNL Mixpanel]

>[!NOTE]
>
>다음 [!DNL Mixpanel] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 analytics 애플리케이션에서 데이터를 수집하도록 지원합니다. 분석 공급자를 지원하는 기능에는 다음이 포함됩니다 [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) 는 사용자가 디지털 제품과 상호 작용하는 방법에 대한 데이터를 캡처할 수 있는 제품 분석 도구입니다. Mixpanel을 사용하면 몇 번의 클릭만으로 데이터를 쿼리하고 시각화할 수 있는 간단한 대화형 보고서로 이 제품 데이터를 분석할 수 있습니다.

소스는 [Mixpanel 이벤트 내보내기 API > 다운로드](https://developer.mixpanel.com/reference/raw-event-export) 이벤트 데이터를 수신하여 [!DNL Mixpanel], 모든 이벤트 속성( `distinct_id`) 및 이벤트를 Experience Platform으로 보낸 정확한 타임스탬프. Mixpanel은 베어러 토큰을 인증 메커니즘으로 사용하여 Mixpanel 이벤트 내보내기 API와 통신합니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 인증 [!DNL Mixpanel] account

이 섹션에서는 계정을 인증하고 을(를) 가져오기 위해 완료해야 하는 필수 구성 요소에 대해 설명합니다 [!DNL Mixpanel] Platform으로 데이터를 전송할 수 있습니다.

을(를) 만들려면 [!DNL Mixpanel] 소스 연결 및 데이터 흐름을 사용하려면 먼저 유효한 [!DNL Mixpanel] 계정이 필요합니다. 유효한 [!DNL Mixpanel] 계정, [Mixpanel 레지스터](https://mixpanel.com/register/) 페이지를 클릭하여 계정을 만듭니다.

을(를) 생성했으면 [!DNL Mixpanel] account, 다음 위치로 이동합니다. [!DNL Project Details] 탭에서 다음을 수행합니다. [!DNL Project Seettings] 페이지의 [!DNL Mixpanel] 프로젝트 ID를 검색하고 시간대를 구성하는 UI.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

다음으로 이동하여 [!DNL Service Accounts] 탭에서 다음을 수행합니다. [!DNL Project Settings] 페이지의 [!DNL Mixpanel] 서비스 계정 자격 증명을 검색할 UI입니다.

>[!TIP]
>
>우수 사례를 위해 [만료 안 함](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Mixpanel 서비스 계정](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

마지막으로, 플랫폼 만들기 [스키마](../../../xdm/schema/composition.md) 에 필요합니다. [!DNL Mixpanel Event Export API]. 스키마에 필요한 매핑에 대한 자세한 내용은 [만들기 [!DNL Mixpanel] UI의 소스 연결](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![스키마 만들기](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connect [!DNL Mixpanel] API를 사용하여 플랫폼 구현

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Mixpanel] API 또는 사용자 인터페이스를 사용하여 플랫폼:

* [소스 연결 및 데이터 흐름 만들기 [!DNL Mixpanel] 흐름 서비스 API 사용](../../tutorials/api/create/analytics/mixpanel.md)

## Connect [!DNL Mixpanel] UI를 사용하여 플랫폼 구현

* [만들기 [!DNL Mixpanel] UI의 소스 연결](../../tutorials/ui/create/analytics/mixpanel.md)
* [UI에서 고객 성공 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/analytics.md)

