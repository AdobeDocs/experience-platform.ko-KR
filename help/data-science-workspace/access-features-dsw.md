---
keywords: Experience Platform;home;Data Science Workspace;popular topics;access control;sandbox;intelligence pack;dsw features;dsw access;Adobe Experience Platform Intelligence;intelligence;aep intelligence package
solution: Experience Platform
title: 데이터 과학 작업 공간 액세스 및 기능
topic: Access and features for data science workspace
description: '다음 문서에서는 데이터 과학 작업 공간 권한 및 기능에 대한 액세스 권한에 대해 간략히 설명합니다. '
translation-type: tm+mt
source-git-commit: 40181fc9b1b08c2e21f806caae76b8af0ec9e5e6
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 3%

---


# 데이터 과학 작업 공간 액세스 및 기능

다음 문서에서는 데이터 과학 작업 공간 권한 및 기능에 대한 액세스 권한에 대해 간략히 설명합니다.

![DSW 탭](./images/access/platform-tabs.png)

- **노트북:** Experience Platform에 대한 데이터를 탐색, 분석 및[모델링할 수 있는 인터랙티브한 개발 환경(JupiterLab](./jupyterlab/overview.md))을 제공합니다.
- **모델:** 고급 기계 학습 레서피 및 모델을 만들고 게시하고 저장하는 데 사용되는 도구를 제공합니다. 자세한 내용은 기계 학습 모델 [만들기 및 게시 자습서를](./models-recipes/create-publish-model.md) 참조하십시오.
- **서비스:** Intelligent Services와 같은 Adobe에서 제공하는 서비스와 [Data Science Workspace를 사용하여 제작한 모든 맞춤형 서비스를](../intelligent-services/home.md) 모두 포함합니다.

서비스 탭만 표시되는 이유는 무엇입니까?

- 조직은 지능형 서비스 고객 AI가 포함된 실시간 고객 데이터 플랫폼(RTCDP)만 사용할 수 있습니다.

데이터 과학 **** 탭을 볼 수 없고 데이터 과학 작업 공간 기능을 활용하려는 경우 회사 관리자에게 문의하여 Adobe Experience Platform 인텔리전스 라이선스가 있는지 확인하십시오.

## Adobe Experience Platform 인텔리전스 패키지 addon

다음 표에서는 Adobe Experience Platform 인텔리전스 패키지 추가 여부에 대한 데이터 과학 작업 공간의 주요 차이점을 설명합니다.

>[!NOTE]
>
>둘 이상의 인텔리전스 패키지 추가 라이선스를 부여할 수 있으며 늘어난 용량이 전체 권한에 추가됩니다. 예를 들어 2개의 Adobe Experience Platform 인텔리전스 패키지 라이선스를 구입한 경우 총 20명의 동시 노트북 사용자에게 권한이 부여됩니다.

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] 고급 패키지 추가 |
| --- | :---: | :---: |
| 지원되는 전자 필기장 사용자 수입니다. | 동시 사용자 5명 | 첫 번째 팩은 동시 사용자 5명을 추가하고 추가 구매는 패키징당 동시 사용자 10명을 추가합니다. |
| R, Python, Scala, PySpark 등 탐색을 위한 통합 Jupiter 노트북 제작 | X | X |
| 쿼리 서비스와 기본 통합. 노트북에서 SQL을 사용하여 데이터 세트를 탐색하고 형성할 수 있습니다. | X | X |
| 예측 분석을 위해 미리 만들어진 노트북 템플릿에 액세스 | X | X |
| Jupiter Notebook을 사용하여 모델을 수동으로 트레이닝하고 점수를 매길 수 있습니다. | X | X |
| 트레이닝 일정을 예약하고 작업을 참조하는 기능을 사용하여 모델을 배포하고 운영할 수 있습니다. |  | X |
| 모델을 손쉽게 구성, 평가, 트레이닝, 점수, 프로덕션에 게시할 수 있는 레서피 프레임워크입니다. |  | X |
| UI 기반의 모델 실험 및 평가 |  | X |
| Tensorflow 모델(GPU 컴퓨팅)에 대한 딥 러닝 지원 |  | X |
| 대용량 데이터 세트(10MM + 행)를 트레이닝하고 점수를 매기려면 Spark 기반의 분산 컴퓨팅 |  | X |

## 액세스 제어

Experience Platform에 대한 액세스 제어는 [Adobe Admin Console을 통해 관리됩니다](https://adminconsole.adobe.com). 이 기능은 Admin Console의 제품 프로필을 활용하므로 사용자에게 사용 권한 및 샌드박스를 연결합니다. See the [access control overview](../access-control/home.md) for more information.

데이터 과학 작업 공간을 사용하려면 &quot;데이터 과학 작업 공간 관리&quot; 권한이 활성화되어 있어야 합니다. 다음 표에서는 이 권한을 활성화하거나 비활성화하는 효과에 대해 설명합니다.

| 사용 권한 | 활성화됨 | 비활성화됨 |
|---|---|---|
| 데이터 과학 작업 공간 관리 | 데이터 과학 작업 공간의 모든 서비스에 대한 액세스를 제공합니다. | 데이터 과학 작업 공간 내의 모든 서비스에 대한 API 및 UI 액세스가 비활성화됩니다. 비활성화된 상태에서 **노트북**, 모델 **및**&#x200B;서비스 **페이지를 선택할 수** 없습니다. <li>실시간 고객 데이터 플랫폼(RTCDP)을 통해 **서비스** 액세스를 계속 이용할 수 있습니다.</li> |

## 샌드박스 지원

샌드박스는 Experience Platform의 단일 인스턴스 내의 가상 파티션입니다. 각 플랫폼 인스턴스는 하나의 프로덕션 샌드박스와 여러 개의 비프로덕션 샌드박스를 지원하며, 각 샌드박스는 자체 플랫폼 리소스 라이브러리를 유지합니다. 비프로덕션 샌드박스를 사용하면 프로덕션 샌드박스에 영향을 주지 않고 기능을 테스트하고 실험을 실행하고 사용자 정의 구성을 만들 수 있습니다. 샌드박스에 대한 자세한 내용은 [샌드박스 개요를 참조하십시오](../sandboxes/home.md).

현재 데이터 과학 작업 영역에는 다음과 같은 샌드박스 제한이 있습니다.

- 컴퓨팅 리소스는 프로덕션 샌드박스와 비프로덕션 샌드박스 간에 공유됩니다.

## 다음 단계

이 문서에서는 데이터 과학 작업 공간에서 사용할 수 있는 다양한 유형의 액세스 및 기능에 대해 간략하게 설명합니다.

전체 일상적인 작업 과정과 같은 데이터 과학 작업 공간에 대한 자세한 내용은 [데이터 과학 작업 공간 연습](./walkthrough.md) 설명서를 참조하십시오. 자세한 내용은 [데이터 과학 작업 공간 개요를 참조하십시오](./home.md).