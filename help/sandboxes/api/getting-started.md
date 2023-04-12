---
keywords: Experience Platform;홈;인기 항목;샌드박스 개발자 안내서
solution: Experience Platform
title: 샌드박스 API 시작하기
description: Sandbox API를 통해 개발자는 Adobe Experience Platform에서 샌드박스를 프로그래밍 방식으로 관리할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 5%

---

# 샌드박스 API 시작하기

Adobe Experience Platform의 샌드박스는 프로덕션 환경에 영향을 주지 않고 기능을 테스트하고, 실험을 실행하고, 사용자 지정 구성을 만들 수 있는 분리된 개발 환경을 제공합니다.

이 개발자 가이드는 Sandbox API를 사용하여 Experience Platform의 샌드박스를 관리하는 데 도움이 되는 단계를 제공하며, 다양한 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 사전 요구 사항

조직의 샌드박스를 관리하려면 샌드박스 관리 권한이 있어야 합니다. 액세스 권한이 없는 사용자는 [사용 가능한 샌드박스 끝점](./available.md) 현재 사용자의 활성 샌드박스를 나열하려면 다음을 수행하십시오. 자세한 내용은 [액세스 제어 개요](../../access-control/home.md) 을 참조하십시오.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에서 사용되는 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 을 참조하십시오.

### 필수 헤더에 대한 값을 수집합니다

이 안내서를 사용하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 를 호출하여 플랫폼 API를 성공적으로 호출했습니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

인증 헤더 외에, 모든 요청에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT 및 PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형: application/json

## 다음 단계

이제 필요한 자격 증명을 수집했으므로 개발자 가이드의 나머지 부분을 계속 읽을 수 있습니다. 각 섹션에서는 종단점에 대한 중요한 정보를 제공하며 CRUD 작업을 수행하기 위한 예제 API 호출을 보여줍니다. 각 호출에는 일반 API 형식, 필수 헤더와 올바른 형식의 페이로드를 보여주는 샘플 요청 및 성공적인 호출을 위한 샘플 응답이 포함되어 있습니다.
