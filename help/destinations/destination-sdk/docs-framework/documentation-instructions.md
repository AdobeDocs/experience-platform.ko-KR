---
title: Adobe Experience Platform에서 대상 문서화
description: Adobe Experience Platform에서 대상에 대한 설명서 페이지를 만드는 단계별 지침
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 1%

---

# Adobe Experience Platform에서 대상 문서화

>[!IMPORTANT]
>
>여기에 설명된 프로세스는 제품화된(공개) 대상을 제출하는 파트너에게만 필요합니다. 직접 사용할 개인 대상을 만드는 경우 대상에 대한 설명서를 만들어 게시할 필요가 없습니다.

## 개요 {#overview}

Adobe Experience Platform에 오신 것을 환영합니다. 여기에 오신 것을 환영합니다!
대상을 문서화하는 것은 Adobe Experience Platform에서 라이브로 설정하기 전에 마지막 단계입니다.

이 설명서 섹션에는 다음이 포함됩니다.

* 새 대상에 대한 설명서 페이지를 만드는 단계별 지침
* 대상을 위해 작성할 템플릿
* [Markdown 사용에 대한 일반 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Adobe Markdown 향에 대한 특정 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions) (Adobe Markdown 향수는 일반 Markdown과 매우 유사합니다.)
* A [우수 사례 페이지](./authoring-best-practices.md) Experience Platform 설명서 품질 표준을 충족하는 대상 페이지의 설명서 페이지를 작성하는 데 도움이 됩니다.

## 전제 조건 {#prerequisites}

이 문서의 지침에 따라 대상에 대한 설명서를 만들려면 다음 항목이 필요합니다.

* **GitHub 계정**. 다음에 등록 [GitHub](https://github.com/) 계정이 아직 없는 경우
* **GitHub Desktop**. 다음을 선택하는 경우 [로컬 환경에서 설명서 만들기](./work-in-local-environment.md), 다음을 사용해야 합니다. [GitHub Desktop](https://desktop.github.com/).
* Adobe과의 통합은 Adobe Experience Platform의 스테이징 환경에 배포된 대상과의 테스트 단계에 있어야 합니다.

## Adobe Experience Platform에서 대상에 대한 설명서를 만드는 고급 지침 {#high-level-instructions}

높은 수준에서 대상에 대한 설명서를 만들려면 다음을 수행해야 합니다 [포크 만들기](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) Adobe Experience Platform 설명서 저장소의 를 편집하고 [제공된 설명서 템플릿](./self-service-template.md) 새 분기에서. Adobe 제공 템플릿을 사용하여 새 대상 페이지를 만듭니다. 준비가 되면 가져오기 요청(PR)을 엽니다. 이 작업을 수행하는 지침은 아래의에 자세히 나와 있습니다. [새 대상 페이지를 만드는 단계](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## 설명서 템플릿 {#documentation-template}

설명서 페이지를 만드는 데 도움이 되도록 Adobe에서 [설명서 템플릿](./self-service-template.md) 당신을 위해. 아래에서 템플릿을 편집하고 가져오기 요청을 여는 방법에 대한 지침을 확인할 수 있습니다. Adobe 설명서 팀이 새 대상에 대한 설명서를 검토하고 게시합니다.

[여기에서 템플릿 다운로드](../assets/docs-framework/yourdestination-template.zip) 파일의 압축을 풀고 `yourdestination.md` 파일.

템플릿 을 사용하여 설명서 페이지를 만드는 방법은 아래에 나와 있습니다.

## 새 대상 페이지를 만드는 단계 {#steps-to-create-docs-page}

GitHub 웹 인터페이스 또는 로컬 환경을 사용하여 Adobe Experience Platform의 새 대상에 대한 설명서를 만들 수 있습니다. 아래 링크에서 두 옵션에 대한 지침을 확인하십시오.

* [GitHub 웹 인터페이스를 사용하여 대상 설명서 페이지를 만듭니다](./use-github-interface-to-create-documentation.md)
* [로컬 환경에서 텍스트 편집기를 사용하여 대상 설명서 페이지를 만듭니다](./work-in-local-environment.md)

## 모범 사례 {#best-practices}

리뷰 [작성 모범 사례](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) 대상 설명서 페이지를 만들기 전과 만드는 동안 또한 다음을 읽어야 합니다. [Adobe 설명서 작성 지침 작성](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) Adobe 설명서 팀이 설명서를 작성할 때 사용하는 몇 가지 추가 작성 팁입니다.