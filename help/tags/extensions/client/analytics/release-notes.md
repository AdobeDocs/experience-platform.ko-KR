---
title: Adobe Analytics 확장 기능 릴리스 노트
description: Adobe Experience Platform의 Adobe Analytics 태그 확장 기능에 대한 최신 릴리스 정보입니다.
exl-id: 3c7b4ec0-4b81-4ef4-b15f-6ad102525840
source-git-commit: 5f4e157a39bf927b3821931d55f968862b2ed16d
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 65%

---

# Adobe Analytics 확장 릴리스 노트

다음은 Adobe Analytics 태그 확장에 대한 릴리스 노트 목록입니다.

>[!NOTE]
>
>Analytics 태그 확장(종종 [AppMeasurement JavaScript 라이브러리](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ko-KR) 업데이트에 대한 응답으로 업데이트되는 경우). 아래 언급된 특정 버전에 대한 자세한 내용은 [AppMeasurement 릴리스 정보](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=ko-KR)를 참조하세요.

## 2024년 10월 28일

**Adobe Analytics 확장 1.9.6**

**기능**:

* 사용자가 [변수 설정 작업](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/analytics/overview#set-variables)의 JSON 버전을 보고 편집할 수 있는 새 기능이 추가되었습니다. Adobe 웹 SDK 확장 기능에는 JSON을 제공하여 [분석 변수를 채우기](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/data-element-types)하는 작업도 포함됩니다. 마이그레이션 중인 고객은 AA 확장에서 웹 SDK 확장으로 JSON 데이터를 복사함으로써 각 변수를 수동으로 추가하는 대신 여러 설정을 한 번에 쉽게 전송할 수 있습니다.

## 2024년 8월 12일

**Adobe Analytics 확장 1.9.5**

**기능**:

* [AppMeasurement을 v2.27.0](https://github.com/adobe/appmeasurement/releases/tag/v2.27.0)(으)로 업그레이드했습니다.

## 2024년 3월 4일 화요일

**Adobe Analytics 확장 1.9.4**

**기능**:

* [AppMeasurement을 v2.26.0](https://github.com/adobe/appmeasurement/releases/tag/v2.26.0)(으)로 업그레이드했습니다.

## 2023년 9월 15일

**Adobe Analytics 확장 1.9.3**

**기능**:

* [AppMeasurement을 v2.25.0](https://github.com/adobe/appmeasurement/releases/tag/v2.25.0)(으)로 업그레이드했습니다.


## 2023년 7월 19일 목요일

**Adobe Analytics 확장 1.9.2**

**기능**:

* [AppMeasurement v2.24.0](https://github.com/adobe/appmeasurement/releases/tag/v2.24.0)(으)로 업그레이드되었습니다.
* 더블바이트로 인코딩된 문자가 포함된 링크 URL을 디코딩하는 선택적 구성(`decodeLinkParameters` 기본 `false`)이 추가되었습니다.

**버그 수정**:

* 높은 엔트로피 [사용자 에이전트 클라이언트 힌트](https://experienceleague.adobe.com/docs/analytics/technotes/client-hints.html) API가 잘못된 브라우저에 대한 추가 오류 처리를 추가했습니다.
* 기본적으로 `x-www-form-urlencoded`을(를) 사용하도록 [POST](https://developer.mozilla.org/ko-KR/docs/Web/HTTP/Methods/POST) Content-Type 헤더를 변경했습니다.

## 2022년 9월 23일

**Adobe Analytics 확장 1.9.1**

**기능**:

* AppMeasurement v2.23.0으로 업그레이드되었습니다.
* 이제 확장은 최신 버전의 AppMeasurement에서 지원하는 높은 엔트로피 [사용자 에이전트 클라이언트 힌트](https://developer.mozilla.org/en-US/docs/Web/HTTP/Client_hints#user-agent_client_hints)를 수집할 수 있습니다.

## 2022년 2월 28일 화요일

**Adobe Analytics 확장 1.9.0**

**버그 수정**:

* AppMeasurement에서 일부 디버그 문을 제거했습니다.

## 2021년 11월 29일

**Adobe Analytics 확장 1.8.8**

**버그 수정**:

* AppMeasurement이 v2.22.3으로 업그레이드되었습니다.

## 2021년 9월 16일

**Adobe Analytics 확장 1.8.7**

**버그 수정**:

* AppMeasurement이 v2.22.2로 업그레이드되었습니다.
* 더 이상 사용되지 않는 buildInfo.environment가 제거되었습니다.

## 2021년 8월 24일

**Adobe Analytics 확장 1.8.6**

**버그 수정**:

* [AppMeasurement을 v2.22.1](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=ko-KR)(으)로 업그레이드했습니다.
* innerHTML을 사용하는 대신 미러 Activity Map 논리를 위한 폴백 linkName이 업데이트되었습니다.

## 2020년 8월 6일

**Adobe Analytics 확장 1.8.5**

**버그 수정**:

* AAM 모듈 설정에서 잘못된 쿠키 이름이 설정된 경우 이 필드가 비어 있었습니다. 이 문제가 이제 수정되었습니다.

**기능**:

* [AppMeasurement가 2.22.0로](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=ko-KR) 업데이트됨.
* 이제 추가 설정이 확인란 대신 아코디언에서 축소되도록 UI에 적게 변경되었습니다.

## 2020년 6월 2일

**Adobe Analytics 확장 1.8.4**

**버그 수정**:

* 이벤트 드롭다운에 장바구니 이벤트(prodView, scAdd, scView 등)가 표시되지 않던 버그를 수정했습니다. 이제 드롭다운에서 이 모든 항목을 선택할 수 있습니다.

**기능**:

* 이제 사용자 지정 코드를 사용하지 않고도 확장에서 활동 맵을 끌 수 있습니다. 활동 맵은 AAM 모듈과 마찬가지로 별도의 모듈로 로드되며, 원할 경우 끌 수 있습니다.
* 계층 변수 및 기타 옵션을 최소화하여 UI를 정리했습니다.
* 확장 구성 UI에서 구매 ID를 설정하는 필드를 추가했습니다.

## 2020년 3월 10일

**Adobe Analytics 확장 1.8.3**

**버그 수정**:

* 사용자 지정 라이브러리를 사용하고 있고 보고서 세트가 Analytics에 구성되지 않은 경우 변수를 설정하려고 할 때 오류가 발생하는 규칙 구성에 영향을 주는 버그를 수정했습니다.
* eVar를 만들 때 prop에서 &quot;복제&quot;하거나 그 반대로 &quot;복제&quot;하는 옵션을 표시하지 않는 버그가 있었습니다. 이제 이전 버전의 동작을 미러링하도록 수정되었습니다.

**기능**:

* [AppMeasurement가 2.20.0으로](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=ko-KR) 업데이트됨

## 2020년 3월 2일

**Adobe Analytics 확장 1.8.2**

**버그 수정**:

* 숫자 이벤트 및 직렬화된 통화에 잘못된 구문이 사용되던 문제가 수정되었습니다.

**기능**:

* [AppMeasurement가 2.18.0으로](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=ko-KR) 업데이트됨
* Audience Manager 모듈의 DIL 라이브러리가 9.4로 업데이트됨
* 확장 프로그램의 입력 필드 길이가 늘어남
* 이제 확장 및 작업 구성의 eVar 및 속성에 Analytics의 친숙한 이름이 표시됩니다.
* 보안 쿠키를 작성할 수 있는 확장 구성의 &#39;쿠키&#39; 섹션에 확인란이 추가되었습니다.
* Audience Manager 모듈에 새 구성이 3개 추가되었습니다. 로깅 활성화, URL 대상 활성화 및 쿠키 대상 활성화에 대한 설정이 추가되었습니다.

## 2019년 11월 13일

**Adobe Analytics 확장 1.8.1**

**버그 수정**:

* 프리미엄 evar 및 prop이 저장되지 않는 버그를 수정했습니다.

## 2019년 11월 1일

**Adobe Analytics 확장 1.8.0**

**버그 수정**:

* 드롭다운에서 적은 수의 고객이 보고서 세트 옵션을 볼 수 없었던 버그를 수정했습니다.
* ECID를 사용할 때 변수가 올바르게 설정되지 않던 버그를 수정했습니다.

**기능**:

* 확장 보기에서 evars, props 및 events를 숫자로 정렬합니다.
* Magento 컨텍스트 데이터 지원을 위해 백엔드 스키마를 변경했습니다.

## 2019년 9월 6일

**Adobe Analytics 확장 1.7.8**

**버그 수정**:

* 일부 사용자가 드롭다운에서 보고서 세트 옵션을 보지 못했던 버그를 수정했습니다.
* 이벤트가 올바르게 실행되지 않는 버그를 수정했습니다.

## 2019년 9월 5일

**Adobe Analytics 확장 1.7.7**

**기능**:

* AppMeasurement를 2.17로 업데이트했습니다.
* 대상자 관리 모듈이 DIL 9.3을 지원하도록 업데이트되었습니다.
* 더 많은 공간을 제공하도록 필드 너비를 업데이트했습니다.

**버그 수정**:

* 옵트인/옵트아웃 설정 버그가 수정되었습니다.
* ECID를 사용할 때 변수가 올바르게 설정되지 않던 버그를 수정했습니다.

## 2019년 7월 18일

**Adobe Analytics 확장 1.7.6**

**기능**:

* Audience Manager용 DIL 9.2를 지원하도록 Adobe Analytics 확장이 업데이트됨

* [AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.15.0)을 지원하도록 확장이 업데이트
* 더 이상 지원되지 않으므로 다음 확인란이 제거됨: &quot;DOM 또는 화재 대상에 대상 게시 IFRAME을 첨부하지 않음&quot;

## 2019년 6월 4일

**Adobe Analytics 확장 1.7.5**

**기능**:

* 알려진 clearVars 문제에 대한 수정이 포함된 [AppMeasurement 2.14.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.14.0)으로 Adobe Analytics 확장이 업데이트됨
* 확장에 Exchange 링크가 추가됨. 드롭다운을 선택하고 &quot;extension info&quot;를 선택하면 Exchange 목록을 확인할 수 있음

**버그 수정**:

* 목록에서 삭제되는 잘못된 evar를 표시한 UI의 버그가 수정됨
* 여러 보고서 세트를 추가하려고 할 때 SSL 추적 서버를 필요로 하는 버그가 수정됨. 여러 보고서 세트를 추가할 때 추적 서버가 필요하지만 SSL 추적 서버 필드는 선택 사항임.

## 2019년 4월 15일

**Adobe Analytics 확장 1.7.4**

**버그 수정**:

* appMeasurement 2.13.0에서 버그를 찾은 후 확장이 롤백되었습니다. appMeasurement 2.13.0으로 인해 ECID를 보내지 않는 문제가 발생했습니다. 따라서 1.7.3을 설치한 경우에는 이 문제를 방지하기 위해 1.7.4로 업그레이드하는 것이 좋습니다. clearVars는 업데이트된 버전의 appMeasurement가 릴리스될 때까지 계속됩니다.

## 2019년 4월 12일

**Adobe Analytics 확장 1.7.3**

**버그 수정**:

* 알려진 clearVars 문제에 대한 수정이 포함된 appMeasurement 2.13.0으로 Adobe Analytics 확장이 업데이트되었습니다.

## 2019년 3월 21일

**Adobe Analytics 확장 1.7.2**

**기능**:

* Adobe Analytics 확장이 DIL 9.1로 업데이트되었습니다.
* Adobe Analytics 확장이 appMeasurement 2.12로 업데이트되었습니다.
* Adobe Analytics 확장 보기가 React-Spectrum으로 업그레이드되었습니다.
* 구성 페이지에서 보고서 세트를 구성할 때 해당 보고서 세트를 더 쉽게 선택할 수 있도록 회사의 모든 보고서 세트에 대한 드롭다운이 표시됩니다.

## 2019년 3월 7일

**Adobe Analytics 확장 1.7.1**

**버그 수정**:

* 1.7에서 버그가 발견된 후 확장이 버전 1.6으로 다시 롤백되었습니다.

## 2019년 2월 11일

**Adobe Analytics 확장 1.6**

**기능**:

* 옵트인을 지원하는 DIL 9.0으로 Adobe Analytics 확장이 업데이트되었습니다.
* 옵트인을 지원하도록 Adobe Analytics 확장이 AppMeasurement 2.11로 업데이트되었습니다.

**버그 수정**:

* 프로토타입 JS 충돌이 수정되었습니다. 이제 Analytics 확장에서 표준 prototype.js 라이브러리를 지원합니다.

## 2018년 11월 9일

**Adobe Analytics 확장 1.5.1**

**버그 수정**:

* Analytics 비콘이 실행되지 않는 문제를 해결하기 위해 DIL 모듈이 7.0으로 다운그레이드되었습니다.

## 2018년 11월 5일

**Adobe Analytics 확장 1.5**

**기능**:

* Audience Manager에서 DIL 8.0을 지원하도록 Adobe Analytics 확장이 업데이트되었습니다.
* Serialize from value 필드를 &quot;Event ID&quot;와 &quot;Event Value&quot;로 구분했습니다. 이렇게 하면 이벤트를 직렬화하지 않고 값을 할당하는 문제가 해결됩니다.
   * 참고: 문자열을 사용하여 ID를 추가하는 데 현재 필드를 사용하는 경우(예: Event7=3:abc123) 입력을 업데이트해야 &quot;Event ID&quot; 필드에 ID가 반영됩니다.

**버그 수정**:

* 통화 코드가 올바르게 입력되지 않는 버그가 수정되었습니다.

## 2018년 10월 11일

**Adobe Analytics 확장 1.4**

**기능**:

* 추적 쿠키 이름이 확장 구성으로 마이그레이션되었습니다.

**버그 수정**:

* trackerProperties 개체를 사용할 수 없는 경우 설정 변수가 충돌하지 않도록 버그가 수정되었습니다.

## 2018년 6월 5일

**Adobe Analytics 확장 1.3**

**기능**:

* AppMeasurement 2.9를 지원하도록 Adobe Analytics 확장이 업데이트되었습니다.
* `windows.s` 아래에 추적기 범위를 전체적으로 지정할 수 있는 Adobe Analytics 확장에 &quot;Make tracker globally accessible&quot; 기능이 추가되었습니다.

**버그 수정**:

* 세부 사항 보기에서 돌아올 때 목록 보기가 재설정되는 버그가 수정되었습니다.
* 수정 선택기에서 리소스 로드를 개선하도록 몇 가지 버그가 수정되었습니다.
* 여러 규칙이 Adobe Analytics 확장의 s.events를 덮어쓰는 버그가 수정되었습니다.

## 2018년 3월 20일

**Adobe Analytics 확장 1.2**

**기능**:

* AppMeasurement.js가 2.8.0으로 업데이트됨
* 서버측 전달을 위한 지원이 추가됨

## 2018년 2월 8일

**Adobe Analytics 확장 1.1**

**기능**:

* AppMeasurement가 버전 2.6으로 업데이트되었습니다.
* 초기화된 Analytics 추적기는 이제 Adobe Experience Platform 태그 확장의 공유 모듈을 통해 노출되므로 다른 확장에 이와 상호 작용하는 코드를 포함할 수 있습니다.

**버그 수정**:

* Error, missing Report Suite ID in AppMeasurement initialization이 브라우저 콘솔에 표시되는 Adobe Analytics 확장의 오류가 수정되었습니다.
