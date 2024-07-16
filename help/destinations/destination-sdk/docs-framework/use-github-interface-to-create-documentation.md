---
title: GitHub 웹 인터페이스를 사용하여 대상 설명서 페이지를 만듭니다
description: 이 페이지의 지침은 GitHub 웹 인터페이스를 사용하여 Experience Platform 대상에 대한 설명서 페이지를 작성하고 검토를 위해 제출하는 방법을 보여줍니다.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# GitHub 웹 인터페이스를 사용하여 대상 설명서 페이지를 만듭니다 {#github-interface}

아래 지침은 GitHub 웹 인터페이스를 사용하여 설명서를 작성하고 가져오기 요청(PR)을 제출하는 방법을 보여줍니다. 여기에 표시된 단계를 수행하기 전에 [Adobe Experience Platform 대상에서 대상 문서화](./documentation-instructions.md)를 읽어야 합니다.

>[!TIP]
>
>Adobe의 기여자 안내서에서 지원 설명서를 참조하십시오.
>* [Git 및 Markdown 작성 도구 설치](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [로컬에서 설명서를 위한 Git 리포지토리 설정](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [주요 변경 사항에 대한 GitHub 기여 워크플로](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## GitHub 작성 환경 설정 {#set-up-environment}

1. 브라우저에서 `https://github.com/AdobeDocs/experience-platform.en`(으)로 이동합니다.
2. 리포지토리를 [포크](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository)하려면 아래 표시된 대로 **포크**&#x200B;를 클릭하십시오. 이렇게 하면 고유한 GitHub 계정에 Experience Platform 리포지토리의 사본이 만들어집니다.

   ![Adobe 문서 리포지토리 포크](../assets/docs-framework/ssd-fork-repository.gif)

3. 아래 표시된 대로 리포지토리의 포크에서 프로젝트에 대한 새 분기를 만듭니다. 작업에 이 새 분기를 사용합니다.

   ![새 GitHub 분기 만들기](../assets/docs-framework/new-branch-github.gif)

4. 포크된 리포지토리의 GitHub 폴더 구조에서 `experience-platform.en/help/destinations/catalog/[...]`(으)로 이동합니다. 여기서 `[...]`은(는) 대상에 대해 원하는 범주입니다. 예를 들어 Experience Platform에 개인화 대상을 추가하는 경우 `personalization` 범주를 선택합니다. **파일 추가 > 새 파일 만들기**&#x200B;를 선택합니다.

   ![새 파일 추가](../assets/docs-framework/github-navigate-and-create-file.gif)

5. 대상 이름을 `YOURDESTINATION.md`로 지정합니다. 여기서 YOURDESTINATION은 Adobe Experience Platform의 대상 이름입니다. 예를 들어 회사의 이름이 Moviestar이면 파일 이름을 `moviestar.md`로 지정합니다.

## 대상의 설명서 페이지 작성 {#author-documentation}

1. [설명서 셀프 서비스 템플릿](./self-service-template.md)을(를) 기반으로 대상 페이지의 콘텐츠를 만듭니다. **[템플릿을 다운로드](../assets/docs-framework/yourdestination-template.zip)**&#x200B;한 다음 압축을 해제하여 `.md` 파일 템플릿을 추출합니다.
2. [dillinger.io](https://dillinger.io/)과 같은 온라인 Markdown 편집기에서 대상에 대한 관련 정보가 있는 템플릿의 콘텐츠를 붙여 넣고 편집합니다. 무엇을 채워야 하고 어떤 단락을 제거할 수 있는지에 대한 자세한 내용은 템플릿의 지침을 따르십시오.

   >[!TIP]
   >
   >언제든지 브라우저 창을 닫고 나중에 다시 열 수 있습니다. 작업이 자동으로 저장되며 브라우저를 다시 열 때 기다리고 있습니다.
3. Markdown 편집기의 콘텐츠를 GitHub의 새 파일에 복사합니다.
4. 사용할 스크린샷이나 이미지의 경우 GitHub 인터페이스를 사용하여 `experience-platform.en/help/destinations/assets/catalog/[...]`에 파일을 업로드하십시오. 여기서 `[...]`은(는) 대상에 대해 원하는 범주입니다. 예를 들어 Experience Platform에 개인화 대상을 추가하는 경우 `personalization` 범주를 선택합니다. 작성 중인 페이지의 이미지에 연결해야 합니다. [이미지에 연결하는 방법 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images)을 참조하세요.

   ![GitHub에 이미지 업로드](../assets/docs-framework/upload-image.gif)

5. 준비가 되면 파일을 분기에 저장합니다.

![파일 만들기 확인](../assets/docs-framework/ssd-confirm-file-creation.png)

## 검토를 위해 설명서 제출 {#submit-review}

>[!TIP]
>
>여기서 깰 수 있는 것은 아무것도 없습니다. 이 섹션의 지침에 따라 설명서 업데이트를 제안하면 됩니다. 제안된 업데이트는 Adobe Experience Platform 설명서 팀에서 승인하거나 편집합니다.

1. 파일을 저장하고 원하는 이미지를 업로드한 후 끌어오기 요청(PR)을 열어 작업 분기를 Adobe 설명서 저장소의 마스터 분기로 병합할 수 있습니다. 작업한 분기가 선택되어 있는지 확인하고 **Contribute > 가져오기 요청 열기**&#x200B;를 선택합니다.

![끌어오기 요청 만들기](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. 기본 및 비교 분기가 올바른지 확인하십시오. PR에 업데이트를 설명하는 메모를 추가하고 **끌어오기 요청 만들기**&#x200B;를 선택합니다. 포크의 작업 분기를 Adobe 저장소의 마스터 분기로 병합하는 PR이 열립니다.

   >[!TIP]
   >
   >Adobe 설명서 팀이 PR을 편집할 수 있도록 **유지 관리자가 편집 허용** 확인란을 선택한 상태로 두십시오.

   ![Adobe 문서 리포지토리에 끌어오기 요청 만들기](../assets/docs-framework/ssd-create-pull-request-2.png)

1. 이때 Adobe 기여자 라이선스 계약(CLA)에 서명하라는 메시지가 표시됩니다. 필수 단계입니다. CLA에 서명한 후 PR 페이지를 새로 고치고 끌어오기 요청을 제출합니다.

1. `https://github.com/AdobeDocs/experience-platform.en`의 **끌어오기 요청** 탭을 검사하여 끌어오기 요청이 제출되었는지 확인할 수 있습니다.

   ![PR 성공](../assets/docs-framework/ssd-pr-successful.png)

1. 감사합니다. Adobe 설명서 팀은 편집이 필요한 경우 PR에 연락하여 설명서가 게시되는 시기를 알려 줍니다.

>[!TIP]
>
>설명서에 이미지 및 링크를 추가하고 Markdown에 대한 기타 질문이 있는 경우 Adobe의 공동 작성 안내서에서 [Markdown 사용](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html)을 읽어 보십시오.
