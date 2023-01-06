---
keywords: Experience Platform;홈;인기 항목;카탈로그 서비스;카탈로그;카탈로그 서비스;카탈로그
solution: Experience Platform
title: 카탈로그 서비스 API 안내서
description: 개발자가 Catalog Service API를 사용하여 Adobe Experience Platform에서 데이터 세트 메타데이터를 관리할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 3%

---

# [!DNL Catalog Service] API 안내서

[!DNL Catalog Service] 는 Adobe Experience Platform 내의 데이터 위치 및 계열에 대한 레코드 시스템입니다. [!DNL Catalog] 는 내에서 데이터에 대한 정보를 찾을 수 있는 메타데이터 저장소 또는 &quot;카탈로그&quot;로 작동합니다 [!DNL Experience Platform]로 설정되어야 합니다. 자세한 내용은 [[!DNL Catalog] 개요](../home.md) 추가 정보.

이 개발자 가이드는 를 사용하는 데 도움이 되는 단계를 제공합니다. [!DNL Catalog] API. 그러면 가이드는 를 사용하여 주요 작업을 수행하기 위한 샘플 API 호출을 제공합니다. [!DNL Catalog].

## 전제 조건

[!DNL Catalog] 에서는 여러 종류의 리소스 및 작업에 대한 메타데이터를 추적합니다 [!DNL Experience Platform]. 이 개발자 안내서를 사용하려면 다양한 [!DNL Experience Platform] 이러한 리소스 생성 및 관리와 관련된 서비스

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.
* [일괄 수집](../../ingestion/batch-ingestion/overview.md): 방법 [!DNL Experience Platform] csv 및 Parquet과 같은 데이터 파일의 데이터를 수집 및 저장합니다.
* [스트리밍 수집](../../ingestion/streaming-ingestion/overview.md): 방법 [!DNL Experience Platform] 클라이언트 및 서버측 장치에서 데이터를 실시간으로 수집 및 저장합니다.

다음 섹션에서는 를 성공적으로 호출하기 위해 알고 있거나 현재 상태여야 하는 추가 정보를 제공합니다 [!DNL Catalog Service] API.

## 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

## 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형: application/json

## 우수 사례 [!DNL Catalog] API 호출

에 대한 GET 요청을 수행할 때 [!DNL Catalog] API에서 가장 좋은 방법은 필요한 개체 및 속성만 반환하기 위해 요청에 쿼리 매개 변수를 포함하는 것입니다. 필터링되지 않은 요청은 응답 페이로드가 과거 3GB에 도달하도록 하여 전반적인 성능이 저하될 수 있습니다.

요청 경로에 해당 ID를 포함하여 특정 개체를 보거나 다음과 같은 쿼리 매개 변수를 사용할 수 있습니다 `properties` 및 `limit` 응답을 필터링합니다. 필터는 쿼리 매개 변수로 전달되고 헤더와 쿼리 매개 변수로 전달될 수 있습니다. 다음 문서를 참조하십시오. [카탈로그 데이터 필터링](filter-data.md) 추가 정보.

일부 쿼리는 API를 많이 로드할 수 있으므로 전역 한계는 [!DNL Catalog] 모범 사례를 더 지원하기 위한 쿼리입니다.

## 다음 단계

이 문서는 [!DNL Catalog] API. 이제 이 개발자 가이드에 제공된 샘플 호출을 진행하여 지침을 따라 수행할 수 있습니다.

이 안내서의 대부분의 예제는 `/dataSets` 엔드포인트. 하지만 원칙은 내의 다른 엔드포인트에 적용할 수 있습니다 [!DNL Catalog] (예: `/batches` 및 `/accounts`). 자세한 내용은 [카탈로그 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/catalog/) 를 참조하십시오.

을 수행하는 방법을 보여주는 단계별 워크플로우입니다. [!DNL Catalog] API는 데이터 수집과 관련되어 있습니다. [데이터 집합 만들기](../datasets/create.md).
