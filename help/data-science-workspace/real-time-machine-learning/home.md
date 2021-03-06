---
keywords: Experience Platform;개발자 가이드;데이터 과학 작업 공간;인기 있는 주제;실시간 기계 학습;
solution: Experience Platform
title: 실시간 기계 학습 개요
topic-legacy: Overview
description: 실시간 머신 러닝을 사용하면 최종 사용자에게 디지털 경험 컨텐츠의 연관성을 크게 향상시킬 수 있습니다. 이는 Experience Edge의 실시간 컨퍼런싱과 지속적인 학습을 통해 가능합니다.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 실시간 기계 학습 개요(알파)

>[!IMPORTANT]
>
>아직 모든 사용자는 실시간 기계 학습을 사용할 수 없습니다. 이 기능은 알파 버전이며 여전히 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

실시간 머신 러닝을 사용하면 최종 사용자에게 디지털 경험 컨텐츠의 연관성을 크게 향상시킬 수 있습니다. 이것은 [!DNL Experience Edge]에 대한 실시간 참조와 지속적인 학습을 활용함으로써 가능합니다.

허브와 [!DNL Edge]에 대한 매끄러운 계산으로 인해 관련이 있고 응답성이 높은 고도로 개인화된 경험을 제공하기 위해 전통적으로 수반되는 지연이 크게 줄어듭니다. 따라서 실시간 머신 러닝을 사용하면 동기 의사 결정을 위한 지연 시간이 매우 짧은 환경 설정을 경험할 수 있습니다. 예를 들어 맞춤형 웹 페이지 컨텐츠를 렌더링하거나 제안 또는 할인 정보를 표시하여 웹 스토어의 이탈률을 줄이고 전환율을 높일 수 있습니다.

## 실시간 기계 학습 아키텍처 {#architecture}

다음 다이어그램은 실시간 기계 학습 아키텍처에 대한 개요를 제공합니다. 현재 알파 버전은 보다 간소화되었습니다.

![알파 아치](../images/rtml/alpha-arch.png)

![간소화된 개요](../images/rtml/end-to-end-arch.png)

## 실시간 기계 학습 워크플로우

다음 워크플로우에서는 실시간 기계 학습 모델을 만들고 활용하는 데 관련된 일반적인 단계와 결과를 간략하게 설명합니다.

### 데이터 수집 및 준비

Adobe Experience Platform의 [!DNL Experience Data Model](XDM)을 사용하여 데이터를 인제스트하고 변환합니다. 이 데이터는 모델 교육에 사용됩니다. XDM에 대한 자세한 내용은 [XDM 개요](../../xdm/home.md)를 참조하십시오.

### 작성

처음부터 제작하거나 Adobe Experience Platform Jupiter Notebook에서 사전에 교육받은 ONNX 모델로 활용하여 실시간 머신 러닝 모델을 제작할 수 있습니다.

### 배포

예측 API 끝점을 사용하여 [!UICONTROL Service Gallery]에서 실시간 기계 학습 서비스를 만들려면 모델을 [!DNL Experience Edge]에 배포합니다.

### 추론

예측 REST API 끝점을 사용하여 기계 학습 인사이트를 실시간으로 생성합니다.

### 게재

그러면 마케터는 Adobe Target을 사용하여 실시간 기계 학습 점수를 경험에 매핑하는 세그먼트와 규칙을 정의할 수 있습니다. 이렇게 하면 브랜드 웹 사이트 방문자가 동일한 페이지 또는 다음 페이지에 고도로 개인화된 경험을 실시간으로 표시할 수 있습니다.

## 현재 기능

실시간 기계 학습은 현재 알파 버전을 통해 제공되고 있습니다. 아래에 설명된 기능은 더 많은 기능과 노드를 사용할 수 있으므로 변경될 수 있습니다.

>[!NOTE]
>
> 알파 제한:
> - 현재 ONNX 기반 모델만 지원됩니다.
> - 노드에 사용된 함수를 직렬화할 수 없습니다. 예를 들어 판다 노드에 사용되는 람다 함수입니다.
> - [!DNL Edge] 배포가 수동으로 완료된 후 20초 동안 잠깁니다.
> - 심층 학습을 위해 데이터를 전송하여 `df.values`을 호출하면 DL 모델에서 허용하는 배열을 반환합니다. 이것은 ONNX 모델 채점 노드가 `df.values`을 사용하고 해당 모델에 대해 점수를 매기도록 출력을 보내기 때문입니다.



### 기능:

|  | 알파(5월) |
| --- | --- |
| **기능** | - RTML 노트북 템플릿 사용, 사용자 정의 머신 러닝 모델 작성, 테스트 및 배포 <br> - 미리 교육된 머신 러닝 모델 가져오기 지원 <br> - 실시간 머신 러닝 SDK <br> - 저작 노드의 시작 집합. <br> - Adobe Experience Platform 허브에 배포됨. |
| **사용 가능** | 북미 |
| **작성 노드** | - Pendans <br> - ScikitLearn <br> - ONNXNode <br> - 분할 <br> - ModelUpload <br> - OneHotEncoder |
| **점수 지정 실행 시간** | ONNX |

## 다음 단계

[시작하기](./getting-started.md) 가이드를 따라 시작할 수 있습니다. 이 안내서에서는 실시간 기계 학습 모델을 만드는 데 필요한 모든 사전 요구 사항을 설정하는 과정을 안내합니다.
