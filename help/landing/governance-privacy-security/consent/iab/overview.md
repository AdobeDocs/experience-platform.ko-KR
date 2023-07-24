---
keywords: Experience Platform;홈;IAB;IAB 2.0;동의;동의
solution: Experience Platform
title: Experience Platform에서 IAB TCF 2.0 지원
description: Adobe Experience Platform에서 세그먼트를 대상으로 활성화할 때 고객 동의 선택 사항을 전달하도록 데이터 작업 및 스키마를 구성하는 방법에 대해 알아보십시오.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 1%

---

# Experience Platform에서 IAB TCF 2.0 지원

다음 [!DNL Transparency & Consent Framework] (TCF): [!DNL Interactive Advertising Bureau] (IAB)는 조직이 유럽 연합의 규정을 준수하여 개인 데이터 처리에 대한 소비자 동의를 획득하고, 기록하고, 업데이트할 수 있도록 하기 위한 개방형 표준 기술 프레임워크입니다 [!DNL General Data Protection Regulation] (GDPR). 프레임워크의 두 번째 반복인 TCF 2.0은 공급업체가 정확한 지리적 위치와 같은 데이터 처리의 특정 기능을 사용할 수 있는지 여부와 방법을 포함하여 소비자가 동의를 제공하거나 보류할 수 있는 방법에 대해 더 많은 유연성을 부여합니다.

>[!NOTE]
>
>TCF 2.0에 대한 자세한 내용은 [IAB 유럽 웹사이트](https://iabeurope.eu/tcf-2-0/), 지원 자료 및 기술 사양 포함.

Adobe Experience Platform은 등록된 항목의 일부입니다. [IAB TCF 2.0 공급업체 목록](https://iabeurope.eu/vendor-list-tcf-v2-0/), ID 아래 **565**. TCF 2.0 요구 사항을 준수하는 플랫폼을 사용하면 고객 동의 데이터를 수집하여 저장된 고객 프로필에 통합할 수 있습니다. 그런 다음 이 동의 데이터를 사용 사례에 따라 프로필이 내보낸 대상 세그먼트에 포함되는지 여부에 팩터링할 수 있습니다.

>[!IMPORTANT]
>
>플랫폼은 TCF 버전 2.0 이상만 준수할 수 있습니다. 이전 버전의 TCF는 지원되지 않습니다.

이 문서에서는 CMP에서 생성된 고객 동의 데이터를 수락하도록 데이터 작업 및 프로필 스키마를 구성하는 방법 및 Platform이 세그먼트를 내보낼 때 사용자 동의 선택 사항을 전달하는 방법에 대한 개요를 제공합니다.

## 사전 요구 사항

이 안내서와 함께 사용하려면 IAB TCF와 통합되고 호환되는 CMP(동의 관리 플랫폼)를 상업용이거나 소유하고 있어야 합니다. 다음을 참조하십시오. [준수 CMP 목록](https://iabeurope.eu/cmp-list/) 추가 정보.

>[!IMPORTANT]
>
>CMP의 ID가 올바르지 않으면 Platform은 데이터를 그대로 처리합니다. TCF 2.0을 적용하려면 데이터를 플랫폼으로 보내기 전에 CMP에 IAB TCF 2.0에 등록된 유효한 ID가 있는지 확인해야 합니다.

이 안내서에서는 다음 플랫폼 서비스에 대한 작업 이해도 필요합니다.

* [경험 데이터 모델(XDM)](../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [Adobe Experience Platform ID 서비스](../../../../identity-service/home.md): 디바이스와 시스템 간에 ID를 연결하여 고객 경험 데이터의 단편화로 인해 발생하는 근본적인 문제를 해결합니다.
* [실시간 고객 프로필](../../../../profile/home.md): 활용 [!DNL Identity Service] 을(를) 사용하여 실시간으로 데이터 세트에서 세부 고객 프로필을 만들 수 있습니다. [!DNL Real-Time Customer Profile] 는 데이터 레이크에서 데이터를 가져오고 고객 프로필을 별도의 데이터 저장소에 유지합니다.
* [Adobe Experience Platform 웹 SDK](../../../../edge/home.md): 다양한 Platform 서비스를 고객 응대 웹 사이트에 통합할 수 있는 클라이언트측 JavaScript 라이브러리.
   * [SDK 동의 명령](../../../../edge/consent/supporting-consent.md): 이 안내서에 표시된 동의 관련 SDK 명령에 대한 사용 사례 개요.
* [Adobe Experience Platform 세그멘테이션 서비스](../../../../segmentation/home.md): 나눌 수 있습니다. [!DNL Real-Time Customer Profile] 데이터는 유사한 트레이트를 공유하고 마케팅 전략에 유사하게 반응하는 개인 그룹으로 분류됩니다.

위에 나열된 플랫폼 서비스 외에도 다음을 잘 알고 있어야 합니다. [대상](../../../../data-governance/home.md) 플랫폼 생태계에서 그들의 역할.

## 고객 동의 흐름 요약 {#summary}

다음 섹션에서는 시스템이 제대로 구성된 후 동의 데이터를 수집하고 적용하는 방법에 대해 설명합니다.

### 동의 데이터 수집

플랫폼을 사용하면 다음 프로세스를 통해 고객 동의 데이터를 수집할 수 있습니다.

1. 고객은 웹 사이트의 대화 상자를 통해 데이터 수집에 대한 동의 환경 설정을 제공합니다.
1. CMP에서 동의 환경 설정 변경을 감지하고 그에 따라 TCF 동의 데이터를 생성합니다.
1. Platform Web SDK를 사용하면 생성된 동의 데이터(CMP에서 반환)가 Adobe Experience Platform으로 전송됩니다.
1. 수집된 동의 데이터는에 수집됩니다 [!DNL Profile]스키마에 TCF 동의 필드가 포함된 데이터 세트가 활성화되었습니다.

CMP 동의 변경 후크에서 트리거한 SDK 명령 외에도 동의 데이터는에 직접 업로드되는 고객 생성 XDM 데이터를 통해 Experience Platform으로 유입될 수 있습니다. [!DNL Profile]-활성화된 데이터 세트.

Adobe Audience Manager에서 Platform과 공유한 모든 세그먼트( 를 통해) [!DNL Audience Manager] 적절한 필드가 을 통해 해당 세그먼트에 적용되는 경우 소스 커넥터 또는 기타)에도 동의 데이터가 포함될 수 있습니다. [!DNL Experience Cloud Identity Service]. 에서 동의 데이터 수집에 대한 자세한 내용 [!DNL Audience Manager]의 문서를 참조하십시오. [IAB TCF를 위한 Adobe Audience Manager 플러그인](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=ko-KR).

### 다운스트림 동의 적용

TCF 동의 데이터가 성공적으로 수집되면 다운스트림 플랫폼 서비스에서 다음 프로세스가 수행됩니다.

1. [!DNL Real-Time Customer Profile] 는 해당 고객의 프로필에 대해 저장된 동의 데이터를 업데이트합니다.
1. Platform(565)에 대한 공급업체 권한이 클러스터의 모든 ID에 대해 제공된 경우에만 Platform이 고객 ID를 처리합니다.
1. TCF 2.0 공급업체 목록의 구성원에 속하는 대상으로 세그먼트를 내보낼 때 Platform은 두 플랫폼 모두에 대한 공급업체 권한이 있는 경우에만 프로필을 포함합니다(565) *및* 개별 대상은 클러스터의 모든 ID에 대해 제공됩니다.

이 문서의 나머지 섹션에서는 위에서 설명한 수집 및 시행 요구 사항을 충족하도록 플랫폼 및 데이터 작업을 구성하는 방법에 대한 지침을 제공합니다.

## CMP 내에서 고객 동의 데이터를 생성하는 방법 결정 {#consent-data}

각 CMP 시스템은 고유하므로 고객이 서비스와 상호 작용할 때 동의를 제공할 수 있는 최상의 방법을 결정해야 합니다. 이를 수행하는 일반적인 방법은 다음 예제와 유사한 쿠키 동의 대화 상자를 사용하는 것입니다.

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

이 대화 상자를 통해 고객은 다음을 옵트인하거나 옵트아웃할 수 있습니다.

| 동의 옵션 | 설명 |
| --- | --- |
| **목적** | 목적 은 브랜드가 고객 데이터를 사용할 수 있는 광고 기술 목적을 정의합니다. Platform에서 고객 ID를 처리하려면 다음 목적을 선택해야 합니다. <ul><li>**목적 1**: 장치에 대한 정보 저장 및/또는 액세스</li><li>**목적 10**: 제품 개발 및 개선</li></ul> |
| **공급업체 권한** | 광고 기술 목적 외에도 이 대화 상자를 통해 고객은 Adobe Experience Platform(565)를 비롯한 특정 공급업체에서 데이터를 사용할지 여부를 선택할 수 있어야 합니다. |

### 동의 문자열 {#consent-strings}

데이터를 수집하는 데 사용하는 방법에 관계없이 목표는 고객이 선택한 동의 옵션을 기반으로 문자열 값을 생성하는 것이며 이를 동의 문자열이라고 합니다.

TCF 사양에서 동의 문자열은 정책 및 공급업체에서 정의한 특정 마케팅 목적 측면에서 고객의 동의 설정에 대한 관련 세부 정보를 인코딩하는 데 사용됩니다. Platform은 이러한 문자열을 사용하여 각 고객에 대한 동의 설정을 저장하므로 해당 설정이 변경될 때마다 새 동의 문자열을 생성해야 합니다.

동의 문자열은 IAB TCF에 등록된 CMP에서만 만들 수 있습니다. 특정 CMP를 사용하여 동의 문자열을 생성하는 방법에 대한 자세한 내용은 [동의 문자열 서식 가이드](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) IAB TCF GitHub 저장소.

## TCF 동의 필드를 사용하여 데이터 세트 만들기 {#datasets}

고객 동의 데이터는 스키마에 TCF 동의 필드가 포함된 데이터 세트로 전송되어야 합니다. 다음 튜토리얼 참조: [tcf 2.0 동의 캡처를 위한 데이터 세트 만들기](./dataset.md) 을 참조하여 필요한 프로필 데이터 세트(및 선택 사항인 경험 이벤트 데이터 세트)를 생성하는 방법을 알아보십시오.

## 업데이트 [!DNL Profile] 동의 데이터를 포함하는 정책 병합 {#merge-policies}

을(를) 생성한 후 [!DNL Profile]동의 데이터 수집을 위한 데이터 세트 활성화 - 고객 프로필에 항상 TCF 동의 필드를 포함하도록 병합 정책이 구성되었는지 확인해야 합니다. 여기에는 데이터 세트 우선 순위를 설정하여 동의 데이터 세트가 잠재적으로 충돌할 수 있는 다른 데이터 세트보다 우선하도록 하는 작업이 포함됩니다.

병합 정책으로 작업하는 방법에 대한 자세한 내용은 [병합 정책 개요](../../../../profile/merge-policies/overview.md). 병합 정책을 설정할 때에는 세그먼트에 에서 제공하는 모든 필수 동의 속성이 포함되어 있는지 확인해야 합니다 [XDM 개인 정보 스키마 필드 그룹](./dataset.md#privacy-field-group)데이터 세트 준비에 대한 안내서에 요약된 대로 입니다.

## Experience Platform 웹 SDK를 통합하여 고객 동의 데이터 수집 {#sdk}

>[!NOTE]
>
>Adobe Experience Platform에서 직접 동의 데이터를 처리하려면 Experience Platform 웹 SDK를 사용해야 합니다. [!DNL Experience Cloud Identity Service] 은(는) 현재 지원되지 않습니다.
>
>[!DNL Experience Cloud Identity Service] 는 Adobe Audience Manager에서 동의 처리에 대해 여전히 지원되지만 TCF 2.0을 준수하려면 라이브러리를 (으)로 업데이트하기만 하면 됩니다. [버전 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

동의 문자열을 생성하도록 CMP를 구성한 후에는 Experience Platform 웹 SDK를 통합하여 해당 문자열을 수집하여 플랫폼으로 보내야 합니다. Platform SDK는 TCF 동의 데이터를 Platform으로 전송하는 데 사용할 수 있는 두 가지 명령(아래 하위 섹션에 설명)을 제공하며, 고객이 동의 정보를 처음으로 제공할 때 및 그 이후에 동의가 변경될 때마다 사용해야 합니다.

**SDK는 즉시 사용할 수 있는 CMP와 인터페이스하지 않습니다**. SDK를 웹 사이트에 통합하는 방법을 결정하고 CMP에서 동의 변경 사항을 수신하고 적절한 명령을 호출하는 것은 사용자가 결정합니다.

### 새 데이터 스트림 만들기

SDK가 Experience Platform에 데이터를 전송하려면 먼저 플랫폼에 대한 새 데이터스트림을 만들어야 합니다. 새 데이터 스트림을 만드는 방법에 대한 특정 단계는 [SDK 설명서](../../../../datastreams/overview.md).

데이터스트림에 대한 고유한 이름을 제공한 후 옆에 있는 토글 버튼을 선택합니다 **[!UICONTROL Adobe Experience Platform]**. 그런 다음 다음 다음 값을 사용하여 나머지 양식을 작성합니다.

| 데이터 스트림 필드 | 값 |
| --- | --- |
| [!UICONTROL 샌드박스] | 플랫폼 이름 [샌드박스](../../../../sandboxes/home.md) 에는 데이터 스트림을 설정하는 데 필요한 스트리밍 연결 및 데이터 세트가 포함되어 있습니다. |
| [!UICONTROL 스트리밍 인렛] | Experience Platform에 대한 유효한 스트리밍 연결입니다. 다음 튜토리얼 참조: [스트리밍 연결 만들기](../../../../ingestion/tutorials/create-streaming-connection-ui.md) 기존 스트리밍 인렛이 없는 경우 |
| [!UICONTROL 이벤트 데이터 세트] | 다음 항목 선택 [!DNL XDM ExperienceEvent] 에서 만들어진 데이터 세트 [이전 단계](#datasets). 다음을 포함한 경우 [[!UICONTROL IAB TCF 2.0 동의] 필드 그룹](../../../../xdm/field-groups/event/iab.md) 이 데이터 세트의 스키마에서 다음을 사용하여 시간 경과에 따른 동의 변경 이벤트를 추적할 수 있습니다. [`sendEvent`](#sendEvent) 명령, 이 데이터 세트에 해당 데이터 저장. 이 데이터 세트에 저장된 동의 값은 다음과 같습니다 **아님** 자동 적용 워크플로우에서 사용됩니다. |
| [!UICONTROL 프로필 데이터 세트] | 다음 항목 선택 [!DNL XDM Individual Profile] 에서 만들어진 데이터 세트 [이전 단계](#datasets). 를 사용하여 CMP 동의 변경 후크에 응답하는 경우 [`setConsent`](#setConsent) 명령, 수집된 데이터는 이 데이터 세트에 저장됩니다. 이 데이터 세트는 프로필이 활성화되므로 자동 시행 워크플로 동안 이 데이터 세트에 저장된 동의 값이 적용됩니다. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

완료되면 다음을 선택합니다. **[!UICONTROL 저장]** 화면 하단의 을 클릭하고 추가 프롬프트에 따라 계속 구성을 완료합니다.

### 동의 변경 명령 만들기

이전 섹션에서 설명한 데이터 스트림을 생성했으면 SDK 명령을 사용하여 동의 데이터를 Platform으로 전송할 수 있습니다. 아래 섹션에서는 각 SDK 명령을 다양한 시나리오에서 어떻게 사용할 수 있는지에 대한 예를 제공합니다.

>[!NOTE]
>
>모든 Platform SDK 명령에 대한 일반적인 구문에 대한 소개는 의 문서를 참조하십시오. [명령 실행](../../../../edge/fundamentals/executing-commands.md).

#### CMP 동의 변경 후크 사용 {#setConsent}

많은 CMP는 동의 변경 이벤트를 수신하는 즉시 사용 가능한 후크를 제공합니다. 이러한 이벤트가 발생하면 `setConsent` 고객의 동의 데이터를 업데이트하는 명령입니다.

다음 `setConsent` 명령에는 (1) 명령 유형을 나타내는 문자열(이 경우, &quot;setConsent&quot;) 및 (2) `consent` 스토리지는 아래와 같이 필수 동의 필드를 제공하는 하나 이상의 객체를 포함해야 합니다.

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| 페이로드 속성 | 설명 |
| --- | --- |
| `standard` | 사용 중인 동의 표준입니다. 이 값은 다음으로 설정해야 합니다. `IAB` tcf 2.0 동의 처리용. |
| `version` | 아래에 표시된 동의 표준의 버전 번호입니다. `standard`. 이 값은 다음으로 설정해야 합니다. `2.0` tcf 2.0 동의 처리용. |
| `value` | CMP에서 생성된 기본 64로 인코딩된 동의 문자열. |
| `gdprApplies` | GDPR이 현재 로그인한 고객에게 적용되는지 여부를 나타내는 부울 값입니다. 이 고객에 대해 TCF 2.0이 적용되려면 값을 로 설정해야 합니다. `true`. 기본값은 입니다. `true` 정의되지 않은 경우. |

다음 `setConsent` 명령은 동의 설정 변경을 감지하는 CMP 후크의 일부로 사용해야 합니다. 다음 JavaScript에서는 `setConsent` 명령은 OneTrust에 사용할 수 있습니다. `OnConsentChanged` 후크:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### 이벤트 사용 {#sendEvent}

를 사용하여 플랫폼에서 트리거된 모든 이벤트에 대한 TCF 2.0 동의 데이터를 수집할 수도 있습니다. `sendEvent` 명령입니다.

>[!NOTE]
>
>이 방법을 사용하려면 경험 이벤트 개인 정보 보호 필드 그룹을 [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] 스키마. 의 섹션을 참조하십시오. [ExperienceEvent 스키마 업데이트](./dataset.md#event-schema) 을 구성하는 방법에 대한 단계는 데이터 세트 준비 안내서에서 참조하십시오.

다음 `sendEvent` 명령은 웹 사이트의 적절한 이벤트 리스너에서 콜백으로 사용해야 합니다. 명령에는 (1) 명령 유형을 나타내는 문자열(이 경우 `sendEvent`) 및 (2) `xdm` 필수 동의 필드를 JSON으로 제공하는 개체:

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| 페이로드 속성 | 설명 |
| --- | --- |
| `xdm.consentStrings` | 필수 동의 필드를 제공하는 개체가 하나 이상 있어야 하는 배열입니다. |
| `consentStandard` | 사용 중인 동의 표준입니다. 이 값은 다음으로 설정해야 합니다. `IAB` tcf 2.0 동의 처리용. |
| `consentStandardVersion` | 아래에 표시된 동의 표준의 버전 번호입니다. `standard`. 이 값은 다음으로 설정해야 합니다. `2.0` tcf 2.0 동의 처리용. |
| `consentStringValue` | CMP에서 생성된 기본 64로 인코딩된 동의 문자열. |
| `gdprApplies` | GDPR이 현재 로그인한 고객에게 적용되는지 여부를 나타내는 부울 값입니다. 이 고객에 대해 TCF 2.0이 적용되려면 값을 로 설정해야 합니다. `true`. 기본값은 입니다. `true` 정의되지 않은 경우. |

### SDK 응답 처리

모두 [!DNL Platform SDK] 명령은 호출의 성공 또는 실패 여부를 나타내는 약속을 반환합니다. 그런 다음 고객에게 확인 메시지를 표시하는 것과 같은 추가 논리에 이러한 응답을 사용할 수 있습니다. 의 섹션을 참조하십시오. [성공 또는 실패 처리](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 특정 예제의 SDK 명령 실행에 대한 안내서에서 참조할 수 있습니다.

## 세그먼트 내보내기 {#export}

>[!NOTE]
>
>세그먼트 내보내기를 시작하기 전에 세그먼트에 모든 필수 동의 필드가 포함되어 있는지 확인해야 합니다. 의 섹션을 참조하십시오. [병합 정책 구성](#merge-policies) 추가 정보.

고객 동의 데이터를 수집하고 필요한 동의 속성을 포함하는 대상 세그먼트를 만들었으면 해당 세그먼트를 다운스트림 대상으로 내보낼 때 TCF 2.0 준수를 적용할 수 있습니다.

동의 설정이 `gdprApplies` 이(가) (으)로 설정됨 `true` 고객 프로필 세트의 경우 다운스트림 대상으로 내보낸 프로필의 데이터는 각 프로필에 대한 TCF 동의 환경 설정을 기반으로 필터링됩니다. 필요한 동의 환경 설정을 충족하지 않는 프로필은 내보내기 프로세스 중에 건너뜁니다.

고객은 다음의 목적(에 명시된 대로)에 동의해야 합니다. [TCF 2.0 정책](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions))을 클릭하여 대상으로 내보내는 세그먼트에 프로필을 포함할 수 있습니다.

* **목적 1**: 장치에 대한 정보 저장 및/또는 액세스
* **목적 10**: 제품 개발 및 개선

또한 TCF 2.0을 사용하려면 데이터를 대상으로 보내기 전에 데이터 소스가 대상의 공급업체 권한을 확인해야 합니다. 따라서 Platform은 해당 대상에 바인딩된 데이터를 포함하기 전에 클러스터의 모든 ID에 대해 대상의 공급업체 권한이 로 옵트인되었는지 확인합니다.

>[!NOTE]
>
>Adobe Audience Manager과 공유되는 모든 세그먼트에는 Platform의 대응 세그먼트와 동일한 TCF 2.0 동의 값이 포함됩니다. 다음 이후 [!DNL Audience Manager] 플랫폼(565)과 동일한 공급업체 ID를 공유합니다. 동일한 목적과 공급업체 권한이 필요합니다. 다음에서 문서 보기: [IAB TCF를 위한 Adobe Audience Manager 플러그인](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=ko-KR) 추가 정보.

## 구현 테스트 {#test-implementation}

TCF 2.0 구현을 구성하고 세그먼트를 대상으로 내보낸 후에는 동의 요구 사항을 충족하지 않는 데이터를 내보낼 수 없습니다. 그러나 내보내는 동안 올바른 고객 프로필이 필터링되었는지 확인하려면 대상의 데이터 저장소를 수동으로 확인하여 동의가 제대로 적용되었는지 확인해야 합니다.

여러 ID가 클러스터를 구성하고 TCF 2.0이 적용되는 경우 단일 ID에 올바른 목적과 공급업체 권한이 포함되지 않은 경우 전체 클러스터가 제외됩니다.

## 다음 단계

이 문서에서는 TCF 2.0에 설명된 대로 비즈니스 의무를 충족하도록 플랫폼 데이터 작업을 구성하는 프로세스에 대해 다룹니다. 의 개요 보기 [거버넌스, 개인 정보 보호 및 보안](../../overview.md) 자세한 내용은 Platform의 개인 정보 보호 관련 기능을 참조하십시오.
