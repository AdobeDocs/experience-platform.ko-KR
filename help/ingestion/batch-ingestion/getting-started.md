---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 데이터 수집 API 시작하기
type: Documentation
description: API를 사용하여 Experience Platform에 데이터를 수집하기 전에 알아야 하는 주요 개념 및 기본 기능에 대해 간략하게 설명합니다.
source-git-commit: 19837e820ab3abdaa0bc8569ad78ce51dec1d21e
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# 데이터 수집 API 시작하기 {#getting-started}

데이터 수집 API 엔드포인트를 사용하여 Adobe Experience Platform에서 데이터를 수집하기 위해 기본 CRUD 작업을 수행할 수 있습니다.

API 안내서를 사용하려면 데이터 작업과 관련된 여러 Adobe Experience Platform 서비스에 대한 작업 이해가 필요합니다. 데이터 수집 API를 사용하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [일괄 수집](./overview.md): 데이터를 Adobe Experience Platform에 배치 파일로 수집할 수 있습니다.
* [[!DNL Real-time Customer Profile]](../home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 고객 프로필을 실시간으로 제공합니다.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Profile] API 종단점을 성공적으로 호출하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

데이터 수집 API 설명서에서는 요청 형식을 적절하게 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서에서 [예제 API 호출](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법 섹션을 참조하십시오.

## 필수 헤더

또한 API 설명서를 사용하려면 [!DNL Platform] 종단점을 성공적으로 호출하기 위해 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

요청 본문에 페이로드가 있는 모든 요청(예: POST, PUT 및 PATCH 호출)에는 `Content-Type` 헤더가 포함되어야 합니다. 각 호출과 관련된 허용된 값은 호출 매개 변수에 제공됩니다.

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.
