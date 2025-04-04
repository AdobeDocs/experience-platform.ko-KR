---
keywords: Experience Platform;JupyterLab;노트북;Data Science Workspace;인기 주제;jupyterlab
solution: Experience Platform
title: JupyterLab UI 개요
description: JupyterLab은 Project Jupyter를 위한 웹 기반 사용자 인터페이스이며 Adobe Experience Platform에 긴밀하게 통합됩니다. 데이터 과학자가 Jupyter Notebooks, 코드 및 데이터를 사용할 수 있는 대화형 개발 환경을 제공합니다. 이 문서에서는 JupyterLab 및 해당 기능에 대한 개요와 일반적인 작업을 수행하는 지침을 제공합니다.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1838'
ht-degree: 2%

---

# [!DNL JupyterLab] UI 개요

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

[!DNL JupyterLab]은(는) [Project Jupyter](https://jupyter.org/)용 웹 기반 사용자 인터페이스이며 Adobe Experience Platform에 긴밀하게 통합되어 있습니다. 데이터 과학자가 Jupyter Notebooks, 코드 및 데이터를 사용할 수 있는 대화형 개발 환경을 제공합니다.

이 문서에서는 [!DNL JupyterLab] 및 해당 기능에 대한 개요와 일반적인 작업을 수행하는 지침을 제공합니다.

## [!DNL Experience Platform]의 [!DNL JupyterLab]

Experience Platform의 JupyterLab 통합은 아키텍처 변경 사항, 디자인 고려 사항, 맞춤형 노트북 확장, 사전 설치된 라이브러리 및 Adobe 테마 인터페이스와 함께 제공됩니다.

다음 목록에서는 Experience Platform에서 JupyterLab에 고유한 기능 중 일부를 간략하게 설명합니다.

| 기능 | 설명 |
| --- | --- |
| **커널** | 커널은 전자 필기장과 다른 [!DNL JupyterLab] 프런트 엔드에서 다양한 프로그래밍 언어로 코드를 실행하고 검사하는 기능을 제공합니다. [!DNL Experience Platform]은(는) [!DNL Python], R, PySpark 및 [!DNL Spark]에서 개발을 지원하는 추가 커널을 제공합니다. 자세한 내용은 [커널](#kernels) 섹션을 참조하십시오. |
| **데이터 액세스** | 읽기 및 쓰기 기능을 완벽하게 지원하므로 [!DNL JupyterLab] 내에서 기존 데이터 세트에 직접 액세스할 수 있습니다. |
| **[!DNL Experience Platform]서비스 통합** | 기본 제공 통합을 사용하면 [!DNL JupyterLab] 내에서 직접 다른 [!DNL Experience Platform] 서비스를 활용할 수 있습니다. 지원되는 통합의 전체 목록은 [다른 Experience Platform 서비스와 통합](#service-integration) 섹션에 나와 있습니다. |
| **인증** | <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab의 기본 제공 보안 모델</a> 외에도 Experience Platform 서비스 간 통신을 포함하여 애플리케이션과 Experience Platform 간의 모든 상호 작용은 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System](IMS)</a>을(를) 통해 암호화되고 인증됩니다. |
| **개발 라이브러리** | [!DNL Experience Platform]에서 [!DNL JupyterLab]은(는) [!DNL Python], R 및 PySpark에 사전 설치된 라이브러리를 제공합니다. 지원되는 라이브러리의 전체 목록은 [부록](#supported-libraries)을 참조하십시오. |
| **라이브러리 컨트롤러** | 미리 설치된 라이브러리가 사용자의 요구 사항에 맞지 않으면 Python 및 R용으로 추가 라이브러리를 설치할 수 있으며, [!DNL Experience Platform]의 무결성을 유지하고 데이터를 안전하게 유지하기 위해 격리된 컨테이너에 임시로 저장됩니다. 자세한 내용은 [커널](#kernels) 섹션을 참조하십시오. |

>[!NOTE]
>
>추가 라이브러리는 라이브러리가 설치된 세션에만 사용할 수 있습니다. 새 세션을 시작할 때 필요한 추가 라이브러리를 다시 설치해야 합니다.

## 다른 [!DNL Experience Platform] 서비스와 통합 {#service-integration}

표준화 및 상호 운용성은 [!DNL Experience Platform]의 핵심 개념입니다. [!DNL Experience Platform]에 포함된 IDE로 [!DNL JupyterLab]을(를) 통합하면 다른 [!DNL Experience Platform] 서비스와 상호 작용할 수 있으므로 [!DNL Experience Platform]을(를) 최대한 활용할 수 있습니다. [!DNL JupyterLab]에서 다음 [!DNL Experience Platform]개의 서비스를 사용할 수 있습니다.

* **[!DNL Catalog Service]:** 읽기 및 쓰기 기능을 사용하여 데이터 세트에 액세스하고 데이터 세트를 탐색합니다.
* **[!DNL Query Service]:** SQL을 사용하여 데이터 세트에 액세스하고 탐색하므로 대량의 데이터를 처리할 때 데이터 액세스 오버헤드가 줄어듭니다.
* 한 번의 클릭으로 레시피를 만들 수 있을 뿐만 아니라 데이터를 교육하고 평가할 수 있는 기능을 갖춘 **[!DNL Sensei ML Framework]:** 모델 개발.
* **[!DNL Experience Data Model (XDM)]:** 표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. Adobe을 기반으로 하는 [XDM(경험 데이터 모델)](https://www.adobe.com/go/xdm-home-en)은(는) 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.

>[!NOTE]
>
>[!DNL JupyterLab]의 일부 [!DNL Experience Platform] 서비스 통합이 특정 커널로 제한됩니다. 자세한 내용은 [커널](#kernels)의 섹션을 참조하십시오.

## 주요 기능 및 공통 작업

[!DNL JupyterLab]의 주요 기능에 대한 정보 및 일반적인 작업 수행에 대한 지침은 아래 섹션에 나와 있습니다.

* [JupyterLab 액세스](#access-jupyterlab)
* [JupyterLab 인터페이스](#jupyterlab-interface)
* [코드 셀](#code-cells)
* [커널](#kernels)
* [커널 세션](#kernel-sessions)
* [런처](#launcher)

### [!DNL JupyterLab] 액세스 {#access-jupyterlab}

[Adobe Experience Platform](https://platform.adobe.com)의 왼쪽 탐색 열에서 **[!UICONTROL 전자 필기장]**&#x200B;을 선택합니다. [!DNL JupyterLab]이(가) 완전히 초기화될 때까지 잠시 기다립니다.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 인터페이스 {#jupyterlab-interface}

[!DNL JupyterLab] 인터페이스는 메뉴 모음, 축소 가능한 왼쪽 사이드바 및 문서 및 활동 탭이 포함된 기본 작업 영역으로 구성됩니다.

**메뉴 모음**

인터페이스 맨 위에 있는 메뉴 모음에는 [!DNL JupyterLab]에서 사용할 수 있는 작업을 키보드 단축키로 표시하는 최상위 메뉴가 있습니다.

* **파일:** 파일 및 디렉터리 관련 작업
* **편집:** 문서 및 기타 활동 편집과 관련된 작업
* [!DNL JupyterLab]의 모양을 변경하는 **보기:** 동작
* **실행:** 전자 필기장 및 코드 콘솔과 같은 다른 활동에서 코드를 실행하기 위한 작업
* **커널:** 커널 관리를 위한 작업
* **탭:** 열려 있는 문서 및 활동 목록입니다.
* **설정:** 일반 설정 및 고급 설정 편집기
* **도움말:** [!DNL JupyterLab] 및 커널 도움말 링크 목록

**왼쪽 사이드바**

왼쪽 사이드바에는 클릭 가능한 탭이 있으며, 이 탭에서는 다음 기능에 액세스할 수 있습니다.

* **파일 브라우저:** 저장된 전자 필기장 문서 및 디렉터리 목록
* **데이터 탐색기:** 데이터 세트와 스키마를 검색, 액세스 및 탐색
* **커널 및 터미널 실행 중:** 종료 기능이 있는 활성 커널 및 터미널 세션 목록
* **명령:** 유용한 명령 목록
* **셀 검사기:** 프레젠테이션 목적으로 전자 필기장을 설정하는 데 유용한 도구 및 메타데이터에 액세스할 수 있는 셀 편집기입니다
* **탭:** 열려 있는 탭 목록입니다.

탭을 선택하여 해당 기능을 노출하거나, 확장된 탭에서 을 선택하여 아래 표시된 대로 왼쪽 사이드바를 축소합니다.

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**기본 작업 영역**

[!DNL JupyterLab]의 기본 작업 영역을 사용하면 문서 및 기타 활동을 크기 조정 또는 세분화할 수 있는 탭 패널로 정렬할 수 있습니다. 탭을 탭 패널 가운데로 드래그하여 탭을 마이그레이션합니다. 탭을 패널의 왼쪽, 오른쪽, 위쪽 또는 아래쪽으로 드래그하여 패널을 나눕니다.

![](../images/jupyterlab/user-guide/main_work_area.gif)

### [!DNL Python]/R의 GPU 및 메모리 서버 구성

[!DNL JupyterLab]에서 오른쪽 상단 모서리의 톱니바퀴 아이콘을 선택하여 *Notebook 서버 구성*&#x200B;을 엽니다. 슬라이더를 사용하여 GPU를 켜고 필요한 메모리 양을 할당할 수 있습니다. 할당할 수 있는 메모리 양은 조직이 프로비저닝한 양에 따라 다릅니다. **[!UICONTROL 구성 업데이트]**&#x200B;를 선택하여 저장합니다.

>[!NOTE]
>
>Notebooks의 경우 조직당 하나의 GPU만 제공됩니다. GPU가 사용 중이면 현재 GPU를 예약한 사용자가 릴리스할 때까지 기다려야 합니다. GPU를 로그아웃하거나 4시간 이상 유휴 상태로 두면 됩니다.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### [!DNL JupyterLab] 종료 및 다시 시작

[!DNL JupyterLab]에서 세션을 종료하여 추가 리소스가 사용되지 않도록 할 수 있습니다. 먼저 **전원 아이콘** ![전원 아이콘](/help/images/icons/power.png)을 선택한 다음 세션을 종료하는 팝오버에서 **[!UICONTROL 시스템 종료]**&#x200B;를 선택하십시오. 12시간 동안 아무 활동이 없으면 노트북 세션이 자동으로 종료됩니다.

[!DNL JupyterLab]을(를) 다시 시작하려면 전원 아이콘 왼쪽에 있는 **다시 시작 아이콘** ![다시 시작 아이콘](/help/images/icons/restart.png)을(를) 선택한 다음 표시되는 팝오버에서 **[!UICONTROL 다시 시작]**&#x200B;을(를) 선택하십시오.

![jupyterlab 종료](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### 코드 셀 {#code-cells}

코드 셀은 Notebooks의 기본 콘텐츠입니다. 여기에는 전자 필기장의 관련 커널 언어로 된 소스 코드와 코드 셀 실행의 결과로 출력된 출력이 포함됩니다. 실행 순서를 나타내는 모든 코드 셀의 오른쪽에 실행 횟수가 표시됩니다.

![](../images/jupyterlab/user-guide/code_cell.png)

일반적인 셀 작업은 아래에 설명되어 있습니다.

* **셀 추가:** 전자 필기장 메뉴에서 더하기 기호(**+**)를 클릭하여 빈 셀을 추가합니다. 새 셀은 현재 상호 작용하고 있는 셀 아래에 배치되거나 특정 셀이 포커스에 있지 않은 경우 수첩의 끝에 배치됩니다.

* **셀 이동:** 이동할 셀의 오른쪽에 커서를 놓은 다음 셀을 클릭하여 새 위치로 끕니다. 또한 한 전자 필기장에서 다른 전자 필기장으로 셀을 이동하면 해당 내용과 함께 셀이 복제됩니다.

* **셀 실행:** 실행하려는 셀의 본문을 클릭한 다음 전자 필기장 메뉴에서 **재생** 아이콘(**▶**)을 클릭합니다. 커널이 실행을 처리할 때 별표(**\***)가 셀의 실행 카운터에 표시되며 완료 시 정수로 대체됩니다.

* **셀 삭제:** 삭제할 셀의 본문을 클릭한 다음 **가위** 아이콘을 클릭합니다.

### 커널 {#kernels}

노트북 커널은 노트북 셀을 처리하는 언어별 컴퓨팅 엔진입니다. [!DNL JupyterLab]은(는) [!DNL Python] 외에도 R, PySpark 및 [!DNL Spark]&#x200B;(Scala)에서 추가 언어 지원을 제공합니다. 전자 필기장 문서를 열면 연결된 커널이 실행됩니다. 노트북 셀이 실행될 때, 커널은 계산을 수행하고 상당한 CPU 및 메모리 리소스를 소비할 수 있는 결과를 생성한다. 할당된 메모리는 커널을 종료할 때까지 해제되지 않습니다.

특정 기능 및 기능은 아래 표에 설명된 대로 특정 커널로 제한됩니다.

| 커널 | 라이브러리 설치 지원 | [!DNL Experience Platform] 통합 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 예 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 예 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **크기 조절** | 아니요 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 커널 세션 {#kernel-sessions}

[!DNL JupyterLab]의 각 활성 전자 필기장 또는 활동이 커널 세션을 사용합니다. 왼쪽 사이드바에서 **터미널 및 커널 실행** 탭을 확장하면 모든 활성 세션을 찾을 수 있습니다. 노트북용 커널의 종류와 상태는 노트북 인터페이스의 오른쪽 상단을 관찰하여 확인할 수 있다. 아래 다이어그램에서 전자 필기장의 연결된 커널은 **[!DNL Python]3**&#x200B;이고 현재 상태는 오른쪽에 회색 원으로 표시됩니다. 속이 빈 원은 공회전 핵을 의미하며, 속이 빈 원은 사용 중인 핵을 의미한다.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

커널이 종료되거나 오랫동안 사용되지 않으면 **커널이 없습니다!단색 원이 있는**&#x200B;이(가) 표시됩니다. 커널 상태를 클릭하고 아래와 같이 적절한 커널 유형을 선택하여 커널을 활성화합니다.

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 런처 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

사용자 지정된 *런처*&#x200B;는 다음을 포함하여 작업을 시작하는 데 도움이 되는 지원되는 커널에 대한 유용한 전자 필기장 서식 파일을 제공합니다.

| 템플릿 | 설명 |
| --- | --- |
| 비어 있음 | 빈 전자 필기장 파일입니다. |
| 스타터 | 샘플 데이터를 사용하여 데이터 탐색을 보여 주는 미리 채워진 노트북입니다. |
| 소매 판매 | 샘플 데이터를 사용하여 [소매 판매 레시피](../pre-built-recipes/retail-sales.md)를 제공하는 미리 채워진 전자 필기장입니다. |
| 레시피 빌더 | [!DNL JupyterLab]에서 레시피를 만들기 위한 전자 필기장 템플릿입니다. 레시피 작성 과정을 시연하고 설명하는 코드와 주석으로 미리 채워져 있다. 자세한 연습은 [레시피 튜토리얼 자습서](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en)를 참조하세요. |
| [!DNL Query Service] | 규모에 맞게 데이터를 분석하는 샘플 워크플로우를 제공하는 [!DNL JupyterLab]에서 직접 [!DNL Query Service]의 사용을 보여 주는 미리 채워진 전자 필기장입니다. |
| XDM 이벤트 | 데이터 구조 전반에서 공통되는 기능에 초점을 맞춰, 가치 후 경험 이벤트 데이터에 대한 데이터 탐색을 보여 주는 미리 채워진 노트북입니다. |
| XDM 쿼리 | 경험 이벤트 데이터에 대한 샘플 비즈니스 쿼리를 보여 주는 미리 채워진 노트북. |
| 집계 | 대량의 데이터를 더 작고 관리하기 쉬운 청크로 집계하는 샘플 워크플로우를 보여주는 미리 채워진 노트북. |
| 클러스터링 | 클러스터링 알고리즘을 사용한 엔드 투 엔드 머신 러닝 모델링 프로세스를 보여 주는 미리 채워진 노트북입니다. |

일부 노트북 템플릿은 특정 커널로 제한됩니다. 각 커널에 대한 템플릿 가용성은 다음 표에 매핑되어 있습니다.

<table>
    <tr>
        <td></td>
        <th><strong>비어 있음</strong></th>
        <th><strong>스타터</strong></th>
        <th><strong>소매 판매</strong></th>
        <th><strong>레시피 빌더</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>XDM 이벤트</strong></th>
        <th><strong>XDM 쿼리</strong></th>
        <th><strong>집계</strong></th>
        <th><strong>클러스터링</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
        <td >예</td>
        <td >예</td>
        <td >예</td>
        <td >예</td>
        <td >예</td>
        <td >예</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >예</td>
        <td >예</td>
        <td >예</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3([!DNL Spark] 2.4)</strong></th>
        <td >아니요</td>
        <td >예</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >예</td>
        <td >예</td>
        <td >아니요</td>
    </tr>
    <tr>
        <th ><strong>스칼라</strong></th>
        <td >예</td>
        <td >예</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >예</td>
    </tr>
</table>

새 *런처*&#x200B;를 열려면 **파일 > 새 런처**&#x200B;을 클릭하세요. 또는 왼쪽 사이드바에서 **파일 브라우저**&#x200B;를 확장하고 더하기 기호(**+**)를 클릭합니다.

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 다음 단계

지원되는 각 전자 필기장과 사용 방법에 대한 자세한 내용은 [Jupyterlab 전자 필기장 데이터 액세스](./access-notebook-data.md) 개발자 안내서를 참조하세요. 이 안내서에서는 JupyterLab Notebooks를 사용하여 데이터 읽기, 쓰기 및 쿼리를 비롯한 데이터에 액세스하는 방법에 중점을 둡니다. 데이터 액세스 안내서에는 지원되는 각 노트북에서 읽을 수 있는 최대 데이터 양에 대한 정보도 포함되어 있습니다.

## 지원되는 라이브러리 {#supported-libraries}

Python, R 및 PySpark에서 지원되는 패키지 목록을 보려면 새 셀에 `!conda list`을(를) 복사하여 붙여 넣은 다음 셀을 실행하십시오. 지원되는 패키지 목록은 알파벳순으로 채워집니다.

![예](../images/jupyterlab/user-guide/libraries.PNG)

또한 다음 종속성이 사용되지만 나열되지 않습니다.
* CUDA 11.2
* CUDNN 8.1

