---
keywords: Experience Platform;홈;인기 항목;세그먼트 평가;세그먼테이션 서비스;세그먼테이션;세그먼테이션;세그먼트 평가;세그먼트 결과 액세스;세그먼트 평가 및 액세스
solution: Experience Platform
title: 세그먼트 결과 평가 및 액세스
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트를 평가하고 세그먼트 결과에 액세스하는 방법을 알려면 이 자습서를 따르십시오.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---

# 세그먼트 결과 평가 및 액세스

이 문서에서는 세그먼트를 평가하고 [[!DNL Segmentation API]](../api/getting-started.md).

## 시작하기

이 자습서에서는 다양한 자습서를 이해하고 있어야 합니다 [!DNL Adobe Experience Platform] 대상 세그먼트 만들기에 관련된 서비스입니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 고객 프로필을 실시간으로 제공합니다.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): 대상 세그먼트를 [!DNL Real-Time Customer Profile] 데이터.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다. 세그멘테이션을 가장 잘 사용하려면 데이터가 [데이터 모델링 우수 사례](../../xdm/schema/best-practices.md).
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

### 필수 헤더

또한 이 자습서에서는 다음을 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 을 성공적으로 호출하기 위해 [!DNL Platform] API. 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

- 권한 부여: 베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 요청 대상 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

## 세그먼트 평가 {#evaluate-a-segment}

세그먼트 정의를 개발, 테스트 및 저장했으면 예약된 평가나 온디맨드 평가를 통해 세그먼트를 평가할 수 있습니다.

[예약된 평가](#scheduled-evaluation) (예약된 세그먼테이션이라고도 함) 을 사용하면 특정 시간에 내보내기 작업을 실행하기 위한 반복 일정을 만들 수 있지만, [온디맨드 평가](#on-demand-evaluation) 에는 세그먼트 작업 만들기가 포함되어 대상자를 즉시 만듭니다. 각 단계에 대한 설명은 아래에 나와 있습니다.

을(를) 아직 완료하지 않았다면 [세분화 API를 사용하여 세그먼트 만들기](./create-a-segment.md) 자습서 또는 을 사용하여 세그먼트 정의 만들기 [세그먼트 빌더](../ui/overview.md)을 눌러 이 자습서를 계속 진행하십시오.

## 예약된 평가 {#scheduled-evaluation}

예약된 평가를 통해 IMS 조직은 내보내기 작업을 자동으로 실행하는 반복 일정을 만들 수 있습니다.

>[!NOTE]
>
>샌드박스에 대해 예약된 평가를 사용하도록 설정할 수 있으며 최대 5개의 병합 정책이 있습니다 [!DNL XDM Individual Profile]. 조직에 5개 이상의 병합 정책이 있는 경우 [!DNL XDM Individual Profile] 단일 샌드박스 환경 내에서 예약된 평가를 사용할 수 없습니다.

### 예약 만들기

에 POST 요청을 함으로써 `/config/schedules` 종단점을 위해 일정을 만들고 일정을 트리거해야 하는 특정 시간을 포함할 수 있습니다.

이 종단점 사용에 대한 자세한 내용은 [endpoint 안내서](../api/schedules.md#create)

### 예약 활성화

기본적으로 예약은 `state` 속성이 `active` 만들기(POST) 요청 본문에서 일정을 활성화( `state` to `active`)에 PATCH 요청을 함으로써 `/config/schedules` 엔드포인트 및 경로에 예약의 ID를 포함합니다.

이 종단점 사용에 대한 자세한 내용은 [endpoint 안내서](../api/schedules.md#update-state)

### 예약 시간 업데이트

에 PATCH 요청을 작성하여 예약 타이밍을 업데이트할 수 있습니다 `/config/schedules` 엔드포인트 및 경로에 예약의 ID를 포함합니다.

이 종단점 사용에 대한 자세한 내용은 [endpoint 안내서](../api/schedules.md#update-schedule)

## 온디맨드 평가

온디맨드 평가를 통해 필요할 때마다 대상 세그먼트를 생성하기 위해 세그먼트 작업을 만들 수 있습니다. 예약된 평가와는 달리, 이 문제는 요청한 경우에만 발생하고 반복되지 않습니다.

### 세그먼트 작업 만들기

세그먼트 작업은 주문형 대상 세그먼트를 만드는 비동기 프로세스입니다. 세그먼트 정의 및 방법을 제어하는 병합 정책을 참조합니다 [!DNL Real-Time Customer Profile] 프로필 조각에서 겹치는 속성을 병합합니다. 세그먼트 작업이 성공적으로 완료되면 처리 중에 발생할 수 있는 오류와 대상자의 최종 크기 등 세그먼트에 대한 다양한 정보를 수집할 수 있습니다. 현재 세그먼트 정의에 적격인 대상을 새로 고치려면 매번 세그먼트 작업을 실행해야 합니다.

에 POST 요청을 만들어 새 세그먼트 작업을 만들 수 있습니다 `/segment/jobs` 의 엔드포인트 [!DNL Real-Time Customer Profile] API.

이 종단점 사용에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서](../api/segment-jobs.md#create)

### 세그먼트 작업 상태 조회

를 사용할 수 있습니다 `id` 작업의 현재 상태를 보기 위해 조회 요청(GET)을 수행하는 특정 세그먼트 작업의 경우.

이 종단점 사용에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서](../api/segment-jobs.md#get)

## 세그먼트 결과 해석

세그먼트 작업이 성공적으로 실행되면 `segmentMembership` 맵은 세그먼트 내에 포함된 각 프로필에 대해 업데이트됩니다. `segmentMembership` 또한 에 수집되는 미리 평가된 대상 세그먼트를 저장합니다 [!DNL Platform]와 같은 다른 솔루션과 통합 허용 [!DNL Adobe Audience Manager].

다음 예는 `segmentMembership` 속성은 각 개별 프로필 레코드에 대한 것처럼 보입니다.

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `lastQualificationTime` | 세그먼트 멤버십 검증이 이루어지고 프로필이 세그먼트에 들어오거나 종료한 타임스탬프. |
| `status` | 현재 요청의 일부로서 세그먼트 기여도 상태입니다. 다음 알려진 값 중 하나와 같아야 합니다. <ul><li>`existing`: 엔티티는 세그먼트에 계속 있습니다.</li><li>`realized`: 엔티티가 세그먼트를 입력하고 있습니다.</li><li>`exited`: 엔티티가 세그먼트를 종료하고 있습니다.</li></ul> |

## 세그먼트 결과 액세스

세그먼트 작업 결과는 다음 두 가지 방법 중 하나로 액세스할 수 있습니다. 개별 프로필에 액세스하거나 전체 대상자를 데이터 세트에 내보낼 수 있습니다.

다음 섹션에서는 이러한 옵션에 대해 자세히 설명합니다.

## 프로필 조회

액세스할 특정 프로필을 알고 있는 경우 [!DNL Real-Time Customer Profile] API. 개별 프로필에 액세스하는 전체 단계는 [프로필 API를 사용하여 실시간 고객 프로필 데이터에 액세스](../../profile/api/entities.md) 자습서입니다.

## 세그먼트 내보내기 {#export}

세분화 작업이 성공적으로 완료된 후( `status` 속성이 &quot;성공&quot;)이면 대상을 액세스 및 작업할 수 있는 데이터 세트로 내보낼 수 있습니다.

대상자를 내보내려면 다음 단계를 수행해야 합니다.

- [대상 데이터 세트 만들기](#create-a-target-dataset) - 대상 구성원을 보유할 데이터 세트를 만듭니다.
- [데이터 집합에서 대상 프로필 생성](#generate-profiles) - 세그먼트 작업 결과를 기반으로 데이터 세트를 XDM 개별 프로필로 채웁니다.
- [내보내기 진행 모니터링](#monitor-export-progress) - 내보내기 프로세스의 현재 진행 상태를 확인합니다.
- [대상 데이터 읽기](#next-steps) - 대상자의 구성원을 나타내는 결과 XDM 개별 프로필을 검색합니다.

### 대상 데이터 세트 만들기 {#create-dataset}

대상을 내보낼 때 먼저 타겟 데이터 세트를 만들어야 합니다. 내보내기가 성공하도록 데이터 세트를 올바르게 구성해야 합니다.

주요 고려 사항 중 하나는 데이터 세트가 기반으로 하는 스키마입니다(`schemaRef.id` 를 반환합니다. 세그먼트를 내보내려면 데이터 세트가 [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). 결합 스키마는 XDM 개별 프로필 클래스인 경우 동일한 클래스를 공유하는 스키마의 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다. 결합 보기 스키마에 대한 자세한 내용은 [스키마 레지스트리 개발자 가이드의 실시간 고객 프로필 섹션](../../xdm/api/getting-started.md).

필요한 데이터 세트를 만드는 방법에는 두 가지가 있습니다.

- **API 사용:** 이 자습서에서 수행하는 단계는 를 참조하는 데이터 세트를 만드는 방법을 간략하게 설명합니다 [!DNL XDM Individual Profile Union Schema] 사용 [!DNL Catalog] API.
- **UI 사용:** 를 사용하려면 [!DNL Adobe Experience Platform] 사용자 인터페이스를 사용하여 결합 스키마를 참조하는 데이터 세트를 만들려면 [UI 자습서](../ui/overview.md) 그런 다음 이 자습서로 돌아가 다음 단계를 계속 진행합니다. [대상 프로필 생성](#generate-profiles).

이미 호환되는 데이터 세트가 있고 해당 ID를 알고 있는 경우 다음 단계로 직접 진행할 수 있습니다 [대상 프로필 생성](#generate-profiles).

**API 형식**

```http
POST /dataSets
```

**요청**

다음 요청은 페이로드에 구성 매개 변수를 제공하는 새 데이터 세트를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 데이터 세트에 대한 수사적 이름입니다. |
| `schemaRef.id` | 데이터 집합과 연결할 결합 보기(스키마)의 ID입니다. |

**응답**

성공적인 응답은 새로 생성된 데이터 세트의 읽기 전용 시스템 생성 고유 ID가 포함된 배열을 반환합니다. 대상 구성원을 성공적으로 내보내려면 올바르게 구성된 데이터 세트 ID가 필요합니다.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 대상 구성원의 프로필 생성 {#generate-profiles}

조합 지속 데이터 세트가 있을 경우, 에 POST 요청을 수행하여 대상 구성원을 데이터 집합에 유지하는 내보내기 작업을 만들 수 있습니다 `/export/jobs` 의 엔드포인트 [!DNL Real-Time Customer Profile] 내보낼 세그먼트에 대한 데이터 세트 ID와 세그먼트 정보를 API로 제공하고 제공합니다.

이 종단점 사용에 대한 자세한 내용은 [작업 끝점 내보내기 안내서](../api/export-jobs.md#create)

### 내보내기 진행 모니터링

내보내기 작업 프로세스에서에 GET 요청을 수행하여 상태를 모니터링할 수 있습니다 `/export/jobs` 엔드포인트 및 포함 `id` 경로에 있는 내보내기 작업의 수입니다. 내보내기 작업은 다음에 대한 `status` 필드는 값 &quot;SUCCEEDED&quot;를 반환합니다.

이 종단점 사용에 대한 자세한 내용은 [작업 끝점 내보내기 안내서](../api/export-jobs.md#get)

## 다음 단계

내보내기가 완료되면 내에서 데이터를 사용할 수 있습니다 [!DNL Data Lake] in [!DNL Experience Platform]. 그런 다음 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 를 사용하여 데이터에 액세스하려면 `batchId` 내보내기와 연관됩니다. 세그먼트의 크기에 따라 데이터는 청크 단위일 수 있으며 배치는 여러 파일로 구성될 수 있습니다.

를 사용하는 방법에 대한 단계별 지침 [!DNL Data Access] API를 사용하여 일괄 처리 파일에 액세스하고 다운로드할 수 있는 경우 [데이터 액세스 자습서](../../data-access/tutorials/dataset-data.md).

를 사용하여 성공적으로 내보낸 세그먼트 데이터에 액세스할 수도 있습니다 [!DNL Adobe Experience Platform Query Service]. UI 또는 RESTful API 사용, [!DNL Query Service] 에서는 내의 데이터에 대한 쿼리를 작성, 유효성 검사 및 실행할 수 있습니다 [!DNL Data Lake].

대상 데이터를 쿼리하는 방법에 대한 자세한 내용은 [[!DNL Query Service]](../../query-service/home.md).
