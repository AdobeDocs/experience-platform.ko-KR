---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: Git을 사용하여 JupiterLab에서 공동 작업
topic: Tutorial
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---


# Git을 사용하여 JupiterLab에서 공동 작업

Git은 소프트웨어 개발 중에 소스 코드의 변경 사항을 추적할 수 있는 분산 버전 제어 시스템입니다. Git은 데이터 과학 작업 공간 JupiterLab 환경 내에 사전 설치되어 있습니다.

## 전제 조건

>[!NOTE]
> 사용하려는 Git 서버는 인터넷을 통해 액세스할 수 있어야 합니다.

Data Science Workspace JupiterLab 환경은 호스팅 환경이므로 기업 방화벽 내에 배포되지 않으므로 사용자가 연결한 Git 서버는 공용 인터넷에서 액세스할 수 있어야 합니다. 이는 [GitHub의 공용 또는 비공개](https://github.com/) 저장소 또는 직접 호스팅하기로 결정한 Git 서버의 다른 인스턴스가 될 수 있습니다.

## Git을 데이터 과학 작업 공간 JupiterLab 노트북 환경에 연결

먼저 JupiterLabs 노트북 [!DNL Adobe Experience Platform] 환경을 시작하고 [탐색합니다](https://platform.adobe.com/notebooks/jupyterLab) .

JupiterLab 내에서 **[!UICONTROL 파일]** 을 선택한 다음 새로 만들기 위로 **[!UICONTROL 이동합니다]**. 표시되는 드롭다운에서 터미널 **[!UICONTROL 을 선택합니다]**.

![JupiterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

그런 다음 *터미널* 내에서 다음 명령을 사용하여 작업 영역으로 이동합니다. `cd my-workspace`.

![cd 작업 공간](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
> 사용 가능한 git 명령 목록을 보려면 명령을 실행합니다. `git -help` Adobe Target을 사용할 수 있습니다.

그런 다음 명령을 사용하여 사용할 저장소를 `git clone` 복제합니다. 프로젝트가 아니라 `https://` URL을 사용하여 복제됩니다 `ssh://`.

**예**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![복제](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
> 쓰기 작업을 수행하려면(예:)`git push` 새 세션마다 다음 구성 명령을 실행해야 합니다. 또한 모든 푸시 명령은 사용자 이름과 암호를 입력하라는 메시지를 표시합니다.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 다음 단계

저장소 복제를 완료하면 로컬 시스템에서와 마찬가지로 Git을 사용하여 노트북에서 다른 사람과 공동 작업을 할 수 있습니다. JupiterLab에서 수행할 수 있는 작업에 대한 자세한 내용은 [JupiterLab 사용자 안내서를 참조하십시오](./overview.md).
