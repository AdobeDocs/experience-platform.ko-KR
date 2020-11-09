---
title: 'Adobe Target 및 Adobe Experience Platform 웹 SDK. '
seo-title: Adobe Experience Platform 웹 SDK 및 Adobe Target 사용
description: Adobe Target을 사용하여 Experience Platform 웹 SDK로 개인화된 컨텐츠를 렌더링하는 방법 학습
seo-description: Adobe Target을 사용하여 Experience Platform 웹 SDK로 개인화된 컨텐츠를 렌더링하는 방법 학습
keywords: target;adobe target;xdm views; views;single page applications;SPA;SPA lifecycle;client-side;AB testing;AB;Experience targeting;XT;VEC
translation-type: tm+mt
source-git-commit: 8aeeef09602386f219fd8284b332469c04e88ffb
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 14%

---


# 단일 페이지 애플리케이션 구현

Adobe Experience Platform 웹 SDK는 단일 페이지 애플리케이션(SPA)과 같은 차세대 클라이언트측 기술을 통해 개인화를 구현할 수 있는 풍부한 기능을 제공합니다.

기존의 웹 사이트는, 웹 사이트 디자인이 URL과 밀접하게 연결되어 있고 한 웹 페이지에서 다른 웹 페이지로 전환하려면 페이지를 로드해야 하는 다중 페이지 애플리케이션으로도 알려진 &quot;페이지-투-페이지&quot; 탐색 모델에서 작동했습니다.

단일 페이지 애플리케이션과 같은 최신 웹 애플리케이션에서는 페이지 재로드와 관계없이 브라우저 UI 렌더링을 신속하게 사용할 수 있도록 하는 모델을 채택했습니다. 이러한 경험은 스크롤, 클릭 및 커서 이동과 같은 고객 상호 작용에 의해 트리거될 수 있습니다. 최신 웹의 패러다임이 진화함에 따라, 페이지 로드와 같은 일반적인 기존 이벤트의 연관성은 더 이상 개인화와 실험을 배포할 수 없습니다.

![](assets/spa-vs-traditional-lifecycle.png)

## SPA용 Platform Web SDK의 이점

다음은 단일 페이지 애플리케이션에 Adobe Experience Platform 웹 SDK를 사용할 때의 몇 가지 이점입니다.

* 페이지 로드 시 모든 오퍼를 캐시하여 여러 서버 호출을 하나의 서버 호출로 줄일 수 있습니다.
* 기존 서버 호출에서 발생하는 지연 시간 없이 오퍼가 캐시를 통해 즉시 표시되므로 사이트의 사용자 경험을 크게 향상시킬 수 있습니다.
* 마케터는 한 줄의 코드와 한 번의 개발자 설정을 통해 SPA에서 VEC(Visual Experience Composer)를 통해 A/B 및 XT(Experience Targeting) 활동을 만들고 실행할 수 있습니다.

## XDM 보기 및 단일 페이지 애플리케이션

SPA용 Adobe Target VEC는 &quot;보기&quot;라는 새로운 개념(예: SPA 경험을 함께 구성하는 시각적 요소의 논리 그룹)을 활용합니다. 따라서 단일 페이지 애플리케이션이 사용자 상호 작용을 기반으로 URL 대신 보기를 통해 전환하는 것으로 간주할 수 있습니다. &quot;보기&quot;는 일반적으로 전체 사이트를 나타내거나 사이트 내의 그룹화된 시각적 요소를 나타낼 수 있습니다.

뷰가 무엇인지 자세히 설명하기 위해 다음 예에서는 Responsive로 구현된 가상 온라인 전자 상거래 사이트를 사용하여 예제 뷰를 탐색합니다.

홈사이트로 간 후, 한 영웅 이미지는 부활절 세일과 사이트에서 이용 가능한 최신 상품을 홍보한다. 이 경우 전체 홈 화면에 대해 보기를 정의할 수 있습니다. 이 보기를 &quot;홈&quot;이라고 할 수 있습니다.

![](assets/example-views.png)

As the customer becomes more interested in the products that the business is selling, they decide to click the **Products** link. 홈 사이트와 유사하게, 제품 사이트 전체를 보기로 정의할 수 있습니다. 이 보기의 이름을 &quot;products-all&quot;로 지정할 수 있습니다.

![](assets/example-products-all.png)

뷰는 사이트의 전체 사이트 또는 시각적 요소 그룹으로 정의될 수 있으므로 제품 사이트에 표시된 4개의 제품을 그룹화하여 보기로 간주할 수 있습니다. 이 보기의 이름이 &quot;제품&quot;일 수 있습니다.

![](assets/example-products.png)

고객이 사이트에서 더 많은 제품을 탐색하기 위해 **추가** 로드 단추를 클릭하기로 결정할 때, 이 경우에는 웹 사이트 URL이 변경되지 않지만, 표시되는 제품의 두 번째 행만 표시하기 위해 여기에서 보기를 만들 수 있습니다. 보기 이름은 &quot;products-page-2&quot;일 수 있습니다.

![](assets/example-load-more.png)

고객은 사이트에서 몇 개의 제품을 구입하기로 결정하고 체크아웃 화면으로 진행합니다. 체크아웃 사이트에서는 일반 배달이나 빠른 배달을 선택할 수 있는 옵션이 고객에게 제공됩니다. 보기는 사이트의 모든 시각적 요소 그룹일 수 있으므로, 배달 환경 설정에 대해 보기를 만들고 &quot;배달 환경 설정&quot;이라고 할 수 있습니다.

![](assets/example-check-out.png)

관점의 개념은 이것보다 훨씬 더 확장될 수 있다. 사이트에서 정의할 수 있는 보기의 몇 가지 예일 뿐입니다.

## XDM 보기 구현

Adobe Target에서 XDM 뷰를 활용하면 마케터가 Visual Experience Composer를 통해 SPA에서 A/B 및 XT 테스트를 실행할 수 있습니다. 1회 개발자 설정을 완료하려면 다음 단계를 수행해야 합니다.

1. [Adobe Experience Platform 웹 SDK 설치](../../fundamentals/installing-the-sdk.md)
2. 단일 페이지 애플리케이션에서 개인화할 모든 XDM 뷰를 결정합니다.
3. XDM 보기를 정의한 후 AB 또는 XT VEC 활동을 전달하려면 단일 페이지 애플리케이션에서 로 설정된 `sendEvent()` `renderDecisions` `true` 기능과 해당 XDM 뷰를 구현하십시오. XDM 뷰를 전달해야 합니다 `xdm.web.webPageDetails.viewName`. 이 단계에서는 마케터가 Visual Experience Composer를 활용하여 해당 XDM에 대한 A/B 및 XT 테스트를 실행할 수 있습니다.

   ```javascript
   alloy("sendEvent",  { 
     "renderDecisions": true, 
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
>첫 번째 `sendEvent()` 호출에서는 최종 사용자에게 렌더링해야 하는 모든 XDM 보기가 가져와 캐시됩니다. 전달된 XDM 보기 이후 `sendEvent()` 호출은 캐시에서 읽히고 서버 호출 없이 렌더링됩니다.

## `sendEvent()` 함수 예제

이 섹션에서는 가상 e커머스 SPA에 대해 반응에서 `sendEvent()` 함수를 호출하는 방법을 보여주는 세 가지 예제를 설명합니다.

### 예 1:A/B 테스트 홈 페이지

마케팅 팀은 전체 홈 페이지에서 A/B 테스트를 실행하려고 합니다.

![](assets/use-case-1.png)

전체 홈 사이트에서 A/B 테스트를 실행하려면, XDM을 다음 `sendEvent()` 으로 설정하고 호출해야 `viewName` 합니다. `home`

```javascript
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent",  { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
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

### 예 2:맞춤형 제품

마케팅 팀은 사용자가 추가 로드를 클릭한 후 가격 레이블 색상을 빨간색으로 변경하여 두 번째 제품 행을 개인화할 **수 있습니다**.

![](assets/use-case-2.png)

```javascript
function onViewChange(viewName) { 

  alloy("sendEvent",  { 
    "renderDecisions": true, 
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
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component’s state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### 예 3:A/B 테스트 전달 환경 설정

The marketing team want to run an A/B test to see whether changing the color of the button from blue to red when **Express Delivery** is selected can boost conversions (as opposed to keeping the button color blue for both delivery options).

![](assets/use-case-3.png)

선택한 배달 환경 설정에 따라 사이트에서 컨텐츠를 개인화하기 위해 각 배달 환경 설정에 대해 보기를 만들 수 있습니다. 일반 **배달을** 선택하면 보기 이름을 &quot;체크아웃-정상&quot;으로 지정할 수 있습니다. If **Express Delivery** is selected, the View can be named &quot;checkout-express&quot;.

```javascript
function onViewChange(viewName) { 

  alloy("sendEvent",  { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName   
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## SPA용 Visual Experience Composer 사용

XDM 뷰 정의를 완료하고 전달된 XDM 뷰`sendEvent()` 로 구현하면 VEC는 이러한 뷰를 감지할 수 있으며 사용자가 A/B 또는 XT 활동에 대한 작업과 수정 사항을 생성할 수 있습니다.

>[!NOTE]
>
>SPA용 VEC를 사용하려면 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 또는 [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension을 설치하고 활성화해야 합니다.

### 수정 패널

수정 패널은 특정 보기에 대해 만들어진 동작을 캡처합니다. 뷰에 대한 모든 작업은 해당 보기 아래에 그룹화됩니다.

![](assets/modifications-panel.png)

### 작업

작업을 클릭하면 이 작업이 적용될 사이트의 요소가 강조 표시됩니다. Each VEC action created under a View has the following icons: **Information**, **Edit**, **Clone**, **Move**, and **Delete**. 이러한 아이콘은 다음 표에 자세히 설명되어 있습니다.

![](assets/action-icons.png)

| 아이콘 | 설명 |
|---|---|
| 정보 | 작업의 세부 사항을 표시합니다. |
| 편집 | 작업의 속성을 직접 편집할 수 있습니다. |
| 복제 | 작업을 수정 패널에 있는 하나 이상의 보기에 복제하거나 VEC에서 탐색하고 이동한 하나 이상의 보기에 복제합니다. 이 작업은 반드시 수정 패널에 있지 않아도 됩니다.<br/><br/>**참고:** 복제 작업이 수행된 후 찾아보기를 통해 VEC의 보기로 이동하여 복제된 작업이 유효한 작업인지 확인해야 합니다. 작업을 보기에 적용할 수 없으면 오류가 표시됩니다. |
| 이동 | 작업을 페이지 로드 이벤트나 수정 패널에 이미 있는 다른 보기로 이동합니다.<br/><br/>**페이지 로드 이벤트:** 페이지 로드 이벤트에 해당하는 모든 작업은 웹 애플리케이션의 초기 페이지 로드에 적용됩니다. <br/><br/>**참고:**&#x200B;이동 작업이 수행된 후 찾아보기를 통해 VEC의 보기로 이동하여 이동이 유효한 작업인지 확인해야 합니다. 작업을 보기에 적용할 수 없으면 오류가 표시됩니다. |
| 삭제 | 작업을 삭제합니다. |

## SPA 예제에 VEC 사용

이 섹션에서는 Visual Experience Composer를 사용하여 A/B 또는 XT 활동에 대한 작업 및 수정 사항을 만들기 위한 세 가지 예제를 설명합니다.

### 예 1:&quot;홈&quot; 보기 업데이트

이 문서의 앞부분에서 &quot;홈&quot;이라는 보기가 전체 홈 사이트에 대해 정의되었습니다. 이제 마케팅 팀은 다음과 같은 방법으로 &quot;홈&quot; 보기를 업데이트하려고 합니다.

* 장바구니에 **추가** 및 **좋아요** 단추를 더 밝은 파란색으로 변경합니다. 이것은 헤더의 구성 요소를 변경하므로 페이지 로드 중에 발생합니다.
* Change the **Latest Products for 2019** label to **Hottest Products for 2019** and change the text color to purple.

To make these updates in the VEC, select **Compose** and apply those changes to the &quot;home&quot; view.

![](assets/vec-home.png)

### 예 2:제품 레이블 변경

&quot;products-page-2&quot; 보기의 경우 마케팅 팀은 **가격** 레이블을 **판매 가격으로** 변경하고 레이블 색상을 빨간색으로 변경하려고 합니다.

VEC에서 이러한 업데이트를 수행하려면 다음 단계가 필요합니다.

1. VEC **에서** 찾아보기를 선택합니다.
2. 사이트 **상단** 탐색에서 제품을 선택합니다.
3. Select **Load More** once to view the second row of products.
4. VEC **에서** 구성을 선택합니다.
5. Apply actions to change the text label to **Sale Price** and the color to red.

![](assets/vec-products-page-2.png)

### 예 3:개인화된 전달 환경 설정

보는 상태 또는 라디오 단추의 옵션과 같은 세부 수준으로 정의할 수 있습니다. 이 문서의 이전 보기는 배달 기본 설정, &quot;체크아웃-보통&quot; 및 &quot;체크아웃-익스프레스&quot;에 대해 정의되었습니다. 마케팅 팀은 &quot;체크아웃-익스프레스&quot; 보기에 대해 단추 색상을 빨간색으로 변경하려고 합니다.

VEC에서 이러한 업데이트를 수행하려면 다음 단계가 필요합니다.

1. VEC **에서** 찾아보기를 선택합니다.
2. 사이트의 장바구니에 제품을 추가합니다.
3. 사이트의 오른쪽 상단 모서리에서 장바구니 아이콘을 선택합니다.
4. 주문 **체크아웃을 선택합니다**.
5. 배달 기본 설정 **에서** 빠른 배달 **라디오 단추를 선택합니다**.
6. VEC **에서** 구성을 선택합니다.
7. [ **지불** ] 단추 색상을 빨간색으로 변경합니다.

>[!NOTE]
>
>&quot;체크아웃 익스프레스&quot; 보기는 **빠른 배달** 라디오 단추를 선택할 때까지 수정 패널에 표시되지 않습니다. 이것은`sendEvent()` 빠른 배달 **** 라디오 단추를 선택하면 함수가 실행되므로 라디오 단추를 선택할 때까지 VEC는 &quot;체크아웃 익스프레스&quot; 보기를 인식하지 않기 때문입니다.

![](assets/vec-delivery-preference.png)