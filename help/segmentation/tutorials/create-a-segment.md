---
solution: Experience Platform
title: 세분화 서비스 API를 사용하여 세그먼트 정의 만들기
type: Tutorial
description: Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트 정의를 개발, 테스트, 미리 보기 및 저장하는 방법을 배우려면 이 자습서를 따르십시오.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 6%

---

# 세분화 서비스 API를 사용하여 세그먼트 정의 만들기

이 문서에서는 [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md)을(를) 사용하여 세그먼트 정의를 개발, 테스트, 미리 보기 및 저장하는 방법에 대한 자습서를 제공합니다.

사용자 인터페이스를 사용하여 세그먼트 정의를 만드는 방법에 대한 자세한 내용은 [세그먼트 빌더 안내서](../ui/segment-builder.md)를 참조하십시오.

## 시작하기

이 자습서에서는 세그먼트 정의를 만드는 데 관련된 다양한 [!DNL Adobe Experience Platform] 서비스에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): 실시간 고객 프로필 데이터의 세그먼트 정의나 기타 외부 소스를 사용하여 대상자를 만들 수 있습니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다. 세그먼테이션을 최대한 활용하려면 [데이터 모델링 모범 사례](../../xdm/schema/best-practices.md)에 따라 데이터가 프로필 및 이벤트로 수집되는지 확인하십시오.

다음 섹션에서는 [!DNL Experience Platform] API를 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Experience Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Experience Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

## 세그먼트 정의 개발

세그먼테이션의 첫 번째 단계는 세그먼트 정의를 정의하는 것입니다. 세그먼트 정의는 [!DNL Profile Query Language]&#x200B;(PQL)로 작성된 쿼리를 캡슐화하는 개체입니다. 이 개체를 PQL 술어라고도 합니다. PQL 조건자는 [!DNL Real-Time Customer Profile]에 제공한 레코드 또는 시계열 데이터와 관련된 조건을 기반으로 세그먼트 정의에 대한 규칙을 정의합니다. PQL 쿼리 작성에 대한 자세한 내용은 [PQL 안내서](../pql/overview.md)를 참조하십시오.

[!DNL Segmentation] API의 `/segment/definitions` 끝점에 대한 POST 요청을 수행하여 새 세그먼트 정의를 만들 수 있습니다. 다음 예제에서는 세그먼트 정의를 성공적으로 정의하는 데 필요한 정보를 포함하여 정의 요청의 형식을 지정하는 방법을 간략하게 설명합니다.

세그먼트 정의를 정의하는 방법에 대한 자세한 내용은 [세그먼트 정의 개발자 안내서](../api/segment-definitions.md#create)를 참조하십시오.

## 대상자 예측 및 미리보기 {#estimate-and-preview-an-audience}

세그먼트 정의를 개발할 때 [!DNL Real-Time Customer Profile] 내의 예상 및 미리 보기 도구를 사용하여 요약 수준 정보를 보고 예상 대상을 격리할 수 있습니다. 예상치는 예상 대상 크기 및 신뢰 구간과 같은 세그먼트 정의에 대한 통계 정보를 제공합니다. 미리 보기는 세그먼트 정의에 대해 페이지가 매겨진 자격 프로필 목록을 제공하므로 결과를 예상과 비교할 수 있습니다.

대상자를 예측하고 미리 보면 원하는 결과가 나올 때까지 PQL 술어를 테스트하고 최적화하여 업데이트된 세그먼트 정의에 사용할 수 있습니다.

세그먼트 정의를 미리 보거나 예상 값을 가져오는 데 필요한 두 가지 단계가 있습니다.

1. [미리보기 작업 만들기](#create-a-preview-job)
2. 미리 보기 작업의 ID를 사용하여 [예상 또는 미리 보기](#view-an-estimate-or-preview)

### 예상 생성 방법

실시간 고객 프로필에 대해 활성화된 데이터가 Experience Platform에 수집되면 프로필 데이터 저장소 내에 저장됩니다. 프로필 스토어로 레코드를 수집하면 총 프로필 수가 5% 이상 증가하거나 감소하면 샘플링 작업이 트리거되어 수를 업데이트합니다. 프로필 수가 5% 이상 변경되지 않으면 샘플링 작업이 매주 자동으로 실행됩니다.

샘플이 트리거되는 방법은 사용 중인 수집 유형에 따라 다릅니다.

- 스트리밍 데이터 워크플로의 경우 5% 증가 또는 감소 임계값이 충족되었는지 확인하기 위해 시간별로 검사가 수행됩니다. 이 임계값이 충족되면 샘플 작업이 자동으로 트리거되어 카운트를 업데이트합니다.
- 일괄 처리 수집의 경우, 프로필 스토어에 일괄 처리를 성공적으로 수집한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 카운트를 업데이트하는 작업이 실행됩니다. 프로필 API를 사용하면 최근에 성공한 샘플 작업을 미리 볼 수 있으며, 데이터 세트 및 ID 네임스페이스별로 프로필 분포를 나열할 수 있습니다.

샘플 크기는 프로필 스토어에 있는 전체 엔티티 수에 따라 다릅니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 저장소의 엔티티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1000~2000만 | 100만 |
| 2,000만 이상 | 총 5% |

예측은 일반적으로 10-15초 동안 실행되며, 대략적인 예측부터 시작하여 더 많은 기록을 읽을수록 구체화됩니다.

### 미리보기 작업 만들기

`/preview` 끝점에 대한 POST 요청을 수행하여 새 미리 보기 작업을 만들 수 있습니다.

미리 보기 작업을 만드는 방법에 대한 자세한 지침은 [미리 보기 및 예상 끝점 안내서](../api/previews-and-estimates.md#create-preview)에서 확인할 수 있습니다.

### 예상 보기 또는 미리 보기

서로 다른 쿼리가 완료되는 데 시간이 오래 걸릴 수 있으므로 예상 및 미리보기 프로세스는 비동기적으로 실행됩니다. 쿼리가 시작되면 API 호출을 사용하여 예측이나 미리보기가 진행되는 현재 상태를 검색(GET)할 수 있습니다.

[!DNL Segmentation Service] API를 사용하여 미리보기 작업의 현재 상태를 해당 ID로 조회할 수 있습니다. 상태가 &quot;RESULT_READY&quot;이면 결과를 볼 수 있습니다. 미리 보기 작업의 현재 상태를 조회하려면 미리 보기 및 예상 끝점 안내서에서 [미리 보기 작업 섹션 검색](../api/previews-and-estimates.md#get-preview)에 대한 섹션을 읽어 보십시오. 예상 작업의 현재 상태를 조회하려면 미리 보기 및 예상 끝점 안내서에서 [예상 작업 검색](../api/previews-and-estimates.md#get-estimate) 섹션을 참조하십시오.


## 다음 단계

세그먼트 정의를 개발, 테스트 및 저장했으면 [!DNL Segmentation Service] API를 사용하여 대상자를 빌드하는 세그먼트 작업을 만들 수 있습니다. 이를 수행하는 방법에 대한 자세한 단계는 [세그먼트 결과 평가 및 액세스](./evaluate-a-segment.md)에 대한 자습서를 참조하십시오.
