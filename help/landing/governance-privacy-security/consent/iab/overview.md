---
keywords: Experience Platform;홈;IAB;IAB 2.0;동의;동의
solution: Experience Platform
title: Experience Platform에서 IAB TCF 2.0 지원
topic-legacy: privacy events
description: 세그먼트를 Adobe Experience Platform의 대상에 활성화할 때 고객 동의 선택 사항을 전달하도록 데이터 작업 및 스키마를 구성하는 방법을 알아봅니다.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2459'
ht-degree: 0%

---

# Experience Platform에서 IAB TCF 2.0 지원

[!DNL Transparency & Consent Framework](TCF)는 [!DNL Interactive Advertising Bureau](IAB)에 의해 설명한 바와 같이, 조직이 유럽 연합의 [!DNL General Data Protection Regulation](GDPR)에 따라 개인 데이터 처리에 대한 소비자 동의를 얻고, 기록하고, 업데이트할 수 있도록 하기 위한 개방형 표준 기술 프레임워크입니다. 프레임워크의 두 번째 반복인 TCF 2.0은 벤더가 정확한 지리적 위치와 같은 데이터 처리 기능의 특정 기능을 사용할 수 있는지 여부 및 방법을 포함하여 고객의 동의를 제공하거나 거부할 수 있는 방법에 대한 유연성을 더욱 높여줍니다.

>[!NOTE]
>
>TCF 2.0에 대한 자세한 내용은 지원 자료 및 기술 사양 등 [IAB Europe 웹 사이트](https://iabeurope.eu/tcf-2-0/)에서 확인할 수 있습니다.

Adobe Experience Platform은 ID **565**&#x200B;에서 등록된 [IAB TCF 2.0 공급업체 목록](https://iabeurope.eu/vendor-list-tcf-v2-0/)의 일부입니다. TCF 2.0 요구 사항을 준수하는 Platform을 사용하면 고객 동의 데이터를 수집하여 저장된 고객 프로파일에 통합할 수 있습니다. 사용 사례에 따라 이 동의 데이터를 내보낸 대상 세그먼트에 프로필이 포함되는지 여부에 포함시킬 수 있습니다.

>[!IMPORTANT]
>
>플랫폼은 TCF 버전 2.0 이상을 준수해야만 합니다. 이전 버전의 TCF는 지원되지 않습니다.

이 문서에서는 데이터 작업 및 프로필 스키마를 구성하여 CMP에서 생성된 고객 동의 데이터를 받아들이는 방법, 세그먼트를 내보낼 때 플랫폼에서 사용자 동의 선택 사항을 전달하는 방법에 대한 개요를 제공합니다.

## 전제 조건

이 안내서를 준수하려면 IAB TCF와 통합되어 있고 규정을 준수하는 CMP(Consent Management Platform)를 사용해야 합니다. 자세한 내용은 [호환 CMP 목록](https://iabeurope.eu/cmp-list/)을 참조하십시오.

>[!IMPORTANT]
>
>CMP의 ID가 유효하지 않은 경우 플랫폼은 데이터를 그대로 처리합니다. TCF 2.0을 적용하려면 Platform으로 데이터를 보내기 전에 CMP에 IAB TCF 2.0에 등록된 유효한 ID가 있는지 확인해야 합니다.

또한 이 안내서를 보려면 다음 플랫폼 서비스에 대한 충분한 지식이 있어야 합니다.

* [경험 데이터 모델(XDM)](../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [Adobe Experience Platform ID 서비스](../../../../identity-service/home.md):디바이스 및 시스템 간의 ID를 결합함으로써 고객 경험 데이터의 세분화로 인해 발생하는 기본적인 문제를 해결합니다.
* [실시간 고객 프로필](../../../../profile/home.md):데이터 세트 [!DNL Identity Service] 에서 실시간으로 상세한 고객 프로파일을 만들 수 있습니다. [!DNL Real-time Customer Profile] 데이터 레이크에서 데이터를 가져와 별도의 데이터 저장소에 있는 고객 프로파일을 유지합니다.
* [Adobe Experience Platform 웹 SDK](../../../../edge/home.md):다양한 플랫폼 서비스를 고객 중심의 웹 사이트에 통합할 수 있는 클라이언트측 JavaScript 라이브러리입니다.
   * [SDK 동의 명령](../../../../edge/consent/supporting-consent.md):이 안내서에 나와 있는 동의 관련 SDK 명령의 사용 사례 개요입니다.
* [Adobe Experience Platform 세그멘테이션 서비스](../../../../segmentation/home.md):비슷한 트레이트를 공유하고 마케팅 전략에  [!DNL Real-time Customer Profile] 비슷하게 반응할 개인 그룹으로 데이터를 나눌 수 있습니다.

위에 나열된 플랫폼 서비스 외에도 [destinations](../../../../data-governance/home.md)와 플랫폼 에코시스템에서의 해당 역할에 대해 잘 알고 있어야 합니다.

## 고객 동의 흐름 요약 {#summary}

다음 섹션에서는 시스템이 제대로 구성된 후 동의 데이터를 수집하고 적용하는 방법을 설명합니다.

### 동의 데이터 수집

플랫폼을 사용하면 다음 프로세스를 통해 고객 동의 데이터를 수집할 수 있습니다.

1. 고객은 웹 사이트의 대화 상자를 통해 데이터 수집에 대한 동의 기본 설정을 제공합니다.
1. CMP는 동의 환경 설정 변경을 감지하고 그에 따라 TCF 동의 데이터를 생성합니다.
1. 플랫폼 웹 SDK를 사용하여 생성된 동의 데이터(CMP에서 반환)가 Adobe Experience Platform으로 전송됩니다.
1. 수집된 동의 데이터는 스키마에 TCF 동의 필드가 포함된 [!DNL Profile] 사용 가능한 데이터 세트에 수집됩니다.

CMP 동의-변경 갈고리로 트리거되는 SDK 명령 외에도 동의 데이터는 고객이 생성한 XDM 데이터를 통해 Experience Platform으로 전달될 수 있으며, 이 데이터는 [!DNL Profile] 사용 가능한 데이터세트에 직접 업로드됩니다.

Adobe Audience Manager에서 플랫폼([!DNL Audience Manager] 소스 커넥터 또는 기타 다른 방법을 통해)과 공유되는 모든 세그먼트에는 동의 데이터도 포함될 수 있습니다. 단, 해당 필드가 [!DNL Experience Cloud Identity Service]을(를) 통해 해당 세그먼트에 적용되었음. [!DNL Audience Manager]에서 동의 데이터를 수집하는 방법에 대한 자세한 내용은 IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)용 [Adobe Audience Manager 플러그인의 문서를 참조하십시오.

### 다운스트림 동의 집행

TCF 동의 데이터를 성공적으로 인제스트하면 다운스트림 플랫폼 서비스에서 다음 프로세스가 발생합니다.

1. [!DNL Real-time Customer Profile] 해당 고객 프로필에 대해 저장된 동의 데이터를 업데이트합니다.
1. 플랫폼의 모든 ID에 대해 공급업체 권한(565)이 제공된 경우에만 플랫폼에서 고객 ID를 처리합니다.
1. 세그먼트를 TCF 2.0 공급업체 목록의 멤버에 속하는 대상으로 내보낼 때 Platform(플랫폼)(565) *과* 모두에 대한 공급업체 권한이 클러스터의 모든 ID에 대해 제공될 경우에만 플랫폼에 프로파일이 포함됩니다.

이 문서의 나머지 섹션에서는 위에서 설명한 수집 및 적용 요건을 충족하기 위해 플랫폼 및 데이터 작업을 구성하는 방법에 대한 지침을 제공합니다.

## CMP {#consent-data} 내에서 고객 동의 데이터를 생성하는 방법 결정

각 CMP 시스템이 고유하므로 고객이 서비스와 상호 작용할 때 동의를 제공할 수 있는 최상의 방법을 결정해야 합니다. 이를 실현하는 일반적인 방법은 다음 예와 유사한 쿠키 동의 대화 상자를 사용하는 것입니다.

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

이 대화 상자를 통해 고객이 다음 옵션 중 하나를 옵트인 또는 옵트아웃할 수 있습니다.

| 동의 옵션 | 설명 |
| --- | --- |
| **목적** | 목적은 브랜드가 고객의 데이터를 사용할 수 있는 광고 기술 목적을 정의합니다. 플랫폼에서 고객 ID를 처리하려면 다음 목적을 고려해야 합니다. <ul><li>**목적 1**:장치에 정보 저장 및/또는 액세스</li><li>**목적 10**:제품 개발 및 개선</li></ul> |
| **공급업체 권한** | 광고 기술 목적 이외에도, 이 대화 상자를 통해 고객이 Adobe Experience Platform(565)를 비롯한 특정 공급업체에서 사용하는 데이터를 수신 또는 거부할 수 있습니다. |

### 동의 문자열 {#consent-strings}

데이터를 수집하는 데 사용하는 방법에 상관없이, 목표는 고객이 선택한 동의 옵션(동의 문자열)을 기반으로 문자열 값을 생성하는 것입니다.

TCF 사양에서 동의 문자열은 정책과 공급업체에서 정의한 특정 마케팅 목적에 따라 고객의 동의 설정에 대한 관련 세부 정보를 인코딩하는 데 사용됩니다. 플랫폼은 이러한 문자열을 사용하여 각 고객의 동의 설정을 저장하므로 해당 설정이 변경될 때마다 새 동의 문자열을 생성해야 합니다.

동의 문자열은 IAB TCF에 등록된 CMP에서만 만들 수 있습니다. 특정 CMP를 사용하여 동의 문자열을 생성하는 방법에 대한 자세한 내용은 IAB TCF GitHub 보고서의 [동의 문자열 서식 지정 안내서](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md)를 참조하십시오.

## TCF 동의 필드가 {#datasets}인 데이터 집합 만들기

고객 동의 데이터는 스키마에 TCF 동의 필드가 들어 있는 데이터 세트로 전송해야 합니다. 이 안내서를 계속하기 전에 TCF 2.0 동의](./dataset.md)을(를) 캡처하기 위한 데이터 세트 만들기에 대한 자습서를 참조하십시오.[

## 동의 데이터 {#merge-policies}를 포함하도록 [!DNL Profile] 병합 정책을 업데이트합니다.

동의 데이터를 수집하기 위해 [!DNL Profile] 사용 가능한 데이터 세트를 만들었으면 병합 정책이 고객 프로필에 항상 TCF 동의 필드를 포함하도록 구성되어 있는지 확인해야 합니다. 데이터세트의 우선 순위를 설정하여 잠재적으로 충돌하는 다른 데이터세트보다 동의 데이터 세트에 대한 우선 순위를 지정합니다.

병합 정책을 사용하는 방법에 대한 자세한 내용은 [병합 정책 사용 안내서](../../../../profile/ui/merge-policies.md)를 참조하십시오. 병합 정책을 설정할 때 데이터 집합 준비에 대한 안내서에 설명된 대로, 세그먼트에 [XDM 개인 정보 믹싱](./dataset.md#privacy-mixin)에서 제공하는 모든 필수 동의 속성이 포함되도록 해야 합니다.

## Experience Platform 웹 SDK를 통합하여 고객 동의 데이터 {#sdk} 수집

>[!NOTE]
>
>Adobe Experience Platform에서 동의 데이터를 직접 처리하려면 Experience Platform 웹 SDK를 사용해야 합니다. [!DNL Experience Cloud Identity Service] 은(는) 현재 지원되지 않습니다.
>
>[!DNL Experience Cloud Identity Service] 는 Adobe Audience Manager의 동의 처리를 위해 여전히 지원되지만 TCF 2.0을 준수하려면 라이브러리가  [버전 5.0으로 업데이트되어야 합니다](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

동의 문자열을 생성하도록 CMP를 구성한 후에는 Experience Platform 웹 SDK를 통합하여 이러한 문자열을 수집하여 플랫폼으로 보내야 합니다. 플랫폼 SDK는 TCF 동의 데이터를 플랫폼에 보내는 데 사용할 수 있는 두 가지 명령(아래 하위 섹션에 설명됨)을 제공하며, 고객이 처음 동의 정보를 제공할 때와 이후 동의 내용이 변경될 때마다 사용해야 합니다.

**SDK는 특별히 제공되는 CMP와 연결되지 않습니다**. SDK를 웹 사이트에 통합하는 방법을 결정하고, CMP의 동의 변경 사항을 수신하고, 적절한 명령을 호출하는 방법은 귀하에게 달려 있습니다.

### 새 에지 구성 만들기

SDK가 데이터를 Experience Platform으로 전송하려면 먼저 [!DNL Adobe Experience Platform Launch]에서 플랫폼에 대한 새 에지 구성을 만들어야 합니다. 새 구성을 만드는 방법에 대한 특정 단계는 [SDK 설명서](../../../../edge/fundamentals/edge-configuration.md)에서 제공됩니다.

구성에 대한 고유한 이름을 제공한 후 **[!UICONTROL Adobe Experience Platform]** 옆에 있는 전환 단추를 선택합니다. 그런 다음 다음 다음 값을 사용하여 나머지 양식을 완료합니다.

| Edge 구성 필드 | 값 |
| --- | --- |
| [!UICONTROL Sandbox] | 에지 구성을 설정하는 데 필요한 스트리밍 연결 및 데이터 세트가 포함된 플랫폼 [샌드박스](../../../../sandboxes/home.md)의 이름입니다. |
| [!UICONTROL Streaming Inlet] | Experience Platform에 대한 유효한 스트리밍 연결 기존 스트리밍 입구가 없는 경우 [스트리밍 연결 만들기](../../../../ingestion/tutorials/create-streaming-connection-ui.md)에서 자습서를 참조하십시오. |
| [!UICONTROL Event Dataset] | [이전 단계](#datasets)에서 만든 [!DNL XDM ExperienceEvent] 데이터 집합을 선택합니다. |
| [!UICONTROL Profile Dataset] | [이전 단계](#datasets)에서 만든 [!DNL XDM Individual Profile] 데이터 집합을 선택합니다. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

완료되면 화면 하단에 있는 **[!UICONTROL Save]**&#x200B;을 선택하고 구성을 완료하라는 추가 지침을 계속 따릅니다.

### 동의 변경 명령 만들기

이전 섹션에 설명된 Edge 구성을 만들었으면 SDK 명령을 사용하여 동의 데이터를 플랫폼에 보낼 수 있습니다. 아래 섹션에서는 다양한 시나리오에서 각 SDK 명령을 사용할 수 있는 방법의 예를 제공합니다.

>[!NOTE]
>
>모든 플랫폼 SDK 명령에 대한 일반적인 구문에 대한 소개는 [명령 실행](../../../../edge/fundamentals/executing-commands.md)에 있는 문서를 참조하십시오.

#### CMP 동의-변경 후크 사용

많은 CMP는 동의 변경 이벤트를 듣는 즉시 사용 가능한 갈고리를 제공합니다. 이러한 이벤트가 발생하면 `setConsent` 명령을 사용하여 고객의 동의 데이터를 업데이트할 수 있습니다.

`setConsent` 명령에는 2개의 인수가 필요합니다.(1) 명령 유형을 나타내는 문자열(이 경우 &quot;setConsent&quot;) 및 (2) 필수 동의 필드를 제공하는 객체를 하나 이상 포함해야 하는 `consent` 배열이 포함된 페이로드를 아래와 같이 나타냅니다.

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
| `standard` | 사용 중인 동의 기준. TCF 2.0 동의 처리를 위해서는 이 값을 `IAB`으로 설정해야 합니다. |
| `version` | `standard` 아래에 표시된 동의 표준의 버전 번호입니다. TCF 2.0 동의 처리를 위해서는 이 값을 `2.0`으로 설정해야 합니다. |
| `value` | CMP에 의해 생성된 기본-64 인코딩 동의 문자열. |
| `gdprApplies` | GDPR이 현재 로그인한 고객에게 적용되는지 여부를 나타내는 부울 값입니다. 이 고객에게 TCF 2.0이 적용되려면 이 값을 `true`으로 설정해야 합니다. 정의되지 않은 경우 기본값은 `true`입니다. |

`setConsent` 명령은 동의 설정의 변경 사항을 감지하는 CMP 후크의 일부로 사용해야 합니다. 다음 JavaScript는 `setConsent` 명령을 OneTrust의 `OnConsentChanged` 후크에 사용할 수 있는 방법의 예를 제공합니다.

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

`sendEvent` 명령을 사용하여 플랫폼에서 트리거된 모든 이벤트에 대해 TCF 2.0 동의 데이터를 수집할 수도 있습니다.

>[!NOTE]
>
>이 메서드를 사용하려면 [!DNL Experience Event Privacy mixin]을(를) [!DNL Profile] 활성화된 [!DNL XDM ExperienceEvent] 스키마에 추가해야 합니다. 이를 구성하는 방법에 대한 단계는 데이터 세트 준비 안내서에서 [ExperienceEvent 스키마](./dataset.md#event-schema)의 섹션을 참조하십시오.

`sendEvent` 명령은 웹 사이트의 적절한 이벤트 리스너에서 콜백으로 사용해야 합니다. 명령에는 다음 두 개의 인수가 필요합니다.(1) 명령 유형을 나타내는 문자열(이 경우 `sendEvent`) 및 (2) 필수 동의 필드를 JSON으로 제공하는 `xdm` 개체가 포함된 페이로드:

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
| `xdm.consentStrings` | 필수 동의 필드를 제공하는 객체를 하나 이상 포함해야 하는 배열입니다. |
| `consentStandard` | 사용 중인 동의 기준. TCF 2.0 동의 처리를 위해서는 이 값을 `IAB`으로 설정해야 합니다. |
| `consentStandardVersion` | `standard` 아래에 표시된 동의 표준의 버전 번호입니다. TCF 2.0 동의 처리를 위해서는 이 값을 `2.0`으로 설정해야 합니다. |
| `consentStringValue` | CMP에 의해 생성된 기본-64 인코딩 동의 문자열. |
| `gdprApplies` | GDPR이 현재 로그인한 고객에게 적용되는지 여부를 나타내는 부울 값입니다. 이 고객에게 TCF 2.0이 적용되려면 이 값을 `true`으로 설정해야 합니다. 정의되지 않은 경우 기본값은 `true`입니다. |

### SDK 응답 처리

모든 [!DNL Platform SDK] 명령은 호출이 성공했는지 실패했는지 여부를 나타내는 약속을 반환합니다. 그런 다음 이러한 응답을 고객에게 확인 메시지를 표시하는 등의 추가 로직에 사용할 수 있습니다. 특정 예제에 대한 SDK 명령 실행에 대한 안내서의 [성공 또는 실패 처리](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure)에 대한 섹션을 참조하십시오.

## 세그먼트 내보내기 {#export}

>[!NOTE]
>
>세그먼트 내보내기를 시작하기 전에 세그먼트에 모든 필수 동의 필드가 포함되어야 합니다. 자세한 내용은 [병합 정책 구성](#merge-policies)의 섹션을 참조하십시오.

고객 동의 데이터를 수집하고 필수 동의 속성이 포함된 대상 세그먼트를 만든 후 해당 세그먼트를 다운스트림 대상으로 내보낼 때 TCF 2.0 규정 준수를 적용할 수 있습니다.

고객 프로필 집합에 대해 동의 설정 `gdprApplies`이(가) `true`으로 설정되어 있는 경우, 다운스트림 대상으로 내보낸 프로필의 모든 데이터는 각 프로필에 대한 TCF 동의 환경 설정에 따라 필터링됩니다. 내보내기 프로세스 중에 필수 동의 기본 설정에 맞지 않는 모든 프로파일은 건너뜁니다.

대상으로 내보내는 세그먼트에 자신의 프로파일을 포함하려면 고객은 다음 목적(예: [TCF 2.0 정책](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions))에 동의해야 합니다.

* **목적 1**:장치에 정보 저장 및/또는 액세스
* **목적 10**:제품 개발 및 개선

또한 TCF 2.0에서는 데이터 소스가 해당 대상으로 데이터를 보내기 전에 대상의 공급업체 권한을 확인해야 합니다. 이와 같이 Platform(플래시 플랫폼)은 대상에 바인딩된 데이터를 포함하기 전에 클러스터의 모든 ID에 대해 대상의 공급업체 권한이 선택되었는지 확인합니다.

>[!NOTE]
>
>Adobe Audience Manager과 공유되는 모든 세그먼트는 플랫폼 상대 세그먼트와 동일한 TCF 2.0 동의 값을 포함합니다. [!DNL Audience Manager]은(는) 플랫폼과 동일한 공급업체 ID를 공유하므로 동일한 목적과 공급업체 권한이 필요합니다. 자세한 내용은 [IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)용 Adobe Audience Manager 플러그인의 문서를 참조하십시오.

## 구현 테스트 {#test-implementation}

TCF 2.0 구현을 구성하고 세그먼트를 대상으로 내보내면 동의 요구 사항을 충족하지 않는 데이터는 내보내지지 않습니다. 그러나 내보내기 중에 적절한 고객 프로필이 필터링되었는지 확인하려면 대상에 있는 데이터 저장소를 수동으로 확인하여 동의가 제대로 적용되었는지 확인해야 합니다.

여러 ID가 클러스터를 구성하고 TCF 2.0이 적용되는 경우 단일 ID에도 올바른 목적과 공급업체 권한이 없는 경우에도 전체 클러스터가 제외됩니다.

## 다음 단계

이 문서에서는 TCF 2.0에서 설명한 바와 같이 귀하의 비즈니스 의무를 충족하도록 플랫폼 데이터 작업을 구성하는 과정에 대해 다룹니다. 플랫폼의 개인정보 보호 관련 기능에 대한 자세한 내용은 [거버넌스, 개인 정보 보호 및 보안](../../overview.md)에 대한 개요를 참조하십시오.
