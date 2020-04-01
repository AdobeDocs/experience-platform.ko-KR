---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: DULE 정책 서비스 API 개발자 가이드
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# DULE 정책 서비스 API 개발자 가이드

DULE(Data Usage Lawring and Enforcement)는 Adobe Experience Platform 데이터 거버넌스의 핵심 메커니즘입니다. DULE 정책 서비스는 데이터 사용 정책을 만들고 관리하여 특정 데이터 사용 레이블로 레이블이 지정된 데이터에 대해 수행할 수 있는 마케팅 작업을 결정할 수 있는 RESTful API를 제공합니다.

이 문서에서는 정책 서비스 API에서 사용할 수 있는 주요 작업을 수행하기 위한 지침을 제공합니다. 아직 업데이트하지 않은 경우 먼저 데이터 거버넌스 개요를 [검토하여 DULE 프레임워크에 익숙해지도록](../home.md) 하십시오. DULE 정책을 만들고 적용하기 위한 단계별 지침은 DULE 정책 [자습서를](../policies/create.md)참조하십시오.

이 문서에서는 Policy Service API를 호출하기 전에 알아야 할 핵심 개념을 소개합니다.

## DULE Policy Service 시작하기

정책 서비스를 사용하기 전에 경험 플랫폼의 데이터에 적절한 DULE 레이블이 적용되어야 합니다. 데이터 세트 및 필드에 데이터 사용 레이블을 적용하기 위한 전체 단계별 지침은 DULE 레이블 [사용 안내서를](../labels/user-guide.md)참조하십시오.

## 전제 조건

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [데이터 거버넌스](../home.md):Adobe Experience Platform에서 데이터 사용 규정 준수를 강화하는 프레임워크
   * [DULE 레이블](../labels/overview.md):데이터 사용 레이블은 XDM(Experience Data Model) 데이터 필드에 적용되어 데이터 액세스 방법에 대한 제한을 지정합니다.
* [XDM(Experience Data Model) 시스템](../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [실시간 고객 프로필](../../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.
* [샌드박스](../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

## 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

* 인증:베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

데이터 거버넌스에 속하는 리소스를 비롯하여 경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형:application/json

## 핵심 리소스와 사용자 지정 리소스 비교

정책 서비스 API 내에서 모든 정책 및 마케팅 작업을 `core` 또는 `custom` 리소스라고 합니다.

리소스는 Adobe에서 정의 및 유지 관리하는 `core` 반면, `custom` 리소스는 개별 고객이 생성 및 유지 관리하므로 이러한 리소스를 만든 IMS 조직에서만 고유하고 볼 수 있습니다. 따라서 목록 및 조회 작업(`GET`)은 `core` 자원에 대해 허용되는 유일한 작업이지만 목록 작성, 조회 및 갱신 작업(`POST`, `PUT`, `PATCH`및 `DELETE`)은 `custom` 자원에 사용할 수 있습니다.

## 정책 상태

데이터 사용 정책은 다음 세 가지 상태 중 하나를 가질 수 있습니다. `DRAFT`또는 `ENABLED`를 `DISABLED`선택합니다.

기본적으로 &quot;ENABLED&quot; 정책만 정책 평가에 참여합니다.

&quot;DRAFT&quot; 정책은 정책 평가에서도 고려할 수 있지만 쿼리 매개 변수를 `?includeDraft=true`설정해야만 고려됩니다. 정책 평가에 대한 자세한 내용은 본 문서의 끝 부분에 있는 [정책 집행](../enforcement/overview.md) 섹션에 있는 문서를 참조하십시오.

## 마케팅 작업 이름 {#marketing-actions}

마케팅 작업 이름은 마케팅 작업에 대한 고유 식별자입니다. 각 `core` 마케팅 작업에는 모든 IMS 조직에 적용되는 고유한 이름이 있습니다. 이러한 이름은 Adobe에서 정의 및 유지 관리합니다. 한편, 모든 고객 정의 마케팅 작업(`custom` 리소스)은 개별 조직 내에서 고유하며 다른 IMS 조직과 표시 또는 공유되지 않습니다.

정책 서비스 API에서 마케팅 작업을 사용하는 단계는 이 문서의 후반부에 있는 마케팅 [작업](#marketing-actions) 섹션에 요약되어 있습니다.

## 다음 단계

사전 요구 사항 지식과 자격 증명이 있으므로 이 개발자 안내서에서 제공하는 샘플 API 호출을 계속 읽을 수 있습니다.

* [마케팅 작업](marketing-actions.md)
* [정책](policies.md)