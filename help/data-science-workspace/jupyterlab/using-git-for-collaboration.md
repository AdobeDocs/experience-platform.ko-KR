---
keywords: Experience Platform;JupyterLab;노트북;Data Science Workspace;인기 항목;Git;Github
solution: Experience Platform
title: Git을 사용하여 JupyterLab에서 공동 작업
type: Tutorial
description: Git은 소프트웨어 개발 중 소스 코드의 변경 사항을 추적하기 위한 분산 버전 제어 시스템입니다. Git은 데이터 과학 Workspace JupyterLab 환경 내에 사전 설치됩니다.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# [!DNL Git]을(를) 사용하여 [!DNL JupyterLab]에서 공동 작업

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

[!DNL Git]은(는) 소프트웨어 개발 중 소스 코드의 변경 내용을 추적하기 위한 분산 버전 제어 시스템입니다. Git이 [!DNL Data Science Workspace JupyterLab] 환경 내에 미리 설치되어 있습니다.

## 전제 조건

>[!NOTE]
>
> 사용하려는 Git 서버는 인터넷을 통해 액세스할 수 있어야 합니다.

[!DNL Data Science Workspace JupyterLab] 환경은 호스팅 환경이며 회사 방화벽 내에 배포되지 않으므로 연결하는 Git 서버는 공용 인터넷에서 액세스할 수 있어야 합니다. [GitHub](https://github.com/)의 공용 또는 개인 리포지토리 또는 직접 호스팅하기로 한 [!DNL Git] 서버의 다른 인스턴스일 수 있습니다.

## [!DNL Git]을(를) [!DNL Data Science Workspace JupyterLab Notebooks] 환경에 연결

환경을 시작하고 [!DNL Adobe Experience Platform] [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) 탐색하여 시작.

[!DNL JupyterLab] 내에서 **[!UICONTROL 파일]**&#x200B;을 선택한 다음 **[!UICONTROL 새로 만들기]** 위로 마우스를 가져갑니다. 표시되는 드롭다운에서 **[!UICONTROL 터미널]**&#x200B;을 선택합니다.

![JupyterLab 탐색](../images/jupyterlab/tutorials/open-terminal.png)

*터미널* 내에서 `cd my-workspace` 명령을 사용하여 작업 영역으로 이동합니다.

![cd 작업 영역](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 사용 가능한 git 명령 목록을 보려면 터미널 내에서 `git -help` 명령을 실행하십시오.

그런 다음 `git clone` 명령을 사용하여 사용할 저장소를 복제합니다. `ssh://`이(가) 아닌 `https://` URL을 사용하여 프로젝트를 복제합니다.

**예**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![복제](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 쓰기 작업(`git push` 예: )을 수행하려면 모든 새 세션에 대해 다음 컨피그레이션 명령을 실행해야 합니다. 또한 푸시 명령은 사용자 이름과 암호를 묻는 메시지를 표시합니다.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 다음 단계

저장소 복제를 완료한 후에는 로컬 컴퓨터에서 일반적인 방법으로 Git을 사용하여 노트북의 다른 사용자와 공동 작업을 수행할 수 있습니다. [!DNL JupyterLab]에서 수행할 수 있는 작업에 대한 자세한 내용은 [[!DNL JupyterLab user guide]](./overview.md)을(를) 참조하십시오.
