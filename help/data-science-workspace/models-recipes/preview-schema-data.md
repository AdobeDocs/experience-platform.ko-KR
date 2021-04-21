---
keywords: Experience Platform;스키마 데이터 미리 보기;데이터 과학 작업 공간;인기 항목
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 미리 보기
topic-legacy: tutorial
type: Tutorial
description: 다음 문서에서는 Adobe Experience Platform에서 스키마 및 데이터 세트를 미리 볼 수 있는 개요를 설명합니다.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 소매 판매 스키마 및 데이터 세트 미리 보기

[소매 판매 스키마 및 데이터 세트](./create-retails-sales-dataset.md) 자습서에서 부트스트랩 스크립트가 성공적으로 완료되면 출력 스키마 및 데이터 세트는 [!DNL Experience Platform]에서 볼 수 있습니다. 스키마 및 데이터 세트를 보려면 아래 절차를 따르십시오.

왼쪽 탐색에 있는 **[!UICONTROL Schemas]** 탭을 선택하고 부트스트랩 스크립트에서 만든 입력 스키마를 찾습니다. 스키마의 이름은 이전 단계에서 `config.yaml`에 정의된 내용과 일치합니다. 스키마 세부 사항을 클릭하여 확인하고 컴포지션을 표시합니다.

![](../images/models-recipes/access-data/schema.PNG)

왼쪽 탐색에 있는 **[!UICONTROL Datasets]** 탭을 선택하고 데이터 세트 이름을 선택하여 만든 입력 데이터 세트를 엽니다. 데이터 세트의 이름은 이전 단계에서 `config.yaml`에 정의된 내용에 해당합니다.

![](../images/models-recipes/access-data/dataset.PNG)

데이터 집합의 하위 집합을 미리 보려면 오른쪽 상단에 있는 **[!UICONTROL Preview Dataset]**&#x200B;을 선택합니다.

![](../images/models-recipes/access-data/preview.PNG)

## 다음 단계

제공된 부트스트랩 스크립트를 사용하여 소매 판매 샘플 데이터를 [!DNL Experience Platform]에 인제스트했습니다.

인제스트된 데이터로 계속 작업하려면:
- [Jupiter 노트북을 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - [!DNL Data Science Workspace]의 Jupiter 노트북을 사용하여 데이터를 액세스, 탐색, 시각화 및 이해할 수 있습니다.
- [소스 파일을 레서피에 패키지화](./package-source-files-recipe.md)
   - 이 자습서에 따라 소스 파일을 가져올 수 있는 레서피 파일에 패키징하여 자신의 모델을 [!DNL Data Science Workspace]으로 가져오는 방법을 알아보십시오.
