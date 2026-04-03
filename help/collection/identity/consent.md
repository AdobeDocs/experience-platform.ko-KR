---
title: 데이터 수집에서의 동의 및 ID
description: 동의 선택 사항이 ECID 생성, 쿠키 지속성 및 방문자 연속성을 비롯한 웹 SDK 구현의 ID 동작에 어떻게 영향을 미치는지 이해합니다.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 2%

---

# 데이터 수집에서의 동의 및 ID

동의와 ID는 웹 SDK 구현에서 밀접하게 연결되어 있습니다. 동의를 수집하는 방법과 시기는 웹 SDK이 ECID를 생성하고, ID 쿠키를 설정하고, Edge Network에 데이터를 전송하는지 여부와 그 시기에 직접 영향을 줍니다. 동의를 신중하게 처리하지 않으면 종종 예상치 못한 방문자 인플레이션, ID 연속성의 차이 또는 둘 다가 발생합니다.

이 페이지에서는 동의 선택 사항이 ID 동작과 상호 작용하는 방법을 설명하고 일반적인 위험을 방지하기 위해 구현을 구성하는 데 필요한 지침을 제공합니다. 웹 SDK에서 ECID, FPID 및 기타 ID 신호를 처리하는 방법에 대한 배경은 [데이터 수집의 ID](./overview.md)를 참조하십시오.

## 동의가 ID에 미치는 영향 {#how-consent-affects-identity}

웹 SDK은 [`defaultConsent`](/help/collection/js/commands/configure/defaultconsent.md) 구성 변수와 [`setConsent`](/help/collection/js/commands/setconsent.md) 명령을 모두 사용하여 Edge Network으로 데이터를 전송하는지 여부를 제어합니다. 동의 상태는 ECID가 생성되는 시기와 ID 쿠키가 설정되는 시기를 직접 결정합니다.

다음 표는 데이터 수집, 쿠키 설정 및 ID 동작에 대한 `defaultConsent`과(와) `setConsent`의 결합된 효과를 보여 줍니다.

| `defaultConsent` | `setConsent` | 데이터 수집 발생 | 브라우저 쿠키 설정 | ID 동작 |
| --- | --- | --- | --- | --- |
| `in` | 설정되지 않음 | 예 | 예 | ECID는 첫 번째 요청에서 즉시 생성됩니다. ID 쿠키는 페이지 로드 시 설정됩니다. |
| `in` | `in` | 예 | 예 | 방문자의 기존 ECID는 유지됩니다. ID 동작은 변경되지 않습니다. |
| `in` | `out` | 아니요 | 예 | 데이터 수집이 중지됩니다. 기존 ECID 및 `kndctr_` ID 쿠키는 만료될 때까지 브라우저에 남아 있습니다. |
| `pending` | 설정되지 않음 | 아니요 | 아니요 | ECID가 생성되지 않습니다. 설정된 쿠키가 없습니다. 이벤트는 `setConsent`을(를) 호출할 때까지 로컬로 큐에 있습니다. |
| `pending` | `in` | 예 | 예 | 큐에 있는 이벤트가 전송됩니다. ECID는 첫 번째 요청에 생성되며 ID 쿠키가 설정됩니다. |
| `pending` | `out` | 아니요 | 예 | 큐에 있는 이벤트는 무시됩니다. ECID가 생성되지 않습니다. 동의 쿠키는 방문자의 기본 설정을 기록하도록 설정됩니다. |
| `out` | 설정되지 않음 | 아니요 | 아니요 | ECID가 생성되지 않습니다. 설정된 쿠키가 없습니다. 전송된 이벤트가 없습니다. |
| `out` | `in` | 예 | 예 | ECID는 첫 번째 요청에 생성되며 ID 쿠키가 설정됩니다. |
| `out` | `out` | 아니요 | 예 | ECID가 생성되지 않습니다. 동의 쿠키는 방문자의 기본 설정을 기록하도록 설정됩니다. |

>[!NOTE]
>
>ID 및 동의 쿠키는 방문자가 옵트아웃해도 설정됩니다. 이러한 쿠키는 방문자의 데이터 수집 환경 설정을 준수하는 데 필요합니다. 웹 SDK에서 설정하는 쿠키의 전체 목록은 [웹 SDK 쿠키](https://experienceleague.adobe.com/ko/docs/core-services/interface/data-collection/cookies/web-sdk)를 참조하십시오.

방문자가 이전에 쿠키를 취소한 후 다시 동의하면(`setConsent` 후 `"general": "in"`(으)로 `"general": "out"`을(를) 호출하여) 웹 SDK은 이벤트 전송을 다시 시작하고 쿠키가 만료되지 않은 경우 쿠키의 기존 ECID를 사용합니다. 방문자의 ID는 유지됩니다.

방문자가 동의를 부여하거나 거부하면 웹 SDK은 `kndctr_` 동의 쿠키에서 기본 설정을 유지합니다. 이후 페이지가 로드되면 SDK에서 이 쿠키를 읽고 저장된 기본 설정을 자동으로 적용합니다. 방문자의 기본 설정이 변경되지 않는 한 `setConsent`을(를) 다시 호출할 필요가 없습니다. 페이지 로드 사이에 `defaultConsent` 구성 값이 유지되지는 않지만 방문자의 해결된 동의(`setConsent`을 통해 설정)는 유지됩니다.

>[!NOTE]
>
>동의가 `pending`인 동안 큐에 있는 이벤트는 메모리에 저장되어 페이지 다시 로드에서 살아남지 못합니다. 방문자가 동의가 해결되기 전에 새 페이지로 이동하면 이전 페이지의 큐에 있는 이벤트가 손실됩니다.

## 구현 패턴 {#implementation-patterns}

### 옵트인 모델(수집 전 동의 필요) {#opt-in}

데이터를 수집하기 전에 규정(예: GDPR)에 명시적 동의가 필요한 경우 이 패턴을 사용하십시오.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "pending"
});

// When the visitor grants consent:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "in" }
  }]
});
```

다음 패턴을 사용하여:
* 동의가 부여될 때까지 ECID가 생성되지 않습니다.
* 동의 전에 트리거된 이벤트(예: 초기 페이지 보기)는 큐에 올라가 동의가 부여된 후에 전송됩니다.
* ID 쿠키는 처음 성공한 Edge Network 요청 이후에만 설정됩니다.

### 옵트아웃 모델(기본적으로 컬렉션, 거부 시 중지) {#opt-out}

규정이 옵트아웃 옵션과 함께 기본적으로 데이터 수집을 허용하는 경우 이 패턴을 사용합니다.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "in"
});

// If the visitor opts out:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "out" }
  }]
});
```

다음 패턴을 사용하여:
* ECID는 첫 번째 페이지 로드 시 즉시 생성됩니다.
* 모든 이벤트는 방문자가 옵트아웃할 때까지 전송됩니다.
* 옵트아웃 이후 웹 SDK은 이벤트 전송을 중단하지만 기존 쿠키는 유지됩니다.

## 자사 디바이스 ID를 사용한 동의 {#consent-with-fpids}

구현에서 [자사 장치 ID(FPID)](./fpid.md)를 사용하는 경우, FPID 쿠키는 웹 SDK의 동의 상태와 독립적으로 서버에 의해 설정됩니다. FPID 쿠키는 자체 인프라에서 관리하는 식별자입니다. 단, FPID는 웹 SDK에서 요청을 할 때만(동의에 의해 제어됨) Edge Network으로 전송됩니다.

* `defaultConsent: "pending"`을(를) 사용하면 FPID가 브라우저에 존재하지만 동의를 받을 때까지 ECID를 시드하는 데 사용되지 않습니다.
* `defaultConsent: "in"`을(를) 사용하면 FPID가 첫 번째 요청에 사용되고 ECID를 즉시 시드합니다.

동의 구현에서 동의 전에 식별자를 설정하지 않아도 하는 경우 동의가 전달될 때까지 FPID 쿠키 설정을 지연합니다. 웹 SDK의 동의 게이팅만으로는 FPID 쿠키가 서버에 의해 관리되므로 설정되지 않습니다.

## 일반적인 함정 {#common-pitfalls}

+++**동의 배너가 ID 쿠키를 지웁니다**

**문제**: 일부 동의 관리 플랫폼(CMP)은 동의 배너를 표시할 때 방문자가 선택하기 전에 `kndctr_` ID 쿠키를 포함하여 모든 쿠키를 지웁니다. 방문자가 동의하면 웹 SDK은 이전 ECID가 삭제되었으므로 새 ECID를 생성합니다. 방문자가 보고에 새 사람으로 나타납니다.

**증상**:
* 동의 배너를 배포한 후 고유 방문자 수가 급증했습니다.
* 재방문자는 동의가 만료될 때마다 새 방문자로 계산되며 배너와 다시 상호 작용합니다.

**솔루션**: `kndctr_` 쿠키를 유지하도록 CMP를 구성합니다. 이러한 쿠키는 추적 쿠키가 아닌 ID 쿠키로서, 디바이스를 식별하며 행동 데이터를 포함하지 않습니다. CMP에서 쿠키를 지워야 하는 경우 `kndctr_` 접두사가 있는 쿠키를 제외 목록에 추가하십시오. 또는 방문자가 쿠키를 사전에 지우지 않고 명시적으로 동의를 거부할 때까지 쿠키 지우기를 지연합니다.

+++

+++**지연된 동의로 인해 ID가 중복됨**

**문제**: `defaultConsent`이(가) `pending`(으)로 설정되면 웹 SDK에서 데이터를 보내기 전에 동의를 기다립니다. 페이지 라이프사이클 후반에 동의가 부여되는 경우(예: 페이지 재로드를 트리거하는 배너 상호 작용 후) 다음 시퀀스로 인해 문제가 발생할 수 있습니다.

1. 페이지가 로드됩니다. `defaultConsent: "pending"` 질문에 답합니다. Web SDK은 요청을 전송하지 않습니다.
2. 방문자가 동의합니다. CMP가 페이지 다시 로드를 트리거합니다.
3. 페이지가 다시 로드됩니다. 웹 SDK은 이제 승인된 동의로 초기화되며 ECID를 생성합니다.

이 흐름은 정상이며 올바르게 작동합니다. CMP 또는 구현이 실수로 2단계와 3단계 사이의 쿠키를 지우거나 다시 로드 시 웹 SDK이 다르게 구성된 경우 문제가 발생합니다.

**솔루션**: 페이지를 로드할 때마다 웹 SDK 구성(특히 `orgId` 및 `defaultConsent`)이 동일한지 확인하십시오. 동의 후 CMP가 다시 로드를 트리거하는 경우 ID 쿠키가 다시 로드에서 유지되는지 확인하십시오.

+++

+++**동의 배너로 `defaultConsent: "in"` 사용**

**문제**: 일부 구현은 `defaultConsent: "in"`을(를) 설정한 다음 방문자가 거부하면 `setConsent`(으)로 `"general": "out"`을(를) 호출합니다. 이 접근 방식은 ECID를 생성하고 동의가 거부되기 전에 하나 이상의 요청을 전송합니다. 규정 요구 사항에 따라 이 초기 데이터 수집은 조직의 개인정보 처리방침과 일치하지 않을 수 있습니다.

**솔루션**: 데이터 수집이나 ECID를 생성하기 전에 규제 환경에서 동의해야 하는 경우 대신 `defaultConsent: "pending"`을(를) 사용하십시오. 이 설정을 사용하면 동의를 명시적으로 부여할 때까지 웹 SDK이 Edge Network과 통신하지 않습니다.

+++
