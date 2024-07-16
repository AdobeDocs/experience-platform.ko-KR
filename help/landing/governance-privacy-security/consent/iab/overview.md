---
keywords: Experience Platform;홈;IAB;IAB 2.0;동의;동의
solution: Experience Platform
title: Experience Platform에서 IAB TCF 2.0 지원
description: Adobe Experience Platform에서 세그먼트를 대상으로 활성화할 때 고객 동의 선택 사항을 전달하도록 데이터 작업 및 스키마를 구성하는 방법에 대해 알아보십시오.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 0%

---

# Experience Platform에서 IAB TCF 2.0 지원

[!DNL Interactive Advertising Bureau](IAB)에 설명된 [!DNL Transparency & Consent Framework](TCF)는 조직이 유럽 연합의 [!DNL General Data Protection Regulation](GDPR)을 준수하여 개인 데이터 처리에 대한 소비자 동의를 얻고, 기록하고, 업데이트할 수 있도록 하기 위한 개방형 표준 기술 프레임워크입니다. 프레임워크의 두 번째 반복인 TCF 2.0은 공급업체가 정확한 지리적 위치와 같은 데이터 처리의 특정 기능을 사용할 수 있는지 여부와 방법을 포함하여 소비자가 동의를 제공하거나 보류할 수 있는 방법에 대해 더 많은 유연성을 부여합니다.

>[!NOTE]
>
>지원 자료 및 기술 사양을 포함하여 TCF 2.0에 대한 자세한 내용은 [IAB 유럽 웹 사이트](https://iabeurope.eu/)를 참조하십시오.

Adobe Experience Platform은 ID **565**&#x200B;에 등록된 [IAB TCF 2.0 공급업체 목록](https://iabeurope.eu/vendor-list-tcf/)의 일부입니다. TCF 2.0 요구 사항을 준수하는 플랫폼을 사용하면 고객 동의 데이터를 수집하여 저장된 고객 프로필에 통합할 수 있습니다. 그런 다음 이 동의 데이터를 사용 사례에 따라 프로필이 내보낸 대상 세그먼트에 포함되는지 여부에 팩터링할 수 있습니다.

>[!IMPORTANT]
>
>플랫폼은 TCF 버전 2.0 이상만 준수할 수 있습니다. 이전 버전의 TCF는 지원되지 않습니다.

이 문서에서는 CMP(동의 관리 플랫폼)에서 생성한 고객 동의 데이터를 수락하도록 데이터 작업 및 프로필 스키마를 구성하는 방법에 대한 개요를 제공합니다. 또한 Platform이 세그먼트를 내보낼 때 사용자 동의 선택 사항을 전달하는 방법을 다룹니다.

## 전제 조건

이 안내서와 함께 따라가려면 상업용이거나 IAB TCF와 통합되고 호환되는 CMP를 사용해야 합니다. 자세한 내용은 [호환 CMP 목록](https://iabeurope.eu/cmp-list/)을 참조하십시오.

>[!IMPORTANT]
>
>CMP의 ID가 올바르지 않으면 Platform은 데이터를 그대로 처리합니다. TCF 2.0을 적용하려면 데이터를 플랫폼으로 보내기 전에 CMP에 IAB TCF 2.0에 등록된 유효한 ID가 있는지 확인해야 합니다.

이 안내서에서는 다음 플랫폼 서비스에 대한 작업 이해도 필요합니다.

* [XDM(경험 데이터 모델)](/help/xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [Adobe Experience Platform ID 서비스](/help/identity-service/home.md): 장치 및 시스템 간에 ID를 연결하여 고객 경험 데이터의 단편화로 인한 근본적인 문제를 해결합니다.
* [실시간 고객 프로필](/help/profile/home.md): [!DNL Identity Service]을(를) 사용하여 데이터 세트에서 실시간으로 세부 고객 프로필을 만듭니다. [!DNL Real-Time Customer Profile]은(는) 데이터 레이크에서 데이터를 가져오고 고객 프로필을 별도의 데이터 저장소에 유지합니다.
* [Adobe Experience Platform Web SDK](/help/web-sdk/home.md): 다양한 플랫폼 서비스를 고객 응대 웹 사이트에 통합할 수 있는 클라이언트측 JavaScript 라이브러리입니다.
   * [SDK 동의 명령](../../../../web-sdk/commands/setconsent.md): 이 안내서에 표시된 동의 관련 SDK 명령에 대한 사용 사례 개요입니다.
* [Adobe Experience Platform 세분화 서비스](/help/segmentation/home.md): [!DNL Real-Time Customer Profile] 데이터를 유사한 트레이트를 공유하고 마케팅 전략에 유사하게 반응하는 개인 그룹으로 나눌 수 있습니다.

위에 나열된 플랫폼 서비스 외에 [대상](/help/data-governance/home.md) 및 플랫폼 생태계에서의 역할도 잘 알고 있어야 합니다.

## 고객 동의 흐름 요약 {#summary}

다음 섹션에서는 시스템이 제대로 구성된 후 동의 데이터를 수집하고 적용하는 방법에 대해 설명합니다.

### 동의 데이터 수집

플랫폼을 사용하면 다음 프로세스를 통해 고객 동의 데이터를 수집할 수 있습니다.

1. 고객은 웹 사이트의 대화 상자를 통해 데이터 수집에 대한 동의 환경 설정을 제공합니다.
1. CMP에서 동의 환경 설정 변경을 감지하고 그에 따라 TCF 동의 데이터를 생성합니다.
1. Platform Web SDK를 사용하면 생성된 동의 데이터(CMP에서 반환)가 Adobe Experience Platform으로 전송됩니다.
1. 수집된 동의 데이터는 스키마에 TCF 동의 필드가 포함된 [!DNL Profile] 사용 데이터 세트로 수집됩니다.

CMP 동의 변경 후크에서 트리거된 SDK 명령 외에도 동의 데이터는 [!DNL Profile] 사용 데이터 세트에 직접 업로드되는 고객 생성 XDM 데이터를 통해 Experience Platform으로 유입될 수도 있습니다.

적절한 필드가 [!DNL Experience Cloud Identity Service]을(를) 통해 해당 세그먼트에 적용된 경우 Adobe Audience Manager이 [!DNL Audience Manager] 소스 커넥터 등을 통해 플랫폼과 공유하는 모든 세그먼트에도 동의 데이터가 포함될 수 있습니다. [!DNL Audience Manager]에서 동의 데이터를 수집하는 방법에 대한 자세한 내용은 [IAB TCF용 Adobe Audience Manager 플러그인](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=ko-KR)에 대한 문서를 참조하십시오.

### 다운스트림 동의 적용

TCF 동의 데이터가 성공적으로 수집되면 다운스트림 플랫폼 서비스에서 다음 프로세스가 수행됩니다.

1. [!DNL Real-Time Customer Profile]은(는) 해당 고객의 프로필에 대해 저장된 동의 데이터를 업데이트합니다.
1. Platform(565)에 대한 공급업체 권한이 클러스터의 모든 ID에 대해 제공된 경우에만 Platform이 고객 ID를 처리합니다.
1. 세그먼트를 TCF 2.0 공급업체 목록의 구성원에 속하는 대상으로 내보낼 때 Platform(565) *과(와)* 모두에 대한 공급업체 권한이 클러스터의 모든 ID에 대해 제공된 경우에만 Platform에 프로필이 포함됩니다.

이 문서의 나머지 섹션에서는 위에서 설명한 수집 및 시행 요구 사항을 충족하도록 플랫폼 및 데이터 작업을 구성하는 방법에 대한 지침을 제공합니다.

## CMP 내에서 고객 동의 데이터를 생성하는 방법 결정 {#consent-data}

각 CMP 시스템은 고유하므로 고객이 서비스와 상호 작용할 때 동의를 제공할 수 있는 최상의 방법을 결정해야 합니다. 쿠키 동의 대화 상자는 고객의 동의를 얻는 일반적인 방법입니다. 아래 CMP 대화 상자 예가 표시됩니다.

![동의 관리 플랫폼 대화 상자 예입니다.](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

이 대화 상자를 통해 고객은 다음을 옵트인하거나 옵트아웃할 수 있습니다.

| 동의 옵션 | 설명 |
| --- | --- |
| **목적** | 목적 은 브랜드가 고객 데이터를 사용할 수 있는 광고 기술 목적을 정의합니다. 플랫폼이 고객 ID를 처리하려면 다음 용도로 를 선택해야 합니다. <ul><li>**목적 1**: 장치에 대한 정보 저장 및/또는 액세스</li><li>**목적 10**: 제품 개발 및 개선</li></ul> |
| **공급업체 권한** | 광고 기술 목적 외에도 이 대화 상자를 통해 고객은 Adobe Experience Platform(565)를 비롯한 특정 공급업체에서 데이터를 사용할지 여부를 선택할 수 있어야 합니다. |

### 동의 문자열 {#consent-strings}

데이터를 수집하는 데 사용하는 방법에 관계없이 목표는 고객이 선택한 동의 옵션을 기반으로 문자열 값을 생성하는 것이며 이를 동의 문자열이라고 합니다.

TCF 사양에서 동의 문자열은 정책 및 공급업체에서 정의한 특정 마케팅 목적 측면에서 고객의 동의 설정에 대한 관련 세부 정보를 인코딩하는 데 사용됩니다. Platform은 이러한 문자열을 사용하여 각 고객에 대한 동의 설정을 저장하므로 해당 설정이 변경될 때마다 새 동의 문자열을 생성해야 합니다.

동의 문자열은 IAB TCF에 등록된 CMP에서만 만들 수 있습니다. 특정 CMP를 사용하여 동의 문자열을 생성하는 방법에 대한 자세한 내용은 IAB TCF GitHub 리포지토리의 [동의 문자열 서식 가이드](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md)를 참조하십시오.

## TCF 동의 필드를 사용하여 데이터 세트 만들기 {#datasets}

고객 동의 데이터는 스키마에 TCF 동의 필드가 포함된 데이터 세트로 전송되어야 합니다. 이 안내서를 계속하기 전에 필수 프로필 데이터 세트(및 선택적 경험 이벤트 데이터 세트)를 만드는 방법에 대한 [TCF 2.0 동의 캡처를 위한 데이터 세트 만들기](./dataset.md)에 대한 자습서를 참조하십시오.

## 동의 데이터를 포함하도록 [!DNL Profile] 병합 정책 업데이트 {#merge-policies}

동의 데이터를 수집하기 위해 [!DNL Profile] 사용 데이터 세트를 만든 후에는 고객 프로필에 항상 TCF 동의 필드를 포함하도록 병합 정책이 구성되었는지 확인해야 합니다. 여기에는 데이터 세트 우선 순위를 설정하여 동의 데이터 세트가 잠재적으로 충돌할 수 있는 다른 데이터 세트보다 우선하도록 하는 작업이 포함됩니다.

병합 정책으로 작업하는 방법에 대한 자세한 내용은 [병합 정책 개요](/help/profile/merge-policies/overview.md)를 참조하십시오. 병합 정책을 설정할 때는 데이터 세트 준비 안내서에 설명된 대로 세그먼트에 [XDM 개인 정보 보호 스키마 필드 그룹](./dataset.md#privacy-field-group)에서 제공하는 모든 필수 동의 특성이 포함되어 있는지 확인해야 합니다.

## Experience Platform 웹 SDK를 통합하여 고객 동의 데이터 수집 {#sdk}

>[!NOTE]
>
>Adobe Experience Platform에서 직접 동의 데이터를 처리하려면 Experience Platform Web SDK를 사용해야 합니다. [!DNL Experience Cloud Identity Service]은(는) 지원되지 않습니다.
>
>[!DNL Experience Cloud Identity Service]은(는) Adobe Audience Manager에서 동의 처리에 대해 계속 지원되지만 TCF 2.0을 준수하려면 라이브러리를 [버전 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases)(으)로 업데이트하기만 하면 됩니다.

동의 문자열을 생성하도록 CMP를 구성한 후에는 Experience Platform 웹 SDK를 통합하여 해당 문자열을 수집하여 플랫폼으로 보내야 합니다. Platform SDK는 TCF 동의 데이터를 Platform으로 전송하는 데 사용할 수 있는 두 가지 명령을 제공합니다(아래 하위 섹션에 설명). 이 명령은 고객이 동의 정보를 처음 제공할 때와 그 후 동의가 변경될 때 항상 사용해야 합니다.

**SDK가 기본 CMP와 인터페이스하지 않습니다**. SDK를 웹 사이트에 통합하는 방법을 결정하고 CMP에서 동의 변경 사항을 수신하고 적절한 명령을 호출하는 것은 사용자가 결정합니다.

### 데이터 스트림 만들기

SDK가 데이터를 Experience Platform으로 보내려면 먼저 플랫폼용 데이터 스트림을 만들어야 합니다. 데이터 스트림을 만드는 방법에 대한 특정 단계는 [SDK 설명서](/help/datastreams/overview.md)에 나와 있습니다.

데이터 스트림에 고유한 이름을 제공한 후 **[!UICONTROL Adobe Experience Platform]** 옆에 있는 전환 단추를 선택하십시오. 그런 다음 다음 다음 값을 사용하여 나머지 양식을 작성합니다.

| 데이터 스트림 필드 | 값 |
| --- | --- |
| [!UICONTROL 샌드박스] | 데이터 스트림을 설정하는 데 필요한 스트리밍 연결 및 데이터 세트가 포함된 Platform [sandbox](/help/sandboxes/home.md)의 이름입니다. |
| [!UICONTROL 스트리밍 인렛] | Experience Platform에 대한 유효한 스트리밍 연결입니다. 기존 스트리밍 인렛이 없는 경우 [스트리밍 연결 만들기](/help/ingestion/tutorials/create-streaming-connection-ui.md)에 대한 자습서를 참조하십시오. |
| [!UICONTROL 이벤트 데이터 세트] | [이전 단계](#datasets)에서 만든 [!DNL XDM ExperienceEvent] 데이터 세트를 선택하십시오. 이 데이터 세트의 스키마에 [[!UICONTROL IAB TCF 2.0 동의] 필드 그룹](/help/xdm/field-groups/event/iab.md)을(를) 포함한 경우 [`sendEvent`](#sendEvent) 명령을 사용하여 시간 경과에 따른 동의 변경 이벤트를 추적하여 해당 데이터를 이 데이터 세트에 저장할 수 있습니다. 이 데이터 집합에 저장된 동의 값은 자동 적용 워크플로우에서 사용되는 **not**&#x200B;입니다. |
| [!UICONTROL 프로필 데이터 세트] | [이전 단계](#datasets)에서 만든 [!DNL XDM Individual Profile] 데이터 세트를 선택하십시오. [`setConsent`](#setConsent) 명령을 사용하여 CMP 동의 변경 후크에 응답할 때 수집된 데이터가 이 데이터 집합에 저장됩니다. 이 데이터 세트는 프로필이 활성화되므로 자동 시행 워크플로 동안 이 데이터 세트에 저장된 동의 값이 적용됩니다. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

완료되면 화면 하단에서 **[!UICONTROL 저장]**&#x200B;을 선택하고 추가 프롬프트에 따라 계속 구성을 완료합니다.

### 동의 변경 명령 만들기

이전 섹션에서 설명한 데이터 스트림을 생성했으면 SDK 명령을 사용하여 동의 데이터를 Platform으로 전송할 수 있습니다. 아래 섹션에서는 각 SDK 명령을 다양한 시나리오에서 어떻게 사용할 수 있는지에 대한 예를 제공합니다.

#### CMP 동의 변경 후크 사용 {#setConsent}

많은 CMP는 동의 변경 이벤트를 수신하는 즉시 사용 가능한 후크를 제공합니다. 이러한 이벤트가 발생하면 [`setConsent`](/help/web-sdk/commands/setconsent.md) 명령을 사용하여 해당 고객의 동의 데이터를 업데이트할 수 있습니다.

`setConsent` 명령에는 두 개의 인수가 필요합니다.

1. 명령 유형을 나타내는 문자열(이 경우, &quot;setConsent&quot;).
1. `consent` 배열이 포함된 페이로드입니다. 배열에는 필수 동의 필드를 제공하는 개체가 하나 이상 있어야 합니다.

`setConsent` 명령은 아래에 표시됩니다.

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
| `standard` | 사용 중인 동의 표준입니다. TCF 2.0 동의 처리를 위해 이 값을 `IAB`(으)로 설정해야 합니다. |
| `version` | `standard` 아래에 표시된 동의 표준의 버전 번호입니다. TCF 2.0 동의 처리를 위해 이 값을 `2.0`(으)로 설정해야 합니다. |
| `value` | CMP에서 생성된 기본 64로 인코딩된 동의 문자열. |
| `gdprApplies` | GDPR이 현재 로그인한 고객에게 적용되는지 여부를 나타내는 부울 값입니다. 이 고객에 대해 TCF 2.0이 적용되려면 값을 `true`(으)로 설정해야 합니다. 정의되지 않은 경우 기본값은 `true`입니다. |

`setConsent` 명령은 동의 설정 변경을 감지하는 CMP 후크의 일부로 사용해야 합니다. 다음 JavaScript에서는 OneTrust의 `OnConsentChanged` 후크에 `setConsent` 명령을 사용하는 방법에 대한 예를 제공합니다.

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

`sendEvent` 명령을 사용하여 플랫폼에서 트리거되는 모든 이벤트에 대한 TCF 2.0 동의 데이터를 수집할 수도 있습니다.

>[!NOTE]
>
>이 메서드를 사용하려면 [!DNL Profile]이(가) 활성화된 [!DNL XDM ExperienceEvent] 스키마에 경험 이벤트 개인 정보 보호 필드 그룹을 추가해야 합니다. 구성 방법에 대한 단계는 데이터 집합 준비 안내서의 [ExperienceEvent 스키마 업데이트](./dataset.md#event-schema)에 대한 섹션을 참조하십시오.

`sendEvent` 명령은 웹 사이트의 적절한 이벤트 수신기에서 콜백으로 사용해야 합니다. 명령에는 (1) 명령 유형을 나타내는 문자열(이 경우 `sendEvent`)과 (2) 필수 동의 필드를 JSON으로 제공하는 `xdm` 개체가 포함된 페이로드의 두 가지 인수가 필요합니다.

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
| `consentStandard` | 사용 중인 동의 표준입니다. TCF 2.0 동의 처리를 위해 이 값을 `IAB`(으)로 설정해야 합니다. |
| `consentStandardVersion` | `standard` 아래에 표시된 동의 표준의 버전 번호입니다. TCF 2.0 동의 처리를 위해 이 값을 `2.0`(으)로 설정해야 합니다. |
| `consentStringValue` | CMP에서 생성된 기본 64로 인코딩된 동의 문자열. |
| `gdprApplies` | GDPR이 현재 로그인한 고객에게 적용되는지 여부를 나타내는 부울 값입니다. 이 고객에 대해 TCF 2.0이 적용되려면 값을 `true`(으)로 설정해야 합니다. 정의되지 않은 경우 기본값은 `true`입니다. |

### SDK 응답 처리

많은 웹 SDK 명령은 호출의 성공 또는 실패 여부를 나타내는 약속을 반환합니다. 그런 다음 고객에게 확인 메시지를 표시하는 것과 같은 추가 논리에 이러한 응답을 사용할 수 있습니다. 자세한 내용은 [명령 응답](/help/web-sdk/commands/command-responses.md)을 참조하세요.

## 세그먼트 내보내기 {#export}

>[!NOTE]
>
>세그먼트 내보내기를 시작하기 전에 세그먼트에 모든 필수 동의 필드가 포함되어 있는지 확인해야 합니다. 자세한 내용은 [병합 정책 구성](#merge-policies) 섹션을 참조하십시오.

고객 동의 데이터를 수집하고 필요한 동의 속성을 포함하는 대상 세그먼트를 만들었으면 해당 세그먼트를 다운스트림 대상으로 내보낼 때 TCF 2.0 준수를 적용할 수 있습니다.

고객 프로필 집합에 대해 동의 설정 `gdprApplies`이(가) `true`(으)로 설정된 경우 다운스트림 대상으로 내보낸 프로필의 모든 데이터는 각 프로필에 대한 TCF 동의 환경 설정을 기반으로 필터링됩니다. 필요한 동의 환경 설정을 충족하지 않는 프로필은 내보내기 프로세스 중에 건너뜁니다.

고객이 대상으로 내보내는 세그먼트에 프로필을 포함하려면 다음 목적([TCF 2.0 정책](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)에 설명된 대로)에 동의해야 합니다.

* **목적 1**: 장치에 대한 정보 저장 및/또는 액세스
* **목적 10**: 제품 개발 및 개선

또한 TCF 2.0을 사용하려면 데이터를 대상으로 보내기 전에 데이터 소스가 대상의 공급업체 권한을 확인해야 합니다. 따라서 Platform은 해당 대상에 바인딩된 데이터를 포함하기 전에 클러스터의 모든 ID에 대해 대상의 공급업체 권한이 로 옵트인되었는지 확인합니다.

>[!NOTE]
>
>Adobe Audience Manager과 공유되는 모든 세그먼트에는 Platform의 해당 세그먼트와 동일한 TCF 2.0 동의 값이 포함됩니다. [!DNL Audience Manager]이(가) 플랫폼(565)과 동일한 공급업체 ID를 공유하므로 동일한 목적과 공급업체 권한이 필요합니다. 자세한 내용은 [IAB TCF용 Adobe Audience Manager 플러그인](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=ko-KR)에 대한 문서를 참조하십시오.

## 구현 테스트 {#test-implementation}

TCF 2.0 구현을 구성하고 세그먼트를 대상으로 내보낸 후에는 동의 요구 사항을 충족하지 않는 데이터를 내보낼 수 없습니다. 내보내는 동안 올바른 고객 프로필이 필터링되었는지 확인하려면 대상의 데이터 저장소를 수동으로 확인하여 동의가 제대로 적용되었는지 확인해야 합니다.

>[!IMPORTANT]
>
>여러 ID가 클러스터를 구성하고 TCF 2.0이 적용되는 경우, 단일 ID에 올바른 목적과 공급업체 권한이 포함되지 않은 경우 전체 클러스터가 제외됩니다.

## 다음 단계

이 문서에서는 TCF 2.0에 설명된 대로 비즈니스 의무를 충족하도록 플랫폼 데이터 작업을 구성하는 프로세스에 대해 다룹니다. Platform의 개인 정보 보호 관련 기능에 대한 자세한 내용은 [거버넌스, 개인 정보 보호 및 보안에 대한 개요](../../overview.md)를 참조하십시오.
