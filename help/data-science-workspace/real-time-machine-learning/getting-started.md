---
keywords: Experience Platform;개발자 안내서;데이터 과학 작업 공간;인기 항목;실시간 머신 러닝
solution: Experience Platform
title: 실시간 머신 러닝 시작
description: 다음 문서에서는 Adobe Experience Platform에서 실시간 기계 학습 모델을 만드는 데 필요한 단계를 간략하게 설명합니다.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 실시간 머신 러닝 시작(알파)

>[!IMPORTANT]
>
>아직 모든 사용자가 실시간 기계 학습을 사용할 수 없습니다. 이 기능은 알파 상태이며 아직 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

실시간 머신 러닝을 활용하려면 Adobe Experience Platform이 제공하는 조직에 액세스 권한이 있어야 합니다. [!DNL Data Science Workspace]. 또한 교육 및 점수에 사용할 전체 데이터 세트가 있어야 합니다.

실시간 기계 학습 가이드는 파이톤 3에 대한 작업 이해를 필요로 합니다. [Jupiter 노트북](../jupyterlab/overview.md), 데이터 과학 및 머신 러닝

**주요 용어:**

- **DSL:** 도메인별 언어
- **Edge:** 실시간 기계 학습 점수 서비스는 활성화 및 응용 프로그램에 가까운 Edge 클러스터에서 실행할 수 있습니다.
- **허브:** 현재 알파는 Adobe Experience Platform Hub에서 실시간 기계 학습 점수 서비스를 실행하는 반면, Experience Edge 네트워크는 개발 중입니다.
- **노드:** 노드는 그래프가 형성된 기본 단위입니다. 각 노드는 특정 작업을 수행하며 링크를 사용하여 함께 체인으로 연결하여 ML 파이프라인을 나타내는 그래프를 구성할 수 있습니다. 노드에 의해 수행되는 작업은 데이터나 스키마의 변형 또는 학습유추와 같은 입력 데이터에 대한 작업을 나타냅니다. 이 노드는 변환 또는 유추된 값을 다음 노드에 출력합니다.

## Adobe Experience Platform의 데이터 세트

실시간 머신 러닝을 사용하려면 데이터 세트에 액세스할 수 있어야 합니다. 외부 데이터 세트를 사용하고 업로드하는 옵션이 있습니다 [!DNL JupyterLab] 아직 수행하지 않았다면 Platform 내에서 새 데이터 세트를 만들거나 만들 수 있습니다.

>[!NOTE]
>
>이미 사용하려는 데이터 세트가 있는 경우 을 건너뛸 수 있습니다 [다음 단계](#next-steps).

### 외부 데이터 세트 사용

에 데이터 업로드와 같은 외부 데이터 세트를 사용하는 방법에 대해 자세히 알아보려면 [!DNL JupyterLab] 환경에서 다음 자습서를 참조하십시오. [전자 필기장을 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md#external-data).

### 새 데이터 세트 만들기

실시간 시스템 학습에서 사용할 새 데이터 세트를 만들려면 데이터 세트에 대한 데이터 스키마가 필요합니다. 그런 다음 생성한 스키마를 사용하여 데이터를 수집해야 합니다. 다음 자습서를 사용하여 데이터 세트를 만들고 채울 수 있습니다 [!DNL Platform]:

- [API에서 데이터 세트를 만들고 채웁니다](../../catalog/datasets/create.md)
- [UI에서 데이터 세트 만들기 및 채우기](../../ingestion/tutorials/ingest-batch-data.md)

## 다음 단계 {#next-steps}

실시간 머신 러닝을 위해 데이터를 준비했으면 다음을 수행하여 시작하십시오 [실시간 기계 학습 노트북 사용 안내서](./rtml-authoring-notebook.md) ONNX 모델을 만들고 실시간 머신 러닝 모델 스토어에 업로드하는 방법을 알아봅니다.
