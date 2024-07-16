---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리
solution: Experience Platform
title: 쿼리 서비스 API 안내서
description: 쿼리 서비스 API를 사용하면 개발자가 표준 SQL을 사용하여 Adobe Experience Platform 데이터를 쿼리할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
role: Developer
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 20%

---

# [!DNL Query Service] API 안내서

이 개발자 안내서는 Adobe Experience Platform [!DNL Query Service] API에서 다양한 작업을 수행하는 단계를 제공합니다.

## 시작하기

이 안내서를 사용하려면 [!DNL Query Service] 사용과 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 이해가 필요합니다.

- [[!DNL Query Service]](../home.md): 데이터 세트를 쿼리하고 결과 쿼리를 [!DNL Experience Platform]의 새 데이터 세트로 캡처하는 기능을 제공합니다.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform]은(는) 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 API를 사용하여 [!DNL Query Service]을(를) 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대해 이 설명서에서 사용되는 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Experience Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

- 인증: `Bearer {ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Platform] API에 대한 모든 요청에는 작업을 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스 작업에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하세요.

## 샘플 API 호출

사용할 헤더를 이해했으므로 [!DNL Query Service] API를 호출할 준비가 되었습니다. 다음 문서는 [!DNL Query Service] API를 사용하여 수행할 수 있는 다양한 API 호출을 안내합니다. 각 예제 호출에는 일반 API 형식, 필요한 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함됩니다.

- [쿼리](queries.md)
- [연결 매개변수](connection-parameters.md)
- [예약된 쿼리](scheduled-queries.md)
- [예약된 쿼리에 대해 실행](runs-scheduled-queries.md)
- [쿼리 템플릿](query-templates.md)
- [가속화된 쿼리](./accelerated-queries.md)
- [경고 구독](./alert-subscriptions.md)

## 다음 단계

[!DNL Query Service] API를 사용하여 호출하는 방법을 배웠으므로 비대화형 쿼리를 직접 만들 수 있습니다. 쿼리를 만드는 방법에 대한 자세한 내용은 [SQL 참조 안내서](../sql/overview.md)를 참조하십시오.
