---
keywords: Experience Platform;홈;인기 항목;카탈로그 서비스;카탈로그;카탈로그 서비스;카탈로그
solution: Experience Platform
title: 카탈로그 서비스 API 안내서
description: 개발자는 카탈로그 서비스 API를 통해 Adobe Experience Platform에서 데이터 세트 메타데이터를 관리할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 07451b8ab4bcb7ca43ad0c8a821478b2c9682894
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 3%

---

# [!DNL Catalog Service] API 안내서

[!DNL Catalog Service] 는 Adobe Experience Platform 내의 데이터 위치와 계보를 위한 기록 시스템입니다. [!DNL Catalog] 는 내에서 데이터에 대한 정보를 찾을 수 있는 메타데이터 저장소 또는 &quot;카탈로그&quot; 역할을 합니다. [!DNL Experience Platform]: 데이터 자체에 액세스할 필요가 없습니다. 다음을 참조하십시오. [[!DNL Catalog] 개요](../home.md) 추가 정보.

이 개발자 안내서에서는 다음을 사용하는 데 도움이 되는 단계를 제공합니다. [!DNL Catalog] API. 안내서에서는 를 사용하여 주요 작업을 수행하기 위한 샘플 API 호출을 제공합니다 [!DNL Catalog].

## 사전 요구 사항

[!DNL Catalog] 내에서 여러 종류의 리소스 및 작업을 위한 메타데이터를 추적합니다. [!DNL Experience Platform]. 이 개발자 안내서를 사용하려면 여러 가지 사항에 대한 작업 이해가 필요합니다 [!DNL Experience Platform] 다음 리소스를 만들고 관리하는 데 관련된 서비스:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.
* [일괄 처리 수집](../../ingestion/batch-ingestion/overview.md): 방법 [!DNL Experience Platform] csv 및 Parquet와 같은 데이터 파일에서 데이터를 수집하고 저장합니다.
* [스트리밍 수집](../../ingestion/streaming-ingestion/overview.md): 방법 [!DNL Experience Platform] 클라이언트 및 서버측 장치에서 실시간으로 데이터를 수집 및 저장합니다.

다음 섹션에서는 를 성공적으로 호출하기 위해 알고 있거나 보유하고 있어야 하는 추가 정보를 제공합니다. [!DNL Catalog Service] API.

## 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

## 필수 헤더에 대한 값 수집

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* Content-Type: application/json

## 에 대한 우수 사례 [!DNL Catalog] API 호출

에 대한 GET 요청을 수행할 때 [!DNL Catalog] API에서 가장 좋은 방법은 필요한 개체와 속성만 반환하기 위해 요청에 쿼리 매개 변수를 포함하는 것입니다. 필터링되지 않은 요청으로 인해 응답 페이로드가 3GB를 초과할 수 있으므로 전체 성능이 저하될 수 있습니다.

요청 경로에 해당 ID를 포함하여 특정 개체를 보거나 와 같은 쿼리 매개 변수를 사용할 수 있습니다. `properties` 및 `limit` 응답을 필터링합니다. 필터는 헤더와 쿼리 매개 변수로 전달할 수 있으며, 쿼리 매개 변수로 전달된 필터가 우선합니다. 다음에 대한 문서 보기: [카탈로그 데이터 필터링](filter-data.md) 추가 정보.

일부 쿼리는 API에 많은 부하를 줄 수 있으므로 전역 제한은에 구현되었습니다. [!DNL Catalog] 모범 사례를 추가로 지원하는 쿼리

## 다음 단계

이 문서에서는 [!DNL Catalog] API. 이제 이 개발자 안내서에 제공된 샘플 호출로 진행하여 지침을 따를 수 있습니다.

이 안내서의 대부분의 예제에서는 `/dataSets` 끝점이지만 원리는 내의 다른 끝점에 적용할 수 있습니다. [!DNL Catalog] (예: `/batches`). 다음을 참조하십시오. [카탈로그 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/catalog/) 각 끝점에 사용할 수 있는 모든 호출 및 작업의 전체 목록입니다.

을 보여 주는 단계별 워크플로 [!DNL Catalog] API는 데이터 수집과 관련되어 있습니다. [데이터 세트 만들기](../datasets/create.md).
