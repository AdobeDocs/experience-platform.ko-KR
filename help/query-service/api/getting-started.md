---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리
solution: Experience Platform
title: Query Service API 안내서
topic-legacy: query templates
description: Query Service API를 사용하여 개발자가 표준 SQL을 사용하여 Adobe Experience Platform 데이터를 쿼리할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 4f85f38e4870f0c2429a3a2a50bd7f95075c6be4
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 5%

---

# [!DNL Query Service] API 안내서

이 개발자 안내서에서는 Adobe Experience Platform에서 다양한 작업을 수행하는 단계를 제공합니다 [!DNL Query Service] API.

## 시작하기

이 안내서에서는 사용과 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 이해를 필요로 합니다 [!DNL Query Service].

- [[!DNL Query Service]](../home.md): 데이터 세트를 쿼리하고 결과 쿼리를 의 새 데이터 세트로 캡처할 수 있는 기능을 제공합니다. [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Query Service] api 사용.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대해 이 설명서에서 사용되는 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Experience Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Platform] 아래에 표시된 대로 API 호출:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스 작업에 대한 자세한 내용은 [!DNL Experience Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

## 샘플 API 호출

이제 사용할 헤더를 이해하므로 을 호출할 준비가 되었습니다. [!DNL Query Service] API. 다음 문서는 [!DNL Query Service] API. 각 예제 호출에는 일반 API 형식, 필수 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함되어 있습니다.

- [쿼리](queries.md)
- [연결 매개 변수](connection-parameters.md)
- [예약된 쿼리](scheduled-queries.md)
- [예약된 쿼리에 대해 실행됩니다](runs-scheduled-queries.md)
- [쿼리 템플릿](query-templates.md)
- [경고 구독](./alert-subscriptions.md)

## 다음 단계

이제 다음을 사용하여 호출을 하는 방법을 배웠습니다. [!DNL Query Service] API를 사용하여 고유한 비대화형 쿼리를 만들 수 있습니다. 쿼리를 만드는 방법에 대한 자세한 내용은 [SQL 참조 안내서](../sql/overview.md).
