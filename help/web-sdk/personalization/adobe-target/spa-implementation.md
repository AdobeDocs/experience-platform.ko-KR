---
title: Adobe Experience Platform Web SDK에 대한 단일 페이지 애플리케이션 구현
description: Adobe Target을 사용하여 Adobe Experience Platform Web SDK의 단일 페이지 애플리케이션(SPA) 구현을 만드는 방법에 대해 알아봅니다.
keywords: target;adobe target;xdm 보기;보기;단일 페이지 애플리케이션;SPA;SPA 라이프사이클;클라이언트측;AB 테스트;AB;경험 타깃팅;XT;VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 0%

---


# 단일 페이지 애플리케이션 구현

Adobe Experience Platform Web SDK는 단일 페이지 애플리케이션(SPA)과 같은 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다.

기존 웹 사이트는 웹 사이트 디자인이 URL과 밀접하게 연결되어 있고 한 웹 페이지에서 다른 웹 페이지로 전환하려면 페이지를 로드해야 하는 다중 페이지 애플리케이션으로도 알려진 &quot;페이지-투-페이지&quot; 탐색 모델에서 작동했습니다.

단일 페이지 애플리케이션과 같은 최신 웹 애플리케이션에서는 대신 종종 페이지 다시 로드와 무관한 브라우저 UI 렌더링을 촉진하는 모델을 채택했습니다. 이러한 경험은 스크롤, 클릭 및 커서 움직임과 같은 고객 상호 작용에 의해 트리거될 수 있습니다. 최신 웹의 패러다임이 발전함에 따라 개인화 및 실험을 배포하기 위한 페이지 로드와 같은 기존 일반 이벤트와의 관련성이 더 이상 작동하지 않습니다.

![기존 페이지 주기와 비교하여 SPA 주기를 보여 주는 다이어그램입니다.](assets/spa-vs-traditional-lifecycle.png)

## SPA용 Platform Web SDK의 이점

단일 페이지 애플리케이션에 Adobe Experience Platform Web SDK를 사용하면 다음과 같은 몇 가지 이점이 있습니다.

* 페이지 로드 시 모든 오퍼를 캐시하여 여러 서버 호출을 하나의 서버 호출로 줄일 수 있습니다.
* 오퍼가 기존 서버 호출로 인해 초래되는 지연 없이 캐시를 통해 즉시 표시되므로 사이트의 사용자 경험을 크게 향상시킬 수 있습니다.
* 단일 코드 행 및 일회용 개발자 설정을 사용하면 마케터가 SPA의 시각적 경험 작성기(VEC)를 통해 A/B 및 경험 타깃팅(XT) 활동을 만들고 실행할 수 있습니다.

## XDM 보기 및 단일 페이지 애플리케이션

SPA용 Adobe Target VEC는 &quot;보기&quot;라는 개념을 이용합니다. 이 개념은 SPA 경험을 함께 구성하는 시각적 요소의 논리 그룹입니다. 따라서 단일 페이지 애플리케이션은 사용자 상호 작용을 기반으로 URL 대신 보기를 통해 전환으로 간주할 수 있습니다. 보기는 일반적으로 전체 사이트를 나타내거나 사이트 내의 그룹화된 시각적 요소를 나타낼 수 있습니다.

&quot;보기&quot;가 무엇인지 더 설명하기 위해 다음 예제에서는 React에 구현된 가상의 온라인 전자 상거래 사이트를 사용하여 &quot;보기&quot; 예를 살펴봅니다.

홈 사이트로 이동한 후 영웅 이미지는 사이트에서 사용할 수 있는 최신 제품과 부활절 판매를 홍보합니다. 이 경우 전체 홈 화면에 대해 보기 를 정의할 수 있습니다. 이 보기는 간단히 &quot;홈&quot;이라고 할 수 있습니다.

![브라우저 창에서 단일 페이지 응용 프로그램의 샘플 이미지입니다.](assets/example-views.png)

고객이 비즈니스에서 판매하는 제품에 관심이 많아짐에 따라 **제품** 링크를 클릭하기로 합니다. 홈 사이트와 유사하게, 제품 사이트 전체를 보기로 정의할 수 있습니다. 이 보기의 이름은 &quot;products-all&quot;로 지정할 수 있습니다.

![모든 제품이 표시된 브라우저 창의 단일 페이지 응용 프로그램의 샘플 이미지입니다.](assets/example-products-all.png)

보기를 전체 사이트 또는 사이트의 시각적 요소 그룹으로 정의할 수 있으므로 제품 사이트에 표시된 4개의 제품을 그룹화하여 보기로 간주할 수 있습니다. 이 보기의 이름은 &quot;products&quot;로 지정할 수 있습니다.

![브라우저 창에 있는 단일 페이지 응용 프로그램의 샘플 이미지입니다(예: 제품 표시).](assets/example-products.png)

고객이 사이트에서 더 많은 제품을 탐색하기 위해 **추가 로드** 단추를 클릭하기로 결정하면 이 경우 웹 사이트 URL은 변경되지 않지만, 표시되는 두 번째 제품 행만 나타내는 보기 를 여기에 만들 수 있습니다. 보기 이름은 &quot;products-page-2&quot;일 수 있습니다.

![브라우저 창의 단일 페이지 응용 프로그램에 대한 샘플 이미지입니다(예: 추가 페이지에 제품 표시).](assets/example-load-more.png)

고객은 사이트에서 몇 가지 제품을 구매하기로 하고 체크아웃 화면으로 진행합니다. 체크아웃 사이트에서는 고객에게 일반 배달 또는 빠른 배달을 선택할 수 있는 옵션이 제공됩니다. &quot;보기&quot;는 사이트에서 임의의 시각적 요소 그룹일 수 있으므로 게재 환경 설정에 대해 보기를 만들고 &quot;게재 환경 설정&quot;이라고 할 수 있습니다.

![브라우저 창의 한 페이지 응용 프로그램 체크 아웃 페이지에 대한 샘플 이미지입니다.](assets/example-check-out.png)

&quot;보기&quot; 개념은 이보다 훨씬 더 확장될 수 있습니다. 다음은 사이트에서 정의할 수 있는 &quot;보기&quot;의 몇 가지 예입니다.

## XDM 보기 구현

Adobe Target에서 XDM 보기 를 활용하여 마케터가 시각적 경험 작성기를 통해 SPA에서 A/B 및 XT 테스트를 실행할 수 있습니다. 이 경우 일회용 개발자 설정을 완료하려면 다음 단계를 수행해야 합니다.

1. [Adobe Experience Platform Web SDK](/help/web-sdk/install/overview.md) 설치
2. 개인화할 단일 페이지 애플리케이션에서 모든 XDM 보기를 확인합니다.
3. XDM 보기를 정의한 후 AB 또는 XT VEC 활동을 전달하려면 단일 페이지 애플리케이션에서 `renderDecisions`을(를) `true`(으)로 설정하고 해당 XDM 보기를 사용하여 `sendEvent()` 함수를 구현하십시오. XDM 보기를 `xdm.web.webPageDetails.viewName`에 전달해야 합니다. 이 단계를 통해 마케터는 시각적 경험 작성기를 활용하여 해당 XDM에 대한 A/B 및 XT 테스트를 시작할 수 있습니다.

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
>첫 번째 `sendEvent()` 호출에서 최종 사용자에게 렌더링해야 하는 모든 XDM 보기를 가져오고 캐시합니다. 전달된 XDM 보기를 사용한 후속 `sendEvent()` 호출은 캐시에서 읽히고 서버 호출 없이 렌더링됩니다.

## `sendEvent()` 함수 예제

이 섹션에서는 가상의 전자 상거래 SPA에 대해 React에서 `sendEvent()` 함수를 호출하는 방법을 보여 주는 세 가지 예를 간략하게 설명합니다.

### 예제 1: A/B 테스트 홈 페이지

마케팅 팀은 전체 홈 페이지에서 A/B 테스트를 실행하려고 합니다.

![브라우저 창에서 단일 페이지 응용 프로그램의 샘플 이미지입니다.](assets/use-case-1.png)

전체 홈 사이트에서 A/B 테스트를 실행하려면 XDM `viewName`을(를) `home`(으)로 설정하여 `sendEvent()`을(를) 호출해야 합니다.

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

### 예제 2: 개인화된 제품

마케팅 팀은 사용자가 **추가 로드**&#x200B;를 클릭한 후 가격 레이블 색상을 빨간색으로 변경함으로써 제품의 두 번째 행을 개인화하려고 합니다.

![개인 맞춤화된 오퍼를 표시하는 브라우저 창의 단일 페이지 응용 프로그램의 샘플 이미지입니다.](assets/use-case-2.png)

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
    var page = this.state.page + 1; // assuming page number is derived from component's state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### 예제 3: A/B 테스트 게재 환경 설정

마케팅 팀은 **빠른 배달**&#x200B;을(를) 선택할 때 단추 색상을 파란색에서 빨간색으로 변경하면 전환을 더 끌어올릴 수 있는지 여부를 확인하기 위해 A/B 테스트를 실행하려고 합니다(두 배달 옵션 모두에 대해 단추 색상을 파란색으로 유지하는 것과 대조적으로).

![A/B 테스트와 함께 브라우저 창에 있는 단일 페이지 응용 프로그램의 샘플 이미지](assets/use-case-3.png)

선택한 게재 환경 설정에 따라 사이트에서 콘텐츠를 개인화하기 위해 각 게재 환경 설정에 대해 &quot;보기&quot;를 만들 수 있습니다. **일반 배달**&#x200B;을 선택하면 보기의 이름을 &quot;checkout-normal&quot;로 지정할 수 있습니다. **빠른 배달**&#x200B;을 선택한 경우 보기의 이름을 &quot;checkout-express&quot;로 지정할 수 있습니다.

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

## SPA용 시각적 경험 작성기 사용

XDM 보기 정의를 완료하고 전달된 해당 XDM 보기로 `sendEvent()`을(를) 구현하면 VEC가 이러한 보기를 감지하고 사용자가 A/B 또는 XT 활동에 대한 작업 및 수정 사항을 만드는 것을 허용할 수 있습니다.

>[!NOTE]
>
>SPA용 VEC를 사용하려면 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 또는 [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper 확장 프로그램을 설치하고 활성화해야 합니다.

### 수정 패널

수정 사항 패널에서는 특정 보기용으로 만들어진 작업을 캡처합니다. 보기에 대한 모든 작업은 해당 보기 아래에 그룹화됩니다.

![브라우저 창의 사이드바에 페이지 로드 옵션이 표시된 수정 사항 패널.](assets/modifications-panel.png)

### 작업

작업을 클릭하면 이 작업이 적용될 사이트의 요소가 강조 표시됩니다. 보기 아래에 만들어진 각 VEC 작업에는 **정보**, **편집**, **복제**, **이동** 및 **삭제** 아이콘이 있습니다. 이러한 아이콘은 다음 표에 자세히 설명되어 있습니다.

![작업 아이콘](assets/action-icons.png)

| 아이콘 | 설명 |
|---|---|
| 정보 | 작업의 세부 정보를 표시합니다. |
| 편집 | 작업의 속성을 직접 편집할 수 있습니다. |
| 복제 | 작업을 수정 패널에 있는 하나 이상의 보기에 복제하거나 VEC에서 탐색하고 이동한 하나 이상의 보기에 복제합니다. 이 작업은 반드시 수정 패널에 있지 않아도 됩니다.<br/><br/>**참고:** 복제 작업이 수행된 후에는 찾아보기를 통해 VEC의 보기로 이동해야 이동이 올바른 작업인지 확인할 수 있습니다. 작업을 보기에 적용할 수 없으면 오류가 표시됩니다. |
| 이동 | 작업을 페이지 로드 이벤트나 수정 패널에 이미 있는 다른 보기로 이동합니다.<br/><br/>**페이지 로드 이벤트:** 페이지 로드 이벤트에 해당하는 모든 작업은 웹 응용 프로그램의 초기 페이지 로드 시 적용됩니다. <br/><br/>**참고:** 이동 작업이 수행된 후에는 찾아보기를 통해 VEC의 보기로 이동해야 이동이 올바른 작업인지 확인할 수 있습니다. 작업을 보기에 적용할 수 없으면 오류가 표시됩니다. |
| 삭제 | 작업을 삭제합니다. |

## SPA용 VEC 사용 예

이 섹션에서는 시각적 경험 작성기를 사용하여 A/B 또는 XT 활동에 대한 작업 및 수정 사항을 만드는 세 가지 예를 간략하게 설명합니다.

### 예제 1: &quot;home&quot; 보기 업데이트

이 문서의 앞부분에서 &quot;홈&quot;이라는 보기가 전체 홈 사이트에 대해 정의되었습니다. 이제 마케팅 팀은 다음과 같은 방법으로 &quot;홈&quot; 보기를 업데이트하려고 합니다.

* **장바구니에 추가** 및 **비슷함** 단추를 파란색으로 더 밝게 변경합니다. 이 문제는 헤더의 구성 요소 변경이 필요하기 때문에 페이지 로드 중에 발생해야 합니다.
* **2019년 최신 제품** 레이블을 **2019년 가장 인기 있는 제품**(으)로 변경하고 텍스트 색상을 자주색으로 변경합니다.

VEC에서 업데이트하려면 **작성**&#x200B;을 선택하고 &quot;홈&quot; 보기에 해당 변경 내용을 적용합니다.

![시각적 경험 작성기 샘플 페이지](assets/vec-home.png)

### 예제 2: 제품 레이블 변경

&quot;products-page-2&quot; 보기의 경우 마케팅 팀이 **가격** 레이블을 **판매 가격**(으)로 변경하고 레이블 색상을 빨간색으로 변경하려고 합니다.

VEC에서 이러한 업데이트를 수행하려면 다음 단계를 수행해야 합니다.

1. VEC에서 **찾아보기**&#x200B;를 선택합니다.
2. 사이트 위쪽 탐색에서 **제품**&#x200B;을 선택합니다.
3. 두 번째 제품 행을 보려면 **추가 로드**&#x200B;를 한 번 선택하십시오.
4. VEC에서 **작성**&#x200B;을 선택합니다.
5. 작업을 적용하여 텍스트 레이블을 **판매 가격**(으)로 변경하고 색상을 빨간색으로 변경합니다.

![제품 레이블이 있는 시각적 경험 작성기 샘플 페이지](assets/vec-products-page-2.png)

### 예제 3: 게재 환경 설정 스타일 개인화

보기는 라디오 버튼의 상태 또는 옵션과 같이 세분화된 수준에서 정의할 수 있습니다. 이 문서의 앞부분에서 &quot;checkout-normal&quot; 및 &quot;checkout-express&quot; 게재 환경 설정을 정의했습니다. 마케팅 팀이 &quot;checkout-express&quot; 보기에 대해 단추 색상을 빨간색으로 변경하려고 합니다.

VEC에서 이러한 업데이트를 수행하려면 다음 단계를 수행해야 합니다.

1. VEC에서 **찾아보기**&#x200B;를 선택합니다.
2. 사이트의 장바구니에 제품을 추가합니다.
3. 사이트의 오른쪽 위 모서리에 있는 장바구니 아이콘을 선택합니다.
4. **주문 체크아웃**&#x200B;을 선택합니다.
5. **배달 기본 설정**&#x200B;에서 **빠른 배달** 라디오 단추를 선택하십시오.
6. VEC에서 **작성**&#x200B;을 선택합니다.
7. **결제** 단추 색상을 빨간색으로 변경합니다.

>[!NOTE]
>
>**빠른 배달** 라디오 단추를 선택할 때까지 &quot;checkout-express&quot; 보기가 수정 패널에 표시되지 않습니다. 이는 **빠른 배달** 라디오 단추가 선택되어 있으면 `sendEvent()` 함수가 실행되므로 라디오 단추를 선택할 때까지 VEC가 &quot;checkout-express&quot; 보기를 인식하지 않기 때문입니다.

![시각적 경험 작성기에서 게재 환경 설정 선택기를 표시합니다.](assets/vec-delivery-preference.png)
