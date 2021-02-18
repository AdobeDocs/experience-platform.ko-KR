---
title: Adobe Experience Platform 웹 SDK용 단일 페이지 애플리케이션 구현
description: Adobe Target을 사용하여 Adobe Experience Platform Web SDK의 단일 페이지 애플리케이션(SPA) 구현을 만드는 방법을 알아봅니다.
keywords: target;adobe target;xdm 보기;보기;단일 페이지 응용 프로그램;SPA;SPA 라이프사이클;클라이언트측;AB 테스트;경험 타깃팅;XT;VEC
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 12%

---


# 단일 페이지 애플리케이션 구현

Adobe Experience Platform 웹 SDK는 단일 페이지 애플리케이션(SPA)과 같은 차세대 클라이언트측 기술을 통해 개인화를 구현할 수 있는 풍부한 기능을 제공합니다.

기존의 웹 사이트는, 웹 사이트 디자인이 URL과 밀접하게 연결되어 있고 한 웹 페이지에서 다른 웹 페이지로 전환하려면 페이지를 로드해야 하는 다중 페이지 애플리케이션으로도 알려진 &quot;페이지-투-페이지&quot; 탐색 모델에서 작동했습니다.

단일 페이지 애플리케이션과 같은 최신 웹 애플리케이션에서는 페이지 재로드와 관계없이 브라우저 UI 렌더링을 신속하게 사용할 수 있도록 하는 모델을 채택했습니다. 이러한 경험은 스크롤링, 클릭 및 커서 이동과 같은 고객 인터랙션에 의해 트리거될 수 있습니다. 최신 웹의 패러다임이 진화함에 따라 페이지 로드와 같은 일반적인 기존 이벤트의 연관성은 더 이상 개인화와 실험을 배포할 수 없습니다.

![](assets/spa-vs-traditional-lifecycle.png)

## SPA용 Platform Web SDK의 이점

단일 페이지 애플리케이션에 Adobe Experience Platform 웹 SDK를 사용할 때 다음과 같은 이점이 있습니다.

* 페이지 로드 시 모든 오퍼를 캐시하여 여러 서버 호출을 하나의 서버 호출로 줄일 수 있습니다.
* 오퍼가 기존 서버 호출에서 발생하는 지연 시간 없이 캐시를 통해 즉시 표시되므로 사이트의 사용자 경험을 크게 향상시킬 수 있습니다.
* 단일 코드 행과 1회 개발자 설정을 통해 마케터는 SPA에서 VEC(Visual Experience Composer)를 통해 A/B 및 XT(Experience Targeting) 활동을 만들고 실행할 수 있습니다.

## XDM 보기 및 단일 페이지 애플리케이션

SPA용 Adobe Target VEC는 뷰라는 개념을 활용합니다.SPA 경험을 구성하는 시각적 요소의 논리적 그룹입니다. 따라서 단일 페이지 애플리케이션은 사용자 상호 작용에 따라 URL 대신 보기를 통해 전환하는 것으로 간주할 수 있습니다. &quot;보기&quot;는 일반적으로 전체 사이트를 나타내거나 사이트 내의 그룹화된 시각적 요소를 나타낼 수 있습니다.

뷰가 무엇인지 자세히 설명하기 위해 다음 예에서는 Response에서 구현된 가상 온라인 전자 상거래 사이트를 사용하여 예제 뷰를 탐색합니다.

홈사이트로 이동한 후, 영웅 이미지는 사이트에서 사용할 수 있는 최신 제품뿐만 아니라 부활절 판매를 촉진합니다. 이 경우 전체 홈 화면에 대해 보기를 정의할 수 있습니다. 이 보기를 &quot;홈&quot;이라고 할 수 있습니다.

![](assets/example-views.png)

고객이 비즈니스를 판매하는 제품에 더 관심을 갖게 되면 **제품** 링크를 클릭하기로 합니다. 홈 사이트와 유사하게, 제품 사이트 전체를 보기로 정의할 수 있습니다. 이 보기의 이름을 &quot;products-all&quot;로 지정할 수 있습니다.

![](assets/example-products-all.png)

뷰는 사이트의 전체 사이트 또는 시각적 요소 그룹으로 정의할 수 있으므로 제품 사이트에 표시된 4개의 제품을 그룹화하여 뷰로 간주할 수 있습니다. 이 보기의 이름이 &quot;제품&quot;일 수 있습니다.

![](assets/example-products.png)

고객이 **자세히 불러오기** 단추를 클릭하여 사이트에서 더 많은 제품을 검색하기로 결정하면 이 경우에는 웹 사이트 URL이 변경되지 않지만, 여기에 보기를 만들어 표시되는 두 번째 제품 행만 나타낼 수 있습니다. 보기 이름은 &quot;products-page-2&quot;일 수 있습니다.

![](assets/example-load-more.png)

고객은 사이트에서 몇 개의 제품을 구입하기로 결정하고 체크아웃 화면으로 이동합니다. 체크아웃 사이트에서 고객에게 일반적인 배달 또는 빠른 배달을 선택할 수 있는 옵션이 제공됩니다. 보기는 사이트의 모든 시각적 요소 그룹일 수 있으므로, 배달 기본 설정에 대해 보기를 만들고 &quot;배달 기본 설정&quot;이라고 할 수 있습니다.

![](assets/example-check-out.png)

보기 개념은 이보다 훨씬 더 확장될 수 있습니다. 사이트에서 정의할 수 있는 보기의 몇 가지 예입니다.

## XDM 보기 구현

Adobe Target에서 XDM 뷰를 활용하면 마케터가 Visual Experience Composer를 통해 SPA에서 A/B 및 XT 테스트를 실행할 수 있습니다. 일회성 개발자 설정을 완료하려면 다음 단계를 수행해야 합니다.

1. [Adobe Experience Platform 웹 SDK](../../fundamentals/installing-the-sdk.md) 설치
2. 단일 페이지 애플리케이션에서 개인화할 모든 XDM 뷰를 결정합니다.
3. XDM 보기를 정의한 후 AB 또는 XT VEC 활동을 전달하려면 단일 페이지 애플리케이션에서 `renderDecisions`을 `true`로 설정하고 해당 XDM 보기를 사용하여 `sendEvent()` 함수를 구현합니다. XDM 보기는 `xdm.web.webPageDetails.viewName`에서 전달되어야 합니다. 이 단계에서는 마케터가 Visual Experience Composer를 활용하여 해당 XDM에 대한 A/B 및 XT 테스트를 시작할 수 있습니다.

   ```javascript
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
>첫 번째 `sendEvent()` 호출에서 최종 사용자에게 렌더링해야 하는 모든 XDM 보기가 가져와 캐시됩니다. 전달된 XDM 보기 이후 `sendEvent()` 호출은 캐시에서 읽히고 서버 호출 없이 렌더링됩니다.

## `sendEvent()` 함수 예제

이 섹션에서는 가설 전자 상거래 SPA에 대해 반응에서 `sendEvent()` 함수를 호출하는 방법을 보여 주는 3가지 예제를 설명합니다.

### 예 1:A/B 테스트 홈 페이지

마케팅 팀은 전체 홈 페이지에서 A/B 테스트를 실행하려고 합니다.

![](assets/use-case-1.png)

전체 홈 사이트에서 A/B 테스트를 실행하려면 XDM `viewName`이 `home`로 설정된 상태로 `sendEvent()`을(를) 호출해야 합니다.

```jsx
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

### 예 2:맞춤형 제품

마케팅 팀은 사용자가 **추가 로드**&#x200B;를 클릭한 후 가격 레이블 색상을 빨간색으로 변경하여 두 번째 제품 행을 맞춤화하려고 합니다.

![](assets/use-case-2.png)

```jsx
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

### 예 3:A/B 테스트 배달 환경 설정

마케팅 팀은 **빠른 배달**&#x200B;이 선택되면 단추의 색상을 파란색에서 빨간색으로 변경할 수 있는지 확인하기 위해 A/B 테스트를 실행하려고 합니다(두 배달 옵션 모두에 대해 단추 색상을 파란색으로 유지하는 대신).

![](assets/use-case-3.png)

선택한 배달 기본 설정에 따라 사이트에서 컨텐츠를 개인화하기 위해 각 배달 기본 설정에 대해 보기를 만들 수 있습니다. **일반 배달**&#x200B;을 선택하면 보기 이름을 &quot;checkout-normal&quot;로 지정할 수 있습니다. **빠른 배달**&#x200B;을 선택한 경우 보기의 이름을 &quot;checkout-express&quot;로 지정할 수 있습니다.

```jsx
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

XDM 뷰 정의를 완료하고 전달된 XDM 뷰 수와 함께 `sendEvent()`을(를) 구현하면 VEC는 이러한 보기를 탐지할 수 있으며 사용자가 A/B 또는 XT 활동에 대한 작업 및 수정을 만들 수 있습니다.

>[!NOTE]
>
>SPA에 대해 VEC를 사용하려면 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 또는 [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC 도우미 확장을 설치하고 활성화해야 합니다.

### 수정 패널

[수정] 패널은 특정 보기에 대해 만들어진 액션을 캡처합니다. 뷰에 대한 모든 작업은 해당 보기 아래에 그룹화됩니다.

![](assets/modifications-panel.png)

### 작업

작업을 클릭하면 이 작업이 적용될 사이트의 요소가 강조 표시됩니다. 보기 아래에 만들어진 각 VEC 작업에는 다음 아이콘이 있습니다.**정보**, **편집**, **복제**, **이동** 및 **삭제**. 이러한 아이콘은 다음 표에 자세히 설명되어 있습니다.

![](assets/action-icons.png)

| 아이콘 | 설명 |
|---|---|
| 정보 | 작업의 세부 사항을 표시합니다. |
| 편집 | 작업의 속성을 직접 편집할 수 있습니다. |
| 복제 | 작업을 수정 패널에 있는 하나 이상의 보기에 복제하거나 VEC에서 탐색하고 이동한 하나 이상의 보기에 복제합니다. 이 작업은 반드시 수정 패널에 있지 않아도 됩니다.<br/><br/>**참고: 복제 작업이** 이루어진 후 찾아보기를 통해 VEC의 보기로 이동하여 복제된 작업이 유효한 작업인지 확인해야 합니다. 작업을 보기에 적용할 수 없으면 오류가 표시됩니다. |
| 이동 | 작업을 페이지 로드 이벤트나 수정 패널에 이미 있는 다른 보기로 이동합니다.<br/><br/>**페이지 로드 이벤트:** 페이지 로드 이벤트에 해당하는 모든 작업은 웹 애플리케이션의 초기 페이지 로드에 적용됩니다. <br/><br/>**참고:** 이동 작업이 수행된 후 찾아보기를 통해 VEC의 보기로 이동하여 이동이 유효한 작업인지 확인해야 합니다. 작업을 보기에 적용할 수 없으면 오류가 표시됩니다. |
| 삭제 | 작업을 삭제합니다. |

## SPA 예제에 VEC 사용

이 섹션에서는 Visual Experience Composer를 사용하여 A/B 또는 XT 활동에 대한 작업 및 수정 작업을 만드는 3가지 예제를 간략히 설명합니다.

### 예 1:&quot;홈&quot; 보기 업데이트

이 문서의 앞부분에서 &quot;home&quot;이라는 보기가 전체 홈 사이트에 대해 정의되었습니다. 이제 마케팅 팀은 다음과 같은 방법으로 &quot;홈&quot; 보기를 업데이트하려고 합니다.

* **장바구니에 추가** 및 **좋아요** 단추를 더 밝은 파란색 공유로 변경합니다. 이것은 헤더의 구성 요소를 변경하는 것과 관련되므로 페이지를 로드하는 동안 발생합니다.
* **2019용 최신 제품** 레이블을 **2019용 가장 많은 제품**&#x200B;으로 변경하고 텍스트 색상을 자주색으로 변경합니다.

VEC에서 이러한 업데이트를 만들려면 **구성**&#x200B;을 선택하고 이러한 변경 내용을 &quot;홈&quot; 보기에 적용하십시오.

![](assets/vec-home.png)

### 예 2:제품 레이블 변경

&quot;products-page-2&quot; 보기의 경우 마케팅 팀은 **Price** 레이블을 **Sale Price**&#x200B;로 변경하고 레이블 색상을 빨간색으로 변경합니다.

VEC에서 이러한 업데이트를 수행하려면 다음 단계가 필요합니다.

1. VEC에서 **찾아보기**&#x200B;를 선택합니다.
2. 사이트의 위쪽 탐색에서 **제품**&#x200B;을 선택합니다.
3. 제품의 두 번째 행을 보려면 **더 보기**&#x200B;를 한 번 선택합니다.
4. VEC에서 **구성**&#x200B;을 선택합니다.
5. 텍스트 레이블을 **판매 가격**&#x200B;으로 변경하고 색상을 빨간색으로 변경하는 작업을 적용합니다.

![](assets/vec-products-page-2.png)

### 예 3:개인화된 전달 환경 설정 스타일 지정

상태 또는 라디오 단추의 옵션과 같이 세부 수준으로 보기를 정의할 수 있습니다. 이 문서의 이전 보기는 &quot;checkout-normal&quot; 및 &quot;checkout-express&quot; 배달 기본 설정에 대해 정의되었습니다. 마케팅 팀은 &quot;체크아웃-익스프레스&quot; 보기에 대해 단추 색상을 빨간색으로 변경하려고 합니다.

VEC에서 이러한 업데이트를 수행하려면 다음 단계가 필요합니다.

1. VEC에서 **찾아보기**&#x200B;를 선택합니다.
2. 사이트의 장바구니에 제품을 추가합니다.
3. 사이트의 오른쪽 상단 모서리에서 장바구니 아이콘을 선택합니다.
4. **주문 체크아웃**&#x200B;을 선택합니다.
5. **배달 기본 설정** 아래의 **배달** 라디오 단추를 선택합니다.
6. VEC에서 **구성**&#x200B;을 선택합니다.
7. **Pay** 단추 색상을 빨간색으로 변경합니다.

>[!NOTE]
>
>&quot;checkout-express&quot; 보기는 **빠른 배달** 라디오 단추를 선택할 때까지 [수정] 패널에 표시되지 않습니다. 이것은 **Express Delivery** 라디오 단추를 선택하면 `sendEvent()` 함수가 실행되기 때문에 라디오 단추를 선택할 때까지 VEC가 &quot;checkout-express&quot; 보기를 인식하지 않기 때문입니다.

![](assets/vec-delivery-preference.png)
