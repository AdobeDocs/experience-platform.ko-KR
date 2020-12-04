---
keywords: Experience Platform;home;popular topics;access control;api;getting started
solution: Experience Platform
title: 액세스 제어 개발자 가이드
topic: developer guide
description: Adobe Experience Platform의 액세스 제어를 통해 Adobe Admin Console을 사용하여 다양한 플랫폼 기능에 대한 역할 및 권한을 관리할 수 있습니다. 다음 섹션에서는 스키마 레지스트리 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 4%

---


# [!DNL Access control] 개발자 가이드

[!DNL Access control] 이 [!DNL Experience Platform] 는 [Adobe Admin Console](https://adminconsole.adobe.com)를 통해 관리된다. 이 기능은 Admin Console의 제품 프로필을 활용하므로 사용자에게 사용 권한 및 샌드박스를 연결합니다. 자세한 내용은 [액세스 제어 개요를](../home.md) 참조하십시오.

이 개발자 안내서에서는 요청에 형식을 지정하는 방법에 대한 정보를 제공하고 다음 작업을 다룹니다. [[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)

- [권한 및 리소스 유형의 목록 이름](./permissions-and-resource-types.md)
- [현재 사용자에 대한 효과적인 정책 보기](./effective-policies.md)

## 시작하기

다음 섹션에서는 [!DNL Schema Registry] API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 다음 단계

이제 필요한 자격 증명을 수집했으므로 개발자 가이드의 나머지 부분을 계속 읽을 수 있습니다. 각 섹션은 해당 끝점과 관련된 중요한 정보를 제공하며 CRUD 작업을 수행하기 위한 예제 API 호출을 보여줍니다. 각 호출에는 일반 API 형식, 필요한 헤더와 올바른 형식의 페이로드를 보여주는 샘플 요청 및 성공적인 호출을 위한 샘플 응답이 포함됩니다.
