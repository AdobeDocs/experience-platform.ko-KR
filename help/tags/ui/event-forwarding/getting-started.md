---
title: 이벤트 전달 시작
description: Adobe Experience Platform에서 이벤트 전달 사용을 시작하려면 이 단계별 자습서를 따르십시오.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 25%

---

# 이벤트 전달 시작

>[!NOTE]
>
>이벤트 전달은 Adobe Real-Time Customer Data Platform 연결, Prime 또는 Ultimate 오퍼링의 일부로 포함된 유료 기능입니다.

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

Adobe Experience Platform에서 이벤트 전달을 사용하려면 다음 세 가지 옵션 중 하나 이상을 사용하여 Adobe Experience Platform Edge Network으로 데이터를 보내야 합니다.

* [Adobe Experience Platform 웹 SDK](../../extensions/client/web-sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)

>[!NOTE]
>Experience Platform Web SDK 및 Experience Platform Mobile SDK에서는 Adobe Experience Platform의 태그를 통해 배포할 필요가 없습니다. 그러나 태그를 사용하여 이러한 SDK를 배포하는 것이 좋습니다.

Edge 네트워크로 데이터를 전송하면 Adobe 솔루션을 전환하여 데이터를 보낼 수 있습니다. Adobe이 아닌 솔루션으로 데이터를 전송하려면 이벤트 전달 시 해당 설정을 지정합니다.

## 전제 조건

* Adobe Real-Time CDP Connections, Prime 또는 Ultimate(가격 책정은 Adobe 계정 팀에 문의)
* Adobe Experience Platform의 이벤트 전달
* Adobe Experience Platform Web SDK, Mobile SDK 또는 Edge Network으로 데이터를 전송하도록 구성된 Edge Network API
* XDM(Experience Data Model)에 데이터 매핑 (태그를 사용하여 이 매핑을 수행할 수 있음)

## XDM 스키마 만들기

Adobe Experience Platform에서 스키마를 만듭니다.

1. **[!UICONTROL 스키마]**>**[!UICONTROL 스키마 만들기]**&#x200B;를 선택하고 **[!UICONTROL XDM ExperienceEvent]** 옵션을 선택하여 스키마를 만듭니다.

1. 스키마에 이름과 간단한 설명을 지정합니다.

1. **[!UICONTROL 필드 그룹]** 옆에 있는 **[!UICONTROL 추가]**&#x200B;를 선택하여 &quot;ExperienceEvent 웹 세부 정보&quot; 필드 그룹을 추가할 수 있습니다.

   >[!NOTE]
   >
   >원하는 경우 여러 필드 그룹을 추가할 수 있습니다.

1. 스키마를 저장하고 지정한 이름을 메모하십시오.

스키마에 대한 자세한 내용은 [XDM(Experience Data Model) 시스템 도움말](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko-KR)을 참조하십시오.

## 이벤트 전달 속성 만들기

**[!UICONTROL Tags]** 작업 영역에서 **[!UICONTROL Edge]** 유형의 속성을 만듭니다.

1. **[!UICONTROL 새 속성]**&#x200B;을 선택합니다.

1. 속성 이름을 지정합니다.

1. &quot;Edge&quot; 플랫폼 유형을 선택합니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

속성을 만든 후 새 속성의 **[!UICONTROL 환경]** 탭으로 이동하여
환경 ID 참고 사항. 데이터 스트림에 사용된 Adobe 조직이 이벤트 전달에 사용된 Adobe 조직과 다른 경우 **[!UICONTROL 환경]** 탭에서 환경 ID를 복사하여 데이터 스트림을 만들 때 붙여 넣을 수 있습니다. 그렇지 않으면, 드롭다운 메뉴에서 환경을 선택할 수 있습니다.

## 데이터 스트림 만들기

Adobe Experience Platform에서 데이터 스트림을 생성하려면 이벤트 전달 속성을 생성할 때 생성된 환경 ID를 사용합니다.

1. 왼쪽 탐색에서 **[!UICONTROL 데이터스트림]**&#x200B;을 선택합니다.

1. 구성의 이름을 지정하고 선택적 설명을 입력합니다.
이 설명은 여러 구성이 있는 목록에서 구성을 식별하는 데 도움이 됩니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

## 이벤트 전달 활성화 {#enable-event-forwarding}

그런 다음 Edge Network을 구성하여 이벤트 전달 및 다른 Adobe 제품으로 데이터를 전송합니다.

1. **[!UICONTROL Datastreams]** 작업 영역에서 만든 속성을 선택합니다.

1. 개발, 프로덕션 또는 스테이징 환경을 선택합니다.

   또는 Adobe 조직 외부의 이벤트 전달 환경으로 데이터를 보내려면 **[!UICONTROL 고급 모드로 전환]**&#x200B;을 선택하고 ID에 붙여 넣으십시오. 이벤트 전달 속성을 만들 때 ID가 제공됩니다.

1. 필요한 도구를 전환하고 필요에 따라 구성합니다.

   * Adobe Analytics에는 보고서 세트 ID가 필요합니다.

   * Adobe Experience Platform에서 이벤트를 전달하려면 속성 ID와 환경 ID가 필요합니다. 이벤트 전달 속성에 대한 게시 경로입니다.

구성한 후 새 속성에 대한 환경 ID를 메모하십시오.

## 이전에 만든 데이터 스트림으로 데이터를 전송하도록 Experience Platform Web SDK 확장 구성

**[!UICONTROL Tags]** 작업 영역에서 속성을 만든 다음 **[!UICONTROL 확장]**(으)로 이동한 다음 카탈로그에서 Experience Platform Web SDK 확장을 선택하여 구성하고 설치합니다.

구성 옵션에 대한 자세한 내용은 [웹 SDK 확장 설명서](../../extensions/client/web-sdk/overview.md)를 참조하십시오.

## Experience Platform Web SDK으로 데이터를 전송하는 태그 규칙 만들기

위에서 설명한 사항이 적용되면 이벤트 전달 및 태그를 사용하지만 페이지에서 하나의 요청만 있으면 되는 데이터 정의, 규칙 등을 빌드합니다.

Experience Platform Web SDK 확장 및 &quot;이벤트 보내기&quot; 작업 유형을 사용하여 페이지 로드 규칙을 만듭니다.

1. **[!UICONTROL 규칙]** 탭을 연 다음 **[!UICONTROL 새 규칙 만들기]**&#x200B;를 선택합니다.

1. 규칙 이름을 지정합니다.

1. **[!UICONTROL 이벤트 추가]**&#x200B;를 선택합니다.

1. 확장을 선택하고 해당 확장에 사용할 수 있는 이벤트 유형 중 하나를 선택하여 이벤트를 추가한 다음 이벤트에 대한 설정을 구성합니다. 예를 들어 **[!UICONTROL 코어 - Window Loaded]**&#x200B;을 선택합니다.

1. Experience Platform Web SDK 확장을 사용하여 작업을 추가합니다. **[!UICONTROL 작업 유형]** 목록에서 **[!UICONTROL 이벤트 보내기]**&#x200B;를 선택하고 원하는 인스턴스(이전에 구성된 Alloy 인스턴스)를 선택한 다음 Alloy 히트 내의 XDM 데이터 블록에 추가할 데이터 요소를 선택합니다.

1. 나머지 설정은 이 예제의 기본값으로 두고 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

다른 예로, 사용자가 지정된 단추 위에 마우스 커서를 놓으면 데이터 레이어를 Edge로 보내는 규칙을 만들 수 있습니다.

## 요약

이제 다음을 적절히 사용하여 Adobe이 아닌 대상으로 데이터를 전달하는 이벤트 전달 규칙을 만들 수 있습니다.

* Experience Data Model 스키마(지정한 이름을 메모하십시오.)
* 이벤트 전달 속성(속성 ID 및 환경 ID를 추적합니다.)
* 데이터 스트림 (이벤트 전달의 환경 ID와 혼동하지 않도록 환경 ID를 참고하십시오.)
* 태그 속성
