---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 데이터 수집 API 시작하기
type: Documentation
description: API를 사용하여 Experience Platform에 데이터를 수집하기 전에 알아야 하는 주요 개념 및 기본 기능에 대해 간략하게 설명합니다.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 데이터 수집 API 시작하기 {#getting-started}

데이터 수집 API 엔드포인트를 사용하여 Adobe Experience Platform에서 데이터를 수집하기 위해 기본 CRUD 작업을 수행할 수 있습니다.

API 안내서를 사용하려면 데이터 작업과 관련된 여러 Adobe Experience Platform 서비스에 대한 작업 이해가 필요합니다. 데이터 수집 API를 사용하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [일괄 수집](./overview.md): 데이터를 Adobe Experience Platform에 배치 파일로 수집할 수 있습니다.
* [[!DNL Real-Time Customer Profile]](../home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 고객 프로필을 실시간으로 제공합니다.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 를 성공적으로 호출하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Profile] API 엔드포인트.

## 샘플 API 호출 읽기

데이터 수집 API 설명서에서는 요청 형식을 적절하게 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

## 필수 헤더

API 설명서를 사용하려면 를 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 을 성공적으로 호출하기 위해 [!DNL Platform] 엔드포인트. 인증 자습서를 완료하면에서 필요한 각 헤더에 대한 값을 제공합니다. [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

요청 본문에 페이로드가 있는 모든 요청(예: POST, PUT 및 PATCH 호출)에는 `Content-Type` 헤더. 각 호출과 관련된 허용된 값은 호출 매개 변수에 제공됩니다.

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 요청 대상 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).
