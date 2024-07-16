---
title: 태그 확장을 사용하여 웹 SDK 설치
description: Adobe Experience Cloud 데이터 수집을 사용하여 웹 SDK 라이브러리를 참조합니다.
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 태그 확장을 사용하여 웹 SDK 설치

Adobe은 웹 SDK를 구현하고 구성할 수 있는 전용 태그 확장 기능을 제공합니다. 이 구현 방법은 데이터 수집 코드를 배포하고 유지 관리하기 위해 Adobe에서 권장하는 기본 방법입니다.

[필수 구성 요소](overview.md)를 충족하면 다음 단계를 사용하여 Web SDK 태그 확장을 배포할 수 있습니다.

## 태그 내에 확장 설치

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택하거나 태그 속성을 만듭니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 **[!UICONTROL 카탈로그]** 탭을 선택합니다.
1. **[!UICONTROL Adobe Experience Platform Web SDK]** 확장을 찾아 설치합니다.
1. 각 환경에 적합한 샌드박스 및 데이터스트림을 선택한 다음 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

자세한 내용은 [Web SDK 태그 확장을 구성](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)하는 방법에 대한 설명서를 참조하십시오.

## 개발에 대한 태그 코드 Publish

이제 이 태그에 대한 Web SDK 확장이 설치되었습니다. 이제 개발 환경에서 사용할 태그 코드를 게시할 수 있습니다.

1. **[!UICONTROL 게시 흐름]**(으)로 이동한 다음 **[!UICONTROL 라이브러리 추가]**&#x200B;를 선택합니다.
1. 이 라이브러리에 &quot;웹 SDK 라이브러리 추가&quot;와 같이 원하는 이름을 지정합니다. [!UICONTROL 환경] 드롭다운 메뉴를 &quot;개발&quot;로 설정합니다.
1. **[!UICONTROL 변경된 모든 리소스 추가]**&#x200B;를 선택한 다음 **[!UICONTROL 개발에 저장 및 빌드]**&#x200B;를 클릭합니다.

## 사이트에 로더 코드 설치

이제 태그 코드가 게시되었으므로 웹 사이트에 태그 로더 코드를 추가할 수 있습니다.

1. **[!UICONTROL 환경]**(으)로 이동한 다음 &quot;개발&quot; 옆에 있는 상자 아이콘을 클릭하여 이 환경에 대한 설치 지침이 포함된 모달 창을 엽니다.
1. 포함 코드를 복사하여 웹 사이트의 `<head>` 태그에 붙여넣습니다.

## 구현 작성 및 프로덕션에 게시

확장 자체에 대한 자세한 내용은 [Web SDK 확장 개요](../../tags/extensions/client/web-sdk/overview.md)를, 태그 인터페이스 탐색에 대한 자세한 내용은 [태그 개요](../../tags/home.md)를 참조하십시오.
