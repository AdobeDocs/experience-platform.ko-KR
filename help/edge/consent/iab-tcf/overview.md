---
title: IAB Transparency & Consent Framework 2.0 개요
seo-title: Interactive Advertising Bureau Transparency & Consent Framework 2.0에서 Adobe Experience Platform 웹 SDK 동의 환경 설정 지원
description: Experience Platform 웹 SDK를 사용하여 IAB TCF 2.0 동의 환경 설정을 지원하는 방법을 알아봅니다.
seo-description: Experience Platform 웹 SDK를 사용하여 IAB TCF 2.0 동의 환경 설정을 지원하는 방법을 알아봅니다.
keywords: consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---


# IAB Transparency &amp; Consent Framework 2.0 개요

Adobe Experience Platform 웹 SDK(AEP 웹 SDK)는 Interactive Advertising Bureau Transparency &amp; Consent Framework, 버전 2.0(IAB TCF 2.0)을 지원합니다. 이 안내서는 실시간 고객 데이터 플랫폼, Audience Manager, 경험 이벤트, Adobe Analytics 및 경험 에지(Experience Edge)와 통합된 AEP 웹 SDK를 통해 IAB TCF 2.0을 지원하기 위한 요구 사항을 보여줍니다.

또한 다음 가이드는 Adobe Experience Platform Launch과 IAB TCF 2.0을 통합하는 방법을 학습하는 데 도움을 줍니다.

- [Adobe Experience Platform Launch](./with-launch.md)
- [Adobe Experience Platform Launch 없이](./without-launch.md)

## 시작하기

IAB TCF 2.0과 함께 AEP 웹 SDK를 구현하려면 XDM(Experience Data Model) 및 경험 이벤트에 대한 충분한 지식이 있어야 합니다. 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(Experience Data Model) 시스템 개요](../../../xdm/home.md):표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. [!DNL Experience Data Model (XDM)]Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하려는 노력의 일환입니다.

## 실시간 고객 데이터 플랫폼 통합

Adobe Experience Platform 기반의 실시간 CDP(Customer Data Platform)를 통해 다양한 엔터프라이즈 소스에서 알려진 익명의 데이터를 취합할 수 있습니다. 이를 통해 모든 채널과 디바이스에서 개인화된 경험을 실시간으로 제공하는 데 사용할 수 있는 고객 프로파일을 만들 수 있습니다. AEP Web SDK를 통해 동의 데이터를 실시간 CDP에 전송하려면 다음을 수행해야 합니다.

- 프로필 개인 정보 혼합에서 사용할 수 있도록 설정된 [!DNL XDM Individual Profile] 클래스를 기반으로 하는 데이터 세트 [!DNL Real-time Customer Profile]입니다.
- 실시간 CDP를 사용하여 에지 구성을 설정하고 위에 언급된 프로필 데이터 세트를 사용합니다.

필요한 데이터 세트를 만드는 방법에 대한 TCF 2.0 동의 [](../../../rtcdp/privacy/iab/dataset-preparation.md) 사항을 캡처하기 위한 데이터 세트를 만드는 방법에 대한 자습서를 참조하십시오.

Edge 구성 만들기에 대한 지침은 [IAB TCF 2.0 준수 개요를](../../../rtcdp/privacy/privacy-overview.md) 참조하십시오.

## Audience Manager 통합

Adobe Audience Manager(AAM)은 다운스트림 파트너에게 고객 개인정보 보호 선택 사항을 평가, 검증 및 전달할 수 있는 IAB TCF 2.0에 대한 지원을 제공합니다. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>AEP 웹 SDK를 통해 Audience Manager과 통합하려면 Adobe Audience Manager으로 이동할 Edge 구성을 설정해야 합니다.

## 경험 이벤트 및 Adobe Analytics 통합

실시간 CDP 및 Audience Manager 고객은 고객의 현재 동의 환경 설정을 추적하는 반면, 경험 이벤트는 이벤트를 수집할 때 활성 상태였던 고객의 동의 환경 설정을 유지할 수 있습니다.

이벤트에 대한 동의 정보를 수집하려면 다음이 필요합니다.

- 개인 정보 혼합이 포함된 [!DNL XDM Experience Event] 클래스를 기반으로 하는 [!DNL Experience Event] 데이터 집합입니다.
- 위에 있는 데이터 세트를 사용하여 [!DNL XDM Experience Event] 설정하는 에지 구성

XDM 경험 이벤트를 Analytics 히트로 변환하는 방법에 대한 자세한 내용은 [Analytics 개요](../../data-collection/adobe-analytics/analytics-overview.md) 설명서를 참조하십시오.

## AEP 웹 SDK 통합

아래 섹션에서는 IAB TCF 2.0과 AEP 웹 SDK의 주요 통합 지점에 대해 설명합니다.

>[!NOTE]
>
>실시간 CDP 또는 Audience Manager이 설정되어 있지 않더라도 IAB TCF 2.0과 웹 SDK를 통합할 수 있습니다. 동의 환경 설정은 경험 이벤트의 컬렉션을 제어하고 ID 쿠키를 설정하는 데 사용할 수 있습니다.

### 기본 동의

기본 동의는 고객에 대해 이미 저장된 동의 환경 설정이 없을 때 사용됩니다. 이는 기본 동의 옵션이 AEP 웹 SDK의 동작을 제어하고 고객의 지역에 따라 변경할 수 있음을 의미합니다.

예를 들어, 개인 정보 보호 규정(GDPR)의 관할에 속하지 않는 고객이 있는 경우 기본 동의를 로 설정할 수 `in`있지만, GDPR 관할지에서는 기본 동의를 로 설정할 수 있습니다 `pending`. 클라우드 관리 플랫폼(CMP)이 고객의 영역을 감지하고 IAB TCF 2.0 `gdprApplies` 에 플래그를 제공할 수 있습니다. 이 플래그를 사용하여 기본 동의를 설정할 수 있습니다.

기본 동의에 대한 자세한 내용은 SDK 구성 설명서의 [기본 동의 섹션](../../fundamentals/configuring-the-sdk.md#default-consent) 을 참조하십시오.

### 변경 시 동의 설정

AEP 웹 SDK에는 IAB TCF 2.0을 사용하여 고객의 동의 환경 설정을 모든 Adobe 서비스에 알리는 `setConsent` 명령이 있습니다. 실시간 CDP와 통합하면 고객 프로필이 업데이트됩니다. Audience Manager과 통합하면 고객 정보가 업데이트됩니다. 이를 호출하면 향후 경험 이벤트 전송 허용 여부를 제어하는 모든 것 또는 아무 것도 동의 환경 설정이 있는 쿠키도 설정됩니다. 이것은 동의가 바뀔 때마다 이 행동을 불러오려는 의도이다. 이후 페이지가 로드되면 경험 이벤트를 전송할 수 있는지 여부와 ID 쿠키를 설정할 수 있는지 여부를 결정하기 위해 경험 에지 동의 쿠키를 읽습니다.

Audience Manager의 IAB TCF 2.0 통합과 유사한 Experience Edge는 고객이 다음 목적을 위해 명시적 동의를 하면 동의를 제공합니다.

- **목적 1:** 장치에 정보 저장 및/또는 액세스
- **목적 10:** 제품 개발 및 개선
- **특수 목적 1:** 보안, 부정 행위 방지 및 디버그를 보장합니다. (IAB TCF 규정에 따라 항상 이에 동의함)
- **Adobe 공급업체 권한:** Adobe에 대한 동의(공급업체 565)

명령에 대한 자세한 내용은 `setConsent` 지원 동의에 대한 [설명서를 참조하십시오](../../consent/supporting-consent.md).

### 경험 이벤트에 동의 추가

AEP 웹 SDK에는 경험 이벤트를 수집하는 명령이 `sendEvent` 있습니다. 경험 이벤트 또는 Adobe Analytics과 통합하고 모든 경험 이벤트에 대한 동의 환경 설정을 원하는 경우 모든 명령에 동의 정보를 추가해야 `sendEvent` 합니다.

명령에 대한 자세한 내용은 `sendEvent` 이벤트 [추적 설명서를 참조하십시오](../../fundamentals/tracking-events.md).

## 다음 단계

이제 IAB Transparency &amp; Consent Framework 2.0에 대한 기본적인 이해가 있으시므로, IAB TCF 2.0을 Adobe Experience Platform Launch [와 함께 사용하는 방법과 Adobe Experience Platform Launch](./with-launch.md) 이 [없는 방법에 대한 가이드를 참조하십시오](./without-launch.md).
