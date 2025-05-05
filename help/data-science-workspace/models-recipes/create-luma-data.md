---
keywords: Experience Platform;luma 웹 데이터;Data Science Workspace;인기 주제;레서피;데모 데이터;데모 웹 데이터;luma 데이터
solution: Experience Platform
title: Luma 웹 스키마 및 데이터 세트 만들기
type: Tutorial
description: 이 자습서에서는 Luma 데모 성향 모델에 필요한 사전 요구 사항 및 에셋을 제공합니다.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Luma 성향 모델 스키마 및 데이터 세트 만들기

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

이 자습서에서는 다른 모든 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 자습서에 필요한 사전 요구 사항 및 자산을 제공합니다. 완료되면 사용자와 조직에서 다음 스키마와 데이터 세트를 사용할 수 있습니다.

**스키마:**

- Luma 웹 데이터 스키마
- 성향 모델 점수 결과 스키마

**데이터 세트:**

- Luma 웹 데이터 세트
- 성향 모델 교육 데이터 세트
- 성향 모델 점수 데이터 세트
- 성향 모델 점수 결과 데이터 세트

## 에셋 다운로드 {#assets}

다음 자습서에서는 사용자 지정 Luma 구매 성향 모델을 사용합니다. 계속하기 전에 [필요한 에셋을 다운로드](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip) zip 폴더를 다운로드하십시오. 이 폴더에는 다음이 포함되어 있습니다.

- 구매 성향 모델 노트북
- 교육 및 채점 데이터 세트(Luma 웹 데이터의 하위 집합)로 데이터를 수집하는 데 사용되는 전자 필기장입니다
- 730,000명의 Luma 사용자의 웹 데이터를 포함하는 데모 JSON 파일
- 웹 데이터 및 모델을 이해하는 데 도움이 되는 Python 3 EDA(탐색적 데이터 분석) 노트북(선택 사항)입니다.

>[!NOTE]
>
> 모든 자습서에 고유한 스키마와 데이터를 사용할 수 있습니다. 그러나 에셋에 제공된 데모 모델은 적절한 구성 파일 및 요구 사항 파일을 제공하지 않으면 작동하지 않습니다. 이 데모 성향 모델은 Luma 웹 데이터에서 작동하도록 설계되었습니다.

### Luma 웹 데이터 스키마를 만들고 데이터 수집

모델을 만들려면 모델을 교육하고 평가하는 데 사용되는 Experience Platform 데이터 세트가 있어야 합니다. [데이터 과학 Workspace 교육 과정](https://experienceleague.adobe.com/?lang=ko&recommended=ExperiencePlatform-U-1-2021.1.dsw)의 다음 비디오 튜토리얼에서는 Luma 스키마를 만들고 구매 성향 모델에서 사용하는 데이터를 수집하는 과정을 안내합니다.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### 교육, 채점 및 채점 결과 데이터 세트 만들기

레시피 빌더 전자 필기장을 실행하거나 API를 사용하여 모델을 교육하고 평가하려면 교육/점수에 사용되는 데이터 세트와 스키마를 지정해야 합니다. 다음 비디오 튜토리얼에서는 Luma 구매 성향 모델에 사용되는 점수 지정 결과 스키마뿐만 아니라 교육, 점수 지정 및 점수 지정 결과 데이터 세트를 설정하는 방법을 안내합니다.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## 다음 단계

이 자습서에 따라 Luma 성향 모델에 필요한 스키마 및 데이터 세트를 만들었습니다. 이제 다음 튜토리얼을 계속 진행하고 [레시피 빌더 전자 필기장](../jupyterlab/create-a-model.md) 튜토리얼을 사용하여 모델을 만들 준비가 되었습니다.

또한 제공된 EDA(Explorative Data Analysis) 노트북을 사용하여 데이터를 탐색할 수 있습니다. 이 전자 필기장을 사용하여 Luma 데이터의 패턴을 이해하고, 데이터의 유효성을 검사하며, 예측 성향 모델에 대한 관련 데이터를 요약할 수 있습니다. 탐색적 데이터 분석에 대한 자세한 내용은 [EDA 설명서](../jupyterlab/eda-notebook.md)를 참조하세요.
