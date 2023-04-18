---
title: Google 데이터 레이어 확장
description: Adobe Experience Platform의 Google 클라이언트 데이터 레이어 태그 확장에 대해 알아봅니다.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 9c608f69f6ba219f9cb4e938a77bd4838158d42c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# Google 데이터 레이어 확장

Google 데이터 레이어 확장을 사용하면 태그 구현에서 Google 데이터 레이어를 사용할 수 있습니다. 확장은 Google 솔루션 및 Google의 오픈 소스와 독립적으로 또는 동시에 사용할 수 있습니다 [데이터 레이어 도우미 라이브러리](https://github.com/google/data-layer-helper).

도우미 라이브러리는 ACDL(Adobe 클라이언트 데이터 날짜)과 유사한 이벤트 기반 기능을 제공합니다. Google 데이터 레이어 확장의 데이터 요소, 규칙 및 작업은 의 데이터 요소와 유사한 기능을 제공합니다 [ACDL 확장](../client-data-layer/overview.md).

## 성숙도

버전 1.2.x는 프로덕션 사용 중인 최신 베타입니다.

## 설치

확장을 설치하려면 데이터 수집 UI에서 확장 카탈로그로 이동하고 을 선택합니다 **[!UICONTROL Google 데이터 레이어]**.

설치되면 확장은 Adobe Experience Platform 태그 라이브러리를 로드할 때마다 데이터 레이어를 만들거나 액세스합니다.

## 확장 보기

확장 구성을 사용하여 확장에서 사용하는 데이터 레이어의 이름을 정의할 수 있습니다. Adobe Experience Platform 태그가 로드될 때 구성된 이름의 데이터 레이어가 없으면 확장이 만들어집니다.

데이터 레이어 이름의 기본값은 Google 기본 이름입니다 `dataLayer`.

>[!NOTE]
>
>Google 또는 Adobe 코드가 먼저 로드되고 데이터 레이어를 만들는지는 중요하지 않습니다. 두 시스템 모두 동일하게 동작합니다. 데이터 레이어가 없으면 해당 레이어를 만들거나 기존 데이터 레이어를 사용합니다.

## 이벤트

>[!NOTE]
>
>단어 _이벤트_ Adobe Experience Platform 태그에서 이벤트 기반 데이터 레이어를 사용하면 오버로드됩니다. _이벤트_ 다음을 수행할 수 있습니다.
> - Adobe Experience Platform은 이벤트(Library Loaded 등)에 태그를 지정합니다.
> - JavaScript 이벤트.
> - 를 사용하여 데이터 레이어에 푸시된 데이터 _이벤트_ 키워드.


확장은 데이터 레이어에서 변경 사항을 수신할 수 있는 가능성을 제공합니다.

>[!NOTE]
>
>의 사용을 이해하는 것이 중요합니다 _이벤트_ 키워드 데이터를 Google 데이터 레이어에 푸시할 때 Adobe 클라이언트 데이터 레이어와 비슷합니다. 다음 _이벤트_ 키워드는 Google 데이터 레이어의 동작을 변경하므로 이 확장 프로그램이 변경됩니다.\
> 이 점을 잘 모르는 경우 Google 설명서를 읽거나 연구를 수행하십시오.

### 데이터 레이어를 푸시할 때 모두 수신

이 옵션을 선택하면 이벤트 리스너가 데이터 레이어의 변경 내용을 수신합니다.

### 제외 이벤트 푸시를 수신

이 옵션을 선택하면 이벤트 리스너가 이벤트를 제외한 모든 데이터 푸시를 데이터 레이어로 수신합니다.

다음 푸시 이벤트 예는 리스너에 의해 추적됩니다.

```js
dataLayer.push({"data":"something"})
```

다음 푸시 이벤트 예는 리스너에 의해 추적되지 않습니다.

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### 모든 이벤트 수신

이 옵션을 선택하면 이벤트 리스너가 데이터 레이어로 푸시된 모든 이벤트를 수신합니다.

다음 푸시 이벤트 예는 리스너에 의해 추적됩니다.

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

다음 푸시 이벤트 예는 리스너에 의해 추적되지 않습니다.

```js
dataLayer.push({"data":"something"})
```

### 특정 이벤트 수신

이벤트를 지정하는 경우 이벤트 리스너는 특정 문자열과 일치하는 모든 이벤트를 추적합니다.

예를 들어, `myEvent` 이 구성을 사용하는 경우 리스너는 다음 푸시 이벤트만 추적합니다.

```js
dataLayer.push({"event":"myEvent"})
```

(ECMAScript/JavaScript) regex를 사용하여 이벤트 이름과 일치시킬 수 있습니다.

예를 들어 &#39;myEvent\d&#39;를 설정하면 `myEvent` 숫자(\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 작업

### 데이터 계층에 푸시 {#push-to-data-layer}

확장은 데이터 계층에 JSON을 푸시하기 위한 두 가지 작업을 제공합니다. 푸시할 JSON을 수동으로 만들기 위한 자유 텍스트 필드와 버전 1.2.0에서 키-값 multifield 대화 상자가 있습니다.

#### 자유 텍스트 JSON

자유 텍스트 작업을 사용하면 JSON에서 직접 데이터 요소를 사용할 수 있습니다. JSON 편집기 내에서 데이터 요소는 퍼센트 표기법을 사용하여 참조해야 합니다. 예: `%dataElementName%`.

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

#### 키-값 multifield

최신 키-값 multifield 대화 상자는 JSON을 수동으로 작성하지 않고도 푸시를 구성할 수 있는 사용자에게 친숙한 인터페이스입니다.

### Google DL이 계산된 상태로 다시 설정

확장은 데이터 레이어를 재설정하는 작업을 제공합니다. Google 데이터 레이어 변경 사항을 처리하는 규칙에 사용하는 경우 데이터 계층은 규칙이 트리거될 당시 데이터 레이어의 계산된 상태로 재설정됩니다. Google 데이터 레이어 변경 사항을 처리하지 않는 규칙에 작업이 사용되는 경우 해당 작업에 데이터 레이어가 비어 있게 됩니다.

## 데이터 요소

제공된 데이터 요소는 Google 데이터 레이어 변경(푸시 이벤트)에 의해 트리거되는 규칙을 실행하는 동안 또는 Library Loaded와 같은 관련 없는 규칙에서 사용할 수 있습니다. 앞의 경우 데이터 요소는 데이터 레이어가 변경될 때 계산된 상태에서 가져온 값을 반환합니다. 후자의 경우 규칙 실행 시 계산된 상태가 사용됩니다.

전환 스위치를 사용하면 데이터 요소가 전체 계산된 상태에서 값을 반환할지 또는 이벤트 정보에서만 반환할지(데이터 레이어 변경으로 트리거되는 규칙에 사용된 경우) 선택할 수 있습니다.

따라서 데이터 요소는 다음을 반환할 수 있습니다.

- 빈 필드: 데이터 레이어 계산 상태.
- 키가 있는 필드(예: 위의 예에서 page.previous_url): 이벤트 개체 또는 계산된 상태의 키 값입니다.

## 추가 정보

확장의 데이터 요소 및 이벤트 대화 상자에는 세부 사용 정보 및 예가 포함됩니다.

추가 일반 정보는 [프로젝트 추가 정보](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
