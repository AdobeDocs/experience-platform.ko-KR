---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;웹 페이지 정보;데이터 유형;데이터 유형;웹 페이지
solution: Experience Platform
title: 웹 페이지 세부 사항 데이터 유형
topic-legacy: overview
description: 이 문서에서는 웹 페이지 세부 정보 XDM(Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 2%

---

# [!UICONTROL Web page details] 데이터 유형

[!UICONTROL Web page details] 는 ExperienceEvent에 의해 기록되는 대로, 로드 및 본 웹 페이지에 대한 세부 사항을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

데이터 유형은 단일 페이지 웹 애플리케이션(SPA)의 전체 페이지 세부 사항 및 초기 페이지 로드를 대상으로 합니다. 새 페이지 로드를 트리거하지 않는 로드된 페이지에서 발생하는 상호 작용에 대해서는 [웹 상호 작용](./web-interactions.md) 데이터 유형을 참조하십시오.

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Measure]](./measure.md) | 웹 페이지의 보기 수. |
| `URL` | 문자열 | 웹 페이지의 표준 또는 일반적인 URL입니다. 페이지에 도달하는 데 사용되는 실제 URL일 수도 있고 아닐 수도 있습니다. 페이지에 도달하는 데 사용되는 URL을 기록하려면 `webLink`을 사용합니다. URI 형식은 [RFC 3986](https://tools.ietf.org/html/rfc3986) 표준을 따라야 합니다. |
| `isErrorPage` | 부울 | 이 속성은 페이지가 오류 페이지인지 여부를 나타내는 플래그를 사용합니다. 이 플래그는 웹 상호 작용을 폭넓게 분류하는 데 사용됩니다. 이 오류는 응용 프로그램에서 정의하며 HTTP 오류 코드와 함께 제공되는 페이지에 해당될 수 있습니다. |
| `isHomePage` | 부울 | 이 속성은 페이지가 홈 페이지인지 여부를 나타내는 플래그를 사용합니다. 이 플래그는 웹 상호 작용을 폭넓게 분류하는 데 사용됩니다. 홈 페이지의 정의는 응용 프로그램에 의해 결정됩니다. |
| `name` | 문자열 | 웹 페이지의 표준 이름입니다. 이 이름이 페이지 제목이거나 페이지 컨텐츠와 직접 연결할 필요는 없지만 분류를 위해 사이트의 페이지를 구성하는 데 사용됩니다. |
| `server` | 문자열 | 웹 페이지를 호스트하는 표준 또는 일반 서버. 이것은 실제로 페이지 상호 작용을 제공한 호스트 또는 서버일 수도 있고 아닐 수도 있습니다. |
| `siteSection` | 문자열 | 이 웹 페이지가 있는 사이트 섹션의 표준 이름입니다. 상호 작용을 분류하거나 분류하는 데 사용할 수 있습니다. |
| `viewName` | 문자열 | 페이지 내의 보기 이름. 이 속성은 페이지 레이아웃의 대부분을 변경하는 탭 또는 컨트롤이 있는 단일 페이지 응용 프로그램 또는 페이지에 일반적으로 사용됩니다. |

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.example.2.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.schema.json)
