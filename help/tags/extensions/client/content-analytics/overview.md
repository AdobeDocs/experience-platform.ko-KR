---
title: Adobe Content Analytics 확장 개요
description: Adobe Experience Platform의 Adobe Content Analytics 태그 확장에 대해 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: d6288d9515d7efaf874cb056f06d04b2002fd369
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Adobe Content Analytics 확장 개요

[!DNL Adobe Content Analytics] 태그 확장을 사용하면 웹 사이트에서 콘텐츠 관련 이벤트를 추적할 수 있습니다. 확장은 웹 속성에서 Experience Platform Edge Network을 통해 Adobe Experience Cloud의 데이터 스트림으로 컨텐츠 데이터(경험 및 자산)를 전송합니다.

확장을 사용하면 특정 콘텐츠 관련 이벤트 데이터를 Platform으로 스트리밍하여 Customer Journey Analytics의 콘텐츠 분석 보고서에서 해당 데이터를 사용할 수 있습니다.

이 문서에서는 태그 UI에서 태그 확장을 구성하는 방법을 설명합니다.

## Adobe Content Analytics 태그 확장 설치 {#install}

>[!NOTE]
>
>Adobe Content Analytics 태그 확장은 [Content Analytics 안내 구성 마법사](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided){target="_blank"}를 사용할 때 자동으로 만들어지는 태그 속성의 일부로 자동으로 설치됩니다.


### 수동 설치

수동 구성의 경우 Adobe Content Analytics 태그 확장 기능을 설치하려면 속성이 설치되어 있어야 합니다. 아직 작성하지 않았다면 [태그 속성 만들기](https://experienceleague.adobe.com/en/docs/platform-learn/implement-in-websites/configure-tags/create-a-property)에 대한 설명서를 참조하십시오.

속성을 만들었거나 [Content Analytics 안내 구성 마법사](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided)를 사용하여 만든 속성을 선택한 후 속성을 열고 왼쪽 막대에서 **[!UICONTROL 확장]** 탭을 선택합니다.

**[!UICONTROL 카탈로그]** 탭을 선택합니다. 사용 가능한 확장 목록에서 **[!DNL Adobe Content Analytics]** 확장을 찾아 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![웹 SDK 확장이 선택된 태그 UI를 표시하는 이미지](assets/aca-tag-install.png)

**[!UICONTROL 설치]**&#x200B;를 선택한 후 Adobe Content Analytics 태그 확장을 구성하고 구성을 저장해야 합니다.


<!--
## Configure schema

The [Content Analytics guided configuration wizard](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) automatically populates the proper value for the **[!UICONTROL Tenant Schema Name]**. 

![Image that shows the Schema configuration of the Adobe Content Analytics tag extension in the Tags UI](assets/aca-tag-schema.png)

>[!WARNING]
>
>Do not modify the value for **[!UICONTROL Tenant Schema Name]**.

-->

## 데이터스트림 구성

[콘텐츠 분석 안내 구성 마법사](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided)가 **[!UICONTROL 샌드박스]** 및 **[!UICONTROL 프로덕션 데이터스트림]**&#x200B;에 대해 적절한 값을 자동으로 선택합니다. 필요에 따라 추가 **[!UICONTROL 스테이징 데이터스트림]** 및 **[!UICONTROL 개발 데이터스트림]**&#x200B;을 구성할 수 있습니다.

![태그 UI에서 Adobe Content Analytics 태그 확장의 데이터 스트림 구성을 보여 주는 이미지](assets/aca-tag-datastreams.png)

다른 샌드박스와 다른 데이터스트림에서 Content Analytics를 사용하려는 경우 **[!UICONTROL 샌드박스]** 및 **[!UICONTROL 프로덕션 데이터스트림]**&#x200B;에 대해 자동으로 선택된 값을 재정의할 수 있습니다. 이 경우 사용 가능한 드롭다운 메뉴에서 샌드박스 및 데이터스트림을 선택하거나 **[!UICONTROL 값 입력]**&#x200B;을 선택하고 각 환경에 대한 사용자 지정 데이터스트림 ID를 입력할 수 있습니다.

>[!IMPORTANT]
>
>다른 샌드박스 및 데이터스트림을 구성할 때
>
>* 선택한 샌드박스가 다른 Content Analytics 구성과 연결되어 있지 않습니다.
>* 선택한 모든 데이터 스트림에는 활성화된 Content Analytics 경험 이벤트 데이터 세트로 구성된 Experience Platform 서비스가 있습니다.

데이터 스트림을 구성하는 방법을 알아보려면 [데이터 스트림](../../../../datastreams/overview.md)의 안내서를 참조하십시오.



## 이벤트 필터링 구성

**[!UICONTROL 이벤트 필터링]** 섹션에서 콘텐츠 분석에 대한 데이터를 수집할 때 정규식을 수정하여 **[!UICONTROL 페이지 URL]** 및 **[!UICONTROL Assets URL]**&#x200B;을(를) 필터링할 수 있습니다. [Content Analytics 안내 구성 마법사](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided)에서 정의한 정규식이 자동으로 채워집니다.

![태그 UI에서 Adobe Content Analytics 태그 확장의 이벤트 필터링 설정을 보여 주는 이미지](assets/aca-tag-eventfiltering.png)


### 예시

* 컨텐츠 분석에서 모든 문서 페이지를 제외하려고 합니다.<br/>다음 정규식을 사용합니다. `^(?!.*documentation).*`
* Content Analytics에서 모든 로고 JPEG 및 SVG 이미지를 제외합니다.<br/>다음 정규식을 사용합니다. `^(?!.*(logo\.jpg|\.svg)).*$`

**[!UICONTROL 정규 표현식 테스트]**&#x200B;를 사용하여 **[!UICONTROL 정규 표현식 테스터]**&#x200B;에서 정규 표현식을 테스트할 수 있습니다.

![Tags UI에서 Adobe Content Analytics 태그 확장의 정규 표현식 테스터를 보여 주는 이미지](assets/aca-tag-regextester.png)

