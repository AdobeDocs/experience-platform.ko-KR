---
title: Adobe Experience Platform 웹 SDK에서 IAB TCF 2.0 지원
description: Adobe Experience Platform 웹 SDK를 사용하여 IAB TCF 2.0 동의 환경 설정을 지원하는 방법에 대해 알아봅니다.
keywords: 동의;setConsent;프로필 개인 정보 필드 그룹;경험 이벤트 개인 정보 필드 그룹;개인 정보 필드 그룹;IAB TCF 2.0;실시간 CDP;실시간 고객 데이터 프로필
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
translation-type: tm+mt
source-git-commit: 7d7502b238f96eda1a15b622ba10bbccc289b725
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Adobe Experience Platform 웹 SDK에서 IAB TCF 2.0 지원

Adobe Experience Platform 웹 SDK는 Interactive Advertising Bureau Transparency &amp; Consent Framework 버전 2.0(IAB TCF 2.0)을 지원합니다. 본 가이드는 실시간 고객 데이터 플랫폼, Audience Manager, 경험 이벤트, Adobe Analytics 및 Experience Edge와 통합되는 Adobe Experience Platform 웹 SDK를 통해 IAB TCF 2.0을 지원하기 위한 요구 사항을 보여줍니다.

또한 Adobe Experience Platform Launch과 IAB TCF 2.0을 통합하는 방법과를 사용하지 않는 방법에 대한 학습을 지원하기 위해 다음 가이드를 사용할 수 있습니다.

- [Adobe Experience Platform Launch 사용](./with-launch.md)
- [Adobe Experience Platform Launch 없이](./without-launch.md)

## 시작하기

IAB TCF 2.0을 사용하여 웹 SDK를 구현하려면 XDM(Experience Data Model) 및 경험 이벤트에 대한 충분한 지식이 있어야 합니다. 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(Experience Data Model) 시스템 개요](../../../xdm/home.md):표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. [!DNL Experience Data Model (XDM)]Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

## Experience Platform 통합

SDK를 사용하여 Adobe Experience Platform에 동의 데이터를 전송하려면 다음이 필요합니다.

- [!DNL XDM Individual Profile] 클래스를 기반으로 하며 [!DNL Real-time Customer Profile]에서 사용할 수 있도록 TCF 2.0 동의 필드를 포함하는 스키마가 있는 데이터 집합입니다.
- Platform(플랫폼) 및 위에 언급된 프로필 사용 데이터 세트에 대해 설정된 Edge 구성

필요한 데이터 세트 및 가장자리 구성을 만드는 방법에 대한 지침은 [TCF 2.0 준수](../../../landing/governance-privacy-security/consent/iab/overview.md)에 대한 안내서를 참조하십시오.

## Audience Manager 통합

Adobe Audience Manager(AAM)에는 다운스트림 파트너에게 고객 개인 정보 선택을 평가, 확인 및 전달할 수 있는 IAB TCF 2.0에 대한 지원이 포함되어 있습니다.<!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Adobe Experience Platform 웹 SDK를 통해 Audience Manager과 통합하려면 Adobe Audience Manager으로 전달할 Edge 구성을 설정해야 합니다.

## 경험 이벤트 및 Adobe Analytics 통합

실시간 CDP 및 Audience Manager의 고객이 고객의 현재 동의 환경 설정을 추적하는 반면, 경험 이벤트는 이벤트를 수집할 때 활성 상태였던 고객의 동의 환경 설정을 유지할 수 있습니다.

이벤트에 대한 동의 정보를 수집하려면 다음이 필요합니다.

- [!DNL Experience Event] 개인 정보 스키마 필드 그룹이 있는 [!DNL XDM Experience Event] 클래스를 기반으로 하는 데이터 집합입니다.
- 위의 [!DNL XDM Experience Event] 데이터 집합으로 설정된 에지 구성

XDM 경험 이벤트를 분석 히트로 변환하는 방법에 대한 자세한 내용은 [분석 개요](../../data-collection/adobe-analytics/analytics-overview.md) 설명서를 읽으십시오.

## Adobe Experience Platform 웹 SDK 통합

아래 섹션에서는 IAB TCF 2.0과 Adobe Experience Platform Web SDK 간의 주요 통합 지점에 대해 설명합니다.

>[!NOTE]
>
>실시간 CDP 또는 Audience Manager을 설정하지 않더라도 IAB TCF 2.0을 웹 SDK와 통합할 수 있습니다. 동의 환경 설정은 경험 이벤트 컬렉션을 제어하고 ID 쿠키를 설정하는 데 사용할 수 있습니다.

### 기본 동의

기본 동의는 고객에 대해 이미 저장된 동의 환경 설정이 없을 때 사용됩니다. 즉, 기본 동의 옵션은 Adobe Experience Platform 웹 SDK의 비헤이비어를 제어할 수 있고 고객의 지역에 따라 변경할 수 있습니다.

예를 들어, GDPR(General Data Protection Regulation)의 관할권이 아닌 고객이 있는 경우, 기본 동의는 `in`로 설정될 수 있지만, GDPR의 관할권 내에서는 기본 동의를 `pending`로 설정할 수 있습니다. CMP(동의 관리 플랫폼)은 고객의 지역을 감지하고 IAB TCF 2.0에 플래그 `gdprApplies`를 제공할 수 있습니다. 이 플래그를 사용하여 기본 동의를 설정할 수 있습니다.

기본 동의에 대한 자세한 내용은 SDK 구성 설명서의 [기본 동의 섹션](../../fundamentals/configuring-the-sdk.md#default-consent)을 참조하십시오.

### 변경 시 동의 설정

Adobe Experience Platform 웹 SDK에는 IAB TCF 2.0을 사용하여 고객의 동의 기본 설정을 모든 Adobe 서비스에 알리는 `setConsent` 명령이 있습니다. 실시간 CDP와 통합하려는 경우 이 명령을 사용하면 고객의 프로필을 업데이트합니다. Audience Manager과 통합하면 고객 정보가 업데이트됩니다. 이 옵션을 호출하면 향후 경험 이벤트 전송 허용 여부를 제어하는 모든 또는 없는 동의 환경 설정이 있는 쿠키도 설정됩니다. 이 작업은 동의가 변경될 때마다 호출됩니다. 향후 페이지 로드 시 경험 이벤트를 전송할 수 있는지 여부 및 ID 쿠키를 설정할 수 있는지 여부를 결정하기 위해 경험 에지 동의 쿠키를 읽습니다.

Audience Manager의 IAB TCF 2.0 통합과 유사한 Experience Edge는 고객이 다음 목적을 위해 명시적 동의를 제공했을 때 동의를 제공합니다.

- **목적 1: 장치에서** 정보 저장 및/또는 액세스
- **목적 10:** 제품 개발 및 개선
- **특별 목적 1:** 보안, 사기 방지 및 디버그를 보장합니다. (IAB TCF 규정에 따라 항상 이에 동의함)
- **Adobe 공급업체 권한:** Adobe에 대한 동의(공급업체 565)

`setConsent` 명령에 대한 자세한 내용은 [지원 동의](../../consent/supporting-consent.md)에 있는 설명서를 참조하십시오.

### 경험 이벤트에 동의 추가

Adobe Experience Platform 웹 SDK에는 경험 이벤트를 수집하는 `sendEvent` 명령이 있습니다. 경험 이벤트 또는 Adobe Analytics과 통합하고 모든 경험 이벤트의 동의 기본 설정을 원하는 경우, 모든 `sendEvent` 명령에 동의 정보를 추가해야 합니다.

`sendEvent` 명령에 대한 자세한 내용은 [추적 이벤트](../../fundamentals/tracking-events.md)에 대한 설명서를 참조하십시오.

## 다음 단계

IAB Transparency &amp; Concepts Framework 2.0에 대한 기본적인 이해가 있으시니, Adobe Experience Platform Launch](./with-launch.md)와 함께 IAB TCF 2.0 [을 사용하는 방법과 Adobe Experience Platform Launch](./without-launch.md)가 없는 [을(를) 참조하십시오.
