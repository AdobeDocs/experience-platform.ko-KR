---
keywords: Experience Platform;스키마 데이터 미리 보기;데이터 과학 작업 공간;인기 있는 항목
solution: Experience Platform
title: 소매 판매 스키마 및 데이터 세트 미리 보기
type: Tutorial
description: 다음 문서에서는 Adobe Experience Platform에서 스키마 및 데이터 세트를 미리 보는 방법에 대해 설명합니다.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 소매 판매 스키마 및 데이터 세트 미리 보기

부트스트랩 스크립트가 성공적으로 완료된 경우 [소매 판매 스키마 및 데이터 세트](./create-retails-sales-dataset.md) 자습서입니다. 출력 스키마와 데이터 세트는 [!DNL Experience Platform]. 스키마 및 데이터 세트를 보려면 아래 절차를 따르십시오.

을(를) 선택합니다 **[!UICONTROL 스키마]** 왼쪽 탐색에 있는 탭에서 부트스트랩 스크립트로 만든 입력 스키마를 찾습니다. 스키마 이름은 `config.yaml` 이전 단계에서 제거합니다. 를 클릭하여 스키마 세부 사항 및 스키마 구성 요소를 확인합니다.

![](../images/models-recipes/access-data/schema.PNG)

을(를) 선택합니다 **[!UICONTROL 데이터 세트]** 왼쪽 탐색에 있는 탭에서 데이터 세트의 이름을 선택하여 만든 입력 데이터 세트를 엽니다. 데이터 집합 이름은 `config.yaml` 이전 단계에서 제거합니다.

![](../images/models-recipes/access-data/dataset.PNG)

선택 **[!UICONTROL 데이터 집합 미리 보기]** 데이터 집합 하위 집합을 미리 보기 위해 오른쪽 상단에 있습니다.

![](../images/models-recipes/access-data/preview.PNG)

## 다음 단계

이제 소매 판매 샘플 데이터를에 성공적으로 수집했습니다. [!DNL Experience Platform] 제공된 부트스트랩 스크립트 사용.

수집된 데이터로 계속 작업하려면:
- [Jupiter 노트북을 사용하여 데이터 분석](../jupyterlab/analyze-your-data.md)
   - 에서 Jupiter 노트북 사용 [!DNL Data Science Workspace] 데이터 액세스, 탐색, 시각화 및 이해
- [배합식에 소스 파일 패키지](./package-source-files-recipe.md)
   - 이 자습서에 따라 고유한 모델을 [!DNL Data Science Workspace] 가져오기 가능한 레서피 파일에 소스 파일을 패키징하여
