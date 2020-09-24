---
keywords: Experience Platform;home;popular topics;segment;Segment;create segment;segmentation;create a segment;Segmentation Service;
solution: Experience Platform
title: 세그먼트 만들기
topic: tutorial
type: Tutorial
description: 이 문서에서는 Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트 정의를 개발, 테스트, 미리 보기 및 저장하기 위한 자습서를 제공합니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# 세그먼트 만들기

이 문서에서는 [[!DNL Adobe Experience Platform 세그멘테이션 서비스 API]를 사용하여 세그먼트 정의를 개발, 테스트, 미리 보기 및 저장하기 위한 자습서를 제공합니다](../api/getting-started.md).

사용자 인터페이스를 사용하여 세그먼트를 만드는 방법에 대한 자세한 내용은 [세그먼트 빌더 안내서를 참조하십시오](../ui/overview.md).

## 시작하기

이 자습서에서는 대상 세그먼트 만들기와 관련된 다양한 [!DNL Adobe Experience Platform] 서비스에 대해 작업해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL 실시간 고객 프로필]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [[!DNL Adobe Experience Platform 세그멘테이션 서비스]](../home.md):실시간 고객 프로필 데이터를 통해 고객 세그먼트를 만들 수 있습니다.
- [[!DNL 경험 데이터 모델(XDM)]](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크

다음 섹션에서는 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 [!DNL Platform] 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 세그먼트 정의 개발

세그멘테이션의 첫 번째 단계는 **세그먼트 정의라는 구문으로 표현되는 세그먼트를 정의하는 것입니다**. 세그먼트 정의는 PQL으로 작성된 쿼리를 캡슐화하는 [!DNL Profile Query Language] 개체입니다. 이 개체를 **PQL 술어라고도 합니다**. PQL은 사용자가 제공하는 레코드 또는 시간 시리즈 데이터와 관련된 조건을 기준으로 세그먼트에 대한 규칙을 정의합니다 [!DNL Real-time Customer Profile]. PQL 쿼리 [작성에 대한 자세한 내용은 PQL](../pql/overview.md) 가이드를 참조하십시오.

API의 종단점에 대한 POST 요청을 만들어 새 세그먼트 정의를 만들 수 `/segment/definitions` [!DNL Segmentation] 있습니다. 다음 예에서는 세그먼트를 성공적으로 정의하기 위해 필요한 정보를 포함하여 정의 요청의 형식을 지정하는 방법에 대해 설명합니다.

세그먼트 정의 방법에 대한 자세한 내용은 [세그먼트 정의 개발자 안내서를 참조하십시오](../api/segment-definitions.md#create).

## 대상 예측 및 미리 보기 {#estimate-and-preview-an-audience}

세그먼트 정의를 개발하면 내 [!DNL Real-time Customer Profile] 에서 예측 및 미리 보기 도구를 사용하여 예상 대상을 분리하는 데 도움이 되는 요약 수준 정보를 볼 수 있습니다. 예상치는 예상 대상 크기 및 신뢰 간격과 같은 세그먼트 정의에 대한 통계 정보를 제공합니다. 미리 보기에서는 세그먼트 정의에 대해 페이지에 지정된 프로필 목록을 제공하므로 결과를 예상과 비교할 수 있습니다.

대상을 예상 및 미리 보기하여 PQL 예측 결과를 테스트 및 최적화하여 원하는 결과를 얻을 수 있도록 한 다음 업데이트된 세그먼트 정의에서 사용할 수 있습니다.

세그먼트를 미리 보거나 견적을 받는 데 필요한 두 가지 단계가 있습니다.

1. [미리 보기 작업 만들기](#create-a-preview-job)
2. [미리 보기 작업의 ID를 사용하여 예상 또는 미리](#view-an-estimate-or-preview) 보기

### 예상 생성 방법

데이터 샘플은 세그먼트를 평가하고 적격한 프로필 수를 계산하는 데 사용됩니다. 새로운 데이터는 매일 아침(오전 7-9AM UTC인 12AM-2PT 사이) 메모리에 로드되며 모든 세그멘테이션 쿼리는 해당 일의 샘플 데이터를 사용하여 계산됩니다. 따라서 추가된 새 필드 또는 수집된 추가 데이터는 다음 날의 추정에 반영됩니다.

샘플 크기는 프로필 스토어의 전체 개체 수에 따라 달라집니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 스토어의 엔티티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1~2000만 | 100만 |
| 2,000만 이상 | 합계의 5% |

추정은 일반적으로 10-15초 이상 실행되며, 추정은 거친 것으로 시작되며 더 많은 기록을 읽으면 세부적으로 조정됩니다.

### 미리 보기 작업 만들기

종단점에 POST 요청을 만들어 새 미리 보기 작업을 만들 수 `/preview` 있습니다.

미리 보기 작업 만들기에 대한 자세한 지침은 미리 [보기 및 예상 끝점 안내서에서 확인할 수 있습니다](../api/previews-and-estimates.md#create-preview).

### 예상 또는 미리 보기 보기

서로 다른 쿼리가 완료하는 데 다른 시간이 걸릴 수 있으므로 미리 보기 및 예상 프로세스는 비동기적으로 실행됩니다. 쿼리가 시작되면 API 호출을 사용하여 진행 중인 예상 또는 미리 보기의 현재 상태를 검색(GET)할 수 있습니다.

API를 [!DNL Segmentation Service] 사용하여 미리 보기 작업의 현재 상태를 ID로 조회할 수 있습니다. 상태가 &quot;RESULT_READY&quot;인 경우 결과를 볼 수 있습니다. 미리 보기 작업의 현재 상태를 확인하려면 미리 보기 및 예상 끝점 안내서에서 미리 보기 작업 섹션 [을](../api/previews-and-estimates.md#get-preview) 검색하는 섹션을 참조하십시오. 예상 작업의 현재 상태를 확인하려면 미리 보기 및 예상 끝점 안내서에서 예상 작업 [을](../api/previews-and-estimates.md#get-estimate) 검색하는 섹션을 참조하십시오.


## 다음 단계

세그먼트 정의를 개발, 테스트 및 저장한 후에는 세그먼트 작업을 만들어 [!DNL Segmentation Service] API를 사용하여 대상을 만들 수 있습니다. 이를 수행하는 방법에 대한 자세한 [단계는 세그먼트 결과](./evaluate-a-segment.md) 평가 및 액세스에 대한 자습서를 참조하십시오.