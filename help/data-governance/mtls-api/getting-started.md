---
title: MTLS 서비스 API 시작하기
description: 이 문서에서는 MTLS API를 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다.
role: Developer
source-git-commit: f0b9d414d7b08015478c132de6910629d86c9cf9
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 7%

---

# MTLS 서비스 API 시작 {#getting-started}

MTLS 서비스 API를 사용하면 Adobe에서 발급한 공개 인증서를 안전하게 검색하고 확인할 수 있습니다.

다음 섹션에서는 MTLS 서비스 API를 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

MTLS 서비스 API 설명서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

## 필수 헤더

또한 API 설명서를 사용하려면 플랫폼 끝점을 성공적으로 호출하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 Experience Platform API 호출에서 필요한 각 헤더에 대한 값이 제공됩니다.

- 인증: `Bearer {ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

## 다음 단계

MTLS 서비스 API를 사용하여 호출하려면 왼쪽 탐색 또는 [개발자 안내서 개요](./overview.md) 내에서 끝점 안내서를 선택하십시오
