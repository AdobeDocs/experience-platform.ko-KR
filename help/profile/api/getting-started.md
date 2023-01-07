---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 실시간 고객 프로필 API 시작하기
type: Documentation
description: 프로필 API 시작 안내서에서는 실시간 고객 프로필 API 엔드포인트를 사용하여 프로필 데이터에 대한 기본 CRUD 작업을 수행하기 위해 알아야 하는 주요 개념 및 기본 기능에 대해 간략하게 설명합니다.
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 시작하기 [!DNL Real-Time Customer Profile] API {#getting-started}

실시간 고객 프로필 API 엔드포인트를 사용하여 계산된 속성 구성, 엔티티 액세스, 프로필 데이터 내보내기 및 불필요한 데이터 세트 또는 배치 삭제와 같은 프로필 데이터에 대한 기본 CRUD 작업을 수행할 수 있습니다.

개발자 안내서를 사용하려면 작업에 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 이해를 필요로 합니다 [!DNL Profile] 데이터. 를 사용하기 전에 [!DNL Real-Time Customer Profile] API입니다. 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL Real-Time Customer Profile]](../home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 고객 프로필을 실시간으로 제공합니다.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): 여러 장치와 시스템에서 ID를 브리징하여 고객 및 고객의 행동을 보다 잘 파악할 수 있습니다.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): 실시간 고객 프로필 데이터에서 대상 세그먼트를 작성할 수 있습니다.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 를 성공적으로 호출하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Profile] API 엔드포인트.

## 샘플 API 호출 읽기

다음 [!DNL Real-Time Customer Profile] API 설명서는 요청의 형식을 제대로 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

## 필수 헤더

API 설명서를 사용하려면 를 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 을 성공적으로 호출하기 위해 [!DNL Platform] 엔드포인트. 인증 자습서를 완료하면에서 필요한 각 헤더에 대한 값을 제공합니다. [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 요청 대상 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

요청 본문에 페이로드가 있는 모든 요청(예: POST, PUT 및 PATCH 호출)에는 `Content-Type` 헤더. 각 호출과 관련된 허용된 값은 호출 매개 변수에 제공됩니다.

## 다음 단계

를 사용하여 호출을 시작하려면 [!DNL Real-Time Customer Profile] API를 사용하려면 사용 가능한 엔드포인트 가이드 중 하나를 선택합니다.
