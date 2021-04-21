---
keywords: Experience Platform;홈;인기 항목;샌드박스 개발자 안내서
solution: Experience Platform
title: 샌드박스 API 안내서
topic-legacy: developer guide
description: Sandbox API를 사용하면 개발자는 Adobe Experience Platform에서 샌드박스를 프로그래밍 방식으로 관리할 수 있습니다. API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보려면 이 안내서를 따르십시오.
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# 샌드박스 API 안내서

Adobe Experience Platform의 샌드박스는 제작 환경에 영향을 미치지 않고 기능을 테스트하고 실험을 실행하며 사용자 정의 구성을 만들 수 있는 분리된 개발 환경을 제공합니다.

이 개발자 안내서에서는 샌드박스 API를 사용하여 Experience Platform의 샌드박스를 관리하는 데 도움이 되는 단계를 제공하며 다양한 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 샌드박스 API 시작하기

IMS 조직에 대한 샌드박스를 관리하려면 샌드박스 관리 권한이 있어야 합니다. 액세스 권한이 없는 사용자는 현재 사용자](./list-active-sandboxes.md)에 대한 활성 샌드박스 목록을 나열하기 위한 끝점만 사용할 수 있습니다. [ Experience Platform에 대한 샌드박스 권한을 할당하는 방법에 대한 자세한 내용은 [액세스 제어 개요](../../access-control/home.md)를 참조하십시오.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출을 위한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법을 참조하십시오.

### 필수 헤더에 대한 값 수집

이 안내서에서는 플랫폼 API를 성공적으로 호출하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증:Bearer `{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

모든 요청에는 인증 헤더 외에 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name:`{SANDBOX_NAME}`

페이로드(POST, PUT 및 PATCH)을 포함하는 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형:application/json

## 다음 단계

이제 필요한 자격 증명을 수집했으므로 개발자 가이드의 나머지 부분을 계속 읽을 수 있습니다. 각 섹션은 해당 끝점에 대한 중요한 정보를 제공하며 CRUD 작업을 수행하기 위한 API 호출 예를 보여줍니다. 각 호출에는 일반 API 형식, 필수 헤더와 올바른 형식의 페이로드를 표시하는 샘플 요청 및 성공적인 호출을 위한 샘플 응답이 포함됩니다.
