---
title: Adobe Experience Platform Assurance 사용
description: 이 안내서에서는 Adobe Experience Platform Assurance를 설치하고 구현한 후에 사용하는 방법을 설명합니다.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 100%

---

# Adobe Experience Platform Assurance 사용

이 튜토리얼에서는 Adobe Experience Platform Assurance를 사용하는 방법을 설명합니다. Adobe Experience Platform Assurance 확장 기능의 설치 및 구현 방법에 대한 지침은[Assurance 확장 기능 구현](./implement-assurance.md)에 관한 튜토리얼을 참조하십시오.

## 세션 만들기

[Assurance UI](https://experience.adobe.com/assurance)에 로그인한 후에 **[!UICONTROL 세션 만들기]**&#x200B;를 선택하여 세션을 만들 수 있습니다.

![세션을 생성할 수 있는 위치를 보여 주는 세션 만들기 버튼이 강조 표시됩니다.](./images/using-assurance/create-session.png)

**[!UICONTROL 새 세션 만들기]** 대화 상자가 표시됩니다. 제공된 지침을 검토한 후 **[!UICONTROL 시작]**&#x200B;을 선택하여 계속 진행하십시오.

![Assurance 사용 방법에 대한 지침을 표시하는 새 세션 만들기 대화 상자가 표시됩니다.](./images/using-assurance/create-new-session.png)

이제 세션을 확인할 이름을 입력한 다음, **[!UICONTROL 기본 URL]**(앱에 대한 딥 링크 URL)을 제공할 수 있습니다. 이러한 세부 정보를 제공한 후 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

>[!INFO]
>
>기본 URL은 URL에서 앱을 시작하는 데 사용되는 루트 정의입니다. Assurance 세션을 시작할 수 있는 세션 URL이 생성됩니다. 예제 값은 다음과 같습니다. `myapp://default` **[!UICONTROL 기본 URL]** 필드에서 앱의 기본 딥 링크 정의를 입력합니다.

![새 세션을 만드는 전체 워크플로가 표시됩니다.](./images/using-assurance/create-session.gif)

## 세션에 연결

세션을 만든 후 **[!UICONTROL 새 세션 만들기]** 대화 상자에 링크, QR 코드 및 PIN이 표시되는지 확인합니다.

![Assurance 세션에 연결하는 옵션을 보여 주는 대화 상자가 표시됩니다.](./images/using-assurance/create-new-session-pin.png)

이 대화 상자가 표시되면 디바이스의 카메라 앱을 사용하여 QR 코드를 스캔하고 앱을 열거나 링크를 복사하여 앱에서 열 수 있습니다. 앱이 시작되면 오버레이된 PIN 입력 화면이 보이게 됩니다. 이전 단계에서 PIN을 입력한 다음 **[!UICONTROL 연결]**&#x200B;을 누릅니다.

Adobe Experience Platform 아이콘(빨간색 Adobe “A”)이 앱에 표시되면 앱이 Assurance에 연결되었음을 확인할 수 있습니다.

![애플리케이션을 Assurance 세션에 연결하는 전체 워크플로가 표시됩니다.](./images/using-assurance/connect-session.gif)

## 세션 내보내기

Assurance 세션을 내보내려면 앱의 세션 세부 정보 페이지에서 세션의 **[!UICONTROL JSON으로 내보내기]**&#x200B;를 선택합니다.

![세션 내보내기](./images/using-assurance/export-session.png)

내보내기 옵션은 검색 필터 결과를 고려하고 이벤트 보기에 표시된 이벤트만 내보냅니다. 예를 들어 “추적” 이벤트를 검색한 다음 **[!UICONTROL JSON으로 내보내기]**&#x200B;를 선택하면 “추적” 이벤트 결과만 내보내집니다.
