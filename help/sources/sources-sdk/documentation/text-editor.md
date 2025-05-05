---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: 로컬 환경에서 텍스트 편집기를 사용하여 소스 설명서 페이지를 만듭니다
description: 이 문서는 로컬 환경을 사용하여 소스에 대한 설명서를 작성하고 가져오기 요청(PR)을 제출하는 방법에 대한 단계를 제공합니다.
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# 로컬 환경에서 텍스트 편집기를 사용하여 소스 설명서 페이지를 만듭니다

이 문서는 로컬 환경을 사용하여 소스에 대한 설명서를 작성하고 가져오기 요청(PR)을 제출하는 방법에 대한 단계를 제공합니다.

>[!TIP]
>
>Adobe 기여 안내서의 다음 문서를 사용하여 설명서 프로세스를 추가로 지원할 수 있습니다. <ul><li>[Git 및 Markdown 작성 도구 설치](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=ko)</li><li>[로컬에서 설명서를 위한 Git 리포지토리 설정](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=ko)</li><li>[주요 변경 사항에 대한 GitHub 기여 워크플로](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=ko)</li></ul>

## 전제 조건

다음 자습서를 사용하려면 로컬 컴퓨터에 GitHub Desktop이 설치되어 있어야 합니다. GitHub Desktop이 없는 경우 응용 프로그램을 [여기](https://desktop.github.com/)에서 다운로드할 수 있습니다.

## GitHub에 연결하고 로컬 작성 환경 설정

로컬 작성 환경을 설정하는 첫 번째 단계는 [Adobe Experience Platform GitHub 저장소](https://github.com/AdobeDocs/experience-platform.en)로 이동하는 것입니다.

![platform-repo](../assets/platform-repo.png)

Experience Platform GitHub 리포지토리의 기본 페이지에서 **포크**&#x200B;를 선택합니다.

![포크](../assets/fork.png)

로컬 컴퓨터에 리포지토리를 복제하려면 **코드**&#x200B;을(를) 선택하십시오. 표시되는 드롭다운 메뉴에서 **HTTPS**&#x200B;을(를) 선택한 다음 **GitHub Desktop으로 열기**&#x200B;를 선택합니다.

>[!TIP]
>
>자세한 내용은 [로컬에서 설명서를 위한 Git 리포지토리 설정](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=ko#create-a-local-clone-of-the-repository)에 대한 자습서를 참조하십시오.

![git-desktop 열기](../assets/open-git-desktop.png)

그런 다음 GitHub Desktop이 `experience-platform.en` 리포지토리를 복제할 수 있도록 잠시 기다려 주십시오.

![복제](../assets/cloning.png)

복제 프로세스가 완료되면 GitHub Desktop으로 이동하여 새 분기를 만듭니다. 위쪽 탐색에서 **기본**&#x200B;을 선택한 다음 **새 분기**&#x200B;를 선택합니다.

![새 분기](../assets/new-branch.png)

표시되는 팝오버 패널에서 분기의 수사적 이름을 입력한 다음 **분기 만들기**&#x200B;를 선택합니다.

![create-branch-vs](../assets/create-branch-vs.png)

그런 다음 **분기 게시**&#x200B;를 선택합니다.

![publish-branch](../assets/publish-branch.png)

## 소스에 대한 설명서 페이지 작성

로컬 컴퓨터에 복제된 저장소와 새 분기가 생성되면 이제 [선택한 텍스트 편집기](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=ko#understand-markdown-editors)를 통해 새 소스에 대한 설명서 페이지 작성을 시작할 수 있습니다.

Adobe에서는 [Visual Studio Code](https://code.visualstudio.com/)을 사용하고 Adobe Markdown 작성 확장을 설치하는 것이 좋습니다. 확장을 설치하려면 Visual Studio Code를 시작한 다음 왼쪽 탐색에서 **확장** 탭을 선택합니다.

![확장](../assets/extension.png)

검색 창에 `Adobe Markdown Authoring`을(를) 입력한 다음 나타나는 페이지에서 **설치**&#x200B;를 선택합니다.

![설치](../assets/install.png)

로컬 컴퓨터가 준비된 상태에서 [소스 설명서 템플릿](../assets/api-template.zip)을(를) 다운로드하고 선택한 범주를 나타내는 [`...`]을(를) 사용하여 `experience-platform.en/help/sources/tutorials/api/create/...`에 파일을 추출합니다. 예를 들어 데이터베이스 소스를 만드는 경우 데이터베이스 폴더를 선택합니다.

마지막으로 템플릿에 요약된 지침에 따라 소스와 관련된 관련 정보로 템플릿을 편집합니다.

![edit-template](../assets/edit-template.png)

## 검토를 위해 설명서 제출

끌어오기 요청(PR)을 만들고 검토할 문서를 제출하려면 먼저 [!DNL Visual Studio Code]&#x200B;(또는 선택한 텍스트 편집기)에 작업을 저장하십시오. 그런 다음 GitHub Desktop을 사용하여 커밋 메시지를 입력하고 **Commit to create-source-documentation**&#x200B;을(를) 선택합니다.

![커밋 대](../assets/commit-vs.png)

그런 다음 **원본 푸시**&#x200B;를 선택하여 작업을 원격 분기에 업로드합니다.

![푸시 원본](../assets/push-origin.png)

끌어오기 요청을 만들려면 **끌어오기 요청 만들기**&#x200B;를 선택합니다.

![create-pr-vs](../assets/create-pr-vs.png)

기준 및 비교 분기가 올바른지 확인합니다. PR에 업데이트를 설명하는 메모를 추가한 다음 **끌어오기 요청 만들기**&#x200B;를 선택합니다. 이렇게 하면 작업의 작업 분기를 Adobe 저장소의 마스터 분기로 병합하기 위한 PR이 열립니다.

>[!TIP]
>
>Adobe 설명서 팀이 PR을 편집할 수 있도록 **유지 관리자가 편집 허용** 확인란을 선택한 상태로 두십시오.

![create-pr](../assets/create-pr.png)

https://github.com/AdobeDocs/experience-platform.en에서 가져오기 요청 탭을 검사하여 가져오기 요청이 제출되었는지 확인할 수 있습니다.

![confirm-pr](../assets/confirm-pr.png)
