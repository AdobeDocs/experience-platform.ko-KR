---
keywords: Experience Platform;home;IAB;IAB 2.0;
solution: Experience Platform
title: 실시간 고객 데이터 플랫폼의 IAB TCF 2.0 지원
topic: privacy events
translation-type: tm+mt
source-git-commit: 06eda1502d34da1caeebbe9b753dd437bbd9d6ab
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 1%

---


# IAB TCF 2.0 지원 [!DNL Real-time Customer Data Platform]

IAB( [!DNL Transparency & Consent Framework] TCF) [!DNL Interactive Advertising Bureau] 가 설명한 바와 같이, TCF는 조직이 유럽 연합의 [!DNL General Data Protection Regulation] (GDPR)에 따라 개인 데이터 처리에 대한 소비자 동의를 얻고, 기록하고, 업데이트할 수 있도록 하기 위한 개방형 표준 기술 프레임워크입니다. 프레임워크의 두 번째 반복인 TCF 2.0은 공급업체가 정확한 지리적 위치와 같은 데이터 처리 기능의 특정 기능을 사용할 수 있는지 여부 및 방법을 포함하여 소비자의 동의 제공 또는 거부 방법에 대한 유연성을 높여줍니다.

>[!NOTE]
>
>TCF 2.0에 대한 자세한 내용은 지원 자료와 기술 사양 등 [IAB 유럽 웹](https://iabeurope.eu/tcf-2-0/)사이트에서 확인할 수 있습니다.

[!DNL Real-time Customer Data Platform (Real-time CDP)] 은 ID [565](https://iabeurope.eu/vendor-list-tcf-v2-0/)아래에 등록된 IAB TCF 2.0 공급업체 목록 ****&#x200B;중 일부입니다. TCF 2.0 요구 사항을 준수하여 고객 동의 데이터를 수집하고 저장된 고객 프로파일에 통합할 수 [!DNL Real-time CDP] 있습니다. 그런 다음 사용 사례에 따라 프로파일을 내보낸 대상 세그먼트에 포함할지 여부를 이 동의 데이터를 포함할 수 있습니다.

>[!IMPORTANT]
>
>[!DNL Real-time CDP] 은 TCF 버전 2.0 이상만 준수할 수 있습니다. 이전 버전의 TCF는 지원되지 않습니다.

이 문서에서는 데이터 작업 및 프로필 스키마를 구성하여 CMP에서 생성된 고객 동의 데이터를 받아들이는 방법과 세그먼트를 내보낼 때 사용자 동의 선택 사항을 전달하는 방법에 대한 개요를 제공합니다. [!DNL Real-time CDP]

## 전제 조건

이 안내서를 준수하려면 IAB TCF와 통합되고 규정을 준수하는 CMP(Consent Management Platform)를 사용해야 합니다. 자세한 내용은 [호환 CMP](https://iabeurope.eu/cmp-list/) 목록을 참조하십시오.

>[!IMPORTANT]
>
>CMP의 ID가 유효하지 않은 경우 데이터를 그대로 [!DNL Real-time CDP] 처리합니다. TCF 2.0을 적용하려면 데이터를 보내기 전에 CMP에 IAB TCF 2.0에 등록된 유효한 ID가 있는지 확인해야 합니다 [!DNL Experience Platform].

또한 이 가이드는 다음 Adobe Experience Platform 서비스에 대한 작업 이해를 필요로 합니다.

* [XDM(Experience Data Model)](../../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
* [Adobe Experience Platform ID 서비스](../../../identity-service/home.md):다양한 디바이스와 시스템에 ID를 연결하여 고객 경험 데이터의 세분화로 인한 기본적인 문제를 해결합니다.
* [실시간 고객 프로필](../../../profile/home.md):데이터 세트 [!DNL Identity Service] 에서 실시간으로 세부 고객 프로파일을 생성합니다. [!DNL Real-time Customer Profile] 데이터 레이크에서 데이터를 가져와 별도의 데이터 저장소에 고객 프로파일을 유지합니다.
* [Adobe Experience Platform 웹 SDK](../../../edge/home.md):다양한 [!DNL Platform] 서비스를 고객 중심의 웹 사이트에 통합할 수 있는 클라이언트측 JavaScript 라이브러리
   * [SDK 동의 명령](../../../edge/fundamentals/supporting-consent.md):이 안내서에 나와 있는 동의 관련 SDK 명령의 사용 사례 개요입니다.
* [Adobe Experience Platform 세그멘테이션 서비스](../../../segmentation/home.md):비슷한 트레이트를 공유하고 마케팅 전략과 유사하게 반응하는 개인 그룹으로 [!DNL Real-time Customer Profile] 데이터를 나눌 수 있습니다.

위에 나열된 [!DNL Platform] 서비스 외에도, 목적지 [](../../destinations/destinations-overview.md) 및 서비스 사용에 대해 잘 알고 있어야 합니다 [!DNL Real-time CDP].

## 고객 동의 흐름 요약 {#summary}

다음 섹션에서는 시스템이 적절하게 구성된 후 동의 데이터가 수집 및 수행되는 방법을 설명합니다.

### 동의 데이터 수집

[!DNL Real-time CDP] 다음 프로세스를 통해 고객 동의 데이터를 수집할 수 있습니다.

1. 고객은 웹 사이트의 대화 상자를 통해 데이터 수집에 대한 동의 환경 설정을 제공합니다.
1. CMP는 동의 환경 설정 변경을 감지하고 그에 따라 IAB 동의 데이터를 생성합니다.
1. 를 사용하여 [!DNL Experience Platform Web SDK]생성된 동의 데이터(CMP에서 반환)가 Adobe Experience Platform으로 전송됩니다.
1. 수집된 동의 데이터는 스키마에 IAB 동의 필드가 포함된 [!DNL Profile]사용 가능한 데이터 세트에 수집됩니다.

CMP 동의-변경 갈등에 의해 트리거되는 SDK 명령 외에도 동의 데이터는 고객이 생성한 XDM 데이터 [!DNL Experience Platform] 를 통해 전달되어 데이터 [!DNL Profile]지원 데이터 세트에 직접 업로드됩니다.

Adobe Audience Manager [!DNL Platform] 가 공유한 모든 세그먼트(소스 커넥터 또는 기타 다른 방법을 통해)는 동의 데이터도 포함할 수 있습니다. 단, 해당 필드가 을 통해 해당 세그먼트에 적용되었다면 이 데이터도 포함할 수 [!DNL Audience Manager] [!DNL Experience Cloud Identity Service]있습니다. 동의서 데이터 수집에 대한 자세한 내용 [!DNL Audience Manager]은 IAB TCF용 [Adobe Audience Manager 플러그인에 있는 문서를 참조하십시오](https://docs.adobe.com/help/ko-KR/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### 다운스트림 동의 집행

IAB 동의 데이터가 수집되면 다운스트림 [!DNL Real-time CDP] 서비스에서 다음 프로세스가 수행됩니다.

1. [!DNL Real-time Customer Profile] 고객 프로필에 대해 저장된 동의 데이터를 업데이트합니다.
1. [!DNL Real-time CDP] 클러스터의 모든 ID에 대한 공급업체 권한 [!DNL Real-time CDP] (565)이 제공되는 경우에만 고객 ID를 처리합니다.
1. 세그먼트를 TCF 2.0 공급업체 목록의 멤버에 속하는 대상으로 내보낼 때, 클러스터 내 모든 ID에 대해 공급업체 권한 [!DNL Real-time CDP] (565) [!DNL Real-time CDP] 과 *대상이 모두 제공되는 경우에만* 프로필이 포함됩니다.

이 문서의 나머지 섹션에서는 위에서 설명한 수집 및 적용 요구 사항을 충족하기 위해 구성 방법 [!DNL Real-time CDP] 과 데이터 작업에 대한 지침을 제공합니다.

## CMP 내에서 고객 동의 데이터를 생성하는 방법 결정 {#consent-data}

각 CMP 시스템이 고유하므로 고객이 서비스와 상호 작용할 때 동의를 제공할 수 있는 최상의 방법을 결정해야 합니다. 이를 실현하는 일반적인 방법은 다음 예와 유사한 쿠키 동의 대화 상자를 사용하는 것입니다.

![](../assets/iab/cmp-dialog.png)

이 대화 상자에서는 고객이 다음 중 선택하여 들어오거나 나갈 수 있어야 합니다.

| 동의 옵션 | 설명 |
| --- | --- |
| **목적** | 목적은 브랜드가 고객의 데이터를 사용할 수 있는 광고 기술 목적을 정의합니다. 고객 ID를 처리하려면 다음 목적 [!DNL Real-time CDP] 을 선택해야 합니다. <ul><li>**목적 1**:장치에 정보 저장 및/또는 액세스</li><li>**목적 10**:제품 개발 및 개선</li></ul> |
| **공급업체 권한** | 또한 광고 기술 목적 외에 고객이 (565)을 비롯한 특정 공급업체에서 자신의 데이터를 사용하는지 여부를 선택할 수 있도록 [!DNL  Real-time CDP] 해야 합니다. |

### 동의 문자열 {#consent-strings}

데이터를 수집하는 데 사용하는 방법에 관계없이, 목표는 고객이 선택한 **동의 문자열**(consent string)을 기반으로 문자열 값을 생성하는 것입니다.

TCF 사양에서 동의 문자열은 정책과 공급업체에서 정의한 특정 마케팅 목적을 기준으로 고객의 동의 설정에 대한 관련 세부 정보를 인코딩하는 데 사용됩니다. [!DNL Real-time CDP] 이러한 문자열을 사용하여 각 고객에 대한 동의 설정을 저장하므로 해당 설정이 변경될 때마다 새 동의 문자열을 생성해야 합니다.

동의 문자열은 IAB TCF에 등록된 CMP에서만 만들 수 있습니다. 특정 CMP를 사용하여 동의 문자열을 생성하는 방법에 대한 자세한 내용은 IAB TCF GitHub 보고서의 [동의 문자열 서식 지정](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) 안내서를 참조하십시오.

## IAB 동의 필드를 사용하여 데이터 집합 만들기 {#datasets}

스키마에 IAB 동의 필드가 포함된 데이터 세트로 고객 동의 데이터를 보내야 합니다. 이 가이드를 계속하기 전에 두 개의 필수 데이터 세트를 만드는 방법에 대한 TCF 2.0 동의 [](./dataset-preparation.md) 를 캡처하기 위한 데이터 세트를 만드는 방법에 대한 자습서를 참조하십시오.

## 동의 데이터를 포함하도록 병합 [!DNL Profile] 정책 업데이트 {#merge-policies}

동의 데이터를 수집하기 위해 [!DNL Profile]활성화된 데이터 세트를 만들었다면 병합 정책이 고객 프로필에 항상 IAB 동의 필드를 포함하도록 구성되었는지 확인해야 합니다. 여기에는 데이터 세트 우선 순위를 설정하여 동의 데이터 세트에 대해 충돌을 일으킬 수 있는 다른 데이터 세트에 비해 우선 순위가 지정됩니다.

병합 정책을 사용하는 방법에 대한 자세한 내용은 [병합 정책 사용 안내서를 참조하십시오](../../../profile/ui/merge-policies.md). 병합 정책을 설정할 때 데이터 세트 준비 가이드에 나와 있는 바와 같이, 세그먼트에 [XDM 개인 정보 혼합에서](./dataset-preparation.md#privacy-mixin)제공하는 모든 필수 동의 속성이 포함되도록 해야 합니다.

## 웹 [!DNL Experience Platform] SDK를 통합하여 고객 동의 데이터 수집 {#sdk}

>[!NOTE]
>
>Adobe Experience Platform에서 직접 동의 데이터를 처리하기 위해 [!DNL Experience Platform] 웹 SDK를 사용해야 합니다. [!DNL Experience Cloud Identity Service] 은 현재 지원되지 않습니다.
>
>[!DNL Experience Cloud Identity Service] 그러나 은(는) Adobe Audience Manager의 동의 처리를 위해 여전히 지원되며, TCF 2.0을 준수하려면 라이브러리가 [버전 5.0으로 업데이트되어야 합니다](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

동의 문자열을 생성하도록 CMP를 구성한 후에는 [!DNL Experience Platform] 웹 SDK를 통합하여 이러한 문자열을 수집하여 전달해야 합니다 [!DNL Platform]. SDK는 [!DNL Platform] IAB 동의 데이터를 플랫폼에 보내는 데 사용할 수 있는 두 가지 명령(아래 하위 섹션에 설명됨)을 제공하며, 고객이 처음 동의 정보를 제공할 때와 이후 동의 내용이 변경될 때마다 사용해야 합니다.

**SDK는 특별한 CMP와 연결되지 않습니다**. SDK를 웹 사이트에 통합하는 방법을 결정하고, CMP에서 동의 변경 사항을 수신하고, 적절한 명령을 호출하는 방법은 전적으로 사용자에게 달려 있습니다.

### 새 에지 구성 만들기

SDK에서 데이터를 전송하려면 [!DNL Experience Platform], 먼저 에 대한 새 Edge 구성 [!DNL Platform] 을 만들어야 합니다 [!DNL Adobe Experience Platform Launch]. 새 구성을 만드는 방법에 대한 특정 단계는 [SDK 설명서에서 제공됩니다](../../../edge/fundamentals/edge-configuration.md).

구성에 고유한 이름을 제공한 후 *[!UICONTROL Adobe Experience Platform]*&#x200B;옆에 있는 전환 단추를 선택합니다. 다음 값을 사용하여 양식의 나머지 부분을 완료합니다.

| Edge 구성 필드 | 값 |
| --- | --- |
| [!UICONTROL 샌드박스] | 에지 구성을 설정하는 데 필요한 스트리밍 연결 및 데이터 세트를 포함하는 [!DNL Platform] 샌드박스 [](../../../sandboxes/home.md) 이름입니다. |
| [!UICONTROL 스트리밍 입구] | 유효한 스트리밍 연결 [!DNL Experience Platform]. 기존 스트리밍 유입 [이 없는 경우 스트리밍 연결](../../../ingestion/tutorials/create-streaming-connection-ui.md) 만들기에 대한 자습서를 참조하십시오. |
| [!UICONTROL 이벤트 데이터 집합] | [!DNL XDM ExperienceEvent] 이전 단계 [](#datasets)에서 만든 데이터 세트를 선택합니다. |
| [!UICONTROL 프로필 데이터 집합] | [!DNL XDM Individual Profile] 이전 단계 [](#datasets)에서 만든 데이터 세트를 선택합니다. |

![](../assets/iab/edge-config.png)

완료되면 **[!UICONTROL 화면]** 하단에 있는 저장을 클릭하고 추가 지시에 따라 구성을 완료합니다.

### 동의-변경 명령

이전 섹션에 설명된 Edge 구성을 만들었다면 SDK 명령을 사용하여 동의 데이터를 보낼 수 있습니다 [!DNL Platform]. 아래 섹션에서는 다양한 시나리오에서 각 SDK 명령을 사용할 수 있는 방법의 예를 제공합니다.

>[!NOTE]
>
>모든 SDK 명령에 대한 일반적인 구문에 대한 소개는 명령 [!DNL Platform] 실행에 관한 문서를 [참조하십시오](../../../edge/fundamentals/executing-commands.md).

#### CMP 동의-변경 후크 사용

많은 CMP는 동의-변경 이벤트를 듣는 즉시 사용 가능한 갈고리를 제공합니다. 이러한 이벤트가 발생하면 `setConsent` 명령을 사용하여 해당 고객의 동의 데이터를 업데이트할 수 있습니다.

명령은 다음 두 개의 인수를 `setConsent` 예상합니다.(1) 명령 유형(이 경우 &quot;setConsent&quot;)을 나타내는 문자열 및 (2) 필수 동의 필드를 제공하는 개체가 하나 이상 있어야 하는 `consent` 배열이 포함된 페이로드를 나타냅니다.

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
| `standard` | 사용 중인 동의 표준. TCF 2.0 동의 처리를 위해서는 이 값을 &quot;IAB&quot;로 설정해야 합니다. |
| `version` | 아래에 명시된 동의 표준의 버전 번호 `standard`. TCF 2.0 동의 처리를 위해서는 이 값을 &quot;2.0&quot;으로 설정해야 합니다. |
| `value` | CMP에서 생성된 기본 64로 인코딩된 동의 문자열. |
| `gdprApplies` | 현재 로그인한 고객에게 GDPR이 적용되는지 여부를 나타내는 부울 값입니다. 이 고객에게 TCF 2.0이 적용되려면 이 값을 &quot;true&quot;로 설정해야 합니다. |

이 `setConsent` 명령은 동의 설정의 변경 사항을 감지하는 CMP 후크의 일부로 사용해야 합니다. 다음 JavaScript는 OneTrust의 후크에 `setConsent` `OnConsentChanged` 명령을 사용할 수 있는 방법의 예를 제공합니다.

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

#### 이벤트 사용

또한 명령을 사용하여 트리거되는 모든 이벤트에 대해 TCF 2.0 동의 데이터 [!DNL Platform] 를 수집할 수 `sendEvent` 있습니다.

>[!NOTE]
>
>이 메서드를 사용하려면 이 메서드를 사용 가능한 스키마 [!DNL Experience Event Privacy mixin] 에 [!DNL Profile]추가해야 [!DNL XDM ExperienceEvent] 합니다. 이 구성 방법에 대한 단계는 데이터 집합 준비 안내서의 ExperienceEvent 스키마 [](./dataset-preparation.md#event-schema) 업데이트에 대한 섹션을 참조하십시오.

이 `sendEvent` 명령은 웹 사이트에서 적절한 이벤트 리스너에 있는 콜백으로 사용해야 합니다. 명령에는 두 개의 인수가 필요합니다.(1) 명령 유형(이 경우 &quot;sendEvent&quot;)을 나타내는 문자열 및 (2) 필수 동의 필드를 JSON으로 제공하는 `xdm` 개체가 포함된 페이로드:

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
| `consentStandard` | 사용 중인 동의 표준. TCF 2.0 동의 처리를 위해서는 이 값을 &quot;IAB&quot;로 설정해야 합니다. |
| `consentStandardVersion` | 아래에 명시된 동의 표준의 버전 번호 `standard`. TCF 2.0 동의 처리를 위해서는 이 값을 &quot;2.0&quot;으로 설정해야 합니다. |
| `consentStringValue` | CMP에서 생성된 기본 64로 인코딩된 동의 문자열. |
| `gdprApplies` | 현재 로그인한 고객에게 GDPR이 적용되는지 여부를 나타내는 부울 값입니다. 이 고객에게 TCF 2.0이 적용되려면 이 값을 &quot;true&quot;로 설정해야 합니다. |

### SDK 응답 처리

모든 [!DNL Platform SDK] 명령은 호출이 성공했는지 실패했는지 여부를 나타내는 약속을 반환합니다. 그런 다음 이러한 응답을 고객에게 확인 메시지 표시와 같은 추가 로직에 사용할 수 있습니다. 특정 예제에 대한 SDK 명령 [실행에 대한 안내서의 성공 또는 실패](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 처리에 대한 섹션을 참조하십시오.

## 세그먼트 내보내기 {#export}

>[!NOTE]
>
>세그먼트 내보내기를 시작하기 전에 세그먼트에 모든 필수 동의 필드가 포함되어 있어야 합니다. 자세한 내용은 병합 정책 [구성에](#merge-policies) 대한 섹션을 참조하십시오.

고객 동의 데이터를 수집하고 필수 동의 속성이 포함된 대상 세그먼트를 만들면 해당 세그먼트를 다운스트림 대상으로 내보낼 때 TCF 2.0 규정 준수를 적용할 수 있습니다.

고객 프로필 집합에 대해 동의 설정 `gdprApplies` 이 설정되어 `true` 있는 경우, 다운스트림 대상으로 내보낸 프로필의 데이터는 각 프로필에 대한 동의 기본 설정에 따라 필터링됩니다. 필요한 동의 환경 설정에 맞지 않는 모든 프로파일은 내보내기 프로세스 중에 건너뜁니다.

대상으로 내보낸 세그먼트에 자신의 프로파일을 포함하려면 고객은 다음 목적( [TCF 2.0 정책에](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)따라 설명)에 동의해야 합니다.

* **목적 1**:장치에 정보 저장 및/또는 액세스
* **목적 10**:제품 개발 및 개선

또한 TCF 2.0에서는 데이터를 대상에 보내기 전에 데이터 소스가 대상의 공급업체 권한을 확인해야 합니다. 이와 같이 대상에 바인딩된 데이터를 포함하기 전에 클러스터의 모든 ID에 대해 대상의 공급업체 권한이 옵트인되었는지 [!DNL Real-time CDP] 확인합니다.

>[!NOTE]
>
>Adobe Audience Manager과 공유되는 모든 세그먼트에는 해당 항목과 동일한 TCF 2.0 동의 값이 [!DNL Platform] 포함됩니다. (565)와 동일한 공급업체 ID를 [!DNL Audience Manager] 공유하므로 [!DNL Real-time CDP] 동일한 목적과 공급업체 권한이 필요합니다. 자세한 내용은 IAB TCF용 [Adobe Audience Manager 플러그인의 문서를](https://docs.adobe.com/help/ko-KR/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) 참조하십시오.

## Test your implementation {#test-implementation}

TCF 2.0 구현을 구성하고 세그먼트를 대상으로 내보내면 동의 요구 사항을 충족하지 않는 데이터는 내보내지지 않습니다. 그러나 내보내기 중에 올바른 고객 프로필이 필터링되었는지 확인하려면 대상의 데이터 저장소를 수동으로 확인하여 동의 내용이 제대로 적용되었는지 확인해야 합니다.

여러 ID가 클러스터를 구성하고 TCF 2.0이 적용되는 경우 단일 ID에도 올바른 목적과 공급업체 권한이 없는 경우 전체 클러스터가 제외됩니다.

## 다음 단계

이 문서에서는 TCF 2.0과 호환되도록 데이터 작업 [!DNL Real-time CDP] [!DNL Real-time CDP]을 구성하는 프로세스에 대해 설명합니다.

* [실시간 CDP의 개인 정보 보호](../privacy-overview.md)
* [실시간 CDP의 데이터 거버넌스](../data-governance-overview.md)