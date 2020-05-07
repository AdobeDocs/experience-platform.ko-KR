---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 실시간 머신 러닝 시작하기
topic: Getting started
translation-type: tm+mt
source-git-commit: c9e6eb41e51ad17ad11b9a669ca5e4cf6c899f8b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# 실시간 머신 러닝 시작하기

>[!IMPORTANT]
>모든 사용자는 아직 실시간 머신 러닝을 사용할 수 없습니다. 이 기능은 알파에 있으며 여전히 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

실시간 머신 러닝을 활용하려면 Adobe Experience Platform 및 Data Science Workspace로 규정된 조직에 액세스해야 합니다. 또한 Platform(플랫폼)에서 데이터 세트를 사용해야 합니다.

실시간 머신 러닝 가이드를 사용하려면 Python 3, Jupiter 노트북 [](../jupyterlab/overview.md), 데이터 과학 및 머신 러닝을 이해하는 작업이 필요합니다.

## Adobe Experience Platform의 데이터 세트

실시간 머신 러닝을 사용하려면 경험 플랫폼 내에 채워진 데이터 세트가 있어야 합니다. 외부 데이터 세트를 사용하여 JupiterLab 환경에 업로드하거나, 아직 업데이트하지 않은 경우 플랫폼 내에서 새로운 데이터 세트를 만들 수 있습니다.

>[!NOTE]
>이미 사용할 데이터 세트를 가지고 있는 경우 다음 두 단계를 건너뛸 수 있습니다.

### 외부 데이터 집합 사용

JupiterLab 환경에 데이터 업로드와 같은 외부 데이터 세트를 사용하는 방법에 대한 자세한 내용은 노트북을 사용하여 데이터 [분석에 대한 자습서를 참조하십시오](../jupyterlab/analyze-your-data.md#external-data).

### 새 데이터 집합 만들기

실시간 시스템 학습에서 사용할 데이터 세트를 새로 만들려면 데이터 세트에 대한 데이터 스키마가 필요합니다. 그런 다음 만든 스키마를 사용하여 데이터를 인제스트해야 합니다. 다음 자습서를 사용하여 플랫폼에 대한 데이터 세트를 만들고 채울 수 있습니다.

- [API에서 데이터 세트 만들기 및 채우기](../../catalog/datasets/create.md)
- [UI에서 데이터 세트 만들기 및 채우기](../../ingestion/tutorials/ingest-batch-data.md)

## Git 및 Docker

데이터 과학 작업 공간 레서피 워크플로우를 사용하여 모델을 교육하려는 경우 Git 및 Docker가 필요합니다.

>[!NOTE]
>Python 노트북을 사용하여 모델을 교육하거나 자신만의 ONNX 모델을 사용하는 경우에는 Git 및 Docker를 다운로드할 필요가 없습니다.

- [Git 설치 가이드](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Docker 설치 가이드](https://docs.docker.com/get-docker/)

## 다음 단계

실시간 머신 러닝을 위한 데이터를 준비했다면 모델 [](./training-ml-model.md) 트레이닝의 튜토리얼을 따라 ONNX 모델을 만들고 Real-time Machine Learning 모델 스토어에 업로드하는 방법을 학습합니다.

