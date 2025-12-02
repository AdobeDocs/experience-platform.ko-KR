---
title: ID로 리디렉션
description: 조직의 도메인 간에 방문자 식별자를 공유할 수 있습니다.
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# ID로 리디렉션

**[!UICONTROL Redirect with identity]** 작업 유형을 사용하면 현재 페이지에서 조직이 소유한 다른 도메인으로 방문자 식별자를 공유할 수 있습니다. 클릭 이벤트와 값 비교 조건과 함께 사용할 수 있도록 설계되었습니다. 기능적으로는 JavaScript 라이브러리의 [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) 명령과 비슷합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Rules]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL Actions]에서 기존 작업을 선택하거나 작업을 만듭니다.
1. [!UICONTROL Extension] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정한 다음 [!UICONTROL Action type]을(를) **[!UICONTROL Redirect with identity]**(으)로 설정합니다.

## 사용 사례

* **도메인에서 개인 식별**: 방문자가 한 도메인에서 조직이 소유한 다른 도메인으로 클릭하는 경우 이 작업을 사용하여 동일한 개인으로 간주할 수 있습니다. 이 식별 방법은 여러 도메인의 데이터를 결합하는 보고서가 있어 방문자 인플레이션을 방지하는 경우 특히 유용합니다.
* **모바일 앱에서 웹 앱으로 개인 식별**: 방문자가 모바일 앱 내부에 있고 웹 앱에 대한 링크를 클릭하는 경우 이 작업을 사용하면 웹 SDK에서 동일한 개인임을 인식하도록 할 수 있습니다. 이 워크플로우를 통해 보고 및 개인화에 대한 일관된 환경을 사용할 수 있습니다.

## 사용 가능한 필드

* **[!UICONTROL Instance]**: 작업이 적용되는 SDK 인스턴스입니다. 구현에서 단일 SDK 인스턴스를 사용하는 경우 이 드롭다운 메뉴가 비활성화됩니다.
* **[!UICONTROL Datastream configuration overrides]**: 이 명령은 데이터 스트림 구성 재정의를 지원하므로 이 데이터를 받을 앱 및 서비스를 제어할 수 있습니다. 개별 명령과 태그 확장 구성 설정 모두에서 데이터스트림 구성 재정의를 설정하면 개별 명령이 우선합니다. 자세한 내용은 [데이터 스트림 구성 재정의](../configure/configuration-overrides.md)를 참조하십시오.

## 규칙 예

이 명령은 일반적으로 클릭을 수신하고 원하는 도메인을 확인하는 특정 규칙과 함께 사용됩니다.

+++규칙 이벤트 기준

`href` 속성이 있는 앵커 태그를 클릭하면 트리거됩니다.

* **[!UICONTROL Extension]**: 코어
* **[!UICONTROL Event type]**: 클릭
* **[!UICONTROL When the user clicks on]**: 특정 요소
* **[!UICONTROL Elements matching the CSS selector]**:`a[href]`

![규칙 이벤트](../assets/id-sharing-event-configuration.png)

+++

+++규칙 조건

원하는 도메인에서만 트리거됩니다.

* **[!UICONTROL Logic type]**: 일반
* **[!UICONTROL Extension]**: 코어
* **[!UICONTROL Condition Type]**: 값 비교
* **[!UICONTROL Left Operand]**:`%this.hostname%`
* **[!UICONTROL Operator]**: RegEx와 일치
* **[!UICONTROL Right Operand]**: 원하는 도메인과 일치하는 정규 표현식입니다. 예, `adobe.com$|behance.com$`

![규칙 조건](../assets/id-sharing-condition-configuration.png)

+++

+++규칙 작업

URL에 ID를 추가합니다.

* **[!UICONTROL Extension]**: Adobe Experience Platform 웹 SDK
* **[!UICONTROL Action Type]**: ID를 사용하여 리디렉션

![규칙 작업](../assets/id-sharing-action-configuration.png)

+++
