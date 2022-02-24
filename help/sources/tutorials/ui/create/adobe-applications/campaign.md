---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;캠페인;캠페인 관리 서비스
title: Platform UI를 사용하여 Adobe Campaign Managed Services 소스 연결 만들기
description: Platform UI를 사용하여 Adobe Experience Platform을 Adobe Campaign Managed Services에 연결하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: 57a34b10e40dee80638392477d49c21e107c491f
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---


# Platform UI를 사용하여 Adobe Campaign Managed Services 소스 연결 만들기

이 자습서에서는 Adobe Campaign Managed Services 데이터를 Adobe Experience Platform으로 가져오기 위한 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 안내서에서는 Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): 플랫폼을 사용하면 다양한 소스에서 데이터를 수집할 수 있으며 다음을 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공할 수 있습니다 [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): 플랫폼은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## Platform에 Adobe Campaign Managed Services 연결

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 검색 창을 사용하여 표시된 소스 범위를 좁힐 수도 있습니다.

아래에 **[!UICONTROL Adobe 애플리케이션]** 카테고리, 선택 **[!UICONTROL Adobe Campaign Managed Services]** 그런 다음 **[!UICONTROL 데이터 추가]**.

### 데이터 선택 {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="ACC 인스턴스"
>abstract="사용할 Adobe Campaign Classic 환경의 이름입니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="대상 매핑"
>abstract="타겟 매핑은 메시지를 전달하기 위해 Campaign에서 사용하는 기술 개체이며 게재를 보내는 데 필요한 모든 기술 설정(주소, 전화 번호, 옵트인 지표, 추가 식별자...)을 포함합니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="스키마 이름"
>abstract="Adobe Campaign 데이터베이스에 정의된 엔터티의 이름입니다."
>text="Learn more in documentation"

다음 [!UICONTROL 데이터 선택] 단계가 나타나고, 사용자 인터페이스에 대한 값을 구성할 수 있는 인터페이스가 제공됩니다 [!UICONTROL Adobe Campaign 인스턴스], [!UICONTROL 대상 매핑], 및 [!UICONTROL 스키마 이름].
