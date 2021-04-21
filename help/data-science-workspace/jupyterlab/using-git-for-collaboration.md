---
keywords: Experience Platform;JupiterLab;노트북;데이터 과학 작업 영역;인기 있는 주제;Git;Github;Git
solution: Experience Platform
title: Git을 사용하여 JupiterLab에서 공동 작업
topic-legacy: tutorial
type: Tutorial
description: Git은 소프트웨어 개발 중에 소스 코드의 변경 사항을 추적하기 위한 분산 버전 제어 시스템입니다. Git은 데이터 과학 작업 공간 JupiterLab 환경 내에 사전 설치되어 있습니다.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# [!DNL Git]을(를) 사용하여 [!DNL JupyterLab]에서 공동 작업

[!DNL Git] 는 소프트웨어 개발 중에 소스 코드의 변경 사항을 추적하기 위한 분산 버전 제어 시스템입니다. Git은 [!DNL Data Science Workspace JupyterLab] 환경 내에 사전 설치되어 있습니다.

## 전제 조건

>[!NOTE]
>
> 사용하려는 Git 서버를 인터넷을 통해 액세스할 수 있어야 합니다.

[!DNL Data Science Workspace JupyterLab] 환경은 호스팅된 환경이며 회사 방화벽 내에 배포되지 않으므로 연결하는 Git 서버는 공용 인터넷에서 액세스할 수 있어야 합니다. 이것은 [GitHub](https://github.com/)에 있는 공용 또는 비공개 저장소이거나, 자신을 호스팅하기로 결정한 [!DNL Git] 서버의 다른 인스턴스일 수 있습니다.

## [!DNL Git]을(를) [!DNL Data Science Workspace JupyterLab Notebooks] 환경에 연결

[!DNL Adobe Experience Platform]을 시작하고 [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) 환경으로 이동하여 시작합니다.

[!DNL JupyterLab] 내에서 **[!UICONTROL File]**&#x200B;을 선택하고 **[!UICONTROL New]** 위로 마우스를 가져갑니다. 나타나는 드롭다운에서 **[!UICONTROL Terminal]**&#x200B;을 선택합니다.

![JupiterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

다음 명령을 사용하여 *Terminal* 내에서 작업 영역으로 이동합니다.`cd my-workspace`.

![cd 작업 영역](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 사용 가능한 git 명령 목록을 보려면 명령을 실행합니다.터미널 내의 `git -help`.

그런 다음 `git clone` 명령을 사용하여 사용할 저장소를 복제합니다. `ssh://` 대신 `https://` URL을 사용하여 프로젝트를 복제합니다.

**예**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![복제](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 쓰기 작업(`git push` 등)을 수행하려면 새 세션마다 다음 구성 명령을 실행해야 합니다. 또한 모든 푸시 명령은 사용자 이름과 암호를 입력하라는 메시지를 표시합니다.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 다음 단계

저장소 복제를 완료한 후에는 일반적으로 로컬 컴퓨터에서 작업하듯이 Git을 사용하여 노트북에서 다른 사람과 공동 작업할 수 있습니다. [!DNL JupyterLab] 내에서 수행할 수 있는 작업에 대한 자세한 내용은 [[!DNL JupyterLab user guide]](./overview.md)을 참조하십시오.
