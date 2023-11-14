---
title: Adobe Experience Platform Web SDK를 사용하여 고객 동의 데이터 처리
description: Adobe Experience Platform Web SDK를 통합하여 Adobe Experience Platform에서 고객 동의 데이터를 처리하는 방법에 대해 알아봅니다.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 1%

---

# Platform Web SDK를 통합하여 고객 동의 데이터 처리

Adobe Experience Platform Web SDK를 사용하면 동의 관리 플랫폼(CMP)에서 생성된 고객 동의 신호를 검색하고 동의 변경 이벤트가 발생할 때마다 Adobe Experience Platform으로 전송할 수 있습니다.

**SDK는 즉시 사용할 수 있는 CMP와 인터페이스하지 않습니다**. SDK를 웹 사이트에 통합하는 방법을 결정하고 CMP에서 동의 변경 사항을 수신하고 적절한 명령을 호출하는 것은 사용자가 결정합니다. 이 문서에서는 CMP를 Platform Web SDK와 통합하는 방법에 대한 일반적인 지침을 제공합니다.

## 전제 조건 {#prerequisites}

이 자습서에서는 CMP 내에서 동의 데이터를 생성하는 방법을 이미 결정하고 Adobe 표준 또는 IAB TCF(Transparency and Consent Framework) 2.0 표준을 준수하는 동의 필드를 포함하는 데이터 세트를 만들었다고 가정합니다. 이 데이터 세트를 아직 만들지 않은 경우 이 안내서로 돌아가기 전에 다음 튜토리얼을 참조하십시오.

* [Adobe 표준을 사용하여 데이터 세트 만들기](./adobe/dataset.md)
* [TCF 2.0 표준을 사용하여 데이터 세트 만들기](./iab/dataset.md)

이 안내서는 UI에서 태그 확장을 사용하여 SDK를 설정하는 워크플로를 따릅니다. 확장을 사용하지 않고 사이트에 독립 실행형 SDK 버전을 직접 포함하려는 경우 이 안내서 대신 다음 문서를 참조하십시오.

* [데이터스트림 구성](../../../datastreams/overview.md)
* [SDK 설치](../../../edge/fundamentals/installing-the-sdk.md)
* [동의 명령에 대한 SDK 구성](../../../edge/consent/supporting-consent.md)

이 안내서의 설치 단계에서는 태그 확장 및 웹 애플리케이션에 태그 확장을 설치하는 방법을 이해해야 합니다. 자세한 내용은 다음 설명서를 참조하십시오.

* [태그 개요](../../../tags/home.md)
* [빠른 시작 안내서](../../../tags/quick-start/quick-start.md)
* [게시 개요](../../../tags/ui/publishing/overview.md)

## 데이터스트림 설정

SDK가 데이터를 Experience Platform으로 보내려면 먼저 데이터 스트림을 구성해야 합니다. 데이터 수집 UI 또는 Experience Platform UI에서 **[!UICONTROL 데이터스트림]** 왼쪽 탐색.

새 데이터 스트림을 만들거나 편집할 기존 데이터 스트림을 선택한 후 옆에 있는 토글 버튼을 선택합니다 **[!UICONTROL Adobe Experience Platform]**. 그런 다음 아래 나열된 값을 사용하여 양식을 작성합니다.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| 데이터 스트림 필드 | 값 |
| --- | --- |
| [!UICONTROL 샌드박스] | 플랫폼 이름 [샌드박스](../../../sandboxes/home.md) 에는 데이터 스트림을 설정하는 데 필요한 스트리밍 연결 및 데이터 세트가 포함되어 있습니다. |
| [!UICONTROL 이벤트 데이터 세트] | An [!DNL XDM ExperienceEvent] sdk를 사용하여 이벤트 데이터를에 전송할 계획인 데이터 세트입니다. Platform 데이터 스트림을 만들기 위해 이벤트 데이터 세트를 제공해야 하지만, 이벤트를 통해 전송된 동의 데이터는 다운스트림 시행 워크플로우에서 적용되지 않습니다. |
| [!UICONTROL 프로필 데이터 세트] | 다음 [!DNL Profile]-만든 고객 동의 필드가 있는 데이터 세트 활성화됨 [이전](#prerequisites). |

완료되면 다음을 선택합니다. **[!UICONTROL 저장]** 화면 하단의 을 클릭하고 추가 프롬프트에 따라 계속 구성을 완료합니다.

## Platform Web SDK 설치 및 구성

이전 섹션에서 설명한 대로 데이터 스트림을 생성했으면 궁극적으로 사이트에 배포할 Platform Web SDK 확장을 구성해야 합니다. 태그 속성에 SDK 확장이 설치되어 있지 않으면 을 선택합니다 **[!UICONTROL 확장]** 왼쪽 탐색 후 **[!UICONTROL 카탈로그]** 탭. 그런 다음 을 선택합니다. **[!UICONTROL 설치]** 사용 가능한 확장 목록 내의 Platform SDK 확장 아래에 있습니다.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

SDK를 구성할 때에서 **[!UICONTROL Edge 구성]**&#x200B;이전 단계에서 생성한 데이터 스트림을 선택합니다.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

선택 **[!UICONTROL 저장]** 확장을 설치합니다.

### 기본 동의를 설정할 데이터 요소 만들기

SDK 확장이 설치되어 있으면 기본 데이터 수집 동의 값( )을 나타내는 데이터 요소를 만들 수 있는 옵션이 제공됩니다.`collect.val`)을 참조하십시오. 이 기능은 다음과 같이 사용자에 따라 다른 기본값을 사용하려는 경우 유용합니다. `pending` 유럽 연합 사용자용 및 `in` 북미 사용자를 위한 것입니다.

이 사용 사례에서는 다음을 구현하여 사용자의 지역을 기반으로 기본 동의를 설정할 수 있습니다.

1. 웹 서버에서 사용자 영역을 확인합니다.
1. 다음 이전 `script` 웹 페이지의 태그(포함 코드), 별도의 렌더링 `script` 를 설정하는 태그 `adobeDefaultConsent` 사용자 영역을 기반으로 합니다.
1. 다음을 사용하는 데이터 요소 설정 `adobeDefaultConsent` JavaScript 변수와 이 데이터 요소를 사용자의 기본 동의 값으로 사용합니다.

사용자의 영역이 CMP에 의해 결정되는 경우 대신 다음 단계를 사용할 수 있습니다.

1. 페이지에서 &quot;CMP 로드된&quot; 이벤트를 처리합니다.
1. 이벤트 처리기에서 `adobeDefaultConsent` 변수를 사용자 영역을 기반으로 한 다음 JavaScript를 사용하여 태그 라이브러리 스크립트를 로드합니다.
1. 다음을 사용하는 데이터 요소 설정 `adobeDefaultConsent` JavaScript 변수와 이 데이터 요소를 사용자의 기본 동의 값으로 사용합니다.

UI에서 데이터 요소를 만들려면 다음을 선택합니다 **[!UICONTROL 데이터 요소]** 왼쪽 탐색에서 을(를) 선택합니다. **[!UICONTROL 데이터 요소 추가]** 데이터 요소 만들기 대화 상자로 이동합니다.

여기에서 다음을 만들어야 합니다. [!UICONTROL JavaScript 변수] 데이터 요소 기준 `adobeDefaultConsent`. 선택 **[!UICONTROL 저장]** 완료 시.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

데이터 요소가 만들어지면 웹 SDK 확장 구성 페이지로 다시 이동합니다. 아래 [!UICONTROL 개인 정보 보호] 섹션, 선택 **[!UICONTROL 데이터 요소에서 제공]**&#x200B;을 클릭하고 제공된 대화 상자를 사용하여 이전에 만든 기본 동의 데이터 요소를 선택합니다.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### 웹 사이트에 확장 배포

확장 구성을 마치면 웹 사이트에 통합할 수 있습니다. 다음을 참조하십시오. [게시 안내서](../../../tags/ui/publishing/overview.md) 업데이트된 라이브러리 빌드를 배포하는 방법에 대한 자세한 내용은 태그 설명서 를 참조하십시오.

## 동의 변경 명령 만들기 {#commands}

웹 사이트에 SDK 확장을 통합한 후에는 Platform 웹 SDK를 사용할 수 있습니다 `setConsent` 동의 데이터를 Platform에 전송하는 명령입니다.

다음 `setConsent` 명령은 다음 두 가지 작업을 수행합니다.

1. 프로필 저장소에서 직접 사용자의 프로필 속성을 업데이트합니다. 이렇게 해도 데이터 레이크로 데이터가 전송되지 않습니다.
1. 다음을 생성합니다. [경험 이벤트](../../../xdm/classes/experienceevent.md) 동의 변경 이벤트에 대한 타임스탬프가 지정된 계정이 기록됩니다. 이 데이터는 데이터 레이크로 직접 전송되며 시간 경과에 따른 동의 환경 설정 변경을 추적하는 데 사용할 수 있습니다.

### 호출 시기 `setConsent`

다음과 같은 두 가지 시나리오가 있습니다. `setConsent` 을(를) 귀하의 사이트에서 호출해야 합니다.

1. 동의가 페이지에 로드될 때(즉, 모든 페이지 로드 시)
1. 동의 설정 변경을 감지하는 CMP 후크 또는 이벤트 리스너의 일부

### `setConsent` 구문

>[!NOTE]
>
>Platform SDK 명령의 일반적인 구문에 대한 소개는 다음 문서를 참조하십시오. [명령 실행](../../../edge/fundamentals/executing-commands.md).

다음 `setConsent` 명령에는 다음 두 개의 인수가 필요합니다.

1. 명령 유형을 나타내는 문자열(이 경우 `"setConsent"`)
1. 단일 배열 유형 속성을 포함하는 페이로드 개체: `consent`. 다음 `consent` 배열에는 Adobe 표준에 대한 필수 동의 필드를 제공하는 개체가 하나 이상 있어야 합니다.

다음 예제는 Adobe 표준에 대한 필수 동의 필드입니다 `setConsent` 호출:

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| 페이로드 속성 | 설명 |
| --- | --- |
| `standard` | 사용 중인 동의 표준입니다. Adobe 표준의 경우 이 값을 로 설정해야 합니다. `Adobe`. |
| `version` | 아래에 표시된 동의 표준의 버전 번호입니다. `standard`. 이 값은 다음으로 설정해야 합니다. `2.0` Adobe 표준 동의 처리용. |
| `value` | 프로필 활성화 데이터 세트의 동의 필드 구조를 준수하는 XDM 객체로 제공되는 고객의 업데이트된 동의 정보. |

>[!NOTE]
>
>와 함께 다른 동의 표준을 사용하는 경우 `Adobe` (예: `IAB TCF`)에 개체를 추가할 수 있습니다. `consent` 각 표준에 대한 배열입니다. 각 객체에는 다음에 대한 적절한 값이 포함되어야 합니다. `standard`, `version`, 및 `value` 을 대표하는 동의 표준입니다.

다음 JavaScript는 웹 사이트에서 동의 환경 설정 변경을 처리하는 함수의 예를 제공합니다. 이 값은 이벤트 리스너 또는 CMP 후크에서 콜백으로 사용할 수 있습니다.

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## SDK 응답 처리

모두 [!DNL Platform SDK] 명령은 호출의 성공 또는 실패 여부를 나타내는 약속을 반환합니다. 그런 다음 고객에게 확인 메시지를 표시하는 것과 같은 추가 논리에 이러한 응답을 사용할 수 있습니다. 의 섹션을 참조하십시오. [성공 또는 실패 처리](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 특정 예제의 SDK 명령 실행에 대한 안내서에서 참조할 수 있습니다.

성공하면 `setConsent` sdk를 사용하여 를 호출하면 Platform UI의 프로필 뷰어를 사용하여 데이터가 프로필 스토어에 도달하는지 확인할 수 있습니다. 의 섹션을 참조하십시오. [id별 프로필 검색](../../../profile/ui/user-guide.md#browse-identity) 추가 정보.

## 다음 단계

이 안내서에 따라 동의 데이터를 Experience Platform으로 보내도록 Platform Web SDK 확장을 구성했습니다. 구현 테스트에 대한 지침은 구현 중인 동의 표준에 대한 설명서를 참조하십시오.

* [Adobe 표준](./adobe/overview.md#test)
* [TCF 2.0 표준](./iab/overview.md#test)
