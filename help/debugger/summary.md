---
title: 요약 탭
description: Adobe Experience Platform Debugger에서 요약 탭을 사용하는 방법에 대해 알아봅니다.
keywords: debugger;experience Platform Debugger 확장 프로그램;chrome;확장 프로그램;요약;지우기;요청;요약 화면;솔루션;정보;analytics;target;dtm;audience manager;launch;id 서비스
seo-description: Experience Platform Debugger Summary Screen
seo-title: Summary Tab
uuid: 46b17eaa-b611-43cf-8c6a-67b2e9b9d940
exl-id: 91234125-15c4-4111-9ee4-f3af093a3c4d
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 85%

---

# 요약 탭

Adobe Experience Platform Debugger을 실행하려면 브라우저에서 검사할 페이지를 연 다음 브라우저 모음에서 아이콘(![](images/start-icon.jpg))을 선택합니다. 확장은 **요약** 탭에서 열립니다.

![](images/summary.jpg)

이 화면에서는 각 Adobe Experience Cloud 솔루션에 대한 정보를 보여 줍니다. 표시되는 정보는 솔루션마다 다르지만, 일반적으로 솔루션 라이브러리 및 버전(예: &quot;AppMeasurement v2.9&quot;)과 계정 식별자(예: Analytics 보고서 세트 ID, Target 클라이언트 코드, Audience Manager 파트너 ID 등) 등의 정보를 포함합니다.

## Experience Platform Debugger에 표시된 정보

Experience Platform Debugger에는 각 솔루션에 대한 다음 정보가 표시됩니다.

**Adobe Analytics**

<table id="table_BEB9CC58E59D4D86BC895A8A51D84A2C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>보고서 세트 </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/ko_KR/reference/report_suites_admin.html" format="html" scope="external">보고서 세트</a>는 선택한 웹 사이트, 웹 사이트 집합 또는 웹 페이지의 하위 집합에 대한 전체적이고 독립적인 보고를 정의합니다 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>버전 </p> </td> 
   <td colname="col2"> <p>페이지에 대해 정의된 <a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ko-KR" format="html" scope="external"> AppMeasurement</a> 버전입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>방문자 버전 </p> </td> 
   <td colname="col2"> <p><a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html" format="html" scope="external"> 방문자 ID</a> 라이브러리의 버전입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>페이지 이름 </p> </td> 
   <td colname="col2"> <p>Analytics로 보낸 <a href="https://experiencecloud.adobe.com/resources/help/ko_KR/sc/implement/pageName.html" format="html" scope="external"> pageName</a> 변수로, 사이트에 대한 친화적인 이름이 들어 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>모듈 </p> </td> 
   <td colname="col2"> <p>Adobe Analytics에서 로드한 모듈입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Audience Manager**

<table id="table_784AEABADBDA4D14BB9A7A9CB9EF07C3"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>파트너 </p> </td> 
   <td colname="col2"> <p>DIL 인스턴스에 대한 <a href="https://experiencecloud.adobe.com/resources/help/ko_KR/aam/r_dil_get_partner.html" format="html" scope="external"> 파트너 이름</a>입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>버전 </p> </td> 
   <td colname="col2"> <p>DIL 인스턴스에 대한 <a href="https://experiencecloud.adobe.com/resources/help/ko_KR/aam/r_api_return_versions_dil.html" format="html" scope="external"> 버전 번호</a>입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>UUID </p> </td> 
   <td colname="col2"> <p>DIL 인스턴스와 연결된 <a href="https://experiencecloud.adobe.com/resources/help/ko_KR/aam/ids-in-aam.html" format="html" scope="external"> 고유 사용자 ID</a>입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform 태그**

<table id="table_E9574975444A407887E26514D1BB1601"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>이름 </p> </td> 
   <td colname="col2"> <p>태그 <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html" format="https" scope="external"> 속성</a>의 이름 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>버전 </p> </td> 
   <td colname="col2"> <p>Turbine</a>의 버전 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>빌드 날짜 </p> </td> 
   <td colname="col2"> <p>태그 <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html" format="https" scope="external"> 라이브러리</a> 빌드 날짜 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>환경 </p> </td> 
   <td colname="col2"> <p>태그 라이브러리에서 사용하는 <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=ko-KR" format="https" scope="external"> 환경</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>확장 </p> </td> 
   <td colname="col2"> <p>페이지에서 사용되는 확장 프로그램 </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform 웹 SDK**

<table id="table_DC76D63FA6EF4891906B9E1D3E4A8A6C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>라이브러리 버전 </p> </td> 
   <td colname="col2"> <p>Adobe Experience Platform 웹 SDK <a href="https://experienceleague.adobe.com/docs/experience-platform/web-sdk/extension/web-sdk-ext-release-notes.html" format="html" scope="external">라이브러리 버전</a>의 번호 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>네임스페이스</p> </td> 
   <td colname="col2"> <p>확장 프로그램에서 식별된 이름</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>속성 ID </p> </td> 
   <td colname="col2"> <p>확장에 지정된 태그 속성의 이름 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Edge 도메인 </p> </td> 
   <td colname="col2"> <p>Adobe Experience Platform 확장 프로그램에서 데이터를 보내고 받는 도메인입니다 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>IMS 조직 ID </p> </td> 
   <td colname="col2"> <p>확장 프로그램에 지정된 대로 Adobe에서 데이터를 전송하려는 조직 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>로깅 활성화됨 </p> </td> 
   <td colname="col2"> <p>이 속성에 대해 로깅을 활성화했는지 아닌지를 지정합니다</p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Cloud ID 서비스**

<table id="table_274CFCEFA8F34D16BB546B4669EC0209"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Experience Cloud 조직 ID </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/ko_KR/mcvid/" format="https" scope="external"> 조직 ID</a>입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>버전 </p> </td> 
   <td colname="col2"> <p><a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html" format="html" scope="external"> 방문자 ID</a> 라이브러리의 버전입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Target**

<table id="table_D30E0CD20FB04E41862B22655136E043"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>클라이언트 코드 </p> </td> 
   <td colname="col2"> <p>Target <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/deploy-at-js/implementing-target-without-a-tag-manager.html" format="html" scope="external"> 클라이언트 코드 </a>입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>버전 </p> </td> 
   <td colname="col2"> <p>현재 <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/target-atjs-versions.html" format="html" scope="external"> at.js</a> 또는 mbox.js 버전입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>전역 요청 이름 </p> </td> 
   <td colname="col2"> <p><a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> 글로벌 mbox</a>는 Target 구현의 각 웹 페이지 맨 위에서 수행된 단일 서버 호출을 나타냅니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>페이지 로드 이벤트 </p> </td> 
   <td colname="col2"> <p>페이지가 로드될 때 실행되는 <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html" format="html" scope="external">이벤트</a> 유형 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>요청 이름 </p> </td> 
   <td colname="col2"> <p>페이지에서 <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> 위치</a> 주위에 있는 요청 이름입니다. 코드 또는 태그 관리자에서 디버깅 이벤트 리스너를 구현하고 Target UI에서 필요한 <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> 응답 토큰</a>을 켜는 경우에만 인증 없이 사용할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>활동 이름 </p> </td> 
   <td colname="col2"> <p>Target <a href="https://experienceleague.adobe.com/docs/target/using/activities/activities.html" format="html" scope="external"> 캠페인 또는 활동</a>의 이름입니다. 코드 또는 태그 관리자에서 디버깅 이벤트 리스너를 구현하고 Target UI에서 필요한 <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> 응답 토큰</a>을 켜는 경우에만 인증 없이 사용할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>활동 ID </p> </td> 
   <td colname="col2"> <p>Target 활동의 ID입니다. 코드 또는 태그 관리자에서 디버깅 이벤트 리스너를 구현하고 Target UI에서 필요한 <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> 응답 토큰</a>을 켜는 경우에만 인증 없이 사용할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>경험 이름 </p> </td> 
   <td colname="col2"> <p>Target <a href="https://experienceleague.adobe.com/docs/target/using/experiences/experiences.html" format="html" scope="external"> 경험</a>의 이름입니다. 코드 또는 태그 관리자에서 디버깅 이벤트 리스너를 구현하고 Target UI에서 필요한 <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> 응답 토큰</a>을 켜는 경우에만 인증 없이 사용할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>경험 ID </p> </td> 
   <td colname="col2"> <p>Target 경험의 ID입니다. 코드 또는 태그 관리자에서 디버깅 이벤트 리스너를 구현하고 Target UI에서 필요한 <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> 응답 토큰</a>을 켜는 경우에만 인증 없이 사용할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>오퍼 이름</p> </td> 
   <td colname="col2"> <p>Target <a href="https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html" format="html" scope="external"> 오퍼</a>의 이름입니다. 코드 또는 태그 관리자에서 디버깅 이벤트 리스너를 구현하고 Target UI에서 필요한 <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> 응답 토큰</a>을 켜는 경우에만 인증 없이 사용할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>오퍼 ID </p> </td> 
   <td colname="col2"> <p>Target 오퍼의 ID입니다. 코드 또는 태그 관리자에서 디버깅 이벤트 리스너를 구현하고 Target UI에서 필요한 <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> 응답 토큰</a>을 켜는 경우에만 인증 없이 사용할 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
