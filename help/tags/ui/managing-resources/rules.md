---
title: 규칙
description: Adobe Experience Platform에서 태그 확장이 작동하는 방식을 알아봅니다.
exl-id: 2beca2c9-72b7-4ea0-a166-50a3b8edb9cd
source-git-commit: 77190e4acf7aad448bbfdebd8ada4dbe9a55f8e0
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 48%

---

# 규칙

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

Adobe Experience Platform의 태그는 규칙 기반 시스템을 따릅니다. 사용자 상호 작용 및 관련 데이터를 찾습니다. 규칙에 요약된 기준이 충족되면, 규칙이 정의한 확장, 스크립트 또는 클라이언트측 코드를 트리거합니다.

서로 다른 제품을 하나의 솔루션으로 통합하는 마케팅 및 광고 기술에 대한 데이터와 기능을 통합하는 규칙을 빌드합니다.

## 규칙 구조

**이벤트(If):** 이벤트는 규칙이 찾아야 할 사항입니다. 이벤트, 해당 조건 및 예외를 선택하여 정의됩니다.

**작업(Then):** 트리거는 규칙 이벤트가 발생하고 모든 조건이 충족되면 발생합니다. 태그 규칙은 서로 다른 작업을 원하는 만큼 트리거할 수 있으며 이러한 작업이 발생하는 순서를 제어할 수 있습니다. 예를 들어, 전자 상거래 감사 페이지에 대한 단일 규칙은 분석 도구 및 타사 태그를 단일 규칙에서 트리거할 수 있습니다. 각 확장이나 태그에 대해 별도의 규칙을 만들 필요가 없습니다.

이벤트 유형을 더 추가할 수 있습니다. 여러 이벤트가 OR로 결합되므로, 이벤트가 충족되면 규칙의 조건이 평가됩니다.

>[!IMPORTANT]
>
>변경 사항은 [게시](../publishing/overview.md)될 때까지 적용되지 않습니다.

### 이벤트 및 조건(if)

조건이 있는 이벤트는 규칙의 *if* 부분입니다.

지정된 이벤트가 발생하면 조건이 평가되고 필요한 경우 지정된 작업이 수행됩니다.

* **이벤트**: 규칙을 트리거하기 위해 발생해야 하는 이벤트를 하나 이상 지정합니다. 여러 이벤트는 OR에 의해 연결됩니다. 지정된 이벤트가 규칙을 트리거합니다.

* **조건**: 이벤트가 규칙 트리거를 위해 true여야 하는 조건을 구성하여 이벤트 범위를 좁힙니다. 예외는 NOT 조건으로 정의됩니다. 여러 조건은 AND로 연결됩니다.

사용할 수 있는 이벤트는 설치된 확장에 따라 다릅니다. 코어 확장의 이벤트에 대한 자세한 내용은 [코어 확장 이벤트 유형](../../extensions/client/core/overview.md#core-extension-event-types)을 참조하십시오.

### 작업(then)

작업은 규칙의 *Then* 부분입니다. 규칙이 실행될 때 발생할 작업을 정의합니다. 이벤트가 트리거되면 조건이 true로 평가되고 예외가 false로 평가될 경우 작업이 수행됩니다. 작업을 끌어 놓아 원하는 대로 순서를 지정할 수 있습니다.

## 규칙 만들기

조건이 충족되면 발생하는 작업을 지정하여 규칙을 만듭니다.

>[!TIP]
>
>오른쪽 패널에서 ![정보](../../images/ui/event-forwarding/overview/about.png)을(를) 선택하여 이 기능에 대해 자세히 알아볼 수 있는 추가 리소스를 볼 수 있습니다.

1. [!UICONTROL 규칙] 탭을 연 다음 **[!UICONTROL 새 규칙 만들기]**&#x200B;를 선택합니다.

   ![이름 필드를 강조 표시하는 규칙 탭](../../images/launch-rule-builder.png)

1. 규칙 이름을 지정합니다.
1. 이벤트 **[!UICONTROL 추가]** 아이콘을 선택합니다.
1. 확장과 해당 확장에 사용할 수 있는 이벤트 유형 중 하나를 선택한 다음 이벤트 설정을 구성합니다.

   ![규칙 이벤트 구성 페이지.](../../images/rule-event-config.png)

   사용 가능한 이벤트 유형은 선택한 확장에 따라 다릅니다. 이벤트 설정은 이벤트 유형에 따라 다릅니다. 일부 이벤트에는 구성해야 하는 속성이 없습니다.

   >[!IMPORTANT]
   >
   >클라이언트측 규칙에서 데이터 요소는 데이터 요소 이름의 시작 및 끝에 `%`으로 토큰화됩니다. 예, `%viewportHeight%`. 이벤트 전달 규칙에서 데이터 요소는 데이터 요소 이름의 시작 부분에 `{{`, 끝 부분에 `}}`(으)로 토큰화됩니다. 예: `{{viewportHeight}}`.

   Edge 네트워크의 데이터를 참조하려면 데이터 요소 경로가 `arc.event._<element>_`여야 합니다.

   `arc`는 Adobe 응답 컨텍스트를 나타냅니다.

   예: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >이 경로가 잘못 지정되면 데이터가 수집되지 않습니다.

1. 순서 매개 변수를 설정한 다음 **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다.

   모든 규칙 구성 요소의 기본 순서는 50입니다. 하나가 더 빨리 실행되도록 하려면 50보다 작은 숫자를 지정합니다.

   * 숫자 순서대로 실행됩니다. 1은 3 앞에 옵니다. 3은 10 앞에 옵니다. 10은 100 앞에 옵니다.
   * 순서가 같은 규칙은 특정 순서로 실행되지 않습니다.
   * 규칙은 순서대로 실행되지만, 반드시 같은 순서로 끝나지 않습니다. 규칙 A와 규칙 B가 이벤트를 공유하고 규칙 A가 우선하도록 순서를 지정하는 경우, 규칙 A가 비동기식으로 어떤 작업을 수행하면 규칙 B가 시작되기 전에 규칙 A가 완료되지 않을 수 있습니다.

     이 규칙을 나중에 실행하려면 50보다 큰 숫자를 지정합니다. 순서 지정에 대한 자세한 내용은 [규칙 순서 지정](rules.md#rule-ordering)을 참조하십시오.

1. 조건 **[!UICONTROL 추가]** 아이콘을 선택한 다음 논리 유형, 확장, 조건 유형을 선택하고 조건에 대한 설정을 구성합니다. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다.

   ![규칙 조건 구성 페이지입니다.](../../images/condition-settings.png)

   사용 가능한 조건 유형은 선택한 확장에 따라 다릅니다. 조건 설정은 조건 유형에 따라 다릅니다.

   논리 유형:

   * 일반 논리 유형을 사용하면 조건이 충족될 경우 작업을 실행할 수 있습니다.
   * 예외 논리 유형은 조건이 충족될 경우 작업을 실행하지 않습니다.

   (고급) 시간 초과: 이 옵션은 속성에 규칙 구성 요소 순서가 활성화되어 있을 때 사용할 수 있습니다. 이 속성은 조건을 실행하는 데 허용된 최대 시간을 정의합니다. 시간 초과에 도달하면 조건이 실패하고 나머지 규칙 조건 및 작업이 처리 큐에서 제거됩니다. 기본값은 2000ms입니다.

   원하는 만큼 조건을 추가할 수 있습니다. 동일한 규칙 내의 여러 조건은 AND로 결합됩니다.

1. 작업 **[!UICONTROL 추가]** 아이콘을 선택한 다음, 확장 및 해당 확장에 사용할 수 있는 작업 유형 중 하나를 선택하고, 작업에 대한 설정을 구성한 다음 **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다.

   ![규칙 작업 구성 페이지입니다.](../../images/action-settings.png)

   사용 가능한 작업 유형은 선택한 확장에 따라 다릅니다. 작업 설정은 작업 유형에 따라 다릅니다.

   (고급) 다음 작업 실행 대기: 이 옵션은 속성에 규칙 구성 요소 순서가 활성화되어 있을 때 사용할 수 있습니다. 이 옵션을 선택하면 이 작업이 완료될 때까지 태그가 다음 작업을 호출하지 않습니다. 이 옵션을 선택하지 않으면 다음 작업이 즉시 실행되기 시작합니다. 기본값은 **[!UICONTROL 확인]**&#x200B;입니다.

   (고급) 시간 초과: 이 옵션은 속성에 규칙 구성 요소 시퀀싱이 활성화되어 있을 때 사용할 수 있습니다. 작업을 완료하는 데 허용되는 최대 시간을 정의합니다. 시간 제한에 도달하면 작업이 실패하고 이 규칙에 대한 모든 후속 작업이 처리 큐에서 제거됩니다. 기본값은 2000ms입니다.


1. 규칙을 검토한 다음 규칙&#x200B;**저장을 선택합니다**.

   나중에 [게시](../publishing/overview.md)하는 경우 이 규칙을 라이브러리에 추가하고 배포합니다.

규칙을 만들거나 편집할 때 [활성 라이브러리](../publishing/libraries.md#active-library)에 저장하고 빌드할 수 있습니다. 이렇게 하면 변경 사항이 라이브러리에 바로 저장되고 빌드가 실행됩니다. 빌드의 상태가 표시됩니다.

## 규칙 순서 지정 {#rule-ordering}

규칙 순서 지정을 사용하면 이벤트를 공유하는 규칙의 실행 순서를 제어할 수 있습니다. 각 규칙에는 순서 우선 순위를 결정하는 정수가 포함되어 있습니다(기본값은 50). 순서에 대해 더 낮은 값이 포함된 규칙이 더 높은 값을 가진 규칙보다 먼저 실행됩니다.

모두 이벤트를 공유하고 모두 기본 우선 순위를 갖는 5개의 규칙 세트를 고려하십시오.

* 마지막으로 실행하려는 규칙이 있는 경우 해당 규칙 구성 요소를 편집하고 50보다 큰 숫자(예: 60)를 지정할 수 있습니다.
* 먼저 실행하려는 규칙이 있는 경우 해당 규칙 구성 요소를 편집하고 50보다 작은 숫자(예: 40)를 지정할 수 있습니다.

>[!NOTE]
>
>궁극적으로, 작업을 순서대로 실행하는 책임은 사용 중인 이벤트 유형의 확장 개발자에게 있습니다. Adobe 확장 개발자는 확장이 의도한 대로 작동하도록 합니다. Adobe은 타사 확장 개발자에게 이를 제대로 수행하기 위한 지침을 제공하지만, 이러한 지침이 어떻게 준수되는지 보장할 수 없습니다.

1과 100 사이의 양수로 규칙 순서를 지정하는 것이 좋습니다(기본값은 50). 규칙 순서는 수동으로 유지해야 하므로 순서 지정 체계를 가능한 한 간단하게 유지하는 것이 좋습니다. 이 제한이 너무 제한적인 경계 사례가 있는 경우 태그는 +/- 2,147,483,648 사이의 규칙 순서 번호를 지원합니다.

### 클라이언트측 규칙 처리

규칙의 로드 순서는 규칙 작업이 JavaScript, HTML 또는 기타 클라이언트측 코드로 구성되어 있는지 여부와 규칙이 페이지 하단 또는 최상위 이벤트 또는 다른 유형의 이벤트를 사용하는지 여부에 따라 달라집니다.

규칙에 대해 구성된 이벤트에 관계없이 사용자 지정 스크립트 내에서 `document.write`를 사용할 수 있습니다.

서로 다른 사용자 지정 코드 유형에 순서를 지정할 수 있습니다. 예를 들어 JavaScript 사용자 지정 코드 작업, HTML 사용자 지정 코드 작업, JavaScript 사용자 지정 코드 작업이 순서대로 있을 수 있습니다. 태그는 이러한 태그가 해당 순서로 실행되는지 확인합니다.

## 규칙 번들링

규칙 이벤트와 조건은 항상 기본 태그 라이브러리에 번들로 제공됩니다. 작업은 기본 라이브러리에 번들로 제공되거나 필요에 따라 하위 리소스로 늦게 로드될 수 있습니다. 작업이 번들로 제공되는지 여부는 규칙 이벤트 유형에 의해 결정됩니다.

### 코어 - 라이브러리 로드됨 또는 코어 - 페이지 상단 이벤트가 있는 규칙

이러한 이벤트는 거의 항상(조건이 false로 평가되지 않는 경우) 실행해야 하므로 효율성을 위해 내장 코드에서 참조하는 파일인 기본 라이브러리에 번들로 제공됩니다.

* **Javascript:** JavaScript가 기본 태그 라이브러리에 포함됩니다. 사용자 지정 스크립트는 스크립트 태그에 래핑되고 `document.write`를 사용하여 문서에 작성됩니다. 규칙에 사용자 지정 스크립트가 여러 개 있는 경우 순서대로 작성됩니다.

* **HTML:** HTML이 기본 태그 라이브러리에 포함되어 있습니다. `document.write`는 문서에 HTML을 작성하는 데 사용됩니다. 규칙에 사용자 지정 스크립트가 여러 개 있는 경우 순서대로 작성됩니다.

### 다른 이벤트가 있는 규칙

Adobe은 다른 규칙이 실제로 트리거되고 해당 작업 코드가 필요하다는 것을 보장할 수 없습니다. 따라서 위에 나열되지 않은 모든 이벤트 유형에 대한 작업은 기본 라이브러리에 패키지되지 않습니다. 대신 하위 리소스로 저장되고, 필요에 따라 주 라이브러리에서 참조합니다.

* **JavaScript:** JavaScript는 서버에서 일반 텍스트로 로드되고, 스크립트 태그에 래핑되고, Postscribe를 사용하여 문서에 추가됩니다. 규칙에 Javascript 사용자 지정 스크립트가 여러 개 있는 경우 서버에서 동시에 로드되지만 규칙에 구성된 순서와 동일한 순서로 실행됩니다.
* **HTML:** HTML은 서버에서 로드되고 Postscribe를 사용하여 문서에 추가됩니다. 규칙에 사용자 지정 HTML 스크립트가 여러 개 있는 경우 서버에서 동시에 로드되지만 규칙에 구성된 순서와 동일한 순서로 실행됩니다.

## 규칙 구성 요소 순서 {#sequencing}

런타임 환경의 동작은 속성에 대해 **[!UICONTROL 시퀀스에서 규칙 구성 요소 실행]**&#x200B;이 설정되었는지 여부에 따라 다릅니다. 이 설정은 규칙 구성 요소를 병렬로(비동기적으로) 평가할 수 있는지 또는 시퀀스 단위로 평가해야 하는지 여부를 결정합니다.

>[!IMPORTANT]
>
>이 설정은 각 규칙 내에서 조건 및 작업이 평가되는 방법만 결정하며 규칙 자체가 속성에서 실행되는 시퀀스에는 영향을 주지 않습니다. 여러 규칙의 실행 순서를 결정하는 방법에 대한 자세한 내용은 규칙 순서[&#128279;](#rule-ordering)에 대한 이전 섹션을 참조하십시오.
>
>이벤트 전달[&#128279;](../event-forwarding/overview.md) 속성에서 규칙 작업은 항상 순차적으로 실행되며 이 설정은 사용할 수 없습니다. 규칙을 만들 때 순서가 올바른지 확인하십시오.

### 활성화됨

런타임에 이벤트가 트리거될 때 이 설정이 활성화되면 규칙의 조건 및 작업이 처리 큐에 추가되고(정의한 순서에 따라) &quot;선입 선출&quot;(FIFO) 방식으로 한 번에 하나씩 처리됩니다. 규칙은 구성 요소가 완료될 때까지 기다렸다가 다음 구성 요소로 이동합니다.

조건이 false로 평가되거나 정의된 시간 초과에 도달하면 해당 규칙의 후속 조건 및 작업이 큐에서 제거됩니다.

작업이 실패하거나 정의된 시간 초과에 도달하면 해당 규칙의 후속 작업이 큐에서 제거됩니다.

### 비활성화됨

비활성화되면 런타임 시 이벤트가 트리거될 때 규칙의 조건이 즉시 평가됩니다. 여러 조건이 동시에 평가됩니다.

모든 조건이 true를 반환하고 예외가 false를 반환하는 경우 규칙의 작업이 즉시 실행됩니다. 작업이 순서대로 호출되지만 태그는 작업이 완료될 때까지 기다리지 않고 다음 작업을 호출합니다. 작업이 동기 상태이면 순서대로 실행됩니다. 하나 이상의 작업이 비동기 상태인 경우 일부 작업이 동시에 실행됩니다.
