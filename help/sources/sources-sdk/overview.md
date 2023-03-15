---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: 셀프서비스 소스(Batch SDK) 개요
description: Adobe Experience Platform 셀프 서비스 소스(Batch SDK)는 흐름 서비스 API를 사용하여 REST API 기반 소스를 통합하여 데이터를 Experience Platform 상태로 만들 수 있는 구성 API 세트입니다.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# 셀프서비스 소스(Batch SDK) 개요

Adobe Experience Platform 셀프 서비스 소스(Batch SDK)는 다음을 사용하여 REST API 기반 소스를 Experience Platform 소스 카탈로그에 통합할 수 있는 프레임워크입니다. [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). 셀프 서비스 소스(Batch SDK)는 자체 소스를 빌드하고 배치 데이터를 Experience Platform 상태로 만들기 위한 구성 API 세트를 제공합니다.

셀프서비스 소스(Batch SDK)를 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* 를 사용하여 새 소스를 구성하고 Experience Platform 카탈로그에 통합 [!DNL Flow Service] API.
* 지원되는 인증 유형과 리소스 데이터를 가져오는 방법에 대한 정보를 포함하여 소스에 대한 사양을 정의합니다.
* 새 소스에 대한 사용자 대면 설명서를 만듭니다.

셀프 서비스 소스 설명서는 REST API 기반 소스 통합을 Experience Platform과 구성, 테스트 및 릴리스하고 소스를 지속적으로 성장하는 소스 카탈로그의 일부로 만드는 지침을 제공합니다.

![카탈로그](./assets/catalog.png)

## 소스 이해

Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Experience Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

소스에 대한 자세한 내용과 현재 Experience Platform에서 지원되는 다른 소스의 목록을 보려면 [소스 개요](../home.md).

## 소스 만들기

셀프 서비스 소스를 통해 자체 REST API 기반 소스를 통합하고 데이터를 로 Experience Platform 상태로 만들 수 있습니다. [!DNL Flow Service]. 를 통해 새 연결 사양을 생성, 구성 및 제출하여 Experience Platform 소스 카탈로그에 소스를 통합할 수 있습니다. [!DNL Flow Service] API.

다음 안내서를 참조하십시오 [새 연결 사양 생성](./api/api-overview.md) 새 소스를 Experience Platform에 통합하는 방법에 대한 자세한 내용

## 소스 문서화

소스가 만들어지면 다음을 참조하십시오. [설명서 안내서](./documentation/doc-overview.md) 를 통해 소스를 문서화하는 방법에 대한 지침은 [!DNL GitHub] 웹 인터페이스 또는 고유한 텍스트 편집기를 통해.

## 고급 프로세스

Experience Platform에서 소스를 구성하는 단계별 프로세스는 아래에 요약되어 있습니다.

* 읽기 [셀프서비스 소스(일괄 처리 SDK) API 안내서](./api/api-overview.md).
   * 읽기 [시작 안내서](./api/getting-started.md).
   * 다음에 대한 자습서를 따르십시오 [새 연결 사양 생성](./api/create.md).
   * 다음에 대한 자습서를 따르십시오 [연결 사양 업데이트](./api/update-connection-specs.md).
   * 다음에 대한 자습서를 따르십시오 [흐름 사양에 새 연결 사양 ID 추가](./api/update-flow-specs.md)
   * [새 소스 제출](./api/submit.md).
* 연결 사양의 구조 및 속성을 더 잘 이해하려면 의 안내서를 참조하십시오 [셀프 서비스 소스에 대한 구성 옵션(일괄 SDK)](./config/config.md).
   * 의 안내서 읽기 [인증 사양 구성](./config/authspec.md) 소스에 사용할 수 있는 다양한 인증 유형을 더 잘 이해합니다.
   * 의 안내서 읽기 [소스 세부 항목 구성](./config/sourcespec.md) 소스에 대해 구성할 수 있는 다양한 페이지 매김 유형, 예약 형식 및 사용자 지정 스키마에 대한 정보입니다.
   * 의 안내서 읽기 [탐색 사양 구성](./config/explorespec.md) 소스에 포함된 오브젝트를 탐색하고 검사하는 데 필요한 매개 변수를 정의하는 방법에 대한 정보입니다.
* 소스 문서화를 시작하려면 [셀프 서비스 소스에 대한 설명서 만들기에 대한 개요](./documentation/doc-overview.md)
   * 사용할 수 있습니다. [sources API 설명서 템플릿](./documentation/template.md) 를 사용하여 API 설명서를 구성할 수 있습니다.
   * 사용할 수 있습니다. [소스 UI 설명서 템플릿](./documentation/ui-template.md) 를 사용하여 UI 설명서를 구성할 수 있습니다.
   * 다음 안내서를 참조하십시오 [GitHub 웹 인터페이스 사용](./documentation/github.md) GitHub를 사용하여 설명서를 만드는 방법에 대한 단계입니다.
   * 다음 안내서를 참조하십시오 [텍스트 편집기 사용](./documentation/text-editor.md) 로컬 컴퓨터를 사용하여 설명서를 만드는 방법에 대한 단계입니다.
