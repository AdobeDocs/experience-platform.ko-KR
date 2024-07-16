---
title: 유효성 검사 편집기 보기
description: 이 안내서에는 Adobe Experience Platform Assurance의 유효성 검사 편집기 보기에 대한 정보가 자세히 나와 있습니다.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 100%

---

# 유효성 검사 편집기 보기

유효성 검사 편집기를 사용하면 JavaScript 기능을 빠르고 쉽게 관리하여 Adobe Experience Platform Assurance 세션에서 이벤트의 유효성을 검사할 수 있습니다. 각 함수는 Assurance 세션에서 이벤트를 수신합니다. 클라이언트 구성, 이벤트 조건, 테스트 및 사용 사례를 검증하는 함수를 작성할 수 있습니다.

## 유효성 검사 편집기 시작하기

[Assurance를 설정](../tutorials/implement-assurance.md)한 후 **[!UICONTROL 홈]** 보기에서 **[!UICONTROL 유효성 검사 편집기]**&#x200B;를 선택합니다

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## 유효성 검사 함수 작성

이 기능을 사용하면 Adobe Experience Platform Assurance 세션에 대한 유효성 검사 기능을 생성, 편집 또는 삭제할 수 있습니다.

1. **[!UICONTROL 새 유효성 검사 만들기]**&#x200B;를 선택합니다.
2. 유효성 검사를 확인할 **이름**&#x200B;을 입력한 다음 **카테고리** 및 **설명**&#x200B;을 제공합니다.
3. 편집기에서 코드를 편집하여 Assurance 세션에 대한 이벤트의 유효성을 검사합니다.

함수 테스트가 완료되면 **[!UICONTROL 게시]**&#x200B;를 선택하여 유효성 검사를 저장합니다.

### 이벤트 정의

| 키 | 유형 | 설명 |
| :--- | :--- | :--- |
| `uuid` | 문자열 | 이벤트에 대한 Universally Unique Identifier입니다. |
| `timestamp` | 숫자 | 이벤트가 Assurance로 전송되었을 때 클라이언트의 타임스탬프입니다. |
| `eventNumber` | 숫자 | 이벤트 발송 시 주문에 사용됩니다. 이 키는 이벤트의 타임스탬프가 동일한 경우에 유용합니다. |
| `vendor` | 문자열 | 역방향 도메인 이름 형식의 공급업체 식별 문자열(예: com.adobe.assurance)입니다. |
| `type` | 문자열 | 이벤트 유형을 나타내는 데 사용됩니다. |
| `payload` | 오브젝트 | 이벤트에 대한 데이터를 정의하고 고유하고 공통된 속성을 포함합니다. 몇 가지 일반적인 속성에는 `ACPExtensionEventSource` 및 `ACPExtensionEventType`이 포함됩니다. |
| `annotations` | 배열 | 주석 오브젝트의 배열입니다. |

### 주석 정의

| 키 | 유형 | 설명 |
| :--- | :--- | :--- |
| `uuid` | 문자열 | 주석에 대한 Universally Unique Identifier입니다. |
| `type` | 문자열 | 주석 유형을 나타내는 데 사용되며 보통 플러그인 이름입니다(예: 분석). |
| `payload` | 오브젝트 | 이벤트를 보완해야 하는 데이터를 정의합니다. Adobe Analytics의 경우 후처리된 히트 데이터가 포함된 위치입니다. |

### 유효성 검사 결과

유효성 검사 함수는 다음을 포함하는 오브젝트를 반환해야 합니다.

| 키 | 유형 | 설명 |
| :--- | :--- | :--- |
| `message` | 문자열 | 요약 결과에 표시할 유효성 검사 메시지입니다. |
| `events` | 배열 | 일치 또는 일치하지 않는 것으로 보고되는 이벤트 UUID의 배열입니다. |
| `links` | 배열 | 참조 문서 및 기타 리소스`{( type: 'doc'|'product', url: String )}`에 대한 `ValidationResultLink` 오브젝트 배열 |
| `result` | 문자열 | 다음은 유효성 검사 결과이며 “일치함”, “일치하지 않음”, “알 수 없음” 등 열거된 문자열 중 하나일 것으로 예상됩니다. |

## 유효성 검사 결과 보기

함수 결과는 코드 편집기 아래의 결과 섹션에 표시됩니다. 유효성 검사 결과가 `unknown` 또는 `not matched`이고 `events` 배열에 하나 이상의 `uuids`가 있는 경우 타임라인에서 이벤트가 다음 색상으로 강조 표시됩니다.

* 녹색 - 일치함
* 주황색 - 알 수 없음
* 빨간색 - 일치하지 않음

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## 문제 해결

개발자 콘솔에 항목을 인쇄하기 위해 `console.log()` 함수를 추가할 수 있습니다. 또는 결과 오브젝트의 메시지 속성을 사용하여 결과 패널에 대한 메시지를 디버그할 수 있습니다.

JavaScript 코드 편집기에서 오류가 발생하면 이유와 함께 오류 상태가 표시됩니다.

유효성 검사에 대한 자세한 내용은 [Adobe Experience Platform Assurance 유효성 검사](https://github.com/adobe/griffon-validation-plugins) GitHub를 참조하십시오. 여기에서 Adobe가 소유한 유효성 검사의 예를 찾을 수 있습니다. 유효성 검사에 대한 자세한 설명은 [wiki](https://github.com/adobe/griffon-validation-plugins/wiki)를 참조하십시오.
