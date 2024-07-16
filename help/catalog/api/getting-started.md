---
keywords: Experience Platform;홈;인기 항목;카탈로그 서비스;카탈로그;카탈로그 서비스;카탈로그
solution: Experience Platform
title: 카탈로그 서비스 API 안내서
description: 개발자는 카탈로그 서비스 API를 통해 Adobe Experience Platform에서 데이터 세트 메타데이터를 관리할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 07451b8ab4bcb7ca43ad0c8a821478b2c9682894
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 22%

---

# [!DNL Catalog Service] API 안내서

[!DNL Catalog Service]은(는) Adobe Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다. [!DNL Catalog]은(는) 데이터 자체에 액세스할 필요 없이 [!DNL Experience Platform] 내에서 데이터에 대한 정보를 찾을 수 있는 메타데이터 저장소 또는 &quot;카탈로그&quot; 역할을 합니다. 자세한 내용은 [[!DNL Catalog] 개요](../home.md)를 참조하세요.

이 개발자 안내서에서는 [!DNL Catalog] API 사용을 시작하는 데 도움이 되는 단계를 제공합니다. 그런 다음 가이드는 [!DNL Catalog]을(를) 사용하여 키 작업을 수행하기 위한 샘플 API 호출을 제공합니다.

## 전제 조건

[!DNL Catalog]은(는) [!DNL Experience Platform] 내의 여러 종류의 리소스 및 작업에 대한 메타데이터를 추적합니다. 이 개발자 안내서를 사용하려면 이러한 리소스를 만들고 관리하는 데 관련된 다양한 [!DNL Experience Platform] 서비스에 대한 작업 이해가 필요합니다.

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): [!DNL Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [일괄 처리 수집](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform]에서 CSV 및 Parquet와 같은 데이터 파일에서 데이터를 수집하고 저장하는 방법입니다.
* [스트리밍 수집](../../ingestion/streaming-ingestion/overview.md): [!DNL Experience Platform]이(가) 클라이언트 및 서버측 장치에서 실시간으로 데이터를 수집 및 저장하는 방법입니다.

다음 단원에서는 [!DNL Catalog Service] API를 성공적으로 호출하기 위해 알고 있어야 하거나 현재 보유하고 있어야 하는 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

## 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api 키: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* Content-Type: application/json

## [!DNL Catalog] API 호출에 대한 모범 사례

[!DNL Catalog] API에 대한 GET 요청을 수행할 때 가장 좋은 방법은 필요한 개체 및 속성만 반환하도록 요청에 쿼리 매개 변수를 포함하는 것입니다. 필터링되지 않은 요청으로 인해 응답 페이로드가 3GB를 초과할 수 있으므로 전체 성능이 저하될 수 있습니다.

요청 경로에 해당 ID를 포함하여 특정 개체를 보거나 `properties` 및 `limit` 같은 쿼리 매개 변수를 사용하여 응답을 필터링할 수 있습니다. 필터는 헤더와 쿼리 매개 변수로 전달할 수 있으며, 쿼리 매개 변수로 전달된 필터가 우선합니다. 자세한 내용은 [카탈로그 데이터 필터링](filter-data.md)에 대한 문서를 참조하십시오.

일부 쿼리는 API에 많은 부하를 줄 수 있으므로 모범 사례를 추가로 지원하기 위해 [!DNL Catalog] 쿼리에 전역 제한이 구현되었습니다.

## 다음 단계

이 문서에서는 [!DNL Catalog] API를 호출하는 데 필요한 사전 지식을 다뤘습니다. 이제 이 개발자 안내서에 제공된 샘플 호출로 진행하여 지침을 따를 수 있습니다.

이 안내서의 예제는 대부분 `/dataSets` 끝점을 사용하지만 [!DNL Catalog] 내의 다른 끝점(예: `/batches`)에 이 원리를 적용할 수 있습니다. 각 끝점에 사용할 수 있는 모든 호출 및 작업의 전체 목록은 [카탈로그 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/catalog/)를 참조하십시오.

[!DNL Catalog] API가 데이터 수집과 어떻게 관련되어 있는지 보여 주는 단계별 워크플로에 대해서는 [데이터 집합 만들기](../datasets/create.md)에 대한 자습서를 참조하십시오.
