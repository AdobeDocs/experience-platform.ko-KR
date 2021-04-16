---
keywords: Experience Platform;홈;인기 항목;세그먼트 평가;세그멘테이션 서비스;세그멘테이션;세그먼트 평가;액세스 세그먼트 결과;평가 및 액세스 세그먼트
solution: Experience Platform
title: 세그먼트 결과 평가 및 액세스
topic: 자습서
type: Tutorial
description: Adobe Experience Platform 세그멘테이션 서비스 API를 사용하여 세그먼트를 평가하고 세그먼트 결과에 액세스하는 방법을 알아보려면 이 자습서를 따르십시오.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
translation-type: tm+mt
source-git-commit: 87729e4996b0b2ac26e1a0abaa80af717825f9e6
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 세그먼트 결과 평가 및 액세스

이 문서에서는 [[!DNL Segmentation API]](../api/getting-started.md)을 사용하여 세그먼트를 평가하고 세그먼트 결과에 액세스하는 자습서를 제공합니다.

## 시작하기

이 자습서에서는 대상 세그먼트 만들기와 관련된 다양한 [!DNL Adobe Experience Platform] 서비스에 대해 제대로 이해해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 수집한 데이터를 기반으로 통합된 고객 프로파일을 실시간으로 제공합니다.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):데이터에서 대상 세그먼트를 만들 수  [!DNL Real-time Customer Profile] 있습니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform(플랫폼)이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필수 헤더

또한 이 자습서에서는 [!DNL Platform] API를 성공적으로 호출하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:Bearer `{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 세그먼트 평가

세그먼트 정의를 개발, 테스트 및 저장한 후에는 예약된 평가나 주문형 평가를 통해 세그먼트를 평가할 수 있습니다.

[예약된 평가](#scheduled-evaluation) (일명 &#39;예약된 세그멘테이션&#39;이라고도 함)를 사용하면 특정 시간에 내보내기 작업을 실행할 수 있는 반복 일정을 만들 수 있지만,  [on-demand 평가에는 ](#on-demand-evaluation) 세그먼트 작업을 생성하여 대상을 즉시 작성할 수 있습니다. 각 단계에 대한 설명은 아래에 나와 있습니다.

아직 [세그멘테이션 API](./create-a-segment.md) 자습서를 사용하여 세그먼트 만들기를 완료하지 않았거나 [세그먼트 빌더](../ui/overview.md)를 사용하여 세그먼트 정의를 만든 경우에는 이 자습서를 진행하기 전에 그렇게 하십시오.

## 예약된 평가 {#scheduled-evaluation}

예약된 평가를 통해, IMS 조직에서 반복 일정을 생성하여 내보내기 작업을 자동으로 실행할 수 있습니다.

>[!NOTE]
>
>[!DNL XDM Individual Profile]에 대해 최대 5개의 병합 정책이 있는 샌드박스에 대해 예약된 평가를 활성화할 수 있습니다. 조직에서 단일 샌드박스 환경 내에서 [!DNL XDM Individual Profile]에 대한 병합 정책이 5개 이상 있는 경우 예약된 평가를 사용할 수 없습니다.

### 일정 만들기

`/config/schedules` 끝점에 POST 요청을 함으로써 일정을 만들고 일정을 트리거해야 하는 특정 시간을 포함할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [예약 끝점 안내서](../api/schedules.md#create)에서 확인할 수 있습니다.

### 예약 활성화

만들기(POST) 요청 본문에 `state` 속성이 `active`으로 설정되어 있지 않으면 기본적으로 일정이 만들어지면 비활성화됩니다. `/config/schedules` 종단점에 PATCH 요청을 하고 경로에 있는 예약의 ID를 포함하여 일정(`state` 을 `active` 로 설정)을 활성화할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [예약 끝점 안내서](../api/schedules.md#update-state)에서 확인할 수 있습니다.

### 예약 시간 업데이트

일정 시간 단축은 `/config/schedules` 끝점에 PATCH 요청을 하고 경로에 예약의 ID를 포함하여 업데이트할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [예약 끝점 안내서](../api/schedules.md#update-schedule)에서 확인할 수 있습니다.

## On-Demand 평가

주문형 평가를 통해 필요할 때마다 대상 세그먼트를 생성하기 위해 세그먼트 작업을 만들 수 있습니다. 예약된 평가와 달리, 이것은 요청이 있을 때만 발생하며 반복되지 않습니다.

### 세그먼트 작업 만들기

세그먼트 작업은 새 대상 세그먼트를 만드는 비동기 프로세스입니다. 세그먼트 정의를 참조하고, [!DNL Real-time Customer Profile]이 프로필 조각에 겹치는 특성을 병합하는 방법을 제어하는 모든 병합 정책을 참조합니다. 세그먼트 작업이 성공적으로 완료되면 처리 중에 발생한 오류와 대상의 최종 크기 등 세그먼트에 대한 다양한 정보를 수집할 수 있습니다.

[!DNL Real-time Customer Profile] API의 `/segment/jobs` 끝점에 POST 요청을 하여 새 세그먼트 작업을 만들 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서](../api/segment-jobs.md#create)에서 확인할 수 있습니다.


### 세그먼트 작업 상태 보기

작업의 현재 상태를 보려면 특정 세그먼트 작업에 `id`을 사용하여 조회 요청(GET)을 수행할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서](../api/segment-jobs.md#get)에서 확인할 수 있습니다.

## 세그먼트 결과 해석

세그먼트 작업이 성공적으로 실행되면 세그먼트 내에 포함된 각 프로필에 대해 `segmentMembership` 맵이 업데이트됩니다. `segmentMembership` 인제스트된 사전 평가 대상 세그먼트를 저장하므로 [!DNL Platform]와 같은 다른 솔루션과 통합할 수 있습니다 [!DNL Adobe Audience Manager].

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
| `lastQualificationTime` | 세그먼트 구성원 자격 어설션이 이루어지고 프로필이 세그먼트를 입력하거나 종료한 타임스탬프. |
| `status` | 현재 요청의 일부로서 세그먼트 기여도 상태입니다. 다음 알려진 값 중 하나와 같아야 합니다. <ul><li>`existing`:엔티티가 세그먼트에 계속 있습니다.</li><li>`realized`:엔티티가 세그먼트를 입력하고 있습니다.</li><li>`exited`:엔티티가 세그먼트를 종료합니다.</li></ul> |

## 세그먼트 결과 액세스

다음 두 가지 방법 중 하나로 세그먼트 작업 결과에 액세스할 수 있습니다.개별 프로파일에 액세스하거나 전체 고객을 데이터 세트로 내보낼 수 있습니다.

다음 섹션에서는 이러한 옵션에 대해 자세히 설명합니다.

## 프로필 찾기

액세스하려는 특정 프로파일을 알고 있는 경우 [!DNL Real-time Customer Profile] API를 사용하여 액세스할 수 있습니다. 개별 프로파일에 액세스하기 위한 전체 단계는 프로파일 API](../../profile/api/entities.md) 튜토리얼을 사용하여 [실시간 고객 프로필 데이터에 액세스하는 것입니다.

## 세그먼트 {#export} 내보내기

세그멘테이션 작업이 성공적으로 완료된 후(`status` 속성의 값이 &quot;성공&quot;됨), 액세스 및 작업이 가능한 데이터 세트로 대상을 내보낼 수 있습니다.

대상을 내보내려면 다음 단계가 필요합니다.

- [대상 데이터 세트](#create-a-target-dataset)  만들기 - 대상 구성원을 포함할 데이터 세트를 만듭니다.
- [데이터 세트에서 대상 프로필 생성](#generate-profiles-for-audience-members)  - 세그먼트 작업의 결과를 기반으로 XDM 개별 프로필로 데이터 세트를 채웁니다.
- [내보내기 진행](#monitor-export-progress)  모니터링 - 내보내기 프로세스의 현재 진행 상태를 확인합니다.
- [대상 데이터](#next-steps)  읽기 - 대상 구성원을 나타내는 결과 XDM 개별 프로필을 검색합니다.

### 대상 데이터 세트 만들기

대상을 내보낼 때 대상 데이터 세트를 먼저 만들어야 합니다. 내보내기가 성공하도록 데이터 세트를 올바르게 구성해야 합니다.

중요 고려 사항 중 하나는 데이터 세트가 기반이 되는 스키마(아래 API 샘플 요청에서 `schemaRef.id`)입니다. 세그먼트를 내보내려면 데이터 세트는 [!DNL XDM Individual Profile Union Schema](`https://ns.adobe.com/xdm/context/profile__union`)을 기반으로 해야 합니다. 결합 스키마는 동일한 클래스를 공유하는 스키마 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다. 이 경우 XDM 개별 프로필 클래스입니다. 결합 보기 스키마에 대한 자세한 내용은 스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md)의 [실시간 고객 프로필 섹션을 참조하십시오.

다음 두 가지 방법으로 필요한 데이터 세트를 만들 수 있습니다.

- **API 사용:** 이 자습서의 다음 단계는  [!DNL XDM Individual Profile Union Schema] API를  [!DNL Catalog] 사용하여 참조하는 데이터 세트를 만드는 방법에 대해 간략히 설명합니다.
- **UI 사용:**  [!DNL Adobe Experience Platform] 사용자 인터페이스를 사용하여 조합 스키마를 참조하는 데이터 세트를 만들려면  [UI ](../ui/overview.md) 튜토리얼에서 단계를 수행한 후 이 튜토리얼로 돌아와 대상 프로필을  [생성하는 단계를 ](#generate-xdm-profiles-for-audience-members)진행하십시오.

이미 호환되는 데이터 세트가 있고 해당 ID를 알고 있는 경우 [대상 프로필 생성](#generate-xdm-profiles-for-audience-members)의 단계로 직접 진행할 수 있습니다.

**API 형식**

```http
POST /dataSets
```

**요청**

다음 요청은 페이로드에서 구성 매개 변수를 제공하는 새 데이터 세트를 만듭니다.

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
    },
    "fileDescription": {
        "persisted": true
    }
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 데이터 세트에 대한 설명형 이름입니다. |
| `schemaRef.id` | 데이터 집합과 연결할 통합 보기(스키마)의 ID입니다. |
| `fileDescription.persisted` | `true`으로 설정하면 데이터 세트가 조합 보기에서 유지될 수 있도록 하는 부울 값입니다. |

**응답**

성공적인 응답은 새로 만든 데이터 세트의 읽기 전용 시스템 생성 고유 ID가 포함된 배열을 반환합니다. 대상 구성원을 성공적으로 내보내려면 제대로 구성된 데이터 집합 ID가 필요합니다.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 대상 멤버 {#generate-profiles} 프로필 생성

조합 지속 데이터 집합이 있으면 내보내기 작업을 만들어 [!DNL Real-time Customer Profile] API의 `/export/jobs` 끝점에 POST 요청을 하고 내보내려는 세그먼트에 대한 데이터 집합 ID 및 세그먼트 정보를 제공하여 대상 구성원을 데이터 집합에 유지할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [내보내기 작업 끝점 안내서](../api/export-jobs.md#create)에서 확인할 수 있습니다.

### 내보내기 진행 상태 모니터링

내보내기 작업 과정에서는 경로에 내보내기 작업의 `/export/jobs`을 포함하여 `id` 끝점에 GET 요청을 하여 상태를 모니터링할 수 있습니다. `status` 필드가 &quot;SUCCEEDED&quot; 값을 반환하면 내보내기 작업이 완료됩니다.

이 끝점 사용에 대한 자세한 내용은 [내보내기 작업 끝점 안내서](../api/export-jobs.md#get)에서 확인할 수 있습니다.

## 다음 단계

내보내기가 성공적으로 완료되면 [!DNL Experience Platform]의 [!DNL Data Lake] 내에서 데이터를 사용할 수 있습니다. 그런 다음 [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)을 사용하여 내보내기와 연결된 `batchId`을 사용하여 데이터에 액세스할 수 있습니다. 세그먼트 크기에 따라 데이터가 청크 단위일 수 있으며 일괄 처리는 여러 파일로 구성될 수 있습니다.

[!DNL Data Access] API를 사용하여 일괄 파일에 액세스하고 다운로드하는 방법에 대한 단계별 지침을 보려면 [데이터 액세스 자습서](../../data-access/tutorials/dataset-data.md)를 따르십시오.

[!DNL Adobe Experience Platform Query Service]을(를) 사용하여 성공적으로 내보낸 세그먼트 데이터에 액세스할 수도 있습니다. UI 또는 RESTful API를 사용하는 [!DNL Query Service]에서는 [!DNL Data Lake] 내의 데이터에 대한 쿼리를 작성하고 유효성을 확인하고 실행할 수 있습니다.

대상 데이터를 쿼리하는 방법에 대한 자세한 내용은 [[!DNL Query Service]](../../query-service/home.md)의 설명서를 참조하십시오.
