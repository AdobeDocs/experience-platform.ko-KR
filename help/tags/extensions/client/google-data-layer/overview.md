---
title: Google 데이터 레이어 확장
description: Adobe Experience Platform의 Google 클라이언트 데이터 레이어 태그 확장에 대해 알아봅니다.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Google 데이터 레이어 확장(베타)

>[!IMPORTANT]
>
>이 확장은 현재 베타 버전이며 프로덕션에서 완전히 테스트되지 않았습니다.

Google 데이터 레이어 확장을 사용하면 태그 구현에서 Google 데이터 레이어를 사용할 수 있습니다. 확장은 Google 솔루션 및 Google의 오픈 소스와 독립적으로 또는 동시에 사용할 수 있습니다 [데이터 레이어 도우미 라이브러리](https://github.com/google/data-layer-helper).

도우미 라이브러리는 ACDL(Adobe 클라이언트 데이터 날짜)과 유사한 이벤트 기반 기능을 제공합니다. Google 데이터 레이어 확장의 데이터 요소, 규칙 및 작업은 의 데이터 요소와 유사한 기능을 제공합니다 [ACDL 확장](../client-data-layer/overview.md).

## 성숙도

확장 버전 1.0.x는 베타입니다. 이 확장은 프로덕션에서 완전히 테스트되지 않았습니다.

## 설치

확장을 설치하려면 Experience Platform UI 또는 데이터 수집 UI에서 확장 카탈로그로 이동하고 을 선택합니다 **Google 데이터 레이어**.

설치하면 확장은 태그 라이브러리가 웹 사이트에 로드될 때마다 데이터 레이어를 만들거나 액세스합니다.

## 확장 보기

확장을 구성할 때(확장을 설치하는 동안 또는 를 선택하여) **[!UICONTROL 구성]** 확장 카탈로그에서)는 확장이 사용하는 데이터 레이어의 이름을 정의해야 합니다. 라이브러리를 로드할 때 구성된 이름의 데이터 레이어가 없으면 확장이 대신 하나를 만듭니다.

>[!NOTE]
>
>Google 또는 Adobe 코드가 먼저 로드되고 데이터 레이어를 만들는지는 중요하지 않습니다. 두 시스템 모두 존재하지 않을 경우 데이터 레이어를 만들거나 기존 데이터 레이어를 사용합니다.

기본적으로 데이터 계층은 Google 기본 이름을 사용합니다 `dataLayer`.

## 이벤트

확장을 사용하면 데이터 레이어 내에서 변경 사항(이벤트)을 수신할 수 있습니다. 이벤트는 다음 중 하나일 수 있습니다.

* 이벤트 태그 지정(예: 로드되는 라이브러리)
* JavaScript 이벤트
* 를 사용하여 데이터 레이어에 푸시된 데이터 `event` 키워드.

의 사용을 이해하는 것이 중요합니다 [`event` 키워드](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) 데이터가 Google 데이터 계층에 푸시되면 Adobe 클라이언트 데이터 레이어와 비슷합니다. 다음 `event` 키워드는 Google 데이터 레이어의 동작을 변경하므로 확장의 동작이 그에 따라 업데이트됩니다.

아래 섹션에서는 확장이 수신할 수 있는 다양한 이벤트 유형을 간략하게 설명합니다.

### 데이터 레이어를 푸시할 때 모두 수신

이 옵션을 선택하면 확장에서 데이터 레이어의 변경 사항을 수신합니다.

### 제외 이벤트 푸시를 수신

이 옵션을 선택하면 확장은 이벤트를 제외하고 데이터 레이어에 푸시되는 모든 내용을 수신합니다.

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

이 옵션을 선택하면 확장은 데이터 레이어로 푸시된 모든 이벤트를 수신합니다.

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

특정 이벤트를 수신하려면 이벤트 리스너가 특정 문자열과 일치하는 이벤트를 추적하도록 이 옵션을 선택합니다.

예를 들어, `myEvent` 이 구성을 사용하는 경우 리스너는 다음 푸시 이벤트만 추적합니다.

```js
dataLayer.push({"event":"myEvent"})
```

정규 표현식 문자열을 사용하여 이벤트 이름과 일치시킬 수도 있습니다. 예를 들어, `myEvent\d` 으로 시작하는 이벤트를 추적합니다. `myEvent` 뒤에 숫자가 옵니다.

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 작업

아래 섹션에서는 [규칙](../../../ui/managing-resources/rules.md).

### 데이터 계층에 푸시 {#push-to-data-layer}

이 작업은 JSON 컨텐츠를 데이터 계층 자체에 푸시하므로 JSON 페이로드에서 직접 데이터 요소를 사용할 수 있습니다. 제공된 JSON 편집기 내에서 퍼센트 표기법을 사용하여 데이터 요소를 참조할 수 있습니다(예: `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Google DL이 계산된 상태로 다시 설정

>[!NOTE]
>
>이 작업은 v1.0.5 이후에 사용할 수 있습니다.

이 작업으로 데이터 레이어가 재설정됩니다. Google 데이터 레이어 변경 사항을 처리하는 규칙에 사용하는 경우 데이터 계층은 규칙이 트리거될 당시 데이터 레이어의 계산된 상태로 재설정됩니다. Google 데이터 레이어 변경 사항을 처리하지 않는 규칙에 작업이 사용되는 경우 해당 작업에 데이터 레이어가 비어 있게 됩니다.

## 데이터 요소

확장은 키를 사용하여 데이터 계층에 액세스하는 고유한 데이터 요소를 제공합니다(예: `page.url` 에서 [위의 코드](#push-to-data-layer)).

데이터 요소는 다음 중 하나를 제공할 수 있습니다.

* 데이터 레이어의 특정 값(예: `page.url`)
* 전체 데이터 레이어 배열(빈 키 필드)
* 키를 사용하여 데이터 레이어 이벤트의 값( `event` 키워드 사용)
* 전체 이벤트 개체(빈 키 필드)

확장은 항상 이벤트 정보에 우선 순위를 제공합니다. 데이터 레이어인 경우 `event` 가 처리되는 경우 값이 항상 해당 이벤트에서 읽됩니다. 다음과 같은 경우 `event` 이 없으면 직접 데이터 레이어에서 값을 대신 읽습니다.

## 추가 정보

추가 정보는 [프로젝트 추가 정보](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) 및 를 사용하도록 선택할 수 있습니다.
