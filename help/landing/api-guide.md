---
keywords: Experience Platform;홈;인기 항목;Adobe Experience Platform;api 안내서;플랫폼 api 안내서;플랫폼 소개;개발자 안내서
solution: Experience Platform
title: Adobe Experience Platform API 시작하기
topic-legacy: api guide
description: Adobe Experience Platform은 서로 밀접하게 연결된 API 서비스를 제공합니다. 이 안내서에는 사용 가능한 서비스, CRUD 작업에 필요한 헤더, 오류 메시지, Postman 컬렉션 및 샘플 API 호출에 대한 정보가 포함되어 있습니다.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Adobe Experience Platform API 시작하기

Adobe Experience Platform은 &quot;API 우선&quot; 철학으로 개발되었습니다. 플랫폼 API를 사용하면 계산된 속성 구성, 데이터/엔티티 액세스, 데이터 내보내기, 불필요한 데이터 또는 배치 삭제 등과 같은 데이터에 대해 기본 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 프로그래밍 방식으로 수행할 수 있습니다.

각 Experience Platform 서비스의 API는 모두 동일한 일련의 인증 헤더를 공유하고 CRUD 작업에 대해 유사한 구문을 사용합니다. 다음 안내서에서는 플랫폼 API를 시작하는 데 필요한 단계를 간략하게 설명합니다.

## 인증 및 헤더

플랫폼 종단점을 성공적으로 호출하려면 다음을 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 아래와 같이 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### 샌드박스 헤더

Experience Platform의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. Platform API에 대한 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: {SANDBOX_NAME}`

Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../sandboxes/home.md).

### 컨텐츠 유형 헤더

요청 본문에 페이로드가 있는 모든 요청(예: POST, PUT 및 PATCH 호출)에는 `Content-Type` 헤더. 허용되는 값은 각 API 엔드포인트에 해당됩니다. 특정 `Content-Type` 엔드포인트에 필요한 값은 가 제공하는 API 요청 예에 표시됩니다 [개별 플랫폼 서비스를 위한 API 안내서](#api-guides).

## Experience Platform API 기본 사항

Adobe Experience Platform API는 플랫폼 리소스를 효과적으로 관리하기 위해 알고 있어야 하는 중요한 몇 가지 기본 기술 및 구문을 사용합니다.

예제 JSON 스키마 개체를 포함하여 Platform에서 사용하는 기본 API 기술에 대한 자세한 내용은 [Experience Platform API 기본 사항](api-fundamentals.md) 안내서.

## Experience Platform API에 대한 Postman 컬렉션

Postman은 사전 설정된 변수로 환경을 설정하고, API 컬렉션을 공유하고, CRUD 요청을 간소화하는 등의 작업을 수행할 수 있는 API 개발을 위한 협업 플랫폼입니다. 대부분의 Platform API 서비스에는 API 호출을 수행하는 데 도움이 되는 Postman 컬렉션이 있습니다.

환경 설정 방법, 사용 가능한 컬렉션 목록, 컬렉션 가져오기 방법 등 Postman에 대한 자세한 내용을 보려면 [Platform Postman 설명서](postman.md).

## 샘플 API 호출 읽기 {#sample-api}

요청 형식은 사용되는 플랫폼 API에 따라 다릅니다. API 호출을 구성하는 방법을 학습하는 가장 좋은 방법은 사용 중인 특정 플랫폼 서비스에 대한 설명서에 제공된 예제를 함께 따르는 것입니다.

용 설명서 [!DNL Experience Platform] 는 두 가지 다른 방법으로 API 호출 예를 보여줍니다. 먼저 호출이 **API 형식**, 사용 중인 작업(예: GET, POST, PUT, PATCH, DELETE)과 엔드포인트를 보여주는 템플릿 표현 `/global/classes`). 일부 템플릿은 처럼 호출을 작성하는 방법을 보여주는 데 도움이 되는 변수의 위치를 보여줍니다 `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

그러면 호출이 **요청**: API와 성공적으로 상호 작용하는 데 필요한 헤더와 전체 &quot;기본 경로&quot;가 포함됩니다. 기본 경로는 모든 끝점에 미리 삽입해야 합니다. 예를 들어, 앞서 언급한 `/global/classes` 엔드포인트가 다음과 같이 됩니다. `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. 설명서 전체에서 API 형식/요청 패턴이 표시되며, Platform API를 직접 호출할 때 예제 요청에 표시된 전체 경로를 사용해야 합니다.

### API 요청 예

다음은 설명서에서 발생할 형식을 보여주는 API 요청 예입니다.

**API 형식**

API 형식은 사용 중인 작업(GET) 및 엔드포인트를 보여줍니다. 변수는 중괄호로 표시됩니다(이 경우 `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**요청**

이 요청 예제에서 API 형식의 변수에는 요청 경로의 실제 값이 지정됩니다. 또한 모든 필수 헤더는 중요한 정보(예: 보안 토큰 및 액세스 ID)가 포함된 샘플 헤더 값 또는 변수로 표시됩니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 전송된 요청을 기반으로 API에 대한 성공적인 호출 후 수신 예정 내용이 표시됩니다. 경우에 따라 응답이 공간에 대해 잘리며, 이는 샘플에 표시되는 추가 정보나 추가 정보를 볼 수 있음을 의미합니다.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## 오류 메시지

다음 [플랫폼 문제 해결 안내서](troubleshooting.md#errors-and-troubleshooting) 는 Experience Platform 서비스를 사용할 때 발생할 수 있는 오류 목록을 제공합니다.

개별 플랫폼 서비스에 대한 문제 해결 안내서는 [서비스 문제 해결 디렉터리](troubleshooting.md#service-troubleshooting-directory).

필수 헤더 및 요청 본문을 포함하여 Platform API의 특정 종단점에 대한 자세한 내용은 [플랫폼 API 안내서](#api-guides).

## 플랫폼 API 안내서 {#api-guides}

| API 안내서 | 설명 |
| --- | --- |
| [[!DNL Access Control] API 안내서](.././access-control/api/getting-started.md) | 다음 [!DNL Access Control] API 엔드포인트는 지정된 샌드박스 내에 지정된 리소스에 대해 사용자에 대해 적용되는 현재 정책을 검색할 수 있습니다. 기타 모든 액세스 제어 기능은 [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [일괄 수집 API 안내서](.././ingestion/batch-ingestion/api-overview.md) | Adobe Experience Platform [!DNL Data Ingestion] API를 사용하면 데이터를 배치 파일로 플랫폼에 수집할 수 있습니다. 수집되는 데이터는 CRM 시스템의 플랫 파일(예: Parquet 파일)의 프로필 데이터 또는 XDM(Schema Registry)의 알려진 스키마를 따르는 데이터일 수 있습니다. |
| [[!DNL Catalog Service] API 안내서](.././catalog/api/getting-started.md) | 다음 [!DNL Catalog Service] API를 사용하여 개발자는 Adobe Experience Platform에서 데이터 세트 메타데이터를 관리할 수 있습니다. 여기에는 데이터 위치, 처리 단계, 처리 중에 발생한 오류 및 데이터 보고서가 포함됩니다. |
| [[!DNL Data Access] API 안내서](.././data-access/api.md) | 다음 [!DNL Data Access] API를 사용하여 개발자는 Experience Platform 내에서 수집된 데이터 세트에 대한 정보를 검색할 수 있습니다. 데이터 세트 파일에 액세스 및 다운로드, 헤더 정보 검색, 실패 및 성공 배치 나열, 미리 보기 CSV/Parquet 파일 다운로드가 포함됩니다. |
| [[!DNL Dataset Service] API 안내서](.././data-governance/labels/dataset-api.md) | 데이터 세트 서비스 API를 사용하면 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 카탈로그 서비스 API와는 별개입니다. |
| [[!DNL Identity Service] API 안내서](.././identity-service/api/getting-started.md) | 다음 [!DNL Identity Service] API를 사용하여 개발자는 Adobe Experience Platform에서 ID 그래프를 사용하여 교차 장치, 교차 채널 및 거의 실시간 고객 ID를 관리할 수 있습니다. |
| [[!DNL Observability Insights] API 안내서](.././observability/api/overview.md) | [!DNL Observability Insights] 는 개발자가 Adobe Experience Platform에서 주요 가시성 지표를 노출할 수 있는 RESTful API입니다. 이러한 지표는 플랫폼 사용 통계, 플랫폼 서비스에 대한 상태 점검, 기록 동향 및 다양한 플랫폼 기능에 대한 성능 지표에 대한 통찰력을 제공합니다. |
| [[!DNL Policy Service] API 안내서](.././data-governance/api/overview.md) <br> (데이터 거버넌스) | 다음 [!DNL Policy Service] API를 사용하면 데이터 사용 레이블 및 정책을 만들고 관리하여 특정 데이터 사용 레이블을 포함하는 데이터에 대해 수행할 수 있는 마케팅 작업을 결정할 수 있습니다. 데이터 세트 및 필드에 레이블을 적용하려면 [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) 안내서 |
| [[!DNL Privacy Service] API 안내서](.././privacy-service/api/getting-started.md) | 다음 [!DNL Privacy Service] API를 사용하여 개발자는 법적 개인 정보 보호 규정을 준수하여 Experience Cloud 애플리케이션에서 개인 데이터에 액세스하거나 삭제하기 위한 고객 요청을 만들고 관리할 수 있습니다. |
| [[!DNL Query Service] API 안내서](.././query-service/api/getting-started.md) | 다음 [!DNL Query Service] API를 사용하여 개발자가 표준 SQL을 사용하여 Adobe Experience Platform 데이터를 쿼리할 수 있습니다. |
| [[!DNL Real-Time Customer Profile] API 안내서](.././profile/api/overview.md) | 개발자는 실시간 고객 프로필 API를 사용하여 프로필 보기, 병합 정책 만들기 및 업데이트, 프로필 데이터 내보내기 또는 샘플링, 더 이상 필요하지 않거나 오류가 추가된 프로필 데이터 삭제 등 프로필 데이터를 탐색 및 작업할 수 있습니다. |
| [샌드박스 API 안내서](.././sandboxes/api/getting-started.md) | Sandbox API를 사용하여 개발자는 Adobe Experience Platform에서 분리된 가상 샌드박스 환경을 프로그래밍 방식으로 관리할 수 있습니다. |
| [[!DNL Schema Registry] API 안내서](.././xdm/api/overview.md) <br> (XDM) | 다음 [!DNL Schema Registry] API를 사용하여 개발자는 Adobe Experience Platform 내의 모든 스키마 및 관련 XDM(Experience Data Model) 리소스를 프로그래밍 방식으로 관리할 수 있습니다. |
| [[!DNL Segmentation Service] API 안내서](.././segmentation/api/overview.md) | 다음 [!DNL Segmentation Service] API를 사용하여 개발자가 Adobe Experience Platform에서 세그멘테이션 작업을 프로그래밍 방식으로 관리할 수 있습니다. 여기에는 세그먼트 작성 및 실시간 고객 프로필 데이터에서 대상 생성 등이 포함됩니다. |
| [[!DNL Sensei Machine Learning] API 안내서](.././data-science-workspace/api/getting-started.md) <br> (데이터 과학 작업 공간) | 다음 [!DNL Sensei Machine Learning] API는 데이터 과학자들이 알고리즘 온보딩, 실험 및 서비스 배포에서 ML(기계 학습) 서비스를 구성하고 관리할 수 있는 메커니즘을 제공합니다. |

각 서비스에 사용할 수 있는 특정 종단점 및 작업에 대한 자세한 내용은 [API 참조 설명서](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O에서 확인하십시오.

## 다음 단계

이 문서에서는 필요한 헤더, 사용 가능한 안내서를 도입하고 API 호출 예를 제공했습니다. 이제 Adobe Experience Platform에서 API를 호출하는 데 필요한 필수 헤더 값이 있으므로 [플랫폼 API 안내서 표](#api-guides).

자주 묻는 질문에 대한 답변은 [플랫폼 문제 해결 안내서](troubleshooting.md).

Postman 환경을 설정하고 사용 가능한 Postman 컬렉션을 탐색하려면 다음을 참조하십시오. [Platform Postman 안내서](postman.md).
