---
title: Mixpanel Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Mixpanel을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# [!DNL Mixpanel]

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 분석 애플리케이션에서 데이터를 수집하는 기능을 지원합니다. 분석 공급자에 대한 지원에는 [!DNL Mixpanel]이(가) 포함됩니다.

[[!DNL Mixpanel]](https://www.mixpanel.com)은(는) 사용자가 디지털 제품과 상호 작용하는 방식에 대한 데이터를 캡처할 수 있는 제품 분석 도구입니다. Mixpanel을 사용하면 몇 번의 클릭만으로 데이터를 쿼리하고 시각화할 수 있는 간단한 대화형 보고서로 이 제품 데이터를 분석할 수 있습니다.

소스는 [Mixpanel 이벤트 내보내기 API > 다운로드](https://developer.mixpanel.com/reference/raw-event-export)를 활용하여 [!DNL Mixpanel] 내에서 수신 및 저장되는 이벤트 데이터와 모든 이벤트 속성(`distinct_id` 포함) 및 이벤트가 Experience Platform으로 전송된 정확한 타임스탬프를 다운로드합니다. Mixpanel은 인증 메커니즘으로 전달자 토큰을 사용하여 Mixpanel 이벤트 내보내기 API와 통신합니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

## [!DNL Mixpanel] 계정 인증

이 섹션에서는 계정을 인증하고 [!DNL Mixpanel] 데이터를 플랫폼으로 가져오기 위해 완료해야 하는 필수 조건 단계에 대해 설명합니다.

[!DNL Mixpanel] 원본 연결 및 데이터 흐름을 만들려면 먼저 올바른 [!DNL Mixpanel] 계정이 있어야 합니다. 유효한 [!DNL Mixpanel] 계정이 없는 경우 [Mixpanel 등록](https://mixpanel.com/register/) 페이지에서 계정을 만드십시오.

[!DNL Mixpanel] 계정을 만들었으면 [!DNL Mixpanel] UI의 [!DNL Project Seettings] 페이지에서 [!DNL Project Details] 탭으로 이동하여 프로젝트 ID를 검색하고 시간대를 구성합니다.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

다음으로, [!DNL Mixpanel] UI의 [!DNL Project Settings] 페이지에서 [!DNL Service Accounts] 탭으로 이동하여 서비스 계정 자격 증명을 검색합니다.

>[!TIP]
>
>가장 좋은 방법은 [만료되지 않는](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration) 서비스 계정을 선택하십시오.

![Mixpanel 서비스 계정](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

마지막으로 [!DNL Mixpanel Event Export API]에 필요한 플랫폼 [스키마](../../../xdm/schema/composition.md)을(를) 만듭니다. 스키마에 필요한 매핑에 대한 자세한 내용은 [UI에서  [!DNL Mixpanel] 소스 연결 만들기](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources)에 대한 안내서를 참조하십시오.

![스키마 만들기](../../images/tutorials/create/mixpanel-export-events/schema.png)

## API를 사용하여 [!DNL Mixpanel]을(를) 플랫폼에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Mixpanel]을(를) 플랫폼에 연결하는 방법에 대한 정보를 제공합니다.

* [흐름 서비스 API를 사용하여  [!DNL Mixpanel] 에 대한 소스 연결 및 데이터 흐름을 만듭니다.](../../tutorials/api/create/analytics/mixpanel.md)

## UI를 사용하여 [!DNL Mixpanel]을(를) 플랫폼에 연결

* [UI에서  [!DNL Mixpanel] 소스 연결 만들기](../../tutorials/ui/create/analytics/mixpanel.md)
* [UI에서 고객 성공 소스 연결에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/analytics.md)
