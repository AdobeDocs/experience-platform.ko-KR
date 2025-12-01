---
title: Adobe Experience Platform Assurance 사용
description: 이 안내서에서는 Adobe Experience Platform Assurance를 설치하고 구현한 후에 사용하는 방법을 설명합니다.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: f8576e7f7e1da7351f7860cba27d5d09d0161132
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 28%

---

# Adobe Experience Platform Assurance 사용

이 튜토리얼에서는 Adobe Experience Platform Assurance를 사용하는 방법을 설명합니다. Adobe Experience Platform Assurance 확장 기능의 설치 및 구현 방법에 대한 지침은[Assurance 확장 기능 구현](./implement-assurance.md)에 관한 튜토리얼을 참조하십시오.

## 세션 만들기

[Assurance UI](https://experience.adobe.com/assurance)에 로그인한 후 **[!UICONTROL Create Session]**&#x200B;을(를) 선택하여 세션 만들기를 시작할 수 있습니다.

![세션을 생성할 수 있는 위치를 보여 주는 세션 만들기 버튼이 강조 표시됩니다.](./images/using-assurance/create-session.png)

**[!UICONTROL Create New Session]** 대화 상자에 세션 만들기를 위한 두 가지 옵션이 표시됩니다.

### 딥링크 연결

고유한 세션 URL, QR 코드 및 PIN을 생성하려면 이 옵션을 선택하십시오. QR 코드를 스캔하거나 앱에서 세션 링크를 수동으로 연 다음 PIN을 입력하여 연결을 설정하십시오.

**[!UICONTROL Deep link connect]**&#x200B;을(를) 선택하고 **[!UICONTROL Start]**&#x200B;을(를) 선택하여 계속합니다.

![딥링크 연결 옵션을 보여 주는 [새 세션 만들기] 대화 상자가 선택되었습니다.](./images/using-assurance/create-new-session-deep-link.png)

이제 이름을 입력하여 세션을 식별한 다음 **[!UICONTROL Base URL]**(앱의 딥링크 URL)을 제공할 수 있습니다. 이러한 세부 정보를 제공한 후 **[!UICONTROL Next]**&#x200B;을(를) 선택하십시오.

>[!INFO]
>
>기본 URL은 URL에서 앱을 시작하는 데 사용되는 루트 정의입니다. Assurance 세션을 시작할 수 있는 세션 URL이 생성됩니다. 예제 값은 다음과 같습니다. `myapp://default` **[!UICONTROL Base URL]** 필드에 앱의 기본 딥링크 정의를 입력하십시오.

![세션 이름 및 기본 URL 입력 필드가 표시됩니다.](./images/using-assurance/create-session-form-deep-link.png)

### 빠른 연결

앱에서 연결을 트리거하면 장치가 사용 가능한 장치 목록에 표시됩니다. Assurance 세션을 만들려면 **[!UICONTROL Quick connect]**&#x200B;을(를) 선택하십시오.

#### 전제 조건

Quick Connect를 사용하기 전에 앱에 필요한 SDK 버전 및 구현이 있는지 확인하십시오.

**Android SDK 요구 사항:**

- Mobile Core v3.1.0 이상
- Adobe Journey Optimizer v3.1.0 이상
- Adobe Experience Platform Assurance v3.0.4 이상

**iOS SDK 요구 사항:**

- Mobile Core v5.2.0 이상
- Adobe Journey Optimizer v5.1.1 이상
- Adobe Experience Platform Assurance v5.0.0 이상

**구현:**

Assurance 연결을 트리거하려면 앱에서 [`startSession` API](https://developer.adobe.com/client-sdks/home/base/assurance/api-reference/#startsession-quick-connect)을(를) 구현해야 합니다. 이 API 호출은 일반적으로 작업 세트에 포함되거나 앱 내에서 트리거됩니다.

#### 빠른 연결 세션 만들기

![빠른 연결 옵션을 보여 주는 [새 세션 만들기] 대화 상자가 선택되었습니다.](./images/using-assurance/create-new-session-quick-connect.png)

**[!UICONTROL Quick connect]**&#x200B;을(를) 선택하고 **[!UICONTROL Start]**&#x200B;을(를) 선택하여 계속 진행하면 장치 선택기 인터페이스가 표시됩니다.

1. **Assurance 연결 트리거** - 모바일 앱 또는 구현에서 `startSession` API를 사용하여 Assurance 연결을 시작하는 작업을 트리거합니다. 이렇게 하면 장치를 검색할 수 있게 됩니다.

2. **장치 선택 및 연결** - 사용 가능한 장치 목록에 장치가 나타나면 장치를 선택하고 **[!UICONTROL Connect]**&#x200B;을(를) 클릭합니다.

![사용 가능한 장치를 표시하는 빠른 연결 장치 선택기 인터페이스입니다.](./images/using-assurance/quick-connect-device-picker.png)

## 세션에 연결

연결하는 단계는 사용 중인 세션 유형에 따라 다릅니다.

### 딥링크 연결 세션

**[!UICONTROL Deep Link Connect]**(으)로 생성된 세션의 경우:

1. 기존 세션의 세션 세부 정보 페이지로 이동하거나 세션 생성 단계를 진행하여 링크, QR 코드 및 PIN을 확인합니다
2. 장치의 카메라 앱을 사용하여 QR 코드를 스캔하거나 링크를 복사하여 앱에서 엽니다
3. 앱이 실행되면 PIN 입력 화면이 오버레이되어 표시됩니다. PIN을 입력하고 **[!UICONTROL Connect]**&#x200B;을(를) 누르십시오.

![Assurance 세션에 연결하는 옵션을 보여 주는 대화 상자가 표시됩니다.](./images/using-assurance/deep-link-connection.png)

### 빠른 연결 세션

**[!UICONTROL Quick Connect]**(으)로 만든 세션(`adobeassurance://`(으)로 시작하는 세션 URL로 식별 가능)의 경우 장치 선택기 인터페이스를 통해 연결이 자동으로 수행됩니다.

1. 기존 세션에 대한 세션 세부 정보 페이지로 이동하거나 세션 생성 후 진행합니다
2. **[!UICONTROL Connect Device]** 섹션에는 장치 선택기 인터페이스가 표시됩니다
3. 앱에서 동작 세트를 트리거하여 장치를 검색 가능하게 만들기
4. 목록에서 장치를 선택하고 **[!UICONTROL Connect]**&#x200B;을(를) 클릭합니다

![연결할 수 있는 장치를 표시하는 장치 선택기 인터페이스입니다.](./images/using-assurance/quick-connect-device-picker.png)

### 연결 확인 중

Adobe Experience Platform 아이콘(빨간색 Adobe “A”)이 앱에 표시되면 앱이 Assurance에 연결되었음을 확인할 수 있습니다.

## 세션 내보내기

Assurance 세션을 내보내려면 앱의 세션 세부 정보 페이지에서 세션의 **[!UICONTROL Export to JSON]**&#x200B;을(를) 선택하십시오.

![세션 내보내기](./images/using-assurance/export-session.png)

내보내기 옵션은 검색 필터 결과를 고려하고 이벤트 보기에 표시된 이벤트만 내보냅니다. 예를 들어 &quot;추적&quot; 이벤트를 검색한 다음 **[!UICONTROL Export to JSON]**&#x200B;을(를) 선택하면 &quot;추적&quot; 이벤트 결과만 내보내집니다.