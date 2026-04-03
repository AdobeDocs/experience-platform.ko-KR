---
title: 데이터 수집에서 identityMap 사용
description: 웹 SDK 구현에서 네임스페이스 전반에 걸쳐 알려진 방문자를 식별하기 위해 identityMap 페이로드를 구성하고 전송하는 방법에 대해 알아봅니다.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 0%

---

# 데이터 수집에서 identityMap 사용

`identityMap` 페이로드 개체는 장치 수준 [ECID](./overview.md)을(를) 벗어난 방문자를 Edge Network에 알리는 방법입니다. 방문자가 로그인하거나, 구매를 완료하거나, 다른 방법으로 알려지면 ECID와 함께 개인 수준 식별자(CRM ID, 해시된 이메일, 로열티 ID 등)를 보낼 수 있습니다. 이러한 개인 수준 식별자는 다운스트림 서비스에 중요한 정보를 제공하여 다음과 같은 작업을 수행할 수 있도록 합니다.

* **장치 및 채널에서 사용자에게 활동을 연결합니다.** [ID 서비스](/help/identity-service/home.md)는 보내는 ID를 [ID 그래프](/help/identity-service/features/identity-graph-viewer.md)에 연결하여 알려진 사용자에게 익명 장치 수준 동작을 연결합니다.
* **통합 고객 프로필을 만듭니다.** [실시간 고객 프로필](/help/profile/home.md)은(는) 이벤트 및 특성을 단일 프로필에 고정하도록 설정한 기본 ID를 사용하여 개인 수준 세분화 및 대상자 빌드를 활성화합니다.
* **다운스트림 대상에서 대상자를 활성화합니다.** 많은 [대상](/help/destinations/home.md)에서 대상을 사용자 기반에 일치시키려면 확인된 사용자 수준 ID(해시된 이메일, 전화번호 등)가 필요합니다.
* **채널 간 여정 오케스트레이션.** [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko-KR)은(는) 확인된 ID를 사용하여 방문자의 인증된 동작을 기반으로 이메일, 푸시 및 인앱 채널 전반에서 여정을 트리거하고 개인화합니다.

이 페이지에서는 `identityMap` 페이로드를 만들고, 각 ID에 적합한 설정을 선택하고, 일반적인 구현 시나리오를 처리하는 방법을 다룹니다.

## 페이로드 구조 {#structure}

`identityMap`은(는) 각 최상위 키가 네임스페이스이고 값이 ID 설명자의 배열인 JSON 개체입니다. 단일 페이로드에 하나 이상의 네임스페이스를 포함할 수 있으며 각 설명자에는 세 개의 필드(`id`, `authenticatedState` 및 `primary`)가 포함되어 있습니다.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

| 필드 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `id` | 문자열 | 예 | 식별자 값(예: `user@example.com` 또는 `ABC123`). |
| `authenticatedState` | 문자열 | 예 | 이 ID가 방문자에게 속한다는 것을 얼마나 확신할 수 있습니까? 유효한 값은 `ambiguous`, `authenticated` 및 `loggedOut`입니다. |
| `primary` | 부울 | 예 | 이 ID가 이벤트의 기본 식별자여야 하는지 여부입니다. 모든 네임스페이스에서 정확히 하나의 ID를 `primary: true`(으)로 표시해야 합니다. |

아래 섹션에서는 페이로드의 각 부분을 자세히 다룹니다.

### 네임스페이스 키 {#namespace-keys}

`identityMap`의 각 최상위 키는 식별자 유형(예: [, &#x200B;](/help/identity-service/features/namespaces.md), `CRMID` 또는 `Email`)을 분류하는 문자열인 `Phone`ID 네임스페이스`LoyaltyId`입니다. 네임스페이스는 페이로드에서 참조하기 전에 ID 서비스에 있어야 합니다. 방문자에 대한 식별자가 두 개 이상 있는 경우 동일한 이벤트에 여러 네임스페이스 키를 포함할 수 있습니다.

ECID를 네임스페이스 키로 포함할 필요는 없습니다. Edge Network은 ID 페이로드에 ECID를 자동으로 추가합니다. ECID를 명시적으로 포함시키는 경우 개인 수준 ID도 있는 경우 `primary`(으)로 표시하지 마십시오.

### `id` {#id}

`id` 필드는 식별자 문자열 자체(이 ID가 나타내는 특정 개인 또는 장치를 Experience Platform에 알려 주는 값)입니다. 각 [ID 네임스페이스](/help/identity-service/features/namespaces.md)에는 특정 값 형식이 필요한데 잘못된 형식의 값을 보내면 올바른 형식의 버전과 병합할 수 없는 고유한 ID가 만들어져 프로필이 조각화됩니다.

`identityMap`에 값을 포함하기 전에 대상 네임스페이스에서 예상하는 형식에 따라 값을 준비합니다.

| 일반적인 네임스페이스 유형 | 값을 준비하는 방법 | 예 |
| --- | --- | --- |
| **CRM/내부 ID** | 레코드 시스템에서 할당하는 정확한 식별자를 사용하십시오. 모든 이벤트(대/소문자, 앞에 0, 접두사)에서 형식을 일관되게 유지합니다. | `ABC-12345`, `00098765` |
| **전자 메일(원시)** | 전체 이메일 주소를 소문자로 바꾸고 선행 및 후행 공백을 트리밍합니다. | `user@example.com` |
| **전자 메일(해시됨)** | 소문자를 사용하고 이메일 주소를 먼저 트리밍한 다음 SHA-256으로 해시합니다. 결과 64자의 16진수 문자열을 보냅니다. 네임스페이스 정의에 솔트가 필요하지 않으면 솔트를 추가하지 마십시오. | `a1b2c3d4e5f6a7b8c9...` |
| **전화(E.164)** | [E.164](https://en.wikipedia.org/wiki/E.164)의 숫자 형식을 `+` 선행, 국가 코드 및 구독자 번호에 공백이나 구두점을 사용하지 말고 지정하십시오. | `+15551234567` |
| **FPID** | [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122) 문자열을 생성합니다. 생성 요구 사항은 [자사 장치 ID](./fpid.md)을(를) 참조하십시오. | `123e4567-e89b-42d3-9456-426614174000` |

표준 네임스페이스 및 해당 정의에 대한 전체 목록은 [ID 네임스페이스 개요](/help/identity-service/features/namespaces.md#standard)를 참조하십시오.

>[!TIP]
>
>`id` 값은 대/소문자를 구분합니다. `User@Example.com`과(와) `user@example.com`은(는) 두 개의 개별 ID로 처리됩니다. 값을 보내기 전에 케이싱을 정규화하여(일반적으로 이메일을 소문자로 바꾸고 공백을 트리밍하여) 그래프에서 중복 ID를 생성하지 않도록 합니다.

#### 런타임에 `id`을(를) 수집하는 중 {#collect-id}

필요한 식별자는 페이지에서 직접 사용할 수 있는 경우가 거의 없습니다. 일반적인 수집 전략은 다음과 같습니다.

* **데이터 계층**: 방문자가 로그인한 후 사이트의 데이터 계층에서 식별자를 읽습니다. 이 위치는 데이터 레이어가 애플리케이션의 백엔드에 의해 채워지고 인증된 세션 상태를 반영하므로 가장 안정적인 방법입니다.
* **인증 토큰 또는 세션 쿠키**: 인증 시스템에서 설정하는 JWT 또는 세션 쿠키에서 식별자를 디코딩하거나 조회합니다. 값을 사용하기 전에 토큰이 여전히 활성 상태인지 확인하십시오.
* **서버측 데이터 보강**: 다운스트림 서비스에 도달하기 전에 [데이터 수집에 대한 데이터 준비](/help/datastreams/data-prep.md) 또는 [이벤트 전달 규칙](/help/tags/ui/event-forwarding/overview.md)을 사용하여 Edge에서 식별자를 매핑하거나 변환합니다. 이 위치는 클라이언트에만 서버측 내부 ID에 매핑되는 불투명한 세션 토큰이 있을 때 유용합니다.

>[!TIP]
>
>지정된 `id` 값이 빈 문자열 `null` 또는 `undefined`(으)로 확인되는 경우 `identityMap`에 네임스페이스를 포함하지 마십시오. 빈 `id`을(를) 보내면 끊어진 ID 레코드가 만들어집니다. 페이로드를 빌드하기 전에 확인을 사용하여 구현을 보호합니다.

### `authenticatedState` {#authenticated-state}

`authenticatedState` 필드는 다운스트림 서비스에 지정된 ID에 신뢰할 수 있는 정도를 알려줍니다. 이 필드에 유효한 값은 다음과 같습니다.

| 값 | 사용 시기 |
| --- | --- |
| **`authenticated`** | 방문자는 현재 세션 동안 적극적으로 ID를 증명했습니다(예: 자격 증명으로 로그인, MFA 완료 또는 유사한 확인). |
| **`loggedOut`** | 방문자는 이전에 인증되었지만 그 이후 로그아웃되었습니다. ID가 장치와 연결되어 있지만 세션이 더 이상 활성 상태가 아닙니다. |
| **`ambiguous`** | 현재 방문자에 속하는 ID로 확인할 수 없습니다. FPID와 같은 장치 수준 식별자 또는 아직 인증이 발생하지 않은 모든 식별자에 이 값을 사용하십시오. |

>[!TIP]
>
>`authenticatedState` 값은 Adobe Experience Platform ID 서비스에서 ID 그래프를 작성하고 병합하는 방법에 영향을 줍니다. 확인되지 않은 ID에 대해 `authenticated`을(를) 보내면 실행 취소하기 어려운 잘못된 장치 간 링크가 만들어질 수 있습니다.

### `primary` {#primary-identity}

모든 `identityMap` 페이로드에는 `primary: true`(으)로 표시된 ID가 하나만 있어야 합니다. 기본 ID는 Experience Platform에서 이벤트의 앵커로 사용되는 ID를 결정합니다.

기본 ID를 설정할 때 다음 지침을 따르십시오.

* **사용자 수준 ID를 사용할 수 있는 경우**(방문자가 로그인됨) 사용자 수준 네임스페이스를 기본 네임스페이스로 표시하고 ECID를 비기본 네임스페이스로 표시합니다. 이렇게 하면 Experience Platform이 이벤트를 장치가 아닌 사용자에게 앵커링합니다.
* **장치 수준 ID만 사용할 수 있는 경우**(방문자가 익명) ECID는 자동으로 기본 ID로 사용됩니다. `identityMap`에 ECID를 포함할 필요가 없습니다. Edge Network에서 자동으로 추가합니다.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

## 구현에서 identityMap 보내기 {#send-identity}

>[!BEGINTABS]

>[!TAB JavaScript 라이브러리]

`identityMap` 호출의 `xdm` 개체에 [`sendEvent`](/help/collection/js/commands/sendevent/overview.md)을(를) 전달합니다.

```js
alloy("sendEvent", {
  xdm: {
    identityMap: {
      CRMID: [
        {
          id: "abc-123-xyz",
          authenticatedState: "authenticated",
          primary: true
        }
      ]
    },
    eventType: "web.webpagedetails.pageViews"
  }
});
```

>[!TAB 웹 SDK 태그 확장]

[ID 맵](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) 데이터 요소 유형을 사용하여 Tags UI에서 ID 페이로드를 빌드합니다.

1. **[!UICONTROL Adobe Experience Platform Web SDK]** 확장과 **[!UICONTROL Identity map]** 데이터 요소 유형으로 데이터 요소를 만듭니다.
2. 네임스페이스, 식별자로 확인되는 데이터 요소 또는 값 및 인증된 상태를 지정하여 ID를 추가합니다.
3. 하나의 ID를 기본으로 표시.
4. **[!UICONTROL Send event]** 아래의 **[!UICONTROL Identity map]** 작업에서 이 데이터 요소를 참조합니다.

>[!ENDTABS]

## 일반적인 시나리오 {#common-scenarios}

+++**로그인**

방문자가 로그인하면 `authenticatedState: "authenticated"` 및 `primary: true`(으)로 개인 수준 식별자를 보냅니다. 인증 후 첫 번째 이벤트와 세션의 모든 후속 이벤트에 이 ID를 포함합니다.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

+++

+++**로그아웃**

방문자가 로그아웃하면 동일한 식별자를 유지하면서 `authenticatedState`을(를) `loggedOut`(으)로 업데이트합니다. 이렇게 하면 세션이 더 이상 활성화되지 않았음을 표시하면서 장치와 개인 간의 연결을 보존합니다.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "loggedOut",
        "primary": false
      }
    ]
  }
}
```

로그아웃 후 ECID는 유효한 기본 ID로 돌아갑니다(Edge Network에서 자동으로 적용). 방문자가 다른 계정으로 로그인하지 않는 한 다른 사용자 수준 ID를 기본으로 표시하지 마십시오.

>[!IMPORTANT]
>
>로그아웃 후에 식별자 전송을 완전히 중지하지 마십시오. `authenticated`에서 `loggedOut`(으)로 전환하면 세션이 종료되었음을 다운스트림 서비스에 알립니다. 식별자를 생략하면 ID 그래프에 완전히 공백이 생겨 프로필이 조각날 수 있습니다.

+++

+++**여러 네임스페이스**

동일한 이벤트에서 여러 ID 네임스페이스를 보낼 수 있습니다. 이 시나리오는 방문자가 로그인되어 있고 사용 가능한 몇 가지 식별자(예: CRM ID, 해시된 이메일 및 충성도 ID)가 있는 경우에 일반적입니다. 알려진 모든 식별자를 포함하고 한 식별자만 기본으로 표시하고 다른 식별자를 `primary: false`(으)로 설정합니다.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email_LC_SHA256": [
      {
        "id": "a1b2c3d4e5f6...",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ],
    "LoyaltyId": [
      {
        "id": "LOY-98765",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

>[!TIP]
>
>동일한 이벤트에서 동일한 `authenticatedState`을(를) 사용하여 여러 네임스페이스를 보내면 ID 서비스에서 해당 ID를 연결하는 가장 강력한 신호를 제공합니다. 사용 가능한 모든 식별자를 별도의 이벤트에 분산하지 않고 인증 지점에 포함합니다.

+++

+++**익명 방문자**

익명 방문자의 경우 일반적으로 `identityMap`을(를) 전혀 보낼 필요가 없습니다. Edge Network은 자동으로 ECID를 할당하고 기본 ID로 사용합니다. [자사 장치 ID](./fpid.md)을(를) 사용하는 경우 FPID는 익명 방문자에게 포함해야 하는 유일한 ID입니다.

+++

## identityMap이 ID 그래프에 미치는 영향 {#identity-graph}

Experience Platform에 도달하는 모든 `identityMap` 페이로드는 [ID 그래프](/help/identity-service/home.md)에 보내는 ID를 연결하는 [ID 서비스](/help/identity-service/features/identity-graph-viewer.md)에 의해 처리됩니다. 포함하는 네임스페이스, `authenticatedState`을(를) 설정하는 방법 및 `primary`(으)로 표시하는 ID는 ID 서비스에서 해당 그래프를 작성하고 병합하는 방법을 직접 구성합니다.

알아야 할 주요 행동:

* 같은 이벤트에서 보낸 **개의 ID가 함께 연결됩니다.** 동일한 `sendEvent` 호출에 CRMID 및 이메일 네임스페이스를 포함하면 Identity Service에서 해당 두 ID 간에 링크를 만듭니다. 식별자를 여러 이벤트에 분산하면 링크가 더 약해지고 그래프가 조각날 수 있습니다.
* **`primary` ID가 실시간 고객 프로필에 이벤트를 고정합니다.** 프로필은 기본 ID를 사용하여 이벤트가 속한 프로필을 결정합니다. 잘못된 ID를 기본으로 표시(예: 개인 수준 ID를 사용할 수 있을 때 ECID를 기본 ID로 설정)하면 개인 수준 프로필이 아닌 장치 수준 프로필에 대해 이벤트가 저장될 수 있습니다.
* **`authenticatedState`은(는) 그래프 신뢰도에 영향을 줍니다.** 실제로 확인되지 않은 ID에 대해 `authenticated`을(를) 보내면 실행 취소하기 어려운 잘못된 장치 간 링크가 만들어질 수 있습니다. 현재 세션 중에 방문자가 적극적으로 ID를 증명한 경우에만 `authenticated`을(를) 사용합니다.

구현에서 [ID 그래프 연결 규칙](/help/identity-service/identity-graph-linking-rules/overview.md)(예: 네임스페이스 우선 순위 또는 ID 최적화 알고리즘)을 사용하는 경우 [구현 안내서](/help/identity-service/identity-graph-linking-rules/implementation-guide.md)를 검토하여 `identityMap`을(를) 통해 보내는 ID와 해당 규칙이 상호 작용하는 방법에 대해 알아보십시오.

>[!NOTE]
>
>`identityMap`은(는) 웹 SDK에서 Edge Network에 요청을 할 때만 전송되며 방문자의 동의 상태에 의해 제어됩니다. 구현에서 `defaultConsent: "pending"`을(를) 사용하는 경우 동의를 받을 때까지 ID가 전송되지 않습니다. 자세한 내용은 [동의 및 ID](./consent.md)를 참조하십시오.
