---
title: Real-Time CDP B2B edition으로 아키텍처 업그레이드
description: Real-Time CDP B2B edition으로의 포괄적인 아키텍처 업그레이드에 대해 알아보려면 이 문서 를 참조하십시오.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d958a947-e195-4dd4-a04c-63ad82829728
source-git-commit: 1a3be99ca3c270dda6e8dc559359cbe21bb8f4fb
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Real-Time CDP B2B edition으로 아키텍처 업그레이드

>[!IMPORTANT]
>
>이 문서에서는 Real-Time CDP B2B 및 B2P 에디션에 대한 아키텍처 업그레이드에 대해 간략하게 설명합니다. 업그레이드는 대부분의 고객의 작업이 필요하지 않습니다. 그러나 자동으로 업그레이드할 수 없는 대상도 있습니다. Adobe은 사용자와 직접 협력하여 이러한 시나리오를 해결합니다. 업그레이드가 Adobe Experience Platform의 기존 기능에 미치는 영향에 대한 자세한 내용은 이 문서 를 참조하십시오. 질문이 있는 경우 Adobe 계정 팀에 문의하십시오.

Adobe은 확장성, 성능 및 안정성을 향상하는 동시에 보다 고급 B2B 사용 사례를 지원하기 위해 Real-Time CDP B2B 및 B2P 에디션을 다시 설계했습니다. 모든 고객이 이러한 개선 사항의 혜택을 누릴 수 있도록 Adobe은 기존의 모든 B2B 및 B2P 고객을 새로운 아키텍처로 업그레이드합니다.

다음과 같은 이점을 얻으려면 향상된 아키텍처를 사용하십시오.

* **데이터 수집의 확장성**: 수천 명의 사용자에게 연결된 계정과 같은 카디널리티가 높은 B2B 관계에 대한 지원이 개선되었습니다.
* **성능이 뛰어나고 안정적인 대상 평가**: 복잡한 B2B 대상을 위한 보다 빠르고 탄력적인 세분화
* **엔티티 해상도**: B2B 엔티티에 대한 ID 해상도를 개선하고 데이터 품질을 개선하며 중복을 줄여 보다 정확한 세분화 및 집계를 가능하게 합니다.

## 새로운 기능

아키텍처 업그레이드에 포함된 주요 개선 사항은 다음을 참조하십시오.

### 대상자 멤버십에 대한 계정 스냅샷

새로운 B2B 아키텍처를 사용하면 이제 스냅샷 내보내기에서 계정 엔티티에 대한 대상 멤버십 세부 사항이 포함됩니다. 이 기능을 사용하면 계정 수준 대상 상태, 타임스탬프 및 멤버십 지표에 액세스할 수 있습니다.

이번 업그레이드를 통해 다음과 같은 작업을 수행할 수 있습니다.

* 마케팅 및 운영 팀이 계정 대상자 멤버십의 유효성을 직접 확인할 수 있습니다.
* 프로필(개인)과 계정 세분화 모델 간의 기능 패리티를 달성하여 엔터티 간 일관된 경험을 보장합니다.

자세한 내용은 [계정 대상자](../segmentation/types/account-audiences.md)에 대한 설명서를 참조하십시오.

### B2B 엔티티를 포함하는 대상에 대한 대상 개수

B2B 엔티티가 있는 대상에 대한 대상 크기 예상은 이제 정확한 정밀도로 계산됩니다. 이러한 예상치는 미리보기 중에 사용할 수 있으며, 복잡한 B2B 관계를 포함하는 대상자에게 보다 정확하고 신뢰할 수 있는 통찰력을 제공합니다.

이번 업그레이드를 통해 다음과 같은 작업을 수행할 수 있습니다.

* 정확한 대상 크기 추정치의 통찰력을 사용하여 대상 만들기 프로세스 동안 계획 및 의사 결정을 개선합니다.
* 보다 정확한 대상 추정에 대한 지식을 사용하여 복잡한 B2B 대상을 자신 있게 설계합니다.
* 보다 스마트한 캠페인 계획, 보다 정확한 타겟팅 및 더 나은 리소스 할당을 허용합니다.

자세한 내용은 [계정 대상자](../segmentation/types/account-audiences.md)에 대한 설명서를 참조하십시오.

## 기존 기능으로 업그레이드

다음 기능은 B2B 아키텍처 업그레이드의 일부로 업데이트되었습니다.

### B2B 속성 및 경험 이벤트를 사용한 다중 엔티티 대상 업데이트

새 아키텍처 업그레이드의 일부로, B2B 속성을 포함하는 단일 다중 엔티티 대상 내에서는 경험 이벤트 필터를 더 이상 사용할 수 없습니다.

세그먼트 빌더를 사용하여 [대상을 추가하고 대상 참조](../segmentation/ui/segment-builder.md#adding-audiences)를 수행하면 동일한 대상 논리를 얻을 수 있습니다

예:

* 경험 이벤트 대상자 만들기
   * 동작 조건을 별도로 정의합니다. 예를 들어 &quot;지난 3일 동안 가격 책정 페이지를 방문한 사람&quot;입니다.
* B2B 속성을 사용하여 다중 엔티티 대상을 만듭니다.
   * 여기에서 경험 이벤트 대상을 이 대상의 기준의 일부로 참조할 수 있습니다. 예를 들어 &quot;계정이 **의 &#39;재무&#39;** 산업에 있는 모든 기회의 **&#39;의사 결정자&#39;**&#x200B;인 직원과 지난 3일 동안 가격 책정 페이지를 방문한 사용자 대상의 구성원입니다.

업그레이드가 완료되면 [segment-of-segment](../segmentation/methods/edge-segmentation.md#edge-segmentation-query-types) 접근 방식을 사용하여 B2B 특성 및 경험 이벤트가 있는 새 다중 엔티티 대상을 만들어야 합니다.

>[!TIP]
>
>**세그먼트**&#x200B;은(는) 하나 이상의 일괄 처리 또는 에지 세그먼트를 포함하는 세그먼트 정의입니다. **참고**: 세그먼트의 세그먼트를 사용하는 경우 **24시간마다**&#x200B;프로필이 중단됩니다.

### B2B 대상에서 엔티티 해결 및 시간 우선 순위 병합

아키텍처 업그레이드의 일환으로 Adobe은 계정 및 기회에 대한 엔티티 해결을 도입합니다. 엔티티 확인은 결정론적 ID 일치 및 최신 데이터를 기반으로 합니다. 엔티티 해결 작업은 B2B 속성을 사용하여 다중 엔티티 대상을 평가하기 전에 일괄 처리 세분화 동안 매일 실행됩니다.

>[!BEGINSHADEBOX]

#### 엔티티 해결은 어떻게 작동합니까?

* **이전**: DUNS(Data Universal Numbering System) 번호를 추가 ID로 사용하고 계정의 DUNS 번호가 CRM과 같은 소스 시스템에서 업데이트된 경우 계정 ID는 이전 및 새 DUNS 번호에 모두 연결됩니다.
* **이후**: DUNS 번호를 추가 ID로 사용하고 계정의 DUNS 번호가 CRM과 같은 소스 시스템에서 업데이트된 경우 계정 ID는 새 DUNS 번호에만 연결되므로 현재 계정 상태를 보다 정확하게 반영합니다.

>[!ENDSHADEBOX]

이번 업그레이드를 통해 다음과 같은 작업을 수행할 수 있습니다.

* 일별 엔터티 확인 작업이 완료되면 [!DNL Profile Access] API를 사용하여 최신 병합 프로필을 봅니다.
* 세분화, 활성화 및 분석을 위해 계정 및 기회 데이터의 정확도와 일관성이 개선되었습니다.

자세한 내용은 [[!DNL Profile Access] API](../profile/api/entities.md)을(를) 참조하십시오.

### 다중 엔티티 B2B 대상의 병합 정책 지원

B2B 특성이 있는 다중 엔티티 대상은 이제 여러 병합 정책 대신 단일 병합 정책(사용자가 구성하는 기본 병합 정책)을 지원합니다.

자세한 내용은 Real-Time CDP B2B edition의 [세그먼테이션 사용 사례 안내서](./segmentation/b2b.md)를 참조하세요.

### [!DNL Profile Access] API에서 B2B 엔터티 조회 및 삭제 사용 중단

[!DNL Profile Access] API를 사용하는 B2B 엔터티에 대한 다음 조회 기능은 더 이상 사용되지 않습니다.

* 계정-사용자 관계
* 영업 기회-사용자 관계
* Campaign
* 캠페인 멤버
* 마케팅 목록
* 마케팅 목록 구성원

[!DNL Profile Access] API를 사용하는 다음 B2B 엔터티에 대한 삭제 요청이 더 이상 사용되지 않습니다.

* 계정
* 계정-사용자 관계
* 기회
* 영업 기회-사용자 관계
* Campaign
* 캠페인 멤버
* 마케팅 목록
* 마케팅 목록 구성원

자세한 내용은 [[!DNL Profile Access] API](../profile/api/entities.md)을(를) 참조하십시오.

### 계정 및 영업 기회 프로필 조회

이제 일별 엔티티 해결 프로세스를 완료한 후에만 계정 및 영업 기회 스키마를 조회 차원 엔티티로 검색할 수 있습니다. 다음 엔티티 해결 주기가 완료될 때까지(일반적으로 24시간마다) 새로 수집된 레코드를 프로필 보강 또는 세그먼트 정의에 사용할 수 없습니다.

<!-- ### Deprecation of audience creation via API for B2B entities

Creation of audiences using B2B entities via API is being deprecated. The list of affected B2B entities include:

* Account
* Opportunity
* Account-Person Relation
* Opportunity-Person Relation
* Campaign
* Campaign Member
* Marketing List
* Marketing List Member

Read the [segment definitions endpoint API guide](../segmentation/api/segment-definitions.md) for more information. -->

### 샌드박스 툴에서 다중 엔티티 대상 가져오기 변경

아키텍처 업그레이드를 사용하면, 이러한 대상을 포함한 패키지가 업그레이드 전에 게시된 경우 B2B 속성 및 경험 이벤트가 있는 다중 엔티티 대상을 더 이상 가져올 수 없습니다. 이러한 대상은 가져오지 못하며 자동으로 새 아키텍처로 변환될 수 없습니다. 이 제한을 해결하려면 업데이트된 대상으로 새 패키지를 만든 다음 샌드박스 도구를 사용하여 해당 대상 샌드박스로 가져와야 합니다.

개발 샌드박스가 새 아키텍처로 업그레이드됩니다. 자동 업데이트할 수 있는 대상은 업그레이드되고 비활성화할 수 없는 대상은 비활성화됩니다. 비활성화된 대상은 업그레이드 후에 다시 만들어야 합니다.

자세한 내용은 [샌드박스 도구 가이드](../sandboxes/ui/sandbox-tooling.md)를 참조하십시오.
