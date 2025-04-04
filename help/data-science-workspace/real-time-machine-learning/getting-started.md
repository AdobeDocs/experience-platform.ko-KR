---
keywords: Experience Platform;개발자 안내서;Data Science Workspace;인기 주제;실시간 머신 러닝;
solution: Experience Platform
title: 실시간 머신 러닝 시작하기
description: 다음 문서에서는 Adobe Experience Platform에서 실시간 머신 러닝 모델을 만드는 데 필요한 단계에 대해 간략히 설명합니다.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# 실시간 머신 러닝 시작하기(Alpha)

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

>[!IMPORTANT]
>
>아직 모든 사용자가 실시간 머신 러닝을 사용할 수 있는 것은 아닙니다. 이 기능은 알파에 있으며 아직 테스트 중입니다. 이 문서는 변경될 수 있습니다.

실시간 머신 러닝을 활용하려면 Adobe Experience Platform 및 [!DNL Data Science Workspace]&#x200B;(으)로 프로비저닝된 조직에 액세스할 수 있어야 합니다. 또한 교육 및 채점에 사용할 전체 데이터 세트가 있어야 합니다.

실시간 머신 러닝을 위한 가이드에는 Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), 데이터 과학 및 머신 러닝에 대한 작업 이해가 필요합니다.

**주요 용어:**

- **DSL:** 도메인별 언어.
- **Edge:** 실시간 머신 러닝 채점 서비스는 활성화 및 응용 프로그램과 더 가까운 Edge 클러스터에서 실행할 수 있습니다.
- **허브:** Edge Network이 개발 중인 동안 현재 알파는 Adobe Experience Platform 허브에서 실시간 머신 러닝 점수 서비스를 실행하고 있습니다.
- **노드:** 노드는 그래프가 형성되는 기본 단위입니다. 각 노드는 특정 작업을 수행하고 링크를 사용하여 서로 체인화되어 ML 파이프라인을 나타내는 그래프를 형성할 수 있습니다. 노드에 의해 수행되는 태스크는 데이터 또는 스키마의 변환, 또는 머신 러닝 추론과 같은 입력 데이터에 대한 동작을 나타낸다. 상기 노드는 상기 변환된 또는 추론된 값을 다음 노드(들)로 출력한다.

## Adobe Experience Platform의 데이터 세트

실시간 머신 러닝을 사용하려면 데이터 세트에 액세스할 수 있어야 합니다. 외부 데이터 세트를 사용하여 [!DNL JupyterLab] 환경에 업로드하거나 Experience Platform 내에서 새 데이터 세트를 만들 수 있는 옵션이 있습니다.

>[!NOTE]
>
>사용하려는 데이터 세트가 이미 있는 경우 [다음 단계](#next-steps)로 건너뛸 수 있습니다.

### 외부 데이터 세트 사용

[!DNL JupyterLab] 환경에 데이터를 업로드하는 것과 같은 외부 데이터 집합을 사용하는 방법에 대한 자세한 내용은 [Notebooks를 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md#external-data)의 자습서를 참조하십시오.

### 새 데이터 세트 만들기

실시간 머신 러닝에서 사용할 새 데이터 세트를 만들려면 데이터 세트에 대한 데이터 스키마가 필요합니다. 그런 다음 생성한 스키마를 사용하여 데이터를 수집해야 합니다. 다음 튜토리얼을 사용하여 [!DNL Experience Platform]에 대한 데이터 집합을 만들고 채웁니다.

- [API에서 데이터 세트 만들기 및 채우기](../../catalog/datasets/create.md)
- [UI에서 데이터 세트 만들기 및 채우기](../../ingestion/tutorials/ingest-batch-data.md)

## 다음 단계 {#next-steps}

실시간 기계 학습을 위한 데이터를 준비했으면 먼저 [실시간 기계 학습 전자 필기장 사용 안내서](./rtml-authoring-notebook.md)에 따라 ONNX 모델을 만들고 실시간 기계 학습 모델 저장소에 업로드하는 방법을 알아봅니다.
