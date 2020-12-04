---
keywords: Experience Platform;machine learning model;Data Science Workspace;Real-time Customer Profile;popular topics;machine learning insights
solution: Experience Platform
title: 머신 러닝 인사이트를 통해 실시간 고객 프로파일 강화
topic: tutorial
type: Tutorial
description: 이 문서에서는 머신 러닝 인사이트를 활용하여 실시간 고객 프로파일을 강화할 수 있는 단계별 튜토리얼을 제공하고, 다음 섹션으로 세분화된 단계를 통해 출력 스키마/데이터 세트를 만들고, 출력 스키마/데이터 세트를 구성하고, 세그먼트 빌더를 사용하여 세그먼트를 만들 수 있습니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---


# 머신 러닝 인사이트 [!DNL Real-time Customer Profile] 로 풍부한 내용 제작

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 머신 러닝 모델을 생성, 평가 및 활용하여 데이터 예측 및 인사이트를 생성할 수 있는 툴과 리소스를 제공합니다. 머신 러닝 인사이트를 [!DNL Profile]사용 가능한 데이터 세트에 인제스트할 때 동일한 데이터를 레코드와 인제스트하여 [!DNL Profile] 관련 요소의 하위 세트로 세그먼트화할 수 있습니다 [!DNL Experience Platform Segmentation Service].

이 문서에서는 머신 러닝 인사이트를 보완하기 위한 단계별 자습서 [!DNL Real-time Customer Profile] 를 제공하며 다음 섹션으로 나눌 수 있습니다.

1. [출력 스키마 및 데이터 집합 만들기](#create-an-output-schema-and-dataset)
2. [출력 스키마 및 데이터 집합 구성](#configure-an-output-schema-and-dataset)
3. [세그먼트 빌더를 사용하여 세그먼트 만들기](#create-segments-using-the-segment-builder)

## 시작하기

이 자습서에서는 데이터 인제스트 및 세그먼트 만들기와 관련된 다양한 측면 [!DNL Adobe Experience Platform] 에 대해 [!DNL Profile] 잘 알아야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL Real-time Customer Profile]](../../rtcdp/overview.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Identity Service]](../../identity-service/home.md):인제스트되고 있는 여러 데이터 소스의 ID를 플랫폼에 연결하여 사용할 수 있습니다. [!DNL Real-time Customer Profile]
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform(플랫폼)이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

위에 언급된 문서 외에도 스키마 및 스키마 편집기에 대한 다음 안내서도 검토하는 것이 좋습니다.

* [스키마 컴포지션의 기본 사항](../../xdm/schema/composition.md):XDM 스키마, 구성 블록, 원칙 및 사용할 스키마 작성에 대한 우수 사례를 설명합니다 [!DNL Experience Platform].
* [스키마 편집기 자습서](../../xdm/tutorials/create-schema-ui.md):내에서 스키마 편집기를 사용하여 스키마를 생성하는 자세한 지침을 제공합니다 [!DNL Experience Platform].

## 출력 스키마 및 데이터 집합 만들기 {#create-an-output-schema-and-dataset}

채점 인사이트를 통해 [!DNL Real-time Customer Profile] 를 향상시키는 첫 번째 단계는 데이터가 정의하는 실제 개체(예: 사람)를 파악하는 것입니다. 데이터에 대한 이해를 통해 관계형 데이터베이스를 디자인하는 것처럼 데이터에 의미가 있는 구조를 설명하고 디자인할 수 있습니다.

스키마 구성은 클래스를 할당하는 것으로 시작됩니다. 클래스는 스키마에 포함할 데이터의 동작 측면(레코드 또는 시간 시리즈)을 정의합니다. 이 섹션에서는 스키마 빌더를 사용하여 스키마를 생성하는 기본 지침을 제공합니다. 보다 자세한 자습서는 스키마 편집기를 사용하여 스키마 [만들기에 대한 자습서를 참조하십시오](../../xdm/tutorials/create-schema-ui.md).

1. Adobe Experience Platform에서 스키마 **[!UICONTROL 탭을]** 클릭하여 스키마 브라우저에 액세스합니다. 스키마 **[!UICONTROL 생성]** 을 **눌러 스키마 편집기**에서 대화식으로 스키마를 작성하고 만들 수 있습니다.
   ![](../images/models-recipes/enrich-rtcdp/schema_browser.png)

2. [ **컴포지션** ] 창 **[!UICONTROL 에서 [할당]** ]을 클릭하여 사용 가능한 클래스를 찾아봅니다.
   * 기존 클래스를 지정하려면 원하는 클래스를 클릭하고 강조 표시한 다음 **[!UICONTROL 클래스 할당을 클릭합니다]**.
      ![](../images/models-recipes/enrich-rtcdp/existing_class.png)

   * 사용자 지정 클래스를 만들려면 브라우저 창의 **[!UICONTROL 가운데]** 위쪽에 있는 새 클래스 만들기를 클릭합니다. 클래스 이름, 설명을 제공하고 클래스의 동작을 선택합니다. 완료되면 **[!UICONTROL 클래스]** 할당을 클릭합니다.
      ![](../images/models-recipes/enrich-rtcdp/create_new_class.png)

   이때 스키마의 구조에는 일부 클래스 필드가 포함되어야 하며 혼합을 할당할 준비가 되었습니다. 혼합이란 특정 개념을 설명하는 하나 이상의 들판으로 이루어진 그룹입니다.

3. [ **컴포지션** ] 창 **[!UICONTROL 에서 []** 혼합 **] 하위 섹션** 에서 [추가]를클릭합니다.
   * 기존 믹스를 할당하려면 원하는 믹스를 클릭하고 강조 표시한 다음 [믹싱 **[!UICONTROL 추가]를 클릭합니다]**. 클래스와 달리, 여러 혼합을 하나의 스키마에 할당하는 것이 적절하다면 가능합니다.
      ![](../images/models-recipes/enrich-rtcdp/existing_mixin.png)

   * 새 혼합을 만들려면 브라우저 창의 가운데 **[!UICONTROL 상단에 있는 [새]** 혼합 만들기]를 클릭합니다. 믹싱에 대한 이름과 설명을 입력한 다음 [믹서 **[!UICONTROL 할당]** ]을 클릭합니다.
      ![](../images/models-recipes/enrich-rtcdp/create_new_mixin.png)

   * 혼합 필드를 추가하려면 [컴포지션] 창 안의 *믹신 이름을* 클릭합니다. 그런 다음 **[!UICONTROL 구조]** 창 내에서 필드 *추가를 클릭하여 혼합 필드를 추가할 수 있는 옵션이* 제공됩니다. 적절하게 혼합 속성을 제공해야 합니다.
      ![](../images/models-recipes/enrich-rtcdp/mixin_properties.png)

4. 스키마 작성을 완료했으면 *구조* 창 내에서 스키마의 최상위 수준 필드를 클릭하여 오른쪽 속성 창에 스키마의 속성을 표시합니다. 이름과 설명을 입력하고 **[!UICONTROL 저장을]** 클릭하여 스키마를 생성합니다.
   ![](../images/models-recipes/enrich-rtcdp/save_schema.png)

5. 왼쪽 탐색 열에서 데이터 집합 **[!UICONTROL 을 클릭하여 새로 만든 스키마를]** 사용하여 출력 데이터 집합을 만든 다음 데이터 집합 **[!UICONTROL 만들기를 클릭합니다]**. 다음 화면에서 스키마에서 데이터 **[!UICONTROL 세트 만들기를 선택합니다]**.
   ![](../images/models-recipes/enrich-rtcdp/dataset_overview.png)

6. 스키마 브라우저를 사용하여 새로 만든 스키마를 찾아 선택한 다음 **[!UICONTROL 다음을 클릭합니다]**.
   ![](../images/models-recipes/enrich-rtcdp/choose_schema.png)

7. 이름과 선택적 설명을 제공한 다음 **[!UICONTROL 마침을]** 클릭하여 데이터 세트를 만듭니다.
   ![](../images/models-recipes/enrich-rtcdp/configure_dataset.png)

출력 스키마 데이터 세트를 만들었으므로 다음 섹션으로 계속 이동하여 프로파일 데이터 세트를 구성하고 활성화할 수 있습니다.

## 출력 스키마 및 데이터 집합 구성 {#configure-an-output-schema-and-dataset}

데이터 세트에 대한 데이터 세트 [!DNL Profile]를 활성화하려면 먼저 데이터 세트의 스키마를 기본 ID 필드를 포함하도록 구성한 다음 스키마를 활성화해야 합니다 [!DNL Profile]. 새 스키마를 만들고 활성화하려면 스키마 편집기를 사용하여 스키마 [만들기에 대한 자습서를 참조하십시오](../../xdm/tutorials/create-schema-ui.md). 그렇지 않은 경우 아래 지침에 따라 기존 스키마와 데이터 세트를 활성화합니다.

1. Adobe Experience Platform에서 스키마 브라우저를 사용하여 활성화할 출력 스키마를 찾은 다음 해당 이름 [!DNL Profile] 을 클릭하여 해당 컴포지션을 확인합니다.
   ![](../images/models-recipes/enrich-rtcdp/schemas.png)

2. 스키마 구조를 확장하고 기본 식별자로 설정할 적절한 필드를 찾습니다. 원하는 필드를 클릭하여 해당 속성을 표시합니다.
   ![](../images/models-recipes/enrich-rtcdp/schema_structure.png)

3. 필드의 ID 속성, **[!UICONTROL 기본 ID]** 속성 **[!UICONTROL 을 활성화한 다음 적절한 ID 네임스페이스를 선택하여 필드를 기본 ID로]** 설정합니다 ****. 변경 **[!UICONTROL 을]** 수행한 후 적용을 클릭합니다.
   ![](../images/models-recipes/enrich-rtcdp/set_identity.png)

4. 스키마 구조의 최상위 객체를 클릭하여 스키마 속성을 표시하고 프로파일 스위치를 전환하여 프로파일에 대한 스키마를 **[!UICONTROL 활성화합니다]** . 저장을 **[!UICONTROL 클릭하여]** 변경 사항을 완료합니다. 이제 이 스키마를 사용하여 만든 데이터 세트를 프로필에 사용할 수 있습니다.
   ![](../images/models-recipes/enrich-rtcdp/enable_schema.png)

5. 데이터 집합 브라우저를 사용하여 활성화할 데이터 집합 [!DNL Profile] 을 찾은 다음 해당 이름을 클릭하여 세부 정보에 액세스합니다.
   ![](../images/models-recipes/enrich-rtcdp/datasets.png)

6. 올바른 정보 열 [!DNL Profile] 에 있는 **[!UICONTROL 프로필]** 스위치를 전환하여 데이터 세트를 활성화합니다.
   ![](../images/models-recipes/enrich-rtcdp/enable_dataset.png)

데이터를 [!DNL Profile]활성화된 데이터 세트에 인제스트하면 동일한 데이터를 레코드와 [!DNL Profile] 수집할 수 있습니다. 스키마와 데이터세트가 준비되면 적절한 모델을 사용하여 점수 실행을 수행하여 데이터 세트에 일부 데이터를 생성하고 이 튜토리얼을 계속 사용하여 세그먼트 빌더를 사용하여 인사이트 세그먼트를 만듭니다.

## 세그먼트 빌더를 사용하여 세그먼트 만들기 {#create-segments-using-the-segment-builder}

활성화된 데이터세트에 대한 인사이트를 생성하고 인제스트한 경우 세그먼트 빌더를 사용하여 관련 요소의 하위 세트를 식별하여 해당 데이터를 관리할 수 있습니다. [!DNL Profile] 아래 절차에 따라 고유한 세그먼트를 만듭니다.

1. Adobe Experience Platform에서 **[!UICONTROL 세그먼트]** 탭 뒤에 **[!UICONTROL 세그먼트]** 만들기를 클릭하여 세그먼트 빌더에 액세스합니다.
   ![](../images/models-recipes/enrich-rtcdp/segments_overview.png)

2. 세그먼트 빌더 내에서 왼쪽 레일은 세그먼트의 핵심 구성 요소에 액세스할 수 있도록 해줍니다.속성, 이벤트 및 기존 세그먼트 각 빌딩 블록은 해당 탭에 표시됩니다. 사용 가능한 스키마가 확장되는 클래스를 [!DNL Profile]선택한 다음, 세그먼트의 구성 요소를 찾아 찾습니다.
   ![](../images/models-recipes/enrich-rtcdp/segment_builder.png)

3. 비교 문을 제공하여 빌드 블록을 규칙 빌더 캔버스로 드래그하여 놓고 완료합니다.
   ![](../images/models-recipes/enrich-rtcdp/drag_fill.gif)

4. 세그먼트를 만드는 동안 세그먼트 속성 패널을 준수하여 예상 세그먼트 결과를 미리 볼 *수* 있습니다.
   ![](../images/models-recipes/enrich-rtcdp/preview_segment.gif)

5. 적절한 **[!UICONTROL 병합 정책을]**&#x200B;선택하고, 이름과 선택적 설명을 입력한 다음, **[!UICONTROL 저장을 클릭하여]** 새 세그먼트를 완료합니다.
   ![](../images/models-recipes/enrich-rtcdp/save_segment.png)


## 다음 단계 {#next-steps}

이 문서에서는 세그먼트 빌더를 사용하여 인사이트 세그먼트를 만드는 워크플로우를 간략히 [!DNL Profile]설명했습니다. 세그먼트 및 세그먼트 빌더에 대한 자세한 내용은 세그멘테이션 [서비스 개요를 참조하십시오](../../segmentation/home.md).