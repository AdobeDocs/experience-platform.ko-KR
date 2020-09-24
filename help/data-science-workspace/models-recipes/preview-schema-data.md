---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: 스키마 및 데이터 집합 미리 보기
topic: tutorial
type: Tutorial
description: 다음 문서에서는 Adobe Experience Platform에서 스키마 및 데이터 세트를 미리 볼 수 있는 개요를 설명합니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# 스키마 및 데이터 집합 미리 보기

소매 판매 스키마 만들기 및 데이터 세트 [](./create-retails-sales-dataset.md) 자습서에서 부트스트랩 스크립트를 성공적으로 완료한 경우 출력 스키마 및 데이터 세트를 볼 수 있습니다 [!DNL Experience Platform]. 스키마 및 데이터 세트를 보려면 아래 단계를 따르십시오.

1. 왼쪽 탐색 열에 있는 **[!UICONTROL 스키마]** 링크를 클릭하고 부트스트랩 스크립트를 통해 생성된 입력 스키마를 찾습니다. 스키마의 이름은 이전 단계에서 정의된 내용과 `config.yaml` 일치합니다. 스키마 세부 사항 및 구성 요소를 클릭하여 확인합니다.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. 왼쪽 탐색 열에 있는 **[!UICONTROL 데이터 집합]** 링크를 클릭하고 목록의 이름을 클릭하여 만든 입력 데이터 집합을 엽니다. 데이터 세트의 이름은 이전 단계에서 정의된 내용과 `config.yaml` 일치합니다.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. 오른쪽 **[!UICONTROL 상단에 있는 데이터 세트]** 미리 보기를 클릭하여 데이터 세트 하위 집합을 미리 봅니다.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## 다음 단계

이제 제공된 부트스트랩 스크립트를 사용하여 소매 세일즈 샘플 데이터 [!DNL Experience Platform] 를 인제스트했습니다.

인제스트된 데이터로 계속 작업하려면:
- [Jupiter 노트북을 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - Jupiter 노트북을 사용하여 데이터 [!DNL Data Science Workspace] 를 액세스, 탐색, 시각화 및 이해할 수 있습니다.
- [소스 파일을 레서피로 패키지](./package-source-files-recipe.md)
   - 이 자습서에 따라 소스 파일을 가져올 수 있는 레시피 파일 [!DNL Data Science Workspace] 에 패키징하여 자신만의 모델을 가져오는 방법을 살펴볼 수 있습니다.