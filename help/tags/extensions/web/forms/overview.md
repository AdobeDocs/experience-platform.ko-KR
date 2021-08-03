---
title: Adobe Experience Manager Forms 확장 개요
description: Adobe Experience Platform의 Adobe Experience Manager Forms 태그 확장에 대해 알아봅니다.
source-git-commit: f31a1d2e84dee262e04f1db0415ffd76248ecb6c
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 6%

---

# Adobe Experience Manager Forms 확장 개요

이 문서에서는 Adobe Experience Platform의 Adobe Experience Manager Forms 태그 확장에 대한 개요를 제공합니다.

## 이벤트

확장에서 제공하는 이벤트 유형은 다음과 같습니다.

1. **렌더링**: 사용자가 양식을 렌더링할 때 트리거됩니다(열기).
1. **오류**: 사용자가 양식에서 유효성 검사 오류를 수행하면 트리거됩니다.
1. **도움말**: 사용자가 필드의 도움말 아이콘을 클릭할 때 트리거됩니다.
1. **제출**: 양식 제출에서 트리거됩니다.
1. **필드 방문**: 필드를 방문할 때 트리거됩니다.
1. **포기**: 사용자가 탭을 닫거나 다른 URL로 이동할 때 트리거됩니다.
1. **저장**: 양식이 포털에 저장되면 트리거됩니다.

>[!IMPORTANT]
>
>현재 Save 이벤트는 Forms as a Cloud Service에 사용할 수 없습니다. 적응형 Forms에서 규칙 편집기에서 발송한 사용자 지정 이벤트는 코어 이벤트 &quot;사용자 지정 이벤트 캡처&quot;를 사용하여 캡처할 수 있습니다.

## 데이터 요소

확장은 Analytics 호출에서 속성을 전송하는 데 사용할 수 있는 몇 가지 데이터 요소를 제공합니다.

## 시작하기

아래 절차에 따라 확장을 시작하십시오.

1. 확장 카탈로그에서 Adobe Experience Manager Forms 확장을 설치합니다. 설치 후에는 추가 구성이 필요하지 않습니다.
2. [Adobe Analytics 확장](../analytics/overview.md#Configure-the-Adobe-Analytics-extension)을 설치하고 구성합니다.

## 규칙 만들기

Experience Manager Forms 확장을 사용하는 규칙은 다음과 같습니다.

![작업 구성](./images/rule.png)

구현에 대해 유사한 규칙을 만들려면 아래 설명된 단계를 따르십시오.

### 이벤트 추가

1. 확장 드롭다운에서 **Adobe Experience Manager Forms**&#x200B;을 선택합니다.
2. 캡처할 이벤트를 선택합니다.

![작업 구성](./images/AEM-forms-event.png)

### 작업 추가

1. 확장 드롭다운에서 &quot;Adobe Analytics&quot;을 선택합니다.
2. 작업 유형 드롭다운에서 &quot;변수 설정&quot;을 선택합니다.
3. 구성 보기에서 전송할 속성 및 이벤트를 선택합니다.
4. 3단계에서 설정된 이벤트 및 속성을 사용하여 분석 호출을 전송하려면 &quot;비콘 보내기&quot; 작업을 추가합니다
   ![작업 구성](./images/AEM-forms-sendBeacon.png)
5. 변수 지우기 작업을 추가합니다.

![작업 구성](./images/AEM-forms-action.png)