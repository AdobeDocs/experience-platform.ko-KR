---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: DULE 정책 서비스 API 개발자 가이드
topic: developer guide
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---


# DULE [!DNL Policy Service] API 개발자 가이드

데이터 사용 표시 및 실행(DULE)은 Adobe Experience Platform 데이터 거버넌스의 핵심 메커니즘입니다. DULE 정책 서비스는 데이터 사용 정책을 만들고 관리하여 특정 데이터 사용 레이블이 지정된 데이터에 대해 취할 수 있는 마케팅 작업을 결정할 수 있도록 해주는 RESTful API를 제공합니다.

이 문서에서는 정책 서비스 API에서 사용할 수 있는 주요 작업을 수행하기 위한 지침을 제공합니다. 아직 그렇게 하지 않은 경우, 먼저 [데이터 거버넌스 개요를](../home.md) 검토하여 DULE 프레임워크에 익숙해지도록 하십시오. DULE 정책을 만들고 적용하기 위한 단계별 지침을 보려면 [DULE 정책 자습서를 참조하십시오](../policies/create.md).

이 문서에서는 Policy Service API를 호출하기 전에 알아야 할 핵심 개념을 소개합니다.

## DULE 시작하기 [!DNL Policy Service]

이 데이터를 사용하여 작업하기 전에 [!DNL Policy Service]데이터에 적절한 DULE 레이블이 [!DNL Experience Platform] 적용되어야 합니다. 데이터 세트 및 필드에 데이터 사용 레이블을 적용하기 위한 전체 단계별 지침은 [DULE 레이블 사용자 안내서에서 확인할 수 있습니다](../labels/user-guide.md).

## 전제 조건

이 가이드는 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [데이터 거버넌스](../home.md): 데이터 사용 규정 준수를 [!DNL Experience Platform] 적용하는 프레임워크입니다.
   * [DULE 레이블](../labels/overview.md): 데이터 사용 레이블은 XDM(Experience Data Model) 데이터 필드에 적용되어 데이터 액세스 방법에 대한 제한을 지정합니다.
* [XDM(Experience Data Model) 시스템](../../xdm/home.md): 고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
* [실시간 고객 프로필](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 Platform 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

## 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증: 무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Data Governance]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형: application/json

## 코어와 사용자 정의 리소스

API 내 [!DNL Policy Service] 에서 모든 정책 및 마케팅 작업을 `core` 또는 `custom` 리소스라고 합니다.

리소스 `core` 는 Adobe에서 정의하고 유지 관리하는 리소스이지만, `custom` 리소스는 개별 고객이 제작 및 유지 관리하므로 이러한 리소스를 만든 IMS 조직에서만 고유하고 볼 수 있습니다. 따라서 목록 및 조회 작업(`GET`)은 `core` 자원에 대해 허용되는 유일한 작업이지만 목록 작성, 조회 및 업데이트 작업(`POST`, `PUT``PATCH`및 `DELETE`)은 `custom` 리소스에 사용할 수 있습니다.

## 정책 상태

데이터 사용 정책에는 다음 세 가지 상태 중 하나가 있을 수 있습니다. `DRAFT`, `ENABLED`또는 `DISABLED`.

기본적으로 &quot;ENABLED&quot; 정책만 정책 평가에 참여합니다.

&quot;DRAFT&quot; 정책은 정책 평가에서도 고려될 수 있지만 쿼리 매개 변수를 설정해야만 고려됩니다 `?includeDraft=true`. 정책 평가에 대한 자세한 내용은 본 문서의 끝 부분에 있는 [정책 집행](../enforcement/overview.md) 섹션에 있는 문서를 참조하십시오.

## 마케팅 작업 이름 {#marketing-actions}

마케팅 작업 이름은 마케팅 작업을 위한 고유한 식별자입니다. 각 `core` 마케팅 활동에는 모든 IMS 조직에 적용되는 고유한 이름이 있습니다. 이러한 이름은 Adobe에서 정의하고 유지 관리합니다. 한편, 모든 고객 정의 마케팅 작업(`custom` 리소스)은 개별 조직 내에서 고유하며 다른 IMS 조직과 보이거나 공유되지 않습니다.

API에서 마케팅 작업을 [!DNL Policy Service] 사용하기 위한 단계는 이 문서의 후반부에 있는 [마케팅 작업](#marketing-actions) 섹션에 요약되어 있습니다.

## 다음 단계

사전 요구 사항 지식과 자격 증명이 있으므로 이 개발자 가이드에 제공된 샘플 API 호출을 계속 읽을 수 있습니다.

* [마케팅 작업](marketing-actions.md)
* [정책](policies.md)