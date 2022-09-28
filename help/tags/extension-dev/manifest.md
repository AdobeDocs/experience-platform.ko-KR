---
title: 확장 매니페스트
description: 확장을 제대로 사용하는 방법을 Adobe Experience Platform에 알려주는 JSON 매니페스트 파일을 구성하는 방법을 알아봅니다.
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '2645'
ht-degree: 69%

---

# 확장 매니페스트

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../term-updates.md)를 참조하십시오.

확장의 기본 디렉터리에 이름이 `extension.json`인 파일을 생성해야 합니다. 여기에는 Adobe Experience Platform에서 해당 확장을 적절히 사용할 수 있도록 해 주는 중요한 세부 정보가 포함되어 있습니다. 일부 컨텐츠는 [npm의 `package.json`](https://docs.npmjs.com/files/package.json) 방식을 따라 형성됩니다.

예제 `extension.json`은 [Hello World 확장 ](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json) GitHub 리포지토리에서 찾을 수 있습니다.

확장 매니페스트는 다음과 같이 구성되어야 합니다.

| 속성 | 설명 |
| --- | --- |
| `name` | 확장의 이름. 다른 모든 확장과는 다른 고유한 이름을 사용하고 [명명 규칙](#naming-rules)을 준수해야 합니다. **이 이름은 태그에서 식별자로 사용되며 확장을 게시한 후에는 변경할 수 없습니다.** |
| `platform` | 확장을 위한 플랫폼. 현재 허용되는 유일한 값은 `web`입니다. |
| `version` | 확장의 버전. 버전은 [semver](https://semver.org/) 버전 관리 형식을 준수해야 합니다. 그리고 [npm 버전 필드](https://docs.npmjs.com/files/package.json#version)와 일치합니다. |
| `displayName` | 사용자가 읽을 수 있는 확장의 이름. Platform 사용자에게 표시됩니다. &quot;태그&quot; 또는 &quot;확장&quot;을 언급할 필요가 없습니다. 사용자는 이미 태그 확장을 보고 있음을 알 수 있습니다. |
| `description` | 확장에 대한 설명. Platform 사용자에게 표시됩니다. 사용자가 웹 사이트에서 제품을 구현할 수 있도록 확장을 지원하는 경우 제품의 기능을 설명하십시오. &quot;태그&quot; 또는 &quot;확장&quot;을 언급할 필요가 없습니다. 사용자는 이미 태그 확장을 보고 있음을 알 수 있습니다. |
| `iconPath` *(선택 사항)* | 확장에 대해 표시될 아이콘의 상대 경로입니다. 슬래시로 시작하지 않아야 합니다. 확장자가 `.svg`인 SVG 파일을 참조해야 합니다. SVG은 정사각형이어야 하며 플랫폼에 따라 조정될 수 있습니다. |
| `author` | author는 다음과 같이 구조화해야 하는 객체입니다. <ul><li>`name`: 확장 작성자의 이름입니다. 아니면 여기에서 회사 이름을 사용할 수도 있습니다.</li><li>`url` *(선택 사항)*: 확장 작성자에 대한 자세한 정보를 확인할 수 있는 URL입니다.</li><li>`email` *(선택 사항)*: 확장 작성자의 이메일 주소입니다.</li></ul>이는 [npm 작성자 필드](https://docs.npmjs.com/files/package.json#people-fields-author-contributors) 규칙과 일치합니다. |
| `exchangeUrl` *(공개 확장의 경우 필수)* | Adobe Exchange에서 확장 목록에 대한 URL입니다. `https://www.adobeexchange.com/experiencecloud.details.######.html` 패턴과 일치해야 합니다. |
| `viewBasePath` | 모든 보기 및 보기 관련 리소스(HTML, JavaScript, CSS, 이미지)를 포함하는 하위 디렉터리에 대한 상대 경로. Platform은 웹 서버에서 이 디렉터리를 호스팅하고 이 디렉터리에서 iframe 컨텐츠를 로드합니다. 필수 필드이므로 슬래시로 시작하지 않아야 합니다. 예를 들어, 모든 보기가 `src/view/`에 포함된 경우 `viewBasePath`의 값은 `src/view/`가 됩니다. |
| `hostedLibFiles` *(선택 사항)* | 대부분의 Adobe 사용자는 자체 서버에서 모든 태그 관련 파일을 호스팅하기를 선호합니다. 이를 통해 런타임 시 파일 가용성에 대한 확실성 수준을 높이고, 보안 취약점에 대한 코드를 쉽게 스캔할 수 있습니다. 확장의 라이브러리 부분이 런타임에 JavaScript 파일을 로드해야 하는 경우 이 속성을 사용하여 해당 파일을 나열하는 것이 좋습니다. 나열된 파일은 태그 런타임 라이브러리와 함께 호스팅됩니다. 그런 다음 [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file) 메서드를 사용하여 검색한 URL을 통해 파일을 로드할 수 있습니다.<br><br>이 옵션에는 호스팅해야 하는 타사 라이브러리 파일의 상대 경로가 포함된 배열이 포함되어 있습니다. |
| `main` *(선택 사항)* | 런타임에 실행해야 하는 라이브러리 모듈의 상대 경로입니다.<br><br>이 모듈은 항상 런타임 라이브러리에 포함되고 실행됩니다. 이 모듈은 항상 런타임 라이브러리에 포함되므로, 반드시 필요한 경우 &quot;기본&quot; 모듈만 사용하고 코드 크기를 최소한으로 유지하는 것이 좋습니다.<br><br>이 모듈은 먼저 실행되지 않을 수 있으며, 다른 모듈이 먼저 실행될 수 있습니다. |
| `configuration` *(선택 사항)* | 이와 관련해서는 확장의 [확장 구성](./configuration.md) 부분에 대해 설명합니다. 사용자가 확장에 대한 전역 설정을 제공해야 하는 경우 필요합니다. 이 필드의 구조를 구성하는 방법에 대한 자세한 내용은 [부록](#config-object)을 참조하십시오. |
| `events` *(선택 사항)* | [이벤트](./web/event-types.md) 유형 정의의 배열입니다. 배열에 있는 각 객체의 구조를 보려면 부록 섹션에서 [유형 정의](#type-definitions)를 참조하십시오. |
| `conditions` *(선택 사항)* | [조건](./web/condition-types.md) 유형 정의의 배열입니다. 배열에 있는 각 객체의 구조에 대한 [유형 정의](#type-definitions)에 대한 부록 섹션을 참조하십시오. |
| `actions` *(선택 사항)* | [작업](./web/action-types.md) 유형 정의 배열입니다. 배열에 있는 각 객체의 구조에 대한 [유형 정의](#type-definitions)에 대한 부록 섹션을 참조하십시오. |
| `dataElements` *(선택 사항)* | [데이터 요소](./web/data-element-types.md) 유형 정의의 배열입니다. 배열에 있는 각 객체의 구조에 대한 [유형 정의](#type-definitions)에 대한 부록 섹션을 참조하십시오. |
| `sharedModules` *(선택 사항)* | 공유 모듈 정의 객체의 배열입니다. 배열의 각 공유 모듈 객체는 다음과 같이 구조화해야 합니다. <ul><li>`name`: 공유 모듈의 이름입니다. 이 이름은 [공유 모듈](./web/shared.md)에 설명된 대로 다른 확장의 공유 모듈을 참조할 때 사용됩니다. 이 이름은 사용자 인터페이스에 표시되지 않습니다. 확장 내의 다른 공유 모듈 이름에서 고유해야 하며 [명명 규칙](#naming-rules)을 준수해야 합니다. **이 이름은 태그에서 식별자로 사용되며 확장을 게시한 후에는 변경할 수 없습니다.**</li><li>`libPath`: 공유 모듈의 상대 경로입니다. 슬래시로 시작하지 않아야 합니다. `.js` 확장이 있는 JavaScript 파일을 참조해야 합니다.</li></ul> |

## 부록

### 명명 규칙 {#naming-rules}

`extension.json`에서 모든 `name` 필드의 값은 다음 규칙을 준수해야 합니다.

* 214자 이하여야 합니다.
* 점 또는 밑줄로 시작할 수 없습니다.
* 대문자를 포함하지 않아야 합니다.
* URL 안전 문자만 포함해야 합니다.

이는 [npm 패키지 이름](https://docs.npmjs.com/files/package.json#name) 규칙과 일치합니다.

### 구성 객체 속성 {#config-object}

구성 객체는 다음과 같이 구조화해야 합니다.

<table>
  <thead>
    <tr>
      <th>속성</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>viewPath</code></td>
      <td>확장 구성 보기에 대한 상대 URL입니다. 이 값은 <code>viewBasePath</code>에 상대적이어야 하며 슬래시로 시작하지 않아야 합니다. 확장자가 <code>.html</code>인 HTML 파일을 참조해야 합니다. 쿼리 문자열 및 조각 식별자(해시) 접미사를 사용할 수 있습니다.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>확장 구성 보기에서 저장되는 유효한 객체의 형식을 설명하는 <a href="https://json-schema.org/">JSON 스키마</a> 객체입니다. 저장된 설정 객체가 이 스키마와 일치하도록 하는 것은 구성 보기 개발자의 책임입니다. 이 스키마는 사용자가 Platform 서비스를 사용하여 데이터를 저장하려고 할 때도 유효성 검사에서 사용됩니다.<br><br>예제 스키마 객체는 다음과 같습니다.
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      <a href="https://www.jsonschemavalidator.net/">JSON 스키마 유효성 검사기</a>와 같은 툴을 사용하여 스키마를 수동으로 테스트하는 것이 좋습니다.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(선택 사항)</em></td>
      <td>객체 배열로서, 각 객체는 런타임 라이브러리로 내보낼 때 모든 해당 설정 객체에서 수행해야 하는 변형을 나타냅니다. 이 배열이 필요한 이유와 그 사용 방법에 대한 자세한 내용은 <a href="#transforms">변형</a> 섹션을 참조하십시오.</td>
    </tr>
  </tbody>
</table>

### 유형 정의 {#type-definitions}

유형 정의는 이벤트, 조건, 작업 또는 데이터 요소 유형을 설명하는 데 사용되는 객체입니다. 객체는 다음과 같이 구성됩니다.

<table>
  <thead>
    <tr>
      <th>속성</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>유형의 이름입니다. 확장 내에서 이름은 고유해야 합니다. 이름은 <a href="#naming-rules">명명 규칙</a>을 준수해야 합니다. <strong>이 이름은 태그에서 식별자로 사용되며 확장을 게시한 후에는 변경할 수 없습니다.</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>데이터 수집 사용자 인터페이스 내에서 유형을 나타내는 데 사용할 텍스트입니다. 사람이 읽을 수 있어야 합니다.</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(선택 사항)</em></td>
      <td>제공되면,  UI의 <code>categoryName</code> 아래에 <code>displayName</code>이 나열됩니다. <code>categoryName</code>이 동일한 모든 유형은 동일한 카테고리에 나열됩니다. 예를 들어, 확장에서 <code>keyUp</code> 이벤트 유형 및 <code>keyDown</code> 이벤트 유형을 제공했는데 둘 다 <code>Keyboard</code>의 <code>categoryName</code> 이벤트 유형이 있는 경우, 사용자가 규칙을 작성할 때 사용 가능한 이벤트 유형 목록에서 선택하는 동안 두 이벤트 유형이 키보드 범주 아래에 나열됩니다. <code>categoryName</code>의 값은 사람이 읽을 수 있어야 합니다.</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>유형의 라이브러리 모듈에 대한 상대 경로입니다. 슬래시로 시작하지 않아야 합니다. <code>.js</code> 확장이 있는 JavaScript 파일을 참조해야 합니다.</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(선택 사항)</em></td>
      <td>유형 보기에 대한 상대 URL입니다. 이 값은 <code>viewBasePath</code>에 상대적이어야 하며 슬래시로 시작하지 않아야 합니다. 확장자가 <code>.html</code>인 HTML 파일을 참조해야 합니다. 쿼리 문자열 및 조각 식별자(해시)는 사용할 수 있습니다. 유형의 라이브러리 모듈에서 사용자의 설정을 사용하지 않는 경우 이 속성을 제외시킬 수 있습니다. 대신, Platform에 구성이 필요하지 않다는 자리 표시자가 표시됩니다.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>사용자가 저장할 수 있는 유효한 설정 객체의 형식을 설명하는 <a href="https://json-schema.org/">JSON 스키마</a> 객체입니다. 설정은 일반적으로 데이터 수집 사용자 인터페이스를 사용하여 사용자가 구성 및 저장합니다. 이러한 경우 확장의 보기에서 사용자가 제공한 설정을 확인하는 데 필요한 단계를 수행할 수 있습니다. 반면, 일부 사용자는 사용자 인터페이스의 지원 없이 직접 태그 API를 사용하도록 선택할 수 있습니다. 이 스키마의 목적은 사용자 인터페이스가 사용되는지의 여부와 관계없이 Platform이 사용자가 저장한 설정 객체가 런타임 시 설정 객체에 적용되는 라이브러리 모듈과 호환되는 형식으로 되어 있는지 확인하기 위한 것입니다.<br><br>예제 스키마 객체는 다음과 같습니다.<br>
<pre class="JSON language-JSON hljs">
{ "$schema": "http://json-schema.org/draft-04/schema#", "type": "object", "properties": { "delay": { "type": "number", "minimum": 1 }, "필수": [ "delay" ], "additionalProperties": false }
</pre>
      <a href="https://www.jsonschemavalidator.net/">JSON 스키마 유효성 검사기</a>와 같은 툴을 사용하여 스키마를 수동으로 테스트하는 것이 좋습니다.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(선택 사항)</em></td>
      <td>객체 배열로서, 각 객체는 런타임 라이브러리로 내보낼 때 모든 해당 설정 객체에서 수행해야 하는 변형을 나타냅니다. 이 배열이 필요한 이유와 사용 방법에 대한 자세한 내용은 <a href="#transforms">변형</a> 섹션을 참조하십시오.</td>
    </tr>
  </tbody>
</table>

### 변형 {#transforms}

특정 사용 사례의 경우 확장은 보기에서 저장한 설정 객체가 태그 런타임 라이브러리로 전송되기 전에 Platform으로 변형되어야 합니다. `extension.json` 내에서 유형 정의를 정의할 때 `transforms` 속성을 설정하여 이러한 변형 중 하나 이상을 수행하도록 요청할 수 있습니다. `transforms` 속성은 각 객체가 수행해야 하는 변형을 나타내는 객체의 배열입니다.

모든 변환에서는 `type` 및 `propertyPath`가 필요합니다. 다음 `type` 다음 중 하나여야 합니다. `function`, `remove`, 및 `file` 및 은 Platform이 설정 객체에 적용할 변형에 대해 설명합니다. 다음 `propertyPath` 는 설정 객체에서 수정해야 하는 속성을 찾을 위치를 태그에 알려주는 마침표로 구분되는 문자열입니다. 다음은 설정 객체 및 일부 `propertyPath`의 예입니다.

```js
{
  foo: {
    bar: "A string",
    baz: [
      "A",
      "B",
      "C"
    ]
  }
}
```

* `foo.bar`의 `propertyPath`를 설정하면 `"A string"` 값이 변형됩니다.
* `foo.baz[]`의 `propertyPath`를 설정하면 `baz` 배열의 각 값이 변형됩니다.
* `foo.baz`의 `propertyPath`를 설정하면 `baz` 배열이 변형됩니다.

속성 경로는 배열과 객체 표기법의 조합을 사용하여 설정 객체의 모든 수준에서 변형을 적용할 수 있습니다.

>[!WARNING]
>
>`propertyPath` 특성(예: `foo.baz[]`)은 아직 확장 샌드박스*툴에서 지원되지 않습니다.

아래 섹션에서는 사용 가능한 변형과 변형을 사용하는 방법에 대해 설명합니다.

#### 함수 변형

함수 변형을 사용하면 Platform 사용자가 작성한 코드를 내보낸 태그 런타임 라이브러리 내의 라이브러리 모듈에서 실행할 수 있습니다.

사용자 정의 스크립트 작업 유형을 제공한다고 가정해 보겠습니다. 사용자 정의 스크립트 작업 보기는 사용자가 일부 코드를 입력할 수 있는 텍스트 영역을 제공할 수 있습니다. 사용자가 텍스트 영역에 다음 코드를 입력했다고 가정해 보겠습니다.

`console.log('Welcome, ' + username +'. This is ZomboCom.');`

사용자가 규칙을 저장할 때, 보기에 의해 저장된 설정 객체는 다음과 같이 표시될 수 있습니다.

```javascript
{
  foo: {
    bar: "console.log('Welcome, ' + username +'. This is ZomboCom.');"
  }
}
```

작업을 사용하는 규칙이 태그 런타임 라이브러리 내에서 실행되면 사용자 코드를 실행하고 사용자 이름을 전달합니다.

설정 객체가 작업 유형의 보기에서 저장될 때 사용자의 코드는 단순한 문자열입니다. 이는 JSON에서 제공되고 올바르게 직렬화할 수 있으므로 좋습니다. 하지만 일반적으로 실행 가능한 함수 대신 문자열로 태그 런타임 라이브러리로 내보내지기 때문에 나쁜 점도 있습니다. 작업 유형의 라이브러리 모듈 내에서 [`eval`](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/eval) 또는 [함수 생성자](https://developer.mozilla.org/ko-KR/docs/Web/JavaScript/Reference/Global_Objects/Function)를 사용하여 코드 실행을 시도할 수 있지만 [컨텐츠 보안 정책](https://developer.mozilla.org/en-US/docs/Web/Security/CSP)으로 인해 실행이 차단될 수 있습니다.

이러한 상황에 대한 해결 방법으로, 함수 변형을 사용하면 태그 런타임 라이브러리에서 내보낼 때 Platform에 실행 가능한 함수에서 사용자 코드를 래핑하라고 알립니다. 예제 문제를 해결하기 위해 다음과 같이 `extension.json`의 유형 정의에 변형을 정의합니다.

```json
{
  "transforms": [
    {
      "type": "function",
      "propertyPath": "foo.bar",
      "parameters": ["username"]
    }
  ]
}
```

* `type`은 설정 객체에 적용할 변형의 유형을 정의합니다.
* `propertyPath` 는 설정 객체에서 수정해야 하는 속성을 찾을 어디에서 찾을 수 있는지 Platform에 알려주는 마침표로 구분되는 문자열입니다.
* `parameters`는 래핑 함수의 서명에 포함되어야 하는 매개 변수 이름의 배열입니다.

설정 객체가 태그 런타임 라이브러리에 전송되면 다음과 같이 변환됩니다.

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

라이브러리 모듈은 사용자 코드가 포함된 함수를 호출하고 `username` 인수를 전달할 수 있습니다.

#### 파일 변형

파일 변형을 사용하면 Platform 사용자가 작성한 코드를 태그 런타임 라이브러리와 별도의 파일로 내보낼 수 있습니다. 파일은 태그 런타임 라이브러리와 함께 호스팅되며 런타임 시 확장에 필요할 때 로드할 수 있습니다.

사용자 정의 스크립트 작업 유형을 제공한다고 가정해 보겠습니다. 작업 유형의 보기에서는 사용자가 일부 코드를 입력할 수 있는 텍스트 영역을 제공할 수 있습니다. 사용자가 텍스트 영역에 다음 코드를 입력했다고 가정해 보겠습니다.

`console.log('This is ZomboCom.');`

사용자가 규칙을 저장할 때, 보기에 의해 저장된 설정 객체는 다음과 같이 표시될 수 있습니다.

```js
{
  foo: {
    bar: "console.log('This is ZomboCom.');"
  }
}
```

사용자의 코드를 태그 런타임 라이브러리에 포함되지 않고 별도의 파일에 삽입하려고 합니다. 작업을 사용하는 규칙이 태그 런타임 라이브러리 내에서 실행되면 문서 본문에 스크립트 요소를 추가하여 사용자 코드를 로드하려고 합니다. 예제 문제를 해결하기 위해 다음과 같이 `extension.json`의 작업 유형 정의에 변형을 정의합니다.

```json
{
  "transforms": [
    {
      "type": "file",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type`은 설정 객체에 적용할 변형의 유형을 정의합니다.
* `propertyPath` 는 설정 객체에서 수정해야 하는 속성을 찾을 어디에서 찾을 수 있는지 Platform에 알려주는 마침표로 구분되는 문자열입니다.

설정 객체가 태그 런타임 라이브러리에 전송되면 다음과 같이 변환됩니다.

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

이 경우 `foo.bar`의 값이 URL로 변형되었습니다. 정확한 URL은 라이브러리가 빌드될 때 결정됩니다. 파일에는 항상 `.js` 확장자가 지정되며 JavaScript 기반 MIME 유형을 사용하여 배달됩니다. 나중에 다른 MIME 유형에 대한 지원을 추가할 수 있습니다.

#### 변형 제거

기본적으로 설정 객체의 모든 속성이 태그 런타임 라이브러리에 표시됩니다. 특정 속성이 확장 보기에만 사용되는 경우, 특히 중요한 정보(예: 비밀 토큰)가 포함된 경우에는 변환 제거를 사용하여 정보가 태그 런타임 라이브러리로 전송되지 않도록 해야 합니다.

새로운 작업 유형을 제공한다고 가정해 보겠습니다. 작업 유형의 보기에서는 사용자가 특정 API에 대한 연결을 허용하는 비밀 키를 입력할 수 있는 입력을 제공할 수 있습니다. 사용자가 입력에 다음 텍스트를 입력했다고 가정해 보겠습니다.

`ABCDEFG`

사용자가 규칙을 저장할 때, 보기에 의해 저장된 설정 객체는 다음과 같이 표시될 수 있습니다.

```js
{
  foo: {
    bar: "ABCDEFG"
  }
}
```

우리는 그 속성을 포함하지 않기를 원합니다 `bar` 를 반환합니다. 예제 문제를 해결하기 위해 다음과 같이 `extension.json`의 작업 유형 정의에 변형을 정의합니다.

```json
{
  "transforms": [
    {
      "type": "remove",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type`은 설정 객체에 적용할 변형의 유형을 정의합니다.
* `propertyPath` 는 설정 객체에서 수정해야 하는 속성을 찾을 어디에서 찾을 수 있는지 Platform에 알려주는 마침표로 구분되는 문자열입니다.

설정 객체가 태그 런타임 라이브러리에 전송되면 다음과 같이 변환됩니다.

```js
{
  foo: {
  }
}
```

이 경우 `foo.bar`의 값이 설정 객체에서 제거되었습니다.
