---
title: 데이터 수집 종단간 개요
description: Adobe Experience Platform의 데이터 수집 기능을 사용하여 Adobe Experience Cloud 솔루션으로 이벤트 데이터를 전송하는 방법에 대한 높은 수준의 개요입니다.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 0%

---

# 데이터 수집 종단간 개요

Adobe Experience Platform은 데이터를 수집하여 다른 Adobe 제품 및 타사 대상으로 전송합니다. 애플리케이션에서 Experience Platform Edge Network로 이벤트 데이터를 전송하려면 이러한 핵심 기술을 이해하고 필요할 때 필요한 대상에 데이터를 제공하도록 구성하는 방법을 알고 있어야 합니다.

이 안내서에서는 플랫폼의 데이터 수집 기능을 사용하여 Edge 네트워크를 통해 이벤트를 전송하는 방법에 대한 높은 수준의 자습서를 제공합니다. 특히 이 자습서에서는 데이터 수집 UI(이전 Adobe Experience Platform Launch) 내에서 Adobe Experience Platform Web SDK 태그 확장을 설치하고 구성하는 단계를 안내합니다.

>[!NOTE]
>
>태그를 사용하지 않으려는 경우 수동으로 SDK를 설치 및 구성하도록 선택할 수도 있지만, 아래 요약된 대로 주변 단계를 계속 완료해야 합니다.
>
>데이터 수집 UI와 관련된 모든 단계는 Experience Platform UI에서도 수행할 수 있습니다.

## 전제 조건

이 자습서에서는 데이터 수집 UI를 사용하여 스키마를 만들고, 데이터 스트림을 구성하고, 웹 SDK를 설치합니다. UI에서 이러한 작업을 수행하려면 다음과 함께 하나 이상의 웹 속성에 대한 액세스 권한이 부여되어야 합니다 [속성 권한](../tags/ui/administration/user-permissions.md#property-rights):

* 개발
* 확장 관리

다음 안내서를 참조하십시오. [데이터 수집을 위한 권한 관리](./permissions.md) 속성 및 속성 권한에 대한 액세스 권한을 부여하는 방법을 알아봅니다.

이 안내서에서 언급된 다양한 데이터 수집 제품을 사용하려면 데이터 세트에 대한 액세스 권한과 스키마를 만들고 관리하는 기능도 있어야 합니다. 이러한 기능 중 하나에 액세스할 수 있어야 하는 경우에는 CSM에 문의하여 필요한 액세스 권한을 받으십시오. Adobe Experience Platform을 구매하지 않은 경우 Adobe은 추가 비용 없이 SDK를 사용하기 위해 필요한 액세스 권한을 제공합니다.

이미 Platform에 액세스할 수 있는 경우에는 모든 권한이 있는지 확인해야 합니다 [권한](../access-control/home.md#permissions) 다음 카테고리에서 사용할 수 있습니다.

* 데이터 모델링
* ID

자세한 내용은 [액세스 제어 UI 개요](../access-control/ui/overview.md) 플랫폼 기능에 대한 권한을 사용자에게 부여하는 방법을 알아봅니다.

## 프로세스 요약

웹 사이트에 대한 데이터 수집을 구성하는 프로세스는 다음과 같이 요약할 수 있습니다.

1. [스키마 만들기](#schema) Edge Network로 전송될 때 데이터를 구성하는 방법을 결정합니다.
1. [데이터 스트림 만들기](#datastream) 데이터를 전송할 대상을 구성하기 위해
1. [웹 SDK 설치 및 구성](#sdk) 웹 사이트에서 특정 이벤트가 발생할 때 데이터 스트림으로 데이터를 전송하는 중입니다.

Edge Network에 데이터를 보낼 수 있게 되면 선택적으로 다음 작업을 수행할 수도 있습니다 [이벤트 전달 구성](#event-forwarding) 조직에 라이센스가 있는 경우

## 스키마 만들기 {#schema}

[XDM(경험 데이터 모델)](../xdm/home.md) 는 스키마 형식의 데이터에 대한 공통 구조 및 정의를 제공하는 오픈 소스 사양입니다. 다시 말해, XDM은 Edge Network 및 기타 Adobe Experience Cloud 애플리케이션에서 실행 가능한 방식으로 데이터를 구조화하고 서식을 지정하는 방법입니다.

데이터 수집 작업을 설정하는 첫 번째 단계는 데이터를 나타내는 XDM 스키마를 만드는 것입니다. 이 자습서의 뒷부분에서 전송할 데이터를 이 스키마의 구조에 매핑합니다.

>[!NOTE]
>
>XDM 스키마는 사용자 지정할 수 있습니다. 아래 요약된 단계는 과도하게 처방되지 않고 웹 SDK에 대한 스키마 요구 사항에 특히 중점을 둡니다. 이러한 매개 변수를 제외하면 원하는 대로 나머지 구조를 정의할 수 있습니다.

UI에서 **[!UICONTROL 스키마]** 을 클릭합니다. 여기에서 조직에 속한 이전에 만든 스키마 목록을 볼 수 있습니다. 계속하려면 **[!UICONTROL 스키마 만들기]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL XDM ExperienceEvent]** 드롭다운 메뉴에서 을 클릭합니다.

![스키마 작업 공간](./images/e2e/schemas.png)

스키마에 필드 그룹 추가를 시작하라는 대화 상자가 나타납니다. 웹 SDK를 사용하여 이벤트를 전송하려면 필드 그룹을 추가해야 합니다 **[!UICONTROL AEP 웹 SDK ExperienceEvent Mixin]**. 이 필드 그룹에는 웹 SDK 라이브러리에서 자동으로 수집하는 데이터 속성에 대한 정의가 포함되어 있습니다.

검색 창을 사용하여 목록 범위를 좁혀 이 필드 그룹을 더 쉽게 찾을 수 있습니다. 찾으면 선택하기 전에 목록에서 선택합니다 **[!UICONTROL 필드 그룹 추가]**.

![스키마 작업 공간](./images/e2e/add-field-group.png)

스키마 캔버스가 나타나고 웹 SDK 필드 그룹에서 제공하는 필드를 포함하여 XDM 스키마의 트리 구조를 보여 줍니다.

![스키마 구조](./images/e2e/schema-structure.png)

트리에서 루트 필드를 선택하여 엽니다 **[!UICONTROL 스키마 속성]** 오른쪽 레일에서 스키마에 대한 이름 및 선택적 설명을 제공할 수 있습니다.

![스키마 이름을 지정합니다](./images/e2e/name-schema.png)

스키마에 필드를 더 추가하려면 **[!UICONTROL 추가]** 아래에 **[!UICONTROL 필드 그룹]** 왼쪽 레일의 섹션에 있습니다.

![필드 그룹 추가](./images/e2e/add-field-groups.png)

>[!NOTE]
>
>다음 안내서를 참조하십시오. [필드 그룹 추가](../xdm/ui/resources/schemas.md#add-field-groups) xdm 설명서에서 사용 사례에 맞는 다른 필드 그룹을 검색하는 방법에 대한 자세한 단계를 설명합니다.
>
>가장 좋은 방법은 Edge 네트워크를 통해 전송할 데이터의 필드만 추가하는 것입니다. 스키마에 필드를 추가하고 저장하면 이후 스키마에 추가 변경만 수행할 수 있습니다. 의 섹션을 참조하십시오. [스키마 진화 규칙](../xdm/schema/composition.md#evolution) 추가 정보.

필요한 필드를 추가한 후에는 을(를) 선택합니다 **[!UICONTROL 저장]** 스키마를 저장하려면 을 클릭합니다.

![스키마 저장](./images/e2e/save-schema.png)

## 데이터 스트림 만들기 {#datastream}

데이터 스트림은 데이터를 전송할 에지 네트워크에 연결하는 구성입니다. 특히, 데이터 스트림은 데이터를 전송할 Experience Cloud 제품 및 각 제품에서 데이터를 처리하고 저장하는 방법을 지정합니다.

>[!NOTE]
>
>사용하려면 [이벤트 전달](../tags/ui/event-forwarding/overview.md) (조직에 기능에 대한 라이센스가 있는 것으로 가정) Adobe 제품을 활성화할 때와 동일한 방법으로 데이터 스트림에 대해 활성화해야 합니다. 이 프로세스에 대한 자세한 내용은 [이후 섹션](#event-forwarding).

선택 **[!UICONTROL 데이터 스트림]** 을 클릭합니다. 여기에서 편집할 목록에서 기존 데이터 스트림을 선택하거나, 을(를) 선택하여 새 구성을 만들 수 있습니다 **[!UICONTROL 새 데이터 스트림]**.

![데이터스트림](./images/e2e/datastreams.png)

데이터 스트림에 대한 구성 요구 사항은 데이터를 전송하는 제품 및 기능에 따라 다릅니다. 각 제품의 구성 옵션에 대한 자세한 내용은 [데이터 세트 개요](../edge/datastreams/overview.md).

## 웹 SDK 설치 및 구성 {#install}

스키마와 데이터 스트림을 만든 후 다음 단계는 Edge 네트워크에 데이터 전송을 시작하도록 Platform Web SDK를 설치 및 구성하는 것입니다.

>[!NOTE]
>
>이 섹션에서는 데이터 수집 UI를 사용하여 웹 SDK 태그 확장을 구성하지만 대신 원시 코드를 사용하여 설치하고 구성할 수도 있습니다. 자세한 내용은 다음 안내서를 참조하십시오.
>
>* [SDK 설치](../edge/fundamentals/installing-the-sdk.md)
>* [SDK 구성](../edge/fundamentals/configuring-the-sdk.md)
>
>또한 이벤트 전달만 사용하려는 경우에도에서 이벤트 전달을 구성하기 전에 설명된 대로 SDK를 설치 및 구성해야 합니다 [이후 단계](#event-forwarding).

프로세스는 다음과 같이 요약할 수 있습니다.

1. [태그 속성에 Adobe Experience Platform Web SDK 설치](#install-sdk) 해당 기능에 액세스할 수 있습니다.
1. [XDM 개체 데이터 요소 만들기](#data-element) 웹 사이트의 변수를 이전에 만든 XDM 스키마 구조에 매핑하려면 다음을 수행하십시오.
1. [규칙 만들기](#rule) 를 눌러 Edge Network에 데이터를 전송해야 하는 시기를 SDK에 알립니다.
1. [라이브러리 빌드 및 설치](#library) 를 클릭하여 웹 사이트에서 규칙을 구현합니다.

### 태그 속성에 SDK 설치 {#install-sdk}

선택 **[!UICONTROL 태그]** 왼쪽 탐색에서 태그 속성 목록을 표시합니다. 원하는 경우 편집할 기존 속성을 선택하거나 **[!UICONTROL 새 속성]** 을 가리키도록 업데이트하는 것이 좋습니다.

![속성](./images/e2e/properties.png)

새 속성을 만드는 경우 수사적 이름을 제공하고 [!UICONTROL 플랫폼] to **[!UICONTROL 웹]**. 웹 속성에 대한 전체 도메인을 제공한 다음 을 선택합니다 **[!UICONTROL 저장]**.

![속성 만들기](./images/e2e/create-property.png)

속성에 대한 개요 페이지가 나타납니다. 여기에서 을 선택합니다. **[!UICONTROL 확장]** 왼쪽 탐색에서 를 선택하고 **[!UICONTROL 카탈로그]**. Platform Web SDK에 대한 목록을 찾고(선택적으로 검색 막대를 사용하여 결과 범위를 좁힐 수 있음), **[!UICONTROL 설치]**.

![웹 SDK 설치](./images/e2e/install-sdk.png)

SDK에 대한 구성 페이지가 나타납니다. 대부분의 필수 값은 필요한 경우 변경할 수 있는 기본값으로 자동 채워집니다.

![웹 SDK 구성](./images/e2e/configure-sdk.png)

그러나 SDK를 설치하려면 먼저 데이터 스트림을 선택해야 데이터를 보낼 위치를 알 수 있습니다. 아래 **[!UICONTROL 데이터 스트림]**&#x200B;를 지정하는 경우 드롭다운 메뉴를 사용하여 [이전 단계](#datastream). 데이터 스트림을 설정한 후에는 **[!UICONTROL 저장]** 를 클릭하여 속성에 SDK 설치를 완료합니다.

![데이터 스트림 설정 및 저장](./images/e2e/set-datastream.png)

### XDM 데이터 요소 만들기 {#data-element}

SDK가 Edge Network에 데이터를 전송하려면 해당 데이터를 [이전 단계](#schema). 이 매핑은 데이터 요소를 사용하여 수행됩니다.

UI에서 **[!UICONTROL 데이터 요소]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 새 데이터 요소 만들기]**.

![새 데이터 요소 만들기](./images/e2e/data-elements.png)

다음 화면에서 을 선택합니다. **[!UICONTROL Adobe Experience Platform Web SDK]** 아래에 [!UICONTROL 확장] 드롭다운을 선택한 다음 **[!UICONTROL XDM 개체]** 를 반환합니다.

![XDM 개체 유형](./images/e2e/xdm-object.png)

XDM 개체 유형에 대한 구성 대화 상자가 나타납니다. 이 대화 상자는 자동으로 Platform 샌드박스를 선택하고, 여기에서 해당 샌드박스에서 생성된 모든 스키마를 볼 수 있습니다. 목록에서 이전에 만든 XDM 스키마를 선택합니다.

![XDM 개체 유형](./images/e2e/select-schema.png)

스키마 구조가 나타납니다. 별표( )가 있는 모든 필드&#x200B;**\***)은 이벤트가 실행될 때 자동으로 채워지는 필드를 나타냅니다. 다른 모든 필드의 경우 스키마의 구조를 탐색하고 나머지 데이터를 채울 수 있습니다.

![데이터를 XDM 필드에 매핑](./images/e2e/map-schema.png)

>[!NOTE]
>
>위의 스크린샷은 웹 사이트의 클라이언트 측에서 전역적으로 액세스할 수 있는 변수를 매핑하는 방법을 보여줍니다(`cartAbandonsTotal`)을 XDM 필드에서 해당 이름을 참조하여 XDM 필드에 추가합니다. [!UICONTROL 값] 퍼센트 기호로 둘러싸인 필드(`%`).
>
>이전에 만든 다른 데이터 요소를 사용하여 이러한 필드를 채울 수도 있습니다. 다음에서 참조를 참조하십시오. [데이터 요소](../tags/ui/managing-resources/data-elements.md) 를 참조하십시오.

스키마에 데이터 매핑을 완료했으면 선택하기 전에 데이터 요소의 이름을 지정하십시오 **[!UICONTROL 저장]**.

![데이터 요소 이름 지정 및 저장](./images/e2e/name-and-save.png)

### 규칙 만들기

데이터 요소를 저장한 후 다음 단계는 웹 사이트에서 특정 이벤트가 발생할 때마다(예: 고객이 장바구니에 제품을 추가할 때) Edge Network에 전송하는 규칙을 만드는 것입니다.

웹 사이트에서 발생할 수 있는 거의 모든 이벤트에 대한 규칙을 설정할 수 있습니다. 예를 들어 이 섹션에서는 고객이 양식을 제출할 때 트리거되는 규칙을 만드는 방법을 보여줍니다. 다음 HTML은 규칙의 주제가 되는 &quot;장바구니에 추가&quot; 양식이 있는 간단한 웹 페이지를 나타냅니다.

```html
<!DOCTYPE html>
<html>
<body>

  <form id="add-to-cart-form">
    <label for="item">Product:</label><br>
    <input type="text" id="item" name="item"><br>
    <label for="amount">Amount:</label><br>
    <input type="number" id="amount" name="amount" value="1"><br><br>
    <input type="submit" value="Add to Cart">
  </form> 

</body>
</html>
```

데이터 수집 UI에서 **[!UICONTROL 규칙]** 왼쪽 탐색에서 를 선택하고 **[!UICONTROL 새 규칙 만들기]**.

![규칙](./images/e2e/rules.png)

다음 화면에서 규칙 이름을 입력합니다. 여기에서 다음 단계는 규칙에 대한 이벤트를 결정하는 것입니다(즉, 규칙이 실행될 때). 선택 **[!UICONTROL 추가]** 아래에 [!UICONTROL 이벤트].

![이름 규칙](./images/e2e/name-rule.png)

이벤트 구성 페이지가 나타납니다. 이벤트를 구성하려면 먼저 이벤트 유형을 선택해야 합니다. 이벤트 유형은 확장에 의해 제공됩니다. 예를 들어 &quot;양식 제출&quot; 이벤트를 설정하려면 다음을 선택합니다 **[!UICONTROL 코어]** 확장을 선택한 다음 **[!UICONTROL 제출]** 아래의 이벤트 유형 **[!UICONTROL 양식]** 카테고리.

>[!NOTE]
>
>구성 방법 등 Adobe 웹 확장에서 제공하는 다양한 이벤트 유형에 대한 자세한 내용은 [Adobe 확장 참조](../tags/extensions/client/overview.md) 태그 설명서에 추가했습니다.

양식 제출 이벤트에서 [CSS 선택기](https://www.w3schools.com/css/css_selectors.asp) 를 눌러 실행할 규칙에 대한 특정 요소를 참조합니다. 아래 예에서는 ID입니다 `add-to-cart-form` 이 규칙은 &quot;장바구니에 추가&quot; 양식에만 실행되도록 사용됩니다. 선택 **[!UICONTROL 변경 내용 유지]** 를 눌러 규칙에 이벤트를 추가합니다.

![이벤트 구성](./images/e2e/event-config.png)

이벤트가 추가되었음을 나타내는 규칙 구성 페이지가 다시 나타납니다. &quot;[!UICONTROL If]규칙에 추가 조건을 추가하여 &quot;

그렇지 않으면, 다음 단계는 규칙이 실행될 때 수행할 작업을 추가하는 것입니다. 선택 **[!UICONTROL 추가]** 아래에 **[!UICONTROL 작업]** 계속하십시오.

![작업 추가](./images/e2e/add-action.png)

작업 구성 페이지가 나타납니다. Edge Network에 데이터를 전송하는 규칙을 가져오려면 **[!UICONTROL Adobe Experience Platform Web SDK]** 확장 및 **[!UICONTROL 이벤트 보내기]** 를 사용 중입니다.

![작업 유형](./images/e2e/action-type.png)

이벤트 보내기 작업을 구성하는 추가 옵션을 보여주는 화면이 업데이트됩니다. 아래 **[!UICONTROL 유형]**&#x200B;를 채울 사용자 지정 유형 값을 제공할 수 있습니다 `eventType` XDM 필드. 아래 **[!UICONTROL XDM 데이터]**&#x200B;이전에 만든 XDM 데이터 유형의 이름을 제공하거나( 퍼센트 기호로 둘러싸인) 데이터베이스 아이콘( )을 선택합니다![데이터베이스 아이콘](./images/e2e/database-symbol.png))을 클릭하여 목록에서 선택합니다. Edge Network에 최종적으로 전송될 데이터입니다.

선택 **[!UICONTROL 변경 내용 유지]** 완료됨.

![작업 구성](./images/e2e/action-config.png)

규칙 구성을 마치면 를 선택합니다 **[!UICONTROL 저장]** 프로세스를 마칩니다.

![규칙 저장](./images/e2e/save-rule.png)

### 라이브러리 빌드 및 설치 {#library}

규칙이 구성되면 태그 라이브러리에 추가하고 해당 라이브러리를 환경에 빌드하고 웹 사이트에 해당 빌드를 설치할 준비가 되었습니다.

>[!NOTE]
>
>아직 데이터 수집 UI에서 환경을 설정하지 않은 경우 빌드를 만들기 전에 먼저 이를 수행해야 합니다. 의 섹션을 참조하십시오. [웹 속성에 대한 환경 구성](../tags/ui/publishing/environments.md#web-configuration) 를 참조하십시오.

라이브러리를 만들고, 라이브러리에 확장 및 규칙을 추가하고, 환경에 해당 라이브러리를 빌드하는 방법에 대해 알아보려면 다음 안내서를 참조하십시오 [라이브러리 관리](../tags/ui/publishing/libraries.md) 태그 설명서에 추가했습니다. 라이브러리를 만들 때 Platform Web SDK 확장 및 이전에 만든 데이터 수집 규칙을 포함해야 합니다.

라이브러리를 만들고 빌드가 환경에 할당되면 웹 사이트의 클라이언트 측에 해당 환경을 설치할 수 있습니다. 의 섹션을 참조하십시오. [환경 설치](../tags/ui/publishing/environments.md#installation) 추가 정보.

웹 사이트에 환경을 설치한 후에는 다음을 수행할 수 있습니다 [구현 테스트](../tags/ui/publishing/embed-code-testing.md) Adobe Experience Platform Debugger 사용.

## 이벤트 전달 구성(선택 사항) {#event-forwarding}

>[!NOTE]
>
>이벤트 전달은 이벤트 라이선스가 부여된 조직에서만 사용할 수 있습니다.

Edge Network에 데이터를 전송하도록 SDK를 구성한 후에는 이벤트 전달을 설정하여 해당 데이터를 전달할 Edge 네트워크에 연결할 수 있습니다.

이벤트 전달을 사용하려면 먼저 이벤트 전달 속성을 만들어야 합니다. 선택 **[!UICONTROL 이벤트 전달]** 왼쪽 탐색 메뉴에서 를 선택하고 **[!UICONTROL 새 속성]**. 선택하기 전에 속성의 이름을 입력합니다 **[!UICONTROL 저장]**.

이벤트 전달 속성을 만들고 나면 다음 단계는 데이터를 전송해야 하는 위치를 결정하는 규칙을 만드는 것입니다. 이벤트 전달 속성에 대한 규칙은 태그 속성과 거의 동일한 방식으로 구축되며, 단, 이벤트를 지정할 수 없습니다(이벤트 전달은 데이터 스트림에서 직접 받는 이벤트만 처리하므로). 규칙 작업의 경우, 사용 가능한 이벤트 전달 확장 중 하나를 사용하거나 사용자 지정 코드를 사용하여 이벤트를 대신 전달할 수 있습니다.

![이벤트 전달 규칙](./images/e2e/event-forwarding-rule.png)

전과 마찬가지로 규칙을 구성했으면 라이브러리에 추가하고 환경에 해당 라이브러리를 빌드해야 합니다.

빌드가 완료되면 최종 단계는 데이터 스트림을 업데이트하는 것입니다 [이전에 구성됨](#datastream) 이벤트 전달을 활성화합니다. 시작하려면 다음으로 이동합니다. **[!UICONTROL 데이터 스트림]** 및 목록에서 해당 데이터 스트림을 선택합니다. 여기에서 이벤트 전달을 위한 토글을 활성화하고 방금 구성한 속성 및 환경의 이름을 제공합니다.

![이벤트 전달 데이터 스트림](./images/e2e/event-forwarding-datastream.png)

## 다음 단계

이 안내서에서는 Platform Web SDK를 사용하여 Edge 네트워크로 데이터를 전송하는 방법에 대한 높은 수준의 종단간 개요를 제공합니다. 관련된 다양한 구성 요소 및 서비스에 대한 자세한 내용은 이 안내서 전체에서 연결된 설명서를 참조하십시오.
