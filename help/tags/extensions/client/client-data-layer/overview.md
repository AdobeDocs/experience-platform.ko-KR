---
title: Adobe 클라이언트 데이터 레이어 확장
description: Adobe Experience Platform의 Adobe 클라이언트 데이터 레이어 태그 확장에 대해 알아봅니다.
exl-id: c4d1b4d3-4b51-4701-be2e-31b08e109bf6
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Adobe 클라이언트 데이터 레이어 확장

이 설명서는 Adobe 클라이언트 데이터 레이어 확장을 사용하는 방법에 대한 예제와 모범 사례를 제공합니다.

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## 설치

확장을 설치하려면 Experience Platform UI 또는 데이터 수집 UI에서 확장 카탈로그로 이동하고 클라이언트 데이터 레이어 Adobe 를 선택합니다.

![카탈로그의 ACDL 확장 보기](./images/catalog.png)

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## 확장 보기

기본적으로 ACDL 스크립트는 변수 이름으로 새 데이터 레이어를 만듭니다 `adobeDataLayer`. 확장 보기는 원하는 경우 이 이름을 변경할 수 있는 기능을 제공합니다. 설정한 이름은 태그가 로드될 때 인스턴스화됩니다.

>[!NOTE]
>
>개체 이름을 변경할 때 원본 `adobeDataLayer` 개체가 여전히 인스턴스화되고 있으며 선택한 새 변수 이름으로 복제되고 있습니다.

## 이벤트

확장은 데이터 레이어에서 이벤트를 수신할 수 있는 기능을 제공합니다. 다음 이벤트를 사용할 수 있습니다.

### 모든 데이터 변경 사항 수신

이 옵션을 선택하면 이벤트 리스너가 데이터 계층에 대한 모든 변경 사항을 수신합니다.

>[!IMPORTANT]
>
>이벤트를 푸시해도 데이터 레이어 자체는 변경되지 않습니다.

다음 예제 푸시 이벤트는 리스너에 의해 추적됩니다.

* ` adobeDataLayer.push({"data":"something"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

다음 예제 푸시 이벤트는 리스너에 의해 추적되지 않습니다.

* ` adobeDataLayer.push({"event":"myevent"})`

### 모든 이벤트 수신

이 옵션을 선택하면 이벤트 리스너가 데이터 레이어로 푸시된 이벤트를 수신합니다.

다음 예제 푸시 이벤트는 리스너에 의해 추적됩니다.

* ` adobeDataLayer.push({"event":"myevent"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

다음 예제 푸시 이벤트는 리스너에 의해 추적되지 않습니다.

* ` adobeDataLayer.push({"data":"something"}) `

### 특정 이벤트 수신

이벤트를 지정하는 경우 이벤트 리스너는 특정 문자열과 일치하는 모든 이벤트를 추적합니다.

예, 설정 `myEvent` 이 구성을 사용하면 리스너가 다음 푸시 이벤트만 추적합니다.

* `adobeDataLayer.push({"event":"myEvent"})`

이벤트 리스너의 범위를 변경할 수도 있습니다. 다른 옵션은 아래에 요약되어 있습니다.

* `all`: 이 옵션은 기본 옵션이며, 위에서 선택한 조건이 과거에 충족되거나 나중에 푸시될 때마다 규칙을 트리거합니다. 비동기 구현을 사용하는 경우 이 옵션이 가장 안전합니다.
* `future`: 이 옵션은 조건과 일치하는 새 푸시 이벤트가 데이터 레이어로 전송될 때만 규칙을 트리거합니다.
* `past`: 이 옵션은 조건과 일치하는 이전 푸시 이벤트에 대해서만 규칙을 트리거합니다. 조건에 일치하는 새 푸시는 무시되며 더 이상 규칙을 트리거하지 않습니다.

## 작업

다음 섹션에서는 확장에서 지원하는 작업에 대해 간략히 설명합니다.

### 데이터 레이어 재설정

확장은 데이터 레이어 길이를 재설정하는 방법을 제공하여 단일 페이지 애플리케이션(SPA)의 제한된 크기를 유지하는 데 도움이 됩니다.

그러나 현재 푸시 방법 중에 이전에 설정한 정보를 완전히 제거할 가능성은 없습니다.

다음 **계산된 상태 재설정 및 설정** 작업은 마지막 계산된 상태를 복사하고 데이터 레이어 개체를 비운 다음 마지막 상태를 다시 푸시합니다.

### 데이터 레이어로 푸시

확장은 JSON 콘텐츠를 데이터 레이어 자체에 푸시하는 작업을 제공합니다. 이 작업을 통해 JSON에서 직접 데이터 요소를 사용할 수 있습니다. JSON 편집기 내에서 퍼센트 표기법을 사용하여 데이터 요소를 참조해야 합니다(예: `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

## 데이터 요소

아래 섹션에서는 확장에서 제공하는 고유한 데이터 요소 유형을 다룹니다.

### 계산된 상태

데이터 레이어 계산된 상태 데이터 요소는 구성 방법에 따라 다음 두 가지 중 하나를 반환할 수 있습니다.

* 전체 데이터 계층 상태: 기본적으로 전체 데이터 계층 계산됨 상태가 반환됩니다.
* 특정 경로: 데이터 레이어에서 반환할 경로를 지정할 수 있습니다. 경로는 점 표기법을 사용하여 지정됩니다(예: `data.foo`).

### 데이터 레이어 크기

이 데이터 요소는 데이터 레이어의 크기를 반환합니다. 데이터 레이어의 크기는 이 개체에 푸시된 요소의 수로 표시됩니다.

다음 푸시 이벤트 목록이 주어지면 이 데이터 요소는 정수를 반환합니다 `2`:

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
