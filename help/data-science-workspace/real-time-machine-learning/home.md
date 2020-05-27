---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 실시간 머신 러닝 개요
topic: Overview
translation-type: tm+mt
source-git-commit: 626bb7a0856a663e235ecd2b19954f4617fe9b6f
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 1%

---


# 실시간 기계 학습 개요(알파)

>[!IMPORTANT]
>모든 사용자는 아직 실시간 머신 러닝을 사용할 수 없습니다. 이 기능은 알파에 있으며 여전히 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

실시간 머신 러닝은 최종 사용자에게 디지털 경험 컨텐츠의 연관성을 크게 향상시킬 수 있습니다. 이는 Adobe Experience Edge에서 실시간 검토 및 지속적인 학습을 활용함으로써 가능합니다.

허브와 에지(Edge) 모두에서 매끄러운 계산으로 인해 관련이 있고 응답성이 높은 고도로 개인화된 경험을 제공하기 위해 전통적으로 관련된 지연이 크게 줄어듭니다. 따라서 실시간 머신 러닝은 동기적 의사 결정을 위한 매우 낮은 지연율을 제공합니다. 예를 들어 맞춤형 웹 페이지 컨텐츠를 렌더링하거나 제안 또는 할인을 적용하여 웹 스토어의 가입/구매 전환율을 높이고 구매 전환율을 향상시킬 수 있습니다.

## 실시간 머신 러닝 아키텍처 {#architecture}

다음 다이어그램은 실시간 기계 학습 아키텍처에 대한 개요를 제공합니다. 현재 알파 버전은 보다 간소화되었습니다.

![알파 아치](../images/rtml/alpha-arch.png)

![간소화된 개요](../images/rtml/end-to-end-arch.png)

## 실시간 머신 러닝 워크플로우

다음 워크플로우에서는 실시간 기계 학습 모델을 만들고 활용하는 데 필요한 일반적인 단계와 결과를 간략하게 설명합니다.

### 자료 수집 및 준비

Adobe Experience Platform의 XDM(Experience Data Model)을 통해 데이터를 수집하여 변환할 수 있습니다. 이 데이터는 모델 교육에 사용됩니다. XDM에 대한 자세한 내용은 [XDM 개요를 참조하십시오](../../xdm/home.md).

### 작성

처음부터 제작하거나 Adobe Experience Platform Jupiter Notebook에서 사전에 교육받은 ONNX 모델로 활용하여 실시간 머신 러닝 모델을 제작할 수 있습니다.

### 배포

Experience Edge에 모델을 배포하여 예측 API 끝점을 사용하여 서비스 갤러리에서 실시간 기계 학습 서비스를 만듭니다.

### 추론

예측 REST API 종단점을 사용하여 머신 러닝 인사이트를 실시간으로 생성할 수 있습니다.

### 게재

그런 다음 마케터는 Adobe Target을 사용하여 실시간 기계 학습 점수를 경험에 매핑하는 세그먼트와 규칙을 정의할 수 있습니다. 이를 통해 브랜드 웹 사이트 방문자에게 매우 개인화된 동일한 경험 또는 다음 페이지를 실시간으로 표시할 수 있습니다.

## 현재 기능

실시간 머신 러닝은 현재 알파에 포함되어 있습니다. 아래 설명된 기능은 더 많은 기능과 노드가 사용 가능하므로 변경될 수 있습니다.

>[!NOTE]
> 알파 제한:
> - 현재 ONNX 기반 모델만 지원됩니다.
> - 노드에 사용된 함수를 직렬화할 수 없습니다. 예를 들어 팬더 노드에서 사용되는 람다 함수입니다.
> - Edge 배포를 수동으로 수행한 후 20초 동안 재활용할 수 있습니다.
> - 심층적인 학습을 위해서는 데이터를 DL 모델에서 허용하는 어레이 `df.values` 를 반환하는 방식으로 전송해야 합니다. 이것은 ONNX 모델 점수 지정 노드가 모델을 기준으로 점수를 매기도록 출력을 사용하고 `df.values` 보내기 때문입니다.



### 기능:

|  | 알파(5월) |
| --- | --- |
| **기능** | - RTML 노트북 템플릿 사용, 사용자 정의 머신 러닝 모델 작성, 테스트 및 배포 <br> - 미리 교육된 머신 러닝 모델 가져오기 지원 <br> - 실시간 머신 러닝 SDK <br> - 작성 노드의 시작 집합. <br> - Adobe Experience Platform 허브에 배포 |
| **가용성** | 북미 |
| **작성 노드** | - 판다 <br> - ScitkitLearn <br> - ONNXN 코드 <br> - 분할 <br> - ModelUpload <br> - OneHotEncoder |
| **점수 지정 실행 시간** | ONNX |

## 다음 단계

시작 [가이드를 따라 시작할](./getting-started.md) 수 있습니다. 이 안내서에서는 실시간 기계 학습 모델을 만드는 데 필요한 모든 사전 요구 사항을 설정하는 과정을 안내합니다.

