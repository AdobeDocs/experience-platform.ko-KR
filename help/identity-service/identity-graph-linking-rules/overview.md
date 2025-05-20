---
title: ID 그래프 연결 규칙
description: Identity Service의 Identity Graph 연결 규칙에 대해 알아봅니다.
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 0aefcfbbbed675a08d9e3023b9f667ec59874e46
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 4%

---

# [!DNL Identity Graph Linking Rules] 개요 {#identity-graph-linking-rules-overview}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_overview"
>title="아이덴티티 그래프 연결 규칙"
>abstract="이러한 원치 않는 병합을 방지하기 위해 ID 그래프 연결 규칙을 통해 제공된 구성을 사용하여 사용자를 정확하게 개인화할 수 있습니다."

>[!IMPORTANT]
>
>ID 설정을 활성화한 후 축소된 그래프의 축소 취소(&quot;고정&quot;)를 요구하는 기존 샌드박스가 있는 경우 Adobe 계정 팀에 문의하십시오.

Adobe Experience Platform ID 서비스 및 실시간 고객 프로필을 사용하면 데이터가 완벽하게 수집되고 병합된 모든 프로필이 CRMID와 같은 개인 식별자를 통해 단일 개별 사용자를 나타낸다고 쉽게 가정할 수 있습니다. 그러나 특정 데이터가 서로 다른 여러 프로필을 하나의 프로필로 병합하려고 할 수 있는 시나리오가 있습니다(&quot;그래프 축소&quot;). 이러한 원치 않는 병합을 방지하기 위해 [!DNL Identity Graph Linking Rules]을(를) 통해 제공된 구성을 사용하고 사용자에게 정확한 개인화를 허용할 수 있습니다.

## 시작하기

다음 문서는 [!DNL Identity Graph Linking Rules]을(를) 이해하는 데 필수적입니다.

* [ID 최적화 알고리즘](./identity-optimization-algorithm.md)
* [구현 안내서](./implementation-guide.md)
* [그래프 구성의 예](./example-configurations.md)
* [문제 해결 및 FAQ](./troubleshooting.md)
* [네임스페이스 우선순위](./namespace-priority.md)
* [그래프 시뮬레이션 UI](./graph-simulation.md)
* [ID 설정 UI](./identity-settings-ui.md)

## 비디오 라이브러리

다음 비디오를 통해 ID 그래프 연결 규칙의 몇 가지 기본 측면에 대해 알아보십시오.

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity Graph Linking Rules: Overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://video.tv.adobe.com/v/3448250/?learn=on&enablevpops" title="ID 그래프 연결 규칙: 개요" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429845/?format=jpeg&nocache=1732633205780" alt="ID 그래프 연결 규칙: 개요"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://video.tv.adobe.com/v/3448250/?learn=on&enablevpops" target="_blank" rel="referrer" title="ID 그래프 연결 규칙: 개요">ID 그래프 연결 규칙: 개요</a>
                    </p>
                    <p class="is-size-6">ID 그래프 연결 규칙에 대한 개요를 보려면 이 비디오를 시청한 후 이 기능을 사용하여 그래프 축소를 방지하는 방법에 대해 알아보십시오.</p>
                </div>
                <div style="display: flex; flex-direction; row;">
                  <a href="https://video.tv.adobe.com/v/3448250/?learn=on&enablevpops" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                  </a>
                  <a href="./overview.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="margin-top: 1rem; margin-left: 0.5rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">읽기</span>
                  </a>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity Graph Linking Rules: Identity Settings">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops" title="ID 그래프 연결 규칙: ID 설정" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3441066/?format=jpeg&nocache=1732633205785" alt="ID 그래프 연결 규칙: ID 설정"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops" target="_blank" rel="referrer" title="ID 그래프 연결 규칙: ID 설정">ID 그래프 연결 규칙: ID 설정</a>
                    </p>
                    <p class="is-size-6">이 비디오를 통해 Real-Time CDP, Adobe Journey Optimizer 및 Customer Journey Analytics과 같은 Adobe Experience Platform 애플리케이션에 대한 ID 설정을 구성하고 고품질 ID 그래프 및 고객 프로필을 작성하는 방법에 대해 알아보십시오.</p>
                </div>
                <div style="display: flex; flex-direction: row;">
                  <a href="https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">시청</span>
                  </a>
                  <a href="identity-settings-ui.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="margin-top: 1rem; margin-left: 0.5rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">읽기</span>
                  </a>
                </div>            
            </div>
        </div>
    </div>
</div>

## 그래프 축소 시나리오 {#graph-collapse-scenarios}

>[!CONTEXTUALHELP]
>id="platform_identities_graphcollapsescenarios"
>title="그래프 축소 시나리오"
>abstract="그래프가 “축소”되거나 여러 개인을 표현하는 데에는 다양한 이유가 있습니다."

이 섹션에서는 [!DNL Identity Graph Linking Rules]을(를) 구성할 때 고려할 수 있는 예제 시나리오를 간략하게 설명합니다.

### 공유 디바이스

단일 디바이스에서 여러 로그인이 발생할 수 있는 인스턴스가 있습니다.

| 공유 디바이스 | 설명 |
| --- | --- |
| 패밀리 컴퓨터 및 태블릿 | 남편과 아내 모두 각자의 은행 계좌에 로그인합니다. |
| 공용 키오스크 | 공항 여행객이 수하물을 체크인하고 탑승권을 인쇄하는 데 고객 충성도 ID를 사용하여 로그온합니다. |
| 콜센터 | 콜센터 직원은 고객 지원 센터에 문의하는 고객을 대신하여 단일 디바이스에 로그인하여 문제를 해결합니다. |

![일부 공통 공유 장치의 다이어그램입니다.](../images/identity-settings/shared-devices.png)

이러한 경우 제한이 활성화되지 않은 그래프 측면에서 단일 ECID가 여러 CRMID에 연결됩니다.

[!DNL Identity Graph Linking Rules]을(를) 사용하여 다음을 수행할 수 있습니다.

* 로그인에 사용되는 ID를 고유 식별자로 구성합니다. 예를 들어 CRMID 네임스페이스가 있는 하나의 ID만 저장하도록 그래프를 제한하여 해당 CRMID를 공유 장치의 고유 식별자로 정의할 수 있습니다.
   * 이렇게 하면 CRMID가 ECID에 의해 병합되지 않도록 할 수 있습니다.

### 잘못된 이메일/전화 시나리오

등록할 때 전화번호 및/또는 이메일 주소로 가짜 값을 제공하는 사용자의 경우도 있습니다. 이러한 경우 제한이 활성화되지 않으면 전화/이메일 관련 ID가 여러 다른 CRMID에 연결됩니다.

![잘못된 전자 메일 또는 전화 시나리오를 나타내는 다이어그램입니다.](../images/identity-settings/invalid-email-phone.png)

[!DNL Identity Graph Linking Rules]을(를) 사용하여 다음을 수행할 수 있습니다.

* CRMID, 전화 번호 또는 이메일 주소를 고유 식별자로 구성하여 한 사람을 계정과 연결된 하나의 CRMID, 전화 번호 및/또는 이메일 주소로 제한합니다.

### 잘못되거나 잘못된 ID 값

네임스페이스에 관계없이 시스템에 고유하지 않고 잘못된 ID 값이 수집되는 경우가 있습니다. 해당 예는 다음과 같습니다.

* ID 값이 &quot;user_null&quot;인 IDFA 네임스페이스.
   * IDFA ID 값에는 36자(영숫자 32자, 하이픈 4개)가 있어야 합니다.
* ID 값이 &quot;지정되지 않음&quot;인 전화번호 네임스페이스.
   * 전화번호에는 알파벳 문자가 없어야 합니다.

이러한 ID를 사용하면 여러 CRMID가 &#39;잘못된&#39; ID와 함께 병합되는 다음과 같은 그래프가 생성될 수 있습니다.

![ID 값이 잘못되었거나 잘못된 ID 데이터의 그래프 예입니다.](../images/identity-settings/bad-data.png)

[!DNL Identity Graph Linking Rules]을(를) 사용하면 이 유형의 데이터로 인해 원치 않는 프로필이 축소되는 것을 방지하기 위해 CRMID를 고유 식별자로 구성할 수 있습니다.

## [!DNL Identity Graph Linking Rules] {#identity-graph-linking-rules}

[!DNL Identity Graph Linking Rules]을(를) 사용하여 다음을 수행할 수 있습니다.

* 고유한 네임스페이스를 구성하여 각 사용자에 대해 단일 ID 그래프/병합된 프로필을 만듭니다. 이렇게 하면 서로 다른 두 개인 식별자가 하나의 ID 그래프로 병합되지 않습니다.
* 우선 순위를 구성하여 온라인에서 인증된 이벤트를 사용자에게 연결

### 용어 {#terminology}

| 용어 | 설명 |
| --- | --- |
| 고유한 네임스페이스 | 고유 네임스페이스는 ID 그래프의 컨텍스트 내에서 구별되도록 설정된 ID 네임스페이스입니다. UI를 사용하여 네임스페이스를 고유하도록 구성할 수 있습니다. 네임스페이스가 고유 ID로 정의되면 그래프에는 해당 네임스페이스를 포함하는 ID가 하나만 있을 수 있습니다. |
| 네임스페이스 우선순위 | 네임스페이스 우선 순위는 네임스페이스 간의 상대적 중요도를 나타냅니다. 네임스페이스 우선 순위는 UI를 통해 구성할 수 있습니다. 주어진 ID 그래프에서 네임스페이스의 등급을 지정할 수 있습니다. 활성화되면 ID 최적화 알고리즘에 대한 입력 및 경험 이벤트 조각에 대한 기본 ID 결정과 같은 다양한 시나리오에서 이름 우선 순위가 사용됩니다. |
| ID 최적화 알고리즘 | ID 최적화 알고리즘을 사용하면 고유한 네임스페이스 및 네임스페이스 우선 순위를 구성하여 만든 지침이 주어진 ID 그래프에 적용되도록 할 수 있습니다. |

### 고유한 네임스페이스 {#unique-namespace}

ID 설정 UI 작업 영역을 사용하여 네임스페이스를 고유하도록 구성할 수 있습니다. 이렇게 하면 주어진 그래프가 고유한 네임스페이스를 포함하는 하나의 ID만 가질 수 있음을 ID 최적화 알고리즘에 알립니다. 이렇게 하면 동일한 그래프 내에 서로 다른 두 개인 식별자가 병합되는 것을 방지할 수 있습니다.

다음 시나리오를 고려하십시오.

* Scott은 태블릿을 사용하고 자신의 Google Chrome 브라우저를 열어 acme<span>.com으로 이동한 다음 로그인하여 새 농구화를 찾습니다.
   * 이 시나리오에서는 배후에 다음 ID를 기록합니다.
      * 브라우저의 사용을 나타내는 ECID 네임스페이스 및 값입니다
      * 인증된 사용자(Scott이 사용자 이름 및 암호 조합으로 로그인함)를 나타내는 CRMID 네임스페이스 및 값입니다.
* 그런 다음 아들 피터는 같은 태블릿을 사용하고 Google Chrome을 사용하여 acme<span>.com으로 이동하며 자신의 계정으로 로그인하여 축구 장비를 찾습니다.
   * 이 시나리오에서는 배후에 다음 ID를 기록합니다.
      * 브라우저를 나타내는 동일한 ECID 네임스페이스 및 값입니다.
      * 인증된 사용자를 나타내는 새 CRMID 네임스페이스 및 값입니다.

CRMID가 고유한 네임스페이스로 구성된 경우 ID 최적화 알고리즘은 CRMID를 함께 병합하지 않고 두 개의 개별 ID 그래프로 분할합니다.

고유한 네임스페이스를 구성하지 않으면 CRMID 네임스페이스가 동일하지만 ID 값이 다른 두 ID와 같이 원치 않는 그래프 병합이 발생할 수 있습니다(이러한 시나리오는 동일한 그래프에서 두 개의 서로 다른 개인 엔티티를 나타내는 경우가 많음).

지정된 ID 그래프에 수집되는 ID 데이터에 제한을 적용하려면 ID 최적화 알고리즘에 알리도록 고유한 네임스페이스를 구성해야 합니다.

### 네임스페이스 우선순위 {#namespace-priority}

네임스페이스 우선 순위는 네임스페이스 간의 상대적 중요도를 나타냅니다. 네임스페이스 우선 순위는 UI를 통해 구성할 수 있으며 주어진 ID 그래프에서 네임스페이스의 등급을 지정할 수 있습니다.

네임스페이스 우선 순위가 사용되는 한 가지 방법은 실시간 고객 프로필에서 경험 이벤트 조각(사용자 비헤이비어)의 기본 ID를 결정하는 것입니다. 우선 순위 설정이 구성된 경우 저장된 프로필 조각을 결정하는 데 웹 SDK의 기본 ID 설정이 더 이상 사용되지 않습니다.

고유 네임스페이스 및 네임스페이스 우선 순위는 모두 ID 설정 UI 작업 영역에서 구성할 수 있습니다. 그러나 이러한 구성의 효과는 서로 다릅니다.

| | ID 서비스 | 실시간 고객 프로필 |
| --- | --- | --- |
| 고유한 네임스페이스 | ID 서비스에서 ID 최적화 알고리즘은 주어진 ID 그래프에 수집되는 ID 데이터를 결정하기 위한 고유한 네임스페이스를 나타냅니다. | 고유 네임스페이스는 실시간 고객 프로필에 영향을 주지 않습니다. |
| 네임스페이스 우선순위 | ID 서비스에서 여러 계층이 있는 그래프의 경우 네임스페이스 우선 순위에 따라 적절한 링크가 제거되는지 결정됩니다. | 경험 이벤트가 프로필에서 수집되면 우선 순위가 가장 높은 네임스페이스가 프로필 조각의 기본 ID가 됩니다. |

* 그래프당 50개 ID 제한에 도달하면 네임스페이스 우선 순위가 그래프 동작에 영향을 주지 않습니다.
* **네임스페이스 우선 순위는 상대적 중요도를 나타내는 네임스페이스에 할당된 숫자 값입니다**. 네임스페이스의 속성입니다.
* **기본 ID는 프로필 조각이 저장된 ID입니다**. 프로필 조각은 특정 사용자에 대한 정보, 즉 속성(일반적으로 CRM 레코드를 통해 수집됨) 또는 이벤트(일반적으로 경험 이벤트 또는 온라인 데이터에서 수집됨)를 저장하는 데이터 레코드입니다.
* 네임스페이스 우선 순위는 경험 이벤트 조각의 기본 ID를 결정합니다.
   * 프로필 레코드의 경우 Experience Platform UI의 스키마 작업 영역을 사용하여 기본 ID를 포함한 ID 필드를 정의할 수 있습니다. 자세한 내용은 [UI에서 ID 필드 정의](../../xdm/ui/fields/identity.md)에 대한 안내서를 참조하십시오.
* 경험 이벤트에 identityMap에서 가장 높은 네임스페이스 우선 순위를 가진 ID가 두 개 이상 있는 경우 &quot;잘못된 데이터&quot;로 간주되므로 수집이 거부됩니다. 예를 들어 identityMap에 `{ECID: 111, CRMID: John, CRMID: Jane}`이(가) 포함되어 있으면 이벤트가 `CRMID: John` 및 `CRMID: Jane`에 동시에 연결되어 있음을 의미하므로 전체 이벤트가 잘못된 데이터로 거부됩니다.

자세한 내용은 [네임스페이스 우선 순위](./namespace-priority.md)에 대한 안내서를 참조하십시오.

## 다음 단계

[!DNL Identity Graph Linking Rules]에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [ID 최적화 알고리즘](./identity-optimization-algorithm.md)
* [구현 안내서](./implementation-guide.md)
* [그래프 구성의 예](./example-configurations.md)
* [문제 해결 및 FAQ](./troubleshooting.md)
* [네임스페이스 우선순위](./namespace-priority.md)
* [그래프 시뮬레이션 UI](./graph-simulation.md)
* [ID 설정 UI](./identity-settings-ui.md)