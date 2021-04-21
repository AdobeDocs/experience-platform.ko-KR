---
keywords: Experience Platform;개발자 가이드;데이터 과학 작업 공간;인기 있는 주제;실시간 기계 학습;
solution: Experience Platform
title: 실시간 머신 러닝 시작하기
topic-legacy: Getting started
description: 다음 문서에서는 Adobe Experience Platform에서 실시간 기계 학습 모델을 만드는 데 필요한 단계를 간략하게 설명합니다.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 실시간 기계 학습 시작(알파)

>[!IMPORTANT]
>
>아직 모든 사용자는 실시간 기계 학습을 사용할 수 없습니다. 이 기능은 알파 버전이며 여전히 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

실시간 머신 러닝을 활용하려면 Adobe Experience Platform 및 [!DNL Data Science Workspace]으로 제공된 조직에 액세스해야 합니다. 또한 트레이닝 및 점수 매기기용으로 전체 데이터 세트를 사용할 수 있어야 합니다.

실시간 기계 학습을 위한 가이드는 Python 3, [Jupiter 노트북](../jupyterlab/overview.md), 데이터 과학 및 기계 학습에 대한 작업 이해를 필요로 합니다.

**주요 용어:**

- **DSL:** 도메인별 언어.
- **Edge:** 실시간 기계 학습 점수 서비스는 활성화 및 응용 프로그램에 가까운 Edge 클러스터에서 실행할 수 있습니다.
- **허브:** 현재 알파는 Experience Edge 네트워크가 개발 중인 동안 Adobe Experience Platform 허브에서 실시간 기계 학습 점수 지정 서비스를 실행 중입니다.
- **Node:** A Node는 그래프가 형성되는 기본 단위입니다. 각 노드는 특정 작업을 수행하고 ML 파이프라인을 나타내는 그래프를 형성하는 링크를 사용하여 함께 연결할 수 있습니다. 노드에서 수행하는 작업은 데이터 또는 스키마 변형 또는 기계 학습 유추와 같은 입력 데이터에 대한 작업을 나타냅니다. 이 노드는 변형되거나 유추된 값을 다음 노드로 출력합니다.

## Adobe Experience Platform의 데이터 세트

실시간 머신 러닝을 사용하려면 데이터 세트에 대한 액세스 권한이 있어야 합니다. 외부 데이터 세트를 사용하여 [!DNL JupyterLab] 환경에 업로드하거나 아직 추가하지 않은 경우 플랫폼 내에서 새 데이터 세트를 만들 수 있습니다.

>[!NOTE]
>
>사용할 데이터 세트가 이미 있는 경우 [다음 단계](#next-steps)로 건너뛸 수 있습니다.

### 외부 데이터 세트 사용

[!DNL JupyterLab] 환경에 데이터 업로드와 같은 외부 데이터 세트를 사용하는 방법에 대한 자세한 내용은 [전자 필기장](../jupyterlab/analyze-your-data.md#external-data)을 사용하여 데이터 분석에서 자습서를 참조하십시오.

### 새 데이터 세트 만들기

실시간 시스템 학습에서 사용할 데이터 세트를 새로 만들려면 데이터 세트에 대한 데이터 스키마가 필요합니다. 생성한 스키마를 사용하여 데이터를 인제스트해야 합니다. 다음 자습서를 사용하여 [!DNL Platform]의 데이터 세트를 만들고 채웁니다.

- [API에서 데이터 세트 만들기 및 채우기](../../catalog/datasets/create.md)
- [UI에서 데이터 세트 만들기 및 채우기](../../ingestion/tutorials/ingest-batch-data.md)

## 다음 단계 {#next-steps}

실시간 머신 러닝을 위한 데이터를 준비했으면 [실시간 머신 러닝 노트북 사용자 가이드](./rtml-authoring-notebook.md)에서 ONNX 모델을 만들고 실시간 머신 러닝 모델 스토어에 업로드하는 방법을 학습합니다.
