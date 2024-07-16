---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: 셀프서비스 소스(Batch SDK) 개요
description: Adobe Experience Platform 셀프 서비스 소스(Batch SDK)는 흐름 서비스 API를 사용하여 REST API 기반 소스를 통합하여 데이터를 Experience Platform 상태로 만들 수 있는 구성 API 세트입니다.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 3%

---

# 셀프서비스 소스(Batch SDK) 개요

Adobe Experience Platform 셀프 서비스 소스(Batch SDK)는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 REST API 기반 소스를 Experience Platform 소스 카탈로그에 통합할 수 있는 프레임워크입니다. 셀프 서비스 소스(Batch SDK)는 자체 소스를 빌드하고 배치 데이터를 Experience Platform 상태로 만들기 위한 구성 API 세트를 제공합니다.

셀프서비스 소스(Batch SDK)를 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* [!DNL Flow Service] API를 사용하여 새 소스를 구성하고 Experience Platform 카탈로그에 통합합니다.
* 지원되는 인증 유형과 리소스 데이터를 가져오는 방법에 대한 정보를 포함하여 소스에 대한 사양을 정의합니다.
* 새 소스에 대한 사용자 대면 설명서를 만듭니다.

셀프 서비스 소스 설명서는 REST API 기반 소스 통합을 Experience Platform과 구성, 테스트 및 릴리스하고 소스를 지속적으로 성장하는 소스 카탈로그의 일부로 만드는 지침을 제공합니다.

![카탈로그](./assets/catalog.png)

## 소스 이해

Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Experience Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

소스에 대한 자세한 정보와 현재 Experience Platform에서 지원되는 다른 소스의 목록을 보려면 [소스 개요](../home.md)를 참조하십시오.

## 소스 만들기

셀프 서비스 소스를 통해 고유한 REST API 기반 소스를 통합하고 데이터를 [!DNL Flow Service](으)로 Experience Platform 상태로 만들 수 있습니다. [!DNL Flow Service] API를 통해 새 연결 사양을 만들고 구성하고 제출하여 Experience Platform 소스 카탈로그에 소스를 통합할 수 있습니다.

새 소스를 Experience Platform에 통합하는 방법에 대한 자세한 내용은 [새 연결 사양 만들기](./api/api-overview.md)에 대한 안내서를 참조하십시오.

## 소스 문서화

소스가 만들어지면 [!DNL GitHub] 웹 인터페이스 또는 자체 텍스트 편집기를 통해 소스를 문서화하는 방법에 대한 지침은 [설명서 안내서](./documentation/doc-overview.md)를 참조하십시오.

## 고급 프로세스

Experience Platform에서 소스를 구성하는 단계별 프로세스는 아래에 요약되어 있습니다.

* [셀프 서비스 원본(일괄 처리 SDK) API 안내서](./api/api-overview.md)를 읽어 보세요.
   * [시작 안내서](./api/getting-started.md)를 읽어 보세요.
   * [새 연결 사양 만들기](./api/create.md)에 대한 자습서를 따르십시오.
   * [연결 사양 업데이트](./api/update-connection-specs.md)에 대한 자습서를 따르십시오.
   * [흐름 사양에 새 연결 사양 ID를 추가](./api/update-flow-specs.md)하는 자습서를 따르십시오.
   * [새 원본을 제출하세요](./api/submit.md).
* 연결 사양의 구조 및 속성을 더 잘 이해하려면 [셀프 서비스 소스(일괄 SDK)에 대한 구성 옵션](./config/config.md)에 대한 안내서를 읽어 보십시오.
   * 소스에 사용할 수 있는 다양한 인증 유형을 더 잘 이해하려면 [인증 사양 구성](./config/authspec.md)에 대한 안내서를 읽어 보십시오.
   * 소스에 대해 구성할 수 있는 다양한 페이지 매김 유형, 예약 형식 및 사용자 지정 스키마에 대한 정보는 [소스 사양 구성](./config/sourcespec.md)에 대한 안내서를 참조하십시오.
   * 소스에 포함된 개체를 탐색하고 검사하는 데 필요한 매개 변수를 정의하는 방법에 대한 자세한 내용은 [탐색 사양 구성](./config/explorespec.md)에 대한 안내서를 참조하십시오.
* 소스 문서화를 시작하려면 [셀프 서비스 소스에 대한 문서 만들기에 대한 개요](./documentation/doc-overview.md)를 읽어 보세요.
   * 이 [소스 API 설명서 템플릿](./documentation/template.md)을(를) 사용하여 API 설명서를 구성할 수 있습니다.
   * 이 [소스 UI 설명서 템플릿](./documentation/ui-template.md)을 사용하여 UI 설명서를 구성할 수 있습니다.
   * GitHub를 사용하여 설명서를 만드는 방법에 대한 단계는 [GitHub 웹 인터페이스 사용](./documentation/github.md)에 대한 안내서를 참조하십시오.
   * 로컬 컴퓨터를 사용하여 설명서를 만드는 방법에 대한 단계는 [텍스트 편집기 사용](./documentation/text-editor.md)에 대한 안내서를 참조하십시오.
