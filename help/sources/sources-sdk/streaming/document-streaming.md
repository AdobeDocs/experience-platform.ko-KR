---
title: 소스 문서(스트리밍 SDK)
description: 새 소스를 Adobe Experience Platform에서 라이브로 만들려면 먼저 새 소스를 문서화하는 작업을 수행해야 합니다.
hide: true
hidefromtoc: true
source-git-commit: a9879530a8911d77dfc4cde3824834e03fa5e0a9
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 소스 문서(스트리밍 SDK)

새 소스를 Adobe Experience Platform에서 라이브로 설정하려면 마지막 단계를 수행해야 새 소스를 작성할 수 있습니다.

이 설명서 안내서에는 다음이 포함되어 있습니다.

* 새 소스에 대한 설명서 페이지를 만드는 데 참조할 수 있는 자습서입니다.
* 새 소스에 대한 설명서 템플릿
* [기술 설명서 작성에 Markdown을 사용하는 방법에 대한 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Adobe Markdown 맛 이해에 대한 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions).

## 전제 조건

새 소스를 문서화하기 전에 다음 항목이 필요합니다.

* **유효한 GitHub 사용자 계정**: 기존 GitHub 계정이 없다면 다음을 통해 계정을 만들어야 합니다 [GitHub 등록 페이지](https://github.com/);
* **GitHub Desktop 액세스**: 를 사용해야 합니다 [GitHub Desktop 앱](https://desktop.github.com/) 로컬 환경에서 소스 설명서를 작성하기 위해
* Adobe와의 통합이 Platform의 스테이징 환경에 배포된 소스와 테스트 단계에 있어야 합니다.

## Platform에서 소스에 대한 설명서를 만드는 고급 지침

높은 수준에서 소스에 대한 설명서를 만들려면 Platform 설명서 리포지토리의 포크를 만들고 새 분기에 제공된 설명서 템플릿을 편집해야 합니다. Adobe 제공 템플릿을 사용하여 새 소스 페이지를 만들고 준비가 되면 끌어오기 요청(PR)을 엽니다. 이렇게 하기 위한 지침은 새 소스 페이지를 만드는 단계에서 아래에 자세히 나와 있습니다.

## 설명서 템플릿

미리 채워진 을 사용할 수 있습니다 [API 설명서 템플릿](streaming-template-api.md) 또는 [UI 설명서 템플릿](streaming-template-ui.md) 를 사용하여 소스에 대한 설명서를 작성할 수 있습니다. 아래에서도 템플릿을 편집하고 끌어오기 요청을 여는 방법에 대한 지침을 찾을 수 있습니다. 새 소스에 대해 제출된 설명서는 Adobe 설명서 팀이 검토 및 게시합니다.

문서 템플릿을 아래에 다운로드할 수도 있습니다.

* [API 설명서 템플릿](../assets/streaming/streaming-template-api.zip)
* [UI 설명서 템플릿](../assets/streaming/streaming-template-ui.zip)

## 새 소스 페이지 만들기

GitHub 웹 인터페이스 또는 로컬 환경을 사용하여 Platform의 새 소스에 대한 설명서를 만들 수 있습니다. 아래 링크에서 두 옵션에 대한 지침을 찾으십시오.

* [GitHub 웹 인터페이스를 사용하여 소스 설명서 페이지를 만듭니다](../documentation/github.md)
* [로컬 환경에서 텍스트 편집기를 사용하여 소스 설명서 페이지를 만듭니다](../documentation/text-editor.md)
