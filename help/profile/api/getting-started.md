---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 실시간 고객 프로필 API 개발자 가이드
topic: guide
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# 실시간 고객 프로필 API 시작하기 {#getting-started}

실시간 고객 프로필 API를 사용하면 계산된 속성 구성, 엔티티 액세스, 프로필 데이터 내보내기, 불필요한 데이터 세트 또는 배치 삭제 등 프로필 리소스에 대해 기본 CRUD 작업을 수행할 수 있습니다.

개발자 안내서를 사용하려면 프로필 데이터 작업과 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 실시간 고객 프로필 API를 사용하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [실시간 고객 프로필](../home.md): 여러 소스에서 수집한 데이터를 기반으로 통합된 고객 프로필을 실시간으로 제공합니다.
* [Adobe Experience Platform ID 서비스](../../identity-service/home.md): 다양한 디바이스와 시스템에 ID를 연결하여 고객 및 고객의 행동을 명확하게 파악할 수 있습니다.
* [Adobe Experience Platform 세그멘테이션 서비스](../../segmentation/home.md): 실시간 고객 프로필 데이터를 통해 고객 세그먼트를 만들 수 있습니다.
* [XDM(Experience Data Model)](../../xdm/home.md): Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [샌드박스](../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 Platform 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 프로필 API 끝점을 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

실시간 고객 프로필 API 설명서는 요청의 형식을 제대로 지정하는 방법을 시연하는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 예제 API 호출 [](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 읽기 방법에 대한 섹션을 참조하십시오.

## 필요한 헤더

또한 API 설명서는 Platform 끝점에 대한 호출을 성공적으로 수행하려면 [인증 자습서를](../../tutorials/authentication.md) 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증: 무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. Platform API에 대한 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

요청 본문에 페이로드가 있는 모든 요청(예: POST, PUT 및 PATCH 호출)에는 `Content-Type` 헤더가 포함되어야 합니다. 각 호출과 관련된 허용된 값은 호출 매개 변수에 제공됩니다.

## 다음 단계

실시간 고객 프로필 API를 사용하여 호출을 시작하려면 사용 가능한 끝점 가이드 중 하나를 선택합니다.