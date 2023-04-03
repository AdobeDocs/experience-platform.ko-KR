---
title: 유효성 검사 편집기 보기
description: 이 안내서에서는 Adobe Experience Platform Assurance의 유효성 검사 편집기 보기에 대한 정보를 자세히 설명합니다.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---


# 유효성 검사 편집기 보기

유효성 검사 편집기를 사용하면 Adobe Experience Platform Assurance 세션에서 이벤트의 유효성을 확인하기 위해 JavaScript 함수를 빠르고 쉽게 관리할 수 있습니다. 각 함수는 보증 세션에서 이벤트를 받습니다. 클라이언트 구성, 이벤트 조건, 테스트 및 사용 사례를 확인하는 함수를 작성할 수 있습니다.

## 유효성 검사 편집기 시작

후 [보증 설정](../tutorials/implement-assurance.md), **[!UICONTROL 홈]** 보기, 선택 **[!UICONTROL 유효성 검사 편집기]**.

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## 유효성 검사 함수 쓰기

이 기능을 사용하면 Adobe Experience Platform Assurance 세션에 대한 유효성 검사 기능을 만들거나, 편집하거나, 삭제할 수 있습니다.

1. 선택 **[!UICONTROL 새 유효성 검사 만들기]**.
2. 을(를) 입력합니다. **이름** 유효성 검사를 식별하려면 **카테고리** 그리고 **설명**.
3. 편집기에서 코드를 편집하여 보증 세션에 대한 이벤트의 유효성을 확인합니다.

함수 테스트가 완료되면 을 선택합니다. **[!UICONTROL 게시]** 유효성 검사를 저장합니다.

### 이벤트 정의

| 키 | 유형 | 설명 |
| :--- | :--- | :--- |
| `uuid` | 문자열 | 이벤트의 Universally Unique Identifier. |
| `timestamp` | 숫자 | 이벤트가 Assurance로 전송될 때 클라이언트의 타임스탬프입니다. |
| `eventNumber` | 숫자 | 이벤트가 전송된 시기를 정렬하는 데 사용됩니다. 이 키는 이벤트에 동일한 타임스탬프가 있을 때 유용합니다. |
| `vendor` | 문자열 | 역 도메인 이름 형식의 공급업체 식별 문자열(예: com.adobe.assurance). |
| `type` | 문자열 | 이벤트 유형을 나타내는 데 사용됩니다. |
| `payload` | 오브젝트 | 이벤트의 데이터를 정의하고 고유하고 일반적인 속성을 포함합니다. 일부 공통 속성은 다음과 같습니다 `ACPExtensionEventSource` 및 `ACPExtensionEventType`. |
| `annotations` | 어레이 | 주석 객체의 배열입니다. |

### 주석 정의

| 키 | 유형 | 설명 |
| :--- | :--- | :--- |
| `uuid` | 문자열 | 주석에 대한 Universally Unique Identifier. |
| `type` | 문자열 | 주석 유형을 나타내는 데 사용되며 일반적으로 플러그인 이름(예: analytics)입니다. |
| `payload` | 오브젝트 | 이벤트를 보완해야 하는 데이터를 정의합니다. Adobe Analytics의 경우 여기서 사후 처리 히트 데이터가 포함됩니다. |

### 유효성 검사 결과

유효성 검사 함수는 다음을 포함하는 개체를 반환해야 합니다.

| 키 | 유형 | 설명 |
| :--- | :--- | :--- |
| `message` | 문자열 | 요약 결과에 표시할 유효성 검사 메시지. |
| `events` | 어레이 | 일치하거나 일치하지 않는다고 보고되는 이벤트 uuid 배열입니다. |
| `links` | 어레이 | 일련의 `ValidationResultLink` 참조 설명서 및 기타 리소스에 대한 객체 `{( type: 'doc'|'product', url: String )}` |
| `result` | 문자열 | 이것은 유효성 검사 결과이며 열거된 문자열 중 하나가 됩니다. &quot;일치함&quot;, &quot;일치하지 않음&quot;, &quot;알 수 없음&quot; |

## 유효성 검사 결과 보기

함수 결과는 코드 편집기 아래의 결과 섹션에 표시됩니다. 유효성 검사 결과가 `unknown` 또는 `not matched` 그리고 `events` 배열에 하나 이상이 있음 `uuids`를 지정하면 이벤트가 다음 색상으로 타임라인에서 강조 표시됩니다.

* 녹색 - 일치함
* 주황 - 알 수 없음
* 빨간색 - 일치하지 않음

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## 문제 해결

추가할 수 있습니다 `console.log()` 개발자 콘솔에 항목을 인쇄하는 함수입니다. 또는 결과 개체의 message 속성을 사용하여 메시지를 결과 패널에 디버그할 수 있습니다.

JavaScript 코드 편집기에서 오류가 발생하면 사유와 함께 오류 상태가 표시됩니다.

유효성 검사에 대한 자세한 내용은 [Adobe Experience Platform Assurance 유효성 검사](https://github.com/adobe/griffon-validation-plugins) GitHub. 여기에서 Adobe이 소유한 유효성 검사의 예를 확인할 수 있습니다. 자세한 내용은 [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) 를 참조하십시오.
