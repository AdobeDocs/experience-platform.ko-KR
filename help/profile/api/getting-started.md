---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 실시간 고객 프로필 API 시작하기
type: Documentation
description: 프로필 API 시작 안내서에서는 실시간 고객 프로필 API 끝점을 사용하여 프로필 데이터에 대한 기본 CRUD 작업을 수행하기 위해 알아야 하는 주요 개념 및 기본 기능에 대해 간략하게 설명합니다.
role: Developer
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# [!DNL Real-Time Customer Profile] API 시작 {#getting-started}

실시간 고객 프로필 API 끝점을 사용하면 계산된 속성 구성, 엔티티 액세스, 프로필 데이터 내보내기, 불필요한 데이터 세트 또는 배치 삭제와 같은 기본 CRUD 작업을 프로필 데이터에 수행할 수 있습니다.

개발자 안내서를 사용하려면 [!DNL Profile] 데이터 작업과 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 이해가 필요합니다. [!DNL Real-Time Customer Profile] API 작업을 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL Real-Time Customer Profile]](../home.md): 여러 소스에서 집계한 데이터를 기반으로 통합 고객 프로필을 실시간으로 제공합니다.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): 디바이스와 시스템 간에 ID를 연결하여 고객 및 고객 행동에 대한 더 나은 보기를 얻을 수 있습니다.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): 실시간 고객 프로필 데이터에서 대상자를 만들 수 있습니다.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform]은(는) 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Profile] API 끝점을 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

[!DNL Real-Time Customer Profile] API 설명서는 요청의 형식을 제대로 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

## 필수 헤더

또한 API 설명서를 사용하려면 [!DNL Platform] 끝점을 성공적으로 호출하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 [!DNL Experience Platform] API 호출의 각 필수 헤더에 대한 값이 제공됩니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Platform] API에 대한 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

요청 본문에 페이로드가 있는 모든 요청(예: POST, PUT 및 PATCH 호출)에는 `Content-Type` 헤더가 포함되어야 합니다. 각 호출에 대해 허용되는 값은 호출 매개 변수에 제공됩니다.

## 다음 단계

[!DNL Real-Time Customer Profile] API를 사용하여 호출을 시작하려면 사용 가능한 끝점 가이드 중 하나를 선택하십시오.
