---
title: 웹 SDK 태그 확장 시작하기
description: 웹 SDK 태그 확장을 사용하여 Adobe Experience Platform Edge Network에 이벤트 데이터를 보냅니다.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 3%

---

# 웹 SDK 태그 확장 시작하기

Adobe Experience Platform의 **tags**(이전 Launch)을(를) 사용하여 웹 사이트에서 Edge Network 및 다운스트림 Adobe 솔루션으로 이벤트 데이터를 보냅니다.

이 단계를 수행하기 전에 다음 [속성 권한](/help/tags/ui/administration/user-permissions.md)에 액세스할 수 있는지 확인하십시오.

* [!UICONTROL Develop]
* [!UICONTROL Manage extensions]

또한 다음 범주의 모든 [권한](/help/access-control/home.md#permissions)이 있는지 확인하십시오.

* 데이터 모델링
* ID

## XDM 스키마 만들기 {#schema}

[XDM(Experience Data Model)](/help/xdm/home.md)은 스키마의 형태로 데이터에 대한 일반적인 구조와 정의를 제공하는 오픈 소스 사양입니다. Edge Network으로 데이터를 전송할 때는 스키마를 구성하는 것이 좋습니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Schemas]**(으)로 이동합니다.
1. **[!UICONTROL Create schema]**&#x200B;를 선택합니다.
1. **[!UICONTROL Experience Event]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.
1. 스키마에 원하는 이름을 지정한 다음 **[!UICONTROL Finish]**&#x200B;을(를) 선택합니다.
1. (선택 사항) 수집하려는 추가 데이터에 대해 더 많은 필드 또는 [필드 그룹](/help/xdm/ui/resources/field-groups.md)을 추가할 수 있습니다.

![스키마 캔버스](assets/getting-started/schema-structure.png)

>[!NOTE]\
>저장되면 스키마에서는 *추가*&#x200B;만 변경할 수 있습니다. 자세한 내용은 [스키마 진화](/help/xdm/schema/composition.md#evolution)을 참조하십시오.

## 데이터 스트림 만들기 {#datastream}

[데이터 스트림](/help/datastreams/overview.md)은(는) 전송한 데이터를 처리하는 방법을 Edge Network에 알려 주는 구성입니다. 지정된 제품에 데이터를 전송하도록 데이터스트림을 구성할 때 데이터스트림은 특정 제품이 인식하는 방식으로 관련 데이터를 각 제품에 자동으로 전달합니다.

1. **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**(으)로 이동합니다.
1. **[!UICONTROL New datastream]**&#x200B;를 선택합니다.
1. 데이터 스트림에 원하는 이름을 지정하고 **[!UICONTROL Mapping schema]**&#x200B;에서 최근에 만든 스키마를 선택합니다.
1. **[!UICONTROL Save]**&#x200B;를 선택합니다.

![데이터스트림 목록](assets/getting-started/datastreams.png)

## 태그 속성 만들기

스키마와 데이터스트림을 만들면 태그 속성을 만들고 구성할 수 있습니다.

1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. **[!UICONTROL New property]**&#x200B;를 선택합니다.
1. 태그 속성에 원하는 이름과 도메인을 지정한 다음 **[!UICONTROL Save]**&#x200B;을(를) 선택합니다.

## 태그 확장 설치

웹 SDK 태그 확장은 지정된 태그 속성에 설치됩니다.

1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]** > **[!UICONTROL Extensions]**(으)로 이동합니다.
1. **[!UICONTROL Catalog]** 탭을 선택합니다. 
1. 검색을 사용하여 **[!UICONTROL Adobe Experience Platform Web SDK]** 확장을 찾습니다.
1. 확장 카드를 선택한 다음 오른쪽의 **[!UICONTROL Install]**&#x200B;을(를) 선택합니다.

![SDK 설치](assets/getting-started/install-sdk.png)

## 태그 확장 구성

웹 SDK 태그 확장을 설치하면 자동으로 [구성](configure/config-overview.md) 페이지로 이동합니다.

1. [데이터스트림 섹션](configure/datastreams.md)에서 각 환경에 대해 원하는 데이터스트림을 선택합니다.

다른 모든 구성 설정은 자동으로 작성되거나 선택 사항입니다. 원하는 구성 설정을 설정한 다음 **[!UICONTROL Save]**&#x200B;을(를) 선택합니다.

## 변수 데이터 요소 만들기

Adobe에서는 [변수](data-element-types.md#variable) 데이터 요소를 사용하여 Adobe으로 보낼 페이로드를 저장하는 것이 좋습니다. XDM 개체도 사용 가능한 데이터 요소이지만 사용 사례에서 더 오래되고 더 제한됩니다.

1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Data elements]** > **[!UICONTROL Create new data element]**&#x200B;을(를) 선택합니다.
1. 데이터 요소 왼쪽에 다음 속성을 지정합니다.
   * **[!UICONTROL Name]**: 원하는 이름
   * **[!UICONTROL Extension]**:[!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Data element type]**: [!UICONTROL Variable]
1. 오른쪽에서 다음 속성을 설정합니다.
   **변수 형식**: XDM
   **[!UICONTROL Sandbox]**: 스키마를 만든 샌드박스
   **[!UICONTROL Schema]**: 원하는 스키마
1. **[!UICONTROL Save]**&#x200B;를 선택합니다.

## 규칙 만들기

규칙은 무언가를 트리거하거나 변수를 설정할 시기를 결정합니다. 라이브러리가 로드될 때마다 실행되는 규칙을 만들면 모든 페이지에 값을 포함할 변수를 쉽게 채울 수 있습니다.

1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Rules]** > **[!UICONTROL Add rule]**&#x200B;을(를) 선택합니다.
1. 규칙에 원하는 이름을 지정합니다.
1. `+` 옆에 있는 &#39;**[!UICONTROL Events]**&#39; 아이콘을 선택하십시오.
1. 이벤트에 다음 설정을 지정합니다.
   * **[!UICONTROL Extension]**:[!UICONTROL Core]
   * **[!UICONTROL Event type]**: [!UICONTROL Library loaded (page top)]
1. **[!UICONTROL Keep changes]**&#x200B;를 선택합니다.

위의 단계는 규칙의 기준 부분을 설정하며, 이것은 라이브러리가 로드되면 트리거됩니다. 다음 단계에서는 해당 기준이 충족될 때 수행할 작업을 설정합니다.

1. `+` 옆에 있는 &#39;**[!UICONTROL Actions]**&#39; 아이콘을 선택하십시오.
1. 왼쪽에 다음 설정을 지정합니다.
   * **[!UICONTROL Extension]**:[!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Send event]
1. 오른쪽에 다음 필드를 설정합니다.
   * **[!UICONTROL XDM]**: XDM 변수 데이터 요소
1. **[!UICONTROL Keep changes]**&#x200B;를 선택합니다.

![작업 구성](assets/getting-started/action-config.png)

## 게시

태그 속성에는 Edge Network으로 데이터를 전송하는 데 필요한 모든 구성 요소가 포함되어 있습니다.

1. **[!UICONTROL Data Collection]** > **[!UICONTROL Publishing flow]**(으)로 이동합니다.
1. **[!UICONTROL Add library]**&#x200B;를 선택합니다.
1. 원하는 이름을 라이브러리에 지정합니다. 버전 제어 소프트웨어에서 작업할 때 이 이름을 커밋 이름과 유사하게 간주합니다.
1. 환경 드롭다운 메뉴를 **[!UICONTROL Development]**(으)로 설정합니다.
1. **[!UICONTROL Add all changed resources]**&#x200B;를 선택합니다.
1. **[!UICONTROL Save & build to Development]**&#x200B;를 선택합니다.

이제 변경 사항이 개발 환경에 배포됩니다.

1. **[!UICONTROL Data Collection]** > **[!UICONTROL Environments]**(으)로 이동합니다.
1. 개발 환경 옆에 있는 설치 아이콘을 선택합니다
1. 사이트의 테스트 웹 페이지 내에 포함 코드를 설치합니다.

태그가 개발 환경에서 작동하는지 확인하면 [!UICONTROL Publishing flow] 인터페이스를 사용하여 라이브러리를 스테이징에 게시한 다음 프로덕션에 게시할 수 있습니다.

1. **라이브러리**&#x200B;에 확장 및 규칙을 추가하고 **환경**&#x200B;에 빌드한 다음 사이트에 포함 코드를 설치하십시오.
2. **Adobe Experience Platform Debugger**(으)로 유효성을 검사합니다.

이제 이벤트를 캡처하여 Edge Network으로 전송하는 린 설정이 있습니다. 이제 스키마에 필드를 추가하거나, 데이터 스트림에 제품을 추가하거나, 태그 속성에 데이터 요소를 추가하여 구현을 더 빌드할 수 있습니다.
