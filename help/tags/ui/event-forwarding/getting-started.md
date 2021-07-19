---
title: 이벤트 전달 시작
description: Adobe Experience Platform에서 이벤트 전달을 사용하여 시작하려면 이 단계별 자습서를 따르십시오.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 27%

---

# 이벤트 전달 시작

>[!NOTE]
>
>Adobe Experience Platform Launch은 Experience Platform에서 데이터 수집 기술 세트로 브랜드 재지정되었습니다. 그 결과 제품 설명서에서 몇 가지 용어 변경 사항이 롤아웃되었습니다. 용어 변경 내용을 통합 참조하려면 다음 [document](../../term-updates.md)을 참조하십시오.

Adobe Experience Platform에서 이벤트 전달을 사용하려면 다음 세 가지 옵션 중 하나 이상을 사용하여 데이터를 Adobe Experience Platform Edge Network에 전송해야 합니다.

* [Adobe Experience Platform 웹 SDK](../../extensions/web/sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [서버 간 API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>Platform Web SDK 및 Platform Mobile SDK는 Adobe Experience Platform에서 태그를 통해 배포할 필요가 없습니다. 그러나 태그를 사용하여 이러한 SDK를 배포하는 것이 좋습니다.

Edge 네트워크로 데이터를 전송하면 Adobe 솔루션을 전환하여 데이터를 보낼 수 있습니다. 데이터를 Adobe이 아닌 솔루션으로 보내려면 이벤트 전달에서 이 설정을 설정하십시오.

## 전제 조건

* Adobe Experience Platform Collection Enterprise(가격 정보는 계정 관리자에게 문의)
* Adobe Experience Platform의 이벤트 전달
* Edge Network로 데이터를 전송하도록 구성된 Adobe Experience Platform 웹 또는 모바일 SDK
* 데이터를 XDM(Experience Data Model)에 매핑 (태그를 사용하여 이 매핑을 수행할 수 있음)

## XDM 스키마 만들기

Adobe Experience Platform에서 스키마를 만듭니다.

1. **[!UICONTROL 스키마]****[!UICONTROL 스키마 만들기]**&#x200B;를 선택하고 **[!UICONTROL XDM ExperienceEvent]** 옵션을 선택하여 스키마를 만듭니다.

1. 스키마에 이름과 간단한 설명을 지정합니다.

1. **[!UICONTROL 필드 그룹]** 옆에 있는 **[!UICONTROL 추가]**&#x200B;를 선택하여 &quot;ExperienceEvent 웹 세부 사항&quot; 필드 그룹을 추가할 수 있습니다.

   >[!NOTE]
   >
   >원하는 경우 여러 필드 그룹을 추가할 수 있습니다.

1. 스키마를 저장하고 지정한 이름을 확인합니다.

스키마에 대한 자세한 내용은 [XDM(Experience Data Model) 시스템 도움말](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko)을 참조하십시오.

## 이벤트 전달 속성 만들기

데이터 수집 UI에서 &quot;Edge&quot; 유형의 속성을 만듭니다.

1. **[!UICONTROL 새 속성]**&#x200B;을 선택합니다.

1. 속성 이름을 지정합니다.

1. &quot;Edge&quot; 플랫폼 유형을 선택합니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

속성을 만든 후 새 속성에 대한 **[!UICONTROL 환경]** 탭으로 이동하여
환경 ID에 대한 참고 사항. 데이터 스트림에 사용된 Adobe 조직이 이벤트 전달에 사용되는 Adobe 조직과 다른 경우 **[!UICONTROL 환경]** 탭에서 환경 ID를 복사하여 데이터 스트림을 만들 때 붙여넣을 수 있습니다. 그렇지 않으면, 드롭다운 메뉴에서 환경을 선택할 수 있습니다.

## 데이터 스트림 만들기

Adobe Experience Platform에서 데이터 스트림을 만들려면 이벤트 전달 속성을 만들 때 생성된 환경 ID를 사용합니다.

1. 데이터 수집 UI의 왼쪽 레일에 있는 링크를 사용하여 데이터 스트림 인터페이스를 엽니다.

1. **[!UICONTROL 데이터 저장소]**&#x200B;를 선택합니다.

1. 구성의 이름을 지정하고 선택적 설명을 입력합니다.
이 설명은 여러 구성이 있는 목록에서 구성을 식별하는 데 도움이 됩니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.



## 이벤트 전달 활성화

다음으로, 이벤트 전달 및 기타 Adobe 제품으로 데이터를 보내도록 Edge Network를 구성합니다.

1. 데이터 저장소 UI에서 생성한 속성을 선택합니다.

1. 개발, 프로덕션 또는 스테이징 환경을 선택합니다.

   또는 Adobe 조직 외부의 이벤트 전달 환경에 데이터를 보내려면 **[!UICONTROL 고급 모드로 전환]**&#x200B;을 선택하고 ID에 붙여넣습니다. ID는 이벤트 전달 속성을 만들 때 제공됩니다.

1. 필요한 도구를 전환하고 필요에 따라 구성합니다.

   * Adobe Analytics에는 보고서 세트 ID가 필요합니다.

   * Adobe Experience Platform에서 이벤트 전달을 사용하려면 속성 ID와 환경 ID가 필요합니다. 이벤트 전달 속성의 게시 경로입니다.

구성한 후 새 속성에 대한 환경 ID를 메모하십시오.

## 이전에 만든 데이터 스트림으로 데이터를 보내도록 태그 Web SDK 확장을 구성합니다

데이터 수집 UI에서 속성을 만든 다음 Adobe Experience Platform 웹 SDK 확장을 사용하여 구성합니다.

1. 속성 이름을 지정합니다.

   Alloy 인스턴스가 여러 개 있을 수 있습니다. 예를 들어, 다른 유료화 전 및 이후 추적 속성이 있을 수 있습니다.

1. 조직 ID를 선택합니다.

1. Edge 도메인을 선택합니다.

구성 옵션에 대한 자세한 내용은 [웹 SDK 확장 설명서](../../extensions/web/sdk/overview.md)를 참조하십시오.

## Platform Web SDK로 데이터를 전송하는 태그 규칙 만들기

위의 사항이 적용되면 이벤트 전달 및 태그를 사용하지만 페이지의 단일 요청만 필요한 데이터 정의, 규칙 등을 작성합니다.

Platform Web SDK 확장 및 &quot;이벤트 보내기&quot; 작업 유형을 사용하여 페이지 로드 규칙을 만듭니다.

1. **[!UICONTROL 규칙]** 탭을 열고 **[!UICONTROL 새 규칙 만들기]**&#x200B;를 선택합니다.

1. 규칙 이름을 지정합니다.

1. **[!UICONTROL 이벤트 추가]**&#x200B;를 선택합니다.

1. 확장을 선택하고 해당 확장에 사용할 수 있는 이벤트 유형 중 하나를 선택하여 이벤트를 추가한 다음 이벤트에 대한 설정을 구성합니다. 예를 들어 **[!UICONTROL 코어 - Window Loaded]**&#x200B;를 선택합니다.

1. Platform 웹 SDK 확장을 사용하여 작업을 추가합니다. **[!UICONTROL 작업 유형]** 목록에서 **[!UICONTROL 이벤트 보내기]**&#x200B;를 선택하고, 원하는 인스턴스(이전에 구성된 합금 인스턴스)를 선택한 다음, 합금 히트 내에서 XDM 데이터 블록에 추가할 데이터 요소를 선택합니다.

1. 이 예제의 나머지 설정을 기본값으로 두고 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

다른 예로, 사용자가 지정된 단추 위에 마우스 커서를 놓으면 데이터 레이어를 Edge로 보내는 규칙을 만들 수 있습니다.

## 요약

이제 다음을 통해 데이터를 비Adobe 대상으로 전달하는 이벤트 전달 규칙을 만들 수 있습니다.

* 경험 데이터 모델 스키마(지정한 이름을 확인합니다.)
* 이벤트 전달 속성(속성 ID 및 환경 ID를 추적합니다.)
* 데이터 스트림(이벤트 전달의 환경 ID와 혼동하지 않도록 환경 ID를 확인합니다.)
* 태그 속성
