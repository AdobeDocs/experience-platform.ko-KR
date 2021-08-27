---
keywords: Experience Platform;홈;인기 항목;카탈로그 서비스;카탈로그;카탈로그 서비스;카탈로그
solution: Experience Platform
title: 카탈로그 서비스 API 안내서
topic-legacy: developer guide
description: 개발자가 Catalog Service API를 사용하여 Adobe Experience Platform에서 데이터 세트 메타데이터를 관리할 수 있습니다. API를 사용하여 주요 작업을 수행하는 방법을 알아보려면 이 안내서를 따르십시오.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# [!DNL Catalog Service] API 안내서

[!DNL Catalog Service] 는 Adobe Experience Platform 내의 데이터 위치 및 계열에 대한 레코드 시스템입니다. [!DNL Catalog] 는 데이터 자체에 액세스할 필요 없이 내에서 데이터에 대한 정보를 찾을 수  [!DNL Experience Platform]있는 메타데이터 저장소 또는 &quot;카탈로그&quot; 역할을 합니다. 자세한 내용은 [[!DNL Catalog] 개요](../home.md)를 참조하십시오.

이 개발자 가이드는 [!DNL Catalog] API 사용을 시작하는 데 도움이 되는 단계를 제공합니다. 그러면 안내서에서는 [!DNL Catalog]을 사용하여 키 작업을 수행하기 위한 샘플 API 호출을 제공합니다.

## 전제 조건

[!DNL Catalog] 에서는 여러 종류의 리소스 및 작업에 대한 메타데이터를  [!DNL Experience Platform]추적합니다. 이 개발자 안내서를 사용하려면 다음 리소스를 만들고 관리하는 데 관련된 다양한 [!DNL Experience Platform] 서비스를 이해할 필요가 있습니다.

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크입니다.
* [일괄 수집](../../ingestion/batch-ingestion/overview.md): CSV  [!DNL Experience Platform] 및 Parquet과 같은 데이터 파일의 데이터를 수집 및 저장하는 방법입니다.
* [스트리밍 수집](../../ingestion/streaming-ingestion/overview.md): 클라이언트  [!DNL Experience Platform] 및 서버측 장치에서 데이터를 실시간으로 수집 및 저장하는 방법입니다.

다음 섹션에서는 [!DNL Catalog Service] API를 성공적으로 호출하기 위해 알고 있거나 현재 상태여야 하는 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서에서 [예제 API 호출](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법 섹션을 참조하십시오.

## 필수 헤더에 대한 값을 수집합니다

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에 필요한 각 헤더에 대한 값을 제공합니다.

* 권한 부여: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형: application/json

## [!DNL Catalog] API 호출에 대한 우수 사례

[!DNL Catalog] API에 대한 GET 요청을 수행할 때 가장 좋은 방법은 필요한 개체 및 속성만 반환하기 위해 요청에 쿼리 매개 변수를 포함하는 것입니다. 필터링되지 않은 요청은 응답 페이로드가 과거 3GB에 도달하도록 하여 전반적인 성능이 저하될 수 있습니다.

요청 경로에 해당 ID를 포함하여 특정 개체를 보거나 `properties` 및 `limit` 등의 쿼리 매개 변수를 사용하여 응답을 필터링할 수 있습니다. 필터는 쿼리 매개 변수로 전달되고 헤더와 쿼리 매개 변수로 전달될 수 있습니다. 자세한 내용은 [카탈로그 데이터 필터링](filter-data.md)에 있는 문서를 참조하십시오.

일부 쿼리는 API에 많은 로드를 줄 수 있으므로 모범 사례를 더 지원하기 위해 [!DNL Catalog] 쿼리에 전역 제한이 구현되었습니다.

## 다음 단계

이 문서는 [!DNL Catalog] API를 호출하는 데 필요한 사전 요구 사항에 대해 다룹니다. 이제 이 개발자 가이드에 제공된 샘플 호출을 진행하여 지침을 따라 수행할 수 있습니다.

이 안내서의 대부분의 예제는 `/dataSets` 종단점을 사용하지만 이 원칙은 [!DNL Catalog](예: `/batches` 및 `/accounts`) 내의 다른 종단점에 적용할 수 있습니다. 각 종단점에 사용할 수 있는 모든 호출 및 작업의 전체 목록은 [카탈로그 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/catalog/)를 참조하십시오.

[!DNL Catalog] API가 데이터 수집과 어떻게 관련되는지를 보여 주는 단계별 워크플로우는 [데이터 집합 만들기](../datasets/create.md)의 자습서를 참조하십시오.
