---
title: Adobe Audience Manager 확장 개요
description: Adobe Experience Platform에서의 Adobe Audience Manager 태그 확장 기능에 대해 알아봅니다.
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 71%

---

# Adobe Audience Manager 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

Audience Manager 태그 확장을 사용하면 Audience Manager에서 사용하는 DIL 코드와 Adobe Experience Platform의 속성을 통합할 수 있습니다.

이 확장을 사용하여 규칙을 작성할 때 사용할 수 있는 옵션에 대한 정보를 보려면 이 참조를 사용하십시오.

>[!NOTE]
>
>이 확장은 Adobe Analytics 데이터의 이벤트 전달에 사용하기 위한 것이 아닙니다. 이벤트 전달의 경우 [Adobe Analytics 확장](../analytics/overview.md).

## Adobe Audience Manager 확장 구성

Adobe Audience Manager 확장이 아직 설치되지 않은 경우 속성을 연 다음 을 선택합니다 **[!UICONTROL 확장 > 카탈로그]**, Adobe Audience Manager 확장을 마우스로 가리킨 다음 **[!UICONTROL 설치]**.

확장을 구성하려면 를 엽니다. [!UICONTROL 확장] 탭을 클릭하고 확장을 마우스로 가리킨 다음 **[!UICONTROL 구성]**.

### DIL 설정

DIL 설정을 구성합니다. 다음 구성 옵션을 사용할 수 있습니다.

![](../../../images/ext-aam-config.png)

#### DIL Version

DIL(데이터 통합 라이브러리) 버전을 표시합니다.

이 설정은 변경할 수 없습니다.

#### 특정 경로 제외

URL이 제외된 경로와 일치하는 경우 확장이 로드되지 않습니다.

선택 **[!UICONTROL 경로 추가]** 제외된 URL을 지정합니다.

URL이 정규 표현식인 경우 Regex를 활성화합니다.

#### Use DIL Site Catalyst Module

[SiteCatalyst 모듈](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_sc_init.html)은 DIL을 사용하여 Analytics 태그 요소를 Audience Manager로 보냅니다.

siteCatalyst.init 파일을 구성하려면 코드 편집기를 사용합니다.

이 구성에 대한 정보가 들어 있는 메모를 만들 수도 있습니다.

#### Use DIL Google Analytics Module

[Google Analytics 모듈](https://experiencecloud.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)을 활성화합니다.

#### DIL.create Initialization Properties

[DIL.create](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html)에서 사용되는 초기화 속성과 [visitorService 개체](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_visitor_service.html)의 네임스페이스 하위 속성을 추가합니다. 두 개의 샘플 사용 사례는 코드 편집기에서 코드 주석에 포함되어 있습니다.

선택 **[!UICONTROL 항목 선택]** 속성을 더 추가합니다.

i 아이콘을 마우스로 가리키면 각 속성이 수행하는 작업을 확인할 수 있습니다. [Audience Manager DIL 설명서](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html)에서 속성에 대한 자세한 내용을 찾을 수 있습니다.

선택 **[!UICONTROL 저장]** 확장 구성을 마치면 됩니다.

## Adobe Audience Manager 확장 작업 유형

이 항목에서는 Audience Manager 확장에서 사용할 수 있는 작업 유형을 설명합니다.

Adobe Audience Manager 확장은 규칙의 Then 부분에서 다음 작업을 제공합니다.

### 사용자 지정 코드 실행

코드 편집기에서 구성한 사용자 지정 코드를 실행합니다.

코드 편집기에서 원하는 코드를 입력한 다음 코드 이름을 입력합니다. 이 코드는 규칙 빌더의 Then 부분에서 사용할 수 있습니다.

![](../../../images/ext-aam-then.png)

구성에 대한 정보가 포함된 메모를 추가할 수도 있습니다.
