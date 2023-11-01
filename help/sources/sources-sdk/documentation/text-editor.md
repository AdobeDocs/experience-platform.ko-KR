---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: 로컬 환경에서 텍스트 편집기를 사용하여 소스 설명서 페이지를 만듭니다
description: 이 문서는 로컬 환경을 사용하여 소스에 대한 설명서를 작성하고 가져오기 요청(PR)을 제출하는 방법에 대한 단계를 제공합니다.
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 3%

---

# 로컬 환경에서 텍스트 편집기를 사용하여 소스 설명서 페이지를 만듭니다

이 문서는 로컬 환경을 사용하여 소스에 대한 설명서를 작성하고 가져오기 요청(PR)을 제출하는 방법에 대한 단계를 제공합니다.

>[!TIP]
>
>Adobe 기여 안내서의 다음 문서를 사용하여 설명서 프로세스를 추가로 지원할 수 있습니다. <ul><li>[Git 및 Markdown 작성 도구 설치](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[로컬로 설명서를 위한 Git 리포지토리 설정](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[주요 변경 사항에 대한 GitHub 기여 워크플로](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## 전제 조건

다음 자습서를 사용하려면 로컬 컴퓨터에 GitHub Desktop이 설치되어 있어야 합니다. GitHub Desktop이 없는 경우 애플리케이션을 다운로드할 수 있습니다 [여기](https://desktop.github.com/).

## GitHub에 연결하고 로컬 작성 환경 설정

로컬 작성 환경을 설정하는 첫 번째 단계는 [Adobe Experience Platform GitHub 저장소](https://github.com/AdobeDocs/experience-platform.en).

![플랫폼 리포지토리](../assets/platform-repo.png)

Platform GitHub 저장소의 기본 페이지에서 을 선택합니다. **포크**.

![포크](../assets/fork.png)

로컬 컴퓨터에 저장소를 복제하려면 **코드**. 표시되는 드롭다운 메뉴에서 을(를) 선택합니다 **HTTPS** 그런 다음 을 선택합니다. **GitHub Desktop으로 열기**.

>[!TIP]
>
>자세한 내용은 다음 자습서를 참조하십시오. [로컬에서 설명서를 위한 Git 리포지토리 설정](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

그런 다음 GitHub Desktop이 `experience-platform.en` 리포지토리.

![클로닝](../assets/cloning.png)

복제 프로세스가 완료되면 GitHub Desktop으로 이동하여 새 분기를 만듭니다. 선택 **기본** 위쪽 탐색에서 를 선택하고 **새 분기**

![새 분기](../assets/new-branch.png)

표시되는 팝오버 패널에서 분기의 수사적 이름을 입력한 다음 을 선택합니다 **분기 만들기**.

![create-branch-vs](../assets/create-branch-vs.png)

그런 다음 을 선택합니다. **분기 게시**.

![publish-분기](../assets/publish-branch.png)

## 소스에 대한 설명서 페이지 작성

로컬 시스템에 복제된 저장소와 새 분기가 생성되면 이제 를 통해 새 소스에 대한 설명서 페이지 작성을 시작할 수 있습니다. [선택한 텍스트 편집기](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors).

Adobe은 다음을 권장합니다. [Visual Studio 코드](https://code.visualstudio.com/) Adobe Markdown 작성 확장을 설치하는 방법을 설명합니다. 확장을 설치하려면 Visual Studio Code를 시작한 다음 **확장** 왼쪽 탐색에서 탭으로 이동합니다.

![확장](../assets/extension.png)

그런 다음 을 입력합니다. `Adobe Markdown Authoring` 검색 창에서 을 선택한 다음 을 선택합니다. **설치** 표시되는 페이지에서 참조할 수 있습니다.

![설치](../assets/install.png)

로컬 컴퓨터가 준비된 상태에서 [소스 설명서 템플릿](../assets/api-template.zip) 및 파일 추출 대상 `experience-platform.en/help/sources/tutorials/api/create/...` 포함 [`...`] 선택한 카테고리를 나타냅니다. 예를 들어 데이터베이스 소스를 만드는 경우 데이터베이스 폴더를 선택합니다.

마지막으로 템플릿에 요약된 지침에 따라 소스와 관련된 관련 정보로 템플릿을 편집합니다.

![edit-template](../assets/edit-template.png)

## 검토를 위해 설명서 제출

가져오기 요청(PR)을 만들고 검토하기 위해 설명서를 제출하려면 먼저 작업 내용을 다음에 저장하십시오. [!DNL Visual Studio Code] (또는 선택한 텍스트 편집기). 그런 다음 GitHub Desktop을 사용하여 커밋 메시지를 입력하고 다음을 선택합니다. **create-source-documentation에 커밋**.

![commit-vs](../assets/commit-vs.png)

그런 다음 을 선택합니다. **푸시 원본** 원격 분기에 작업을 업로드합니다.

![push-origin](../assets/push-origin.png)

끌어오기 요청을 만들려면 다음을 선택합니다. **가져오기 요청 만들기**.

![create-pr-vs](../assets/create-pr-vs.png)

기준 및 비교 분기가 올바른지 확인합니다. PR에 업데이트를 설명하는 메모를 추가한 다음 을 선택합니다 **가져오기 요청 만들기**. 그러면 작업의 작업 분기를 Adobe 저장소의 마스터 분기로 병합하는 PR이 열립니다.

>[!TIP]
>
>나가기 **유지 관리자의 편집 허용** Adobe 설명서 팀이 PR을 편집할 수 있도록 확인란을 선택했습니다.

![create-pr](../assets/create-pr.png)

https://github.com/AdobeDocs/experience-platform.en에서 가져오기 요청 탭을 검사하여 가져오기 요청이 제출되었는지 확인할 수 있습니다.

![confirm-pr](../assets/confirm-pr.png)
