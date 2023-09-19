---
title: Adobe Experience Platform 웹 SDK의 IAB TCF 2.0 지원
description: Adobe Experience Platform 웹 SDK를 사용하여 IAB TCF 2.0 동의 환경 설정을 지원하는 방법을 알아봅니다
keywords: 동의;setConsent;프로필 개인 정보 필드 그룹;경험 이벤트 개인 정보 필드 그룹;개인 정보 필드 그룹;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---

# Adobe Experience Platform 웹 SDK의 IAB TCF 2.0 지원

Adobe Experience Platform Web SDK는 Interactive Advertising Bureau Transparency &amp; Consent Framework 버전 2.0(IAB TCF 2.0)을 지원합니다. 이 안내서에서는 Adobe Real-time Customer Data Platform, Audience Manager, 경험 이벤트, Adobe Analytics 및 Edge Network와 통합된 Adobe Experience Platform Web SDK를 통해 IAB TCF 2.0을 지원하기 위한 요구 사항을 보여줍니다.

또한 다음 안내서를 통해 태그와 함께/없이 IAB TCF 2.0을 통합하는 방법을 학습할 수 있습니다.

- [태그 포함](./with-launch.md)
- [태그 없음](./without-launch.md)

## 시작하기

IAB TCF 2.0으로 Web SDK를 구현하려면 XDM(경험 데이터 모델) 및 경험 이벤트에 대한 작업 이해를 가지고 있어야 합니다. 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(경험 데이터 모델) 시스템 개요](../../../xdm/home.md): 표준화와 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. [!DNL Experience Data Model (XDM)]는 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.

## Experience Platform 통합

SDK를 사용하여 Adobe Experience Platform에 동의 데이터를 전송하려면 다음 조건을 충족해야 합니다.

- 스키마를 기반으로 하는 데이터 세트 [!DNL XDM Individual Profile] 클래스에서 사용 가능한 TCF 2.0 동의 필드를 포함합니다. [!DNL Real-Time Customer Profile].
- 위에서 언급한 플랫폼 및 프로필 지원 데이터 세트로 설정된 데이터 스트림입니다.

다음 안내서를 참조하십시오. [TCF 2.0 규정 준수](../../../landing/governance-privacy-security/consent/iab/overview.md) 필요한 데이터 세트 및 데이터 스트림을 만드는 방법에 대한 지침입니다.

## Audience Manager 통합

Adobe Audience Manager(AAM)에는 IAB TCF 2.0에 대한 지원이 포함되어 있으므로 고객 개인 정보 보호 선택 사항을 평가하고 준수하며 다운스트림 파트너에게 전달할 수 있습니다. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Adobe Experience Platform Web SDK를 통해 Audience Manager과 통합하려면 Adobe Audience Manager에 전달할 데이터 스트림을 설정했는지 확인하십시오.

## 경험 이벤트 및 Adobe Analytics 통합

Real-Time CDP 및 Audience Manager 대상자는 고객의 현재 동의 환경 설정을 추적하는 반면, 경험 이벤트는 이벤트가 수집될 때 활성화되었던 고객의 동의 환경 설정을 보관할 수 있습니다.

이벤트에 대한 동의 정보를 수집하려면 다음 조건을 충족해야 합니다.

- 다음을 기반으로 하는 데이터 세트 [!DNL XDM Experience Event] 클래스, 포함 [!DNL Experience Event] 개인 정보 스키마 필드 그룹.
- 로 설정된 데이터 스트림 [!DNL XDM Experience Event] 위의 데이터 세트입니다.

XDM 경험 이벤트를 Analytics 히트로 변환하는 방법에 대한 자세한 내용은 [Analytics 개요](../../data-collection/adobe-analytics/analytics-overview.md) 설명서를 참조하십시오.

## Adobe Experience Platform Web SDK 통합

아래 섹션에서는 IAB TCF 2.0과 Adobe Experience Platform 웹 SDK 간의 주요 통합 지점에 대해 설명합니다.

>[!NOTE]
>
>Real-Time CDP 또는 Audience Manager을 설정하지 않아도 Web SDK와 IAB TCF 2.0을 통합할 수 있습니다. 동의 환경 설정을 사용하여 경험 이벤트 수집 및 ID 쿠키 설정을 제어할 수 있습니다.

### 기본 동의

고객에 대해 이미 저장된 동의 기본 설정이 없는 경우 기본 동의가 사용됩니다. 즉, 기본 동의 옵션은 Adobe Experience Platform Web SDK의 동작을 제어하고 고객의 지역에 따라 변경할 수 있습니다.

예를 들어 고객이 GDPR(일반 데이터 보호 규정)의 적용을 받지 않는 경우 기본 동의를 로 설정할 수 있습니다. `in`, 그러나 GDPR의 관할 구역에서 기본 동의를 로 설정할 수 있습니다. `pending`. CMP(동의 관리 플랫폼)가 고객의 지역을 감지하고 플래그를 제공할 수 있습니다 `gdprApplies` IAB TCF 2.0으로 이 플래그는 기본 동의를 설정하는 데 사용할 수 있습니다.

기본 동의에 대한 자세한 내용은 [기본 동의 섹션](../../fundamentals/configuring-the-sdk.md#default-consent) SDK 구성 설명서에서 확인할 수 있습니다.

### 변경 시 동의 설정

Adobe Experience Platform Web SDK에는 `setConsent` iab TCF 2.0을 사용하여 고객의 동의 환경 설정을 모든 Adobe 서비스에 전달하는 명령입니다. Real-Time CDP과 통합하는 경우 고객 프로필을 업데이트합니다. Audience Manager과 통합하는 경우 고객 정보가 업데이트됩니다. 이를 호출하면 향후 경험 이벤트 전송 허용 여부를 제어하는 all-or-nothing 동의 환경 설정이 있는 쿠키도 설정됩니다. 동의가 변경될 때마다 이 작업을 호출하기 위한 것입니다. 이후 페이지 로드 시 Edge Network 동의 쿠키를 읽어 경험 이벤트를 전송할 수 있는지 여부와 ID 쿠키를 설정할 수 있는지 여부를 결정합니다.

Audience Manager의 IAB TCF 2.0 통합과 마찬가지로 Edge Network는 고객이 다음 목적에 대한 명시적 동의를 제공한 경우 동의합니다.

- **목적 1:** 장치에 대한 정보 저장 및/또는 액세스
- **목적 10:** 제품 개발 및 개선
- **특수 목적 1:** 보안을 보장하고, 사기를 방지하고, 디버그를 수행할 수 있습니다. (IAB TCF 규정에 따라, 이는 항상 동의합니다.)
- **Adobe 공급업체 권한:** Adobe 동의(공급업체 565)

에 대한 자세한 내용은 `setConsent` 명령,에서 설명서 읽기 [동의 지원](../../consent/supporting-consent.md).

### 경험 이벤트에 동의 추가

Adobe Experience Platform Web SDK에는 `sendEvent` 경험 이벤트를 수집하는 명령입니다. 경험 이벤트 또는 Adobe Analytics과 통합하고 모든 경험 이벤트에 대한 동의 환경 설정을 원하는 경우 모든 활동에 동의 정보를 추가해야 합니다 `sendEvent` 명령입니다.

에 대한 자세한 내용은 `sendEvent` 명령,에서 설명서 읽기 [이벤트 추적](../../fundamentals/tracking-events.md).

## 다음 단계

이제 IAB 투명성 및 동의 프레임워크 2.0에 대한 기본 사항을 이해했으므로 IAB TCF 2.0 사용에 대한 안내서 중 하나를 참조하십시오 [태그 포함](./with-launch.md) 또는 [태그 없음](./without-launch.md).
