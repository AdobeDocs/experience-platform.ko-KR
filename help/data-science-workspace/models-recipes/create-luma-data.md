---
keywords: Experience Platform;luma 웹 데이터;Data Science Workspace;인기 항목;레서피;데모 데이터;데모 웹 데이터;luma 데이터
solution: Experience Platform
title: Luma 웹 스키마 및 데이터 세트 만들기
type: Tutorial
description: 이 자습서에서는 Luma 데모 성향 모델에 필요한 사전 요구 사항과 자산을 제공합니다.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Luma 성향 모델 스키마 및 데이터 세트 만들기

이 자습서에서는 다른 모든 항목에 필요한 사전 요구 사항과 자산을 제공합니다 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 튜토리얼. 완료되면 사용자 및 IMS 조직에서 다음 스키마와 데이터 세트를 사용할 수 있습니다.

**스키마:**

- Luma 웹 데이터 스키마
- 성향 모델 점수 결과 스키마

**데이터 세트:**

- Luma 웹 데이터 세트
- 성향 모델 교육 데이터 세트
- 성향 모델 점수 데이터 세트
- 성향 모델 점수 결과 데이터 세트

## 자산 다운로드 {#assets}

다음 자습서에서는 사용자 지정 Luma 구매 성향 모델을 사용합니다. 계속하기 전에 [필요한 자산 다운로드](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) zip 폴더. 이 폴더에는 다음이 포함되어 있습니다.

- 구매 성향 모델 노트북
- 교육 및 점수 데이터 세트에 데이터를 수집하는 데 사용되는 노트북(Luma 웹 데이터의 하위 집합)
- 730,000명의 Luma 사용자의 웹 데이터가 포함된 데모 JSON 파일
- 웹 데이터 및 모델을 이해하는 데 도움이 되는 Python 3 EDA(예비 데이터 분석) 노트북(선택 사항)

>[!NOTE]
>
> 자습서에 고유한 스키마와 데이터를 사용할 수 있습니다. 그러나 자산에 제공된 데모 모델은 적절한 구성 파일 및 요구 사항 파일을 제공하지 않는 한 작동하지 않습니다. 이 데모 성향 모델은 Luma 웹 데이터와 작동하도록 디자인되었습니다.

### Luma 웹 데이터 스키마를 만들고 데이터를 수집합니다

모델을 만들려면 모델을 교육하고 점수를 매기는 데 사용되는 Platform의 데이터 세트가 있어야 합니다. 다음 비디오 자습서는 [데이터 과학 작업 공간 교육 과정](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) 는 Luma 스키마를 만들고 구매 성향 모델에 사용되는 데이터를 수집하는 과정을 안내합니다.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### 교육, 점수 책정 및 점수 결과 데이터 세트 만들기

레서피 빌더 전자 필기장을 실행하거나 API를 사용하여 모델을 교육하고 점수를 매기려면 교육/점수에 사용되는 데이터 세트와 스키마를 지정해야 합니다. 다음 비디오 자습서에서는 Luma 구매 성향 모델에 사용되는 점수 결과 스키마뿐만 아니라 교육, 점수 및 점수 결과 데이터 세트를 설정하는 과정을 안내합니다.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## 다음 단계

이 자습서를 따라 Luma 성향 모델에 필요한 스키마 및 데이터 세트를 만들었습니다. 이제 다음 자습서를 계속 진행하고 다음 자습서를 사용하여 모델을 만들 수 있습니다. [레시피 빌더 노트북](../jupyterlab/create-a-model.md) 자습서입니다.

또한 제공된 EDA(Survey Data Analysis) 전자 필기장을 사용하여 데이터를 탐색할 수 있습니다. 이 전자 필기장은 Luma 데이터의 패턴을 이해하고, 데이터 안전성을 확인하고, 예측 성향 모델에 대한 관련 데이터를 요약하는 데 사용할 수 있습니다. 예비 데이터 분석에 대해 자세히 알아보려면 [EDA 설명서](../jupyterlab/eda-notebook.md).
