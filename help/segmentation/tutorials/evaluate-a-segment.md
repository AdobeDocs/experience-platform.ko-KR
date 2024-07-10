---
solution: Experience Platform
title: 세그먼트 결과 평가 및 액세스
type: Tutorial
description: Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트 정의를 평가하고 세그멘테이션 결과에 액세스하는 방법에 대해 알아보려면 이 자습서를 따르십시오.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 1%

---

# 세그먼트 정의 결과 평가 및 액세스

이 문서에서는 다음을 사용하여 세그먼트 정의를 평가하고 이러한 결과에 액세스하는 자습서를 제공합니다. [[!DNL Segmentation API]](../api/getting-started.md).

## 시작하기

이 자습서에서는 다양한 을(를) 작업 이해해야 합니다 [!DNL Adobe Experience Platform] 대상자 만들기와 관련된 서비스입니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계한 데이터를 기반으로 통합 고객 프로필을 실시간으로 제공합니다.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): 다음에서 대상자를 빌드할 수 있습니다. [!DNL Real-Time Customer Profile] 데이터.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다. 세그먼테이션을 최대한 활용하려면 데이터에 따라 프로필 및 이벤트가 수집되는지 확인하십시오. [데이터 모델링 우수 사례](../../xdm/schema/best-practices.md).
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

### 필수 헤더

이 자습서에서는 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 을(를) 성공적으로 호출하기 위해 [!DNL Platform] API. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

## 세그먼트 정의 평가 {#evaluate-a-segment}

세그먼트 정의를 개발, 테스트 및 저장했으면 예약된 평가 또는 온디맨드 평가를 통해 세그먼트 정의를 평가할 수 있습니다.

[예약된 평가](#scheduled-evaluation) (&#39;예약된 세그먼테이션&#39;이라고도 함) 특정 시간에 내보내기 작업 실행을 위한 반복 일정을 만들 수 있지만 [온디맨드 평가](#on-demand-evaluation) 에는 대상자를 즉시 빌드하기 위한 세그먼트 작업 생성이 포함됩니다. 각 단계에 대한 단계는 아래에 요약되어 있습니다.

아직 완료하지 않은 경우 [segmentation API를 사용하여 세그먼트 정의 만들기](./create-a-segment.md) 튜토리얼 또는 을 사용하여 세그먼트 정의를 만들었습니다. [세그먼트 빌더](../ui/segment-builder.md), 이 자습서를 계속 진행하기 전에 그렇게 하십시오.

## 예약된 평가 {#scheduled-evaluation}

예약된 평가를 통해 조직에서 반복 일정을 만들어 내보내기 작업을 자동으로 실행할 수 있습니다.

>[!NOTE]
>
>최대 5개의 병합 정책이 있는 샌드박스에 대해 예약된 평가를 활성화할 수 있습니다. [!DNL XDM Individual Profile]. 조직에 5개 이상의 병합 정책이 있는 경우 [!DNL XDM Individual Profile] 단일 샌드박스 환경 내에서는 예약된 평가를 사용할 수 없습니다.

### 일정 만들기

에 POST 요청 수행 `/config/schedules` 엔드포인트에서는 일정을 만들고 일정이 트리거되어야 하는 특정 시간을 포함할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [일정 끝점 안내서](../api/schedules.md#create)

### 일정 활성화

기본적으로 스케줄은 다음 경우를 제외하고 생성 시 비활성화됩니다. `state` 속성이 로 설정되어 있습니다. `active` (POST) 만들기 요청 본문에서 확인할 수 있습니다. 예약을 활성화할 수 있습니다(다음을 설정하십시오.) `state` 끝 `active`)에 PATCH 요청을 하여 `/config/schedules` 엔드포인트 및 경로에 일정 ID 포함.

이 끝점 사용에 대한 자세한 내용은 [일정 끝점 안내서](../api/schedules.md#update-state)

### 예약 시간 업데이트

에 PATCH 요청을 하여 예약 시간을 업데이트할 수 있습니다. `/config/schedules` 엔드포인트 및 경로에 일정 ID 포함.

이 끝점 사용에 대한 자세한 내용은 [일정 끝점 안내서](../api/schedules.md#update-schedule)

## 온디맨드 평가

온디맨드 평가를 사용하면 세그먼트 작업을 만들어 필요할 때마다 대상자를 생성할 수 있습니다. 예약된 평가와 달리, 이 작업은 요청된 경우에만 수행되며 반복되지 않습니다.

### 세그먼트 작업 만들기

세그먼트 작업은 요청 시 대상 세그먼트를 만드는 비동기 프로세스입니다. 세그먼트 정의와 방법을 제어하는 병합 정책을 참조합니다 [!DNL Real-Time Customer Profile] 은 프로필 조각에서 겹치는 속성을 병합합니다. 세그먼트 작업이 성공적으로 완료되면 처리 중에 발생할 수 있는 오류와 대상자의 최종 크기 등 세그먼트 정의에 대한 다양한 정보를 수집할 수 있습니다. 세그먼트 정의는 현재 세그먼트 정의가 적합한 대상자를 새로 고침할 때마다 실행되어야 합니다.

에 POST 요청을 하여 새 세그먼트 작업을 만들 수 있습니다. `/segment/jobs` 의 엔드포인트 [!DNL Real-Time Customer Profile] API.

이 끝점 사용에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서](../api/segment-jobs.md#create)

### 세그먼트 작업 상태 조회

다음을 사용할 수 있습니다. `id` 특정 세그먼트 작업에서 작업의 현재 상태를 보기 위해 조회 요청(GET)을 수행할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서](../api/segment-jobs.md#get)

## 세그먼트 작업 결과 해석

세그먼트 작업이 성공적으로 실행되면 `segmentMembership` 맵은 세그먼트 정의 내에 포함된 각 프로필에 대해 업데이트됩니다. `segmentMembership` 는 또한 수집되는 사전 평가된 대상자를 저장합니다. [!DNL Platform], 과 같은 다른 솔루션과 통합 가능 [!DNL Adobe Audience Manager].

다음 예제는 `segmentMembership` 속성은 각 개별 프로필 레코드에 대해 다음과 같습니다.

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
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
| `lastQualificationTime` | 세그먼트 멤버십이 어설션되고 프로필이 세그먼트 정의를 입력 또는 종료한 시점의 타임스탬프. |
| `status` | 현재 요청의 일부로 세그먼트 정의의 기여도 상태. 은(는) 다음 알려진 값 중 하나와 같아야 합니다. <ul><li>`realized`: 엔티티가 세그먼트 정의에 적합함.</li><li>`exited`: 엔티티가 세그먼트 정의를 종료하는 중입니다.</li></ul> |

>[!NOTE]
>
>에 있는 모든 세그먼트 멤버십 `exited` 을(를) 기준으로 30일 이상 상태 `lastQualificationTime`이 삭제될 수 있습니다.

## 세그먼트 작업 결과 액세스

세그먼트 작업의 결과는 다음 두 가지 방법 중 하나로 액세스할 수 있습니다. 개별 프로필에 액세스하거나 전체 대상을 데이터 세트로 내보낼 수 있습니다.

다음 섹션에서는 이러한 옵션에 대해 자세히 설명합니다.

## 프로필 조회

액세스하려는 특정 프로필을 알고 있는 경우 [!DNL Real-Time Customer Profile] API. 개별 프로필에 액세스하는 전체 단계는 [프로필 API를 사용하여 실시간 고객 프로필 데이터에 액세스](../../profile/api/entities.md) 튜토리얼.

## 세그먼트 내보내기 {#export}

세분화 작업이 성공적으로 완료된 후(값: `status` 속성은 &quot;SUCCEEDED&quot;)이며, 대상자를 액세스 및 작업이 가능한 데이터 세트로 내보낼 수 있습니다.

대상을 내보내려면 다음 단계가 필요합니다.

- [타겟 데이터 세트 만들기](#create-a-target-dataset) - 대상 구성원을 보관할 데이터 세트를 만듭니다.
- [데이터 세트에서 대상 프로필 생성](#generate-profiles) - 세그먼트 작업의 결과를 기반으로 데이터 세트를 XDM 개별 프로필로 채웁니다.
- [내보내기 진행 상황 모니터링](#monitor-export-progress) - 내보내기 프로세스의 현재 진행 상황을 확인합니다.
- [대상 데이터 읽기](#next-steps) - 대상자의 구성원을 나타내는 결과 XDM 개별 프로필을 검색합니다.

### 타겟 데이터 세트 만들기 {#create-dataset}

대상을 내보낼 때는 먼저 대상 데이터 세트를 만들어야 합니다. 내보내기가 성공하도록 데이터 세트를 올바르게 구성해야 합니다.

주요 고려 사항 중 하나는 데이터 세트의 기반이 되는 스키마 입니다(`schemaRef.id` (아래 API 샘플 요청). 세그먼트 정의를 내보내려면 데이터 세트가 [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). 유니온 스키마는 동일한 클래스를 공유하는 스키마의 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다(이 경우 XDM 개별 프로필 클래스). 유니온 보기 스키마에 대한 자세한 내용은 다음을 참조하십시오. [스키마 레지스트리 개발자 안내서의 실시간 고객 프로필 섹션](../../xdm/api/getting-started.md).

필요한 데이터 세트를 만드는 방법에는 두 가지가 있습니다.

- **API 사용:** 이 자습서의 다음 단계에서는 다음을 참조하는 데이터 세트를 만드는 방법을 간략하게 설명합니다. [!DNL XDM Individual Profile Union Schema] 사용 [!DNL Catalog] API.
- **UI 사용:** 을(를) 사용하려면 [!DNL Adobe Experience Platform] 유니온 스키마를 참조하는 데이터 세트를 만들려면 사용자 인터페이스 [UI 튜토리얼](../ui/overview.md) 그런 다음 이 튜토리얼로 돌아가서 의 단계를 계속합니다. [대상자 프로필 생성](#generate-profiles).

이미 호환되는 데이터 세트가 있고 해당 ID를 알고 있는 경우 다음 단계로 직접 진행할 수 있습니다. [대상자 프로필 생성](#generate-profiles).

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
| `schemaRef.id` | 데이터 세트와 연결할 유니온 뷰(스키마)의 ID입니다. |

**응답**

성공한 응답은 새로 만든 데이터 세트의 읽기 전용 시스템 생성 고유 ID가 포함된 배열을 반환합니다. 대상 구성원을 성공적으로 내보내려면 적절하게 구성된 데이터 세트 ID가 필요합니다.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 대상자 구성원에 대한 프로필 생성 {#generate-profiles}

유니온이 지속되는 데이터 세트가 있는 경우 POST에 요청을 하여 대상 구성원을 데이터 세트에 지속하는 내보내기 작업을 만들 수 있습니다. `/export/jobs` 의 엔드포인트 [!DNL Real-Time Customer Profile] API를 제공하고, 내보내려는 세그먼트 정의에 대한 데이터 세트 ID와 세그먼트 정의 정보를 제공합니다.

이 끝점 사용에 대한 자세한 내용은 [내보내기 작업 엔드포인트 안내서](../api/export-jobs.md#create)

### 내보내기 진행 상황 모니터링

내보내기 작업 프로세스에서에 GET 요청을 하여 상태 모니터링 `/export/jobs` 엔드포인트 및 포함 `id` 경로의 내보내기 작업. 내보내기 작업이 완료되면 다음과 같은 작업이 완료됩니다. `status` 필드는 &quot;SUCCEEDED&quot; 값을 반환합니다.

이 끝점 사용에 대한 자세한 내용은 [내보내기 작업 엔드포인트 안내서](../api/export-jobs.md#get)

## 다음 단계

내보내기가 완료되면 데이터 를 [!DNL Data Lake] 위치: [!DNL Experience Platform]. 그런 다음 를 사용할 수 있습니다. [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 을 사용하여 데이터에 액세스 `batchId` 내보내기와 연결되었습니다. 세그먼트 정의의 크기에 따라 데이터는 청크 단위일 수 있으며 배치는 여러 파일로 구성될 수 있습니다.

사용 방법에 대한 단계별 지침: [!DNL Data Access] 배치 파일에 액세스하고 다운로드하려면 API를 [데이터 액세스 자습서](../../data-access/tutorials/dataset-data.md).

을 사용하여 성공적으로 내보낸 세그먼트 정의 데이터에 액세스할 수도 있습니다. [!DNL Adobe Experience Platform Query Service]. UI 또는 RESTful API를 사용하여 [!DNL Query Service] 을(를) 사용하면 내에서 데이터에 대한 쿼리를 작성하고, 유효성을 검사하고, 실행할 수 있습니다. [!DNL Data Lake].

대상 데이터를 쿼리하는 방법에 대한 자세한 내용은 [[!DNL Query Service]](../../query-service/home.md).
