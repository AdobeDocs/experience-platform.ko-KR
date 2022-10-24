---
keywords: Experience Platform;홈;Data Science Workspace;인기 항목;액세스 제어;샌드박스;인텔리전스 팩;dsw 기능;dsw 액세스;Adobe Experience Platform Intelligence;인텔리전스;aep 인텔리전스 패키지
solution: Experience Platform
title: 데이터 과학 작업 공간 액세스 및 기능
topic-legacy: Access and features for data science workspace
description: 다음 문서에서는 Data Science Workspace 권한 및 기능에 대한 액세스를 간략하게 설명합니다.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# 데이터 과학 작업 공간 액세스 및 기능

다음 문서에서는 Data Science Workspace 권한 및 기능에 대한 액세스를 간략하게 설명합니다.

![DSW 탭](./images/access/platform-tabs.png)

- **노트북:** 대화형 개발 환경 제공([JupiterLab](./jupyterlab/overview.md)) Experience Platform에서 데이터를 탐색, 분석 및 모델링할 수 있습니다.
- **모델:** 고급 기계 학습 레서피 및 모델을 만들고, 게시하고, 저장하는 데 사용되는 도구를 제공합니다. 자세한 내용은 [기계 학습 모델 만들기 및 게시](./models-recipes/create-publish-model.md) 자습서입니다.
- **서비스:** 과 같은 Adobe 제공 서비스를 모두 포함합니다. [AI/ML 서비스](../intelligent-services/home.md) 및 Data Science Workspace으로 만든 사용자 지정 서비스를 사용할 수 있습니다.

서비스 탭만 표시되는 이유는 무엇입니까?

- 조직은 고객 AI AI/ML 서비스를 포함하는 Adobe Real-time Customer Data Platform(Real-Time CDP)에만 액세스할 수 있습니다.

다음을 볼 수 없는 경우 **데이터 과학** 탭하고 Data Science Workspace 기능을 활용하려면 회사 관리자에게 문의하여 Adobe Experience Platform Intelligence 라이센스가 있는지 확인하십시오.

## Data Science Workspace 패키지

Data Science Workspace 기능은 Adobe Experience Platform Intelligence 패키지 및 Advanced Intelligence Pack 추가 기능에서 사용할 수 있습니다

다음 표에서는 Advanced Intelligence Pack 추가 기능을 사용하거나 사용하지 않는 Data Science Workspace 권한에 대한 몇 가지 주요 차이점을 설명합니다.

>[!NOTE]
>
>두 개 이상의 Advanced Intelligence Pack Addon 라이센스를 제공할 수 있으며 증가된 용량이 전체 사용 권한에 추가됩니다. 예를 들어, 2개의 Adobe Experience Platform Advanced Intelligence Pack Addons에 대한 라이센스가 있으면 총 20명의 동시 노트북 사용자가 부여됩니다.

| Data Science Workspace 권한 | Adobe Experience Platform Intelligence 패키지 전용 | Adobe Experience Platform Intelligence 및 Advanced Intelligence Pack 추가 기능 |
| --- | :---: | :---: |
| 지원되는 노트북 사용자 수입니다. | 동시 사용자 5명 | 첫 번째 팩은 동시 사용자 5명을 추가하고 추가 구매는 패키지당 동시 사용자 10명을 추가합니다. |
| 예비 데이터 분석 및 모델 작성을 위한 통합 Jupiter Notebook이 가능합니다. | X(R, Python 및 Scala 라이브러리 지원) | X (PySpark 및 Spark ML 라이브러리 추가) |
| Query Service와의 네이티브 통합. 전자 필기장에서 SQL을 사용하여 데이터 집합을 탐색 및 모양을 만들 수 있습니다. | X | X |
| 예측 분석을 위해 사전 빌드된 노트북 템플릿에 액세스 | X | X |
| Jupiter Notebook을 사용하여 모델을 수동으로 트레이닝하고 점수를 매깁니다. | X | X |
| 교육 및 인보싱 작업 일정을 예약할 수 있는 기능을 사용하여 모델을 배포 및 운영할 수 있습니다. |  | X |
| 레서피 프레임워크를 사용하여 모델을 손쉽게 구성, 평가, 교육, 점수 책정 및 프로덕션에 게시할 수 있습니다. |  | X |
| UI 기반의 모델 실험 및 평가 |  | X |
| Tensorflow 모델(GPU Compute)에 대한 심층 학습 지원 |  | X |
| 대규모 데이터 세트(10MM + 행)에 대해 교육 및 점수를 매기는 Spark 기반 분산 컴퓨팅 |  | X |

## 액세스 제어

Experience Platform에 대한 액세스 제어는 [Adobe Admin Console](https://adminconsole.adobe.com). 이 기능은 사용 권한 및 샌드박스를 사용자와 연결하는 Admin Console의 제품 프로필을 활용합니다. 자세한 내용은 [액세스 제어 개요](../access-control/home.md) 추가 정보.

Data Science Workspace를 사용하려면 &quot;데이터 과학 작업 공간 관리&quot; 권한을 활성화해야 합니다. 다음 표에서는 이 권한을 활성화하거나 비활성화하는 효과에 대해 설명합니다.

| 사용 권한 | 활성화됨 | 비활성화됨 |
|---|---|---|
| 데이터 과학 작업 공간 관리 | Data Science Workspace의 모든 서비스에 대한 액세스 권한을 제공합니다. | 데이터 과학 작업 공간 내의 모든 서비스에 대한 API 및 UI 액세스가 비활성화됩니다. 비활성화된 상태에서 **노트북**, **모델**, 및 **서비스** 페이지를 사용할 수 없습니다. <li>액세스 권한 **서비스** Adobe Real-time Customer Data Platform(Real-Time CDP)을 통해 계속 사용할 수 있습니다.</li> |

## 샌드박스 지원

샌드박스는 단일 Experience Platform 인스턴스 내의 가상 파티션입니다. 각 Platform 인스턴스는 여러 프로덕션 및 비프로덕션 샌드박스를 지원하며, 각 샌드박스는 자체 플랫폼 리소스 라이브러리를 유지합니다. 비프로덕션 샌드박스를 사용하면 프로덕션 샌드박스에 영향을 주지 않고 기능을 테스트하고, 실험을 실행하고, 사용자 지정 구성을 만들 수 있습니다. 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../sandboxes/home.md).

현재 Data Science Workspace 에는 다음과 같은 샌드박스 제한이 있습니다.

- 컴퓨팅 리소스는 프로덕션 샌드박스와 비프로덕션 샌드박스에서 공유됩니다.

## 다음 단계

이 문서에서는 Data Science Workspace에서 사용할 수 있는 다양한 유형의 액세스 및 기능에 대해 간략하게 설명합니다.

전체 일상적인 워크플로우와 같은 Data Science Workspace에 대해 자세히 알아보려면 [데이터 과학 작업 공간 안내](./walkthrough.md) 설명서. 일반적인 정보를 보려면 [Data Science Workspace 개요](./home.md).
