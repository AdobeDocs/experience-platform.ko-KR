---
keywords: Experience Platform;사용 안내서;고객 아이디;인기 있는 주제;인스턴스 구성;인스턴스 만들기;;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 고객 AI 인스턴스 구성
topic: Instance creation
description: 지능형 서비스는 고객 AI를 다른 사용 사례용으로 구성할 수 있는 사용이 간편한 Adobe Sensei 서비스로 제공합니다. 다음 섹션에서는 고객 AI 인스턴스를 구성하는 절차를 제공합니다.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
translation-type: tm+mt
source-git-commit: 2ef2a6431865e8ffdc2abd6cf527249e8b5ca4d0
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---

# 고객 AI 인스턴스 구성

고객 AI를 통해 지능형 서비스에 가입함으로써 머신 러닝에 대한 걱정 없이 고객 성향 점수를 생성할 수 있습니다.

지능형 서비스는 고객 AI를 다른 사용 사례용으로 구성할 수 있는 사용이 간편한 Adobe Sensei 서비스로 제공합니다. 다음 섹션에서는 고객 AI 인스턴스를 구성하는 절차를 제공합니다.

## 인스턴스 {#set-up-your-instance} 설정

플랫폼 UI의 왼쪽 탐색 영역에서 **[!UICONTROL Services]**&#x200B;을 선택합니다. **[!UICONTROL Services]** 브라우저가 나타나고 언제든지 사용 가능한 모든 서비스가 표시됩니다. 고객 AI의 컨테이너에서 **[!UICONTROL Open]**&#x200B;을 선택합니다.

![](../images/user-guide/navigate-to-service.png)

**고객 AI** UI가 나타나고 모든 서비스 인스턴스가 표시됩니다.

- **[!UICONTROL Create instance]** 컨테이너의 오른쪽 하단에 있는 **[!UICONTROL Total profiles scored]** 지표를 찾을 수 있습니다. 이 지표는 모든 샌드박스 환경 및 삭제된 서비스 인스턴스를 포함하여 현재 달력 연도에 대해 고객 AI가 획득한 총 프로필 수를 추적합니다.

![](../images/user-guide/total-profiles.png)

서비스 인스턴스는 UI 오른쪽의 컨트롤을 사용하여 편집, 복제 및 삭제할 수 있습니다. 이러한 컨트롤을 표시하려면 기존 **[!UICONTROL Service instances]**&#x200B;에서 인스턴스를 선택합니다. 컨트롤에는 다음이 포함됩니다.

- **[!UICONTROL Edit]**:을  **[!UICONTROL Edit]** 선택하면 기존 서비스 인스턴스를 수정할 수 있습니다. 인스턴스의 이름, 설명 및 점수 지정 빈도를 편집할 수 있습니다.
- **[!UICONTROL Clone]**:을  **[!UICONTROL Clone]** 선택하면 현재 선택한 서비스 인스턴스 설정이 복사됩니다. 그런 다음 워크플로우를 수정하여 일부를 수정하고 새 인스턴스로 이름을 변경할 수 있습니다.
- **[!UICONTROL Delete]**:모든 내역 실행을 포함하는 서비스 인스턴스를 삭제할 수 있습니다.
- **[!UICONTROL Data source]**:이 인스턴스에서 사용하는 데이터 세트에 대한 링크입니다.
- **[!UICONTROL Last run details]**:이것은 실행이 실패할 때만 표시됩니다. 여기에 오류 코드와 같이 실행이 실패한 이유에 대한 정보가 표시됩니다.
- **[!UICONTROL Score definition]**:이 인스턴스에 대해 구성한 목표에 대한 빠른 개요입니다.

![](../images/user-guide/service-instance-panel.png)

새 인스턴스를 만들려면 **[!UICONTROL Create instance]**&#x200B;을 선택합니다.

![](../images/user-guide/dashboard.png)

**[!UICONTROL Setup]** 단계부터 인스턴스 만들기 작업 과정이 나타납니다.

다음은 인스턴스를 제공해야 하는 값에 대한 중요한 정보입니다.

- 인스턴스 이름은 고객 AI 점수가 표시되는 모든 위치에서 사용됩니다. 따라서, 이름은 예측 점수가 나타내는 것을 설명해야 합니다(예: &quot;잡지 가입을 취소할 가능성&quot;).

- 성향 유형은 점수와 지표 극성의 의도를 결정합니다. **[!UICONTROL Churn]** 또는 **[!UICONTROL Conversion]**&#x200B;을 선택할 수 있습니다. 성향 유형이 인스턴스에 미치는 영향에 대한 자세한 내용은 인사이트 문서의 [점수 요약](./discover-insights.md#scoring-summary) 아래의 메모를 참조하십시오.

- 데이터 소스는 데이터가 있는 곳입니다. 데이터 세트는 점수를 예측하는 데 사용되는 입력 데이터 집합입니다. 고객 AI는 기본적으로 고객 경험 이벤트, Adobe Analytics 및 Adobe Audience Manager 데이터를 사용하여 성향 점수를 계산합니다. 드롭다운 선택기에서 데이터 세트를 선택하면 고객 AI와 호환되는 데이터만 나열됩니다.

- 자격 조건을 갖춘 인구를 지정하지 않으면 기본적으로 성향 점수가 모든 프로파일에 대해 생성됩니다. 이벤트를 기반으로 프로파일을 포함하거나 제외할 조건을 정의하여 적격한 모집단을 지정할 수 있습니다.

필요한 값을 제공한 다음 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../images/user-guide/setup.png)

### 목표 정의 {#define-a-goal}

**[!UICONTROL Define goal]** 단계가 나타나고 예측 목표를 시각적으로 정의할 수 있는 대화형 환경을 제공합니다. 목표는 하나 이상의 이벤트로 구성되며, 여기서 각 이벤트의 발생은 이벤트가 보유하는 조건을 기준으로 합니다. 고객 AI 인스턴스의 목표는 주어진 기간 내에 목표를 달성할 가능성이 있는지에 대한 판단입니다.

목표를 만들려면 **[!UICONTROL Enter Field Name]**&#x200B;을 선택하고 드롭다운 목록에서 필드를 선택합니다. 두 번째 입력을 선택하고 이벤트 조건에 대한 절을 선택한 다음 이벤트를 완료할 대상 값을 제공합니다. **[!UICONTROL Add event]**&#x200B;을 선택하여 추가 이벤트를 구성할 수 있습니다. 마지막으로, 예측 시간(일)을 적용하여 목표를 완료한 다음 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../images/user-guide/goal.png)

#### 발생하며 발생하지 않음

목표를 정의하는 동안 **[!UICONTROL Will occur]** 또는 **[!UICONTROL Will not occur]**&#x200B;을 선택할 수 있습니다. **[!UICONTROL Will occur]**&#x200B;을 선택하면 고객 이벤트 데이터가 인사이트 UI에 포함되려면 정의한 이벤트 조건을 충족해야 합니다.

예를 들어 고객이 구매할지 여부를 예측할 수 있도록 앱을 설정하려면 **[!UICONTROL Will occur]** 뒤에 **[!UICONTROL All of]**&#x200B;을 선택한 다음 **commerce.purchases.id** 및 **exists**&#x200B;을 연산자로 입력합니다.

![발생함](../images/user-guide/occur.png)

그러나 특정 기간에 어떤 이벤트가 발생하지 않을 것인지를 예측하는 데 관심이 있는 경우도 있습니다. 이 옵션을 사용하여 목표를 구성하려면 최상위 드롭다운 메뉴에서 **[!UICONTROL Will not occur]**&#x200B;을 선택합니다.

예를 들어 어떤 고객이 덜 참여하는지 예측하고자 하는 경우 다음 달에 계정 로그인 페이지를 방문하지 마십시오. **[!UICONTROL Will not occur]** 뒤에 **[!UICONTROL All of]**&#x200B;을 선택한 다음 **web.webInteraction.URL** 및 **[!UICONTROL equals]**&#x200B;를 **account-login**&#x200B;의 연산자로 입력합니다.

![발생하지 않음](../images/user-guide/not-occur.png)

#### 모든 항목 및 모든 항목

경우에 따라 이벤트 조합이 발생하는지 여부와 그 밖의 경우에는 사전 정의된 집합에서 이벤트 발생을 예측할 수 있습니다. 고객에게 이벤트 조합이 있는지 여부를 예측하려면 **[!UICONTROL Define Goal]** 페이지의 두 번째 수준 드롭다운에서 **[!UICONTROL All of]** 옵션을 선택합니다.

예를 들어 고객이 특정 제품을 구매하는지 여부를 예측할 수 있습니다. 이 예측 목표는 다음 두 조건에 의해 정의됩니다.`commerce.order.purchaseID` **exists** 및 `productListItems.SKU` **등분** 특정 값

![모든 예](../images/user-guide/all-of.png)

고객이 주어진 집합에서 이벤트를 가질 것인지 여부를 예측하기 위해 **[!UICONTROL Any of]** 옵션을 사용할 수 있습니다.

예를 들어 고객이 특정 URL을 방문하는지 아니면 특정 이름을 가진 웹 페이지를 방문하는지를 예측할 수 있습니다. 이 예측 목표는 다음 두 조건에 의해 정의됩니다.`web.webPageDetails.URL` **은**&#x200B;로 시작하고 `web.webPageDetails.name` **은**&#x200B;로 시작합니다.

![예](../images/user-guide/any-of.png)

### 일정 *(선택 사항)* {#configure-a-schedule} 구성

**[!UICONTROL Advanced]** 단계가 나타납니다. 이 선택 단계를 통해 예측 실행을 자동화하는 일정을 구성하거나, 특정 이벤트를 필터링하는 예측 제외를 정의하거나, 아무 것도 필요하지 않은 경우 **[!UICONTROL Finish]**&#x200B;을 선택할 수 있습니다.

**[!UICONTROL Scoring Frequency]**&#x200B;을(를) 구성하여 점수 지정 일정을 설정합니다. 자동화된 예측 실행을 주별 또는 월별 기준으로 실행하도록 예약할 수 있습니다.

![](../images/user-guide/schedule.png)

일정 구성 아래에서는 점수를 생성할 때 특정 조건을 충족하는 이벤트가 평가되지 않도록 예측 제외를 정의할 수 있습니다. 이 기능을 사용하여 관련 없는 데이터 입력을 필터링할 수 있습니다.

특정 이벤트를 제외하려면 **[!UICONTROL Add exclusion]**&#x200B;을 선택하고 목표가 정의된 방법과 동일한 방식으로 이벤트를 정의합니다. 제외를 제거하려면 이벤트 컨테이너의 오른쪽 상단에 있는 줄임표(**[!UICONTROL ...]**)를 선택한 다음 **[!UICONTROL Remove Container]**&#x200B;을 선택합니다.

![](../images/user-guide/exclusion.png)

필요에 따라 이벤트를 제외하고 **[!UICONTROL Finish]**&#x200B;을 선택하여 인스턴스를 만듭니다.

![](../images/user-guide/advanced.png)

인스턴스가 성공적으로 생성되면 예측 실행이 즉시 트리거되고 정의된 일정에 따라 후속 실행이 실행됩니다.

>[!NOTE]
>
>입력 데이터의 크기에 따라 예측 실행을 완료하는 데 최대 24시간이 걸릴 수 있습니다.

이 섹션을 따라 고객 AI 인스턴스를 구성했으며 예측 실행이 실행되었습니다. 실행이 성공적으로 완료되면, 점수에서 얻은 인사이트가 예측된 점수로 프로파일을 자동으로 채웁니다. 이 튜토리얼의 다음 섹션으로 이동하기 전에 최대 24시간을 기다려 주십시오.

## 다음 단계 {#next-steps}

이 튜토리얼을 따라 고객 AI 인스턴스와 성향 점수가 성공적으로 구성되었습니다. 이제 세그먼트 빌더를 사용하여 [예상 점수](./create-segment.md) 또는 [고객 AI](./discover-insights.md)에서 인사이트를 찾는 고객 세그먼트를 만들 수 있습니다.

## 추가 리소스

다음 비디오는 고객 AI에 대한 구성 작업 과정에 대한 이해를 지원하기 위해 만들어졌습니다. 또한 모범 사례와 사용 사례 예도 제공됩니다.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
