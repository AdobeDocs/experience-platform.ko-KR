---
title: Real-time Customer Data Platform B2B Edition에 대한 세그멘테이션 사용 사례
description: 사용 가능한 다양한 Adobe Real-time Customer Data Platform B2B Edition 사용 사례에 대한 개요입니다.
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1283'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B Edition에 대한 세그먼테이션 사용 사례

이 문서에서는 Adobe Real-time Customer Data Platform B2B Edition의 세그먼트 정의 예와 일반적인 B2B 사용 사례에 대해 서로 다른 유형의 속성을 결합할 수 있는 방법에 대해 설명합니다. 대상이 B2B 워크플로우에 어떻게 적합한지 이해하려면 다음을 참조하십시오. [엔드 투 엔드 자습서](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>이러한 세그멘테이션 사용 사례에 필요한 속성은 Real-time Customer Data Platform B2B Edition 고객만 사용할 수 있습니다. Real-time Customer Data Platform B2B Edition을 사용하지 않는 경우 다음을 참조하십시오. [세분화 개요](./segmentation-overview.md) 을 가리키도록 업데이트하는 것이 좋습니다.

## 전제 조건 {#prerequisites}

B2B 클래스에 대한 세그멘테이션 속성을 사용하려면 먼저 다음 단계를 완료해야 합니다.

1. B2B 클래스를 사용하는 스키마를 만듭니다. B2B Edition 클래스에는 계정, 캠페인, 기회, 마케팅 목록 등이 포함됩니다. 에 대한 자세한 정보 [B2B 클래스에서 사용할 스키마를 설정하는 방법](../schemas/b2b.md) 스키마 설명서를 참조하십시오.
1. XDM(Experience Data Model) B2B 스키마 간에 관계를 만듭니다. B2B Edition 속성을 기반으로 하는 세그먼트에는 확장된 B2B 세그먼테이션 기능을 완전히 사용하려면 클래스 간 관계가 필요합니다. 다음 문서를 참조하십시오. [두 B2B 스키마 간의 관계를 정의하는 방법](../../xdm/tutorials/relationship-b2b.md) 추가 정보.
1. B2B 스키마를 기반으로 하여 데이터 세트를 사용하여 데이터를 수집하십시오. 다음에 대한 소스 설명서를 참조하십시오. [데이터 수집 방법에 대한 정보](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. 다음 문서를 참조하십시오. [세그먼트 빌더 사용 안내서](../../segmentation/ui/segment-builder.md) 를 참조하십시오.

이러한 요구 사항이 충족되면 일반적인 B2B 사용 사례를 위해 이러한 속성을 결합할 수 있습니다.

## 시작하기 {#getting-started}

B2B 클래스에 대한 결합 스키마에 관계가 설정되고 데이터가 수집되는 데 사용되면 해당 속성은 세그먼트 빌더의 왼쪽 레일에서 사용할 수 있습니다.

B2B 클래스와 해당 속성은 `B2B` 분류 작업 공간 내에서 레이블을 지정하여 Real-time Customer Data Platform 내에서 표준으로 사용할 수 있는 태그와 구분하십시오.

B2B 사용 사례에 대한 세그먼트를 효과적으로 만들려면 스키마에 대한 전문적인 지식을 가지고 데이터 모델이 어떤 모습인지 이해하는 것이 중요합니다. 또한 한 데이터 객체에서 다른 데이터 객체로 이동하는 경로를 인식하는 것이 유용합니다.

아래 이미지는 Real-Time CDP B2B Edition 내에서 사용할 수 있는 B2B 클래스 간의 관계를 보여줍니다.

![B2B 클래스 ERD](../assets/segmentation/b2b-classes.png)

데이터 모델이 복잡할 수 있으므로 Platform UI를 사용하여 데이터 모델의 보다 자세한 시각적 표현을 보고 사용 사례와 관련된 속성을 찾을 수 있습니다. 시작하려면 플랫폼 UI로 이동하고 왼쪽 탐색에서 스키마 를 선택합니다.

사용 가능한 목록에서 적절한 스키마를 선택하고 [!UICONTROL 조성물] 사이드 레일. 아래 예에서 &quot;개인&quot; 관계를 선택하면 현재 스키마에서 관련 &quot;개인&quot; 스키마를 참조하거나(관계의 소스 스키마인 경우), 또는 &quot;개인&quot; 스키마(관계의 대상 스키마인 경우)에 의해 참조되는 속성이 표시됩니다.

![스키마 작업 공간에서 사람 관계를 사용하는 소스 키 예제](../assets/segmentation/source-key-schema-relationship-example.png)

이 관계는 `Key` 아래 이미지에 표시된 대로 폴더를 지정합니다.

![세그먼테이션 작업 공간에서 세그먼트 빌더를 사용하는 소스 키 예](../assets/segmentation/source-key-segmentation-example.png)

자세한 내용은 [Real-time Customer Data Platform B2B Edition 설명서의 스키마](../schemas/b2b.md) 사용 가능한 B2B 클래스에 대한 자세한 정보.

아래 사용 사례에서는 이러한 결과를 얻기 위해 다른 스키마 간의 관계를 설정하는 데 사용되는 클래스에 대한 정보를 제공합니다. 이러한 예를 사용하여 세그먼트를 만드는 데 도움이 될 수 있습니다.

## 다양한 세그먼테이션 사용 사례 예 {#use-cases}

다음 사용 사례는 B2B Edition을 사용하여 세그먼테이션에 사용할 수 있습니다. 각 예제는 세그먼트가 수행하는 작업에 대한 설명과 세그먼트를 만드는 데 사용되는 클래스에 대한 설명을 제공합니다. 제공된 이미지는 [!UICONTROL 속성] 스키마의 구조를 반영하는 사이드 레일. 다음 [!UICONTROL 세그먼트 속성] 표시 오른쪽의 섹션에는 세그먼트 속성에 대한 문서화된 분류가 포함되어 있습니다.

### 예제 1: B2B 기회에 대한 &quot;의사 결정권자&quot; 찾기 {#find-decision-maker}

모든 기회의 &quot;의사 결정&quot;인 모든 사람들을 찾아라. 이 세그먼트에는 [!UICONTROL XDM 개별 프로필] 클래스 및 [!UICONTROL XDM 비즈니스 기회 개인 관계] 클래스 이름을 지정합니다.

![UI 예제 1 설정 표시](../assets/segmentation/example-1.png)

### 예제 2: 특정 달러 금액 이상의 기회에 할당된 B2B 프로필 찾기 {#find-opportunities-amount}

영업 기회 금액이 지정된 금액(100만 달러)보다 많은 영업 기회에 직접 할당되는 모든 고객을 찾습니다. 이 세그먼트에는 [!UICONTROL XDM 개별 프로필] 클래스, [!UICONTROL XDM 비즈니스 기회 개인 관계] 클래스 및 [!UICONTROL XDM 비즈니스 기회] 클래스 이름을 지정합니다.

![UI 예제 2 설정 표시](../assets/segmentation/example-2.png)

### 예제 3: 위치별 기회에 지정된 B2B 프로파일 찾기 {#find-opportunities-location}

계정이 지정된 위치(캐나다)에 있는 기회에 직접 지정되는 모든 사람을 찾습니다. 이 세그먼트에는 [!UICONTROL XDM 개별 프로필] 클래스, [!UICONTROL XDM 비즈니스 기회 개인 관계] 클래스, [!UICONTROL XDM 비즈니스 기회] 클래스 및 [!UICONTROL XDM 비즈니스 계정] 클래스 이름을 지정합니다.

![UI 예제 3 설정 표시](../assets/segmentation/example-3.png)

### 예제 4: 업계 및 브라우징 동작별로 &quot;의사 결정자&quot;를 찾아 기회를 확인하십시오 {#find-industry-browsing-behavior}

&quot;금융&quot; 업계에 있는 영업 기회의 &quot;의사 결정 업체&quot;인 모든 사람을 찾아 지난 3일 동안 가격 책정 페이지를 방문했습니다. 이 세그먼트에는 [!UICONTROL XDM 개별 프로필] 클래스, [!UICONTROL XDM 비즈니스 기회 개인 관계] 클래스, [!UICONTROL XDM 비즈니스 기회] 클래스 및 [!UICONTROL XDM 비즈니스 계정] 클래스 및 [!UICONTROL XDM ExperienceEvent] 클래스 이름을 지정합니다.

![UI 예제 4 설정 표시](../assets/segmentation/example-4.png)

### 예제 5: 부서 이름 및 영업 기회 금액별로 영업 기회에 대한 B2B 프로파일 찾기 {#find-department-opportunity-amount}

HR(Human Resources) 부서에서 근무하며, 지정된 금액(100만 달러) 이상의 개설 기회를 가진 계정과 관련된 모든 고객을 찾습니다. 이 세그먼트에는 [!UICONTROL XDM 개별 프로필] 클래스, [!UICONTROL XDM 비즈니스 계정] 클래스 및 [!UICONTROL XDM 비즈니스 기회] 클래스 이름을 지정합니다.

![UI에 예제 5 설정 표시](../assets/segmentation/example-5.png)

### 예제 6: 직책 및 연간 계정 매출별로 B2B 프로필 찾기 {#find-by-job-title-and-revenue}

직책(1억 달러)이 부사장이고 해당 금액의 연간 매출액을 가진 모든 계정(1억 달러)과 관련된 모든 사람을 찾아서 지난 달에 적어도 3번 가격 책정 페이지를 방문한 적이 있습니다. 이 세그먼트에는 [!UICONTROL XDM 개별 프로필] 클래스, [!UICONTROL XDM 비즈니스 계정] 클래스 및 [!UICONTROL XDM ExperienceEvent] 클래스 이름을 지정합니다.

![UI에 6가지 설정 예 표시](../assets/segmentation/example-6.png)

### 예제 7: 영업 기회 상태 및 검색 동작별로 &quot;의사 결정자&quot;를 찾습니다. {#find-by-opportunity-status-and-browsing-behavior}

영업 기회 종료의 &quot;의사 결정권자&quot;인 모든 고객을 찾아 지난 주에 가격 책정 페이지를 방문했습니다. 이 세그먼트에는 [!UICONTROL XDM 개별 프로필] 클래스, [!UICONTROL XDM 비즈니스 기회 개인 관계] 클래스, [!UICONTROL XDM 비즈니스 기회] 클래스 및 [!UICONTROL XDM ExperienceEvent] 클래스 이름을 지정합니다.

![UI 예제 7 설정 표시](../assets/segmentation/example-7.png)

### 예제 8: 관련 계정을 사용하여 세그먼테이션 도달 범위를 확장합니다. {#related-accounts}

HR(Human Resources) 부서에서 근무하며 모든 계정과 관련된 모든 인력을 찾습니다 *또는 계정의 관련 계정 중 하나* 해당 금액 ( 백만 달러 ) 이상의 영업 기회가 있는 기회가 한 개 이상 있습니다. 이 세그먼트에는 [!UICONTROL XDM 개별 프로필] 클래스, [!UICONTROL XDM 비즈니스 계정] 클래스 및 [!UICONTROL XDM 비즈니스 기회] 클래스 이름을 지정합니다.

![관련 계정에 대한 세그먼테이션 표시 UI](../assets/segmentation/segmentation-related-accounts.png)

### 예제 9: 프로필 자격을 얻으려면 리드 점수 및/또는 계정 점수를 사용하십시오 {#account-scoring}

리드 점수가 80점이 넘는 모든 프로필을 찾습니다.

![예측 리드 및 계정 점수 책정 세분화 표시 UI](../assets/segmentation/segmentation-predictive-lead-and-account-scoring.png)

## 다음 단계 {#next-steps}

이 개요를 읽고 나면 이제 Real-Time CDP, B2B Edition을 사용하여 사용할 수 있는 세그먼테이션 가능성을 이해할 수 있습니다. 세그멘테이션 서비스에 대한 자세한 내용은 [세그먼테이션 설명서](../../segmentation/home.md).
