---
title: 셀프 서비스 소스(스트리밍 SDK) 시작하기
description: 이 문서에서는 Self-Serve Sources(스트리밍 SDK)를 사용하여 새 소스를 만들기 전에 알아야 하는 사전 요구 사항에 대한 소개를 제공합니다.
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 셀프 서비스 소스(스트리밍 SDK) 시작하기

셀프서비스 소스(스트리밍 SDK)를 사용하면 자체 소스를 통합하여 스트리밍 데이터를 Adobe Experience Platform에 가져올 수 있습니다. 이 문서에서는 을 호출하기 전에 알아야 하는 핵심 개념을 소개합니다 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 높은 수준의 프로세스

Experience Platform에서 소스를 구성하는 단계별 프로세스는 다음과 같습니다.

### 통합

* [스트리밍 SDK에 대한 새 연결 사양 만들기](create.md).
* [새로운 연결 사양 ID로 스트리밍 흐름 사양을 업데이트합니다](update-flow-specs.md).
* [스트리밍 소스 테스트 및 제출](submit.md).

### 설명서

* 소스 문서화를 시작하려면 다음을 참조하십시오 [셀프 서비스 소스를 위한 설명서 작성에 대한 개요](../documentation/doc-overview.md).
* 안내서 읽기 [gitHub 웹 인터페이스 사용](../documentation/github.md) gitHub를 사용하여 설명서를 만드는 방법에 대한 절차.
* 안내서 읽기 [텍스트 편집기 사용](../documentation/text-editor.md) 로컬 시스템을 사용하여 설명서를 만드는 방법에 대한 단계입니다.
* [스트리밍 SDK API 설명서 템플릿을 사용하여 API에 소스를 문서화합니다](streaming-template-api.md).
* [스트리밍 SDK UI 설명서 템플릿을 사용하여 UI에서 소스를 문서화합니다](streaming-template-ui.md).

문서 템플릿을 아래에 다운로드할 수도 있습니다.

* [API 설명서 템플릿](../assets/streaming/streaming-template-api.zip)
* [UI 설명서 템플릿](../assets/streaming/streaming-template-ui.zip)

## 전제 조건

>[!IMPORTANT]
>
>Experience Platform과 통합하려는 소스는 끝점을 구독할 수 있는 웹 후크를 지원하여 업데이트를 보낼 수 있어야 합니다.

셀프 서비스 소스(스트리밍 SDK)를 사용하려면 Adobe Experience Platform 소스로 제공된 샌드박스 조직에 액세스할 수 있는지 확인해야 합니다.

또한 이 안내서에서는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 샘플 API 호출 읽기

셀프 서비스 소스(스트리밍 SDK) 및 [!DNL Flow Service] API 설명서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 을 참조하십시오.

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

자체 제공 소스(스트리밍 SDK)로 새 소스를 만들려면 [새 소스 만들기](./create.md).
