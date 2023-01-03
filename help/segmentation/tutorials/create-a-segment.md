---
keywords: Experience Platform;홈;인기 항목;세그먼트;세그먼트;세그먼트 만들기;세그먼테이션;세그먼트 만들기;세그먼테이션 서비스;
solution: Experience Platform
title: 세그먼테이션 서비스 API를 사용하여 세그먼트 만들기
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트 정의를 개발, 테스트, 미리 보기 및 저장하는 방법을 알려면 이 자습서를 따르십시오.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 세그먼테이션 서비스 API를 사용하여 세그먼트 만들기

이 문서에서는 [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

사용자 인터페이스를 사용하여 세그먼트를 작성하는 방법에 대한 자세한 내용은 [세그먼트 빌더 안내서](../ui/overview.md).

## 시작하기

이 자습서에서는 다양한 자습서를 이해하고 있어야 합니다 [!DNL Adobe Experience Platform] 대상 세그먼트 만들기에 관련된 서비스입니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): 실시간 고객 프로필 데이터에서 대상 세그먼트를 작성할 수 있습니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다. 세그멘테이션을 가장 잘 사용하려면 데이터가 [데이터 모델링 우수 사례](../../xdm/schema/best-practices.md).

다음 섹션에서는 를 성공적으로 호출하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Platform] API.

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

- 권한 부여: 베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

## 세그먼트 정의 개발

세그먼테이션의 첫 번째 단계는 세그먼트 정의라고 하는 구문으로 표시되는 세그먼트를 정의하는 것입니다. 세그먼트 정의는 [!DNL Profile Query Language] (PQL). 이 개체를 PQL 술어라고도 합니다. PQL은 사용자가 제공하는 레코드 또는 시계열 데이터와 관련된 조건을 기반으로 세그먼트에 대한 규칙을 정의합니다 [!DNL Real-Time Customer Profile]. 자세한 내용은 [PQL 안내서](../pql/overview.md) pql 쿼리 작성에 대한 자세한 정보.

에 POST 요청을 만들어 새 세그먼트 정의를 만들 수 있습니다 `/segment/definitions` 의 엔드포인트 [!DNL Segmentation] API. 다음 예제에서는 세그먼트를 성공적으로 정의하기 위해 필요한 정보를 포함하여 정의 요청 형식을 지정하는 방법을 간략하게 설명합니다.

세그먼트 정의 방법에 대한 자세한 내용은 [세그먼트 정의 개발자 안내서](../api/segment-definitions.md#create).

## 대상 예측 및 미리 보기 {#estimate-and-preview-an-audience}

세그먼트 정의를 개발할 때 내에서 예측 및 미리 보기 도구를 사용할 수 있습니다 [!DNL Real-Time Customer Profile] 예상되는 대상을 분리하는 데 도움이 되는 요약 수준 정보를 보려면 을 참조하십시오. 추정은 예상 대상 크기 및 신뢰 구간과 같은 세그먼트 정의에 대한 통계 정보를 제공합니다. 미리 보기는 세그먼트 정의에 대한 페이지 매김된 프로필 목록을 제공하여 결과를 예상과 비교할 수 있도록 합니다.

대상을 추정하고 미리 보면 원하는 결과를 생성할 때까지 PQL 설명을 테스트 및 최적화하여 업데이트된 세그먼트 정의에서 사용할 수 있습니다.

세그먼트를 미리 보거나 예상치를 얻는 데 필요한 두 가지 단계가 있습니다.

1. [미리 보기 작업 만들기](#create-a-preview-job)
2. [예측 또는 미리 보기 보기](#view-an-estimate-or-preview) 미리 보기 작업의 ID 사용

### 추정이 생성되는 방법

데이터 샘플은 세그먼트를 평가하고 자격 있는 프로필의 수를 예상하는 데 사용됩니다. 새로운 데이터는 매일 오전 12AM-2AM PT(오전 7-9AM UTC) 사이에 메모리에 로드되며 모든 세그먼테이션 쿼리는 해당 날짜의 샘플 데이터를 사용하여 예측됩니다. 따라서 추가된 모든 새 필드나 수집된 추가 데이터는 다음 날의 추정에 반영됩니다.

샘플 크기는 프로필 저장소의 전체 엔티티 수에 따라 다릅니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 저장소의 엔터티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1~2,000만 | 100만 |
| 2천만 명 이상 | 합계의 5% |

추정은 일반적으로 10~15초 이상 실행되며, 더 많은 레코드가 읽히는 동안 대략적인 추정과 세분화됩니다.

### 미리 보기 작업 만들기

에 POST 요청을 만들어 새 미리 보기 작업을 만들 수 있습니다 `/preview` 엔드포인트.

미리 보기 작업 만들기에 대한 자세한 지침은 [미리 보기 및 예상 끝점 안내서](../api/previews-and-estimates.md#create-preview).

### 예측 또는 미리 보기 보기

다른 쿼리가 완료하는 데 시간이 다른 데 걸릴 수 있으므로 예측 및 미리 보기 프로세스가 비동기식으로 실행됩니다. 쿼리가 시작되면 API 호출을 사용하여 추정치나 미리 보기가 진행되는 동안 예측의 현재 상태를 검색(GET)할 수 있습니다.

사용 [!DNL Segmentation Service] API를 사용하여 미리 보기 작업의 현재 상태를 ID로 조회할 수 있습니다. 상태가 &quot;RESULT_READY&quot;인 경우 결과를 볼 수 있습니다. 미리 보기 작업의 현재 상태를 조회하려면 [미리 보기 작업 섹션 검색](../api/previews-and-estimates.md#get-preview) 미리 보기 및 예상 끝점 안내서에서 를 참조하십시오. 예상 작업의 현재 상태를 조회하려면 [예상 작업 검색](../api/previews-and-estimates.md#get-estimate) 미리 보기 및 예상 끝점 안내서에서 를 참조하십시오.


## 다음 단계

세그먼트 정의를 개발, 테스트 및 저장한 후, 세그먼트 작업을 만들어 [!DNL Segmentation Service] API. 다음에서 자습서를 참조하십시오. [세그먼트 결과 평가 및 액세스](./evaluate-a-segment.md) 를 참조하십시오.
