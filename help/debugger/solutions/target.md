---
title: Adobe Experience Platform Debugger를 사용하여 Adobe Target 구현 테스트
description: Adobe Experience Platform Debugger를 사용하여 Adobe Target에서 활성화된 웹 사이트를 테스트하고 디버깅하는 방법을 알아봅니다.
exl-id: f99548ff-c6f2-4e99-920b-eb981679de2d
source-git-commit: c3b5b63767a934be16a479d04853e1250b3bf775
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 4%

---

# Adobe Experience Platform Debugger를 사용하여 Adobe Target 구현 테스트

Adobe Experience Platform Debugger는 Adobe Target 구현과 연결된 웹 사이트를 테스트하고 디버깅하는 데 유용한 도구 모음을 제공합니다. 이 안내서에서는 Target이 활성화된 웹 사이트에서 Platform Debugger를 사용하기 위한 몇 가지 일반적인 워크플로우 및 모범 사례를 다룹니다.

## 전제 조건

Target에 Platform Debugger를 사용하려면 웹 사이트에서 [at.js 라이브러리](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) 버전 1.x 이상 이전 버전은 지원되지 않습니다.

## Platform Debugger 초기화

브라우저에서 테스트할 웹 사이트를 연 다음 Platform Debugger 확장을 엽니다.

선택 **[!DNL Target]** 왼쪽 탐색. Platform Debugger가 사이트에서 호환되는 at.js 버전이 실행 중임을 감지하면 Adobe Target 구현 세부 사항이 표시됩니다.

![Platform Debugger에서 선택된 Target 보기로, 현재 표시된 브라우저 페이지에서 Adobe Target이 활성 상태임을 나타냅니다.](../images/solutions/target/target-initialized.png)

## 전역 구성 정보

구현의 전역 구성에 대한 정보는 Platform Debugger의 Target 보기 맨 위에 표시됩니다.

![Platform Debugger 내에서 강조 표시된 Target에 대한 전역 구성 정보](../images/solutions/target/global-config.png)

| 이름 | 설명 |
| --- | --- |
| 클라이언트 코드 | 조직을 식별하는 고유 ID입니다. |
| 버전 | 현재 웹 사이트에 설치된 Adobe Target 라이브러리의 버전입니다. |
| 전역 요청 이름 | 의 이름입니다. [글로벌 mbox](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) Target 구현의 경우 기본 이름은 입니다. `target-global-mbox`. |
| 페이지 로드 이벤트 | 다음 여부를 나타내는 부울 값 [페이지 로드 이벤트](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) 이(가) 발생했습니다. 페이지 로드 이벤트는 at.js 2.x에 대해서만 지원됩니다. 호환되지 않는 버전의 경우, 이 값은 기본적으로 로 설정됩니다. `None`. |

{style="table-layout:auto"}

## [!DNL Network Requests] {#network}

선택 **[!DNL Network Requests]** 페이지에서 수행된 각 네트워크 요청에 대한 요약 정보를 보려면 다음을 수행하십시오.

![다음 [!DNL Network Requests] platform Debugger 내에서 선택한 Target에 대한 섹션](../images/solutions/target/network-requests.png)

페이지에서 작업(페이지 다시 로드 포함)을 수행하면 새 열이 표에 자동으로 추가되므로 작업의 시퀀스와 각 요청 간 값이 변경되는 방법을 볼 수 있습니다.

![다음 [!DNL Network Requests] platform Debugger 내에서 선택한 Target에 대한 섹션](../images/solutions/target/new-request.png)

다음 값이 캡처됩니다.

| 이름 | 설명 |
| --- | --- |
| [!DNL Page Title] | 이 요청을 시작한 페이지의 제목입니다. |
| [!DNL Page URL] | 요청을 시작한 페이지의 URL입니다. |
| [!DNL URL] | 요청의 원시 URL. |
| [!DNL Method] | 요청에 대한 HTTP 메서드. |
| [!DNL Query String] | URL에서 가져온 요청의 쿼리 문자열입니다. |
| [!DNL POST Body] | 요청 본문(POST 요청에 대해서만 설정됨). |
| [!DNL Pathname] | 요청 URL의 경로 이름입니다. |
| [!DNL Hostname] | 요청 URL의 호스트 이름입니다. |
| [!DNL Domain] | 요청 URL의 도메인입니다. |
| [!DNL Timestamp] | 브라우저의 시간대 내에서 요청(또는 이벤트)이 발생한 시점의 타임스탬프입니다. |
| [!DNL Time Since Page Load] | 요청 시 페이지가 처음 로드된 이후 경과된 시간입니다. |
| [!DNL Initiator] | 요청 개시자입니다. 즉, 누가 요청을 했는가? |
| [!DNL clientCode] | Target이 인식하는 조직 계정의 식별자입니다. |
| [!DNL requestType] | 요청에 사용된 API입니다. at.js 1.x를 사용하는 경우 값은 다음과 같습니다. `/json`. at.js 2.x를 사용하는 경우 값은 다음과 같습니다. `delivery`. |
| [!DNL Audience Manager Blob] | &quot;blob&quot;이라고도 하는 암호화된 Audience Manager 메타데이터에 대한 정보를 제공합니다. |
| [!DNL Audience Location Hint] | 데이터 수집 지역 ID. 특정 ID 서비스 데이터 센터의 지리적 위치에 대한 숫자 식별자입니다. 자세한 내용은 다음 Audience Manager 설명서를 참조하십시오. [DCS 지역 ID, 위치 및 호스트 이름](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=ko-KR) 및 의 Experience Cloud ID 서비스 안내서 [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=en#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | 브라우저 높이(픽셀 단위)입니다. |
| [!DNL Browser Time Offset] | 시간대와 연결된 브라우저의 시간 오프셋입니다. |
| [!DNL Browser Width] | 브라우저 너비(픽셀 단위)입니다. |
| [!DNL Color Depth] | 화면의 색상 깊이입니다. |
| [!DNL context] | 화면 차원 및 클라이언트 플랫폼을 포함하여 요청을 하는 데 사용되는 브라우저에 대한 컨텍스트 정보가 포함된 객체입니다. |
| [!DNL prefetch] | 다음 기간 동안에서 사용되는 매개 변수 `prefetch` 처리 중입니다. |
| [!DNL execute] | 다음 기간 동안 사용되는 매개변수 `execute` 처리 중입니다. |
| [!DNL Experience Cloud Visitor ID] | 하나가 감지되면 는 [Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) 현재 사이트 방문자에게 할당됩니다. |
| [!DNL experienceCloud] | 이 특정 사용자 세션(A4T)의 Experience Cloud ID를 보유합니다. [보조 데이터 ID](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A), 및 [방문자 ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html). |
| [!DNL id] | 다음 [TARGET ID](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) 방문자용입니다. |
| [!DNL Mbox Host] | 다음 [호스트](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Target 요청이 수행된 대상입니다. |
| [!DNL Mbox PC] | 다음을 캡슐화하는 문자열 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 세션 ID 및 [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) 위치 힌트. 이 값은 at.js에서 세션 및 에지 위치가 고정된 상태를 유지하도록 하는 데 사용됩니다. |
| [!DNL Mbox Referrer] | 특정 항목의 URL 레퍼러 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 요청. |
| [!DNL Mbox URL] | 에 대한 URL [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 서버입니다. |
| [!DNL Mbox Version] | 버전 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 사용 중입니다. |
| [!DNL mbox3rdPartyId] | 다음 [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 현재 방문자에게 할당되었습니다. |
| [!DNL mboxRid] | 다음 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 요청 ID. |
| [!DNL requestId] | 요청에 대한 고유 ID. |
| [!DNL Screen Height] | 화면의 픽셀 단위 높이입니다. |
| [!DNL Screen Width] | 화면의 픽셀 단위 폭입니다. |
| [!DNL Supplemental Data ID] | 방문자를 해당 Adobe Target 및 Adobe Analytics 호출과 일치시키는 데 사용되는 시스템 생성 ID입니다. 다음을 참조하십시오. [A4T 문제 해결 안내서](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) 추가 정보. |
| [!DNL vst] | 다음 [Experience Cloud ID 서비스 API 구성](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html). |
| [!DNL webGLRenderer] | 페이지에서 사용되는 WebGL 렌더러에 대한 정보를 제공합니다(해당하는 경우). |

{style="table-layout:auto"}

특정 네트워크 이벤트에 대한 매개변수의 세부 정보를 보려면 해당 테이블 셀을 선택합니다. 설명 및 해당 값을 포함하여 매개 변수에 대한 추가 정보를 제공하는 팝오버가 나타납니다. 값이 JSON 객체인 경우 대화 상자에 객체 구조에 대한 탐색 가능한 보기가 포함됩니다.

![다음 [!DNL Network Requests] platform Debugger 내에서 선택한 Target에 대한 섹션](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

선택 **[!DNL Configuration]** Target을 위해 추가 디버깅 도구 선택을 활성화하거나 비활성화합니다.

![다음 [!DNL Configuration Requests] platform Debugger 내에서 선택한 Target에 대한 섹션](../images/solutions/target/configuration.png)

| 디버깅 도구 | 설명 |
| --- | --- |
| [!DNL Target Console Logging] | 활성화되면 브라우저의 콘솔 탭에서 at.js 로그에 액세스할 수 있습니다. 이 기능은 를 추가하여 활성화할 수도 있습니다 `mboxDebug` 브라우저 URL에 대한 매개 변수(임의 값 포함)를 쿼리합니다. |
| [!DNL Target Diable] | 활성화되면 페이지에서 모든 Target 기능이 비활성화됩니다. 이 확장은 페이지별 오퍼가 Target에서 문제를 일으키는 원인인지 확인하는 데 사용할 수 있습니다. |
| [!DNL Target Trace] | **참고**: 이 기능을 사용하려면 로그인해야 합니다.<br><br>활성화되면 모든 퀘스트와 함께 추적 토큰이 전송되고 각 응답에서 추적 개체가 반환됩니다. `at.js` 응답을 구문 분석합니다 `window.__targetTraces`. 각 추적 개체에는 [[!DNL Network Requests] tab] 아래에 추가 항목이 있습니다.<ul><li>요청 전후의 속성을 볼 수 있는 프로필 스냅숏입니다.</li><li>일치함 및 일치하지 않음 [활동](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html)현재 프로필이 특정 활동에 자격이 되거나 되지 않는 이유를 보여 줍니다.<ul><li>이렇게 하면 프로필이 특정 시점에 대해 자격이 있는 대상과 그 이유를 식별하는 데 도움이 될 수 있습니다.</li><li>Target 문서에는 다양한 활동 유형에 대한 자세한 정보가 포함되어 있습니다.</li></ul></li></ul> |

{style="table-layout:auto"}
