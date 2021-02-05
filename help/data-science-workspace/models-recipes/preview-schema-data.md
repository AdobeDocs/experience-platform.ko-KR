---
keywords: Experience Platform;스키마 데이터 미리 보기;데이터 과학 작업 공간;인기 항목
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 미리 보기
topic: tutorial
type: Tutorial
description: 다음 문서에서는 Adobe Experience Platform에서 스키마 및 데이터 세트를 미리 볼 수 있는 개요를 설명합니다.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 소매 판매 스키마 및 데이터 세트 미리 보기

[소매 판매 스키마 만들기](./create-retails-sales-dataset.md) 자습서에서 부트스트랩 스크립트가 성공적으로 완료되면 출력 스키마 및 데이터 세트는 [!DNL Experience Platform]에서 볼 수 있습니다. 스키마 및 데이터 세트를 보려면 아래 절차를 따르십시오.

1. 왼쪽 탐색 열에 있는 **[!UICONTROL 스키마]** 링크를 클릭하고 부트스트랩 스크립트에서 만든 입력 스키마를 찾습니다. 스키마의 이름은 이전 단계에서 `config.yaml`에 정의된 내용과 일치합니다. 스키마 세부 사항을 클릭하여 확인하고 컴포지션을 표시합니다.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. 왼쪽 탐색 열에 있는 **[!UICONTROL 데이터 집합]** 링크를 클릭하고 목록의 이름을 클릭하여 만든 입력 데이터 집합을 엽니다. 데이터 세트의 이름은 이전 단계에서 `config.yaml`에 정의된 것과 일치합니다.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. 오른쪽 상단의 데이터 세트 미리 보기&#x200B;]**를 클릭하여 데이터 세트 하위 집합을 미리 봅니다.**[!UICONTROL 

   ![](../images/models-recipes/access-data/preview_dataset.png)

## 다음 단계

제공된 부트스트랩 스크립트를 사용하여 소매 판매 샘플 데이터를 [!DNL Experience Platform]에 인제스트했습니다.

인제스트된 데이터로 계속 작업하려면:
- [Jupiter 노트북을 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - [!DNL Data Science Workspace]의 Jupiter 노트북을 사용하여 데이터를 액세스, 탐색, 시각화 및 이해할 수 있습니다.
- [소스 파일을 레서피에 패키지화](./package-source-files-recipe.md)
   - 이 자습서에 따라 소스 파일을 가져올 수 있는 레서피 파일에 패키징하여 자신의 모델을 [!DNL Data Science Workspace]으로 가져오는 방법을 알아보십시오.