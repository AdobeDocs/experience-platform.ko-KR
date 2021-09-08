---
title: 로컬 환경에서 텍스트 편집기를 사용하여 대상 설명서 페이지를 만듭니다
seo-title: Use a text editor in your local environment to create a destination documentation page
description: 이 페이지의 지침은 로컬 환경에서 텍스트 편집기를 사용하여 설명서를 작성하고 끌어오기 요청을 제출하는 방법을 보여줍니다.
seo-description: The instructions on this page show you how to use a text editor to work in your local environment to author documentation and submit a pull request.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e1e7d2f70c032d02f96b3999e4fca736070c6ca9
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 3%

---

# 로컬 환경에서 텍스트 편집기를 사용하여 대상 설명서 페이지를 만듭니다 {#local-authoring}

이 페이지의 지침은 로컬 환경에서 텍스트 편집기를 사용하여 설명서를 작성하고 끌어오기 요청(PR)을 제출하는 방법을 보여줍니다. 여기에 표시된 단계를 진행하려면 먼저 [Adobe Experience Platform 대상에서 대상 문서화](./documentation-instructions.md)를 읽어야 합니다.

>[!TIP]
>
>Adobe 기여자 안내서의 지원 설명서를 참조하십시오.
>* [Git 및 Markdown 작성 도구 설치](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [로컬로 설명서를 위한 Git 리포지토리 설정](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [주요 변경 사항에 대한 GitHub 기여 워크플로우](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## GitHub에 연결하고 로컬 작성 환경을 설정합니다 {#set-up-environment}

1. 브라우저에서 `https://github.com/AdobeDocs/experience-platform.en`(으)로 이동합니다.
2. 리포지토리를 [포크](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository)하려면 스크린샷에 표시된 대로 **포크**&#x200B;를 클릭합니다.

   ![포크 Adobe 설명서 저장소](./assets/ssd-fork-repo.png)

3. 로컬 컴퓨터에 리포지토리 복제. 아래 표시된 대로 **코드 > HTTPS > GitHub Desktop에서 열기**&#x200B;를 선택합니다. [GitHub Desktop](https://desktop.github.com/)이 설치되어 있는지 확인합니다. 자세한 내용은 Adobe 기여자 안내서에서 [리포지토리의 로컬 복제 만들기](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository)를 참조하십시오.

   ![로컬 환경에 Adobe 설명서 리포지토리 복제](./assets/clone-local.png)

4. 로컬 파일 구조에서 `experience-platform.en/help/destinations/catalog/[...]` 로 이동합니다. 여기서 `[...]` 은 대상에 대해 원하는 카테고리입니다. 예를 들어 개인화 대상을 Experience Platform에 추가하는 경우 `personalization` 폴더를 선택합니다.

## 대상에 대한 설명서 페이지 작성 {#author-documentation}

1. 설명서 페이지는 [셀프 서비스 대상 템플릿](./self-service-template.md)을 기반으로 합니다. [대상 템플릿](assets/yourdestination-template.zip)을 다운로드하십시오. 압축을 풀고 파일 `yourdestination-template.md` 을 위의 4단계에서 언급한 디렉토리에 추출합니다.  파일 이름을 `YOURDESTINATION.md` 로 바꾸십시오. 여기서 YOURDESTINATION은 Adobe Experience Platform의 대상 이름입니다. 예를 들어 회사가 Moviestar라고 하는 경우 파일의 이름을 `moviestar.md`로 지정합니다.
2. [선택 사항 텍스트 편집기에서 새 파일을 엽니다](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). Adobe은 [Visual Studio 코드](https://code.visualstudio.com/)를 사용하고 Adobe Markdown 작성 확장을 설치하는 것을 권장합니다. 확장을 설치하려면 Visual Studio 코드를 열고 화면 왼쪽에서 **[!DNL Extensions]** 탭을 선택하고 `adobe markdown authoring`을 검색합니다. 확장을 선택하고 **[!DNL Install]** 을 클릭합니다.
   ![Adobe Markdown 작성 확장 설치](./assets/install-adobe-markdown-extension.gif)
3. 대상에 대한 관련 정보로 템플릿을 편집합니다. 템플릿의 지침을 따릅니다.
4. 설명서에 추가할 스크린샷 또는 이미지의 경우 `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`으로 이동하십시오. 여기서 `[...]`는 대상에 대해 원하는 카테고리입니다. 예를 들어 개인화 대상을 Experience Platform에 추가하는 경우 `personalization` 폴더를 선택합니다. 대상에 대한 새 폴더를 만들고 이미지를 여기에 저장합니다. 작성 중인 페이지에서 해당 페이지에 연결해야 합니다. [이미지에 연결하는 방법 지침을 참조하십시오](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. 준비가 되면 작업 중인 파일을 저장합니다.

## 검토할 설명서 제출 {#submit-review}

1. GitHub Desktop에서 업데이트에 대한 작업 분기를 만들고 **분기 게시**&#x200B;를 선택하여 분기를 GitHub에 게시합니다.

![새 분기 로컬](./assets/new-branch-local.gif)

1. GitHub Desktop에서 아래 표시된 대로 [작업을 커밋합니다](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit).

   ![로컬 커밋](./assets/commit-local.png)

1. GitHub Desktop에서 작업을 [push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push)원격](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) 분기로 아래와 같이 푸시합니다.[

   ![커밋 푸시](./assets/push-local-to-remote.png)

1. GitHub 웹 인터페이스에서 끌어오기 요청(PR)을 열어 작업 분기를 Adobe 설명서 저장소의 마스터 분기에 병합합니다. 작업한 분기가 선택되어 있는지 확인하고 **가져오기 요청**&#x200B;을 선택합니다.

   ![가져오기 요청 만들기](./assets/ssd-create-pull-request-1.png)

1. 기본 및 비교 분기가 올바른지 확인합니다. 업데이트를 설명하는 PR에 메모를 추가하고 **끌어오기 요청 만들기**&#x200B;를 선택합니다. 이렇게 하면 포크의 작업 분기를 Adobe 저장소의 마스터 분기에 병합하는 PR이 열립니다.
   >[!TIP]
   >
   >Adobe 설명서 팀이 PR을 편집할 수 있도록 **유지 관리자가 편집 허용** 확인란을 선택한 상태로 둡니다.

   ![문서 저장소로 가져오기 요청 만들기](./assets/ssd-create-pull-request-2.png)

1. 이때 Adobe 기여자 라이선스 계약(CLA)에 서명하라는 알림이 표시됩니다. 이것은 필수 단계입니다. CLA에 로그인한 후 PR 페이지를 새로 고침하고 가져오기 요청을 제출합니다.

1. `https://github.com/AdobeDocs/experience-platform.en`에서 **끌어오기 요청** 탭을 검사하여 끌어오기 요청이 제출되었는지 확인할 수 있습니다.

![PR 성공](./assets/ssd-pr-successful.png)

1. 감사합니다. Adobe 설명서 팀은 편집이 필요한 경우 PR에서 연락하여 설명서가 언제 게시되는지 알려줍니다.

>[!TIP]
>
>이미지 및 링크를 설명서에 추가하고, Markdown과 관련된 다른 질문에 대한 자세한 내용은 Adobe의 공동 작업 작성 안내서에서 [Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) 사용 을 참조하십시오.
