---
title: Real-Time CDP B2B에서 계정 일치로 리드
type: Documentation
description: Experience Platform CDP B2B의 리드-계정 일치 기능에 대한 개요 및 추가 정보입니다.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 4ba609e777716b1b38f5b143587e5476d851e344
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# Real-Time CDP B2B에서 계정 일치로 리드

## 개요 {#overview}

계정 기반 마케팅은 B2B 마케팅에 있어서 점점 더 중요한 전략이다. 계정 기반 마케팅은 특정 고가치 고객을 확보하기 위해 다음과 같은 주요 이점을 제공합니다.

- ROI 지우기
- 영업 및 마케팅 조정
- 개인화된 접근 방식
- 리소스 낭비 감소
- 판매 주기 단축

계정 기반 마케팅은 알려진 고객을 판매 계정에 연결하는 기능을 제공합니다. 이를 통해 마케팅 팀은 고객 여정 초기에 타겟 계정의 잠재적 리드와 참여하여 전환 가능성을 높일 수 있습니다. 알려진 개인 레코드에는 일반적으로 다음 정보의 일부 또는 전체가 포함됩니다.

- 개인 이름
- 이메일 주소
- 연락처 번호
- 회사명
- 회사 웹 사이트
- 직위
- 위치

## 작동 방식 {#how-it-works}

일별 실행 작업은 기존 계정 연결 없이 알려진 리드 프로필을 일치시키기 위해 결정론적 및 확률론적 요소를 모두 사용합니다. 알려진 잠재 고객 프로필에는 다음 속성 중 하나를 사용할 수 있습니다.

- b2b.companyName
- b2b.companyWebsite
- 회사 이메일

>[!NOTE]
>
> b2b.personKey.sourceKey 특성이 있어야 합니다.

b2b.companyName, b2b.companyWebsite 및 b2b.personKey.sourceKey 속성은 B2B 개인 스키마의 b2b 필드 그룹에 있을 수 있습니다.

![특성을 표시하는 B2B 개인 스키마](/help/rtcdp/accounts/images/b2b-person-schema.png)

workEmail 속성은 B2B 개인 스키마에서 최상위 필드 그룹으로 찾을 수 있습니다.

![B2B 개인 스키마에 회사 전자 메일이 표시됨](/help/rtcdp/accounts/images/b2b-person-workemail.png)

일치 점수가 내부 신뢰 임계값을 초과하는 경우에만 프로필이 가장 잘 일치합니다. 결과는 기존 계정 사용자 관계 XDM의 새 시스템 데이터 세트에 저장됩니다.

리드-계정 일치 서비스는 24시간마다 한 번씩 제공되는 새로운 사용자 프로필 스냅샷을 사용할 수 있게 될 때 실행됩니다. [계정 일치 리드의 구성](/help/rtcdp/accounts/account-profile-ui-guide.md)에 대한 자세한 내용은 설명서를 참조하세요.

## 리드-계정 일치 결과를 조회하는 방법 {#how-to-view}

작업 실행 후 결과는 기존 계정 사용자 관계 XDM의 새 데이터 세트에 저장됩니다.

데이터 집합을 미리 보려면 오른쪽 상단에서 **[!UICONTROL 데이터 집합 미리 보기]**&#x200B;를 선택하십시오.

![새 데이터 세트](/help/rtcdp/accounts/images/b2b-dataset-output.png)

데이터 세트에는 일치된 계정 정보와 선택한 데이터 세트에 대한 일치 점수가 포함됩니다. **[!UICONTROL 관계 Source]** 필드는 잠재 고객에서 계정 일치 프로세스로의 관계 여부를 나타냅니다.

![데이터 집합 신뢰도 점수 및 출력 미리 보기](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## 리드-계정 일치 작업 모니터링 {#monitoring-jobs}

대시보드를 통해 리드-계정 일치 작업에 대한 작업 상태 및 관련 지표를 모니터링할 수 있습니다.

[리드-계정 일치 작업 모니터링](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)에 대한 자세한 내용은 설명서를 참조하세요.
