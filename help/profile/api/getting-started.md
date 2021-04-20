---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 실시간 고객 프로필 API 시작하기
topic: guide
type: Documentation
description: 프로필 API 시작 안내서는 실시간 고객 프로필 API 끝점을 사용하여 프로필 데이터에 대한 기본 CRUD 작업을 수행하기 위해 알아야 하는 주요 개념 및 기본 기능에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] API {#getting-started} 시작하기

실시간 고객 프로필 API 끝점을 사용하면 계산된 특성 구성, 개체에 액세스, 프로필 데이터 내보내기, 필요 없는 데이터 집합 또는 배치 삭제와 같이 프로필 데이터에 대해 기본 CRUD 작업을 수행할 수 있습니다.

개발자 안내서를 사용하려면 [!DNL Profile] 데이터 작업과 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. [!DNL Real-time Customer Profile] API를 사용하여 작업하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL Real-time Customer Profile]](../home.md):여러 소스에서 수집한 데이터를 기반으로 통합된 고객 프로파일을 실시간으로 제공합니다.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):다양한 디바이스와 시스템에 ID를 연결함으로써 고객과 고객의 행동을 명확하게 파악할 수 있습니다.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md):실시간 고객 프로필 데이터에서 대상 세그먼트를 만들 수 있습니다.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform(플랫폼)이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Profile] API 끝점을 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

[!DNL Real-time Customer Profile] API 설명서는 요청의 형식을 제대로 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

## 필수 헤더

또한 API 설명서는 [!DNL Platform] 끝점을 성공적으로 호출하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

요청 본문에 페이로드가 있는 모든 요청(POST, PUT 및 PATCH 호출 등)은 `Content-Type` 헤더를 포함해야 합니다. 각 호출에 적용되는 허용된 값은 호출 매개 변수에 제공됩니다.

## 다음 단계

[!DNL Real-time Customer Profile] API를 사용하여 호출을 시작하려면 사용 가능한 끝점 안내선 중 하나를 선택합니다.