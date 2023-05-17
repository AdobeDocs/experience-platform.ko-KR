---
title: GitHub 웹 인터페이스를 사용하여 대상 설명서 페이지를 만듭니다
description: 이 페이지의 지침은 GitHub 웹 인터페이스를 사용하여 Experience Platform 대상에 대한 설명서 페이지를 작성 및 검토를 위해 제출하는 방법을 보여줍니다.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 1%

---

# GitHub 웹 인터페이스를 사용하여 대상 설명서 페이지를 만듭니다 {#github-interface}

아래 지침은 GitHub 웹 인터페이스를 사용하여 설명서를 작성하고 가져오기 요청(PR)을 제출하는 방법을 보여줍니다. 여기에 표시된 단계를 살펴보려면 다음을 참조하십시오 [Adobe Experience Platform 대상에서 대상 문서화](./documentation-instructions.md).

>[!TIP]
>
>Adobe 기여자 안내서의 지원 설명서를 참조하십시오.
>* [Git 및 Markdown 작성 도구 설치](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [로컬로 설명서를 위한 Git 리포지토리 설정](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [주요 변경 사항에 대한 GitHub 기여 워크플로](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## GitHub 작성 환경 설정 {#set-up-environment}

1. 브라우저에서 `https://github.com/AdobeDocs/experience-platform.en`.
2. 종료 [포크](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) 저장소에서 **포크** 아래와 같이 표시됩니다. 이렇게 하면 고유한 GitHub 계정에 Experience Platform 리포지토리의 복사본이 만들어집니다.

   ![포크 Adobe 설명서 저장소](../assets/docs-framework/ssd-fork-repository.gif)

3. 리포지토리의 포크에서 아래 표시된 대로 프로젝트에 대한 새 분기를 만듭니다. 이 새 분기를 너의 일에 사용해라.

   ![새 GitHub 분기 만들기](../assets/docs-framework/new-branch-github.gif)

4. 포크된 리포지토리의 GitHub 폴더 구조에서 다음 위치로 이동합니다. `experience-platform.en/help/destinations/catalog/[...]`, 위치 `[...]` 는 대상에 대해 원하는 카테고리입니다. 예를 들어 개인화 대상을 Experience Platform에 추가하는 경우 `personalization` 카테고리. 선택 **파일 추가 > 새 파일 만들기**.

   ![새 파일 추가](../assets/docs-framework/github-navigate-and-create-file.gif)

5. 대상에 이름을 지정합니다 `YOURDESTINATION.md`: 여기서 대상은 Adobe Experience Platform에 있는 대상의 이름입니다. 예를 들어 회사가 Moviestar라고 하는 경우 파일의 이름을 지정합니다 `moviestar.md`.

## 대상에 대한 설명서 페이지 작성 {#author-documentation}

1. 를 기반으로 대상 페이지의 컨텐츠를 작성합니다 [설명서 셀프 서비스 템플릿](./self-service-template.md). **[다운로드](../assets/docs-framework/yourdestination-template.zip)** 템플릿을 추출하고 압축을 푼 후에 `.md` 파일 템플릿.
2. 템플릿 컨텐츠를 다음과 같이 온라인 Markdown 편집기에서 대상에 대한 관련 정보로 붙여넣고 편집합니다 [dillinger.io](https://dillinger.io/). 입력해야 할 내용과 제거할 수 있는 단락에 대한 자세한 내용은 템플릿의 지침을 따르십시오.

   >[!TIP]
   >
   >언제든지 브라우저 창을 닫고 나중에 다시 열 수 있습니다. 작업이 자동으로 저장되며 브라우저를 다시 열 때 대기합니다.
3. Markdown 편집기의 컨텐츠를 GitHub의 새 파일에 복사합니다.
4. 사용할 스크린샷 또는 이미지의 경우 GitHub 인터페이스를 사용하여 파일을 `experience-platform.en/help/destinations/assets/catalog/[...]`, 위치 `[...]` 는 대상에 대해 원하는 카테고리입니다. 예를 들어 개인화 대상을 Experience Platform에 추가하는 경우 `personalization` 카테고리. 작성 중인 페이지의 이미지에 연결해야 합니다. 자세한 내용은 [이미지에 연결하는 방법 지침](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![GitHub에 이미지 업로드](../assets/docs-framework/upload-image.gif)

5. 준비가 되면 분기에 파일을 저장합니다.

![파일 만들기 확인](../assets/docs-framework/ssd-confirm-file-creation.png)

## 검토할 설명서 제출 {#submit-review}

>[!TIP]
>
>여기서 벗어날 수 있는 것은 아무것도 없습니다. 이 섹션의 지침에 따라 설명서 업데이트를 제안하는 것입니다. 제안된 업데이트는 Adobe Experience Platform 설명서 팀이 승인하거나 편집합니다.

1. 파일을 저장하고 원하는 이미지를 업로드한 후 끌어오기 요청(PR)을 열어 작업 분기를 Adobe 설명서 저장소의 마스터 분기에 병합할 수 있습니다. 작업한 분기가 선택되어 있는지 확인하고 를 선택합니다 **Contribute > 끌어오기 요청 열기**.

![가져오기 요청 만들기](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. 기본 및 비교 분기가 올바른지 확인합니다. PR에 업데이트를 설명하는 메모를 추가하고 을(를) 선택합니다 **가져오기 요청 만들기**. 이렇게 하면 포크의 작업 분기를 Adobe 저장소의 마스터 분기에 병합하는 PR이 열립니다.

   >[!TIP]
   >
   >을(를) 종료하십시오. **유지 관리자의 편집 허용** Adobe 설명서 팀이 PR을 편집할 수 있도록 확인란을 선택했습니다.

   ![문서 저장소로 가져오기 요청 만들기](../assets/docs-framework/ssd-create-pull-request-2.png)

1. 이때 Adobe 기여자 라이선스 계약(CLA)에 서명하라는 알림이 표시됩니다. 이것은 필수 단계입니다. CLA에 로그인한 후 PR 페이지를 새로 고침하고 가져오기 요청을 제출합니다.

1. 를 검사하여 끌어오기 요청이 제출되었는지 확인할 수 있습니다. **끌어오기 요청** 탭 `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR 성공](../assets/docs-framework/ssd-pr-successful.png)

1. 감사합니다. Adobe 설명서 팀은 편집이 필요한 경우 PR에서 연락하여 설명서가 언제 게시되는지 알려줍니다.

>[!TIP]
>
>설명서 및 Markdown에 대한 기타 질문에 대한 이미지 및 링크를 추가하려면 다음을 참조하십시오 [Markdown 사용](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) Adobe의 공동 작성 사용 안내서에서.
