---
keywords: Experience Platform;홈;Data Science Workspace;인기 주제;액세스 제어;샌드박스;인텔리전스 팩;dsw 기능;dsw 액세스;Adobe Experience Platform 인텔리전스;인텔리전스;aep 인텔리전스 패키지
solution: Experience Platform
title: 데이터 과학 Workspace 액세스 및 기능
description: 다음 문서에서는 Data Science Workspace 권한 및 기능에 대한 액세스 권한에 대해 간략하게 설명합니다.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 데이터 과학 Workspace 액세스 및 기능

다음 문서에서는 Data Science Workspace 권한 및 기능에 대한 액세스 권한에 대해 간략하게 설명합니다.

![DSW 탭](./images/access/platform-tabs.png)

- **Notebooks:** Experience Platform 시 데이터를 탐색, 분석 및 모델링할 수 있는 대화형 개발 환경([JupyterLab](./jupyterlab/overview.md))을 제공합니다.
- **모델:** 고급 머신 러닝 레서피 및 모델을 만들고 게시하고 저장하는 데 사용되는 도구를 제공합니다. 자세한 내용은 [기계 학습 모델 만들기 및 게시](./models-recipes/create-publish-model.md) 자습서를 참조하십시오.
- **서비스:** Adobe 제공 서비스(예: [AI/ML 서비스](../intelligent-services/home.md))와 Data Science Workspace으로 만든 사용자 지정 서비스를 모두 포함합니다.

서비스 탭만 표시되는 이유는 무엇입니까?

- 조직은 고객 AI AI/ML 서비스가 포함된 Adobe Real-time Customer Data Platform(Real-Time CDP)만 권한을 가질 수 있습니다.

**데이터 과학** 탭을 볼 수 없고 데이터 과학 Workspace 기능을 활용하려면 회사 관리자에게 문의하여 Adobe Experience Platform Intelligence 라이선스가 있는지 확인하십시오.

## Data Science Workspace 패키징

데이터 과학 Workspace 기능은 Adobe Experience Platform Intelligence 패키지 및 Advanced Intelligence Pack 추가 기능에서 사용할 수 있습니다

다음 표에서는 Advanced Intelligence Pack 추가 기능이 있는 경우와 없는 경우의 Data Science Workspace 권한에 대한 몇 가지 주요 차이점을 간략히 설명합니다.

>[!NOTE]
>
>하나 이상의 Advanced Intelligence Pack Addon에 라이센스를 부여할 수 있으며 증가된 용량은 전체 자격에 추가됩니다. 예를 들어 2개의 Adobe Experience Platform Advanced Intelligence Pack 추가 기능에 라이선스를 부여한 경우 총 20명의 동시 Notebook 사용자에게 권한이 부여됩니다.

| 데이터 과학 Workspace 권한 | Adobe Experience Platform Intelligence Package 전용 | Adobe Experience Platform Intelligence plus 고급 인텔리전스 팩 추가 기능 |
| --- | :---: | :---: |
| 지원되는 Notebook 사용자 수입니다. | 동시 사용자 5명 | 첫 번째 팩은 동시 사용자 5명을 추가하고 추가 구매는 패키지당 동시 사용자 10명을 추가합니다. |
| 탐색적 데이터 분석 및 모델 작성을 위한 통합 Jupyter Notebooks를 사용할 수 있습니다. | X(R, Python 및 Scala 라이브러리 지원) | X (PySpark 및 Spark ML 라이브러리 추가) |
| 쿼리 서비스와 기본 통합. Notebooks에서 SQL을 사용하여 데이터 세트를 탐색하고 구체화하는 기능. | X | X |
| 예측 분석을 위해 미리 빌드된 노트북 템플릿에 액세스합니다. | X | X |
| Jupyter Notebooks로 모델을 수동으로 교육하고 평가합니다. | X | X |
| 교육 및 예측 작업을 예약할 수 있는 기능을 사용하여 모델을 배포 및 운영합니다. | | X |
| 모델을 프로덕션에 쉽게 구성, 평가, 교육, 점수 및 게시할 수 있는 레시피 프레임워크입니다. |  | X |
| UI 기반 모델 실험 및 평가. | | X |
| Tensorflow 모델(GPU Compute)에 대한 딥러닝 지원. | | X |
| 대규모 데이터 세트(10MM + 행)에 대해 교육하고 평가하는 Spark 기반 분산 컴퓨팅. | | X |

## 액세스 제어

Experience Platform에 대한 액세스 제어는 [Adobe Admin Console](https://adminconsole.adobe.com)을(를) 통해 관리됩니다. 이 기능은 사용 권한 및 샌드박스를 사용자와 연결하는 Admin Console의 제품 프로필을 활용합니다. 자세한 내용은 [액세스 제어 개요](../access-control/home.md)를 참조하십시오.

Data Science Workspace을 사용하려면 &quot;Data Science Workspace 관리&quot; 권한이 활성화되어 있어야 합니다. 다음 표에서는 이 권한을 활성화하거나 비활성화할 때의 효과를 설명합니다.

| 사용 권한 | 활성화됨 | 비활성화됨 |
|---|---|---|
| 데이터 과학 관리 Workspace | 데이터 과학 Workspace의 모든 서비스에 대한 액세스를 제공합니다. | 데이터 과학 Workspace 내의 모든 서비스에 대한 API 및 UI 액세스가 비활성화됩니다. 비활성화되어 있는 동안에는 **Notebooks**, **모델** 및 **서비스** 페이지를 선택할 수 없습니다. <li>**서비스**&#x200B;에 대한 액세스는 Adobe Real-time Customer Data Platform(Real-Time CDP)를 통해 계속 사용할 수 있습니다.</li> |

## 샌드박스 지원

샌드박스는 단일 Experience Platform 인스턴스 내의 가상 파티션입니다. 각 플랫폼 인스턴스는 여러 프로덕션 및 비프로덕션 샌드박스를 지원하며, 각 샌드박스는 고유한 플랫폼 리소스 라이브러리를 유지 관리합니다. 비프로덕션 샌드박스를 사용하면 프로덕션 샌드박스에 영향을 주지 않고 기능을 테스트하고, 실험을 실행하고, 사용자 지정 구성을 수행할 수 있습니다. 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../sandboxes/home.md)를 참조하십시오.

현재 Data Science Workspace에는 다음과 같은 샌드박스 제한이 있습니다.

- 컴퓨팅 리소스는 프로덕션 및 비프로덕션 샌드박스에서 공유됩니다.

## 다음 단계

이 문서에서는 데이터 과학 Workspace에서 사용할 수 있는 다양한 유형의 액세스 및 기능에 대해 간략히 설명했습니다.

전체 일별 워크플로와 같이 데이터 과학 Workspace에 대한 자세한 내용은 [데이터 과학 Workspace 연습](./walkthrough.md) 설명서를 참조하십시오. 자세한 내용은 [데이터 과학 Workspace 개요](./home.md)를 참조하세요.
