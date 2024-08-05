---
keywords: Experience Platform;스키마 데이터 미리 보기;데이터 과학 Workspace;인기 있는 주제
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 미리 보기
type: Tutorial
description: 다음 문서에서는 Adobe Experience Platform에서 스키마 및 데이터 세트를 미리 보는 방법에 대해 간략하게 설명합니다.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 3%

---

# 소매 판매 스키마 및 데이터 세트 미리 보기

>[!NOTE]
>
>Data Science Workspace은 더 이상 구입할 수 없습니다.
>
>이 설명서는 Data Science Workspace에 대한 이전 권한이 있는 기존 고객을 대상으로 합니다.

[소매 판매 스키마 및 데이터 세트](./create-retails-sales-dataset.md) 자습서에서 부트스트랩 스크립트가 성공적으로 완료되면. [!DNL Experience Platform]에서 출력 스키마와 데이터 세트를 볼 수 있습니다. 스키마 및 데이터 세트를 보려면 아래 단계를 따르십시오.

왼쪽 탐색에 있는 **[!UICONTROL 스키마]** 탭을 선택하고 부트스트랩 스크립트로 만든 입력 스키마를 찾습니다. 스키마 이름은 이전 단계의 `config.yaml`에 정의된 이름과 일치합니다. 을 클릭하여 스키마 세부 정보 및 구성을 확인합니다.

![](../images/models-recipes/access-data/schema.PNG)

왼쪽 탐색에 있는 **[!UICONTROL 데이터 세트]** 탭을 선택하고 데이터 세트 이름을 선택하여 만든 입력 데이터 세트를 엽니다. 데이터 집합 이름은 이전 단계의 `config.yaml`에 정의된 이름과 같습니다.

![](../images/models-recipes/access-data/dataset.PNG)

데이터 집합의 하위 집합을 미리 보려면 오른쪽 상단의 **[!UICONTROL 데이터 집합 미리 보기]**&#x200B;를 선택하십시오.

![](../images/models-recipes/access-data/preview.PNG)

## 다음 단계

제공된 부트스트랩 스크립트를 사용하여 소매 판매 샘플 데이터를 [!DNL Experience Platform]에 수집했습니다.

수집된 데이터로 작업을 계속하려면 다음을 수행합니다.
- [Jupyter Notebooks를 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - [!DNL Data Science Workspace]의 Jupyter Notebooks를 사용하여 데이터에 액세스하고, 탐색하고, 시각화하고, 이해할 수 있습니다.
- [소스 파일을 레시피에 패키징](./package-source-files-recipe.md)
   - 가져오기 가능한 레시피 파일에 소스 파일을 패키지하여 자신의 모델을 [!DNL Data Science Workspace](으)로 가져오는 방법을 알아보려면 이 자습서를 따르십시오.
