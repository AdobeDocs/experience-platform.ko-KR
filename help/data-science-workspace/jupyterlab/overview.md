---
keywords: Experience Platform;JupyterLab;노트북;Data Science Workspace;인기 항목;jupyterlab
solution: Experience Platform
title: JupyterLab UI 개요
description: JupyterLab은 Project Jupyter를 위한 웹 기반 사용자 인터페이스이며 Adobe Experience Platform에 긴밀하게 통합됩니다. 데이터 과학자가 Jupyter Notebooks, 코드 및 데이터를 사용할 수 있는 대화형 개발 환경을 제공합니다. 이 문서에서는 JupyterLab 및 해당 기능에 대한 개요와 일반적인 작업을 수행하는 지침을 제공합니다.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---

# [!DNL JupyterLab] UI 개요

[!DNL JupyterLab] 은 의 웹 기반 사용자 인터페이스입니다. [프로젝트 Jupyter](https://jupyter.org/) 및 는 Adobe Experience Platform에 긴밀하게 통합되어 있습니다. 데이터 과학자가 Jupyter Notebooks, 코드 및 데이터를 사용할 수 있는 대화형 개발 환경을 제공합니다.

이 문서에서는 다음에 대한 개요를 제공합니다. [!DNL JupyterLab] 일반적인 작업을 수행하는 지침뿐만 아니라 그 기능.

## [!DNL JupyterLab] 날짜 [!DNL Experience Platform]

Experience Platform의 JupyterLab 통합은 아키텍처 변경 사항, 디자인 고려 사항, 맞춤형 노트북 확장, 사전 설치된 라이브러리 및 Adobe 테마 인터페이스와 함께 제공됩니다.

다음 목록에서는 Platform의 JupyterLab에 고유한 기능 중 일부를 간략하게 설명합니다.

| 기능 | 설명 |
| --- | --- |
| **커널** | 커널: 노트북 및 기타 제공 [!DNL JupyterLab] 프론트엔드는 다양한 프로그래밍 언어로 코드를 실행하고 검사하는 기능을 제공합니다. [!DNL Experience Platform] 에서 개발을 지원하기 위한 추가 커널 제공 [!DNL Python], R, PySpark 및 [!DNL Spark]. 다음을 참조하십시오. [커널](#kernels) 섹션에 자세히 설명되어 있습니다. |
| **데이터 액세스** | 내에서 직접 기존 데이터 세트에 액세스 [!DNL JupyterLab] 읽기 및 쓰기 기능을 완벽하게 지원합니다. |
| **[!DNL Platform]서비스 통합** | 기본 제공 통합을 사용하면 다른 기능을 활용할 수 있습니다 [!DNL Platform] 내에서 직접 서비스 제공 [!DNL JupyterLab]. 지원되는 통합의 전체 목록은 의 섹션에 제공됩니다. [다른 플랫폼 서비스와 통합](#service-integration). |
| **인증** | 에 더하여 <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab의 내장 보안 모델</a>를 사용하면 Platform Service-to-Service 통신을 포함하여 애플리케이션과 Experience Platform 간의 모든 상호 작용이 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **개발 라이브러리** | 위치 [!DNL Experience Platform], [!DNL JupyterLab] 는 사전 설치된 라이브러리를 제공합니다. [!DNL Python], R 및 PySpark. 다음을 참조하십시오. [부록](#supported-libraries) 지원되는 라이브러리의 전체 목록입니다. |
| **라이브러리 컨트롤러** | 사전 설치된 라이브러리가 사용자의 요구 사항에 맞지 않을 경우 Python 및 R용으로 추가 라이브러리를 설치할 수 있으며, 의 무결성을 유지하기 위해 격리된 컨테이너에 임시로 저장됩니다. [!DNL Platform] 데이터를 안전하게 보호할 수 있습니다. 다음을 참조하십시오. [커널](#kernels) 섹션에 자세히 설명되어 있습니다. |

>[!NOTE]
>
>추가 라이브러리는 라이브러리가 설치된 세션에만 사용할 수 있습니다. 새 세션을 시작할 때 필요한 추가 라이브러리를 다시 설치해야 합니다.

## 다른 항목과 통합 [!DNL Platform] 서비스 {#service-integration}

표준화 및 상호 운용성은 핵심 개념입니다 [!DNL Experience Platform]. 의 통합 [!DNL JupyterLab] 날짜 [!DNL Platform] as a embedded IDE allows it to interact상호 작용 [!DNL Platform] 를 통해 다음을 활용할 수 있습니다. [!DNL Platform] 잠재력을 최대한 발휘할 수 있도록 다음 [!DNL Platform] 다음에서 서비스를 사용할 수 있습니다. [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** 읽기 및 쓰기 기능을 사용하여 데이터 세트에 액세스하고 데이터 세트를 탐색합니다.
* **[!DNL Query Service]:** SQL을 사용하여 데이터 세트에 액세스하고 탐색하므로 대량의 데이터를 처리할 때 데이터 액세스 오버헤드를 줄일 수 있습니다.
* **[!DNL Sensei ML Framework]:** 한 번의 클릭으로 레시피 생성은 물론 데이터를 교육하고 평가할 수 있는 기능을 갖춘 모델 개발입니다.
* **[!DNL Experience Data Model (XDM)]:** 표준화와 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. [경험 데이터 모델(XDM)](https://www.adobe.com/go/xdm-home-en)는 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.

>[!NOTE]
>
>일부 [!DNL Platform] 서비스 통합 [!DNL JupyterLab] 특정 커널로 제한됩니다. 의 섹션을 참조하십시오. [커널](#kernels) 을 참조하십시오.

## 주요 기능 및 공통 작업

의 주요 기능 관련 정보 [!DNL JupyterLab] 및 일반적인 작업 수행에 대한 지침은 아래 섹션에 나와 있습니다.

* [JupyterLab 액세스](#access-jupyterlab)
* [JupyterLab 인터페이스](#jupyterlab-interface)
* [코드 셀](#code-cells)
* [커널](#kernels)
* [커널 세션](#kernel-sessions)
* [런처](#launcher)

### 액세스 [!DNL JupyterLab] {#access-jupyterlab}

위치 [Adobe Experience Platform](https://platform.adobe.com), 선택 **[!UICONTROL 노트북]** 왼쪽 탐색 열에서 참조할 수 있습니다. 다음에 대한 일정 시간 허용: [!DNL JupyterLab] 을(를) 완전히 초기화합니다.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 인터페이스 {#jupyterlab-interface}

다음 [!DNL JupyterLab] 인터페이스는 메뉴 모음, 축소 가능한 왼쪽 사이드바 및 문서 및 활동 탭이 포함된 기본 작업 영역으로 구성됩니다.

**메뉴 바**

인터페이스 맨 위에 있는 메뉴 모음에는 사용 가능한 작업을 표시하는 최상위 메뉴가 있습니다. [!DNL JupyterLab] 키보드 단축키 사용:

* **파일:** 파일 및 디렉터리 관련 작업
* **편집:** 문서 및 기타 활동 편집 관련 작업
* **보기:** 의 모양을 변경하는 작업 [!DNL JupyterLab]
* **실행:** 전자 필기장 및 코드 콘솔과 같은 다른 활동에서 코드를 실행하는 작업
* **커널:** 커널 관리 작업
* **탭:** 열려 있는 문서 및 활동 목록
* **설정:** 일반 설정 및 고급 설정 편집기
* **도움말:** 의 목록 [!DNL JupyterLab] 및 커널 도움말 링크

**왼쪽 사이드바**

왼쪽 사이드바에는 클릭 가능한 탭이 있으며, 이 탭에서는 다음 기능에 액세스할 수 있습니다.

* **파일 브라우저:** 저장된 전자 필기장 문서 및 디렉터리 목록
* **데이터 탐색기:** 데이터 세트 및 스키마 찾아보기, 액세스 및 탐색
* **커널 및 터미널 실행:** 종료 기능이 있는 활성 커널 및 터미널 세션 목록
* **명령:** 유용한 명령 목록
* **셀 관리자:** 프레젠테이션 목적으로 전자 필기장을 설정하는 데 유용한 도구 및 메타데이터에 대한 액세스를 제공하는 셀 편집기
* **탭:** 열려 있는 탭 목록

탭을 선택하여 해당 기능을 노출하거나, 확장된 탭에서 을 선택하여 아래 표시된 대로 왼쪽 사이드바를 축소합니다.

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**주 작업 영역**

의 주요 작업 영역 [!DNL JupyterLab] 문서 및 기타 활동을 크기를 조정하거나 세분화할 수 있는 탭 패널로 정렬할 수 있습니다. 탭을 탭 패널 가운데로 드래그하여 탭을 마이그레이션합니다. 탭을 패널의 왼쪽, 오른쪽, 위쪽 또는 아래쪽으로 드래그하여 패널을 나눕니다.

![](../images/jupyterlab/user-guide/main_work_area.gif)

### 의 GPU 및 메모리 서버 구성 [!DNL Python]/R

위치 [!DNL JupyterLab] 오른쪽 상단 모서리에서 톱니바퀴 아이콘을 선택하여 엽니다. *Notebook 서버 구성*. 슬라이더를 사용하여 GPU를 켜고 필요한 메모리 양을 할당할 수 있습니다. 할당할 수 있는 메모리 양은 조직이 프로비저닝한 양에 따라 다릅니다. 선택 **[!UICONTROL 구성 업데이트]** 저장.

>[!NOTE]
>
>Notebooks의 경우 조직당 하나의 GPU만 제공됩니다. GPU가 사용 중이면 현재 GPU를 예약한 사용자가 릴리스할 때까지 기다려야 합니다. GPU를 로그아웃하거나 4시간 이상 유휴 상태로 두면 됩니다.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### 종료 및 다시 시작 [!DNL JupyterLab]

위치 [!DNL JupyterLab]를 클릭하여 추가 리소스가 사용되지 않도록 세션을 종료할 수 있습니다. 다음을 선택하여 시작 **전원 아이콘** ![전원 아이콘](../images/jupyterlab/user-guide/power_button.png)을 선택한 다음 을 선택합니다. **[!UICONTROL 종료]** 세션을 종료하는 팝오버로 표시됩니다. 12시간 동안 아무 활동이 없으면 노트북 세션이 자동으로 종료됩니다.

다시 시작하려면 [!DNL JupyterLab]를 선택하고 **다시 시작 아이콘** ![다시 시작 아이콘](../images/jupyterlab/user-guide/restart_button.png) 전원 아이콘 바로 왼쪽에 있는 다음 을 선택합니다 **[!UICONTROL 다시 시작]** 표시되는 팝오버에서

![jupyterlab 종료](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### 코드 셀 {#code-cells}

코드 셀은 Notebooks의 기본 콘텐츠입니다. 여기에는 전자 필기장의 관련 커널 언어로 된 소스 코드와 코드 셀 실행의 결과로 출력된 출력이 포함됩니다. 실행 순서를 나타내는 모든 코드 셀의 오른쪽에 실행 횟수가 표시됩니다.

![](../images/jupyterlab/user-guide/code_cell.png)

일반적인 셀 작업은 아래에 설명되어 있습니다.

* **셀 추가:** 더하기 기호(**+**)을 클릭하여 빈 셀을 추가합니다. 새 셀은 현재 상호 작용하고 있는 셀 아래에 배치되거나 특정 셀이 포커스에 있지 않은 경우 수첩의 끝에 배치됩니다.

* **셀 이동:** 이동할 셀의 오른쪽에 커서를 놓은 다음 셀을 클릭하여 새 위치로 끕니다. 또한 한 전자 필기장에서 다른 전자 필기장으로 셀을 이동하면 해당 내용과 함께 셀이 복제됩니다.

* **셀 실행:** 실행하려는 셀의 본문을 클릭한 다음 **play** 아이콘(**▶**)을 클릭하여 제품에서 사용할 수 있습니다. 별표(**\***)은 커널이 실행을 처리할 때 셀의 실행 카운터에 표시되며, 완료시 정수로 대체됩니다.

* **셀 삭제:** 삭제할 셀의 본문을 클릭한 다음 **가위** 아이콘.

### 커널 {#kernels}

노트북 커널은 노트북 셀을 처리하는 언어별 컴퓨팅 엔진입니다. 에 더하여 [!DNL Python], [!DNL JupyterLab] 는 R, PySpark 및 [!DNL Spark] (Scala). 전자 필기장 문서를 열면 연결된 커널이 실행됩니다. 노트북 셀이 실행될 때, 커널은 계산을 수행하고 상당한 CPU 및 메모리 리소스를 소비할 수 있는 결과를 생성한다. 할당된 메모리는 커널을 종료할 때까지 해제되지 않습니다.

특정 기능 및 기능은 아래 표에 설명된 대로 특정 커널로 제한됩니다.

| 커널 | 라이브러리 설치 지원 | [!DNL Platform] 통합 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 예 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 예 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **스칼라** | 아니요 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 커널 세션 {#kernel-sessions}

의 각 활성 노트북 또는 활동 [!DNL JupyterLab] 커널 세션을 활용합니다. 를 확장하면 모든 활성 세션을 찾을 수 있습니다. **터미널과 커널** 왼쪽 사이드바에서 탭으로 이동합니다. 노트북용 커널의 종류와 상태는 노트북 인터페이스의 오른쪽 상단을 관찰하여 확인할 수 있다. 아래 다이어그램에서 노트북의 관련 커널은 **[!DNL Python]3** 그리고 현재 상태는 오른쪽에 회색 원으로 표시됩니다. 속이 빈 원은 공회전 핵을 의미하며, 속이 빈 원은 사용 중인 핵을 의미한다.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

커널이 종료되거나 오랫동안 비활성화되면 **커널 없음!** 단색 원이 있는 이 표시됩니다. 커널 상태를 클릭하고 아래와 같이 적절한 커널 유형을 선택하여 커널을 활성화합니다.

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 런처 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

맞춤화된 *런처* 에서는 다음을 포함하여 작업을 시작하는 데 도움이 되는 지원되는 커널에 유용한 노트북 템플릿을 제공합니다.

| 템플릿 | 설명 |
| --- | --- |
| 빈 | 빈 전자 필기장 파일입니다. |
| 스타터 | 샘플 데이터를 사용하여 데이터 탐색을 보여 주는 미리 채워진 노트북입니다. |
| 소매 판매 | 다음을 포함하는 미리 채워진 노트북 [소매 판매 레시피](../pre-built-recipes/retail-sales.md) 샘플 데이터를 사용합니다. |
| 레시피 빌더 | 에서 레시피를 만들기 위한 전자 필기장 템플릿 [!DNL JupyterLab]. 레시피 작성 과정을 시연하고 설명하는 코드와 주석으로 미리 채워져 있다. 다음을 참조하십시오. [전자 필기장-레시피 튜토리얼](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) 자세한 연습입니다. |
| [!DNL Query Service] | 의 사용을 보여주는 미리 채워진 노트북 [!DNL Query Service] 에서 직접 [!DNL JupyterLab] 는 규모에 맞게 데이터를 분석하는 샘플 워크플로우를 제공합니다. |
| XDM 이벤트 | 데이터 구조 전반에서 공통되는 기능에 초점을 맞춰, 가치 후 경험 이벤트 데이터에 대한 데이터 탐색을 보여 주는 미리 채워진 노트북입니다. |
| XDM 쿼리 | 경험 이벤트 데이터에 대한 샘플 비즈니스 쿼리를 보여 주는 미리 채워진 노트북. |
| 집계 | 대량의 데이터를 더 작고 관리하기 쉬운 청크로 집계하는 샘플 워크플로우를 보여주는 미리 채워진 노트북. |
| 클러스터링 | 클러스터링 알고리즘을 사용한 엔드 투 엔드 머신 러닝 모델링 프로세스를 보여 주는 미리 채워진 노트북입니다. |

일부 노트북 템플릿은 특정 커널로 제한됩니다. 각 커널에 대한 템플릿 가용성은 다음 표에 매핑되어 있습니다.

<table>
    <tr>
        <td></td>
        <th><strong>빈</strong></th>
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
        <td >yes</td>
        <td >yes</td>
        <td >yes</td>
        <td >yes</td>
        <td >yes</td>
        <td >yes</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >yes</td>
        <td >yes</td>
        <td >yes</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 ([!DNL Spark] 2.4)</strong></th>
        <td >아니요</td>
        <td >yes</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >yes</td>
        <td >yes</td>
        <td >아니요</td>
    </tr>
    <tr>
        <th ><strong>스칼라</strong></th>
        <td >yes</td>
        <td >yes</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >아니요</td>
        <td >yes</td>
    </tr>
</table>

새 페이지를 열려면 *런처*, 클릭 **파일 > 새 런처**. 또는 를 확장합니다. **파일 브라우저** 왼쪽 사이드바에서 더하기 기호(**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 다음 단계

지원되는 각 전자 필기장 및 사용 방법에 대한 자세한 내용은 [Jupyterlab 노트북 데이터 액세스](./access-notebook-data.md) 개발자 안내서. 이 안내서에서는 JupyterLab Notebooks를 사용하여 데이터 읽기, 쓰기 및 쿼리를 비롯한 데이터에 액세스하는 방법에 중점을 둡니다. 데이터 액세스 안내서에는 지원되는 각 노트북에서 읽을 수 있는 최대 데이터 양에 대한 정보도 포함되어 있습니다.

## 지원되는 라이브러리 {#supported-libraries}

Python, R 및 PySpark에서 지원되는 패키지 목록의 경우 복사하여 붙여넣기 `!conda list` 새 셀에서 셀을 실행합니다. 지원되는 패키지 목록은 알파벳순으로 채워집니다.

![예](../images/jupyterlab/user-guide/libraries.PNG)

또한 다음 종속성이 사용되지만 나열되지 않습니다.
* CUDA 11.2
* CUDNN 8.1

