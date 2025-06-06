---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;열거형;기본 ID;기본 ID;XDM 개별 프로필;경험 이벤트;XDM 경험 이벤트;XDM 경험 이벤트;experienceEvent;experienceevent;XDM 경험 이벤트;스키마 디자인;우수 사례
solution: Experience Platform
title: 데이터 모델링 우수 사례
description: 이 문서에서는 XDM(경험 데이터 모델) 스키마와 Adobe Experience Platform에서 사용할 스키마를 구성하기 위한 구성 요소, 원칙 및 모범 사례에 대해 소개합니다.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: 7521273c0ea4383b7141e9d7a82953257ff18c34
workflow-type: tm+mt
source-wordcount: '3236'
ht-degree: 1%

---

# 데이터 모델링을 위한 모범 사례

[!DNL Experience Data Model]&#x200B;(XDM)은 다운스트림 Adobe Experience Platform 서비스에서 사용할 일반적인 구조 및 정의를 제공하여 고객 경험 데이터를 표준화하는 핵심 프레임워크입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 고객 작업에서 중요한 통찰력을 얻고 고객 대상을 정의하고 개인화를 위해 고객 특성을 표현하는 데 사용할 수 있습니다.

XDM은 디자인으로 인해 매우 다재다능하고 사용자 정의가 가능하므로 스키마를 디자인할 때 데이터 모델링에 대한 모범 사례를 따르는 것이 중요합니다. 이 문서에서는 고객 경험 데이터를 XDM에 매핑할 때 수행해야 하는 주요 의사 결정 및 고려 사항을 다룹니다.

## 시작하기

이 안내서를 읽기 전에 [XDM 시스템 개요](../home.md)에서 XDM과 Experience Platform 내에서의 역할에 대한 높은 수준의 소개를 검토하십시오.

이 안내서는 스키마 디자인과 관련된 주요 고려 사항에만 중점을 두므로 이 안내서 전체에서 언급된 개별 스키마 요소에 대한 자세한 설명은 [스키마 컴포지션의 기본 사항](./composition.md)을 읽어 보는 것이 좋습니다.

## 모범 사례 요약 {#summary}

Experience Platform에서 사용할 데이터 모델을 디자인하는 데 권장되는 접근 방식은 다음과 같이 요약할 수 있습니다.

1. 데이터에 대한 비즈니스 사용 사례를 이해합니다.
1. 이러한 사용 사례를 해결하기 위해 Experience Platform으로 가져와야 하는 기본 데이터 소스를 식별합니다.
1. 관심이 있을 수 있는 보조 데이터 소스를 식별합니다. 예를 들어, 현재 조직의 한 사업부만 데이터를 Experience Platform으로 포팅하려는 경우 유사한 사업부도 향후에 유사한 데이터를 포팅하려는 경우 이러한 문제가 발생할 수 있습니다. 이러한 보조 소스를 사용하면 전체 조직에서 데이터 모델을 표준화할 수 있습니다.
1. 식별된 데이터 소스에 대한 높은 수준의 ERD(엔티티 관계 다이어그램)를 만듭니다.
1. 높은 수준의 ERD를 Experience Platform 중심의 ERD(프로필, 경험 이벤트 및 조회 엔티티 포함)로 변환합니다.

비즈니스 사용 사례를 수행하는 데 필요한 적용 가능한 데이터 소스 식별과 관련된 단계는 조직마다 다릅니다. 이 문서의 나머지 섹션에서는 데이터 소스가 식별된 후 ERD를 구성하고 구성하는 마지막 단계에 중점을 두고 있지만, 다이어그램의 다양한 구성 요소에 대한 설명은 데이터 소스 중 어느 것을 Experience Platform으로 마이그레이션해야 하는지에 대한 의사 결정에 영향을 줄 수 있습니다.

## 높은 수준의 ERD 만들기 {#create-an-erd}

Experience Platform으로 가져올 데이터 소스를 결정했으면 높은 수준의 ERD를 만들어 데이터를 XDM 스키마에 매핑하는 프로세스를 안내합니다.

아래 예제는 Experience Platform으로 데이터를 가져오려는 회사에 대한 간소화된 ERD를 나타냅니다. 다이어그램은 고객 계정, 호텔 및 몇 가지 일반적인 전자 상거래 이벤트를 포함하여 XDM 클래스로 정렬해야 하는 필수 엔터티를 강조 표시합니다.

![데이터 수집을 위해 XDM 클래스로 정렬해야 하는 필수 엔터티를 강조 표시하는 엔터티 관계 다이어그램입니다.](../images/best-practices/erd.png)

## 프로필, 조회 및 이벤트 카테고리로 엔티티 정렬 {#sort-entities}

Experience Platform으로 가져올 필수 엔티티를 식별하기 위해 ERD를 만들었으면 이러한 엔티티를 프로필, 조회 및 이벤트 카테고리로 정렬해야 합니다.

| 카테고리 | 설명 |
| --- | --- |
| 프로필 엔티티 | 프로필 엔티티는 개인(일반적으로 고객)과 관련된 속성을 나타냅니다. 이 범주에 속하는 엔터티는 **[!DNL XDM Individual Profile]클래스**&#x200B;을(를) 기반으로 하는 스키마로 표시되어야 합니다. |
| 엔터티 조회 | 조회 엔티티는 개별 개인과 관련될 수 있지만 개인을 식별하는 데 직접 사용될 수 없는 개념을 나타냅니다. 이 범주에 속하는 엔터티는 **사용자 지정 클래스**&#x200B;를 기반으로 하는 스키마로 표시되어야 하며 [스키마 관계](../tutorials/relationship-ui.md)를 통해 프로필 및 이벤트에 연결되어 있습니다. |
| 이벤트 엔티티 | 이벤트 엔티티는 고객이 수행할 수 있는 작업, 시스템 이벤트 또는 시간에 따른 변경 사항을 추적할 수 있는 기타 개념과 관련된 개념을 나타냅니다. 이 범주에 속하는 엔터티는 **[!DNL XDM ExperienceEvent]클래스**&#x200B;을(를) 기반으로 하는 스키마로 표시되어야 합니다. |

{style="table-layout:auto"}

### 엔티티 정렬 고려 사항 {#considerations}

아래 섹션에서는 엔티티를 위의 카테고리로 정렬하는 방법에 대한 추가 지침을 제공합니다.

#### 변경 가능한 데이터 및 변경 불가능한 데이터 {#mutable-and-immutable-data}

엔티티 카테고리 사이를 정렬하는 주요 방법은 캡처되는 데이터를 변경할 수 있는지 여부입니다.

프로필 또는 조회 엔티티에 속하는 속성은 일반적으로 변경할 수 있습니다. 예를 들어, 고객의 환경 설정은 시간이 지남에 따라 변경될 수 있으며, 구독 플랜의 매개 변수는 시장 트렌드에 따라 업데이트될 수 있습니다.

그와 대조적으로 이벤트 데이터는 일반적으로 변경할 수 없습니다. 이벤트가 특정 타임스탬프에 연결되므로 이벤트가 제공하는 &quot;시스템 스냅샷&quot;은 변경되지 않습니다. 예를 들어 이벤트는 장바구니를 체크아웃할 때 고객의 환경 설정을 캡처할 수 있으며, 나중에 고객의 환경 설정이 변경되더라도 변경되지 않습니다. 이벤트 데이터는 기록된 후에는 변경할 수 없습니다.

요약하면, 프로필 및 조회 엔티티는 변경 가능한 속성을 포함하며, 캡처 대상에 대한 최신 정보를 나타내는 반면 이벤트는 특정 시점의 시스템에 대한 변경 불가능한 레코드입니다.

#### 고객 속성 {#customer-attributes}

엔티티에 개별 고객과 관련된 속성이 포함된 경우 프로필 엔티티일 수 있습니다. 고객 속성의 예는 다음과 같습니다.

* 이름, 생년월일, 성별 및 계정 ID 등 개인 세부 정보.
* 주소 및 GPS 정보 등 위치 정보.
* 전화번호 및 이메일 주소 등 연락처 정보.

#### 시간 경과에 따른 데이터 추적 {#track-data}

엔티티 내의 특정 속성이 시간에 따라 어떻게 변경되는지 분석하려는 경우 이벤트 엔티티일 가능성이 높습니다. 예를 들어 장바구니에 제품 항목을 추가하는 것은 Experience Platform에서 장바구니에 추가 이벤트로 추적할 수 있습니다.

| 고객 ID | 유형 | 제품 ID | 수량 | 타임스탬프 |
| --- | --- | --- | --- | --- |
| 1234567 | 이벤트가 복제되지 않도록 하면서 현재 이벤트 변수에 | 275098 | 2 | 10월 1일 오전 10:32 |
| 1234567 | 제거 | 275098 | 1 | 10월 1일 오전 10:33 |
| 1234567 | 이벤트가 복제되지 않도록 하면서 현재 이벤트 변수에 | 486502 | 1 | 10월 1일 오전 10:41 |
| 1234567 | 이벤트가 복제되지 않도록 하면서 현재 이벤트 변수에 | 910482 | 5 | 10월 3일 오후 2:15 |

{style="table-layout:auto"}

#### 세그먼테이션 사용 사례 {#segmentation-use-cases}

엔티티를 분류할 때 특정 비즈니스 사용 사례를 해결하기 위해 빌드할 수 있는 대상을 고려하는 것이 중요합니다.

예를 들어 한 회사는 작년에 5회 이상 구입한 고객 충성도 프로그램의 &quot;골드&quot; 또는 &quot;플래티넘&quot; 회원을 모두 알고 싶어합니다. 이러한 세분화 논리를 기반으로 관련 엔터티가 어떻게 표시되어야 하는지에 대해 다음과 같은 결론을 내릴 수 있습니다.

* &quot;Gold&quot; 및 &quot;Platinum&quot;은 개별 고객에게 적용할 수 있는 충성도 상태를 나타냅니다. 세그먼테이션 논리는 고객의 현재 충성도 상태에만 관련되므로 이 데이터를 프로필 스키마의 일부로 모델링할 수 있습니다. 시간이 지남에 따라 충성도 상태의 변화를 추적하려는 경우 충성도 상태 변화에 대한 추가 이벤트 스키마를 생성할 수도 있습니다.
* 구매는 특정 시간에 발생하는 이벤트이며, 세분화 논리는 지정된 기간 내의 구매 이벤트와 관련이 있습니다. 따라서 이 데이터를 이벤트 스키마로 모델링해야 합니다.

#### 활성화 사용 사례 {#activation-use-cases}

세분화 사용 사례에 대한 고려 사항 외에도 해당 대상에 대한 활성화 사용 사례를 검토하여 추가적인 관련 속성을 식별해야 합니다.

예를 들어 회사에서 `country = US`에 대한 규칙을 기반으로 대상을 빌드했습니다. 그런 다음 특정 다운스트림 타겟으로 해당 대상자를 활성화하면 회사는 홈 상태를 기반으로 내보낸 모든 프로필을 필터링하려고 합니다. 따라서 적용 가능한 프로필 엔터티에서도 `state` 특성을 캡처해야 합니다.

#### 집계된 값 {#aggregated-values}

데이터의 사용 사례 및 세부기간에 따라 프로필 또는 이벤트 엔티티에 포함되기 전에 특정 값을 미리 집계해야 하는지 여부를 결정해야 합니다.

예를 들어 회사에서 장바구니 구매 수를 기반으로 대상을 구축하려고 합니다. 각 타임스탬프가 지정된 구매 이벤트를 자체 엔터티로 포함하여 이 데이터를 가장 낮은 세부 기간으로 통합하도록 선택할 수 있습니다. 그러나 이로 인해 기록된 이벤트의 수가 기하급수적으로 증가할 수 있습니다. 수집된 이벤트의 수를 줄이려면 1주일 또는 1개월 동안 집계 값 `numberOfPurchases`을(를) 만들도록 선택할 수 있습니다. MIN 및 MAX과 같은 다른 집계 함수도 이러한 상황에 적용할 수 있습니다.

>[!CAUTION]
>
>Experience Platform은 향후 릴리스에 예정되어 있지만 현재 자동 값 합계를 수행하지 않습니다. 집계된 값을 사용하도록 선택하는 경우 데이터를 Experience Platform으로 보내기 전에 외부에서 계산을 수행해야 합니다.

#### 카디널리티 {#cardinality}

ERD에 설정된 카디널리티는 또한 개체를 분류하는 방법에 대한 몇 가지 단서를 제공할 수 있습니다. 두 엔티티 간에 일대다 관계가 있는 경우 &quot;다&quot;를 나타내는 엔티티가 이벤트 엔티티일 가능성이 높습니다. 그러나 &quot;다&quot;가 프로필 엔티티 내에서 배열로 제공되는 조회 엔티티 세트인 경우도 있습니다.

>[!NOTE]
>
>모든 활용 사례에 맞는 보편적 접근법이 없기 때문에 카디널리티에 따른 개체 분류 시 각 상황별 장단점을 고려하는 것이 중요하다. 자세한 내용은 [다음 섹션](#pros-and-cons)을 참조하세요.

다음 표에서는 몇 가지 일반적인 엔티티 관계와 그로부터 파생될 수 있는 범주를 간략하게 설명합니다.

| 관계 | 카디널리티 | 엔티티 카테고리 |
| --- | --- | --- |
| 고객 및 카트 체크아웃 | 일대다 | 단일 고객은 시간이 지남에 따라 추적할 수 있는 이벤트인 장바구니 체크아웃을 많이 가질 수 있습니다. 따라서 고객은 프로필 엔티티가 되고 장바구니 체크아웃은 이벤트 엔티티가 됩니다. |
| 고객 및 충성도 계정 | 일대일 | 단일 고객은 하나의 충성도 계정만 가질 수 있으며 충성도 계정은 하나의 고객에게만 속할 수 있습니다. 관계가 일대일 관계이므로 고객 및 충성도 계정은 모두 프로필 엔티티를 나타냅니다. |
| 고객 및 구독 | 일대다 | 단일 고객은 많은 구독을 보유할 수 있습니다. 회사는 고객의 현재 가입에만 관련되므로 고객은 프로필 엔티티인 반면 가입은 조회 엔티티입니다. |

{style="table-layout:auto"}

### 다양한 엔티티 클래스의 장단점 {#pros-and-cons}

이전 섹션에서는 엔티티를 분류하는 방법을 결정하는 몇 가지 일반적인 지침을 제공했지만, 종종 다른 엔티티 카테고리보다 한 엔티티 카테고리를 선택하는 데 장단점이 있을 수 있음을 이해하는 것이 중요합니다. 다음 사례 연구는 이러한 상황에서 옵션을 고려할 수 있는 방법을 설명하기 위한 것입니다.

회사는 한 고객이 많은 구독을 가질 수 있는 고객의 활성 구독을 추적합니다. 또한 회사는 활성 구독이 있는 모든 사용자 찾기와 같은 세분화 사용 사례에 대한 구독을 포함하려고 합니다.

이 시나리오에는 데이터 모델에서 고객의 구독을 나타내는 두 가지 잠재적인 옵션이 있습니다.

1. [프로필 속성 사용](#profile-approach)
1. [이벤트 엔티티 사용](#event-approach)

#### 접근법 1: 프로필 속성 사용 {#profile-approach}

첫 번째 방법은 고객의 프로필 엔터티 내에 `subscriptionID` 배열을 포함하는 것입니다.

![클래스 및 구조가 강조 표시된 스키마 편집기의 고객 스키마](../images/best-practices/profile-schema.png)

**장점**

* 세분화는 의도한 사용 사례에 적합합니다.
* 스키마는 고객의 최신 구독 레코드만 보존합니다.

**단점**

* 배열의 모든 필드에 변경 사항이 발생할 때마다 전체 배열을 다시 지정해야 합니다.
* 서로 다른 데이터 소스 또는 사업부가 스토리지에 데이터를 공급하는 경우 업데이트된 최신 스토리지를 모든 채널에서 동기화해야 하는 어려움이 있습니다.

#### 접근법 2: 이벤트 엔티티 사용 {#event-approach}

두 번째 방법은 이벤트 스키마를 사용하여 구독 이벤트를 나타내는 것입니다. 여기에는 고객 ID와 함께 구독 ID 및 구독 이벤트가 발생한 시간의 타임스탬프가 포함됩니다.

![XDM 경험 이벤트 클래스와 구독 구조가 강조 표시된 구독 이벤트 스키마의 다이어그램입니다.](../images/best-practices/event-schema.png)

**장점**

* 세분화 규칙은 보다 유연하게 사용할 수 있습니다(예: 지난 30일 동안 구독을 변경한 모든 고객 찾기).
* 고객의 구독 상태가 변경되면 고객의 프로필 속성 내에서 더 이상 길고 복잡한 배열을 업데이트할 필요가 없습니다. 이 기능은 여러 소스에서 고객의 구독 목록이 동시에 변경되는 경우 특히 유용합니다.

**단점**

* 세분화는 원래 의도한 사용 사례(고객의 가장 최근 구독 상태 식별)에 대해 더 복잡해집니다. 이제 대상자는 고객이 상태를 확인할 수 있도록 마지막 구독 이벤트에 플래그를 지정하는 추가 논리가 필요합니다.
* 이벤트는 프로필 스토어에서 자동으로 만료되고 삭제될 위험이 더 높습니다. 자세한 내용은 [경험 이벤트 만료](../../profile/event-expirations.md)에 대한 안내서를 참조하십시오.

## 분류된 엔터티를 기반으로 스키마 만들기 {#schemas-for-categorized-entities}

엔티티를 프로필, 조회 및 이벤트 카테고리로 정렬했으면 데이터 모델을 XDM 스키마로 변환을 시작할 수 있습니다. 데모 목적으로 앞에 표시된 예제 데이터 모델은 다음 다이어그램에서 적절한 카테고리로 정렬되었습니다.

![프로필, 조회 및 이벤트 엔터티에 포함된 스키마 다이어그램](../images/best-practices/erd-sorted.png)

엔티티가 정렬되는 카테고리는 해당 스키마의 기반이 되는 XDM 클래스를 결정해야 합니다. 반복하려면:

* 프로필 엔터티는 [!DNL XDM Individual Profile] 클래스를 사용해야 합니다.
* 이벤트 엔터티는 [!DNL XDM ExperienceEvent] 클래스를 사용해야 합니다.
* 조회 엔티티는 조직에서 정의한 사용자 정의 XDM 클래스를 사용해야 합니다. 그런 다음 프로필 및 이벤트 엔티티는 스키마 관계를 통해 이러한 조회 엔티티를 참조할 수 있습니다.

>[!NOTE]
>
>이벤트 엔티티는 거의 항상 별도의 스키마로 표시되지만 프로필 또는 조회 카테고리의 엔티티는 카디널리티에 따라 단일 XDM 스키마에서 함께 결합될 수 있습니다.
>
>예를 들어 고객 엔터티는 LoyaltyAccount 엔터티와 일대일 관계를 가지므로 고객 엔터티의 스키마에는 각 고객에 대한 적절한 충성도 필드를 포함하는 `LoyaltyAccount` 개체도 포함될 수 있습니다. 그러나 관계가 일대다인 경우 &quot;다&quot;를 나타내는 엔티티는 복잡성에 따라 별도의 스키마 또는 프로필 속성 배열로 표시될 수 있습니다.

아래 섹션에서는 ERD를 기반으로 스키마를 구성하는 일반적인 지침을 제공합니다.

### 반복적인 모델링 방식 채택 {#iterative-modeling}

스키마 진화의 [규칙](./composition.md#evolution)은 스키마가 구현되면 비파괴적인 변경만 수행할 수 있음을 나타냅니다. 즉, 스키마에 필드를 추가하고 해당 필드에 대해 데이터가 수집되면 필드를 더 이상 제거할 수 없습니다. 따라서 시간이 지남에 따라 복잡성을 점진적으로 증가시키는 간소화된 구현부터 시작하여 스키마를 처음 만들 때 반복적인 모델링 접근 방식을 채택하는 것이 중요합니다.

스키마에 포함할 특정 필드가 필요한지 확실하지 않은 경우 제외하는 것이 좋습니다. 필드가 나중에 필요하다고 판단되면 항상 스키마의 다음 반복에 추가할 수 있습니다.

### ID 필드 {#identity-fields}

Experience Platform에서 ID로 표시된 XDM 필드는 여러 데이터 소스에서 가져온 개별 고객에 대한 정보를 결합하는 데 사용됩니다. 스키마에 ID로 표시된 필드가 여러 개 있을 수 있지만 [!DNL Real-Time Customer Profile]에서 사용할 수 있도록 스키마에 대해 하나의 기본 ID를 정의해야 합니다. 이러한 필드의 사용 사례에 대한 자세한 내용은 스키마 컴포지션 기본 사항의 [ID 필드](./composition.md#identity)에 대한 섹션을 참조하십시오.

스키마를 디자인할 때 관계형 데이터베이스 테이블의 모든 기본 키는 기본 ID에 대한 후보일 수 있습니다. 적용 가능한 ID 필드의 다른 예로는 고객 이메일 주소, 전화번호, 계정 ID 및 [ECID](../../identity-service/features/ecid.md)가 있습니다.

### Adobe 애플리케이션 스키마 필드 그룹 {#adobe-application-schema-field-groups}

Experience Platform은 다음 Adobe 애플리케이션과 관련된 데이터를 캡처할 수 있도록 기본 제공되는 여러 XDM 스키마 필드 그룹을 제공합니다.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

예를 들어 [[!UICONTROL Adobe Analytics ExperienceEvent 템플릿] 필드 그룹](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json)을 사용하여 [!DNL Analytics]별 필드를 XDM 스키마에 매핑할 수 있습니다. 작업 중인 Adobe 애플리케이션에 따라 스키마에서 이러한 Adobe 제공 필드 그룹을 사용해야 합니다.

![[!UICONTROL Adobe Analytics ExperienceEvent 템플릿의 스키마 다이어그램].](../images/best-practices/analytics-field-group.png)

Adobe 응용 프로그램 필드 그룹은 개별 고객의 표준 id 값을 매핑하는 시스템 생성 읽기 전용 개체인 `identityMap` 필드를 사용하여 기본 기본 id를 자동으로 할당합니다.

Adobe Analytics의 경우 ECID가 기본 기본 ID입니다. 고객이 ECID 값을 제공하지 않으면 기본 ID의 기본값이 AAID로 설정됩니다.

>[!IMPORTANT]
>
>Adobe 애플리케이션 필드 그룹을 사용할 때 다른 필드는 기본 ID로 표시되지 않아야 합니다. ID로 표시해야 하는 추가 속성이 있는 경우 이러한 필드를 보조 ID로 대신 할당해야 합니다.

## 데이터 유효성 검사 필드 {#data-validation-fields}

데이터를 데이터 레이크로 수집하면 제한된 필드에 대해서만 데이터 유효성 검사가 실행됩니다. 일괄 처리 수집 중에 특정 필드의 유효성을 검사하려면 필드를 XDM 스키마에서 제한된 것으로 표시해야 합니다. 잘못된 데이터가 Experience Platform에 수집되지 않도록 하려면 스키마를 생성할 때 필드 수준 유효성 검사에 대한 기준을 정의하는 것이 좋습니다.

>[!IMPORTANT]
>
>중첩된 열에는 유효성 검사가 적용되지 않습니다. 필드 형식이 배열 열 내에 있는 경우 데이터의 유효성을 검사하지 않습니다.

특정 필드에 대한 제약 조건을 설정하려면 스키마 편집기에서 필드를 선택하여 **[!UICONTROL 필드 속성]** 사이드바를 엽니다. 사용 가능한 필드에 대한 정확한 설명은 [유형별 필드 속성](../ui/fields/overview.md#type-specific-properties)에 대한 설명서를 참조하십시오.

![제약 조건 필드가 [!UICONTROL 필드 속성] 사이드바에서 강조 표시된 스키마 편집기.](../images/best-practices/data-validation-fields.png)

### 데이터 무결성을 유지하기 위한 팁 {#data-integrity-tips}

다음은 스키마를 만들 때 데이터 무결성을 유지하기 위한 제안 사항입니다.

* **기본 ID 고려**: 웹 SDK, 모바일 SDK, Adobe Analytics 및 Adobe Journey Optimizer과 같은 Adobe 제품의 경우 `identityMap` 필드가 기본 ID로 사용되는 경우가 많습니다. 추가 필드를 해당 스키마의 기본 ID로 지정하지 마십시오.
* **ID로 `_id`을(를) 사용하지 않는지 확인**: Experience Event 스키마의 `_id` 필드는 레코드 고유성을 위한 ID이므로 ID로 사용할 수 없습니다.
* **길이 제약 조건 설정**: ID로 표시된 필드에 최소 및 최대 길이를 설정하는 것이 좋습니다. 최소 및 최대 길이 제약 조건을 충족하지 않고 ID 필드에 사용자 지정 네임스페이스를 할당하려고 하면 경고가 트리거됩니다. 이러한 제한 사항은 일관성 및 데이터 품질을 유지하는 데 도움이 됩니다.
* **일관된 값에 패턴을 적용**: ID 값이 특정 패턴을 따르는 경우 **[!UICONTROL 패턴]** 설정을 사용하여 이 제약 조건을 적용해야 합니다. 이 설정에는 숫자만, 대문자, 소문자 또는 특정 문자 조합과 같은 규칙이 포함될 수 있습니다. 정규 표현식을 사용하여 문자열의 패턴을 일치시킵니다.
* **Analytics 스키마에서 eVar 제한**: 일반적으로 Analytics 스키마에는 ID로 지정된 eVar이 하나만 있어야 합니다. 두 개 이상의 eVar을 ID로 사용하려는 경우 데이터 구조를 최적화할 수 있는지 다시 확인해야 합니다.
* **선택한 필드가 고유한지 확인**: 선택한 필드는 스키마의 기본 ID와 비교하여 고유해야 합니다. 그렇지 않은 경우 ID로 표시하지 않습니다. 예를 들어 여러 고객이 동일한 이메일 주소를 제공할 수 있는 경우 해당 네임스페이스는 적합한 ID가 아닙니다. 이 원칙은 전화번호와 같은 다른 ID 네임스페이스에도 적용됩니다. 고유하지 않은 필드를 ID로 표시하면 원치 않는 프로필이 축소될 수 있습니다.
* **최소 문자열 길이 확인**: 문자열 값은 비워 둘 수 없으므로 모든 문자열 필드는 길이가 최소 한 자 이상이어야 합니다. 그러나 필수가 아닌 필드에는 Null 값을 사용할 수 있습니다. 새 문자열 필드에는 기본적으로 최소 1의 길이가 제공됩니다.

## 다음 단계

이 문서에서는 Experience Platform용 데이터 모델을 설계하기 위한 일반 지침 및 모범 사례에 대해 다룹니다. 요약하려면:

* 스키마를 구성하기 전에 데이터 테이블을 프로필, 조회 및 이벤트 카테고리로 정렬하는 하향식 접근 방식을 사용하십시오.
* 다양한 목적을 위해 스키마를 디자인할 때는 여러 가지 접근 방식과 옵션이 있습니다.
* 데이터 모델은 세그먼테이션 또는 고객 여정 분석과 같은 비즈니스 사용 사례를 지원해야 합니다.
* 스키마를 가능한 한 단순하게 만들고 반드시 필요한 경우에만 새 필드를 추가합니다.

준비가 되면 [UI에서 스키마 만들기](../tutorials/create-schema-ui.md)에 대한 자습서를 참조하여 스키마를 만들고, 엔터티에 적절한 클래스를 할당하고, 데이터를 매핑할 필드를 추가하는 방법에 대한 단계별 지침을 확인하십시오.
