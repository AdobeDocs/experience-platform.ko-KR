---
keywords: Experience Platform;home;popular topics;schema;Schema;enum;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;primary identity;primary idenity;XDM individual profile;XDM fields;enum datatype;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;schema design
solution: Experience Platform
title: 스키마 컴포지션의 기본 사항
topic: overview
description: 이 문서에서는 XDM(Experience Data Model) 스키마 및 Adobe Experience Platform에서 사용할 스키마를 작성하기 위한 기본 블록, 원칙 및 모범 사례에 대해 소개합니다.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '2839'
ht-degree: 0%

---


# 스키마 컴포지션의 기본 사항

이 문서에서는 [!DNL Experience Data Model] (XDM) 스키마 및 Adobe Experience Platform에서 사용할 스키마를 구성하는 기본 블록, 원칙 및 모범 사례에 대해 소개합니다. XDM과 XDM의 사용 방법에 대한 일반적인 정보 [!DNL Platform]는 [XDM 시스템 개요를 참조하십시오](../home.md).

## 스키마 이해

스키마는 데이터의 구조와 형식을 나타내고 유효성을 검사하는 규칙 세트입니다. 높은 수준의 스키마는 실제 개체(예: 사람)에 대한 추상적인 정의를 제공하고, 해당 개체의 각 인스턴스(예: 이름, 성, 생일 등)에 어떤 데이터가 포함되어야 하는지 개요를 제공합니다.

스키마는 데이터 구조를 설명하는 것 외에도, 제한과 기대를 데이터에 적용하므로 시스템 간에 이동할 때 데이터의 유효성을 검사할 수 있습니다. 이러한 표준 정의를 사용하면 출처에 관계없이 데이터를 일관되게 해석할 수 있고 애플리케이션 간에 번역이 필요하지 않습니다.

[!DNL Experience Platform] 스키마 사용을 통해 이 의미 체계 정규화를 유지합니다. 스키마는 데이터 [!DNL Experience Platform]를 설명하는 표준 방식이므로, 스키마를 따르는 모든 데이터를 조직 간의 충돌 없이 다시 사용할 수 있으며 여러 조직 간에 공유할 수도 있습니다.

### 관계형 테이블과 포함된 객체

관계형 데이터베이스를 사용하는 경우 최상의 방법은 데이터를 표준화하거나 엔티티를 개별 조각으로 나누어 여러 테이블에 표시합니다. 데이터를 전체적으로 읽거나 엔티티를 업데이트하려면 JOIN을 사용하여 여러 개별 테이블에서 읽기 및 쓰기 작업을 수행해야 합니다.

포함된 개체를 사용하여 XDM 스키마는 복잡한 데이터를 직접 표시하고 계층적 구조의 독립된 문서에 저장할 수 있습니다. 이 구조에 대한 주요 이점 중 하나는 많은 비용이 드는 결합 표에 연결하여 엔티티를 재구성하지 않고도 데이터를 쿼리할 수 있다는 것입니다.

### 스키마 및 빅데이터

최신 디지털 시스템은 트랜잭션 데이터, 웹 로그, 사물의 인터넷, 디스플레이 등 다양한 행동 신호를 생성합니다. 이러한 빅데이터는 탁월한 경험을 최적화할 수 있는 기회를 제공하지만 데이터의 규모와 다양성으로 인해 사용하기가 어렵습니다. 데이터의 가치를 높이려면 데이터의 구조, 형식 및 정의를 표준화해야 일관되고 효율적으로 처리할 수 있습니다.

스키마는 여러 소스에서 데이터를 통합하고, 공통 구조 및 정의를 통해 표준화하며, 솔루션 간에 공유함으로써 이 문제를 해결합니다. 이를 통해 후속 프로세스 및 서비스는 데이터에 대해 질문되는 모든 유형의 질문에 응답하여 데이터 모델링에 대한 기존의 접근 방식에서 벗어나 데이터를 미리 파악하고 이러한 기대에 부합하도록 데이터를 모델링할 수 있습니다.

### 스키마 기반의 [!DNL Experience Platform]

표준화는 이면의 핵심 개념이다 [!DNL Experience Platform]. Adobe을 기반으로 하는 XDM은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 표준 스키마를 정의하는 것입니다.

The infrastructure which [!DNL Experience Platform] is built, knowing [!DNL XDM System], professiones the schema-based workflows and includes the [!DNL Schema Registry], schema [!DNL Schema Editor]metadata and service containing patterns. See the [XDM System overview](../home.md) for more information.

## 스키마 계획

스키마를 구축하는 첫 번째 단계는 스키마 내에서 캡처하려는 개념 또는 실제 개체를 결정하는 것입니다. 설명하려는 개념을 식별하면 데이터 유형, 잠재적 ID 필드 및 차후에 스키마가 어떻게 발전할 것인지 등을 고려하여 스키마를 계획할 수 있습니다.

### 데이터 비헤이비어는 [!DNL Experience Platform]

에서 사용하기 위한 데이터 [!DNL Experience Platform] 는

* **데이터**&#x200B;기록:제목 속성에 대한 정보를 제공합니다. 대상은 조직 또는 개인일 수 있습니다.
* **시계열 데이터**:작업을 직접 또는 간접적으로 레코드 제목에 의해 수행한 시점에 시스템의 스냅샷을 제공합니다.

모든 XDM 스키마는 레코드 또는 시간 시리즈로 분류할 수 있는 데이터를 설명합니다. 스키마의 데이터 동작은 스키마의 **클래스에**&#x200B;의해 정의됩니다. 이 클래스는 스키마를 처음 만들 때 스키마에 할당됩니다. XDM 클래스는 이 문서의 후반부에 자세히 설명되어 있습니다.

레코드 및 시간 시리즈 스키마 모두 ID 맵을 포함합니다(`xdm:identityMap`). 이 필드에는 다음 섹션에 설명된 대로 &quot;ID&quot;로 표시된 필드에서 추출되는 대상의 ID 표현이 포함되어 있습니다.

### [!UICONTROL ID]

스키마는 데이터를 인제스트하는 데 사용됩니다 [!DNL Experience Platform]. 이 데이터를 여러 서비스에서 사용하여 개별 엔티티의 단일 통합 뷰를 만들 수 있습니다. 따라서 고객 ID에 대해 생각해 볼 스키마와 데이터가 어디에서 오는지에 관계없이 주체를 식별하는 데 사용할 수 있는 필드를 고려할 때 중요합니다.

이 프로세스를 돕기 위해 스키마 내의 키 필드를 ID로 표시할 수 있습니다. 데이터 수집 시 해당 필드의 데이터는 해당 개인에 대한 &quot;[!UICONTROL ID 그래프]&quot;에 삽입됩니다. 그런 다음 그래프 데이터에 [[!DNL 실시간 고객 프로필]](../../profile/home.md) 및 기타 [!DNL Experience Platform] 서비스에서 액세스하여 각 개별 고객에 대한 연결된 보기를 제공할 수 있습니다.

일반적으로 &quot;ID&quot;로 표시된 필드는[!UICONTROL 다음과]같습니다.이메일 주소, 전화 번호, [[!DNL Experience Cloud ID(ECID)]](https://docs.adobe.com/content/help/ko-KR/id-service/using/home.html), CRM ID 또는 기타 고유한 ID 필드 또한 &quot;[!UICONTROL Identity]&quot; 필드도 양호할 수 있으므로 조직 고유의 식별자를 고려해야 합니다.

가장 강력한 프로파일을 구축하기 위해 데이터를 취합하는 것을 돕기 위해 스키마 계획 단계 동안 고객 ID를 고려하는 것이 중요합니다. ID 정보를 통해 고객에게 디지털 경험을 전달하는 방법에 대한 자세한 내용은 [Adobe Experience Platform ID 서비스](../../identity-service/home.md) 개요를 참조하십시오.

#### xdm:identityMap {#identityMap}

`xdm:identityMap` 은 연결된 네임스페이스와 함께 개인에 대한 다양한 ID 값을 설명하는 맵 유형 필드입니다. 이 필드는 스키마 자체의 구조 내에서 ID 값을 정의하는 대신 스키마에 대한 ID 정보를 제공하는 데 사용할 수 있습니다.

간단한 ID 맵의 예는 다음과 같습니다.

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

위의 예에서 보듯이 개체의 각 키는 ID 네임스페이스를 `identityMap` 나타냅니다. 각 키의 값은 각 네임스페이스에 대한 ID 값(`id`)을 나타내는 개체 배열입니다. Adobe 응용 프로그램에서 인식하는 표준 ID 네임스페이스의 [!DNL Identity Service] 목록은 설명서를 [](../../identity-service/troubleshooting-guide.md#standard-namespaces) 참조하십시오.

>[!NOTE]
>
>값이 기본 ID(ID)인지 여부에 대한 부울 값`primary`을 각 ID 값에 제공할 수도 있습니다. 기본 ID는 에서 사용할 스키마에 대해서만 설정해야 합니다 [!DNL Real-time Customer Profile]. 자세한 내용은 [조합 스키마](#union) 섹션을 참조하십시오.

### 스키마 진화 원리 {#evolution}

디지털 경험의 특성이 계속 진화하므로 이를 나타내는 데 사용되는 스키마가 있어야 합니다. 따라서 스키마의 이전 버전에 대한 파괴적인 변경 없이 잘 디자인된 스키마를 필요에 따라 변경 및 진화할 수 있습니다.

이전 버전과의 호환성을 유지하는 것은 스키마 진화에 필수이므로, 순전히 추가 버전 관리 원칙을 [!DNL Experience Platform] 적용하여 스키마의 모든 개정은 원본을 훼손하지 않는 업데이트 및 변경 사항만 발생하도록 합니다. 즉, 변경 내용 **은 지원되지 않습니다.**

| 지원되는 변경 사항 | 변경 내용 분리(지원되지 않음) |
|------------------------------------|---------------------------------|
| <ul><li>기존 스키마에 새 필드 추가</li><li>필수 필드 선택 사항 만들기</li></ul> | <ul><li>이전에 정의한 필드 제거</li><li>새로운 필수 필드 소개</li><li>기존 필드 이름 변경 또는 재정의</li><li>이전에 지원되는 필드 값 제거 또는 제한</li><li>트리의 다른 위치로 속성 이동</li></ul> |

>[!NOTE]
>
>스키마를 사용하여 데이터를 인제스트하지 않은 경우 해당 스키마 [!DNL Experience Platform]에 변경 사항을 적용할 수 있습니다. 하지만 스키마를 사용한 후에는 버전 관리 정책을 [!DNL Platform]사용해야 합니다.

### 스키마 및 데이터 수집

데이터를 인제스트하려면 먼저 데이터 세트 [!DNL Experience Platform]를 만들어야 합니다. 데이터 세트는 [[!DNL Catalog Service]에 대한 데이터 변환 및 추적을 위한 기본](../../catalog/home.md)블록이며, 일반적으로 인제스트된 데이터를 포함하는 테이블 또는 파일을 나타냅니다. 모든 데이터 집합은 기존 XDM 스키마를 기반으로 하며, 이는 인제스트된 데이터가 포함되어야 하는 내용과 데이터 구성 방식에 대한 제약 조건을 제공합니다. 자세한 내용은 [Adobe Experience Platform 데이터 수집](../../ingestion/home.md) 개요를 참조하십시오.

## 스키마 구성 블록

[!DNL Experience Platform] 에서는 표준 구성 블록을 결합하여 스키마를 만드는 컴포지션 방법을 사용합니다. 이 방법은 기존 구성 요소의 재사용을 촉진하고 업계 전반의 표준화를 촉진하여 공급업체 스키마 및 구성 요소를 지원합니다 [!DNL Platform].

스키마는 다음 공식을 사용하여 구성됩니다.

**클래스 + Mixin&amp;ast;= XDM 스키마**

&amp;ast;스키마는 클래스와 _0 이상의_ 혼합으로 구성됩니다. 즉, 혼합을 사용하지 않고 데이터 집합 스키마를 구성할 수 있습니다.

### 클래스

스키마 구성은 클래스를 할당하는 것으로 시작됩니다. 클래스는 스키마에 포함할 데이터의 동작 측면(레코드 또는 시간 시리즈)을 정의합니다. 이 외에도 클래스는 해당 클래스를 기반으로 하는 모든 스키마에는 호환이 가능한 여러 데이터 세트를 병합할 수 있는 방법이 포함되어 있어야 하는 가장 작은 수의 공통 속성을 설명합니다.

또한 클래스는 스키마에서 사용할 수 있는 믹스를 결정합니다. 이 내용은 다음에 나오는 [믹신](#mixin) 섹션에서 더 자세히 설명합니다.

&quot;산업&quot; 클래스라고 하는 모든 통합 [!DNL Experience Platform]과 함께 제공되는 표준 클래스가 있습니다. 업계 클래스는 다양한 사용 사례에 적용되는 일반적으로 승인된 업계 표준입니다. 업계 클래스의 예로는 Adobe에서 제공하는 [!DNL XDM Individual Profile] 및 [!DNL XDM ExperienceEvent] 클래스가 있습니다.

[!DNL Experience Platform] 또한 &quot;공급업체&quot; 클래스를 사용할 수 있습니다. 이 클래스는 [!DNL Experience Platform] 파트너가 정의하며 해당 공급업체 서비스 또는 애플리케이션을 사용하는 모든 고객이 사용할 수 [!DNL Platform]있습니다.

또한 &quot;고객&quot; 클래스라고 하는 각 조직의 특정 사용 사례를 설명하는 데 사용되는 [!DNL Platform]클래스도 있습니다. 고객 클래스는 고유한 사용 사례를 설명하는 데 사용할 수 있는 업계 또는 공급업체 클래스가 없을 때 조직에 의해 정의됩니다.

예를 들어 충성도 프로그램의 구성원을 나타내는 스키마는 개인에 대한 레코드 데이터를 설명하므로 Adobe에 의해 정의된 표준 산업 클래스인 [!DNL XDM Individual Profile] 클래스를 기반으로 할 수 있습니다.

### 믹신 {#mixin}

혼합은 개인 세부 사항, 호텔 선호도 또는 주소와 같은 특정 기능을 구현하는 하나 이상의 필드를 정의하는 재사용 가능한 구성 요소입니다. 혼합은 호환 클래스를 구현하는 스키마의 일부로 포함되도록 되어 있습니다.

믹스는 데이터(레코드 또는 시간 시리즈)의 동작을 기반으로 호환하는 클래스를 정의합니다. 즉, 모든 클래스에 모든 믹스인을 사용할 수 없습니다.

혼합은 클래스와 동일한 범위와 정의를 가집니다.개별 조직에서 사용하는 업계 믹싱, 벤더 믹싱 및 고객 혼합이 있습니다 [!DNL Platform]. [!DNL Experience Platform] 다양한 표준 업계 믹스가 포함되어 있으며 벤더가 사용자의 믹스를 정의할 수 있고 개별 사용자가 고유한 개념으로 믹스를 정의할 수 있습니다.

예를 들어, &quot;[!UICONTROL 로열티 멤버]&quot; 스키마에 대해 &quot;[!UICONTROL 이름]&quot; 및 &quot;[!UICONTROL 홈 주소]&quot;와 같은 세부 정보를 캡처하려면 이러한 일반적인 개념을 정의하는 표준믹스를 사용할 수 있습니다. 그러나 일반적이지 않은 사용 사례(예: &quot;[!UICONTROL 로열티 프로그램 수준]&quot;)에만 적용되는 개념에는 미리 정의된 믹스가 없는 경우가 많습니다. 이 경우 이 정보를 캡처하려면 자신의 믹스를 정의해야 합니다.

스키마는 &quot;0개 이상&quot; 혼합으로 구성되므로 혼합을 전혀 사용하지 않고 유효한 스키마를 구성할 수 있습니다.

### Data type {#data-type}

데이터 유형은 기본 리터럴 필드와 같은 방식으로 클래스 또는 스키마의 참조 필드 유형으로 사용됩니다. 주요 차이점은 데이터 유형이 여러 하위 필드를 정의할 수 있다는 것입니다. 혼합과 유사하게, 데이터 유형은 다중 필드 구조를 일관되게 사용할 수 있지만, 데이터 형식을 필드의 &quot;데이터 유형&quot;으로 추가하여 스키마의 어느 곳에나 포함할 수 있으므로 혼합보다 유연성이 더 높습니다.

[!DNL Experience Platform] 는 일반적인 데이터 구조를 설명하는 표준 패턴 사용을 지원하기 [!DNL Schema Registry] 위한 목적으로 여러 가지 일반적인 데이터 유형을 제공합니다. 이 내용은 [!DNL Schema Registry] 자습서에서 자세히 설명되며, 여기에서 데이터 유형을 정의하는 단계를 진행하면 더 명확해집니다.

### 필드

필드는 스키마의 가장 기본적인 구성 블록입니다. 필드는 특정 데이터 유형을 정의하여 포함할 수 있는 데이터 유형에 대한 제약 조건을 제공합니다. 이러한 기본 데이터 유형은 단일 필드를 정의하는 반면, 이전에 언급한 [데이터 유형은](#data-type) 여러 하위 필드를 정의하고 다양한 스키마 전체에서 동일한 다중 필드 구조를 다시 사용할 수 있도록 허용합니다. 따라서 필드의 &quot;데이터 유형&quot;을 레지스트리에 정의된 데이터 형식 중 하나로 정의하는 것 외에도 다음과 같은 기본 스칼라 유형을 [!DNL Experience Platform] 지원합니다.

* 문자열
* 정수
* 숫자
* 부울
* Array
* 개체

이러한 스칼라 형식의 유효한 범위는 특정 패턴, 형식, 최소/최대 또는 사전 정의된 값으로 더 제한될 수 있습니다. 이러한 제약 조건을 사용하면 다음을 포함하여 보다 다양한 특정 필드 유형을 나타낼 수 있습니다.

* 열거형
* Long
* Short
* 바이트
* 날짜
* 날짜-시간
* 맵

>[!NOTE]
>
>&quot;map&quot; 필드 유형은 단일 키에 대한 여러 값을 포함하여 키-값 쌍 데이터를 허용합니다. 맵은 시스템 수준에서만 정의할 수 있습니다. 즉, 산업이나 공급업체 정의 스키마에서 맵을 만날 수 있지만, 사용자가 정의한 필드에 사용할 수는 없습니다. 스키마 [레지스트리 API 개발자 안내서에는](../api/getting-started.md) 필드 유형 정의에 대한 자세한 내용이 포함되어 있습니다.

다운스트림 서비스 및 애플리케이션에서 사용되는 일부 데이터 작업은 특정 필드 유형에 대해 제한을 적용합니다. 해당되는 서비스에는 다음이 포함되지만 이에 국한되지 않습니다.

* [[!DNL 실시간 고객 프로필]](../../profile/home.md)
* [[!DNL ID 서비스]](../../identity-service/home.md)
* [[!DNL 세그멘테이션]](../../segmentation/home.md)
* [[!DNL 쿼리 서비스]](../../query-service/home.md)
* [[!DNL 데이터 과학 작업 공간]](../../data-science-workspace/home.md)

다운스트림 서비스에서 사용할 스키마를 만들기 전에 해당 서비스에 대한 적절한 설명서를 검토하여 스키마가 의도한 데이터 작업에 대한 필드 요구 사항과 제한 사항을 보다 잘 파악하십시오.

### XDM 필드

XDM은 기본 필드 및 고유한 데이터 유형을 정의하는 기능 외에도 [!DNL Experience Platform] 서비스에 의해 암시적으로 이해되고 구성 요소 간에 사용될 때 보다 높은 일관성을 제공하는 표준 필드 및 데이터 유형을 제공합니다 [!DNL Platform] .

&quot;이름&quot; 및 &quot;이메일 주소&quot;와 같은 이러한 필드는 기본 스칼라 필드 형식을 벗어나는 추가된 의미를 포함하므로 동일한 XDM 데이터 형식을 공유하는 모든 필드가 동일한 방식으로 동작한다고 [!DNL Platform] 합니다. 이러한 동작은 데이터가 어디에서 오는지 또는 데이터가 사용되는 서비스에 관계없이 일관되도록 신뢰할 수 [!DNL Platform] 있습니다.

사용 가능한 XDM 필드 [의 전체 목록은 XDM 필드 사전을](field-dictionary.md) 참조하십시오. 모든 위치에서 일관성과 표준화를 지원하기 위해 가능한 경우 XDM 필드 및 데이터 유형을 사용하는 것이 좋습니다 [!DNL Experience Platform].

## 컴포지션 예

스키마는 인제스트될 데이터의 형식 및 구조를 나타내며 컴포지션 모델을 사용하여 [!DNL Platform]빌드합니다. 이전에 언급했듯이 이러한 스키마는 클래스와 호환되는 0개 이상의 혼합으로 구성됩니다.

예를 들어 소매 저장소에서 구매한 내용을 설명하는 스키마를 &quot;[!UICONTROL 스토어 트랜잭션]&quot;이라고 할 수 있습니다. 스키마는 표준 [!DNL XDM ExperienceEvent] 커머스 [!UICONTROL 및 사용자 정의 제품 정보] 혼합과 결합된 클래스를 [!UICONTROL 구현합니다] .

웹 사이트 트래픽을 추적하는 다른 스키마를 &quot;[!UICONTROL 웹 방문]&quot;이라고 할 수 있습니다. 수업도 [!DNL XDM ExperienceEvent] 구현하지만 이번에는 표준 [!UICONTROL 웹] 믹싱을 결합해 만든 것이다.

아래 다이어그램은 이러한 스키마와 각 혼합으로 만든 필드를 보여줍니다. 또한 이 안내서에 앞서 언급된 &quot; [!DNL XDM Individual Profile] 충성도 구성원&quot; 스키마를 비롯하여 클래스를 기반으로 하는 두 개의 스키마도 포함되어 있습니다.

![](../images/schema-composition/composition.png)

### 합집합 {#union}

특정 사용 사례에 대한 스키마를 구성할 수 [!DNL Experience Platform] 있지만 특정 클래스 유형에 대한 스키마의 &quot;union&quot;을 볼 수도 있습니다. 이전 다이어그램은 XDM ExperienceEvent 클래스를 기반으로 두 개의 스키마와 [!DNL XDM Individual Profile] 클래스를 기반으로 한 두 개의 스키마를 보여줍니다. 아래에 표시된 유니온은 동일한 클래스(및[!DNL XDM ExperienceEvent] 각각)를 공유하는 모든 스키마의 필드 [!DNL XDM Individual Profile]를 집계합니다.

![](../images/schema-composition/union.png)

함께 사용할 스키마를 활성화하면 해당 클래스 유형 [!DNL Real-time Customer Profile]에 대한 공용 조합에 포함됩니다. [!DNL Profile] 고객 속성에 대한 강력하고 중앙 집중식 프로필뿐만 아니라 고객이 모든 시스템과 통합한 모든 이벤트에 대해 타임스탬프가 있는 계정을 제공합니다 [!DNL Platform]. [!DNL Profile] 조합 뷰를 사용하여 이 데이터를 표시하고 각 개별 고객을 전체적으로 확인합니다.

작업 방법에 대한 자세한 내용 [!DNL Profile]은 [실시간 고객 프로필 개요를 참조하십시오](../../profile/home.md).

## 데이터 파일을 XDM 스키마에 매핑

인제스트된 모든 데이터 파일은 XDM 스키마의 구조를 준수해야 [!DNL Experience Platform] 합니다. XDM 계층(샘플 파일 포함)을 준수하기 위해 데이터 파일의 형식을 지정하는 방법에 대한 자세한 내용은 [샘플 ETL 변환에 대한 문서를 참조하십시오](../../etl/transformations.md). 데이터 파일을 인제스트하는 방법에 대한 일반적인 [!DNL Experience Platform]내용은 [일괄 처리 인제스트 개요를 참조하십시오](../../ingestion/batch-ingestion/overview.md).

## 다음 단계

스키마 컴포지션의 기본 사항을 이해하면 스키마를 사용하여 스키마 작성을 시작할 수 있습니다 [!DNL Schema Registry].

이 [!DNL Schema Registry] 는 Adobe Experience Platform [!DNL Schema Library] 내의 라이브러리에 액세스하는 데 사용되며 사용 가능한 모든 라이브러리 리소스에 액세스할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이 [!DNL Schema Library] 에는 Adobe으로 정의된 산업 리소스, 파트너가 정의한 공급업체 리소스, [!DNL Experience Platform] 조직의 구성원이 구성한 클래스, 믹싱, 데이터 유형 및 스키마가 포함되어 있습니다.

UI를 사용하여 스키마 작성을 시작하려면, [스키마 편집기 자습서와](../tutorials/create-schema-ui.md) 함께 이 문서 전체에서 언급된 &quot;충성도 멤버&quot; 스키마를 빌드하십시오.

API를 [!DNL Schema Registry] 사용하려면 먼저 스키마 레지스트리 API 개발자 [안내서를 읽어 봅니다](../api/getting-started.md). 개발자 안내서를 읽은 후 스키마 레지스트리 API를 사용하여 스키마 [만들기에 대한 자습서에 설명된 단계를 따릅니다](../tutorials/create-schema-api.md).