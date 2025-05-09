---
keywords: Experience Platform;홈;인기 항목;Adobe Experience Platform;api 안내서;플랫폼 api 안내서;플랫폼 소개;개발자 안내서
solution: Experience Platform
title: Adobe Experience Platform API 시작하기
description: Adobe Experience Platform은 서로 밀접하게 연결된 API 서비스를 제공합니다. 이 안내서에는 사용 가능한 서비스, CRUD 작업에 필요한 헤더, 오류 메시지, Postman 컬렉션 및 샘플 API 호출에 대한 정보가 포함되어 있습니다.
role: Developer
feature: API
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 0%

---

# Adobe Experience Platform API 시작하기

Adobe Experience Platform은 &quot;API 우선&quot; 철학 하에 개발되었습니다. Experience Platform API를 사용하면 계산된 속성 구성, 데이터/엔티티 액세스, 데이터 내보내기, 불필요한 데이터 또는 배치 삭제 등과 같은 데이터에 대한 기본 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 프로그래밍 방식으로 수행할 수 있습니다.

각 Experience Platform 서비스의 API는 모두 동일한 인증 헤더 세트를 공유하며 CRUD 작업에 유사한 구문을 사용합니다. 다음 안내서에서는 Experience Platform API를 시작하는 데 필요한 단계에 대해 간략히 설명합니다.

## 인증 및 헤더

Experience Platform 끝점을 성공적으로 호출하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 Experience Platform API 호출에서 필요한 각 헤더에 대한 값이 제공됩니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### 샌드박스 헤더

Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. Experience Platform API에 대한 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: {SANDBOX_NAME}`

Experience Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../sandboxes/home.md)를 참조하십시오.

### Content-type 헤더

요청 본문(POST, PUT 및 PATCH 호출 등)에 페이로드가 있는 모든 요청에는 `Content-Type` 헤더가 포함되어야 합니다. 허용되는 값은 각 API 엔드포인트에 따라 다릅니다. 끝점에 특정 `Content-Type` 값이 필요한 경우 해당 값이 개별 Experience Platform 서비스에 대해 [API 안내서](#api-guides)에서 제공하는 예제 API 요청에 표시됩니다.

## Experience Platform API 기본 사항

Adobe Experience Platform API는 Experience Platform 리소스를 효과적으로 관리하기 위해 이해해야 하는 몇 가지 기본 기술 및 구문을 사용합니다.

예제 JSON 스키마 개체를 포함하여 Experience Platform에서 사용하는 기본 API 기술에 대한 자세한 내용은 [Experience Platform API 기본 사항](api-fundamentals.md) 안내서를 참조하십시오.

## Experience Platform API용 Postman 컬렉션

Postman은 사전 설정된 변수로 환경을 설정하고, API 컬렉션을 공유하고, CRUD 요청을 간소화하는 등 다양한 작업을 수행할 수 있는 API 개발을 위한 협업 플랫폼입니다. 대부분의 Experience Platform API 서비스에는 API 호출을 지원하는 데 사용할 수 있는 Postman 컬렉션이 있습니다.

환경 설정 방법, 사용 가능한 컬렉션 목록, 컬렉션을 가져오는 방법 등 Postman에 대해 자세히 알아보려면 [Experience Platform Postman 설명서](postman.md)를 참조하세요.

## 샘플 API 호출 읽기 {#sample-api}

요청 형식은 사용 중인 Experience Platform API에 따라 다릅니다. API 호출을 구성하는 방법을 알아보는 가장 좋은 방법은 사용 중인 특정 Experience Platform 서비스에 대한 설명서에 제공된 예제를 따르는 것입니다.

[!DNL Experience Platform]에 대한 설명서는 두 가지 다른 방법으로 API 호출 예를 보여 줍니다. 먼저 호출이 **API 형식**&#x200B;으로 표시되며, 템플릿 표현은 작업(GET, POST, PUT, PATCH, DELETE)과 사용 중인 끝점(예: `/global/classes`)만 표시합니다. 일부 템플릿은 `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`과 같이 호출이 형식화되어야 하는 방법을 보여 주는 변수의 위치도 보여 줍니다.

그런 다음 호출은 **Request**&#x200B;에서 cURL 명령으로 표시되며, 여기에는 API와 성공적으로 상호 작용하는 데 필요한 헤더와 전체 &quot;기본 경로&quot;가 포함됩니다. 기본 경로는 모든 끝점에 미리 첨부되어야 합니다. 예를 들어, 앞서 언급한 `/global/classes` 끝점은 `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`이(가) 됩니다. 설명서 전체에서 API 형식/요청 패턴이 표시되며, Experience Platform API를 직접 호출할 때 예제 요청에 표시된 전체 경로를 사용해야 합니다.

### API 요청 예

다음은 설명서에서 보게 되는 형식을 보여 주는 예제 API 요청입니다.

**API 형식**

API 형식은 작업(GET)과 사용 중인 끝점을 보여 줍니다. 변수는 중괄호(`{CONTAINER_ID}`)로 표시됩니다.

```http
GET /{CONTAINER_ID}/classes
```

**요청**

이 예제 요청에서는 API 형식의 변수에 요청 경로에 실제 값이 제공됩니다. 또한 모든 필수 헤더는 샘플 헤더 값 또는 중요한 정보(예: 보안 토큰 및 액세스 ID)가 포함되어야 하는 변수로 표시됩니다.

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

응답은 전송된 요청을 기반으로 API에 대한 성공적인 호출 이후 예상되는 수신 여부를 보여 줍니다. 경우에 따라 응답이 공백으로 잘려서 샘플에 표시되는 추가 정보나 추가 정보를 볼 수 있습니다.

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

[Experience Platform 문제 해결 안내서](troubleshooting.md#errors-and-troubleshooting)에서는 Experience Platform 서비스를 사용할 때 발생할 수 있는 오류 목록을 제공합니다.

개별 Experience Platform 서비스에 대한 문제 해결 안내서는 [서비스 문제 해결 디렉터리](troubleshooting.md#service-troubleshooting-directory)를 참조하십시오.

필요한 헤더 및 요청 본문을 포함하여 Experience Platform API의 특정 끝점에 대한 자세한 내용은 [Experience Platform API 안내서](#api-guides)를 참조하십시오.

## Experience Platform API 안내서 {#api-guides}

| API 안내서 | 설명 |
| --- | --- |
| [[!DNL Access Control] API 안내서](.././access-control/api/getting-started.md) | [!DNL Access Control] API 끝점은 지정된 샌드박스 내의 지정된 리소스에 대해 사용자에 대해 유효한 현재 정책을 검색할 수 있습니다. 다른 모든 액세스 제어 기능은 [Adobe Admin Console](https://adminconsole.adobe.com/)을 통해 제공됩니다. |
| [일괄 처리 수집 API 안내서](.././ingestion/batch-ingestion/api-overview.md) | Adobe Experience Platform [!DNL Data Ingestion] API를 사용하면 데이터를 Experience Platform에 배치 파일로 수집할 수 있습니다. 수집되는 데이터는 CRM 시스템의 플랫 파일(예: Parquet 파일)의 프로필 데이터이거나 스키마 레지스트리(XDM)의 알려진 스키마를 준수하는 데이터일 수 있습니다. |
| [[!DNL Catalog Service] API 안내서](.././catalog/api/getting-started.md) | [!DNL Catalog Service] API를 통해 개발자는 Adobe Experience Platform에서 데이터 세트 메타데이터를 관리할 수 있습니다. 여기에는 데이터 위치, 처리 단계, 처리 중 발생한 오류 및 데이터 보고서가 포함됩니다. |
| [[!DNL Data Access] API 안내서](.././data-access/api.md) | [!DNL Data Access] API를 통해 개발자는 Experience Platform 내에서 수집된 데이터 세트에 대한 정보를 검색할 수 있습니다. 여기에는 데이터 세트 파일 액세스 및 다운로드, 헤더 정보 검색, 실패 및 성공한 배치 나열, 미리보기 CSV/Parquet 파일 다운로드 등이 포함됩니다. |
| [[!DNL Dataset Service] API 안내서](.././data-governance/labels/dataset-api.md) | 데이터 세트 서비스 API를 사용하면 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 카탈로그 서비스 API와 별개입니다. |
| [[!DNL Data Hygiene API guide]](../hygiene/api/overview.md) | [!DNL Data Hygiene] API를 사용하면 Adobe Experience Platform에서 고객의 저장된 개인 데이터를 프로그래밍 방식으로 수정하거나 삭제할 수 있으며 데이터 세트의 만료 날짜를 예약할 수 있습니다. |
| [[!DNL Edge Network] API 안내서](https://developer.adobe.com/data-collection-apis/docs/getting-started/) | [!DNL Edge Network API]은(는) 다양한 데이터 수집, 개인화, 광고 및 마케팅 사용 사례에 사용할 수 있습니다. [!DNL Edge Network API]은(는) 서버, 장치 [!DNL IoT]개, 셋톱 박스 및 다양한 다른 장치에서 사용할 수 있습니다. |
| [[!DNL Identity Service] API 안내서](.././identity-service/api/getting-started.md) | [!DNL Identity Service] API를 통해 개발자는 Adobe Experience Platform의 ID 그래프를 사용하여 크로스 디바이스, 크로스 채널 및 거의 실시간으로 고객을 식별할 수 있습니다. |
| [[!DNL MTLS Service API guide]](../data-governance/mtls-api/overview.md) | [!DNL MTLS Service] API를 사용하면 조직의 Adobe에서 발급한 공개 인증서를 안전하게 검색할 수 있습니다. |
| [[!DNL Observability Insights] API 안내서](.././observability/api/overview.md) | [!DNL Observability Insights]은(는) 개발자가 Adobe Experience Platform의 주요 가시성 지표를 표시할 수 있도록 하는 RESTful API입니다. 이러한 지표는 Experience Platform 사용 통계, Experience Platform 서비스에 대한 상태 점검, 내역 트렌드 및 다양한 Experience Platform 기능에 대한 성능 지표에 대한 통찰력을 제공합니다. |
| [[!DNL Policy Service] API 안내서](.././data-governance/api/overview.md) <br>(데이터 거버넌스) | [!DNL Policy Service] API를 사용하면 데이터 사용 레이블 및 정책을 만들고 관리하여 특정 데이터 사용 레이블이 포함된 데이터에 대해 취할 수 있는 마케팅 작업을 결정할 수 있습니다. 데이터 세트 및 필드에 레이블을 적용하려면 [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) 안내서를 참조하세요. |
| [[!DNL Privacy Service] API 안내서](.././privacy-service/api/getting-started.md) | [!DNL Privacy Service] API를 통해 개발자는 법적 개인 정보 보호 규정을 준수하여 Experience Cloud 애플리케이션에서 개인 데이터에 액세스하거나 삭제하기 위한 고객 요청을 만들고 관리할 수 있습니다. |
| [[!DNL Query Service] API 안내서](.././query-service/api/getting-started.md) | [!DNL Query Service] API를 통해 개발자는 표준 SQL을 사용하여 Adobe Experience Platform 데이터를 쿼리할 수 있습니다. |
| [[!DNL Real-Time Customer Profile] API 안내서](.././profile/api/overview.md) | 실시간 고객 프로필 API를 사용하면 개발자가 프로필 보기, 병합 정책 만들기 및 업데이트, 프로필 데이터 내보내기 및 샘플링, 더 이상 필요하지 않거나 오류로 추가된 프로필 데이터 삭제 등을 포함하여 프로필 데이터를 탐색하고 작업할 수 있습니다. |
| [샌드박스 API 안내서](.././sandboxes/api/getting-started.md) | 개발자는 샌드박스 API를 통해 Adobe Experience Platform에서 격리된 가상 샌드박스 환경을 프로그래밍 방식으로 관리할 수 있습니다. |
| [[!DNL Schema Registry] API 안내서](.././xdm/api/overview.md) <br>(XDM) | [!DNL Schema Registry] API를 통해 개발자는 Adobe Experience Platform 내의 모든 스키마 및 관련 XDM(Experience Data Model) 리소스를 프로그래밍 방식으로 관리할 수 있습니다. |
| [[!DNL Segmentation Service] API 안내서](.././segmentation/api/overview.md) | [!DNL Segmentation Service] API를 통해 개발자는 Adobe Experience Platform에서 세그멘테이션 작업을 프로그래밍 방식으로 관리할 수 있습니다. 여기에는 세그먼트를 작성하고 실시간 고객 프로필 데이터에서 대상을 생성하는 작업이 포함됩니다. |
| [[!DNL Sensei Machine Learning] API 안내서](.././data-science-workspace/api/getting-started.md) <br>(Data Science Workspace) | [!DNL Sensei Machine Learning] API는 데이터 과학자가 알고리즘 온보딩, 실험 및 서비스 배포에서 머신 러닝(ML) 서비스를 구성하고 관리할 수 있는 메커니즘을 제공합니다. |

각 서비스에 사용할 수 있는 특정 끝점 및 작업에 대한 자세한 내용은 Adobe I/O의 [API 참조 설명서](https://www.adobe.com/go/platform-api-reference-en)를 참조하세요.

## 다음 단계

이 문서에서는 필수 헤더와 사용 가능한 안내서를 소개하고 예제 API 호출을 제공했습니다. 이제 Adobe Experience Platform에서 API를 호출하는 데 필요한 헤더 값이 있으므로 [Experience Platform API 안내서 테이블](#api-guides)에서 탐색할 API 끝점을 선택하십시오.

FAQ에 대한 답변은 [Experience Platform 문제 해결 안내서](troubleshooting.md)를 참조하십시오.

Postman 환경을 설정하고 사용 가능한 Postman 컬렉션을 살펴보려면 [Experience Platform Postman 안내서](postman.md)를 참조하세요.
