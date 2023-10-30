---
title: 샌드박스 도구 API 시작하기
description: 샌드박스 도구 API를 사용하여 아티팩트를 검사하고 샌드박스 간에 샌드박스 구성의 스냅샷을 내보내고 가져올 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: 0b34d153-a603-4397-a375-9cc846efe23a
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 14%

---

# 샌드박스 도구 API 시작하기 {#getting-started}

이 개발자 안내서는 샌드박스 도구 API를 사용하여 Adobe Experience Platform에서 패키지 및 도구를 관리하는 데 도움이 되는 단계를 제공하며 다양한 작업을 수행하기 위한 샘플 API 호출이 포함되어 있습니다.

## 샘플 API 호출 읽기 {#api-calls}

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON 데이터도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](/help/landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 참조하십시오.

## 필수 헤더에 대한 값 수집 {#headers}

이 안내서를 사용하려면 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 를 입력하여 Platform API를 성공적으로 호출할 수 있습니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더의 값이 제공됩니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

인증 헤더 외에 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT 및 PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## 다음 단계 {#next-steps}

필요한 자격 증명을 수집했으므로 이제 나머지 개발자 안내서를 계속 읽을 수 있습니다. 각 섹션에서는 해당 끝점에 대한 중요한 정보를 제공하고 CRUD 작업을 수행하기 위한 예제 API 호출을 보여줍니다. 각 호출에는 일반 API 형식, 필요한 헤더와 올바른 형식의 페이로드를 보여주는 샘플 요청 및 성공적인 호출을 위한 샘플 응답이 포함됩니다.

샌드박스 도구 API를 호출하기 시작하려면 다음 API 튜토리얼을 참조하십시오.

* [패키지 끝점](./packages.md)
* [도구 엔드포인트](./tools.md)
