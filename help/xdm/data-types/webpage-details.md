---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;웹 페이지 세부 정보;데이터 유형;데이터 유형;데이터 유형;웹 페이지
solution: Experience Platform
title: 웹 페이지 세부 정보 데이터 유형
description: 이 문서에서는 XDM(Experience Data Model) 데이터 유형 웹 페이지 세부 사항에 대한 개요를 제공합니다.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# [!UICONTROL 웹 페이지 세부 정보] 데이터 유형

[!UICONTROL 웹 페이지 세부 정보] 는 ExperienceEvent로 기록된 대로 로드 및 표시된 웹 페이지에 대한 세부 사항을 설명하는 표준 Experience Data Model(XDM) 데이터 유형입니다.

데이터 유형은 단일 페이지 웹 애플리케이션(SPA)의 전체 페이지 세부 사항 및 초기 페이지 로드를 위한 것입니다. 새 페이지 로드를 트리거하지 않는 로드된 페이지에서 발생하는 상호 작용의 경우 [웹 인터랙션](./web-interaction.md) 데이터 유형.

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL 측정]](./measure.md) | 웹 페이지의 조회수. |
| `URL` | 문자열 | 웹 페이지의 표준 또는 일반 URL. 이는 페이지에 도달하기 위해 사용되는 실제 URL이거나 아닐 수 있습니다. 페이지 사용 도달 시 사용한 URL을 기록하려면 `webLink`. URI 형식은 다음을 따라야 합니다. [RFC 3986](https://tools.ietf.org/html/rfc3986) 표준. |
| `isErrorPage` | 부울 | 이 속성은 플래그를 사용하여 페이지가 오류 페이지인지 여부를 나타냅니다. 이 플래그는 웹 상호 작용을 광범위하게 분류하는 데 사용됩니다. 오류는 애플리케이션에서 정의되며, HTTP 오류 코드와 함께 제공되는 페이지에 해당할 수 있습니다. |
| `isHomePage` | 부울 | 이 속성은 플래그를 사용하여 페이지가 홈 페이지인지 여부를 나타냅니다. 이 플래그는 웹 상호 작용을 광범위하게 분류하는 데 사용됩니다. 홈 페이지의 정의는 애플리케이션에 의해 결정됩니다. |
| `name` | 문자열 | 웹 페이지의 표준 이름. 이 이름은 페이지 제목이 아니거나 페이지 콘텐츠와 직접 연결되는 것은 아니지만 분류 목적으로 사이트의 페이지를 구성하는 데 사용됩니다. |
| `server` | 문자열 | 웹 페이지를 호스팅하는 표준 또는 일반 서버. 이는 실제로 페이지 상호 작용을 제공하는 호스트 또는 서버일 수도 있고 아닐 수도 있습니다. |
| `siteSection` | 문자열 | 이 웹 페이지가 있는 사이트 섹션의 표준 이름입니다. 이는 상호 작용을 분류하거나 범주화하는 데 사용할 수 있다. |
| `viewName` | 문자열 | 페이지 내의 보기 이름입니다. 이 속성은 일반적으로 단일 페이지 애플리케이션이나 대부분의 페이지 레이아웃을 변경하는 탭 또는 컨트롤이 있는 페이지에서 사용됩니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
