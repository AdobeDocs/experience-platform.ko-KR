---
keywords: Experience Platform;홈;인기 항목;세그먼트 평가;세그먼테이션 서비스;세그먼테이션;세그먼테이션;세그먼트 평가;세그먼트 결과 액세스;세그먼트 평가 및 액세스
solution: Experience Platform
title: 세그먼트 결과 평가 및 액세스
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트를 평가하고 세그먼트 결과에 액세스하는 방법을 알려면 이 자습서를 따르십시오.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 453e120fa20232533289ee5ff34821ce8c0c310b
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 0%

---

# 세그먼트 결과 평가 및 액세스

이 문서에서는 [[!DNL Segmentation API]](../api/getting-started.md) 을 사용하여 세그먼트를 평가하고 세그먼트 결과에 액세스하는 자습서를 제공합니다.

## 시작

이 자습서에서는 대상 세그먼트 만들기와 관련된 다양한 [!DNL Adobe Experience Platform] 서비스를 이해하고 있어야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 고객 프로필을 실시간으로 제공합니다.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): 데이터에서 대상 세그먼트를 작성할 수  [!DNL Real-time Customer Profile] 있습니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [샌드박스](../../sandboxes/home.md):  [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필수 헤더

또한 이 자습서에서는 [!DNL Platform] API를 성공적으로 호출하기 위해 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에 필요한 각 헤더에 대한 값을 제공합니다.

- 권한 부여: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

## 세그먼트 평가

세그먼트 정의를 개발, 테스트 및 저장했으면 예약된 평가나 온디맨드 평가를 통해 세그먼트를 평가할 수 있습니다.

[예약된 평가](#scheduled-evaluation) (&#39;예약된 세그먼테이션&#39;이라고도 함)를 사용하면 특정 시간에 내보내기 작업을 실행하기 위한 반복 일정을 만들 수 있지만,  [온디맨드 ](#on-demand-evaluation) 평가에는 세그먼트를 만들어 대상을 즉시 빌드합니다. 각 단계에 대한 설명은 아래에 나와 있습니다.

[세그멘테이션 API](./create-a-segment.md) 자습서를 사용하여 세그먼트를 만들거나 [세그먼트 빌더](../ui/overview.md)를 사용하여 세그먼트 정의를 만든 적이 없는 경우 이 자습서를 계속 진행하기 전에 수행하십시오.

## 예약된 평가 {#scheduled-evaluation}

예약된 평가를 통해 IMS 조직은 내보내기 작업을 자동으로 실행하는 반복 일정을 만들 수 있습니다.

>[!NOTE]
>
>샌드박스에서 [!DNL XDM Individual Profile]에 대해 최대 5개의 병합 정책을 사용하는 예약된 평가를 사용하도록 설정할 수 있습니다. 조직에서 단일 샌드박스 환경 내에서 [!DNL XDM Individual Profile]에 대한 병합 정책이 5개 이상 있는 경우 예약된 평가를 사용할 수 없습니다.

### 예약 만들기

`/config/schedules` 종단점에 POST 요청을 수행하면 일정을 만들고 일정을 트리거해야 하는 특정 시간을 포함할 수 있습니다.

이 종단점 사용에 대한 자세한 내용은 [예약 종단점 안내서](../api/schedules.md#create)에 있습니다.

### 예약 활성화

기본적으로, 만들기(POST) 요청 본문에서 `state` 속성이 `active`로 설정되지 않은 경우 예약은 생성 시 비활성화됩니다. `/config/schedules` 종단점에 PATCH 요청을 하고 경로에 예약의 ID를 포함하여 일정을 활성화(`state`)할 수 있습니다.`active`

이 종단점 사용에 대한 자세한 내용은 [예약 종단점 안내서](../api/schedules.md#update-state)에 있습니다.

### 예약 시간 업데이트

예약 타이밍 은 `/config/schedules` 종단점에 PATCH 요청을 하고 경로에 예약의 ID를 포함하여 업데이트할 수 있습니다.

이 종단점 사용에 대한 자세한 내용은 [예약 종단점 안내서](../api/schedules.md#update-schedule)에 있습니다.

## 온디맨드 평가

온디맨드 평가를 통해 필요할 때마다 대상 세그먼트를 생성하기 위해 세그먼트 작업을 만들 수 있습니다. 예약된 평가와는 달리, 이 문제는 요청한 경우에만 발생하고 반복되지 않습니다.

### 세그먼트 작업 만들기

세그먼트 작업은 새 대상 세그먼트를 만드는 비동기 프로세스입니다. 이 시퀀스는 세그먼트 정의 및 [!DNL Real-time Customer Profile]이 프로필 조각에 겹치는 속성을 병합하는 방법을 제어하는 병합 정책을 참조합니다. 세그먼트 작업이 성공적으로 완료되면 처리 중에 발생할 수 있는 오류와 대상자의 최종 크기 등 세그먼트에 대한 다양한 정보를 수집할 수 있습니다.

[!DNL Real-time Customer Profile] API의 `/segment/jobs` 종단점에 POST 요청을 하여 새 세그먼트 작업을 만들 수 있습니다.

이 종단점 사용에 대한 자세한 내용은 [세그먼트 작업 종단점 안내서](../api/segment-jobs.md#create)에서 확인할 수 있습니다


### 세그먼트 작업 상태 조회

특정 세그먼트 작업에 `id` 을 사용하여 조회 요청(GET)을 수행하여 작업의 현재 상태를 볼 수 있습니다.

이 종단점 사용에 대한 자세한 내용은 [세그먼트 작업 종단점 안내서](../api/segment-jobs.md#get)에서 확인할 수 있습니다

## 세그먼트 결과 해석

세그먼트 작업이 성공적으로 실행되면 세그먼트 내에 포함된 각 프로필에 대해 `segmentMembership` 맵이 업데이트됩니다. `segmentMembership` 또한 는 와 같은 다른 솔루션과 통합할 수 있도록 수집된  [!DNL Platform]사전 평가된 대상 세그먼트를  [!DNL Adobe Audience Manager]저장합니다.

다음 예제에서는 각 개별 프로필 레코드에 대해 `segmentMembership` 속성이 어떻게 표시되는지 보여 줍니다.

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

사용하려는 특정 프로필을 알고 있는 경우 [!DNL Real-time Customer Profile] API를 사용하여 액세스할 수 있습니다. 개별 프로필에 액세스하는 전체 단계는 프로필 API](../../profile/api/entities.md) 자습서를 사용하여 [실시간 고객 프로필 데이터에 액세스 를 참조하십시오.

## 세그먼트 내보내기 {#export}

세분화 작업이 성공적으로 완료되면(`status` 속성 값이 &quot;SUCCEEDED&quot;) 대상을 액세스 및 작업할 수 있는 데이터 세트로 내보낼 수 있습니다.

대상자를 내보내려면 다음 단계를 수행해야 합니다.

- [대상 데이터 세트 만들기](#create-a-target-dataset)  - 대상 구성원을 보유할 데이터 세트를 만듭니다.
- [데이터 세트에서 대상 프로필 생성](#generate-profiles-for-audience-members)  - 세그먼트 작업의 결과를 기반으로 데이터 세트를 XDM 개별 프로필로 채웁니다.
- [내보내기 진행 모니터링](#monitor-export-progress)  - 내보내기 프로세스의 현재 진행 상태를 확인합니다.
- [대상 데이터 읽기](#next-steps)  - 대상자의 구성원을 나타내는 결과 XDM 개별 프로필을 검색합니다.

### 대상 데이터 세트 만들기

대상을 내보낼 때 먼저 타겟 데이터 세트를 만들어야 합니다. 내보내기가 성공하도록 데이터 세트를 올바르게 구성해야 합니다.

주요 고려 사항 중 하나는 데이터 세트가 기반으로 하는 스키마( 아래 API 샘플 요청에서`schemaRef.id`)입니다. 세그먼트를 내보내려면 데이터 세트가 [!DNL XDM Individual Profile Union Schema](`https://ns.adobe.com/xdm/context/profile__union`)을 기반으로 해야 합니다. 결합 스키마는 XDM 개별 프로필 클래스인 경우 동일한 클래스를 공유하는 스키마의 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다. 결합 보기 스키마에 대한 자세한 내용은 스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md)의 [실시간 고객 프로필 섹션을 참조하십시오.

필요한 데이터 세트를 만드는 방법에는 두 가지가 있습니다.

- **API 사용:** 이 자습서에서 수행하는 단계는  [!DNL XDM Individual Profile Union Schema]   [!DNL Catalog] API를 사용하여 를 참조하는 데이터 세트를 만드는 방법을 간략하게 설명합니다.
- **UI 사용:**  [!DNL Adobe Experience Platform] 사용자 인터페이스를 사용하여 결합 스키마를 참조하는 데이터 세트를 만들려면  [UI ](../ui/overview.md) 자습서의 단계를 수행한 다음 이 자습서로 돌아가 대상 프로필을  [생성하는 단계를](#generate-xdm-profiles-for-audience-members) 진행합니다.

이미 호환되는 데이터 세트가 있고 해당 ID를 알고 있는 경우 대상 프로필 생성](#generate-xdm-profiles-for-audience-members)에 대한 단계로 직접 진행할 수 있습니다.[

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

조합 지속 데이터 세트가 있으면 [!DNL Real-time Customer Profile] API에서 `/export/jobs` 종단점에 POST 요청을 하고 내보내려는 세그먼트에 대한 데이터 세트 ID 및 세그먼트 정보를 제공하여 대상 구성원을 데이터 집합에 유지하는 내보내기 작업을 만들 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [작업 내보내기 끝점 안내서](../api/export-jobs.md#create)에서 확인할 수 있습니다

### 내보내기 진행 모니터링

내보내기 작업 프로세스로서 `/export/jobs` 종단점에 GET 요청을 수행하고 경로에 내보내기 작업의 `id` 을 포함하여 해당 상태를 모니터링할 수 있습니다. `status` 필드가 &quot;SUCCEEDED&quot; 값을 반환하면 내보내기 작업이 완료됩니다.

이 끝점 사용에 대한 자세한 내용은 [작업 내보내기 끝점 안내서](../api/export-jobs.md#get)에서 확인할 수 있습니다

## 다음 단계

내보내기가 완료되면 [!DNL Experience Platform]의 [!DNL Data Lake] 내에서 데이터를 사용할 수 있습니다. 그런 다음 [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) 를 사용하여 내보내기와 연결된 `batchId`를 사용하여 데이터에 액세스할 수 있습니다. 세그먼트의 크기에 따라 데이터는 청크 단위일 수 있으며 배치는 여러 파일로 구성될 수 있습니다.

[!DNL Data Access] API를 사용하여 배치 파일에 액세스하고 다운로드하는 방법에 대한 단계별 지침은 [데이터 액세스 자습서](../../data-access/tutorials/dataset-data.md)를 따르십시오.

[!DNL Adobe Experience Platform Query Service] 을 사용하여 성공적으로 내보낸 세그먼트 데이터에 액세스할 수도 있습니다. UI 또는 RESTful API를 사용하는 경우 [!DNL Query Service]을(를) 사용하여 [!DNL Data Lake] 내의 데이터에 대해 쿼리를 작성, 유효성 검사 및 실행할 수 있습니다.

대상 데이터를 쿼리하는 방법에 대한 자세한 내용은 [[!DNL Query Service]](../../query-service/home.md)의 설명서를 참조하십시오.
