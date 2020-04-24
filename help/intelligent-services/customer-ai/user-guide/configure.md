---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: 고객 AI 인스턴스 구성
topic: Instance creation
translation-type: tm+mt
source-git-commit: f7c59ef097c00073fbf9f6522b6e70ed24cc8bf1

---


# 고객 AI 인스턴스 구성

고객 AI를 통해 머신 러닝에 대한 걱정 없이 고객 성향 점수를 생성할 수 있습니다.

Intelligent Services는 고객 AI를 사용하기 쉬운 Adobe Sensei 서비스로 제공하며, 이 서비스는 다양한 사용 사례에 맞게 구성할 수 있습니다. 다음 섹션에서는 고객 AI 인스턴스를 구성하는 절차를 제공합니다.

## 인스턴스 설정 {#set-up-your-instance}

플랫폼 UI에서 왼쪽 탐색 **[!UICONTROL Services]** 을 클릭합니다. 브라우저가 **[!UICONTROL Services]** 나타나고 언제든지 사용 가능한 모든 서비스가 표시됩니다. 고객 AI의 컨테이너에서 을 클릭합니다 **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

고객 *AI* 화면에는 모든 기존 고객 AI 인스턴스가 표시됩니다. **[!UICONTROL Create instance]**&#x200B;를 클릭합니다.

![](../images/user-guide/dashboard.png)

인스턴스 생성 워크플로우가 나타나고 설정 *단계부터* 시작됩니다.

다음은 인스턴스를 제공해야 하는 값에 대한 중요한 정보입니다.

* 인스턴스 이름은 고객 AI 점수가 표시되는 모든 위치에서 사용됩니다. 따라서, 이름은 예측 점수가 나타내는 것(예: &quot;잡지 구독을 취소할 가능성&quot;)을 설명해야 합니다.

* 성향 유형은 점수와 지표 극성을 결정합니다. 또는 **[!UICONTROL Churn]** 를 선택할 수 **[!UICONTROL Conversion]**&#x200B;있습니다. 성향 유형이 인스턴스에 어떤 영향을 주는지에 대한 자세한 내용은 인사이트 문서의 [점수 요약](./discover-insights.md#scoring-summary) 아래 메모를 참조하십시오.

* 데이터 소스는 데이터가 있는 곳입니다. 데이터 집합은 점수를 예측하는 데 사용되는 입력 데이터 집합입니다. Customer AI는 디자인별로 고객 경험 이벤트 데이터를 사용하여 성향 점수를 계산합니다. 드롭다운 선택기에서 데이터 세트를 선택하면 고객 AI와 호환되는 데이터만 나열됩니다.

* 기본적으로 자격 조건을 갖춘 인구를 지정하지 않으면 모든 프로필에 대해 성향 점수가 생성됩니다. 이벤트를 기반으로 프로파일을 포함하거나 제외하는 조건을 정의하여 적격한 인구를 지정할 수 있습니다.

필요한 값을 제공한 다음 을 클릭합니다 **[!UICONTROL Next]**.

![](../images/user-guide/setup.png)

### 목표 정의 {#define-a-goal}

목표 *정의* 단계가 나타나고 목표를 시각적으로 정의할 수 있는 대화형 환경을 제공합니다. 목표는 하나 이상의 이벤트로 구성되며, 여기서 각 이벤트의 발생은 이벤트가 보유하는 조건을 기반으로 합니다. 고객 AI 인스턴스의 목적은 주어진 기간 내에 목표 달성 가능성을 판단하는 것입니다.

드롭다운 목록에서 필드를 **[!UICONTROL Enter Field Name]** 클릭하고 선택합니다. 두 번째 입력을 클릭하고 이벤트 조건에 대한 절을 선택한 다음 이벤트를 완료할 대상 값을 제공합니다. 추가 이벤트는 클릭하여 구성할 수 **[!UICONTROL Add event]**&#x200B;있습니다. 마지막으로, 예상 기간을 일 수로 적용하여 목표를 완료한 다음 을 클릭합니다 **[!UICONTROL Next]**.

![](../images/user-guide/goal.png)

### 일정 구성 *(선택 사항)*{#configure-a-schedule}

고급 *단계가* 나타납니다. 이 선택 단계에서는 예측 실행을 자동화하고, 특정 이벤트를 필터링하기 위한 예측 제외를 정의하거나, 아무 것도 필요하지 않은 **[!UICONTROL Finish]** 경우 클릭하도록 예약을 구성할 수 있습니다.

점수 지정 빈도를 구성하여 점수 지정 *일정을 설정합니다*. 자동화된 예측 실행은 주별 또는 월별 기준으로 실행되도록 예약할 수 있습니다.

![](../images/user-guide/schedule.png)

일정 구성 아래에서는 점수를 생성할 때 특정 조건을 충족하는 이벤트가 평가되지 않도록 예측 제외를 정의할 수 있습니다. 이 기능을 사용하여 관련 없는 데이터 입력을 필터링할 수 있습니다.

특정 이벤트를 제외하려면 목표를 정의하는 방법과 동일한 방식으로 이벤트를 클릭하고 **[!UICONTROL Add exclusion]** 정의합니다. 제외를 제거하려면 이벤트 컨테이너의 오른쪽 위에 있는 줄임표(**[!UICONTROL ...]**)를 클릭한 다음 을 클릭합니다 **[!UICONTROL Remove Container]**.

![](../images/user-guide/exclusion.png)

필요에 따라 이벤트를 제외시킨 다음 클릭하여 인스턴스를 **[!UICONTROL Finish]** 만듭니다.

![](../images/user-guide/advanced.png)

인스턴스가 성공적으로 만들어지면 예측 실행이 즉시 트리거되고 정의된 일정에 따라 후속 실행이 실행됩니다.

>[!NOTE] 입력 데이터의 크기에 따라 예측 실행을 완료하는 데 최대 24시간이 걸릴 수 있습니다.

이 섹션 다음에는 고객 AI 인스턴스를 구성했으며 예측 실행이 실행되었습니다. 성공적인 실행이 완료되면 점수에서 얻은 인사이트가 예측된 점수로 프로파일을 자동으로 채웁니다. 이 튜토리얼의 다음 섹션을 계속하기 전에 최대 24시간을 기다려 주십시오.

## 다음 단계 {#next-steps}

이 튜토리얼을 따라 고객 AI 인스턴스와 생성된 성향 점수를 성공적으로 구성했습니다. 이제 세그먼트 빌더를 사용하여 예측된 점수가 [있는 고객 세그먼트를](./create-segment.md) 만들거나 고객 AI를 통해 인사이트를 [찾을 수 있습니다](./discover-insights.md).

