---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;웹 페이지 정보;데이터 유형;데이터 유형;데이터 유형;웹 페이지
solution: Experience Platform
title: 웹 페이지 세부 사항 데이터 유형
description: 이 문서에서는 웹 페이지 세부 사항 XDM(Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 3%

---

# [!UICONTROL 웹 페이지 세부 사항] 데이터 유형

[!UICONTROL 웹 페이지 세부 사항] 는 ExperienceEvent가 기록한 대로 방금 로드 및 본 웹 페이지에 대한 세부 사항을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

데이터 유형은 SPA(단일 페이지 웹 애플리케이션)의 전체 페이지 세부 사항 및 초기 페이지 로드를 위한 것입니다. 새 페이지 로드를 트리거하지 않는 로드된 페이지에서 발생하는 상호 작용에 대해서는 를 참조하십시오. [웹 상호 작용](./web-interaction.md) 데이터 유형.

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL 측정]](./measure.md) | 웹 페이지에 대한 보기 수. |
| `URL` | 문자열 | 웹 페이지의 정규적이거나 일반적인 URL입니다. 페이지에 도달하는 데 사용되는 실제 URL일 수도 있고 아닐 수도 있습니다. 페이지 사용에 도달하는 데 사용되는 URL을 기록하려면 `webLink`. URI 형식은 [RFC 3986](https://tools.ietf.org/html/rfc3986) 표준. |
| `isErrorPage` | 부울 | 이 속성은 플래그를 사용하여 페이지가 오류 페이지인지 여부를 나타냅니다. 이 플래그는 웹 상호 작용을 광범위하게 분류하는 데 사용됩니다. 오류는 애플리케이션에서 정의하며, HTTP 오류 코드가 있는 페이지에 해당합니다. |
| `isHomePage` | 부울 | 이 속성은 플래그를 사용하여 페이지가 홈 페이지인지 여부를 나타냅니다. 이 플래그는 웹 상호 작용을 광범위하게 분류하는 데 사용됩니다. 홈 페이지의 정의는 애플리케이션에 의해 결정됩니다. |
| `name` | 문자열 | 웹 페이지의 규범적 이름입니다. 이 이름이 반드시 페이지 제목이거나 페이지 컨텐츠와 직접 연결될 필요는 없지만, 분류를 위해 사이트의 페이지를 구성하는 데 사용됩니다. |
| `server` | 문자열 | 웹 페이지를 호스트하는 수직 또는 일반적인 서버입니다. 페이지 상호 작용을 실제로 제공한 호스트 또는 서버일 수도 있고 그렇지 않을 수도 있습니다. |
| `siteSection` | 문자열 | 이 웹 페이지가 있는 사이트 섹션의 수직 이름입니다. 상호 작용을 분류하거나 분류하는 데 사용할 수 있습니다. |
| `viewName` | 문자열 | 페이지 내에 있는 보기의 이름입니다. 이 속성은 일반적으로 페이지 레이아웃의 대부분을 변경하는 탭 또는 컨트롤이 있는 단일 페이지 애플리케이션이나 페이지에서 사용됩니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
