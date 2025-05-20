---
title: 네임스페이스 우선순위
description: ID 서비스의 네임스페이스 우선 순위에 대해 알아봅니다.
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: 579489e711858c3e80ca5d14eb4ad9187ecf80f8
workflow-type: tm+mt
source-wordcount: '2102'
ht-degree: 2%

---

# 네임스페이스 우선순위 {#namespace-priority}

>[!CONTEXTUALHELP]
>id="platform_identities_namespacepriority"
>title="네임스페이스 우선순위"
>abstract="네임스페이스 우선순위는 링크가 아이덴티티 그래프에서 제거되는 방식을 결정합니다."

모든 고객 구현은 특정 조직의 목표를 충족하도록 고유하고 맞춤화되며, 따라서 지정된 네임스페이스의 중요성은 고객마다 다릅니다. 실제 사례는 다음과 같습니다.

* 회사에서 각 전자 메일 주소를 단일 개인 엔터티를 나타내도록 간주할 수 있으므로 [ID 설정](./identity-settings-ui.md)을 사용하여 전자 메일 네임스페이스를 고유하게 구성할 수 있습니다. 그러나 다른 회사에서는 1인 엔티티를 여러 개의 이메일 주소가 있는 것으로 나타내어 이메일 네임스페이스를 고유하지 않도록 구성할 수 있습니다. 이러한 회사에서는 여러 이메일 주소에 연결된 1인 식별자가 있을 수 있도록 CRMID 네임스페이스와 같은 고유한 다른 ID 네임스페이스를 사용해야 합니다.
* &quot;로그인 ID&quot; 네임스페이스를 사용하여 온라인 동작을 수집할 수 있습니다. 이 로그인 ID는 CRMID와 1:1 관계를 가질 수 있으며, 이는 CRM 시스템의 속성을 저장하고 가장 중요한 네임스페이스로 간주될 수 있습니다. 이 경우 CRMID 네임스페이스가 개인을 더 정확하게 나타내는 반면 로그인 ID 네임스페이스가 두 번째로 가장 중요하다고 판단하게 됩니다.

프로필 및 관련 ID 그래프의 형성 및 분할 방식에 영향을 주므로 ID 서비스에서 네임스페이스의 중요성을 반영하는 구성을 수행해야 합니다.

## 우선 순위 결정

네임스페이스 우선 순위 결정은 다음 요소를 기반으로 합니다.

### ID 그래프 구조

조직의 그래프 구조가 계층화된 경우 네임스페이스 우선 순위는 이를 반영하여 그래프 축소에서 올바른 링크가 제거되도록 해야 합니다.

>[!TIP]
>
>* &quot;그래프 축소&quot;는 여러 개별 프로필이 실수로 하나의 ID 그래프에 병합되는 시나리오를 의미합니다.
>
>* 레이어 그래프는 여러 수준의 링크가 있는 ID 그래프를 나타냅니다. 세 개의 레이어가 있는 그래프의 예를 보려면 아래 이미지를 보십시오.

![그래프 레이어 다이어그램](../images/namespace-priority/graph-layers.png)

### 네임스페이스의 의미론적 의미

ID는 실제 개체를 나타냅니다. ID 그래프에 표시되는 객체는 세 개입니다. 중요도 순서로 다음과 같습니다.

* 사람(크로스 디바이스, 이메일, 전화번호)
* 하드웨어 장치
* 웹 브라우저(쿠키)

개인 네임스페이스는 웹 브라우저에 비해 상대적으로 변경이 불가능한 하드웨어 장치(예: IDFA, GAID)에 비해 상대적으로 변경이 불가능합니다. 기본적으로 사용자(사용자)는 항상 단일 엔티티이며, 여러 하드웨어 장치(전화, 노트북, 태블릿 등)를 사용하고 여러 브라우저(Google Chrome, Safari, FireFox 등)를 사용할 수 있습니다.

이 주제에 접근하는 또 다른 방법은 카디널리티를 통해서이다. 주어진 개인에 대해 몇 개의 ID가 만들어집니까? 대부분의 경우 한 사람은 CRMID, 소수의 하드웨어 장치 식별자(IDFA/GAID 재설정은 자주 발생하지 않아야 함) 및 훨씬 더 많은 쿠키(개인이 여러 장치에서 탐색하거나 시크릿 모드를 사용하거나 지정된 시간에 쿠키를 재설정할 수 있음)를 갖게 됩니다. 일반적으로 **낮은 카디널리티는 더 높은 값을 가진 네임스페이스를 나타냅니다**.

## 네임스페이스 우선 순위 설정 유효성 검사

네임스페이스의 우선 순위를 정하는 방법에 대한 아이디어가 있으면 UI에서 그래프 시뮬레이션 도구를 사용하여 다양한 그래프 축소 시나리오를 테스트하고 우선 순위 구성이 예상 그래프 결과를 반환하는지 확인할 수 있습니다. 자세한 내용은 [그래프 시뮬레이션 도구 사용 가이드](./graph-simulation.md)를 참조하세요.

## 네임스페이스 우선 순위 구성

[ID 설정 UI](./identity-settings-ui.md)를 사용하여 네임스페이스 우선 순위를 구성할 수 있습니다. ID 설정 인터페이스에서 네임스페이스를 드래그 앤 드롭하여 상대적 중요도를 결정할 수 있습니다.

>[!IMPORTANT]
>
>디바이스/쿠키 네임스페이스에 개인 네임스페이스보다 우선 순위를 지정할 수 없습니다. 이 제한은 잘못된 구성이 발생하지 않도록 합니다.

## 네임스페이스 우선 순위 사용

현재 네임스페이스 우선 순위는 실시간 고객 프로필의 시스템 동작에 영향을 줍니다. 아래 다이어그램은 이 개념을 보여 줍니다. 자세한 내용은 [Adobe Experience Platform 및 응용 프로그램 아키텍처 다이어그램](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications)에 대한 안내서를 참조하십시오.

![네임스페이스 우선 순위 응용 프로그램 범위의 다이어그램](../images/namespace-priority/application-scope.png)

## Identity Service: Identity Optimization 알고리즘

비교적 복잡한 그래프 구조의 경우, 네임스페이스 우선 순위는 그래프 축소 시나리오가 발생할 때 올바른 링크가 제거되도록 하는 데 중요한 역할을 합니다. 자세한 내용은 [ID 최적화 알고리즘 개요](../identity-graph-linking-rules/identity-optimization-algorithm.md)를 참조하세요.

## 실시간 고객 프로필: 경험 이벤트에 대한 기본 ID 결정

* 지정된 샌드박스에 대한 ID 설정을 구성하면 경험 이벤트에 대한 기본 ID가 구성에서 가장 높은 네임스페이스 우선 순위에 따라 결정됩니다.
   * 이는 체험 행사가 그 자체로 역동적이기 때문이다. ID 맵에는 3개 이상의 ID가 포함될 수 있으며 네임스페이스 우선 순위는 가장 중요한 네임스페이스가 경험 이벤트에 연결되어 있도록 합니다.
* 따라서 다음 구성 **은(는) 더 이상 실시간 고객 프로필에서 사용되지 않습니다**:
   * 웹 SDK, Mobile SDK 또는 Edge Network API를 사용하여 `identityMap`에서 ID를 보낼 때 기본 ID 구성(`primary=true`)이 사용됩니다(ID 네임스페이스 및 ID 값은 프로필에서 계속 사용됨). **참고**: 데이터 레이크 저장소 또는 Adobe Target과 같은 실시간 고객 프로필 외부의 서비스는 기본 ID 구성(`primary=true`)을 계속 사용합니다.
   * XDM 경험 이벤트 클래스 스키마에서 기본 ID로 표시된 모든 필드.
   * Adobe Analytics 소스 커넥터(ECID 또는 AAID)의 기본 기본 ID 설정.
* 반면 **네임스페이스 우선 순위는 프로필 레코드의 기본 ID를 결정하지 않습니다**.
   * 프로필 레코드의 경우 기본 ID를 포함하여 스키마에서 ID 필드를 계속 정의해야 합니다. 자세한 내용은 [UI에서 ID 필드 정의](../../xdm/ui/fields/identity.md)에 대한 안내서를 참조하십시오.

>[!TIP]
>
>* 네임스페이스 우선 순위는 **네임스페이스의 속성**&#x200B;입니다. 네임스페이스에 할당되어 상대적 중요도를 나타내는 숫자 값입니다.
>
>* 기본 ID는 프로필 조각이 저장되는 ID입니다. 프로필 조각은 특정 사용자에 대한 정보(예: 속성(CRM 레코드) 또는 이벤트(예: 웹 사이트 검색))를 저장하는 데이터 레코드입니다.

### 예시 상황

이 섹션에서는 우선 순위 구성이 데이터에 어떤 영향을 미칠 수 있는지 예를 제공합니다.

주어진 샌드박스에 대해 다음 구성이 설정되었다고 가정해 봅시다.

| 네임스페이스 | 네임스페이스의 실제 애플리케이션 | 우선 순위 |
| --- | --- | --- |
| CRMID | 사용자 | 1 |
| IDFA | Apple 하드웨어 장치(iPhone, IPad 등) | 2 |
| GAID | Google 하드웨어 장치(Google Pixel, Pixelbook 등) | 3 |
| ECID | 웹 브라우저(Firefox, Safari, Google Chrome 등) | 4 |
| AAID | 웹 브라우저 | 5 |

{style="table-layout:auto"}

위에 설명된 구성이 주어지면 사용자 작업과 기본 ID 결정은 다음과 같이 해결됩니다.

| 사용자 작업(경험 이벤트) | 인증 상태 | 데이터 소스 | 이벤트의 네임스페이스 | 기본 ID 네임스페이스 |
| --- | --- | --- | --- | --- |
| 신용 카드 오퍼 페이지 보기 | 인증되지 않음(익명) | Web SDK | `{ECID}` | ECID |
| 도움말 페이지 보기 | 인증되지 않음 | Mobile SDK | `{ECID, IDFA}` | IDFA |
| 당좌 예금 잔액 조회 | Authenticated | Web SDK | `{CRMID, ECID}` | CRMID |
| 주택 융자에 등록 | Authenticated | Analytics 소스 커넥터 | `{CRMID, ECID, AAID}` | CRMID |
| $1,000를 수표에서 저축으로 전송 | Authenticated | Mobile SDK | `{CRMID, GAID, ECID}` | CRMID |

{style="table-layout:auto"}

## 세그먼테이션 서비스: 세그먼트 멤버십 메타데이터 저장소

![세그먼트 멤버십 저장소 다이어그램](../images/namespace-priority/segment-membership-storage.png)

병합된 프로필이 지정된 경우 네임스페이스 우선 순위가 가장 높은 ID에 대해 세그먼트 멤버십이 저장됩니다.

예를 들어 다음 두 가지 프로필이 있다고 가정해 보겠습니다.

* 프로필 1은 John을 나타냅니다.
   * John의 프로필은 S1(세그먼트 멤버십 1)에 대한 자격이 있습니다. 예를 들어 S1은 남성으로 식별하는 고객 세그먼트를 의미할 수 있습니다.
   * John의 프로필도 S2(세그먼트 멤버십 2)에 참가할 수 있습니다. 충성도 상태가 gold인 고객 세그먼트를 의미할 수 있습니다.
* 프로필 2는 제인을 나타냅니다.
   * Jane의 프로필은 S3(세그먼트 멤버십 3)에 사용할 수 있습니다. 이는 여성으로 식별하는 고객 세그먼트를 의미할 수 있습니다.
   * Jane의 프로필도 S4(세그먼트 멤버십 4)에 참가할 수 있습니다. 충성도 상태가 백금인 고객의 세그먼트를 참조할 수 있습니다.

John과 Jane이 장치를 공유하는 경우 ECID(웹 브라우저)가 한 사람에서 다른 사람으로 이동합니다. 단, 이는 John과 Jane에 대해 저장된 세그먼트 멤버십 정보에 영향을 주지 않습니다.

세그먼트 자격 기준이 ECID에 대해 저장된 익명 이벤트만을 기반으로 하는 경우 Jane은 해당 세그먼트에 대한 자격을 갖습니다.

## 기타 Experience Platform 서비스에 대한 영향 {#implications}

이 섹션에서는 네임스페이스 우선 순위가 다른 Experience Platform 서비스에 어떤 영향을 미칠 수 있는지 간략하게 설명합니다.

### 고급 데이터 라이프사이클 관리

데이터 위생 레코드 삭제 요청은 특정 ID에 대해 다음 방식으로 작동합니다.

* 실시간 고객 프로필: 지정된 ID를 기본 ID로 하는 프로필 조각을 삭제합니다. **이제 네임스페이스의 기본 ID가 네임스페이스 우선 순위에 따라 결정됩니다.**
* 데이터 레이크: 지정된 ID를 기본 ID로 하는 레코드를 삭제합니다. 실시간 고객 프로필과 달리, 데이터 레이크의 기본 ID는 WebSDK(`primary=true`)에 지정된 기본 ID 또는 기본 ID로 표시된 필드를 기반으로 합니다

자세한 내용은 [고급 수명 주기 관리 개요](../../hygiene/home.md)를 참조하십시오.

### 계산된 속성

ID 설정이 활성화된 경우 계산된 속성은 네임스페이스 우선 순위를 사용하여 계산된 속성 값을 저장합니다. 주어진 이벤트에 대해 네임스페이스 우선 순위가 가장 높은 ID는 계산된 속성 값을 해당 이벤트에 대해 기록합니다. 자세한 내용은 [연산 특성 UI 안내서](../../profile/computed-attributes/ui.md)를 참조하십시오.

### 데이터 레이크

데이터 레이크에 대한 데이터 수집은 [웹 SDK](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) 및 스키마에 구성된 기본 ID 설정을 계속 적용합니다.

데이터 레이크는 네임스페이스 우선 순위를 기반으로 기본 ID를 결정하지 않습니다. 예를 들어 Adobe Customer Journey Analytics은 데이터 레이크의 데이터를 사용하므로 네임스페이스 우선 순위가 활성화된 후에도(예: 새 연결에 데이터 세트 추가) Customer Journey Analytics은 ID 맵에서 값을 계속 사용합니다.

### XDM(경험 데이터 모델) 스키마

XDM 개인 프로필과 같이 XDM 경험 이벤트가 아닌 스키마는 ID로 표시한 [개 필드를 계속 적용합니다](../../xdm/ui/fields/identity.md).

XDM 스키마에 대한 자세한 내용은 [스키마 개요](../../xdm/home.md)를 참조하십시오.

### 인텔리전트 서비스

데이터를 선택할 때 점수를 계산하는 이벤트와 계산된 점수를 저장하는 이벤트를 결정하는 데 사용할 네임스페이스를 지정해야 합니다. 개인을 나타내는 네임스페이스를 선택하는 것이 좋습니다.

* WebSDk를 사용하여 웹 동작 데이터를 수집하는 경우 ID 맵 내에서 CRMID 네임스페이스를 선택하는 것이 좋습니다.
* Analytics 소스 커넥터를 사용하여 웹 동작 데이터를 수집하는 경우 CRMID(ID 설명자)를 선택해야 합니다.

이 구성은 인증된 이벤트를 사용해서만 점수를 계산하는 결과를 초래합니다.

자세한 내용은 [Attribution AI](../../intelligent-services/attribution-ai/overview.md) 및 [Customer AI](../../intelligent-services/customer-ai/overview.md)에 대한 문서를 참조하십시오.

### 파트너가 빌드한 대상

공유 장치와 관련된 프로필에 대한 업데이트된 대상 실격 결과는 다운스트림 대상으로 전송되지 않을 수 있습니다. 이는 다음과 같은 드문 특정 상황에서 발생할 수 있습니다.

* 대상 자격은 익명 활동만 기반으로 합니다.
* 여러 프로필에 대한 로그인은 짧은 기간에 이루어집니다.

파트너가 만든 대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md#adobe-built-and-partner-built-destinations)를 참조하십시오.

### Privacy Service

[Privacy Service 삭제 요청](../privacy.md)은(는) 특정 id에 대해 다음과 같은 방식으로 작동합니다.

* 실시간 고객 프로필: 지정된 ID 값을 기본 ID로 하는 프로필 조각을 삭제합니다. **이제 네임스페이스의 기본 ID가 네임스페이스 우선 순위에 따라 결정됩니다.**
* 데이터 레이크: 지정된 ID를 기본 또는 보조 ID로 사용하는 레코드를 삭제합니다.

자세한 내용은 [개인 정보 보호 서비스 개요](../../privacy-service/home.md)를 참조하세요.

### Edge 세그멘테이션 및 Edge Network 애플리케이션

[!DNL Identity Graph Linking Rules]의 컨텍스트에서는 Edge 세그멘테이션 및 Edge Network 응용 프로그램에 대해 유의해야 할 두 가지 주요 동작 변경 내용이 있습니다.

1. `identityMap`은(는) 고유한 것으로 표시된 개인 네임스페이스를 포함해야 합니다. ID(ID 설명자)로 표시된 필드는 지원되지 않습니다.
2. 최종 사용자가 인증된 상태에서 탐색하는 경우 개인 네임스페이스에 `primary = true` 구성이 있어야 합니다.

#### 에지 세분화

특정 이벤트에서는 [XDM 필드](../../xdm/ui/fields/identity.md)(으)로 전송된 ID가 무시되고 세그먼트 멤버십 메타데이터 저장소에 사용되지 않으므로 개인 엔터티를 나타내는 모든 네임스페이스가 `identityMap`에 포함되어 있는지 확인하십시오.

* **이벤트 적용 가능성**: 이 동작은 Edge Network(예: WebSDK 및 Mobile SDK)로 직접 전송된 이벤트에만 적용됩니다. HTTP API 소스, 기타 스트리밍 소스 및 일괄 처리 소스와 함께 수집된 이벤트와 같이 [Experience Platform 허브](../../landing/edge-and-hub-comparison.md)에서 수집된 이벤트에는 이 제한이 적용되지 않습니다.
* **Edge 세그멘테이션 특성**: 이 동작은 가장자리 세그멘테이션에만 적용됩니다. 배치 및 스트리밍 세분화는 허브에서 평가되는 별도의 서비스이며 동일한 프로세스를 따르지 않습니다. 자세한 내용은 [Edge 세그멘테이션 안내서](../../segmentation/methods/edge-segmentation.md)를 참조하십시오.
* 자세한 내용은 [Adobe Experience Platform 및 응용 프로그램 아키텍처 다이어그램](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications#detailed-architecture-diagram) 및 [Edge Network 및 허브 비교](../../landing/edge-and-hub-comparison.md) 페이지를 참조하십시오.

#### Edge Network 애플리케이션

Edge Network의 응용 프로그램이 지체 없이 Edge 프로필에 액세스할 수 있도록 하려면 이벤트에 CRMID의 `primary=true`이(가) 포함되어 있는지 확인하십시오. 이렇게 하면 허브에서 ID 그래프 업데이트를 기다리지 않고 즉시 사용할 수 있습니다.

* Adobe Target, Offer Decisioning 및 사용자 지정 Personalization 대상 등 Edge Network의 애플리케이션은 계속해서 이벤트의 기본 ID를 사용하여 Edge 프로필의 프로필에 액세스합니다.
* Edge Network 동작에 대한 자세한 내용은 [Experience Platform 웹 SDK 및 Edge Network 아키텍처 다이어그램](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/deployment/websdk#experience-platform-webmobile-sdk-or-edge-network-server-api-deployment)을 참조하세요.
* Web SDK에서 기본 ID를 구성하는 방법에 대한 자세한 내용은 [데이터 요소 유형](../../tags/extensions/client/web-sdk/data-element-types.md) 및 [Web SDK의 ID 데이터](../../web-sdk/identity/overview.md)에 대한 설명서를 참조하십시오.
* ECID가 경험 이벤트에 포함되어 있는지 확인합니다. ECID가 누락된 경우 `primary=true`이(가) 있는 이벤트 페이로드에 추가되므로 예기치 않은 결과가 발생할 수 있습니다.