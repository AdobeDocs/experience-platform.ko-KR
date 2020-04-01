---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 액세스 제어 개발자 가이드
topic: developer guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# 액세스 제어 개발자 가이드

경험 플랫폼의 액세스 제어는 Adobe Admin Console을 통해 [관리됩니다](https://adminconsole.adobe.com). 이 기능은 사용 권한 및 샌드박스를 사용자와 연결하는 Admin Console의 제품 프로필을 활용합니다. 자세한 내용은 [액세스 제어 개요를](../home.md) 참조하십시오.

이 개발자 안내서에서는 액세스 제어 API에 대한 요청의 형식을 지정하는 방법에 [대한](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)정보를 제공하며 다음 작업을 다룹니다.

- [권한 및 리소스 유형의 목록 이름](./permissions-and-resource-types.md)
- [현재 사용자에 대한 효과적인 정책 보기](./effective-policies.md)

## 시작하기

다음 섹션에서는 스키마 레지스트리 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 다음 단계

이제 필요한 자격 증명을 수집했으므로 개발자 가이드의 나머지 부분을 계속 읽을 수 있습니다. 각 섹션에서는 끝점에 대한 중요한 정보를 제공하며 CRUD 작업 수행을 위한 예제 API 호출을 보여줍니다. 각 호출에는 일반 API **형식**, 필요한 헤더와 올바른 형식의 페이로드를 표시하는 샘플 **요청** 및 성공적인 호출을 위한 샘플 **응답이** 포함됩니다.