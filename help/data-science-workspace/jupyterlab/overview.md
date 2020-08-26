---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: JupiterLab 사용 안내서
topic: Overview
description: JupiterLab은 Project Jupiter를 위한 웹 기반의 유저 인터페이스로 Adobe Experience Platform과 긴밀하게 통합되어 있습니다. 데이터 과학자들이 Jupiter 노트북, 코드 및 데이터를 사용하여 작업할 수 있는 인터랙티브한 개발 환경을 제공합니다.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 11%

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
* [PySpark/Spark 실행 리소스](#execution-resource)
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
| 소매 판매 | 샘플 데이터를 사용하는 <a href="https://adobe.ly/2wOgO3L" target="_blank">소매 영업 레서피를</a> 설명하는 미리 채워진 노트북입니다. |
| 레서피 빌더 | 레서피를 만드는 전자 필기장 템플릿입니다 [!DNL JupyterLab]. 이 레시피 제작 과정을 설명하고 설명하는 코드와 해설이 미리 준비되어 있습니다. 자세한 연습을 보려면 <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">전자 필기장에서 레서피 자습서를</a> 참조하십시오. |
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

## 전자 필기장을 사용하여 [!DNL Platform] 데이터 액세스

지원되는 각 커널은 노트북 내의 데이터 세트에서 데이터를 읽을 수 있도록 하는 내장 기능을 제공합니다 [!DNL Platform] . 그러나 페이지 매김 데이터에 대한 지원은 [!DNL Python] 및 R 노트북으로 제한됩니다.

### 노트북 데이터 제한

다음 정보는 읽을 수 있는 최대 데이터 양, 사용된 데이터 유형 및 데이터를 읽는 예상 기간을 정의합니다. 및 [!DNL Python] R의 경우 40GB RAM으로 구성된 노트북 서버가 벤치마크에 사용되었습니다. PySpark 및 Scala의 경우 64GB RAM, 8개 코어, 2개의 DBU로 구성된 데이터베이스 클러스터는 아래 나와 있는 벤치마크에 최대 4명의 작업자를 사용했습니다.

사용한 ExperienceEvent 스키마 데이터는 최대 10억 개(1B) 행에 이르는 1,000개 행에서 다양한 크기로 사용됩니다. PySpark 및 [!DNL Spark] 지표의 경우 XDM 데이터에 10일의 날짜 범위가 사용되었습니다.

임시 스키마 데이터는 CTAS(Create Table as Select)를 사용하여 [!DNL Query Service] 미리 처리되었습니다. 또한 이 데이터는 최대 10억(1B) 행에 이르는 1,000개 행부터 크기가 달라집니다.

#### [!DNL Python] 노트북 데이터 제한

**XDM ExperienceEvent 스키마:** 최대 200만 개의 XDM 데이터 행(~6.1GB의 디스크 데이터)을 22분 이내에 읽을 수 있어야 합니다. 행을 더 추가하면 오류가 발생할 수 있습니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 디스크 크기(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK(초) | 20.3 | 86.8 | 63 | 659 | 1315 |

**임시 스키마:** XDM(Ad-Hoc) 데이터가 아닌 데이터의 최대 5백만 행(~5.6GB의 디스크에 있는 데이터)을 14분 이내에 읽을 수 있어야 합니다. 행을 더 추가하면 오류가 발생할 수 있습니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 디스크 크기(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK(초) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### 노트북 데이터 제한

**XDM ExperienceEvent 스키마:** 13분 이내에 최대 100만 개의 XDM 데이터 행(디스크에 3GB 데이터)을 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 디스크 크기(MB) | 18.73 | 187.5 | 308 | 3000 |
| R 커널(초) | 14.03 | 69.6 | 86.8 | 775 |

**임시 스키마:** 최대 300만 개의 애드혹 데이터 행(293MB 데이터 디스크)을 10분 이내에 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 디스크 크기(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK(초) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### PySpark([!DNL Python] 커널) 노트북 데이터 제한:

**XDM ExperienceEvent 스키마:** 대화형 모드에서는 20분 내에 최대 5백만 개의 XDM 데이터 행(~13.42GB 디스크 데이터)을 읽을 수 있습니다. 대화형 모드는 최대 5백만 개의 행만 지원합니다. 큰 데이터 세트를 읽으려면 일괄 처리 모드로 전환하는 것이 좋습니다. 일괄 처리 모드에서는 약 14시간 내에 XDM 데이터의 최대 5억개 행(~1.31TB 데이터)을 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 디스크 크기 | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK(대화형 모드) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK(배치 모드) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**임시 스키마:** 인터랙티브 모드에서는 XDM이 아닌 데이터의 최대 10억개 행(~1.05TB 데이터 디스크)을 3분 이내에 읽을 수 있어야 합니다. 일괄 처리 모드에서는 18분 내에 XDM 외의 데이터를 최대 10억개 행(~1.05TB 데이터 디스크에 포함)으로 읽을 수 있습니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 디스크 크기 | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| SDK 대화형 모드(초) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | 22s | 28.4s | 40s | 97.4s | 154.5s |
| SDK 배치 모드(초) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

#### [!DNL Spark] (스칼라 커널) 노트북 데이터 제한:

**XDM ExperienceEvent 스키마:** 인터랙티브 모드에서는 18분 이내에 최대 5백만 개의 XDM 데이터 행(~13.42GB 디스크 데이터)을 읽을 수 있습니다. 대화형 모드는 최대 5백만 개의 행만 지원합니다. 큰 데이터 세트를 읽으려면 일괄 처리 모드로 전환하는 것이 좋습니다. 일괄 처리 모드에서는 약 14시간 내에 XDM 데이터의 최대 5억개 행(~1.31TB 데이터)을 읽을 수 있어야 합니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 디스크 크기 | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK 대화형 모드(초) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK 배치 모드(초) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**임시 스키마:** 인터랙티브 모드에서는 XDM이 아닌 데이터의 최대 10억개 행(~1.05TB 데이터 디스크)을 3분 이내에 읽을 수 있어야 합니다. 일괄 처리 모드에서는 16분 내에 XDM 외의 데이터를 최대 10억개 행(~1.05TB 데이터 디스크에 포함)으로 읽을 수 있습니다.

| 행 수 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 디스크 크기 | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| SDK 대화형 모드(초) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | 29.2s | 29.7s | 36.9s | 83.5s | 139s |
| SDK 배치 모드(초) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

### 데이터 세트 [!DNL Python]/R에서 읽기

[!DNL Python] 및 R 노트북에서는 데이터 세트에 액세스할 때 데이터를 게시할 수 있습니다. 페이지 매김이 있거나 없는 데이터를 읽는 샘플 코드는 아래에 나와 있습니다.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### 페이지 매김 없이 데이터 세트 [!DNL Python]에서 읽기

다음 코드를 실행하면 전체 데이터 세트를 읽습니다. 실행이 성공하면 데이터는 변수에서 참조하는 판더 데이터 프레임으로 저장됩니다 `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`:액세스할 데이터 집합의 고유 ID

#### 페이지 매김이 있는 데이터 세트 [!DNL Python]에서 읽기

다음 코드를 실행하면 지정된 데이터 집합의 데이터가 읽습니다. 페이지 매김은 함수 `limit()` 및 `offset()` 각각 데이터를 제한 및 오프셋하여 이루어집니다. 데이터 제한은 데이터를 읽기 전에 건너뛸 데이터 포인트 수를 나타내는 반면 데이터 제한은 읽을 최대 데이터 포인트 수를 나타냅니다. 읽기 작업이 성공적으로 실행되면 데이터가 변수에서 참조하는 판더 데이터 프레임으로 저장됩니다 `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`:액세스할 데이터 집합의 고유 ID

### PySpark/[!DNL Spark]/Scala의 데이터 세트에서 읽기

활성 PySpark 또는 Scala 전자 필기장이 열리고 왼쪽 사이드바에서 **Data Explorer** 탭을 확장하고 데이터 세트 **를 두 번 클릭하여 사용 가능한 데이터 집합** 목록을 봅니다. 액세스할 데이터 세트 목록을 마우스 오른쪽 단추로 클릭하고 **노트북에서 데이터 탐색을 클릭합니다**. 다음 코드 셀이 생성됩니다.

#### PySpark([!DNL Spark] 2.4) {#pyspark2.4}

Spark 2.4가 도입됨에 따라 [`%dataset`](#magic) 맞춤형 기능이 제공됩니다.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### 스칼라([!DNL Spark] 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>
>Scala에서는 값 `sys.env()` 을 선언하고 반환하는 데 사용할 수 있습니다 `option`.

### PySpark 3([!DNL Spark] 2.4) 노트북에서 %dataset 매직 사용 {#magic}

2.4의 도입으로 새로운 PySpark 3( [!DNL Spark] 2.4) 노트북( `%dataset`[!DNL Spark][!DNL Python] 3커널)에서 사용할 수 있는 맞춤형 기능이 제공됩니다.

**사용**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**설명**

노트북( [!DNL Data Science Workspace] [!DNL Python][!DNL Python] 3커널)에서 데이터 세트를 읽거나 쓰는 사용자 정의 매직 명령입니다.

* **{action}**:데이터 세트에 대해 수행할 작업 유형입니다. 두 가지 작업을 &quot;읽기&quot; 또는 &quot;쓰기&quot;로 사용할 수 있습니다.
* **—datasetId {id}**:데이터를 읽거나 쓸 수 있도록 데이터 집합의 ID를 제공하는 데 사용됩니다. 이것은 필수 인수입니다.
* **—dataFrame {df}**:판다들의 데이터 프레임 이것은 필수 인수입니다.
   * 작업이 &quot;읽기&quot;인 경우 {df}는 데이터 집합 읽기 작업의 결과를 사용할 수 있는 변수입니다.
   * 작업이 &quot;write&quot;이면 이 데이터 프레임 {df}이(가) 데이터 세트에 기록됩니다.
* **—mode(선택 사항)**:허용되는 매개 변수는 &quot;batch&quot; 및 &quot;interactive&quot;입니다. 기본적으로 모드는 &quot;interactive&quot;로 설정됩니다. 대량의 데이터를 읽을 때는 &quot;일괄 처리&quot; 모드를 사용하는 것이 좋습니다.

**예**

* **예제**&#x200B;보기: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **쓰기 예**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### 데이터 쿼리 [!DNL Query Service] 는 [!DNL Python]

[!DNL JupyterLab] 을 [!DNL Platform] 사용하면 전자 필기장의 SQL을 사용하여 [!DNL Python] Adobe Experience Platform 쿼리 서비스를 통해 데이터에 액세스할 수 있습니다 <a href="https://www.adobe.com/go/query-service-home-en" target="_blank"></a>. 데이터 세트를 통해 액세스하는 [!DNL Query Service] 것은 실행 시간이 매우 짧기 때문에 대규모 데이터 세트를 처리하는 데 유용합니다. 데이터를 쿼리하는 데 처리 시간 제한 [!DNL Query Service] 이 10분입니다.

를 사용하기 전에 [!DNL Query Service] SQL 구문 [!DNL JupyterLab]에 대한 작업 지식이 <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">[!DNL Query Service] 있는지 확인하십시오</a>.

데이터를 쿼리하려면 대상 데이터 집합 이름을 제공해야 [!DNL Query Service] 합니다. 데이터 탐색기를 사용하여 원하는 데이터 세트를 찾아 필요한 **코드 셀을 생성할 수 있습니다**. 데이터 세트 목록을 마우스 오른쪽 단추로 클릭하고 **노트북의** 데이터 쿼리를 클릭하여 다음 두 개의 코드 셀을 생성합니다.


이 [!DNL Query Service] 에서 활용하려면 먼저 작업 중인 [!DNL JupyterLab]노트북과 작업 중인 [!DNL Python] 노트북 간에 연결을 만들어야 합니다 [!DNL Query Service]. 이렇게 하려면 첫 번째 생성된 셀을 실행하여 할 수 있습니다.

```python
qs_connect()
```

두 번째 생성된 셀에서 첫 번째 행을 SQL 쿼리 앞에 정의해야 합니다. 기본적으로 생성된 셀은 쿼리 결과를 팬더 데이터 프레임으로 저장하는 선택적 변수(`df0`)를 정의합니다. <br>이 `-c QS_CONNECTION` 인수는 필수 항목이며 커널에 대해 SQL 쿼리를 실행하라고 지시합니다 [!DNL Query Service]. 추가 인수 목록은 [부록을](#optional-sql-flags-for-query-service) 참조하십시오.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

다음 예제와 같이 문자열 형식의 구문을 사용하고 변수를 중괄호(중괄호)로 묶어서 SQL 쿼리 내에서 직접 Python 변수를 참조할 수 있습니다.`{}`

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### ExperienceEvent 데이터 필터링: [!DNL Python]/R

또는 R 전자 필기장에서 ExperienceEvent 데이터 세트에 액세스하고 필터링하려면, 논리 연산자를 사용하여 특정 시간 범위를 정의하는 필터 규칙과 함께 데이터 세트( [!DNL Python]`{DATASET_ID}`)의 ID를 제공해야 합니다. 시간 범위를 정의하면 지정된 모든 페이지 지정이 무시되고 전체 데이터 세트가 고려됩니다.

필터링 연산자 목록은 아래에 설명되어 있습니다.

* `eq()`: 같음
* `gt()`: 보다 큼
* `ge()`: 크거나 같음
* `lt()`: 보다 작음
* `le()`: 작거나 같음
* `And()`:논리 AND 연산자
* `Or()`:논리 OR 연산자

다음 셀에서는 2019년 1월 1일부터 2019년 12월 31일 종료 사이에만 존재하는 데이터로 ExperienceEvent 데이터 세트를 필터링합니다.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### PySpark/에서 ExperienceEvent 데이터 필터링[!DNL Spark]

PySpark 또는 Scala 전자 필기장에서 ExperienceEvent 데이터 세트에 액세스하고 이를 필터링하려면 데이터 세트 ID(`{DATASET_ID}`), 조직의 IMS ID 및 특정 시간 범위를 정의하는 필터 규칙을 제공해야 합니다. 필터링 시간 범위는 함수 매개 변수가 SQL 쿼리 문자열 `spark.sql()`인 함수를 사용하여 정의됩니다.

다음 셀에서는 2019년 1월 1일부터 2019년 12월 31일 종료 사이에만 존재하는 데이터로 ExperienceEvent 데이터 세트를 필터링합니다.

#### PySpark 3([!DNL Spark] 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### 스칼라([!DNL Spark] 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>
>Scala에서는 값 `sys.env()` 을 선언하고 반환하는 데 사용할 수 있습니다 `option`. 이렇게 하면 변수가 한 번만 사용된다는 사실을 알고 있으면 변수를 정의할 필요가 없습니다. 다음 예는 위 예제 `val userToken` 에서 가져온 다음 이 예제의 대체 요소 `option` 로 인라인 내에 선언합니다.
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

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
| 판다 | 1.3.7 |
| autovizwidget | 0.12.9 |
| 알트에어 | 3.1.0 |
| bega_datasets | 0.7.0 |
| 모의 | 1.0.1 |
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
| sql | 0.20.1 |
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

## 다음에 대한 선택적 SQL 플래그 [!DNL Query Service] {#optional-sql-flags-for-query-service}

이 표에서는 사용할 수 있는 선택적 SQL 플래그에 대해 간략하게 설명합니다 [!DNL Query Service].

| **플래그** | **설명** |
| --- | --- |
| `-h`, `--help` | 도움말 메시지를 표시하고 종료합니다. |
| `-n`, `--notify` | 쿼리 결과에 알리는 토글 옵션. |
| `-a`, `--async` | 이 플래그를 사용하면 쿼리를 비동기 방식으로 실행하고 쿼리를 실행하는 동안 커널을 해제할 수 있습니다. 쿼리가 완료되지 않은 경우 정의되지 않을 수도 있으므로 쿼리 결과를 변수에 지정할 때는 주의하십시오. |
| `-d`, `--display` | 이 플래그를 사용하면 결과가 표시되지 않습니다. |

