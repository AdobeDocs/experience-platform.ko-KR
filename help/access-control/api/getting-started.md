---
keywords: Experience Platform;홈;인기 항목;액세스 제어;api;시작하기
solution: Experience Platform
title: 액세스 제어 API 안내서
description: Adobe Experience Platform의 액세스 제어를 사용하면 Adobe Admin Console을 사용하여 다양한 Platform 기능에 대한 역할과 권한을 관리할 수 있습니다. 다음 섹션에서는 개발자가 스키마 레지스트리 API를 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다.
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---

# [!DNL Access Control] API 안내서

[!DNL Access control] 대상 [!DNL Experience Platform] 를 통해 관리됩니다. [Adobe Admin Console](https://adminconsole.adobe.com). 이 기능은 사용 권한 및 샌드박스를 사용자와 연결하는 Admin Console의 제품 프로필을 활용합니다. 다음을 참조하십시오. [액세스 제어 개요](../home.md) 추가 정보.

이 개발자 안내서에서는 요청에 대한 형식을 지정하는 방법에 대한 정보를 제공합니다. [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)및 는 다음 작업을 다룹니다.

- [권한 및 리소스 유형의 목록 이름](./permissions-and-resource-types.md)
- [현재 사용자에 대한 유효 액세스 정책 보기](./effective-policies.md)

## 시작하기

다음 섹션에서는 를 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다. [!DNL Access Control] API.

### 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값 수집

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

## 다음 단계

필요한 자격 증명을 수집했으므로 이제 나머지 개발자 안내서를 계속 읽을 수 있습니다. 각 섹션에서는 해당 끝점에 대한 중요한 정보를 제공하고 CRUD 작업을 수행하기 위한 예제 API 호출을 보여줍니다. 각 호출에는 일반 API 형식, 필요한 헤더와 올바른 형식의 페이로드를 보여주는 샘플 요청 및 성공적인 호출을 위한 샘플 응답이 포함됩니다.
