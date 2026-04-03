---
title: 데이터 수집에서의 ID 문제 해결
description: 방문자 인플레이션, ECID 불일치, 쿠키 충돌 및 FPID 문제를 포함하여 웹 SDK 구현에서 일반적인 ID 문제를 진단합니다.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# 데이터 수집에서의 ID 문제 해결

ID 문제는 구현 자체의 오류라기보다는 다운스트림 보고(부풀려진 방문자 수, 파편화된 프로필 또는 잘못된 개인화)의 증상으로 나타나는 경우가 많습니다. 이 페이지는 웹 SDK 구현에서 가장 일반적인 ID 문제를 진단하고 해결하는 데 도움이 됩니다. 데이터 수집에서 ID가 작동하는 방식에 대한 배경은 [ID 개요](./overview.md)를 참조하십시오.

## ID 값 검사 {#inspect-identity}

특정 문제를 해결하기 전에 웹 SDK에서 사용 중인 현재 ID 값을 검색하십시오. [`getIdentity`](/help/collection/js/commands/getidentity.md) 명령을 사용하여 ECID 및 기타 ID 신호를 봅니다.

```js
alloy("getIdentity", { namespaces: ["ECID", "CORE"] }).then(function(result) {
  console.log("ECID:", result.identity.ECID);
  console.log("CORE ID:", result.identity.CORE);
  console.log("Edge region:", result.edge.regionID);
});
```

브라우저의 개발자 도구에서 ID 값을 검사할 수도 있습니다.

1. **응용 프로그램** 탭(Chrome/Edge) 또는 **저장소** 탭(Firefox/Safari)을 엽니다.
2. 도메인에서 `kndctr_` 접두사가 있는 쿠키를 찾습니다. `kndctr_<ORG_ID>_AdobeOrg_identity` 쿠키에 ECID가 포함되어 있습니다.
3. **네트워크** 탭을 열고 Edge Network에 대한 `interact` 또는 `collect` 요청을 찾습니다. `identityMap`에 대한 요청 페이로드와 ID 핸들에 대한 응답 페이로드를 검사합니다.

## 일반적인 문제 {#common-issues}

+++**방문자 수 인플레이션**

**증상**: Analytics 보고서에 예상보다 많은 고유 방문자가 표시되거나 세션 간 동일한 사람이 여러 방문자로 표시됩니다.

**가능한 원인**:

| 원인 | 식별 방법 | 해결 방법 |
| --- | --- | --- |
| 짧은 쿠키 수명 | 브라우저에서 `kndctr_` 쿠키의 만료를 확인하세요. 만료일이 7일 이하이면 브라우저 정책에서 쿠키 지속 시간을 제한할 수 있습니다. | 더 긴 쿠키 지속성을 위해 DNS A/AAAA 레코드를 사용하여 서버에서 설정한 [자사 장치 ID(FPID)](./fpid.md)을(를) 구현합니다. |
| 첫 번째 요청에 FPID 누락 | 페이지 로드 시 첫 번째 Edge Network 요청을 검사합니다. FPID 쿠키가 없으면 Edge Network에서 새 ECID를 생성합니다. 첫 번째 요청 후에 FPID가 설정되면 해당 첫 번째 요청에서 생성된 ECID가 분리됩니다. | 웹 SDK이 첫 번째 요청을 보내기 전에 FPID 쿠키를 설정합니다. [쿠키를 설정할 시기](./fpid.md#when-to-set-cookie)를 참조하세요. |
| 도메인 간 `orgId` 불일치 | 도메인 간 `orgId` 구성 값을 비교합니다. 일치하지 않는 값으로 인해 별도의 ID 범위가 발생합니다. | 조직 내의 모든 도메인에서 동일한 [`orgId`](/help/collection/js/commands/configure/orgid.md)을(를) 사용합니다. |
| 쿠키 삭제 동의 배너 | 동의 구현에서 동의가 부여되기 전에 모든 쿠키를 지운 다음 웹 SDK이 초기화되면 새 ECID가 생성됩니다. | 동의가 설정될 때까지 `kndctr_` 쿠키를 유지하거나 웹 SDK 초기화를 지연하도록 동의 배너를 구성합니다. [동의 및 ID](./consent.md)도 참조하세요. |
| JavaScript 집합 FPID 쿠키 | `document.cookie`을(를) 사용하여 설정된 쿠키에는 최대 24시간까지 수명을 제한하는 브라우저 제한 사항(ITP, ETP)이 적용됩니다. | JavaScript이 아닌 DNS A/AAAA 레코드를 사용하여 서버에서 FPID 쿠키를 설정합니다. |

+++

+++**페이지 간에 예기치 않게 ECID가 변경되었습니다**

**증상**: ECID가 동일한 도메인의 다른 페이지에서 다르거나 모든 페이지 로드 시 변경됩니다.

**진단 단계**:

1. `kndctr_` ID 쿠키가 두 페이지에 있는지 확인하십시오. 한 페이지에서 누락된 경우 웹 SDK이 해당 페이지에 구성되어 있는지 확인합니다.
2. 쿠키 도메인이 충분히 광범위하게 설정되었는지 확인합니다. `shop.example.com`에 설정된 쿠키를 `www.example.com`에서 사용할 수 없습니다. 자사 수집 및 쿠키 설정 인프라가 동일한 도메인 범위를 사용하는지 확인합니다.
3. 탐색 시 쿠키를 지우는 JavaScript(예: 공격적인 쿠키 동의 스크립트 또는 개인 정보 보호 도구)를 확인합니다.
4. 단일 페이지 애플리케이션을 사용하는 경우 앱 초기화 시 웹 SDK이 한 번 구성되었는지 확인하고, 모든 경로 변경 시 다시 초기화되지 않았는지 확인합니다. 재초기화하면 새 ECID를 생성할 수 있습니다.

+++

+++**FPID가 ECID를 시드하지 않습니다**

**증상**: FPID 쿠키를 설정했지만 `getIdentity`에서 방문 간에 일관되지 않은 ECID를 반환하거나 FPID가 Edge Network 요청 페이로드에 표시되지 않습니다.

**진단 단계**:

1. **FPID 쿠키 형식을 확인하십시오**: FPID는 올바른 [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122)이어야 합니다. 브라우저의 개발자 도구를 열고 FPID 쿠키를 찾은 다음 값이 `xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx` 패턴과 일치하는지 확인합니다.
2. **데이터 스트림에서 쿠키 이름을 확인하십시오**: [데이터 스트림 쿠키 메서드](./fpid.md#setting-cookie-datastreams)를 사용하는 경우 데이터 스트림에 구성된 쿠키 이름은 서버가 설정하는 쿠키의 이름과 정확히 일치해야 합니다.
3. **쿠키가 요청 시 전송되는지 확인**: 네트워크 탭에서 Edge Network 요청의 `Cookie` 헤더를 검사합니다. FPID 쿠키를 포함해야 합니다.
4. **ID 우선 순위 확인**: 기존 ECID가 `kndctr_` 쿠키에 이미 저장되어 있는 경우 FPID보다 우선합니다. FPID는 기존 ECID가 없는 경우에만 새 ECID를 시드합니다. 전체 우선 순위는 [FPID 작동 방식](./fpid.md#how-fpids-work)을 참조하십시오.
5. **CNAME의 유효성을 검사합니다**: 데이터 스트림 쿠키 메서드를 사용하는 경우 자사 컬렉션 CNAME이 올바르게 구성되어 있고 요청이 이를 통해 라우팅되는지 확인하십시오.

+++

+++**도메인 간 ID가 작동하지 않음**

**증상**: 한 도메인에서 다른 도메인으로 클릭하는 방문자는 대상 도메인에서 새 방문자로 취급됩니다.

**진단 단계**:

1. **URL 확인**: 방문자가 링크를 클릭할 때 대상 URL을 검사합니다. `adobe_mc` 쿼리 문자열 매개 변수를 포함해야 합니다. 매개 변수가 없으면 소스 도메인에 매개 변수가 추가되지 않습니다. [도메인 간 공유 구현](./cross-domain-sharing.md#implement-cross-domain-sharing)을 참조하십시오.
2. **시간 확인**: `adobe_mc` 매개 변수가 5분 후에 만료됩니다. 대상 페이지를 로드하는 데 너무 오래 걸리는 경우(예: 리디렉션 또는 느린 네트워크 때문) 웹 SDK에서 읽기 전에 매개 변수가 만료될 수 있습니다.
3. **일치하는 `orgId`을(를) 확인**: 두 도메인이 동일한 [`orgId`](/help/collection/js/commands/configure/orgid.md)을(를) 사용해야 합니다. 조직 ID가 일치하지 않으면 대상 도메인에서 전달된 ID를 거부합니다.
4. **웹 SDK이 대상에 있는지 확인**: 대상 페이지에는 웹 SDK이 설치 및 구성되어 있어야 합니다. 이 매개 변수가 없으면 `adobe_mc` 매개 변수는 무시됩니다.
5. **URL 제거를 확인**: 일부 리디렉션 서비스, CDN 또는 서버측 논리는 알 수 없는 쿼리 문자열 매개 변수를 제거합니다. `adobe_mc`이(가) 원본 페이지와 대상 페이지 사이의 중간 리디렉션을 유지하는지 확인합니다.

+++

+++**Mobile-to-Web ID 핸드오프가 실패했습니다**

**증상**: 모바일 앱에서 시작하여 WebView 또는 모바일 브라우저를 여는 방문자는 웹 측에서 새 방문자로 취급됩니다.

**진단 단계**:

1. **URL을 확인합니다**: WebView에 전달되는 URL을 기록합니다. `adobe_mc`[`getUrlVariables`에서 생성한 ](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) 매개 변수를 포함해야 합니다.
2. **SDK 버전 확인**: Edge Network 확장을 위한 모바일 ID는 버전 1.1.0 이상이어야 하며 웹 SDK은 버전 2.11.0 이상이어야 합니다.
3. **시간 확인**: 도메인 간 공유와 마찬가지로 `adobe_mc` 매개 변수가 5분 후에 만료됩니다. URL이 구성된 후 WebView가 즉시 로드되는지 확인합니다.
4. **일치 `orgId`확인**: Experience Cloud 조직 ID는 모바일 SDK 구성과 웹 SDK 구성 모두에서 동일해야 합니다.

+++
