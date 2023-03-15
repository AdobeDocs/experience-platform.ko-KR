---
keywords: Experience Platform;JupyterLab;노트북;Data Science Workspace;인기 항목;Git;Github
solution: Experience Platform
title: Git을 사용하여 JupyterLab에서 공동 작업
type: Tutorial
description: Git은 소프트웨어 개발 중 소스 코드의 변경 사항을 추적하기 위한 배포된 버전 제어 시스템입니다. Git은 Data Science Workspace JupyterLab 환경 내에 사전 설치됩니다.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# 에서 공동 작업 [!DNL JupyterLab] 사용 [!DNL Git]

[!DNL Git] 는 소프트웨어 개발 중 소스 코드의 변경 사항을 추적하기 위한 분산 버전 제어 시스템입니다. Git이 [!DNL Data Science Workspace JupyterLab] 환경.

## 전제 조건

>[!NOTE]
>
> 사용하려는 Git 서버는 인터넷을 통해 액세스할 수 있어야 합니다.

다음 [!DNL Data Science Workspace JupyterLab] 환경은 호스팅 환경이며 회사 방화벽 내에 배포되지 않으므로 연결하는 Git 서버는 공용 인터넷에서 액세스할 수 있어야 합니다. 의 공용 또는 개인 저장소일 수 있습니다. [GitHub](https://github.com/) 또는 다른 인스턴스 [!DNL Git] 직접 호스팅하기로 결정한 서버입니다.

## 연결 [!DNL Git] (으)로 [!DNL Data Science Workspace JupyterLab Notebooks] 환경

실행으로 시작 [!DNL Adobe Experience Platform] 및 로 이동 [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) 환경.

다음 범위 내 [!DNL JupyterLab], 선택 **[!UICONTROL 파일]** 그런 다음 마우스를 위에 놓음 **[!UICONTROL 신규]**. 표시되는 드롭다운에서 을 선택합니다 **[!UICONTROL 터미널]**.

![JupyterLab 탐색](../images/jupyterlab/tutorials/open-terminal.png)

다음, 내 *터미널* 다음 명령을 사용하여 작업 공간으로 이동합니다. `cd my-workspace`.

![작업 영역](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 사용 가능한 git 명령 목록을 보려면 명령을 실행합니다. `git -help` 을 참조하십시오.

그런 다음 를 사용하여 사용할 저장소를 복제합니다. `git clone` 명령입니다. 을(를) 사용하여 프로젝트 복제 `https://` 대신 URL `ssh://`.

**예**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![복제](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 쓰기 작업을 수행하려면(`git push` (예:) 모든 새 세션에 대해 다음 구성 명령을 실행해야 합니다. 또한 푸시 명령은 사용자 이름과 암호를 묻는 메시지를 표시합니다.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 다음 단계

저장소 복제를 완료한 후에는 로컬 컴퓨터에서 일반적인 방법으로 Git을 사용하여 노트북의 다른 사용자와 공동 작업을 수행할 수 있습니다. 내에서 수행할 수 있는 작업에 대한 자세한 정보 [!DNL JupyterLab], 다음을 참조하십시오. [[!DNL JupyterLab user guide]](./overview.md).
