---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: 소스 SDK 개요(베타)
topic-legacy: overview
description: Adobe Experience Platform Sources SDK는 Flow Service API를 사용하여 REST API 기반 소스를 통합하여 데이터를 Experience Platform으로 가져올 수 있는 구성 API 세트입니다.
hide: true
hidefromtoc: true
source-git-commit: d98cf404fd1a4d150f202154aba87b0089418957
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 소스 SDK 개요(베타)

>[!IMPORTANT]
>
>소스 SDK는 현재 베타 버전이며 조직에서 아직 액세스할 수 없습니다. 이 설명서에 설명된 기능은 변경될 수 있습니다.

Adobe Experience Platform 소스 SDK는 를 사용하여 REST API 기반 소스를 통합할 수 있는 구성 API 세트입니다 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) Experience Platform으로 데이터를 가져오기 위해

소스 SDK를 사용하여 다음을 수행할 수 있습니다.

* 를 사용하여 기능 만들기, 읽기, 업데이트 및 삭제를 완료하고 플랫폼 카탈로그에 새 소스를 구성합니다 [!DNL Flow Service] API.
* 지원되는 인증 유형과 리소스 데이터를 가져오는 방법을 비롯하여 소스에 대한 사양을 정의합니다.
* 새 소스에 대한 사용자 관련 설명서를 만듭니다.

소스 SDK 설명서는 Adobe Experience Platform Sources SDK를 사용하여 Platform과의 REST API 기반 소스 통합을 구성, 테스트 및 출시하고, 소스가 지속적으로 증가하고 있는 소스 카탈로그의 일부가 되도록 하는 지침을 제공합니다.

![카탈로그](./assets/catalog.png)

## 소스 이해

플랫폼은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

소스에 대한 자세한 내용을 확인하고 현재 Platform에서 지원되는 다른 소스 목록을 보려면 [소스 개요](../home.md).

## 소스 만들기

Sources SDK를 통해 고유한 REST API 기반 소스를 통합하고 데이터를 Platform과 함께 가져올 수 있습니다. [!DNL Flow Service]. 소스 SDK를 사용하면 를 통해 새 연결 사양을 만들고 제출함으로써 새로운 소스를 Platform과 통합할 수 있습니다 [!DNL Flow Service] API.

다음 안내서를 참조하십시오. [새 연결 사양 생성](./api/api-overview.md) 를 참조하십시오.

## 소스 문서 작성

소스가 생성되면 다음을 참조하십시오. [설명서 안내서](./documentation/doc-overview.md) 을 통해 소스를 문서화하는 방법에 대한 지침 [!DNL GitHub] 웹 인터페이스 또는 텍스트 편집기를 통해 사용할 수 있습니다.

## 높은 수준의 프로세스

Experience Platform에서 소스를 구성하는 단계별 프로세스는 다음과 같습니다.

* 다음 문서를 참조하십시오. [Sources SDK API 안내서](./api/api-overview.md);
   * 다음 문서를 참조하십시오. [시작 안내서](./api/getting-started.md);
   * 다음의 자습서를 따르십시오 [새 연결 사양 생성](./api/create.md);
   * 다음의 자습서를 따르십시오 [연결 사양 업데이트](./api/update-connection-specs.md);
   * 다음의 자습서를 따르십시오 [흐름 사양에 새 연결 사양 ID 추가](./api/update-flow-specs.md)
   * [새 소스 제출](./api/submit.md).
* 연결 사양의 구조 및 속성을 보다 잘 이해하려면 다음 안내서를 참조하십시오 [소스 SDK에 대한 구성 옵션](./config/config.md);
   * 다음 안내서를 참조하십시오. [인증 사양 구성](./config/authspec.md);
   * 다음 안내서를 참조하십시오. [소스 사양 구성](./config/sourcespec.md);
   * 다음 안내서를 참조하십시오. [탐색 사양 구성](./config/explorespec.md);
* 소스 문서화를 시작하려면 다음을 참조하십시오 [소스 SDK용 설명서 작성에 대한 개요](./documentation/doc-overview.md)
   * 이 기능을 사용할 수 있습니다 [소스 설명서 템플릿](./documentation/template.md) 설명서를 구조화하는 방법
   * 다음 안내서를 참조하십시오. [gitHub 웹 인터페이스 사용](./documentation/github.md) gitHub를 사용하여 설명서를 만드는 방법에 대한 절차를 설명합니다.
   * 다음 안내서를 참조하십시오. [텍스트 편집기 사용](./documentation/text-editor.md) 로컬 시스템을 사용하여 설명서를 만드는 방법에 대한 단계입니다.

