---
title: 소스 문서화(Streaming SDK)
description: Adobe Experience Platform에서 새 소스를 라이브로 만들 수 있는 마지막 단계는 새 소스를 문서화하는 것입니다.
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 소스 문서화(Streaming SDK)

>[!NOTE]
>
>Streaming SDK는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

Adobe Experience Platform에서 새 소스를 라이브로 설정하기 전 마지막 단계는 새 소스를 문서화하는 것입니다.

이 설명서 안내서에는 다음이 포함됩니다.

* 새 소스에 대한 설명서 페이지를 만들기 위해 참조할 수 있는 튜토리얼
* 새 소스에 대해 작성할 설명서 템플릿
* [기술 설명서 작성에 Markdown을 사용하는 방법에 대한 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Adobe Markdown 기능 이해에 대한 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions).

## 전제 조건

새 소스 문서화를 시작하려면 먼저 다음 항목이 필요합니다.

* **유효한 GitHub 사용자 계정**: 기존 GitHub 계정이 없는 경우 [GitHub 등록 페이지](https://github.com/);
* **GitHub Desktop에 액세스**: 다음을 사용해야 합니다. [GitHub 데스크탑 앱](https://desktop.github.com/) 로컬 환경에서 소스 설명서를 생성하려면 다음을 수행합니다.
* Adobe과의 통합은 Platform의 스테이징 환경에 배포된 소스와 테스트 단계에 있어야 합니다.

## Platform에서 소스에 대한 설명서를 만드는 고급 지침

상위 수준에서 소스에 대한 설명서를 만들려면 Platform 설명서 리포지토리의 포크를 만들고 제공된 설명서 템플릿을 새 분기에서 편집해야 합니다. Adobe이 제공한 템플릿을 사용하여 새 소스 페이지를 만들고 준비가 되면 가져오기 요청(PR)을 엽니다. 이 작업을 수행하는 지침은 새 소스 페이지를 만드는 단계의 아래에 자세히 나와 있습니다.

## 설명서 템플릿

미리 채워진 을 사용할 수 있습니다 [API 설명서 템플릿](streaming-template-api.md) 또는 [UI 설명서 템플릿](streaming-template-ui.md) 소스에 대한 설명서를 만드는 데 도움이 되도록 합니다. 아래에서 템플릿을 편집하고 가져오기 요청을 여는 방법에 대한 지침을 확인할 수 있습니다. 새 소스에 대해 제출된 설명서는 Adobe 설명서 팀에서 검토하고 게시합니다.

아래의 설명서 템플릿을 다운로드할 수도 있습니다.

* [API 설명서 템플릿](../assets/streaming/streaming-template-api.zip)
* [UI 설명서 템플릿](../assets/streaming/streaming-template-ui.zip)

## 새 소스 페이지 만들기

GitHub 웹 인터페이스 또는 로컬 환경을 사용하여 Platform의 새 소스에 대한 설명서를 만들 수 있습니다. 아래 링크에서 두 옵션에 대한 지침을 확인하십시오.

* [GitHub 웹 인터페이스를 사용하여 소스 설명서 페이지 만들기](../documentation/github.md)
* [로컬 환경에서 텍스트 편집기를 사용하여 소스 설명서 페이지를 만듭니다](../documentation/text-editor.md)
