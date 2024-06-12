---
solution: Experience Platform
title: 통합 태그 API 시작하기
description: 다음 설명서는 통합 태그 API를 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다.
role: Developer
source-git-commit: 8280281fa8b676b13c0601e2c9a50515ce8979c3
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 9%

---

# 통합 태그 API 시작하기 {#getting-started}

통합 태그 API를 사용하면 Adobe Experience Platform 내에서 비즈니스 개체를 분류하고 관리할 수 있습니다.

다음 섹션에서는 통합 태그 API를 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

통합 태그 API 설명서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 참조하십시오.

## 필수 헤더

API 설명서를 사용하려면 를 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 를 입력하여 Platform 끝점을 성공적으로 호출했습니다. 인증 자습서를 완료하면 아래와 같이 Experience Platform API 호출에서 필요한 각 헤더에 대한 값이 제공됩니다.

- 인증: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스 작업에 대한 자세한 정보 [!DNL Experience Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

## 다음 단계

통합 태그 API를 사용하여 호출하려면 왼쪽 탐색 또는 내에서 사용 가능한 엔드포인트 안내서 중 하나를 선택합니다. [개발자 안내서 개요](./overview.md)
