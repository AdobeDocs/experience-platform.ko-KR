---
title: Real-Time CDP B2B의 예측 리드 및 계정 점수
type: Documentation
description: Experience Platform CDP B2B의 예측 리드 및 계정 점수 기능에 대한 개요와 추가 정보입니다.
feature: Profiles, B2B
badgeB2B: label="B2B 버전" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 2%

---

# Real-Time CDP B2B의 예측 리드 및 계정 점수

B2B 마케터는 마케팅 단계의 맨 위에서 여러 가지 문제에 직면합니다. 효과를 거두기 위해서는 B2B 마케터들은 많은 수의 사람들이 고가치 타겟에 집중할 수 있도록 자격을 부여하는 자동화된 방법이 필요하다. 자격은 마케팅 전환뿐만 아니라 궁극적인 판매 성과와 일치해야 합니다.

계정 은 B2B 제품 및 서비스를 구매하는 최종 엔티티입니다. 효과적인 마케팅 및 판매를 위해 B2B 마케터는 개인의 뿐만 아니라 계정의 구매 가능성까지 알아야 합니다.

계정 기반 마케팅은 특히 마케팅 타겟으로 계정을 전략화합니다. 거래처 성향 점수는 B2B 마케터가 투자수익률을 극대화하기 위해 거래처 간 우선순위를 매기는 데 큰 도움이 됩니다.

예측 리드 및 계정 점수 책정 서비스는 영업 기회 단계 전환 이벤트를 학습하고 예측하며 계정 점수를 산출하기 위해 개인 활동을 계정 수준으로 집계하여 위의 문제를 해결합니다. 점수는 사용자 프로필 및 계정 프로필의 사용자 정의 필드로 쉽게 사용할 수 있으며, 대상을 세분화하기 위한 세그먼트 기준으로 쉽게 포함할 수 있습니다. B2B 마케터가 점수를 유도한 요소를 더 잘 이해하는 데 도움이 되는 가장 영향력 있는 요소는 집계와 단위 수준 모두에서 사용할 수도 있습니다.

## 예측 리드 및 계정 점수 이해 {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] 데이터 원본은 개인 프로필 수준에서 전환 이벤트를 제공할 수 있는 유일한 데이터 원본이므로 현재 필요합니다.

예측 리드 및 계정 점수는 트리 기반(랜덤 포레스트/그래디언트 부스팅) 머신 러닝 방법을 사용하여 예측 리드 점수화 모델을 구축합니다.

관리자는 구성된 각 전환 이벤트에 대해 모델이라고도 하는 여러 프로필 점수 목표를 구성하여 구성된 각 목표에 대해 별도의 점수를 생성할 수 있습니다.

예측 리드 및 계정 점수는 다음 전환 목표 유형 및 필드를 지원합니다.

| 목표 유형 | 필드 |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>예: `opportunityEvent.dataValueChanges.attributeName`은(는) `Stage`이고 `opportunityEvent.dataValueChanges.newValue`은(는) `Contract`입니다.</ul> |

이 알고리즘에서는 다음 속성과 입력 데이터를 고려합니다.

* 개인 프로필

| XDM 필드 | 필수/선택 사항 |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | 필수 여부 |
| `workAddress.country` | 선택 사항입니다 |
| `extSourceSystemAudit.createdDate` | 필수 여부 |
| `extendedWorkDetails.jobTitle` | 선택 사항입니다 |

>[!NOTE]
> 
>이 알고리즘은 Person:personComponents 필드 그룹의 `sourceAccountKey.sourceKey` 필드만 검사합니다.

* 계정 프로필

| XDM 필드 | 필수/선택 사항 |
| --- | --- |
| `accountKey.sourceKey` | 필수 여부 |
| `extSourceSystemAudit.createdDate` | 필수 여부 |
| `accountOrganization.industry` | 선택 사항입니다 |
| `accountOrganization.numberOfEmployees` | 선택 사항입니다 |
| `accountOrganization.annualRevenue.amount` | 선택 사항입니다 |

* 경험 이벤트

| XDM 필드 | 필수/선택 사항 |
| --- | --- |
| `_id` | 필수 여부 |
| `personKey.sourceKey` | 필수 여부 |
| `timestamp` | 필수 여부 |
| `eventType` | 필수 여부 |

다음과 같은 엄격한 제한이 설정되어 여러 모델이 지원됩니다.

* 각 프로덕션 샌드박스는 5개의 모델을 사용할 수 있습니다.
* 각 개발 샌드박스는 하나의 모델을 사용할 수 있습니다.

데이터 품질 요구 사항은 다음과 같습니다.

* 가장 최근 2년 동안의 데이터가 교육 목적으로 제공되는 것이 이상적입니다.
* 필요한 최소 데이터 길이는 6개월에 예측 기간을 더한 값입니다.
* 각 예측 목표에 대해 적어도 10개의 정규화된 전환 이벤트가 필요하다.

채점 작업은 매일 실행되며 결과는 프로필 속성 및 계정 속성으로 저장되며 세그먼트 정의 및 개인화에 사용할 수 있습니다. 계정 개요 대시보드에서 기본 분석 인사이트를 사용할 수도 있습니다.

[예측 리드 및 계정 점수를 관리](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) 서비스를 관리하는 방법에 대한 자세한 내용은 설명서를 참조하세요.

## 예측 리드 및 계정 점수 책정 결과 보기 {#how-to-view}

작업 실행 후 결과는 이름 `LeadsAI.Scores` - ***점수 이름***&#x200B;의 각 모델에 대한 새 시스템 데이터 집합에 저장됩니다. 각 점수 필드 그룹은 `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`에 있을 수 있습니다.

| 속성 | 설명 |
| --- | --- |
| 점수 | 정의된 시간대 내에 프로필이 예측된 목표를 달성할 상대적 가능성. 이 값은 확률 백분율이 아니라 전체 모집단과 비교한 프로필의 가능성으로 간주됩니다. 이 점수의 범위는 0부터 100까지입니다. |
| 백분위수 | 이 값은 점수가 비슷한 다른 프로필과 관련된 프로필의 성능에 대한 정보를 제공합니다. 백분위수의 범위는 1부터 100까지입니다. |
| 모델 유형 | 선택한 모델 유형은 개인 점수인지 계정 점수인지 나타냅니다. |
| 스코어 날짜 | 채점이 발생한 날짜. |
| 영향력 있는 요소 | 프로필이 전환될 가능성이 높은 이유에 대한 예측된 이유. 인자는 다음 속성으로 구성됩니다.<ul><li>코드: 프로필의 예측된 점수에 긍정적인 영향을 주는 프로필 또는 행동 속성.</li><li>값: 프로필 또는 동작 속성의 값입니다.</li><li>중요도: 프로필 또는 행동 속성이 예측된 점수(낮음, 중간, 높음)에 대해 갖는 가중치를 나타냅니다.</li></ul> |

### 고객 프로필 점수 보기

개인 프로필에 대한 예측 점수를 보려면 왼쪽 패널의 고객 섹션에서 **[!UICONTROL 프로필]**&#x200B;을 선택한 다음 ID 네임스페이스와 ID 값을 입력하십시오. 완료되면 **[!UICONTROL 보기]**&#x200B;를 선택하세요.

그런 다음 목록에서 프로필을 선택합니다.

![고객 프로필](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

이제 **[!UICONTROL 세부 정보]** 페이지에 예측 점수가 포함됩니다. 예측 점수 옆에 있는 차트 아이콘을 클릭합니다.

![고객 프로필 예측 점수](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

팝업 대화 상자는 점수, 전체 점수 분포, 이 점수에 대해 가장 영향력 있는 상위 요인 및 점수 목표 정의를 표시합니다.

![고객 프로필 예측 점수 세부 정보](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## 예측 리드 및 계정 점수 지정 작업 모니터링 {#monitoring-jobs}

대시보드를 통해 기본 지표와 일별 작업 실행 상태를 모니터링할 수 있습니다. 지표에는 다음이 포함됩니다.

* 채점된 총 개인/계정 프로필
* 다음 채점 작업(날짜)
* 다음 교육 작업(일자)

자세한 내용은 [예측 리드 및 계정 점수에 대한 작업 모니터링](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)에 대한 설명서를 참조하십시오.
