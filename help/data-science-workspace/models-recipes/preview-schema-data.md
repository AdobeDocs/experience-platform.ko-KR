---
keywords: Experience Platform;스키마 데이터 미리 보기;데이터 과학 작업 영역;자주 사용하는 항목
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 미리 보기
type: Tutorial
description: 다음 문서에서는 Adobe Experience Platform에서 스키마 및 데이터 세트를 미리 보는 방법에 대해 간략하게 설명합니다.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 소매 판매 스키마 및 데이터 세트 미리 보기

에서 부트스트랩 스크립트가 성공적으로 완료되면 [소매 판매 스키마 및 데이터 세트](./create-retails-sales-dataset.md) 튜토리얼. 출력 스키마 및 데이터 세트가에서 볼 수 있음 [!DNL Experience Platform]. 스키마 및 데이터 세트를 보려면 아래 단계를 따르십시오.

다음 항목 선택 **[!UICONTROL 스키마]** 왼쪽 탐색에 있는 탭에서 부트스트랩 스크립트로 만든 입력 스키마를 찾습니다. 스키마 이름은에 정의된 항목과 일치합니다 `config.yaml` 이전 단계에서 가져온 것입니다. 을 클릭하여 스키마 세부 정보 및 구성을 확인합니다.

![](../images/models-recipes/access-data/schema.PNG)

다음 항목 선택 **[!UICONTROL 데이터 세트]** 왼쪽 탐색에 있는 탭을 열고 데이터 세트 이름을 선택하여 만든 입력 데이터 세트를 엽니다. 데이터 세트의 이름은에 정의된 항목과 일치합니다 `config.yaml` 이전 단계에서 가져온 것입니다.

![](../images/models-recipes/access-data/dataset.PNG)

선택 **[!UICONTROL 데이터 세트 미리 보기]** 데이터 세트의 하위 집합을 미리 볼 수 있도록 오른쪽 상단에 있습니다.

![](../images/models-recipes/access-data/preview.PNG)

## 다음 단계

이제 소매 판매 샘플 데이터를에 성공적으로 수집했습니다. [!DNL Experience Platform] 제공된 부트스트랩 스크립트 사용.

수집된 데이터로 작업을 계속하려면 다음을 수행합니다.
- [Jupyter Notebooks를 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - 에서 Jupyter Notebooks 사용 [!DNL Data Science Workspace] 데이터에 액세스하고, 탐색하고, 시각화하고, 이해할 수 있습니다.
- [소스 파일을 레시피에 패키징](./package-source-files-recipe.md)
   - 이 튜토리얼을 따라 나만의 모델을 로 가져오는 방법을 알아봅니다. [!DNL Data Science Workspace] 가져온 레시피 파일에 소스 파일을 패키지하여.
