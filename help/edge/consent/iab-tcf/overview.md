---
title: Adobe Experience Platform Web SDK의 IAB TCF 2.0 지원
description: Adobe Experience Platform Web SDK를 사용하여 IAB TCF 2.0 동의 환경 설정을 지원하는 방법을 알아봅니다
keywords: 동의;설정 동의;프로필 개인 정보 필드 그룹;경험 이벤트 개인 정보 필드 그룹;개인 정보 필드 그룹;IAB TCF 2.0;실시간 CDP;실시간 고객 데이터 프로필
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: da7696d288543abd21ff8a1402e81dcea32efbc2
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK의 IAB TCF 2.0 지원

Adobe Experience Platform Web SDK는 Interactive Advertising Bureau Transparency &amp; Consent Framework 버전 2.0(IAB TCF 2.0)을 지원합니다. 이 안내서에서는 실시간 고객 데이터 플랫폼, Audience Manager, 경험 이벤트, Adobe Analytics 및 Experience Edge와 통합된 Adobe Experience Platform Web SDK를 통해 IAB TCF 2.0을 지원하는 요구 사항을 보여줍니다.

또한 다음 가이드를 사용하여 Adobe Experience Platform Launch과 IAB TCF 2.0을 통합하는 방법을 학습할 수 있습니다.

- [Adobe Experience Platform Launch 사용](./with-launch.md)
- [Adobe Experience Platform Launch 제외](./without-launch.md)

## 시작

IAB TCF 2.0을 사용하여 웹 SDK를 구현하려면 XDM(Experience Data Model) 및 Experience Event에 대한 작업 이해를 가져야 합니다. 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(경험 데이터 모델) 시스템 개요](../../../xdm/home.md): 표준화와 상호 운용성은 Adobe Experience Platform의 주요 개념입니다. [!DNL Experience Data Model (XDM)]Adobe 기반의 은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하려는 노력입니다.

## Experience Platform 통합

SDK를 사용하여 Adobe Experience Platform에 동의 데이터를 전송하려면 다음 조건을 충족해야 합니다.

- [!DNL XDM Individual Profile] 클래스를 기반으로 하며 [!DNL Real-time Customer Profile]에서 사용할 수 있도록 활성화된 TCF 2.0 동의 필드를 포함하는 데이터 집합입니다.
- 위에 언급된 플랫폼 및 프로필 사용 데이터 세트를 사용하여 설정된 데이터 스트림.

필요한 데이터 세트 및 데이터 스트림을 만드는 방법에 대한 지침은 [TCF 2.0 준수](../../../landing/governance-privacy-security/consent/iab/overview.md)의 안내서를 참조하십시오.

## Audience Manager 통합

Adobe Audience Manager(AAM)에는 다운스트림 파트너에게 고객 개인 정보 보호 선택 사항을 평가, 수행 및 전달할 수 있는 IAB TCF 2.0에 대한 지원이 포함되어 있습니다. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Adobe Experience Platform Web SDK를 통해 Audience Manager과 통합하려면 Adobe Audience Manager에 전달할 데이터 스트림을 설정했는지 확인합니다.

## Experience Events 및 Adobe Analytics 통합

실시간 CDP와 Audience Manager의 대상은 고객의 현재 동의 환경 설정을 추적하는 반면 Experience Events는 이벤트가 수집될 때 활성 상태인 고객의 동의 환경 설정을 보유할 수 있습니다.

이벤트에 대한 동의 정보를 수집하려면 다음 조건을 충족해야 합니다.

- [!DNL Experience Event] 개인 정보 스키마 필드 그룹이 있는 [!DNL XDM Experience Event] 클래스를 기반으로 하는 데이터 집합입니다.
- 위의 [!DNL XDM Experience Event] 데이터 세트를 사용하여 설정된 데이터 스트림.

XDM 경험 이벤트를 Analytics 히트로 변환하는 방법에 대한 자세한 내용은 [Analytics 개요](../../data-collection/adobe-analytics/analytics-overview.md) 설명서를 참조하여 시작하십시오.

## Adobe Experience Platform 웹 SDK 통합

아래 섹션에서는 IAB TCF 2.0과 Adobe Experience Platform Web SDK 간의 주요 통합 지점을 설명합니다.

>[!NOTE]
>
>실시간 CDP나 Audience Manager을 설정하지 않고도 웹 SDK와 IAB TCF 2.0을 통합할 수 있습니다. 동의 환경 설정은 경험 이벤트 컬렉션을 제어하고 ID 쿠키를 설정하는 데 사용할 수 있습니다.

### 기본 동의

고객에 대해 이미 저장된 동의 기본 설정이 없을 때 기본 동의가 사용됩니다. 즉, 기본 동의 옵션은 Adobe Experience Platform Web SDK의 동작을 제어하고 고객의 지역에 따라 변경할 수 있습니다.

예를 들어, GDPR(일반 데이터 보호 규정)의 관할에 속하지 않는 고객이 있는 경우 기본 동의는 `in`으로 설정될 수 있지만 GDPR의 관할 내에서는 기본 동의를 `pending`로 설정할 수 있습니다. CMP(동의 관리 플랫폼)가 고객의 지역을 감지하고 IAB TCF 2.0에 플래그 `gdprApplies`를 제공할 수 있습니다. 이 플래그는 기본 동의를 설정하는 데 사용할 수 있습니다.

기본 동의에 대한 자세한 내용은 SDK 구성 설명서의 [기본 동의 섹션](../../fundamentals/configuring-the-sdk.md#default-consent)을 참조하십시오.

### 변경 시 동의 설정

Adobe Experience Platform Web SDK에는 IAB TCF 2.0을 사용하여 고객의 동의 환경 설정을 모든 Adobe 서비스에 전달하는 `setConsent` 명령이 있습니다. 실시간 CDP와 통합하는 경우 고객 프로필이 업데이트됩니다. Audience Manager과 통합하는 경우 고객 정보가 업데이트됩니다. 이를 호출하면 향후 경험 이벤트의 전송 허용 여부를 제어하는 전체 또는 임의 동의 환경 설정이 있는 쿠키도 설정됩니다. 이 작업은 동의가 변경될 때마다 호출됩니다. 향후 페이지가 로드될 때 Experience Edge 동의 쿠키를 읽어 Experience Event를 전송할 수 있는지 여부 및 ID 쿠키를 설정할 수 있는지 여부를 결정합니다.

Audience Manager의 IAB TCF 2.0 통합과 유사한 Experience Edge는 고객이 다음 용도에 대해 명시적 동의를 제공하면 동의를 제공합니다.

- **목적 1:** 장치에서 정보 저장 및/또는 액세스
- **목적 10:** 제품 개발 및 개선
- **특수 목적 1:** 보안 확보, 사기 방지 및 디버그 (IAB TCF 규정에 따라 항상 동의함)
- **Adobe 공급업체 권한:** Adobe 동의(공급업체 565)

`setConsent` 명령에 대한 자세한 내용은 [지원 동의](../../consent/supporting-consent.md)에서 설명서를 참조하십시오.

### 경험 이벤트에 동의 추가

Adobe Experience Platform Web SDK에는 Experience Event를 수집하는 `sendEvent` 명령이 있습니다. Experience Events 또는 Adobe Analytics과 통합하고 모든 Experience Event에 대한 동의 환경 설정을 원하는 경우 모든 `sendEvent` 명령에 동의 정보를 추가해야 합니다.

`sendEvent` 명령에 대한 자세한 내용은 [추적 이벤트](../../fundamentals/tracking-events.md)에서 설명서를 참조하십시오.

## 다음 단계

IAB Transparency &amp; Consent Framework 2.0에 대한 기본적인 이해가 있으므로 Adobe Experience Platform Launch](./with-launch.md) 사용 시 IAB TCF 2.0 [Adobe Experience Platform Launch](./without-launch.md) 사용 안 함 또는 [없이 사용하는 방법에 대한 안내서를 참조하십시오.
