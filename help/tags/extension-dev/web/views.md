---
title: 웹 확장의 보기
description: Adobe Experience Platform 웹 확장에서 라이브러리 모듈의 보기를 정의하는 방법을 알아봅니다.
exl-id: 4471df3e-75e2-4257-84c0-dd7b708be417
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 73%

---

# 웹 확장의 보기

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

각 이벤트, 조건, 작업 또는 데이터 요소 유형마다 사용자가 설정을 제공할 수 있는 보기를 제공할 수 있습니다. 또한 확장에는 사용자가 전체 확장에 대한 전역 설정을 제공할 수 있는 최상위 [확장 구성 보기](../configuration.md)가 있을 수 있습니다. 뷰 개발 프로세스는 모든 유형의 뷰에서 동일합니다.

## 문서 유형 포함

HTML 파일에 `doctype` 태그를 포함해야 합니다. 일반적으로 이는 HTML 파일이 다음으로 시작됨을 의미합니다.

```xml
<!DOCTYPE html>
```

## 태그 iframe 스크립트 포함

보기의 HTML 내에 태그 iframe 스크립트를 포함합니다.

```html
<script src="https://assets.adobedtm.com/activation/reactor/extensionbridge/extensionbridge.min.js"></script>
```

이 스크립트는 보기가 태그 애플리케이션과 통신할 수 있도록 하는 통신 API를 제공합니다.

## 확장 브리지 통신 API에 등록

iframe 스크립트가 로드되면 통신에서 사용할 태그에 몇 가지 메서드를 제공해야 합니다. 다음과 같이 `window.extensionBridge.register`를 호출하고 객체를 전달합니다.

```js
window.extensionBridge.register({
  init: function(info) {
    // Populate view with info.settings which will exist if the user is editing something
    // that was previously saved.
    if (info.settings) {
      document.getElementById('name').value = info.settings.name;
    }
  },
  validate: function() {
    // Return whether the view is valid.
    return document.getElementById('name').value.length > 0;
  },
  getSettings: function() {
    // Return user-provided settings.
    return {
      name: document.getElementById('name').value
    };
  }
});
```

특정 보기 요구 사항에 맞게 각 메서드의 내용을 수정해야 합니다.

### [!DNL init]

`init` 메서드는 보기가 iframe에 로드되는 즉시 태그에 의해 호출됩니다. 그러면 다음 속성을 포함하는 객체인 단일 인수(`info`)가 전달됩니다.

| 속성 | 설명 |
| --- | --- |
| `settings` | 이 보기에서 이전에 저장한 설정이 포함된 객체입니다. `settings`가 `null`인 경우 사용자가 저장된 버전을 로드하지 않고 초기 설정을 개발 중임을 나타냅니다. `settings`가 객체인 경우에는 사용자가 이전의 지속형 설정을 편집하도록 선택했으므로 이 객체를 사용하여 뷰를 채워야 합니다. |
| `extensionSettings` | 확장 구성 보기에서 설정이 저장되었습니다. 확장 구성 보기가 아닌 보기의 확장 설정에 액세스하는 데 유용합니다. 현재 보기가 확장 구성 보기인 경우 `settings`을(를) 사용합니다. |
| `propertySettings` | 속성에 대한 설정이 포함된 객체입니다. 이 객체에 포함된 사항에 대한 자세한 내용은 [터빈 객체 안내서](../turbine.md#property-settings)를 참조하십시오. |
| `tokens` | API 토큰이 포함된 객체입니다. 보기 내에서 Adobe API에 액세스하려면 일반적으로 `tokens.imsAccess` 아래의 IMS 토큰을 사용해야 합니다. 이 토큰은 Adobe에서 개발한 확장에만 사용할 수 있습니다. Adobe에서 개발한 확장을 제공하는 Adobe 직원의 경우 [데이터 수집 엔지니어링 팀에 전자 메일을 보내](mailto:reactor@adobe.com)하고 허용 목록에 추가할 수 있도록 확장 이름을 제공하십시오. |
| `company` | 단일 속성 `orgId`을(를) 포함하는 개체로, Adobe Experience Cloud ID(24자 영숫자 문자열)를 나타냅니다. |
| `schema` | [JSON 스키마](https://json-schema.org/) 형식의 객체입니다. 이 객체는 [확장 매니페스트](../manifest.md)에서 가져오며 양식 유효성 검사에 도움이 될 수 있습니다. |

이 정보를 사용하여 양식을 렌더링하고 관리해야 합니다. `info.settings`만 처리하면 되지만, 필요한 경우 다른 정보가 제공됩니다.

### [!DNL validate]

사용자가 &quot;저장&quot; 버튼을 누르면 `validate` 메서드가 호출됩니다. 다음 중 하나가 반환됩니다.

* 사용자의 입력이 유효한지 여부를 나타내는 부울 값.
* 사용자의 입력이 유효한지 여부를 나타내는 부울을 사용하여 나중에 해결할 약속.

라이브러리 모듈은 해당 입력에 따라 작동하므로 유효한 입력을 구성하는 것은 확장 개발자의 책임입니다.

사용자의 입력이 잘못된 경우, 사용자가 수정해야 하는 사항을 알 수 있도록 보기 내에 이 정보를 표시하십시오.

### [!DNL getSettings]

사용자가 &quot;저장&quot; 버튼을 누르고 보기의 유효성을 검사한 후에 `getSettings` 메서드가 호출됩니다. 함수는 다음 중 하나를 반환합니다.

* 사용자 입력에 따른 설정이 포함된 객체.
* 사용자 입력에 따른 설정이 포함된 객체를 사용하여 나중에 해결할 약속.

이 설정 객체는 나중에 태그 런타임 라이브러리에서 제공됩니다. 이 객체의 내용은 사용자가 제공합니다. 객체는 JSON과 직렬화 또는 역직렬화할 수 있어야 합니다. 함수 또는 [RegExp](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/RegExp) 인스턴스와 같은 값은 이러한 기준을 충족하지 않으므로 허용되지 않습니다.

## 공유 보기 활용

`window.extensionBridge` 개체에는 태그를 통해 사용할 수 있는 기존 보기를 이용할 수 있는 여러 메서드가 있으므로 보기 내에서 해당 보기를 재현할 필요가 없습니다. 사용 가능한 메서드는 다음과 같습니다.

### [!DNL openCodeEditor]

```js
window.extensionBridge.openCodeEditor().then(function(code) { 
  console.log(code);
});
```

이 메서드를 호출하면 사용자가 코드 조각을 편집할 수 있는 모달이 표시됩니다. 사용자가 코드 편집을 완료하면 약속이 업데이트된 코드로 해결됩니다. 사용자가 변경 내용을 저장하지 않고 코드 편집기를 닫으면 약속이 해결되지 않습니다. `options` 객체를 다음과 같이 구조화해야 합니다.

| 속성 | 설명 |
| --- | --- |
| `code` | 편집기에 표시되어야 하는 코드입니다. 일반적으로 사용자가 기존 코드를 편집할 때 제공됩니다. 이 값을 제공하지 않는 경우 코드 편집기를 열면 비어 있게 됩니다. |
| `language` | 편집할 코드의 언어입니다. 유효한 옵션은 `javascript`, `html` `css`, `json` 및 `plaintext`입니다. 이 값을 제공하지 않으면 이 `javascript`를 가정합니다. |

### [!DNL openRegexTester]

```js
window.extensionBridge.openRegexTester().then(function(pattern) { 
  console.log(pattern);
});
```

이 메서드를 호출하면 사용자가 정규 표현식 패턴을 테스트 및 수정할 수 있는 모달이 표시됩니다. 사용자가 정규 표현식 편집을 완료하면 약속이 업데이트된 정규 표현식 패턴으로 해결됩니다. 사용자가 변경 내용을 저장하지 않고 regex 테스터를 닫으면 약속이 해결되지 않습니다. `options` 객체에는 다음 속성이 포함되어야 합니다.

| 속성 | 설명 |
| --- | --- |
| `pattern` | 테스터 내의 패턴 필드의 초기 값으로 사용해야 하는 정규 표현식 패턴입니다. 일반적으로 사용자가 기존 정규 표현식을 편집할 때 제공됩니다. 이 값이 제공되지 않으면 처음에는 패턴 필드가 비어 있게 됩니다. |
| `flags` | 테스터가 사용해야 하는 일반 표현식 플래그입니다. 예를 들어, `gi`는 전역 일치 플래그와 대/소문자 무시 플래그를 지정합니다. 이러한 플래그는 테스터 내의 사용자가 수정할 수 없지만 일반 표현식을 실행할 때 확장에서 사용할 특정 플래그를 표시하는 데 사용됩니다. 제공되지 않으면 테스터에서 플래그가 사용되지 않습니다. 정규 표현식 플래그에 대한 자세한 내용은 [MDN의 RegExp 설명서](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/RegExp)를 참조하십시오.<br><br>일반적인 시나리오는 일반 표현식에 대한 대소문자 구분을 전환할 수 있는 확장입니다. 이 기능을 지원하기 위해 확장은 일반적으로 확장 보기 내에 확인란을 제공하며 이 확인란을 선택하면 대소문자 무시(`i` 플래그로 표시됨)가 활성화됩니다. 뷰로 저장된 설정 객체의 경우 일반 표현식을 실행하는 라이브러리 모듈에서 `i` 플래그를 사용할지 여부를 알 수 있도록 확인란을 선택했는지 여부를 표시해야 합니다. 또한, 확장 보기에서 일반 표현식 테스터를 열려면 대/소문자 구분 확인란이 선택되면 `i` 플래그를 전달해야 합니다. 이렇게 하면 사용자가 대/소문자 구분을 활성화한 상태로 정규 표현식을 제대로 테스트할 수 있습니다. |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

이 메서드를 호출하면 사용자가 데이터 요소를 선택할 수 있는 모달이 표시됩니다. 사용자가 데이터 요소 선택을 완료하면 선택한 데이터 요소의 이름으로 약속이 해결됩니다(기본적으로 이름의 앞 및 뒤에는 퍼센트 기호가 표시됨). 사용자가 변경 내용을 저장하지 않고 요소 선택기를 닫으면 약속이 해결되지 않습니다.

`options` 개체에는 단일 부울 속성인 `tokenize`이(가) 있어야 합니다. 이 속성은 약속을 해결하기 전에 선택한 데이터 요소의 이름을 퍼센트 기호로 둘러싸야 하는지 여부를 나타냅니다. 이 기능이 유용한 이유를 살펴보려면 [데이터 요소 지원](#supporting-data-elements) 섹션을 참조하십시오. 이 옵션은 기본적으로 `true`로 설정되어 있습니다.

## 데이터 요소 지원 {#supporting-data-elements}

보기에 사용자가 데이터 요소를 활용하려는 양식 필드가 있을 수 있습니다. 예를 들어, 보기에 사용자가 제품 이름을 입력해야 하는 텍스트 필드가 있는 경우 사용자가 필드에 하드 코딩된 값을 입력하는 것은 적합하지 않을 수 있습니다. 대신 필드의 값이 동적(런타임 시 결정)이고 데이터 요소를 사용하여 이를 수행할 수 있습니다.

예를 들어, 변환을 추적하기 위해 비콘을 보내는 확장을 개발하고 있다고 가정해 보겠습니다. 그리고 이 경우 비콘이 보내는 데이터 중 하나가 제품 이름입니다. 사용자가 비콘을 구성할 수 있는 확장 보기에는 제품 이름에 대한 텍스트 필드가 있을 수 있습니다. 제품 이름은 비콘이 전송될 페이지에 따라 달라지기 때문에 Experience Platform 사용자가 &quot;Calzone Oven XL&quot;과 같은 정적 제품 이름을 입력하는 것은 일반적으로 의미가 없습니다. 이 기능은 데이터 요소에 가장 적합합니다.

사용자가 제품 이름 값에 대해 이름이 `productname`인 데이터 요소를 사용하려는 경우 앞과 뒤 모두에 퍼센트 기호가 있는 데이터 요소의 이름(`%productname%`)을 입력할 수 있습니다. 퍼센트 기호가 래핑된 데이터 요소 이름을 &quot;데이터 요소 토큰&quot;라고 합니다. Experience Platform 사용자는 이러한 구문에 익숙할 수 있습니다. 그러면 확장은 내보내는 `settings` 객체 내에 데이터 요소 토큰을 저장합니다. 설정 객체는 다음과 유사할 수 있습니다.

```js
{
  productName: '%productname%'
}
```

런타임 시 설정 객체를 라이브러리 모듈에 전달하기 전에 설정 객체가 스캔되고 모든 데이터 요소 토큰이 해당 값으로 대체됩니다. 런타임 시 `productname` 데이터 요소의 값이 `Ceiling Medallion Pro 2000`인 경우 라이브러리 모듈에 전달되는 설정 객체는 다음과 같습니다.

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

사용자가 데이터 요소를 사용하고 데이터 요소를 쉽게 입력할 수 있도록 하는 데 도움이 될 수 있는 위치를 나타내려면 다음과 같이 해당 필드 옆에 아이콘 버튼을 추가하는 것이 좋습니다.

![데이터 요소 필드](../images/data-element-field.png)

>[!NOTE]
>
>적절한 아이콘을 다운로드하려면 Adobe Spectrum[&#128279;](https://spectrum.adobe.com/page/icons/)의 아이콘 페이지로 이동하여 &quot;[!DNL Data]&quot;을(를) 검색합니다.

텍스트 필드 옆에 있는 버튼을 사용자가 선택하면 `window.extensionBridge.openDataElementSelector`위의 설명[과 같이 ](#open-data-element)가 호출됩니다. 이름 및 유형 퍼센트 기호를 기억하도록 하는 대신 사용자가 선택할 수 있는 사용자 데이터 요소 목록이 표시됩니다. 사용자가 데이터 요소를 선택하면 퍼센트 기호로 둘러싸인 선택한 데이터 요소의 이름이 전달됩니다(`tokenize` 옵션을 `false`로 설정한 경우 제외). 그런 다음 텍스트 필드를 결과로 채우는 것이 좋습니다.

### 데이터 요소 토큰 바꾸기

앞에서 설명한 대로, 지속형 설정 객체가 다음과 같이 구성되어 있는 경우:

```js
{
  productName: '%productname%'
}
```

그리고 런타임에 `productname` 데이터 요소의 값이 `Ceiling Medallion Pro 2000`인 경우 라이브러리 모듈에 전달되는 설정 객체는 다음과 같습니다.

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

설정 내의 값이 퍼센트 기호, 문자열, 퍼센트 기호 _및_&#x200B;로만 구성되는 경우, _데이터 요소 값의 유형을 변경하지 않고_ 데이터 요소 값으로 바뀝니다.

예를 들어, 런타임에 `productname`의 값이 문자열이 아닌 숫자`538`(문자열 아님)인 경우 라이브러리 모듈에 전달되는 설정 객체는 다음과 같습니다.

```js
{
  productName: 538
}
```

결과 `538`은 여기에서 문자열이 아닌 숫자입니다. 마찬가지로 런타임 시 데이터 요소 값이 함수(드물지만 사용 가능한 경우)인 경우 결과적인 설정 객체는 다음과 같습니다.

```js
{
  productName: function() { … }
}
```

반면, 지속형 설정 객체가 다음과 같다고 가정해 보겠습니다.

```js
{
  productName: '%productname% - %modelnumber%'
}
```

이 경우 `productName`의 값이 단일 데이터 요소 토큰 을 초과하므로 결과는 항상 문자열입니다. 각 데이터 요소 토큰은 문자열로 캐스팅된 후 해당 값으로 대체됩니다. 런타임 시 `productname`의 값이 `Ceiling Medallion Pro`(문자열)이고 `modelnumber`의 값이 `2000`(숫자)인 경우 라이브러리 모듈에 전달되는 결과 설정 객체는 다음과 같습니다.

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## 탐색 방지

확장 보기와 포함된 데이터 수집 사용자 인터페이스 간의 통신은 확장 보기 내에서의 탐색 발생 여부에 따라 달라집니다. 그러므로 사용자가 확장 보기의 HTML 페이지에서 이동할 수 있는 기능을 확장 보기에 추가하지 마십시오. 예를 들어, 확장 보기 내에 링크를 제공하는 경우에는 새 브라우저 창에서 열려야 합니다(일반적으로 앵커 태그에 `target="_blank"` 추가). 확장 보기 내에서 `form` 요소를 사용할 수 있도록 하는 경우에는 양식이 제출되지 않아야 합니다. 양식 내에 `button` 요소가 있지만 `type="button"`을 추가하지 않으면 실수로 양식을 제출할 수 있습니다. 확장 보기 내에서 양식을 제출하면 HTML 문서가 새로 고쳐져 사용자 환경이 손상될 수 있습니다.
