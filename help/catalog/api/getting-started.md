---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 카탈로그 서비스 개발자 가이드
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# 카탈로그 서비스 개발자 가이드

Catalog Service는 Adobe Experience Platform의 데이터 위치 및 계열에 대한 기록 시스템입니다. 카탈로그는 데이터 자체에 액세스할 필요 없이 경험 플랫폼 내에서 데이터에 대한 정보를 찾을 수 있는 메타데이터 저장소 또는 &quot;카탈로그&quot;로 작동합니다. 자세한 내용은 [카탈로그 개요를](../home.md) 참조하십시오.

이 개발자 안내서에서는 카탈로그 API 사용을 시작하는 데 도움이 되는 단계를 제공합니다. 그런 다음 가이드는 카탈로그를 사용하여 키 작업을 수행하기 위한 샘플 API 호출을 제공합니다.

## 전제 조건

Catalog는 Experience Platform에서 다양한 종류의 리소스 및 작업에 대한 메타데이터를 추적합니다. 이 개발자 가이드는 이러한 리소스를 만들고 관리하는 것과 관련된 다양한 Experience Platform 서비스에 대한 실무적인 이해가 필요합니다.

* [XDM(Experience Data Model)](../../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [일괄 처리](../../ingestion/batch-ingestion/overview.md):Experience Platform이 CSV 및 Partiquet과 같은 데이터 파일의 데이터를 인제스트 및 저장하는 방법입니다.
* [스트리밍 통합](../../ingestion/streaming-ingestion/overview.md):Adobe Experience Platform을 통해 클라이언트 및 서버측 디바이스에서 실시간으로 데이터를 인제스트 및 저장하는 방법

다음 섹션에서는 Catalog Service API를 성공적으로 호출하기 위해 알아야 하거나 현재 보유하고 있는 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

## 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

* 인증:베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형:application/json

## 카탈로그 API 호출에 대한 우수 사례

카탈로그 API에 대한 GET 요청을 수행할 때 필요한 개체 및 속성만 반환하려면 요청에 쿼리 매개 변수를 포함하는 것이 좋습니다. 필터링되지 않은 요청은 응답 페이로드가 3GB가 지난 크기에 도달하면 전반적인 성능이 저하될 수 있습니다.

요청 경로에 ID를 포함하거나 쿼리 매개 변수(예: `properties` 및 응답 필터링)를 사용하여 특정 개체를 볼 `limit` 수 있습니다. 필터는 쿼리 매개 변수로 전달된 필터가 우선하므로 헤더와 쿼리 매개 변수로 전달할 수 있습니다. 자세한 내용은 카탈로그 데이터 [필터링에](filter-data.md) 대한 문서를 참조하십시오.

일부 쿼리는 API에 많은 로드를 가져올 수 있으므로 우수 사례를 더 지원하기 위해 카탈로그 쿼리에 글로벌 제한이 구현되었습니다.

## 다음 단계

이 문서에서는 카탈로그 API를 호출하는 데 필요한 사전 요구 사항에 대해 설명합니다. 이제 이 개발자 안내서에서 제공하는 샘플 호출을 진행하여 지침을 따라 수행할 수 있습니다.

이 안내서의 대부분의 예제는 `/dataSets` 끝점을 사용하지만, 이러한 원칙은 카탈로그 내의 다른 끝점에 적용할 수 있습니다(예: `/batches` 및 `/accounts`). 각 [끝점에 대해 사용 가능한 모든 호출 및 작업의 전체 목록은 카탈로그 서비스 API 참조를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) 참조하십시오.

카탈로그 API가 데이터 수집과 관련된 방식을 보여주는 단계별 작업 과정은 데이터 세트 [만들기에 대한 자습서를 참조하십시오](../datasets/create.md).
