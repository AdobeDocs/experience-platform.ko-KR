---
title: 코어 이벤트 전달 확장 개요
description: Adobe Experience Platform의 핵심 이벤트 전달 확장에 대해 알아봅니다.
feature: Event Forwarding
exl-id: b5ee4ccf-6fa5-4472-be04-782930f07e20
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 91%

---

# 코어 이벤트 전달 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

코어 이벤트 전달 확장은 Adobe Experience Platform에서 이벤트 전달을 위한 기본 이벤트, 조건 및 데이터 유형을 제공합니다.

이 확장을 사용하여 규칙을 작성할 때 사용할 수 있는 옵션에 대한 정보를 보려면 이 참조를 사용하십시오.

## 코어 확장 조건 유형

이 섹션에서는 코어 확장에서 사용할 수 있는 조건 유형을 설명합니다.  이러한 조건 유형은 일반 또는 예외 논리 유형과 함께 사용할 수 있습니다.

### 사용자 지정 코드

이벤트의 조건으로 존재해야 하는 사용자 지정 코드를 지정합니다. 내장된 코드 편집기를 사용하여 사용자 지정 코드를 입력합니다. Adobe Experience Platform의 이벤트 전달은 ES6을 지원합니다.

1. 선택 **[!UICONTROL 편집기 열기]**.
1. 사용자 지정 코드를 입력합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

사용자 지정 코드의 데이터 요소 값에 액세스하려면 `getDataElementValue` 메서드를 사용합니다. 예를 들어 `productName`이라는 데이터 요소의 값을 검색하려면 다음을 입력합니다.

```javascript
getDataElementValue('productName') 
```

#### ruleStash 개체

사용자 지정 코드에서는 `ruleStash` 개체를 사용할 수도 있습니다.

```javascript
utils.logger.log(context.arc.ruleStash);
```

`ruleStash`는 작업 모듈에서 모든 결과를 수집하는 개체입니다.

각 확장에는 고유한 네임스페이스가 있습니다. 예를 들어, 확장명의 이름이 `send-beacon`인 경우, `send-beacon` 작업의 모든 결과가 `ruleStash['send-beacon']` 네임스페이스에 저장됩니다.

```javascript
utils.logger.log(context.arc.ruleStash['adobe-cloud-connector']);
```

이 네임스페이스는 각 확장에 대해 고유하며 시작 부분에 `undefined` 값이 있습니다.

이 네임스페이스는 각 동작에서 반환된 결과로 재정의됩니다. 네임스페이스에 특별한 상황이 발생하지 않습니다. 예를 들어, 두 가지 작업 `generate-fullname` 및 `generate-fulladdress`을 포함하는 `transform` 확장이 있는 경우, 다음 두 작업을 규칙에 추가합니다.

`generate-fullname` 작업의 결과가 `Firstname Lastname`이면 작업이 완료된 후 다음과 같이 규칙 스태시가 표시됩니다.

```js
{
  transform: 'Firstname Lastname`
}
```

`generate-address` 작업의 결과가 `3900 Adobe Way`이면 작업이 완료된 후 다음과 같이 규칙 스태시가 표시됩니다.

```js
{
  transform: '3900 Adobe Way`
}
```

`Firstname Lastname`은 더 이상 규칙 스태시에 존재하지 않습니다. `generate-address` 작업에서 주소를 재정의했기 때문입니다.

`ruleStash`의 `transform` 네임스페이스 안에 있는 두 작업의 결과를 저장하려면 다음 예제와 비슷한 작업 모듈을 작성할 수 있습니다.

```javascript
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;
  if (!transformRuleStash) {
    transformRuleStash = {};
  }
  transformRuleStash.fullName = 'Firstname Lastname';
  return transformRuleStash;
}
```

이 작업을 처음 실행할 때 `ruleStash`은 `undefined`이고 빈 개체로 초기화됩니다. 다음 번에 이 작업을 실행하면 이전에 호출한 작업에 의해 `ruleStash`가 반환됩니다. 개체를 `ruleStash`로 사용하면 확장의 다른 작업에서 이전에 설정한 데이터를 손실하지 않고 새 데이터를 추가할 수 있습니다.

이 경우 전체 확장 규칙 스태시를 항상 반환하도록 주의해야 합니다. 값만 반환(예: 5)하려는 경우, 규칙 스태시가 다음과 같습니다.

```js
{
  transform: 5
}
```

### 값 비교 {#value-comparison}

두 값을 비교하여 이 조건이 true를 반환하는지 여부를 확인합니다.

규칙에 여러 조건이 있는 경우 이 조건이 true를 반환하지만 다른 조건이 false로 평가되거나 예외 항목 중 하나가 true로 평가되기 때문에 규칙이 실행되지 않을 수 있습니다.

1. 값을 제공합니다.
1. 연산자를 선택합니다. 자세한 내용은 아래의 값 비교 연산자 목록을 참조하십시오.
1. 비교할 다른 값을 제공합니다.

다음 값 비교 연산자를 사용할 수 있습니다.

**같음:** 엄격하지 않은 비교(JavaScript에서 == 연산자)를 사용하여 두 값이 같으면 조건이 true를 반환합니다. 값은 모든 유형일 수 있습니다. _true_, _false_, _null_ 또는 _undefined_&#x200B;와 같은 단어를 값 필드에 입력할 때 이 단어는 문자열로 비교되고 같은 의미의 JavaScript로 변환되지 않습니다.

**같지 않음:** 엄격하지 않은 비교(JavaScript에서 != 연산자)를 사용하여 두 값이 같지 않으면 조건이true를 반환합니다. 값은 모든 유형일 수 있습니다. _true_, _false_, _null_ 또는 _undefined_&#x200B;와 같은 단어를 값 필드에 입력할 때 이 단어는 문자열로 비교되고 같은 의미의 JavaScript로 변환되지 않습니다.

**포함:** 첫 번째 값에 두 번째 값이 포함되면 조건이 true를 반환합니다. 숫자는 문자열로 변환됩니다. 숫자 또는 문자열 이외의 값은 false를 반환하는 조건이 됩니다.

**포함하지 않음:** 첫 번째 값에 두 번째 값이 포함되지 않으면 조건이 true를 반환합니다. 숫자는 문자열로 변환됩니다. 숫자 또는 문자열 이외의 값은 true를 반환하는 조건이 됩니다.

**다음으로 시작:** 첫 번째 값이 두 번째 값으로 시작하는 경우 조건이 true를 반환합니다. 숫자는 문자열로 변환됩니다. 숫자 또는 문자열 이외의 값은 false를 반환하는 조건이 됩니다.

**다음으로 시작하지 않음:** 첫 번째 값이 두 번째 값으로 시작되지 않으면 조건이 true를 반환합니다. 숫자는 문자열로 변환됩니다. 숫자 또는 문자열 이외의 값은 true를 반환하는 조건이 됩니다.

**종료 문자:** 첫 번째 값이 두 번째 값으로 끝나는 경우 조건이 true를 반환합니다. 숫자는 문자열로 변환됩니다. 숫자 또는 문자열 이외의 값은 false를 반환하는 조건이 됩니다.

**다음으로 끝나지 않음:** 첫 번째 값이 두 번째 값으로 끝나지 않으면 조건이 true를 반환합니다. 숫자는 문자열로 변환됩니다. 숫자 또는 문자열 이외의 값은 true를 반환하는 조건이 됩니다.

**RegEx와 일치:** 첫 번째 값이 정규 표현식과 일치하면 조건이 true를 반환합니다. 숫자는 문자열로 변환됩니다. 숫자 또는 문자열 이외의 값은 false를 반환하는 조건이 됩니다.

**Regex와 일치하지 않음:** 첫 번째 값이 정규 표현식과 일치하지 않으면 조건이 true를 반환합니다. 숫자는 문자열로 변환됩니다. 숫자 또는 문자열 이외의 값은 true를 반환하는 조건이 됩니다.

**다음보다 작음:** 첫 번째 값이 두 번째 값보다 작은 경우 조건이 true를 반환합니다. 숫자를 나타내는 문자열은 숫자로 변환됩니다. 숫자 또는 변환 가능한 문자열 이외의 값은 false를 반환하는 조건이 됩니다.

**다음보다 작거나 같음:** 첫 번째 값이 두 번째 값보다 작거나 같은 경우 조건이 true를 반환합니다. 숫자를 나타내는 문자열은 숫자로 변환됩니다. 숫자 또는 변환 가능한 문자열 이외의 값은 false를 반환하는 조건이 됩니다.

**다음보다 큼:** 첫 번째 값이 두 번째 값보다 큰 경우 조건이 true를 반환합니다. 숫자를 나타내는 문자열은 숫자로 변환됩니다. 숫자 또는 변환 가능한 문자열 이외의 값은 false를 반환하는 조건이 됩니다.

**다음보다 크거나 같음:** 첫 번째 값이 두 번째 값보다 크거나 같은 경우 조건이 true를 반환합니다. 숫자를 나타내는 문자열은 숫자로 변환됩니다. 숫자 또는 변환 가능한 문자열 이외의 값은 false를 반환하는 조건이 됩니다.

**참인 경우:** 값이 true 값을 갖는 부울이면 조건이 true를 반환합니다. 제공한 값이 다른 유형인 경우 부울로 변환되지 않습니다. true 값을 갖는 부울 이외의 값은 false를 반환하는 조건이 됩니다.

**참 같은 값(Truthy)인 경우:** 값이 부울로 변환된 후 true이면 조건이 true를 반환합니다. 신뢰할 수 있는 값의 예는 [MDN의 Truthy 설명서](https://developer.mozilla.org/ko-KR/docs/Glossary/Truthy)를 참조하십시오.

**거짓인 경우:** 값이 false 값을 갖는 부울이면 조건이 true를 반환합니다. 제공한 값이 다른 유형인 경우 부울로 변환되지 않습니다. false 값을 갖는 부울 이외의 값은 false를 반환하는 조건이 됩니다.

**거짓 같은 값(Falsy):** 값이 부울로 변환된 후 false이면 조건이 true를 반환합니다. 잘못된 값의 예는 [MDN의 Falsy 설명서](https://developer.mozilla.org/ko-KR/docs/Glossary/Falsy)를 참조하십시오.



## 코어 확장 작업 유형

이 섹션에서는 코어 확장에서 사용할 수 있는 작업 유형을 설명합니다.

### 사용자 지정 코드

이벤트가 트리거되고 조건이 평가된 후 실행되는 코드를 제공합니다. Adobe Experience Platform의 이벤트 전달은 ES6을 지원합니다.

1. 작업 코드에 이름을 지정합니다.
1. 선택 **[!UICONTROL 편집기 열기]**.
1. 코드를 편집한 다음 **[!UICONTROL 저장]**.

사용자 지정 코드의 데이터 요소 값에 액세스하려면 `getDataElementValue` 메서드를 사용합니다. 예를 들어 `productName`이라는 데이터 요소의 값을 검색하려면 다음을 입력합니다.

```javascript
getDataElementValue('productName') 
```

이벤트 전달 작업은 순차적으로 실행됩니다. 한 작업의 사용자 지정 코드에서 후속 작업에서 사용할 수 있는 값을 반환할 수도 있습니다. 반환된 값은 해당 작업 내의 코드나 외부 소스에 대한 호출의 응답 본문에서 가져올 수 있습니다. 코어 확장이 사용되는 단일 규칙 내에서 이전에 실행된 작업의 데이터를 참조하려면 `Path` 유형의 데이터 요소를 만들고 다음 경로를 사용하여 코어 확장 내의 사용자 지정 코드에 정의된 `productCategory` 변수의 값을 참조합니다.

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## 코어 확장 데이터 요소 유형

데이터 요소 유형은 확장에 의해 결정됩니다. 만들 수 있는 유형에는 제한이 없습니다.

다음 섹션에서는 코어 확장에서 사용할 수 있는 데이터 요소 유형에 대해 설명합니다. 확장마다 다른 유형의 데이터 요소를 사용합니다.

### 사용자 지정 코드

사용자 지정 JavaScript는 다음을 선택하여 UI에 입력할 수 있습니다.  **[!UICONTROL 편집기 열기]** 를 클릭하고 코드를 편집기 창에 삽입합니다.

데이터 요소 값으로 어떤 값을 사용해야 하는지 알 수 있도록 편집기 창에 문장이 반환되어야 합니다. return 문이 포함되지 않거나 `null` 또는 `undefined` 값이 반환되면 데이터 요소의 기본값은 `null` 또는 `undefined`을 반영합니다. 

사용자 지정 코드의 데이터 요소 값에 액세스하려면 `getDataElementValue` 메서드를 사용합니다. 예를 들어 `productName`이라는 데이터 요소의 값을 검색하려면 다음을 입력합니다.

```javascript
getDataElementValue('productName') 
```

**예:**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### 경로

Adobe Experience Platform Edge Network로 전송된 이벤트에 대한 키-값 쌍의 경로는 경로 데이터 요소 유형을 사용하여 참조할 수 있습니다.

이벤트의 전체 개체를 참조하려면 `arc`를 경로로 입력합니다. 축약어 `arc`는 Adobe Resource Context를 의미하며 Adobe Experience Platform Edge Network로 전송된 이벤트의 최상위 레벨 경로입니다.

예를 들어, 클라이언트에서 Edge Network로 `interact` 호출을 보낼 경우 브라우저 콘솔에서 볼 수 있는 다음과 같은 요청이 있습니다.

```javascript
"events": [ 
        { 
             "xdm": { 
                    "page": { 
                            "btnHover": false, 
                            "pageName": "We Travel Home Page", 
                            "siteSection": "Landing Page" 
                     }] 
```

`pageName`을 참조하는 경로를 입력하려면 경로 필드에 다음을 입력합니다.

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>다음 `interact` 클라이언트로부터의 호출이 `events`, 하지만 이벤트 전달을 위해서는 다음이 필요합니다 `event`. 이는 이벤트 전달이 각 이벤트를 개별적으로 검사하기 때문이며, 클라이언트에서와 같이 여러 이벤트를 일괄 처리하는 것은 아닙니다.
