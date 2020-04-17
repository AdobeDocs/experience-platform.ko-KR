---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 개인 정보 서비스 개발자 가이드
description: RESTful API를 사용하여 Adobe Experience Cloud 애플리케이션 전반에서 데이터 주체의 개인 데이터를 관리합니다
topic: developer guide
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# 개인 정보 서비스 개발자 가이드

Adobe Experience Platform 개인 정보 보호 서비스는 Adobe Experience Cloud 응용 프로그램에서 데이터 주체(고객)의 개인 데이터를 관리(액세스 및 삭제)할 수 있도록 해주는 RESTful API 및 사용자 인터페이스를 제공합니다. 또한 개인 정보 보호 서비스는 Experience Cloud 응용 프로그램과 관련된 작업의 상태 및 결과에 액세스할 수 있는 중앙 감사 및 로깅 메커니즘을 제공합니다.

이 안내서에서는 개인정보 보호 서비스 API를 사용하는 방법에 대해 설명합니다. UI 사용 방법에 대한 자세한 내용은 개인 정보 서비스 [UI 개요를](../ui/overview.md)참조하십시오. 개인 정보 서비스 API에서 사용 가능한 모든 끝점의 전체 목록을 보려면 API [참조를](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)참조하십시오.

## 시작하기

이 안내서는 다음과 같은 경험 플랫폼 기능을 이해하는 데 필요합니다.

* [개인 정보 서비스](../home.md):Adobe Experience Cloud 애플리케이션 전반에서 데이터 주체(고객)의 액세스 및 삭제 요청을 관리할 수 있는 RESTful API 및 사용자 인터페이스를 제공합니다.

다음 섹션에서는 Privacy Service API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

* 인증:베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형:application/json

## 다음 단계

이제 사용할 헤더를 이해했으므로 Privacy Service API에 대한 호출을 시작할 수 있습니다. 개인정보 [보호 작업에](privacy-jobs.md) 대한 문서는 개인정보 보호 서비스 API를 사용하여 수행할 수 있는 다양한 API 호출을 안내합니다. 각 예제 호출에는 일반 API 형식, 필요한 헤더를 표시하는 샘플 요청 및 샘플 응답이 포함됩니다.
