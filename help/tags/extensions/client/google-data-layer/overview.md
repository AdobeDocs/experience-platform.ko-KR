---
title: Google 데이터 레이어 확장
description: Adobe Experience Platform의 Google 클라이언트 데이터 레이어 태그 확장에 대해 알아봅니다.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: c61afdc2c3df98a0ef815d7cb034ba2907c52908
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# Google 데이터 레이어 확장

Google 데이터 레이어 확장을 사용하면 Tags 구현에서 Google 데이터 레이어를 사용할 수 있습니다. 확장 프로그램은 Google 솔루션 및 Google의 오픈 소스 [데이터 레이어 도우미 라이브러리](https://github.com/google/data-layer-helper)와 함께 독립적으로 또는 동시에 사용할 수 있습니다.

도우미 라이브러리는 ACDL(Adobe 클라이언트 데이터 레이어)에 유사한 이벤트 기반 기능을 제공합니다. Google 데이터 레이어 확장의 데이터 요소, 규칙 및 작업은 [ACDL 확장](../client-data-layer/overview.md)의 기능과 유사한 기능을 제공합니다.

## 설치

확장을 설치하려면 데이터 수집 UI에서 확장 카탈로그로 이동하고 **[!UICONTROL Google 데이터 레이어]**&#x200B;를 선택합니다.

확장이 설치되면 Adobe Experience Platform 태그 라이브러리의 모든 로드에서 데이터 레이어를 만들거나 해당 데이터 레이어에 액세스합니다.

## 확장 보기

확장 구성을 사용하여 확장에서 사용하는 데이터 계층의 이름을 정의할 수 있습니다. Adobe Experience Platform Tags가 로드될 때 구성된 이름의 데이터 레이어가 없으면 확장에서 만듭니다.

데이터 레이어 이름 기본값은 Google 기본 이름 `dataLayer`입니다.

>[!NOTE]
>
>Google 또는 Adobe 코드가 먼저 로드되고 데이터 레이어를 생성하는지 여부는 중요하지 않습니다. 두 시스템은 동일하게 동작합니다. 데이터 레이어가 없는 경우 만들거나 기존 데이터 레이어를 사용합니다.

## 이벤트

>[!NOTE]
>
>Adobe Experience Platform Tags에서 이벤트 기반 데이터 레이어를 사용할 때 _event_ 단어가 오버로드됩니다. _이벤트_&#x200B;은(는) 다음과 같을 수 있습니다.
> - Adobe Experience Platform 태그 이벤트(라이브러리가 로드됨 등).
> - JavaScript 이벤트.
> - _event_ 키워드를 사용하여 데이터 레이어로 푸시된 데이터입니다.

확장은 데이터 레이어에서 변경 사항을 수신 대기할 수 있는 기능을 제공합니다.

>[!NOTE]
>
>Adobe 클라이언트 데이터 레이어와 마찬가지로 Google 데이터 레이어에 데이터를 푸시할 때 _event_ 키워드의 사용을 이해하는 것이 중요합니다. _event_ 키워드는 Google 데이터 계층의 동작을 변경하므로 이 확장을 변경합니다.\
> 이 점에 대해 잘 모르는 경우 Google 설명서를 읽어보거나 조사를 수행하십시오.

### Google 이벤트 유형

Google에서는 `push()` 메서드를 사용하는 Google Tag Manager와 `gtag()` 메서드를 사용하는 Google Analytics 4의 두 가지 푸시 이벤트 수단을 지원합니다.

1.2.1 이전의 Google 데이터 레이어 확장 버전은 이 페이지의 코드 예제와 같이 `push()`에서 만든 이벤트만 지원합니다.

버전 1.2.1 이상에서는 `gtag()`을(를) 사용하여 만든 이벤트를 지원합니다.  이 옵션은 선택 사항이며 확장 구성 대화 상자에서 활성화할 수 있습니다.

`push()` 및 `gtag()` 이벤트에 대한 자세한 내용은 [Google 설명서](https://developers.google.com/analytics/devguides/collection/ga4/reference/events?client_type=gtag)를 참조하세요.  확장 기능의 구성 및 규칙 대화 상자에도 정보가 제공됩니다.

### 데이터 레이어의 모든 푸시를 수신합니다.

이 옵션을 선택하면 이벤트 리스너가 데이터 계층에 대한 모든 변경 사항을 수신합니다.

### 이벤트를 제외한 푸시 수신

이 옵션을 선택하면 이벤트 리스너가 이벤트를 제외하고 데이터를 데이터 레이어로 푸시하는 것을 수신합니다.

다음 예제 푸시 이벤트는 리스너에 의해 추적됩니다.

```js
dataLayer.push({"data":"something"})
```

다음 예제 푸시 이벤트는 리스너에 의해 추적되지 않습니다.

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### 모든 이벤트 수신

이 옵션을 선택하면 이벤트 리스너가 데이터 레이어로 푸시된 이벤트를 수신합니다.

다음 예제 푸시 이벤트는 리스너에 의해 추적됩니다.

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

다음 예제 푸시 이벤트는 리스너에 의해 추적되지 않습니다.

```js
dataLayer.push({"data":"something"})
```

### 특정 이벤트 수신

이벤트를 지정하는 경우 이벤트 리스너는 특정 문자열과 일치하는 모든 이벤트를 추적합니다.

예를 들어 이 구성을 사용할 때 `myEvent`을(를) 설정하면 리스너는 다음 푸시 이벤트만 추적합니다.

```js
dataLayer.push({"event":"myEvent"})
```

(ECMAScript / JavaScript) 정규 표현식을 사용하여 이벤트 이름을 일치시킬 수 있습니다.

예를 들어 &#39;myEvent\d&#39;를 설정하면 숫자(\d)로 `myEvent`이(가) 추적됩니다.

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 작업

### 데이터 레이어로 푸시 {#push-to-data-layer}

확장은 데이터 레이어에 JSON을 푸시하는 두 가지 작업을 제공합니다. 푸시할 JSON을 수동으로 만들 수 있는 자유 텍스트 필드와 버전 1.2.0부터 키-값 다중 필드 대화 상자입니다.

#### 자유 텍스트 JSON

자유 텍스트 작업을 통해 JSON에서 직접 데이터 요소를 사용할 수 있습니다. JSON 편집기 내에서 퍼센트 표기법을 사용하여 데이터 요소를 참조해야 합니다. 예: `%dataElementName%`.

```json
{
  "page": {
    "url": "%url%",
    "previous_url": "%previous_url%",
    "concatenated_values": "static string %dataElement%"
  }
}
```

#### 키-값 다중 필드

최신 키-값 다중 필드 대화 상자는 JSON을 수동으로 작성하지 않고도 푸시를 구성할 수 있는 보다 사용자 친화적인 인터페이스입니다.

### Google DL이 계산된 상태로 재설정

확장은 데이터 레이어를 재설정하는 작업을 제공합니다. Google 데이터 레이어 변경을 처리하는 규칙에 사용되는 경우 데이터 레이어는 규칙이 트리거될 때 데이터 레이어의 계산된 상태로 재설정됩니다. Google 데이터 레이어 변경을 처리하지 않는 규칙에서 이 작업을 사용하면 이 작업은 데이터 레이어를 비웁니다.

## 데이터 요소

제공된 데이터 요소는 Google 데이터 계층 변경(푸시 이벤트)에 의해 트리거된 규칙을 실행하는 동안 또는 Library Loaded와 같은 관련 없는 규칙에서 사용할 수 있습니다. 전자의 경우, 데이터 요소는 데이터 계층 변경 시 계산된 상태에서 가져온 값을 반환합니다. 후자의 경우 규칙 실행 시 계산된 상태가 사용됩니다.

토글 스위치를 사용하면 데이터 요소가 전체 계산된 상태에서 값을 반환할지 또는 이벤트 정보(데이터 레이어 변경으로 트리거된 규칙에 사용되는 경우)에서만 값을 반환할지 여부를 선택할 수 있습니다.

따라서 데이터 요소는 다음을 반환할 수 있습니다.

- 빈 필드: 데이터 레이어 계산된 상태입니다.
- 키가 있는 필드(예: 위의 예에서 page.previous_url): 이벤트 개체 또는 계산된 상태에 있는 키의 값입니다.

## 추가 정보

확장의 데이터 요소 및 이벤트 대화 상자에는 자세한 사용 정보 및 예가 포함되어 있습니다.

추가 일반 정보는 [프로젝트 추가 정보](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)에 있습니다.
