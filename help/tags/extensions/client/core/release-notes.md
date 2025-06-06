---
title: 코어 확장에 대한 릴리스 노트
description: Adobe Experience Platform의 코어 확장에 대한 최신 릴리스 정보입니다.
exl-id: a049b2d5-7a00-435d-bcc7-112658a53a1e
source-git-commit: 1342461c95fa096496739fc14c92a7edd5aa6b57
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 47%

---

# 코어 확장 릴리스 노트

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

## 2025년 5월 8일

v3.4.3

* **데이터 요소** > **Javascript 도구** > **단순 바꾸기**&#x200B;에 **모두 바꾸기**&#x200B;에 대한 확인란이 표시되지만 확인란이 활성화된 상태로 규칙을 저장하려고 하면 오류가 발생하는 문제가 수정되었습니다.
* @adobe/react-spectrum을 v3.41.0으로 업그레이드합니다.
* @adobe/reactor-sandbox를 v13.2.1로 업그레이드합니다.

## 2024년 10월 23일

v3.4.2

* &quot;및 특정 속성 값 있음...&quot;이 활성화되면 양식 -> 변경 이벤트에 대한 스키마 유효성 검사 오류를 수정합니다.

## 2023년 3월 29일

v3.4.1

* 새 웹 네이티브 위임 이벤트를 추가합니다.
   * Keydown
   * KeyUp
* 다음 위임에 대해 여러 값에 대해 테스트(&quot;다른 항목 추가&quot; 옵션)하는 기능을 추가합니다.
   * 이벤트
      * 변경
   * 조건
      * Cookie
      * 랜딩 페이지
      * 쿼리 문자열 매개 변수
      * 트래픽 소스
      * 변수
* 뷰포트에 들어오는 요소를 수동으로 검색하는 대신 [교차 관찰자 API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)를 사용하도록 events/EntersViewport 대리자를 변경합니다.
* DTM 쿠키를 LocalStorage로 마이그레이션하던 코드를 제거합니다.
* LocalStorage 및 SessionStorage API를 사용할 수 없는 경우 콘솔에 경고를 기록합니다.

## 2022년 1월 4일

v3.3.0

* 직접 호출 규칙에 보낼 사용자 지정 이벤트 정보를 제공할 수 있도록 [직접 호출 트리거 작업](./overview.md#direct-call-action)을 변경합니다.

## 2021년 10월 8일

v3.2.2

* 사용 가능한 모든 연산자에 대한 조건부 값 데이터 요소 JSON 스키마를 수정합니다.
* https://github.com/adobe/reactor-extension-core/issues/64을 수정합니다.

## 2021년 9월 23일

v3.2.1

* 필드 값이 0일 때 조건부 값 데이터 요소 보기 초기화가 제대로 작동하지 않는 오류를 수정했습니다.

## 2021년 9월 23일

v3.2.0

조건부 값 데이터 요소에는 다음과 같은 변경 사항이 도입되었습니다.

* 정의되지 않은 값을 반환 값으로 설정할지 여부를 사용자가 선택할 수 있는 조건부 및 대체 값에 대한 확인란을 추가합니다.
* 숫자 값은 설정 객체에서 숫자로 표시됩니다.
* 대체 값과 같은 방식으로 작동할 수 있도록 조건부 값이 더 이상 필요하지 않습니다.

## 2021년 9월 17일

v3.1.1

* 날짜 범위 조건 보기를 로드할 수 없는 JS 오류를 수정했습니다.

## 2021년 9월 16일

v3.1.0

새 데이터 요소가 추가되었습니다.

* 병합된 개체 - 각 개체를 제공할 여러 데이터 요소를 선택합니다. 이러한 오브젝트는 서로 깊게(재귀적으로) 병합되어 새 오브젝트를 생성합니다.
* 조건부 값 - 비교 결과에 따라 두 값(conditionalValue 또는 fallbackValue) 중 하나를 반환합니다.
* 런타임 환경 - 환경 스테이지, 라이브러리 빌드 날짜, 속성 이름, 속성 ID, 규칙 이름, 규칙 ID, 이벤트 유형, 이벤트 세부 사항 페이로드, 직접 호출 식별자 등의 Launch 환경 변수 중 하나를 반환합니다.
* JavaScript 도구 - 일반적인 JavaScript 작업에 대한 래퍼: 기본 문자열 조작(바꾸기, 하위 문자열, 정규 표현식 일치, 첫 번째 및 마지막 인덱스, 분할, 슬라이스), 기본 배열 작업(슬라이스, 조인, pop, shift) 및 기본 범용 작업(슬라이스, 길이)입니다.
* 장치 속성 - 창 크기 또는 화면 크기와 같은 장치 속성을 반환합니다.

## 2021년 8월 11일

v3.0.0

* PDCL-6153: 캐시된 사용자 지정 코드 작업에 대해 정규화된 URL을 안정적으로 가져올 수 있는 지원을 추가합니다.

코어 확장의 v3.0.0은 Turbine 웹 런타임[&#128279;](https://github.com/adobe/reactor-turbine/releases/tag/v27.2.0)의 v27.2.0의 변경 사항과 함께 적용되므로 사용자의 회사에서 Premium CDN을 지원하는 경우 많은 Adobe 관리 호스팅 영역 간에 라이브러리를 로드할 수 있습니다.

이 업그레이드는 Premium CDN이 없는 사용자에 대해 선택 사항이며 이전 버전과 호환됩니다. 회사에서 Premium CDN이 활성화된 고객은 필수입니다.

## 2021년 5월 20일

v2.0.7

* 텍스트 입력에 대한 마우스 상호 작용이 더 이상 올바르게 작동하지 않는 문제를 수정합니다.
* 브라우저 및 운영 체제 조건의 사용을 중단합니다.

## 2021년 5월 4일

v2.0.6

* 화면 크기가 변경될 때 왜곡되는 아이콘을 수정하기 위한 작은 업데이트입니다.

## 2021년 3월 11일 금요일

v2.0.5

* 이제 v2.0.4 릴리스에서 추가된 데이터 요소 값을 지원하여 문자열을 숫자로 올바르게 변환할 수 있도록 지연 옵션이 있는 이벤트 및 작업에 대한 런타임 평가의 코드를 업데이트했습니다.

## 2021년 3월 9일 수요일

v2.0.4

* 다양한 필드에 대한 데이터 요소 지원이 추가되었습니다. &#39;Time on Page&#39;, &#39;Enters Viewport&#39;, &#39;Hover&#39; 및 &#39;Media Time Played&#39; 이벤트에 데이터 요소 지원이 추가되었습니다. 조건: &#39;사이트에서 보낸 시간&#39; 및 &#39;값 비교&#39;
* 링크 지연을 사용할 때 ctrl/cmd+클릭 및 마우스 가운데 버튼을 클릭할 수 있는 기본 동작에 대한 지원을 추가합니다.
* **클릭 이벤트에 대한 링크 지연을 &quot;더 이상 지원되지 않음&quot;으로 표시했습니다.** - 자세한 내용은 Adobe Experience Platform의 [데이터 수집 블로그](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403?profile.language=ko)에서 확인할 수 있습니다.

## 2021년 1월 6일

v1.9.0

* **새 &quot;직접 호출 트리거&quot; 작업** - 이제 코어 확장에 `Trigger Direct Call`(이)라는 새 작업 유형이 포함됩니다.  다른 규칙의 작업을 통해 직접 호출 규칙을 트리거하려는 경우 이 유형을 사용할 수 있습니다. 이 메서드는 `_satellite.track()` 메서드에 직접 매핑됩니다. 이 공헌에 대해 Jan Exner에게 대단히 감사드립니다.

## 2020년 12월 8일

v1.8.4

* 사용자가 CSP nonce를 지우거나 설정이 해제되지 않았던 버그를 수정했습니다.

## 2020년 7월 28일

v1.8.3

* CSP 임시값이 사용자 지정 코드 작업 호출 동안 새로 가져오는 대신 확장 시작 시 한 번만 읽히는 버그가 수정되었습니다.

## 2020년 7월 13일

v1.8.2

* 사용자 지정 코드 작업에서 태그 이름(예: 댓글)이 없는 토큰을 포함하는 HTML 코드에 대한 오류가 발생한 버그를 수정했습니다.

## 2020년 7월 10일

v1.8.1

* 페이지에 쓰기 전에 `script` 및 `style` 태그의 특성 내 사용자 지정 HTML 엔티티가 올바르게 디코딩되지 않았던 버그를 수정했습니다.&quot;
* 외부 사용자 지정 코드 작업에 컨텐츠가 없을 때 오류가 발생하는 버그를 수정했습니다. 외부 사용자 지정 코드 작업은 라이브러리와 다른 파일에서 로드되는 작업입니다(이 작업은 규칙을 트리거하는 이벤트가 libraryLoaded 또는 pageBottom이 아닐 때 발생함).

## 2020년 7월 6일

v1.8.0

* **사용자 지정 코드의 약속** - 사용자 지정 코드 조건 및 전역 범위에서 실행되지 않는 JavaScript 작업은 이제 약속을 반환할 수 있습니다.  이를 사용하여 다음 항목으로 이동하기 전에 사용자 지정 코드에서 비동기 프로세스가 완료될 때까지 기다리는 후속 조건과 작업을 수행할 수 있습니다.
* **HTML 사용자 지정 코드 작업의 콜백** - `onCustomCodeSuccess()` 및 `onCustomCodeFailure()` 콜백을 사용하여 HTML 사용자 지정 코드 작업에서 동일한 항목을 달성할 수 있습니다.

자세한 내용은 조건 > 사용자 지정 코드 및 작업 > 사용자 지정 코드에서 [핵심 확장 참조](./overview.md)를 참조하십시오.

## 2020년 4월 7일

v1.7.3

* **텍스트 필드 길이 증가** - 사용자의 화면 너비를 효과적으로 활용하고 더 긴 텍스트 문자열을 위해 더 많은 공간을 제공하기 위해 텍스트 입력 필드를 플렉스 레이아웃으로 변경했습니다.

## 2019년 11월 1일

v1.7.0

* **`event`사용자 지정 코드 데이터 요소 내의 변수에 액세스** - 이제 규칙 컨텍스트 내에서 실행될 때 사용자 지정 코드 데이터 요소 내에서 이벤트를 참조할 수 있습니다. 개체에는 규칙을 트리거한 이벤트에 대한 유용한 정보가 포함됩니다. 이 공헌에 대해 Stewart Schilling에게 대단히 감사드립니다.

## 2019년 10월 7일

v1.6.2

* **새 &quot;상수&quot; 데이터 요소 유형** - 이제 코어 확장에 `Constant`라는 새 데이터 요소가 포함됩니다.  여러 조건, 작업 또는 사용자 지정 코드에서 참조할 상수 값을 저장해야 하는 경우 사용할 수 있습니다. 이 공헌에 대해 Jan Exner에게 대단히 감사드립니다.

## 2019년 9월 11일

v1.6.1

* **CSP 임시 항목 지원** - 코어 확장에는 이제 선택적 구성 매개 변수가 있습니다. 임시 항목을 참조하는 데이터 요소를 추가할 수 있습니다. 구성된 경우 태그가 페이지에 추가하는 모든 인라인 스크립트는 사용자가 구성한 임시 항목을 사용합니다. 이 변경 사항은 태그 스크립트가 CSP 환경에서 로드될 수 있도록 컨텐츠 보안 정책을 임시로 사용할 수 있도록 지원합니다. CSP에서 태그를 사용하는 방법에 대한 자세한 내용은 [여기](../../../ui/client-side/content-security-policy.md)에서 확인할 수 있습니다.

## 2019년 6월 18일

v1.5.0

* **직접 호출 로깅** - 이제 직접 호출 규칙에 대한 브라우저 로깅이 전달될 때 추가 정보를 제공합니다.

## 2019년 5월 8일

v1.4.3

* **입력 필드** - 이제 입력 필드가 훨씬 길어졌습니다.
* **사용자 지정 이벤트** - 이제 창에서 전달된 이벤트와 함께 사용자 지정 이벤트 유형을 사용할 수 있습니다.
* **버그 수정** - 값 비교 조건이 0 값을 갖지 않는 버그가 수정되었습니다.
* **버그 수정** - exchange\_url 필드가 업데이트되었으므로 이제 Adobe Exchange에서 코어 확장 목록을 볼 수 있습니다.

## 2019년 1월 8일

v1.4.2

* **뷰포트 입력 이벤트** - 이전에는 뷰포트 입력 이벤트가 페이지당 한 번만 트리거되었습니다. 이제 요소가 뷰포트에 입력될 때마다 트리거하도록 이 동작을 구성할 수 있습니다.
* **사용자 지정 이벤트 이벤트** - 이제 조건 및 작업 내에서 사용할 수 있는 컨텍스트 데이터를 사용자 지정 이벤트에 포함할 수 있습니다.
* **클릭 이벤트** - 클릭 이벤트에 링크 지연을 설정하면 앵커 자체뿐만 아니라 앵커 하위 항목에 대해서도 올바르게 등록됩니다.

## 2018년 11월 8일

* **Persist Cohort 옵션** 집단 유지 옵션이 샘플링 조건에 추가되었습니다. 이 옵션은 세션 간 샘플 집단 내외에 사용자를 유지하는 효과가 있습니다. 예를 들어 &quot;persist cohort&quot; 확인란이 선택되어 있고 제공된 방문자에 대해 처음 실행된 조건이 true를 반환하는 경우, 동일한 방문자에 대해 이후에 실행되는 모든 조건은 true를 반환합니다. 마찬가지로, &quot;persist cohort&quot; 확인란이 선택되어 있고 제공된 방문자에 대해 처음 실행된 조건이 false를 반환하는 경우, 동일한 방문자에 대해 이후에 실행되는 모든 조건은 false를 반환합니다.
* **버그 수정** - 태그가 동기적으로 로드되었지만 잘못 설치된(`_satellite.pageBottom()`에 대한 호출이 없음) 페이지에서 Page Bottom 이벤트와 사용자 지정 코드 작업을 사용하는 규칙이 웹 사이트 콘텐츠를 지우는 문제가 해결되었습니다.
* **버그 수정** - 브라우저의 DOMContentLoaded 이벤트가 실행된 후 태그 라이브러리가 비동기적으로 로드되고 로드를 마치면 뷰포트 입력이 작동하지 않는 문제가 해결되었습니다.

## 2018년 5월 24일

* **기능** - 값 비교 조건이 추가되었습니다. 이 조건은 사용 가능한 여러 연산자를 사용하여 두 값을 비교합니다. 이 기능은 너무 구체적이었던 이전의 여러 조건의 기능을 대체합니다.
* **기능** - 최대 빈도 조건이 추가되었습니다. 이 조건을 사용하면 기간 또는 이벤트 발생 내에서 조건이 true를 반환하는 횟수를 지정할 수 있습니다. 예: 하루 5회, 방문당 2회

## 2018년 4월 11일

* **기능** - 이제 데이터 요소가 다른 데이터 요소를 참조할 수 있습니다.

## 2018년 3월 20일

* **버그 수정** - 사용자 지정 코드 창에서 `document.write` 오류가 발생하고 비동기 배포에서 실행되지 않았습니다.
* **버그 수정** - 기본 모듈이 라이브러리에 포함되지 않았습니다.
* **버그 수정** - 난수 데이터 요소의 최소값과 최대값에서 문제가 발생했습니다.

## 2018년 1월 10일

* **기능** - 난수 데이터 요소
* **기능** - 페이지 정보 데이터 요소
* **기능** - 날짜 조건
* **기능** - 샘플링 조건
