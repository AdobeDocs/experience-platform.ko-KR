---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: 셀프 서비스 소스 시작하기(배치 SDK)
description: 이 문서에서는 Self-Serve Sources(배치 SDK)를 사용하여 새 소스를 만들기 전에 알아야 하는 전제 조건 정보를 소개합니다.
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# 셀프 서비스 소스 시작하기(배치 SDK)

셀프서비스 소스(배치 SDK)를 사용하면 REST 기반 소스를 통합하여 배치 데이터를 Adobe Experience Platform에 가져올 수 있습니다. 이 문서에서는 을 호출하기 전에 알아야 하는 핵심 개념을 소개합니다 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 전제 조건

셀프 서비스 소스(배치 SDK)를 사용하려면 Adobe Experience Platform 소스로 제공된 IMS 조직 샌드박스에 액세스할 수 있는지 확인해야 합니다.

또한 이 안내서에서는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 샘플 API 호출 읽기

셀프 서비스 소스(배치 SDK) 및 [!DNL Flow Service] API 설명서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 을 참조하십시오.

## 필수 헤더에 대한 값을 수집합니다

플랫폼 API를 호출하려면 먼저 를 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

에 속하는 리소스를 포함하여 플랫폼의 모든 리소스 [!DNL Flow Service]은 특정 가상 샌드박스로 구분됩니다. Platform API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 설명서](../../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## 다음 단계

셀프 서비스 소스(배치 SDK)로 새 소스를 만들려면 [새 소스 만들기](./create.md).
