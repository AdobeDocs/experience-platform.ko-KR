---
title: Adobe Experience Platform 웹 SDK를 사용하여 고객 동의 데이터 처리
topic: 시작하기
description: Adobe 2.0 표준을 사용하여 Adobe Experience Platform에서 고객 동의 데이터를 처리하기 위해 Adobe Experience Platform Web SDK를 통합하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: fee3f005ca3679f8639cea45c16150090b2a1e0f
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 0%

---


# Adobe 2.0 표준을 사용하여 고객 동의 데이터를 처리하기 위해 플랫폼 웹 SDK 통합

Adobe Experience Platform 웹 SDK를 사용하면 동의 관리 플랫폼(CMP)에서 생성된 고객 동의 신호를 검색하고 동의 변경 이벤트가 발생할 때마다 Adobe Experience Platform으로 보낼 수 있습니다.

**SDK는 특별히 제공되는 CMP와 연결되지 않습니다**. SDK를 웹 사이트에 통합하는 방법을 결정하고, CMP의 동의 변경 사항을 수신하고, 적절한 명령을 호출하는 방법은 귀하에게 달려 있습니다. 이 문서에서는 CMP를 Platform Web SDK와 통합하는 방법에 대한 일반적인 지침을 제공합니다.

## 전제 조건

이 자습서에서는 CMP 내에서 동의 데이터를 생성하는 방법을 이미 결정했으며, 실시간 고객 프로필에 대해 활성화된 동의 필드가 포함된 데이터 세트를 만들었다고 가정합니다. 이러한 단계에 대한 자세한 내용은 이 안내서로 돌아가기 전에 Experience Platform](./overview.md)의 [동의 처리에 대한 개요를 참조하십시오.

또한 이 안내서를 보려면 Adobe Experience Platform Launch 익스텐션과 웹 애플리케이션에 설치되는 방법에 대한 작업 지식이 필요합니다. 자세한 내용은 다음 문서를 참조하십시오.

* [platform launch 개요](https://experienceleague.adobe.com/docs/launch/using/home.html)
* [빠른 시작 가이드](https://experienceleague.adobe.com/docs/launch/using/get-started/quick-start.html)
* [게시 개요](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html)

## Edge 구성 설정

SDK가 데이터를 Experience Platform으로 전송하려면 Adobe Experience Platform Launch에서 플랫폼에 대한 기존 에지 구성을 설정해야 합니다. 또한 구성에 대해 선택한 [!UICONTROL Profile Dataset]에는 표준 동의 필드가 포함되어야 합니다.

새 구성을 만들거나 편집할 기존 구성을 선택한 후 **[!UICONTROL Adobe Experience Platform]** 옆에 있는 전환 단추를 선택합니다. 그런 다음 아래 나열된 값을 사용하여 양식을 완료합니다.

![](../../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Edge 구성 필드 | 값 |
| --- | --- |
| [!UICONTROL Sandbox] | 에지 구성을 설정하는 데 필요한 스트리밍 연결 및 데이터 세트가 포함된 플랫폼 [샌드박스](../../../../sandboxes/home.md)의 이름입니다. |
| [!UICONTROL Streaming Inlet] | Experience Platform에 대한 유효한 스트리밍 연결 기존 스트리밍 입구가 없는 경우 [스트리밍 연결 만들기](../../../../ingestion/tutorials/create-streaming-connection-ui.md)에서 자습서를 참조하십시오. |
| [!UICONTROL Event Dataset] | SDK를 사용하도록 이벤트 데이터를 보낼 계획인 [!DNL XDM ExperienceEvent] 데이터 집합. 플랫폼 에지 구성을 만들기 위해 이벤트 데이터 세트를 제공해야 하는 경우, 이벤트를 통해 직접 동의 데이터를 전송하는 것은 현재 지원되지 않습니다. |
| [!UICONTROL Profile Dataset] | 이전에 만든 고객 동의 필드가 있는 [!DNL Profile] 사용 데이터 세트. |

완료되면 화면 하단에 있는 **[!UICONTROL Save]**&#x200B;을 선택하고 구성을 완료하라는 추가 지침을 계속 따릅니다.


## 플랫폼 웹 SDK 확장 설치 및 구성

이전 섹션에 설명된 대로 Edge 구성을 만들었다면, 사이트에 최종적으로 배포할 Platform Web SDK 익스텐션을 구성해야 합니다. platform launch 속성에 SDK 확장이 설치되어 있지 않은 경우 왼쪽 탐색 영역에서 **[!UICONTROL Extensions]**&#x200B;을 선택하고 **[!UICONTROL Catalog]** 탭을 선택합니다. 그런 다음 사용 가능한 확장 목록 내에서 플랫폼 SDK 확장 프로그램 아래의 **[!UICONTROL Install]**&#x200B;을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/sdk/install.png)

SDK를 구성할 때 **[!UICONTROL Edge Configurations]** 아래에서 이전 단계에서 만든 구성을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

**[!UICONTROL Save]**&#x200B;을 선택하여 확장을 설치합니다.

### 기본 동의를 설정하는 데이터 요소 만들기

SDK 확장이 설치되어 있으면 사용자에 대한 기본 데이터 수집 동의 값(`collect.val`)을 나타내는 데이터 요소를 만들 수 있습니다. 이 기능은 유럽연합 사용자의 경우 `pending`, 북미 사용자의 경우 `in` 등과 같이 사용자에 따라 다른 기본값을 가지려는 경우에 유용합니다.

이 사용 사례에서는 다음을 구현하여 사용자의 지역을 기준으로 기본 동의를 설정할 수 있습니다.

1. 웹 서버에서 사용자의 영역을 결정합니다.
1. 웹 페이지에서 Platform launch 스크립트 태그(포함 코드)를 실행하기 전에 사용자 영역을 기준으로 `adobeDefaultConsent` 변수를 설정하는 별도의 스크립트 태그를 렌더링합니다.
1. `adobeDefaultConsent` JavaScript 변수를 사용하는 데이터 요소를 설정하고 이 데이터 요소를 사용자의 기본 동의 값으로 사용합니다.

사용자 영역이 CMP로 결정되는 경우 대신 다음 단계를 사용할 수 있습니다.

1. 페이지에서 &quot;CMP 로딩&quot; 이벤트를 처리합니다.
1. 이벤트 핸들러에서 사용자의 영역을 기준으로 `adobeDefaultConsent` 변수를 설정한 다음 JavaScript를 사용하여 Platform launch 라이브러리 스크립트를 로드합니다.
1. `adobeDefaultConsent` JavaScript 변수를 사용하는 데이터 요소를 설정하고 이 데이터 요소를 사용자의 기본 동의 값으로 사용합니다.

platform launch UI에서 데이터 요소를 만들려면 왼쪽 탐색 영역에서 **[!UICONTROL Data Elements]**&#x200B;을 선택하고 **[!UICONTROL Add Data Element]**&#x200B;을 선택하여 데이터 요소 만들기 대화 상자로 이동합니다.

여기서 `adobeDefaultConsent`을(를) 기반으로 [!UICONTROL JavaScript Variable] 데이터 요소를 만들어야 합니다. 완료되면 **[!UICONTROL Save]**&#x200B;을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

데이터 요소가 만들어지면 웹 SDK 확장 구성 페이지로 돌아갑니다. [!UICONTROL Privacy] 섹션에서 **[!UICONTROL Provided by data element]**&#x200B;을 선택하고 제공된 대화 상자를 사용하여 이전에 만든 기본 동의 데이터 요소를 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### 웹 사이트에 확장 프로그램 배포

확장 구성을 완료하면 웹 사이트에 통합할 수 있습니다. 업데이트된 라이브러리 빌드를 배포하는 방법에 대한 자세한 내용은 Platform launch 설명서의 [게시 가이드](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html)를 참조하십시오.

## 동의 변경 명령 만들기

SDK 익스텐션을 웹 사이트에 통합하면 플랫폼 웹 SDK `setConsent` 명령을 사용하여 동의 데이터를 플랫폼에 보낼 수 있습니다.

사이트에서 `setConsent`을(를) 호출해야 하는 두 가지 시나리오가 있습니다.

1. 페이지에 동의가 로드될 때(즉, 페이지가 로드될 때마다)
1. 동의 설정의 변경 사항을 감지하는 CMP 후크 또는 이벤트 리스너의 일부로서

>[!NOTE]
>
>플랫폼 SDK 명령에 대한 일반적인 구문에 대한 소개는 [명령 실행](../../../../edge/fundamentals/executing-commands.md)에 있는 문서를 참조하십시오.

`setConsent` 명령에는 2개의 인수가 필요합니다.

1. 명령 유형을 나타내는 문자열(이 경우 `"setConsent"`)
1. 단일 배열 유형 속성을 포함하는 페이로드 객체입니다.`consent`. `consent` 배열은 Adobe 표준에 대한 필수 동의 필드를 제공하는 객체를 하나 이상 포함해야 합니다.

Adobe 표준에 대한 필수 동의 필드는 다음 예 `setConsent` 호출에 표시됩니다.

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
| `standard` | 사용 중인 동의 기준. Adobe 표준의 경우 이 값은 `Adobe`으로 설정해야 합니다. |
| `version` | `standard` 아래에 표시된 동의 표준의 버전 번호입니다. Adobe 표준 동의 처리를 위해서는 이 값을 `2.0`으로 설정해야 합니다. |
| `value` | 프로필 사용 데이터 세트의 동의 필드 구조를 준수하는 XDM 개체로 제공되는 고객의 업데이트된 동의 정보입니다. |

>[!NOTE]
>
>`Adobe`(예: `IAB TCF`)과 함께 다른 동의 표준을 사용하는 경우 각 표준에 대해 `consent` 배열에 개체를 추가할 수 있습니다. 각 개체는 해당 개체가 나타내는 동의 표준에 대해 `standard`, `version` 및 `value`에 적절한 값을 포함해야 합니다.

다음 JavaScript는 이벤트 리스너 또는 CMP 후크의 콜백으로 사용할 수 있는 웹 사이트에서 동의 환경 설정을 변경하는 사항을 처리하는 함수의 예를 제공합니다.

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

모든 [!DNL Platform SDK] 명령은 호출이 성공했는지 실패했는지 여부를 나타내는 약속을 반환합니다. 그런 다음 이러한 응답을 고객에게 확인 메시지를 표시하는 등의 추가 로직에 사용할 수 있습니다. 특정 예제에 대한 SDK 명령 실행에 대한 안내서의 [성공 또는 실패 처리](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure)에 대한 섹션을 참조하십시오.

## 다음 단계

이 안내서를 따르면 Experience Platform에 동의 데이터를 전송하도록 플랫폼 웹 SDK 확장을 구성했습니다. 이제 [구현 테스트](./overview.md#test-implementation)에 대한 단계에 대한 동의 처리 개요로 돌아갈 수 있습니다.