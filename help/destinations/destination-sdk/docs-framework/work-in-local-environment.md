---
title: 로컬 환경에서 텍스트 편집기를 사용하여 대상 설명서 페이지를 만듭니다
description: 이 페이지의 지침은 텍스트 편집기를 사용하여 로컬 환경에서 작업하여 Experience Platform 대상에 대한 설명서 페이지를 작성하고 검토를 위해 제출하는 방법을 보여줍니다.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# 로컬 환경에서 텍스트 편집기를 사용하여 대상 설명서 페이지를 만듭니다 {#local-authoring}

이 페이지의 지침은 로컬 환경에서 텍스트 편집기를 사용하여 설명서를 작성하고 가져오기 요청(PR)을 제출하는 방법을 보여줍니다. 여기에 표시된 단계를 수행하기 전에 [Adobe Experience Platform 대상에서 대상 문서화](./documentation-instructions.md)를 읽어야 합니다.

>[!TIP]
>
>Adobe의 기여자 안내서에서 지원 설명서를 참조하십시오.
>* [Git 및 Markdown 작성 도구 설치](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=ko)
>* [로컬에서 설명서를 위한 Git 리포지토리 설정](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=ko)
>* [주요 변경 사항에 대한 GitHub 기여 워크플로](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=ko).

## GitHub에 연결하고 로컬 작성 환경 설정 {#set-up-environment}

1. 브라우저에서 `https://github.com/AdobeDocs/experience-platform.en`(으)로 이동합니다.
2. 리포지토리를 [포크](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=ko#fork-the-repository)하려면 아래 표시된 대로 **포크**&#x200B;를 클릭하십시오. 이렇게 하면 자체 GitHub 계정에 Experience Platform 저장소의 복사본이 만들어집니다.

   ![Adobe 문서 리포지토리 포크](../assets/docs-framework/ssd-fork-repository.gif)

3. 로컬 컴퓨터에 저장소를 복제합니다. 아래와 같이 **코드 > HTTPS > GitHub Desktop으로 열기**&#x200B;를 선택합니다. [GitHub Desktop](https://desktop.github.com/)이 설치되어 있는지 확인하십시오. 자세한 내용은 Adobe 기여자 안내서에서 [저장소의 로컬 복제 만들기](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=ko#create-a-local-clone-of-the-repository)를 참조하십시오.

   ![로컬 환경에 Adobe 설명서 리포지토리 복제](../assets/docs-framework/clone-local.png)

4. 로컬 파일 구조에서 `experience-platform.en/help/destinations/catalog/[...]`(으)로 이동합니다. 여기서 `[...]`은(는) 대상에 대해 원하는 범주입니다. 예를 들어 Experience Platform에 개인화 대상을 추가하는 경우 `personalization` 폴더를 선택합니다.

## 대상의 설명서 페이지 작성 {#author-documentation}

1. 설명서 페이지는 [셀프서비스 대상 템플릿](../docs-framework/self-service-template.md)을(를) 기반으로 합니다. [대상 템플릿](../assets/docs-framework/yourdestination-template.zip)을(를) 다운로드합니다. 압축을 풀고 위의 4단계에서 언급된 디렉터리에 `yourdestination-template.md` 파일을 추출합니다.  `YOURDESTINATION.md` 파일의 이름을 바꾸십시오. 여기서 YOURDESTINATION은 Adobe Experience Platform의 대상 이름입니다. 예를 들어 회사의 이름이 Moviestar이면 파일 이름을 `moviestar.md`로 지정합니다.
2. [선택한 텍스트 편집기](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=ko#understand-markdown-editors)에서 새 파일을 엽니다. Adobe에서는 [Visual Studio Code](https://code.visualstudio.com/)을 사용하고 Adobe Markdown 작성 확장을 설치하는 것이 좋습니다. 확장을 설치하려면 Visual Studio Code를 열고 화면 왼쪽의 **[!DNL Extensions]** 탭을 선택한 다음 `adobe markdown authoring`을(를) 검색합니다. 확장을 선택하고 **[!DNL Install]**&#x200B;을(를) 클릭합니다.
   ![Adobe Markdown 작성 확장 설치](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. 대상에 대한 관련 정보로 템플릿을 편집합니다. 템플릿의 지침을 따릅니다.
4. 설명서에 추가할 스크린샷이나 이미지를 보려면 `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`(으)로 이동하십시오. 여기서 `[...]`은(는) 대상에 대해 원하는 범주입니다. 예를 들어 Experience Platform에 개인화 대상을 추가하는 경우 `personalization` 폴더를 선택합니다. 대상에 대한 새 폴더를 만들고 여기에 이미지를 저장합니다. 작성 중인 페이지에서 해당 페이지에 연결해야 합니다. [이미지에 연결하는 방법 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=ko#link-to-images)을 참조하세요.
5. 준비가 되면 작업 중인 파일을 저장합니다.

## 검토를 위해 설명서 제출 {#submit-review}

>[!TIP]
>
>여기서 깰 수 있는 것은 아무것도 없습니다. 이 섹션의 지침에 따라 설명서 업데이트를 제안하면 됩니다. 제안된 업데이트는 Adobe Experience Platform 설명서 팀에서 승인하거나 편집합니다.

1. GitHub Desktop에서 업데이트에 대한 작업 분기를 만들고 **분기 게시**&#x200B;를 선택하여 분기를 GitHub에 게시합니다.

![새 분기 로컬](../assets/docs-framework/new-branch-local.gif)

1. GitHub Desktop에서 아래와 같이 작업을 [커밋](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit)합니다.

   ![로컬 커밋](../assets/docs-framework/commit-local.png)

1. GitHub Desktop에서 아래와 같이 작업을 [remote](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) 분기로 [푸시](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push)합니다.

   ![커밋 푸시](../assets/docs-framework/push-local-to-remote.png)

1. GitHub 웹 인터페이스에서 가져오기 요청(PR)을 열어 작업 분기를 Adobe 문서 저장소의 마스터 분기로 병합합니다. 작업한 분기가 선택되어 있는지 확인하고 **참여 > 가져오기 요청 열기**&#x200B;를 선택합니다.

   ![끌어오기 요청 만들기](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. 기본 및 비교 분기가 올바른지 확인하십시오. PR에 업데이트를 설명하는 메모를 추가하고 **끌어오기 요청 만들기**&#x200B;를 선택합니다. 포크의 작업 분기를 Adobe 저장소의 마스터 분기로 병합하기 위한 PR이 열립니다.

   >[!TIP]
   >
   >Adobe 설명서 팀이 PR을 편집할 수 있도록 **유지 관리자가 편집 허용** 확인란을 선택한 상태로 두십시오.

   ![Adobe 설명서 리포지토리에 끌어오기 요청 만들기](../assets/docs-framework/ssd-create-pull-request-2.png)

1. 이때 Adobe 기여자 라이선스 계약(CLA)에 서명하라는 메시지가 표시됩니다. 필수 단계입니다. CLA에 서명한 후 PR 페이지를 새로 고치고 끌어오기 요청을 제출합니다.

1. `https://github.com/AdobeDocs/experience-platform.en`의 **끌어오기 요청** 탭을 검사하여 끌어오기 요청이 제출되었는지 확인할 수 있습니다.

![PR 성공](../assets/docs-framework/ssd-pr-successful.png)

1. 감사합니다. 편집이 필요한 경우 Adobe 설명서 팀이 PR에 연락하여 설명서가 게시되는 시기를 알려줍니다.

>[!TIP]
>
>설명서에 이미지와 링크를 추가하고 Markdown에 대한 기타 질문이 있는 경우 Adobe의 공동 작업 쓰기 안내서에서 [Markdown 사용](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=ko)을 읽어 보십시오.
