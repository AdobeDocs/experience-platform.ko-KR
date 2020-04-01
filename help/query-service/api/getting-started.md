---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 쿼리 서비스 개발자 가이드
topic: query templates
translation-type: tm+mt
source-git-commit: 91104399e50bce03fed7c9196e6e83fc48a54d1c

---


# 쿼리 서비스 개발자 가이드

이 개발자 안내서에서는 Adobe Experience Platform 쿼리 서비스 API에서 다양한 작업을 수행하기 위한 단계를 제공합니다.

## 시작하기

이 가이드는 쿼리 서비스 사용과 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 이해를 필요로 합니다.

- [쿼리 서비스](../home.md):Experience Platform에서 데이터 세트를 쿼리하고 결과 쿼리를 새로운 데이터 집합으로 캡처하는 기능을 제공합니다.
- [XDM(Experience Data Model) 시스템](../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [샌드박스](../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 API를 사용하여 쿼리 서비스를 성공적으로 사용하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 이 문서에서 샘플 API 호출에 사용되는 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 예제 API 호출을 [읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

Experience Platform API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 자습서를 완료하면 다음과 같이 모든 플랫폼 API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 경험 플랫폼의 샌드박스 작업에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

## 샘플 API 호출

이제 사용할 헤더를 이해했으므로 쿼리 서비스 API에 대한 호출을 시작할 수 있습니다. 다음 문서에서는 쿼리 서비스 API를 사용하여 수행할 수 있는 다양한 API 호출을 설명합니다. 각 예제 호출에는 일반 API 형식, 필요한 헤더를 표시하는 샘플 요청 및 샘플 응답이 포함됩니다.

- [쿼리](queries.md)
- [연결 매개 변수](connection-parameters.md)
- [예약된 쿼리](scheduled-queries.md)
- [예약된 쿼리에 대해 실행](runs-scheduled-queries.md)
- [쿼리 템플릿](query-templates.md)

## 다음 단계

이제 쿼리 서비스 API를 사용하여 호출을 수행하는 방법을 알았으므로, 비대화형 쿼리를 직접 만들 수 있습니다. 쿼리를 만드는 방법에 대한 자세한 내용은 SQL [참조 안내서를](../sql/overview.md)참조하십시오.