---
title: 실시간 CDP B2B에서 예측 리드 및 계정 점수 책정
type: Documentation
description: Experience Platform CDP B2B의 예측 리드 및 계정 점수 책정 기능에 대한 개요 및 추가 정보입니다.
source-git-commit: 5ac8e099a6de563371f9a53a8b4816e6cf4d1953
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 2%

---

# 실시간 CDP B2B에서 예측 리드 및 계정 점수 책정

B2B 마케터는 마케팅 단계 맨 위에서 여러 어려움에 직면해 있습니다. 효과를 거두기 위해 B2B 마케터는 많은 수의 사람들이 가치가 높은 타겟에 집중할 수 있도록 자동화된 방법을 필요로 합니다. 마케팅 전환뿐만 아니라 최종 판매 결과와 자격을 맞춰야 합니다.

계정 은(는) B2B 제품 및 서비스를 구매하는 최종 엔티티입니다. 효과적으로 마케팅하고 판매하기 위해 B2B 마케터는 개인의 뿐 아니라 계정의 구입 가능성을 알아야 합니다.

계정 기반 마케팅, 특히 계정을 마케팅 타겟으로 전략화합니다. 계정 성향-구매 점수는 B2B 마케터가 투자 수익률을 극대화하기 위해 계정 중에서 우선 순위를 지정하는 데 크게 도움이 됩니다.

예측 리드 및 계정 점수 책정 서비스는 영업 기회 단계 전환 이벤트에 대한 학습 및 예측과 개인 활동을 계정 레벨로 합산하여 계정 점수를 생성함으로써 위의 문제를 해결합니다. 점수는 개인 프로필 및 계정 프로필에 대한 사용자 정의 필드로 쉽게 사용할 수 있으며 세그먼트 기준으로 쉽게 포함하여 대상을 세분화할 수 있습니다. 가장 큰 영향을 주는 요소는 집계 및 단위 수준 모두에서 사용할 수 있으므로 B2B 마케터가 점수를 매긴 요소를 더 잘 이해할 수 있습니다.

## 예측 리드 및 계정 점수 이해하기 {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] 개인 프로필 수준에서 전환 이벤트를 제공할 수 있는 유일한 데이터 소스이므로 데이터 소스가 현재 필요합니다.

예측 리드 및 계정 점수 책정 에서는 트리 기반(임의 포리스트/그라데이션 증폭) 기계 학습 방법을 사용하여 예측 리드 점수 모델을 구축합니다.

관리자는 구성된 각 변환 이벤트에 대해 하나씩, 모델이라고도 하는 여러 프로필 점수 목표를 구성할 수 있으므로 구성된 각 목표에 대해 별도의 점수를 생성할 수 있습니다.

예측 리드 및 계정 점수는 다음과 같은 전환 목표 유형 및 필드를 지원합니다.

| 목표 유형 | 필드 |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>예: `opportunityEvent.dataValueChanges.attributeName` 다음과 같음 `Stage` 및 `opportunityEvent.dataValueChanges.newValue` 다음과 같음 `Contract`</ul> |

알고리즘에서는 다음 속성을 고려하며 데이터를 입력합니다.

* 개인 프로필

| XDM 필드 | 필수/선택적 |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | 필수 여부 |
| `workAddress.country` | 선택 사항입니다 |
| `extSourceSystemAudit.createdDate` | 필수 여부 |
| `extendedWorkDetails.jobTitle` | 선택 사항입니다 |

>[!NOTE]
> 
>알고리즘이 검사만 `sourceAccountKey.sourceKey` 개인:personComponents 필드 그룹의 필드입니다.

* 계정 프로필

| XDM 필드 | 필수/선택적 |
| --- | --- |
| `accountKey.sourceKey` | 필수 여부 |
| `extSourceSystemAudit.createdDate` | 필수 여부 |
| `accountOrganization.industry` | 선택 사항입니다 |
| `accountOrganization.numberOfEmployees` | 선택 사항입니다 |
| `accountOrganization.annualRevenue.amount` | 선택 사항입니다 |

* 경험 이벤트

| XDM 필드 | 필수/선택적 |
| --- | --- |
| `_id` | 필수 여부 |
| `personKey.sourceKey` | 필수 여부 |
| `timestamp` | 필수 여부 |
| `eventType` | 필수 여부 |

다음과 같은 하드 제한이 설정되어 여러 모델이 지원됩니다.

* 각 프로덕션 샌드박스에는 5개의 모델을 사용할 수 있습니다.
* 각 개발 샌드박스에는 하나의 모델을 사용할 수 있습니다.

데이터 품질 요구 사항은 다음과 같습니다.

* 가장 최근의 데이터 중 2년 동안의 교육용 데이터가 있어야 합니다.
* 필요한 데이터의 최소 길이는 6개월과 예측 창입니다.
* 각 예측 목표에 대해 10개 이상의 정규화된 전환 이벤트가 필요합니다.

점수 작업은 매일 실행되고 결과는 프로필 속성 및 계정 속성으로 저장되며 세그먼트 정의 및 개인화에 사용할 수 있습니다. 즉시 사용 가능한 분석 인사이트는 계정 개요 대시보드에서도 사용할 수 있습니다.

방법에 대한 자세한 내용은 설명서 를 참조하십시오 [예측 리드 및 계정 점수 관리](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) 서비스.

## 예측 리드 및 계정 점수 결과 보기 {#how-to-view}

작업이 실행되면 이름 아래에 각 모델의 새 시스템 데이터 세트에 결과가 저장됩니다 `LeadsAI.Scores` - ***점수 이름***. 각 점수 필드 그룹은 `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| 속성 | 설명 |
| --- | --- |
| 점수 | 정의된 기간 내에 예상 목표를 달성하는 프로필에 대한 상대적 가능성입니다. 이 값은 전체 모집단에 비해 확률 비율로 간주되지 않고 프로필의 가능성이 높습니다. 이 점수는 0부터 100까지입니다. |
| 백분위수 | 이 값은 유사한 점수가 있는 다른 프로필과 상대적인 프로필 성능에 대한 정보를 제공합니다. 백분위수 범위는 1부터 100까지입니다. |
| 모델 유형 | 선택한 모델 유형은 개인 또는 계정 점수입니다. |
| 점수 날짜 | 점수가 발생한 날짜입니다. |
| 영향력 있는 요소 | 프로필이 전환될 가능성이 높은 이유에 대한 예측된 이유입니다. 요소는 다음 속성으로 구성됩니다.<ul><li>코드: 프로필의 예측된 점수에 긍정적인 영향을 주는 프로필 또는 행동 속성입니다.</li><li>값: 프로필 또는 동작 속성의 값입니다.</li><li>중요도: 프로필 또는 행동 속성이 예측된 점수(낮음, 중간, 높음)에 갖는 가중치를 나타냅니다.</li></ul> |

### 고객 프로필 점수 보기

개인 프로필에 대한 예측 점수를 보려면 **[!UICONTROL 프로필]** 왼쪽 패널의 고객 섹션 아래에 id 네임스페이스 및 id 값을 입력합니다. 완료되면 을 선택합니다. **[!UICONTROL 보기]**.

그런 다음 목록에서 프로필을 선택합니다.

![고객 프로필](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

다음 **[!UICONTROL 세부 사항]** 이제 페이지에 예측 점수가 포함됩니다. 예측 점수 옆에 있는 차트 아이콘을 클릭합니다.

![고객 프로필 예측 점수](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

팝업 대화 상자에는 점수, 전체 점수 분포, 이 점수에 대한 상위 영향력 있는 요소 및 점수 목표 정의가 표시됩니다.

![고객 프로필 예측 점수 세부 정보](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## 예측 리드 및 계정 점수 작업 모니터링 {#monitoring-jobs}

대시보드를 통해 기본 지표 및 일별 작업 실행 상태를 모니터링할 수 있습니다. 지표에는 다음이 포함됩니다.

* 점수를 받은 총 개인/계정 프로필
* 다음 점수 작업(날짜)
* 다음 교육 작업(날짜)

자세한 내용은 [예측 리드 및 계정 점수 책정 모니터링 작업](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
