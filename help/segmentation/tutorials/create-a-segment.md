---
keywords: Experience Platform;홈;인기 항목;세그먼트;세그먼트;세그먼트 만들기;세그먼테이션;세그먼트 만들기;세그먼테이션 서비스;
solution: Experience Platform
title: 세분화 서비스 API를 사용하여 세그먼트 만들기
type: Tutorial
description: Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트 정의를 개발, 테스트, 미리 보기 및 저장하는 방법을 배우려면 이 자습서를 따르십시오.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 세분화 서비스 API를 사용하여 세그먼트 만들기

이 문서에서는 다음을 사용하여 세그먼트 정의를 개발, 테스트, 미리 보기 및 저장하는 자습서를 제공합니다. [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

사용자 인터페이스를 사용하여 세그먼트를 만드는 방법에 대한 자세한 내용은 [세그먼트 빌더 안내서](../ui/overview.md).

## 시작하기

이 자습서에서는 다양한 을(를) 작업 이해해야 합니다 [!DNL Adobe Experience Platform] 대상 세그먼트 만들기와 관련된 서비스입니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): 실시간 고객 프로필 데이터에서 대상 세그먼트를 만들 수 있습니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다. 세그먼테이션을 최대한 활용하려면 데이터에 따라 프로필 및 이벤트가 수집되는지 확인하십시오. [데이터 모델링 우수 사례](../../xdm/schema/best-practices.md).

다음 섹션에서는 를 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다. [!DNL Platform] API.

### 샘플 API 호출 읽기

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값 수집

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

## 세그먼트 정의 개발

세그먼테이션의 첫 번째 단계는 세그먼트 정의라고 하는 구문에 표시되는 세그먼트를 정의하는 것입니다. 세그먼트 정의는 작성된 쿼리를 캡슐화하는 개체입니다 [!DNL Profile Query Language] (PQL). 이 개체를 PQL 술어라고도 합니다. PQL 술어는 제공하는 레코드 또는 시계열 데이터와 관련된 조건을 기반으로 세그먼트에 대한 규칙을 정의합니다 [!DNL Real-Time Customer Profile]. 다음을 참조하십시오. [PQL 안내서](../pql/overview.md) PQL 쿼리 작성에 대한 자세한 내용

에 POST 요청을 하여 새 세그먼트 정의를 만들 수 있습니다. `/segment/definitions` 의 엔드포인트 [!DNL Segmentation] API. 다음 예제에서는 세그먼트를 성공적으로 정의하기 위해 필요한 정보를 포함하여 정의 요청 형식을 지정하는 방법을 간략하게 설명합니다.

세그먼트 정의 방법에 대한 자세한 내용은 다음을 참조하십시오. [세그먼트 정의 개발자 안내서](../api/segment-definitions.md#create).

## 대상자 예측 및 미리보기 {#estimate-and-preview-an-audience}

세그먼트 정의를 개발할 때 내의 예상 및 미리보기 도구를 사용할 수 있습니다. [!DNL Real-Time Customer Profile] 예상되는 대상을 격리하는 데 도움이 되는 요약 수준 정보를 봅니다. 예상치는 예상 대상 크기 및 신뢰 구간과 같은 세그먼트 정의에 대한 통계 정보를 제공합니다. 미리 보기는 세그먼트 정의에 대해 페이지가 매겨진 자격 프로필 목록을 제공하므로 결과를 예상과 비교할 수 있습니다.

대상자를 예측하고 미리 봄으로써 원하는 결과가 나올 때까지 PQL 술어를 테스트하고 최적화할 수 있습니다. 그런 다음 이 술어를 업데이트된 세그먼트 정의에 사용할 수 있습니다.

세그먼트를 미리 보거나 예상 값을 가져오는 데 필요한 두 가지 단계가 있습니다.

1. [미리보기 작업 만들기](#create-a-preview-job)
2. [예상 보기 또는 미리 보기](#view-an-estimate-or-preview) 미리보기 작업의 ID 사용

### 예상 생성 방법

데이터 샘플은 세그먼트를 평가하고 적격 프로필의 수를 예상하는 데 사용됩니다. 새 데이터는 매일 아침 메모리에 로드되고(12AM-2AM PT 사이, 7-9AM UTC) 모든 세그멘테이션 쿼리는 해당 날짜의 샘플 데이터를 사용하여 추정됩니다. 따라서 새 필드가 추가되거나 수집된 추가 데이터는 다음 날 추정에 반영됩니다.

샘플 크기는 프로필 스토어에 있는 전체 엔티티 수에 따라 다릅니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 저장소의 엔티티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1000~2000만 | 100만 |
| 2,000만 이상 | 총 5% |

예측은 일반적으로 10-15초 동안 실행되며, 대략적인 예측부터 시작하여 더 많은 기록을 읽을수록 구체화됩니다.

### 미리보기 작업 만들기

에 POST 요청을 하여 새 미리보기 작업을 생성할 수 있습니다. `/preview` 엔드포인트.

미리보기 작업 생성에 대한 자세한 지침은 [미리 보기 및 예상 끝점 안내서](../api/previews-and-estimates.md#create-preview).

### 예상 보기 또는 미리 보기

서로 다른 쿼리가 완료되는 데 시간이 오래 걸릴 수 있으므로 예상 및 미리보기 프로세스는 비동기적으로 실행됩니다. 쿼리가 시작되면 API 호출을 사용하여 예측이나 미리보기가 진행되는 현재 상태를 검색(GET)할 수 있습니다.

사용 [!DNL Segmentation Service] API를 사용하면 미리보기 작업의 현재 상태를 해당 ID로 조회할 수 있습니다. 상태가 &quot;RESULT_READY&quot;이면 결과를 볼 수 있습니다. 미리보기 작업의 현재 상태를 조회하려면 의 섹션을 참조하십시오. [미리보기 작업 섹션 검색](../api/previews-and-estimates.md#get-preview) 미리 보기 및 예상 엔드포인트 안내서에서 참조하십시오. 예상 작업의 현재 상태를 조회하려면 다음 섹션을 참조하십시오. [예상 작업 검색 중](../api/previews-and-estimates.md#get-estimate) 미리 보기 및 예상 엔드포인트 안내서에서 참조하십시오.


## 다음 단계

세그먼트 정의를 개발, 테스트 및 저장했으면 다음을 사용하여 대상을 구축하는 세그먼트 작업을 생성할 수 있습니다. [!DNL Segmentation Service] API. 다음 튜토리얼 참조: [세그먼트 결과 평가 및 액세스](./evaluate-a-segment.md) 을 수행하는 방법에 대한 자세한 단계입니다.
