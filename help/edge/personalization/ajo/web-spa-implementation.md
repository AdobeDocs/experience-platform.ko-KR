---
title: 단일 페이지 애플리케이션 구현
description: Adobe Journey Optimizer에서 SPA 보기를 구현하는 방법 알아보기
source-git-commit: c91a3ef135937ec5c5f87741699ef216df5ac85a
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# 단일 페이지 애플리케이션(SPA) 구현 {#web-spa-implementation}

Adobe Experience Platform Web SDK는 단일 페이지 애플리케이션(SPA)과 같은 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다.

기존 웹 사이트는 웹 사이트 디자인이 URL과 밀접하게 연결되어 있고 한 웹 페이지에서 다른 웹 페이지로 전환하려면 페이지를 로드해야 하는 다중 페이지 애플리케이션으로도 알려진 &quot;페이지-투-페이지&quot; 탐색 모델에서 작동합니다.

단일 페이지 애플리케이션(SPA)과 같은 최신 웹 애플리케이션에서는 대신 종종 페이지 다시 로드와 무관한 브라우저 UI 렌더링을 촉진하는 모델을 채택했습니다. 이러한 경험은 스크롤, 클릭 및 커서 움직임과 같은 고객 상호 작용에 의해 트리거될 수 있습니다. 최신 웹의 패러다임이 발전함에 따라 개인화 및 실험을 배포하기 위한 페이지 로드와 같은 기존 일반 이벤트와의 관련성이 더 이상 작동하지 않습니다.

![페이지 라이프사이클 다이어그램입니다.](assets/web-spa-vs-traditional-lifecycle.png)

## SPA용 Web SDK 사용의 이점 {#web-spa-benefits}

단일 페이지 애플리케이션에 Web SDK를 사용하면 다음과 같은 몇 가지 이점이 있습니다.

* 페이지 로드 시 모든 오퍼를 캐시하여 여러 서버 호출을 하나의 서버 호출로 줄일 수 있습니다.
* 오퍼가 기존 서버 호출로 인해 초래되는 지연 없이 캐시를 통해 즉시 표시되므로 사이트의 사용자 경험을 크게 향상시킬 수 있습니다.
* 일회용 개발자 설정을 사용하면 마케터가 SPA에서 Adobe Journey Optimizer Web Visual Editor를 통해 개인화 및 실험 활동을 만들고 실행할 수 있습니다.

## XDM 보기 및 단일 페이지 애플리케이션 {#web-spa-xdm}

Journey Optimizer 웹 편집기는 라는 개념을 이용합니다 _조회수_.

보기는 SPA 경험을 함께 구성하는 시각적 요소의 논리 그룹입니다. 따라서 단일 페이지 애플리케이션은 사용자 상호 작용을 기반으로 URL 대신 보기를 통해 전환으로 간주할 수 있습니다. 보기는 일반적으로 전체 사이트, 단일 페이지 또는 페이지 내의 그룹화된 시각적 요소를 나타낼 수 있습니다.

보기에 대해 자세히 설명하기 위해 다음 예제에서는 가상의 온라인 전자 상거래 사이트를 사용합니다.

* 홈 사이트로 이동하면 영웅 이미지는 사이트에서 사용할 수 있는 다양한 제품 카탈로그뿐만 아니라 시즌 컬렉션을 홍보합니다. 이 경우, 전체 홈 화면에 대해 뷰를 정의할 수 있습니다. 이 견해는 간단히 &quot;홈&quot;이라고 할 수 있다.

  ![홈 페이지를 보여주는 샘플 웹 사이트 이미지.](assets/web-spa-home.png)

* 고객이 비즈니스에서 판매하는 제품에 대한 관심이 높아짐에 따라 **남성** 링크를 클릭합니다. 홈 페이지와 비슷한 전체 **남성** 페이지는 보기로 정의할 수 있습니다. 이 보기의 이름은 &quot;men&quot;으로 지정할 수 있습니다.

  ![특정 보기를 표시하는 샘플 웹 사이트 이미지.](assets/web-spa-men.png)

* 보기를 전체 사이트 또는 사이트의 시각적 요소 그룹으로 정의할 수 있으므로 제품 사이트에 표시된 네 가지 제품을 그룹화하여 보기로 간주할 수 있습니다. 이 보기의 이름은 &quot;products&quot;로 지정할 수 있습니다.

  ![특정 보기를 표시하는 샘플 웹 사이트 이미지.](assets/web-spa-men-products.png)

* 고객이 를 클릭하기로 결정하면 **모든 남성용 제품** 버튼을 클릭하여 사이트에서 더 많은 제품을 탐색합니다. 이 경우 웹 사이트 URL은 변경되지 않지만, 표시되는 제품의 두 번째 행만 나타내는 보기를 여기에 만들 수 있습니다. 보기 이름은 &quot;products-page-2&quot;일 수 있습니다.

* 고객은 사이트에서 몇 가지 제품을 구매하기로 하고 체크아웃 화면으로 진행합니다. 장바구니 화면 자체를 &quot;장바구니&quot;라는 보기와 연결할 수 있습니다. 또는 아래의 권장 제품을 처리하기 위해 체크아웃 화면 내에서 다른 보기를 사용할 수 있습니다.

  ![특정 보기를 표시하는 샘플 웹 사이트 이미지.](assets/web-spa-cart.png)

보기의 개념은 이보다 훨씬 더 확장될 수 있다. 다음은 사이트에서 정의할 수 있는 보기의 몇 가지 예입니다.

## XDM 보기 구현 {#implement-xdm-views}

Adobe Journey Optimizer에서 XDM 보기를 활용하여 마케터가 Journey Optimizer 웹 시각적 편집기를 통해 SPA에서 웹 개인화 및 실험 캠페인을 실행할 수 있도록 할 수 있습니다.

이 경우 일회용 개발자 설정을 완료하려면 다음 단계를 수행해야 합니다.

1. 설치 [Adobe Experience Platform 웹 SDK](../../fundamentals/installing-the-sdk.md) 및 확인 [웹 채널 사전 요구 사항](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/configure-web-channel/web-prerequisites.html) 페이지를 가리키도록 업데이트하는 중입니다.

2. 개인화할 단일 페이지 애플리케이션에서 모든 XDM 보기를 확인합니다.

3. XDM 보기를 정의한 후 해당 보기에 컨텐츠를 전달하려면 를 구현해야 합니다 `sendEvent()` 함수 `renderDecisions` 을 로 설정 `true` 단일 페이지 애플리케이션에서 해당 XDM 보기를 사용할 수 있습니다. XDM 보기를 전달해야 합니다. `xdm.web.webPageDetails.viewName`. 이 단계를 통해 마케터는 Journey Optimizer 웹 편집기 내에서 이러한 보기를 검색하고 해당 보기에 대한 콘텐츠 수정 사항을 적용할 수 있습니다.

```
 alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
   "web": {
    "webPageDetails": {
    "viewName":"home"
   }
  }
 }
});
```

>[!NOTE]
>
>첫 번째 `sendEvent()` 를 호출하면 최종 사용자에게 렌더링해야 하는 모든 XDM 보기를 가져오고 캐시합니다. 후속 `sendEvent()` 전달된 XDM 보기가 있는 호출은 캐시에서 읽히고 서버 호출 없이 렌더링됩니다.

## `sendEvent()` 함수 예제

이 섹션에서는 를 호출하는 방법을 보여 주는 두 가지 예를 간략하게 설명합니다. `sendEvent()` 가상 전자 상거래 SPA에 대해 React에서 작동합니다.

### 예제 1: A/B 테스트 홈 페이지 {#web-spa-sample-1}

마케팅 팀은 전체 홈 페이지에서 A/B 테스트를 실행하려고 합니다.

![](assets/web-spa-home.png)

전체 홈 사이트에서 A/B 테스트를 실행하려면 `sendEvent()` 은(는) XDM을 사용하여 호출해야 합니다. `viewName` 을 로 설정 `home`:

```js
function onViewChange() {

  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash

  viewName = viewName || 'home'; // view name cannot be empty

  // Sanitize viewName to get rid of any trailing symbols derived from URL

  if (viewName.startsWith('#') || viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }

  alloy("sendEvent", {
    "renderDecisions": true,

    "xdm": {
      "web": {
        "webPageDetails": {
          "viewName":"home"
        }
      }
    }
  });
}

// react router v4

const history = syncHistoryWithStore(createBrowserHistory(), store);

history.listen(onViewChange);

// react router v3

<Router history={hashHistory} onUpdate={onViewChange} >
```

### 예제 2: 개인화된 제품 {#web-spa-sample-2}

마케팅 팀은 사용자가 클릭하여 모든 남성 제품을 표시한 후 가격 레이블 색상을 빨간색으로 변경함으로써 제품의 두 번째 행을 개인화하려고 합니다.

![](assets/web-spa-men-products.png)

```js
function onViewChange(viewName) {

    alloy("sendEvent", {
        "renderDecisions": true,
        "xdm": {
            "web": {
                "webPageDetails": {
                    "viewName": viewName
                }
            }
        }
    });
}

class Products extends Component {

    render() {
        return (

            <
            button type = "button"
            onClick = {
                this.handleLoadMoreClicked
            } > All Men 's Products</button>
        );
    }

    handleLoadMoreClicked() {
        var page = this.state.page + 1; // assuming page number is derived from component's state
        this.setState({
            page: page
        });
        onViewChange('PRODUCTS-PAGE-' + page);
    }
}
```
