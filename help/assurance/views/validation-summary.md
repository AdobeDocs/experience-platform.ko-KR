---
title: 유효성 검사 편집기 보기
description: 이 안내서에서는 Adobe Experience Platform Assurance의 유효성 검사 편집기 보기에 대한 자세한 정보를 설명합니다.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---

# 유효성 검사 편집기 보기

유효성 검사 편집기를 사용하면 Adobe Experience Platform Assurance 세션에서 이벤트의 유효성을 검사하기 위해 JavaScript 함수를 빠르고 쉽게 관리할 수 있습니다. 각 기능은 보증 세션에서 이벤트를 수신합니다. 클라이언트 구성, 이벤트 조건, 테스트 및 사용 사례의 유효성을 검사하는 함수를 작성할 수 있습니다.

## 유효성 검사 편집기 시작

다음 이후 [보증 설정](../tutorials/implement-assurance.md), **[!UICONTROL 홈]** 보기, 선택 **[!UICONTROL 유효성 검사 편집기]**.

![유효성 검사-편집기-스크린샷](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## 유효성 검사 함수 작성

이 기능을 사용하면 Adobe Experience Platform Assurance 세션에 대한 유효성 검사 기능을 만들거나 편집하거나 삭제할 수 있습니다.

1. 선택 **[!UICONTROL 새 유효성 검사 만들기]**.
2. 입력 **이름** 유효성 검사를 식별한 다음 **범주** 및 a **설명**.
3. 편집기에서 코드를 편집하여 Assurance 세션에 대한 이벤트의 유효성을 검사합니다.

함수 테스트가 완료되면 다음을 선택합니다. **[!UICONTROL 게시]** 을 클릭하여 유효성 검사를 저장합니다.

### 이벤트 정의

| 키 | 유형 | 설명 |
| :--- | :--- | :--- |
| `uuid` | 문자열 | 이벤트에 대한 Universally Unique Identifier. |
| `timestamp` | 숫자 | 이벤트가 Assurance로 전송된 클라이언트의 타임스탬프. |
| `eventNumber` | 숫자 | 이벤트를 전송할 때 주문하는 데 사용됩니다. 이 키는 이벤트에 동일한 타임스탬프가 있는 경우에 유용합니다. |
| `vendor` | 문자열 | 역방향 도메인 이름 형식의 공급업체 식별 문자열(예: com.adobe.assurance). |
| `type` | 문자열 | 이벤트 유형을 나타내는 데 사용됩니다. |
| `payload` | 오브젝트 | 이벤트에 대한 데이터를 정의하고 고유하고 일반적인 속성을 포함합니다. 몇 가지 일반적인 속성은 다음과 같습니다. `ACPExtensionEventSource` 및 `ACPExtensionEventType`. |
| `annotations` | 배열 | 주석 객체의 배열입니다. |

### 주석 정의

| 키 | 유형 | 설명 |
| :--- | :--- | :--- |
| `uuid` | 문자열 | 주석에 대한 Universally Unique Identifier. |
| `type` | 문자열 | 주석 유형을 나타내는 데 사용되며 일반적으로 플러그인의 이름입니다(예: analytics). |
| `payload` | 오브젝트 | 이벤트를 보완해야 하는 데이터를 정의합니다. Adobe Analytics의 경우 후처리된 히트 데이터가 여기에 포함됩니다. |

### 유효성 검사 결과

유효성 검사 함수는 다음을 포함하는 개체를 반환해야 합니다.

| 키 | 유형 | 설명 |
| :--- | :--- | :--- |
| `message` | 문자열 | 요약 결과에 표시할 유효성 검사 메시지입니다. |
| `events` | 배열 | 일치하거나 일치하지 않는 것으로 보고할 이벤트 UID 배열입니다. |
| `links` | 배열 | 배열 `ValidationResultLink` 설명서 및 기타 리소스에 대한 참조 개체 `{( type: 'doc'|'product', url: String )}` |
| `result` | 문자열 | 유효성 검사 결과이며, 열거형 문자열 &quot;일치함&quot;, &quot;일치하지 않음&quot;, &quot;알 수 없음&quot; 중 하나여야 합니다. |

## 유효성 검사 결과 보기

함수의 결과는 코드 편집기 아래의 결과 섹션에 표시됩니다. 유효성 검사 결과가 `unknown` 또는 `not matched` 및 `events` 배열에 하나 이상의 `uuids`에서는 이벤트가 타임라인에서 다음 색상으로 강조 표시됩니다.

* 녹색 - 일치함
* 주황색 - 알 수 없음
* 빨간색 - 일치하지 않음

![타임링-유효성 검사-하이라이트-스크린샷](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## 문제 해결

다음을 추가할 수 있습니다. `console.log()` 개발자 콘솔에 항목을 인쇄하는 데 사용됩니다. 또는 결과 개체의 message 속성을 사용하여 메시지를 결과 패널에 디버그할 수 있습니다.

JavaScript 코드 편집기에서 오류가 발생하면 오류와 함께 오류 상태가 표시됩니다.

유효성 검사에 대한 자세한 내용은 [Adobe Experience Platform 보증 유효성 검사](https://github.com/adobe/griffon-validation-plugins) GitHub. 여기에서 Adobe이 소유한 유효성 검사의 예를 찾을 수 있습니다. 다음을 참조하십시오. [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) 유효성 검사에 대한 자세한 설명입니다.
