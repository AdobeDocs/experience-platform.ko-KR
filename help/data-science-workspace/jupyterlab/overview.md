---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: JupiterLab 사용 안내서
topic: Overview
description: JupiterLab은 Project Jupiter를 위한 웹 기반의 유저 인터페이스로 Adobe Experience Platform과 긴밀하게 통합되어 있습니다. 데이터 과학자들이 Jupiter 노트북, 코드 및 데이터를 사용하여 작업할 수 있는 인터랙티브한 개발 환경을 제공합니다. 이 문서에서는 JupiterLab 및 그 기능에 대한 개요와 일반적인 작업 수행 지침을 제공합니다.
translation-type: tm+mt
source-git-commit: d5e7679ac41fd476c77a98920d7f7aeaefacec6d
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 9%

---


# [!DNL JupyterLab] 사용 안내서

[!DNL JupyterLab] 는 [프로젝트 주피터를 위한 웹 기반의 유저](https://jupyter.org/) 인터페이스로 Adobe Experience Platform과 긴밀하게 통합되어 있습니다. 데이터 과학자들이 Jupiter 노트북, 코드 및 데이터를 사용하여 작업할 수 있는 인터랙티브한 개발 환경을 제공합니다.

이 문서에서는 일반적인 작업 [!DNL JupyterLab] 을 수행하기 위한 지침뿐만 아니라 기능과 기능에 대한 개요를 제공합니다.

## [!DNL JupyterLab] on [!DNL Experience Platform]

Experience Platform의 JupiterLab과의 통합은 아키텍처 변경 사항, 디자인 고려 사항, 맞춤형 노트북 익스텐션, 사전 설치된 라이브러리 및 Adobe 테마 인터페이스와 함께 제공됩니다.

다음 목록은 Platform의 JupiterLab에만 고유한 일부 기능에 대해 간략하게 설명합니다.

| 기능 | 설명 |
| --- | --- |
| **커널** | 커널 기능을 사용하면 노트북 및 기타 [!DNL JupyterLab] 프런트 엔드가 다른 프로그래밍 언어로 코드를 실행하고 검사할 수 있습니다. [!DNL Experience Platform] 는 R, PySpark 및 InDesign Server의 개발 지원을 위한 추가 커널을 [!DNL Python]제공합니다 [!DNL Spark]. 자세한 내용은 [커널](#kernels) 섹션을 참조하십시오. |
| **데이터 액세스** | 읽기 및 쓰기 기능에 대한 완벽한 지원을 통해 기존 데이터 세트 [!DNL JupyterLab] 에 직접 액세스할 수 있습니다. |
| **[!DNL Platform]서비스 통합** | 통합 기능을 사용하면 내부에서 바로 다른 [!DNL Platform] 서비스를 이용할 수 있습니다 [!DNL JupyterLab]. 지원되는 통합에 대한 전체 목록은 다른 플랫폼 서비스와의 [통합 섹션에 나와 있습니다](#service-integration). |
| **인증** | JupiterLab <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">의 내장된 보안 모델</a>외에도 플랫폼 서비스 간 커뮤니케이션을 비롯한 애플리케이션과 Experience Platform 간의 모든 상호 작용은 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)를 통해 암호화되어 인증됩니다</a>. |
| **개발 라이브러리** | 에서 [!DNL Experience Platform]는 PySpark용 사전 설치된 라이브러리 [!DNL JupyterLab] [!DNL Python]를 제공합니다. 지원되는 라이브러리의 전체 [목록은 부록을](#supported-libraries) 참조하십시오. |
| **라이브러리 컨트롤러** | 사전 설치된 라이브러리가 사용자의 요구 사항에 맞지 않을 경우 Python 및 R용으로 추가 라이브러리를 설치할 수 있으며, 격리된 컨테이너에 임시로 저장하여 데이터의 무결성을 유지하고 데이터를 안전하게 유지할 수 [!DNL Platform] 있습니다. 자세한 내용은 [커널](#kernels) 섹션을 참조하십시오. |

>[!NOTE]
>
>추가 라이브러리는 설치된 세션에서만 사용할 수 있습니다. 새 세션을 시작할 때 필요한 추가 라이브러리를 다시 설치해야 합니다.

## 다른 [!DNL Platform] 서비스와 통합 {#service-integration}

표준화와 상호 운용성은 그 이면의 핵심 개념입니다 [!DNL Experience Platform]. 내장된 IDE로 [!DNL JupyterLab] 를 통합하면 다른 [!DNL Platform] 서비스와 인터랙션할 수 있으므로 모든 가능성을 활용할 [!DNL Platform] [!DNL Platform] 수 있습니다. 다음 [!DNL Platform] 서비스를 사용할 수 있습니다 [!DNL JupyterLab].

* **[!DNL Catalog Service]:** 읽기 및 쓰기 기능을 사용하여 데이터 세트에 액세스하고 탐색할 수 있습니다.
* **[!DNL Query Service]:** SQL을 사용하여 데이터 세트에 액세스하고 탐색할 수 있으므로 대량의 데이터를 처리할 때 낮은 데이터 액세스 오버헤드를 제공할 수 있습니다.
* **[!DNL Sensei ML Framework]:** 한 번의 클릭으로 레서피 제작뿐만 아니라 데이터 트레이닝 및 점수 측정 기능을 사용하여 개발 모델을 모델링할 수 있습니다.
* **[!DNL Experience Data Model (XDM)]:** 표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. [Adobe 기반의 XDM(Experience Data Model)](https://www.adobe.com/go/xdm-home-en)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

>[!NOTE]
>
>일부 [!DNL Platform] 서비스 통합 [!DNL JupyterLab] 은 특정 커널로 제한됩니다. 자세한 내용은 [커널의](#kernels) 섹션을 참조하십시오.

## 주요 기능 및 일반 작업

일반적인 작업 수행의 주요 기능 [!DNL JupyterLab] 및 지침에 대한 정보는 아래 섹션에 나와 있습니다.

* [Access JupiterLab](#access-jupyterlab)
* [JupiterLab 인터페이스](#jupyterlab-interface)
* [코드 셀](#code-cells)
* [커널](#kernels)
* [커널 세션](#kernel-sessions)
* [론처](#launcher)

### 액세스 [!DNL JupyterLab] {#access-jupyterlab}

[Adobe Experience Platform](https://platform.adobe.com)의 왼쪽 탐색 **열에서 전자 필기장** 을 선택합니다. 완전히 초기화하는 데 약간의 시간 [!DNL JupyterLab] 이 소요됩니다.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 인터페이스 {#jupyterlab-interface}

이 [!DNL JupyterLab] 인터페이스는 메뉴 막대, 축소 가능한 왼쪽 사이드바, 문서와 활동의 탭이 포함된 기본 작업 영역으로 구성됩니다.

**메뉴 막대**

인터페이스 맨 위에 있는 메뉴 모음에는 키보드 단축키와 함께 사용할 수 있는 작업을 표시하는 최상위 메뉴 [!DNL JupyterLab] 가 있습니다.

* **파일:** 파일 및 디렉토리와 관련된 작업
* **편집:** 문서 및 기타 활동 편집 관련 작업
* **보기:** Action that alter the appearance of [!DNL JupyterLab]
* **실행:** 전자 필기장 및 코드 콘솔과 같은 다양한 활동에서 코드를 실행하기 위한 작업
* **커널:** 커널 관리를 위한 작업
* **탭:** 열려 있는 문서 및 활동 목록
* **설정:** 일반 설정 및 고급 설정 편집기
* **도움말:** 커널 도움말 [!DNL JupyterLab] 링크 목록

**왼쪽 세로 막대**

왼쪽 사이드바는 다음 기능에 대한 액세스를 제공하는 클릭 가능한 탭을 포함합니다.

* **파일 브라우저:** 저장된 노트북 문서 및 디렉토리 목록
* **데이터 탐색기:** 데이터 세트 및 스키마 검색, 액세스 및 탐색
* **커널 및 터미널 실행:** 종료 가능한 활성 커널 및 터미널 세션 목록
* **명령:** 유용한 명령 목록
* **셀 관리자:** 프레젠테이션용으로 전자 필기장을 설정하는 데 유용한 도구 및 메타데이터에 액세스할 수 있는 셀 편집기
* **탭:** 열려 있는 탭 목록

탭을 클릭하여 해당 기능을 표시하거나 확장된 탭을 클릭하여 아래 표시된 대로 왼쪽 사이드바를 축소합니다.

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**주 작업 영역**

의 기본 작업 영역을 [!DNL JupyterLab] 사용하면 문서 및 기타 활동을 탭 패널로 크기를 조절하거나 세분할 수 있습니다. 탭을 마이그레이션하려면 탭 패널의 가운데로 탭을 드래그합니다. 탭을 패널 왼쪽, 오른쪽, 위쪽 또는 아래쪽으로 드래그하여 패널을 나눕니다.

![](../images/jupyterlab/user-guide/main_work_area.gif)

### 코드 셀 {#code-cells}

코드 셀은 노트북의 기본 컨텐츠입니다. 여기에는 전자 필기장의 관련 커널의 언어로 된 소스 코드와 코드 셀을 실행한 결과로 출력된 소스 코드가 포함됩니다. 실행 횟수는 실행 순서를 나타내는 모든 코드 셀의 오른쪽에 표시됩니다.

![](../images/jupyterlab/user-guide/code_cell.png)

일반적인 셀 작업은 아래에 설명되어 있습니다.

* **셀 추가:** 노트북 메뉴에서 더하기 기호(**+**)를 클릭하여 빈 셀을 추가합니다. 새 셀은 현재 상호 작용하는 셀 아래에 놓이거나 특정 셀이 포커스가 있는 경우 전자 필기장의 끝에 배치됩니다.

* **셀 이동:** 이동할 셀 오른쪽에 커서를 놓고 셀을 클릭하고 새 위치로 드래그합니다. 또한 노트북 간에 셀을 이동하면 해당 컨텐트와 함께 셀이 복제됩니다.

* **셀 실행:** 실행할 셀의 본문을 클릭한 다음 노트북 메뉴에서 **재생** 아이콘(****▶)을 클릭합니다. 커널이 실행을 처리할 때 셀의 실행 카운터에 별표(**\***)가 표시되고 완료될 때 정수로 대체됩니다.

* **셀 삭제:** 삭제할 셀의 본문을 클릭한 다음 **가리기** 아이콘을 클릭합니다.

### 커널 {#kernels}

노트북 커널은 노트북 전지를 처리하기 위한 언어별 컴퓨팅 엔진이다. 또한 [!DNL Python]R, PySpark 및 [!DNL JupyterLab] [!DNL Spark] (Scala)에서 추가 언어 지원을 제공합니다. 노트북 문서를 열면 연관된 커널이 실행됩니다. 노트북 셀이 실행되면 커널이 계산을 수행하고 상당한 CPU 및 메모리 리소스를 소모할 수 있는 결과를 생성합니다. 커널이 종료될 때까지 할당된 메모리는 해제되지 않습니다.

아래 표에 설명된 특정 기능과 기능은 특정 커널로 제한됩니다.

| 커널 | 라이브러리 설치 지원 | [!DNL Platform] 통합 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 예 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 예 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | 아니요 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 커널 세션 {#kernel-sessions}

활성 전자 필기장이나 활동의 각 활동은 커널 세션을 [!DNL JupyterLab] 사용합니다. 왼쪽 사이드바에서 **실행 단말기 및 커널** 탭을 확장하여 모든 활성 세션을 찾을 수 있습니다. 노트북 인터페이스의 맨 위 오른쪽에 있는 커널의 유형과 상태를 관찰하여 확인할 수 있습니다. 아래 다이어그램에서 전자 필기장의 관련 커널은 **[!DNL Python]3이며** 현재 상태는 오른쪽에 회색 원으로 표시됩니다. 빈 원은 유휴 커널을 의미하고 단색 원은 사용 중인 커널을 의미합니다.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

커널이 장기간 종료되거나 비활성 상태인 경우 **커널 없음!** 단색 원이 표시됩니다. 커널 상태를 클릭하고 아래에 설명된 대로 적절한 커널 유형을 선택하여 커널을 활성화합니다.

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 론처 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

사용자 지정 *시작* 프로그램은 다음을 포함하여 작업을 시작할 수 있도록 지원되는 커널에 사용할 수 있는 유용한 노트북 템플릿을 제공합니다.

| 템플릿 | 설명 |
| --- | --- |
| 비어 있음 | 빈 전자 필기장 파일입니다. |
| 스타터 | 샘플 데이터를 사용한 데이터 탐색을 시연하는 미리 채워진 노트북입니다. |
| 소매 판매 | 샘플 데이터를 사용한 [소매 판매 레서피를](https://adobe.ly/2wOgO3L) 설명하는 미리 채워진 노트북입니다. |
| 레서피 빌더 | 레서피를 만드는 전자 필기장 템플릿입니다 [!DNL JupyterLab]. 이 레시피 제작 과정을 설명하고 설명하는 코드와 해설이 미리 준비되어 있습니다. 자세한 연습을 보려면 [전자 필기장에서 레서피 자습서를](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) 참조하십시오. |
| [!DNL Query Service] | 데이터를 규모에 맞게 분석하는 제공된 샘플 워크플로우와 함께 [!DNL Query Service] 직접 [!DNL JupyterLab] 의 사용을 시연하는 미리 채워진 노트북입니다. |
| XDM 이벤트 | 데이터 구조 전체에서 공통적인 기능에 초점을 맞춘 후값 경험 이벤트 데이터에 대한 데이터 탐색을 시연하는 미리 채워진 노트북입니다. |
| XDM 쿼리 | 경험 이벤트 데이터에 대한 샘플 비즈니스 쿼리를 보여 주는 미리 채워진 전자 필기장입니다. |
| 집계 | 많은 양의 데이터를 작고 관리하기 쉬운 청크로 취합하는 샘플 워크플로우를 보여주는 미리 채워진 노트북입니다. |
| 클러스터링 | 클러스터링 알고리즘을 사용하여 종단간 머신 러닝 모델링 과정을 설명하는 미리 채워진 노트북입니다. |

일부 노트북 템플릿은 특정 커널로 제한됩니다. 각 커널에 대한 템플릿 가용성은 다음 표에 매핑됩니다.

<table>
    <tr>
        <td></td>
        <th><strong>비어 있음</strong></th>
        <th><strong>스타터</strong></th>
        <th><strong>소매 판매</strong></th>
        <th><strong>레서피 빌더</strong></th>
        <th><strong>[!DNL 쿼리 서비스]</strong></th>
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
        <th  ><strong>PySpark 3([!DNL Spark] 2.4)</strong></th>
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
        <th ><strong>Scala</strong></th>
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

새 *론쳐를 열려면 파일*> 새 론처 **를 클릭합니다**. 또는 왼쪽 사이드바에서 **파일 브라우저** 를 확장하고 더하기 기호(**+**)를 클릭합니다.

![](../images/jupyterlab/user-guide/new_launcher.gif)

### GPU 및 메모리 서버 구성( [!DNL Python]/R)

오른쪽 상단 모서리의 톱니바퀴 아이콘 [!DNL JupyterLab] 을 선택하여 *노트북 서버 구성을 엽니다*. 슬라이더를 사용하여 GPU를 켜거나 필요한 메모리 양을 할당할 수 있습니다. 할당할 수 있는 메모리 양은 조직이 프로비저닝한 양에 따라 다릅니다. 저장할 **[!UICONTROL 구성]** 업데이트를 선택합니다.

>[!NOTE]
>
>노트북에 대해 조직당 하나의 GPU만 제공됩니다. GPU를 사용 중인 경우 현재 GPU를 출시할 수 있도록 예약한 사용자가 대기해야 합니다. 이 작업은 4시간 이상 GPU를 유휴 상태로 내보내거나 종료하여 수행할 수 있습니다.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## 다음 단계

지원되는 각 노트북에 대한 자세한 내용과 사용 방법에 대한 자세한 내용은 [Jupiterlab 노트북 데이터 액세스](./access-notebook-data.md) 개발자 안내서를 참조하십시오. 이 안내서에서는 JupiterLab 전자 필기장을 사용하여 데이터 읽기, 쓰기 및 쿼리 등 데이터에 액세스하는 방법에 중점을 둡니다. 데이터 액세스 안내서에는 지원되는 각 노트북에서 읽을 수 있는 최대 데이터 양에 대한 정보도 포함되어 있습니다.

## 지원되는 라이브러리 {#supported-libraries}

### [!DNL Python] / R

| 라이브러리 | 버전 |
| :------ | :------ |
| 노트북 | 6.0.0 |
| 요청 | 2.22.0 |
| 불순하 | 4.0.0 |
| folio | 0.10.0 |
| ipywidgets | 7.5.1 |
| 보케 | 1.3.1 |
| 겐심 | 3.7.3 |
| 이평선 | 0.5.2 |
| jq | 1.6 |
| 커라스 | 2.2.4 |
| nltk | 3.2.5 |
| 판다 | 0.22.0 |
| pandasql | 0.7.3 |
| 베개 | 6.0.0 |
| scitkit 이미지 | 0.15.0 |
| scitkit 학습 | 0.21.3 |
| 혈통 | 1.3.0 |
| 스크랩해 | 1.3.0 |
| seaborn | 0.9.0 |
| 스타스모델스 | 0.10.1 |
| 탄성 | 5.1.0.17 |
| 플롯 | 0.11.5 |
| py-xgboost | 0.90 |
| opencv | 3.4.1 |
| 불스파크 | 2.4.3 |
| 불성화 | 1.0.1 |
| wxpython | 4.0.6 |
| 컬러리스트 | 0.3.0 |
| 지질학 | 0.5.1 |
| 파이스프 | 2.1.0 |
| 사철 | 1.6.4 |
| rpy2 | 2.9.4 |
| r-essentials | 3.6 |
| 알갱이 | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-gethemes | 4.2.0 |
| r-gvis | 0.4.4 |
| 영어 | 1.2.4.1 |
| 벼락 | 3.0 |
| r-조작 | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| 생존율 | 2.44_1.1 |
| r-동물원 | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| r-쿼드프로그 | 1.5_7 |
| r-rjson | 0.2.20 |
| r-forecast | 8.7 |
| r-rsolnp | 1.16 |
| 망사 | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-corrplot | 0.84 |
| r-fn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-randomizable forest | 4.6_14 |
| 역경 | 1.2.1 |
| r-tree | 1.0_39 |
| 피몬고 | 3.8.0 |
| 화살 | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| 통나무 | 0.3.2 |
| 비단뱀 | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupiter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| azure | 0.36.0 |
| [!DNL jupyterlab] | 1.0.4 |
| fanda_ml | 0.6.1 |
| tensorflow gpu | 1.14.0 |
| nodejs | 12.3.0 |
| 모의 | 3.0.5 |
| 점선 | 0.3.3 |
| 글꼴 아나콘드 | 1.0 |
| psycopg2 | 2.8.3 |
| 코 | 1.3.7 |
| autovizwidget | 0.12.9 |
| 알트에어 | 3.1.0 |
| bega_datasets | 0.7.0 |
| 종소 | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1.0 |
| nbimporter | 0.3.1 |

### PySpark

| 라이브러리 | 버전 |
| :------ | :------ |
| 요청 | 2.18.4 |
| 겐심 | 2.3.0 |
| 커라스 | 2.0.6 |
| nltk | 3.2.4 |
| 판다 | 0.20.1 |
| pandasql | 0.7.3 |
| 베개 | 5.3.0 |
| scitkit 이미지 | 0.13.0 |
| scitkit 학습 | 0.19.0 |
| 혈통 | 0.19.1 |
| 스크랩해 | 1.3.3 |
| 스타스모델스 | 0.8.0 |
| 탄성 | 4.0.30.44 |
| py-xgboost | 0.60 |
| opencv | 3.1.0 |
| 화살 | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |