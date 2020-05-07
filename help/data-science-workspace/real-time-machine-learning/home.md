---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 실시간 머신 러닝 개요
topic: Overview
translation-type: tm+mt
source-git-commit: ab8b000bec0ae30c695582f57c40105b7ca1f22f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---


# 실시간 머신 러닝 개요

>[!IMPORTANT]
>모든 사용자는 아직 실시간 머신 러닝을 사용할 수 없습니다. 이 기능은 알파에 있으며 여전히 테스트되고 있습니다. 이 문서는 변경될 수 있습니다.

Adobe Experience Platform의 실시간 머신 러닝 프레임워크를 사용하면 머신 러닝을 통해 정확한 타이밍에 적합한 최종 사용자에게 적합한 경험을 전달할 수 있으며, 이를 통해 짧은 시간에 적합한 채널을 확보할 수 있습니다.

## 이점

실시간 머신 러닝은 최종 사용자에게 디지털 경험 컨텐츠의 연관성을 크게 향상시킬 수 있습니다. 이는 Adobe Experience Edge에서 실시간 검토 및 지속적인 학습을 활용함으로써 가능합니다.

허브와 에지(Edge) 모두에서 매끄러운 계산으로 인해 관련이 있고 응답성이 높은 고도로 개인화된 경험을 제공하기 위해 전통적으로 관련된 지연이 크게 줄어듭니다. 따라서 실시간 머신 러닝은 동기적 의사 결정을 위한 매우 낮은 지연율을 제공합니다. 예를 들어 맞춤형 웹 페이지 컨텐츠를 렌더링하거나 제안 또는 할인을 적용하여 웹 스토어의 가입/구매 전환율을 높이고 구매 전환율을 향상시킬 수 있습니다.

## 실시간 머신 러닝 아키텍처

다음 다이어그램은 실시간 기계 학습 아키텍처에 대한 개요를 제공합니다.

![간소화된 개요](../images/rtml/simple-overview.png)

## 실시간 기계 학습 워크플로우(알파)

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

그런 다음 마케터는 Adobe Target을 사용하여 실시간 기계 학습 점수를 경험에 매핑하는 세그먼트와 규칙을 정의할 수 있습니다. 이를 통해 브랜드 웹 사이트 방문자가 100ms 이내에 동일한 페이지 또는 다음 페이지의 고도로 개인화된 경험을 실시간으로 표시할 수 있습니다.

## 개발 계획

실시간 머신 러닝은 현재 알파 단계에 있습니다. 아래 표는 향후 베타 반복에서 릴리스될 일부 기능 및 업데이트에 대해 설명합니다.

<table>
    <th></th>
    <th>알파(5월)</th>
    <th>베타</th>
    <tr>
        <td>
            <strong>기능</strong>
        </td>
        <td>
            <li>데이터 과학 작업 공간은 노트북 실행 프로그램 통합을 통해 고유한 모델과 작성자를 가져옵니다.</li>
            <li>제작 연산자 시작 세트입니다.</li>
            <li>허브에 배포</li>
            <li>Scykit 학습 기반의 모델을 참조하십시오.</li>
        </td>
        <td>
            <li>데이터 과학 작업 공간 서비스 갤러리 UI 통합.</li>
            <li>추론 결과를 통해 실시간 고객 프로파일을 자동으로 강화할 수 있습니다.</li>
            <li>심층 학습 모델</li>
            <li>사용자 지정 연산자를 비롯한 저작 연산자 세트가 확장되었습니다.</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>가용성</strong>
        </td>
        <td>
            북미
        </td>
        <td>
            <li>북미</li>
            <li>유럽 및 중동(EMEA)</li>
            <li>아시아 태평양(APAC)</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>작성</strong>
        </td>
        <td>
            <li>Python 지원</li>
            <li>실시간 머신 러닝 SDK</li>
            <li>Python 작성 노드: 판다, ScikitLearn, ONNXNode, Split, ModelUpload, OneHotEncoder.</li>
        </td>
        <td>
            <li>100%</li>
            <li>추가 Python 작성 노드: 실시간 고객 프로파일 리더, 실시간 고객 프로파일 작성기, 숫자 배열, XDM2Frame, Frame2XDM </li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>점수 지정 실행 시간</strong>
        </td>
        <td>
            ONNX
        </td>
        <td>
            ONNX
        </td>
    </tr>
</table>

## 다음 단계

시작 [가이드를 따라 시작할](./getting-started.md) 수 있습니다. 이 안내서에서는 실시간 기계 학습 모델을 만드는 데 필요한 모든 사전 요구 사항을 설정하는 과정을 안내합니다.

