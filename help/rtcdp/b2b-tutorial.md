---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;실시간 고객 데이터 플랫폼;실시간 cdp;b2b;cdp
solution: Experience Platform
title: Real-time Customer Data Platform B2B Edition 시작하기
description: Adobe Real-time Customer Data Platform B2B Edition 구현을 설정할 때 이 샘플 시나리오를 예로 사용하십시오.
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B Edition 시작하기

이 문서에서는 주요 개념을 설명하는 사용 사례 예를 사용하여 Real-time Customer Data Platform(CDP) B2B Edition을 시작하기 위한 높은 수준의 종단 간 워크플로우를 제공합니다.

기술 회사인 보데아는 이메일 및 LinkedIn 광고 캠페인을 통해 고객을 효과적으로 타겟팅하기 위해 서로 다른 분산된 데이터 소스의 개인 및 계정 데이터를 결합하려고 합니다. Bodea는 Marketo Engage을 마케팅 자동화 플랫폼으로 사용하며, 고객 데이터를 포함하는 여러 CRM의 B2B 관련 대상을 세그먼트화해야 합니다.

## 시작하기

이 자습서 워크플로우는 데모의 일부로 여러 Adobe Experience Platform 서비스를 사용합니다. 따라서 다음 서비스를 잘 이해하는 것이 좋습니다.

- [XDM(경험 데이터 모달)](../xdm/home.md)
- [소스](../sources/home.md)
- [세그먼테이션](../segmentation/home.md)
- [대상](../destinations/home.md)

## 데이터에 대한 스키마 만들기

초기 설정의 일부로, Bodea의 IT 부서는 데이터가 Platform으로 들어올 때 표준 형식을 따르도록 하기 위해 XDM 스키마를 만들어야 하며, 다양한 플랫폼 서비스 및 Adobe Experience Cloud 제품(예: Adobe Analytics 및 Adobe Target)에서 실행 가능합니다.

>[!WARNING]
>
>이 자습서 전체에서 연결된 관련 소스 설명서에서 설명한 대로 수집 패턴을 따라야 합니다. 다른 필드 매핑 방법은 작동하지 않을 수 있습니다.

Adobe Experience Platform을 사용하면 B2B 데이터 소스에 필요한 스키마와 네임스페이스를 자동으로 생성할 수 있습니다. 이 도구를 사용하면 생성된 스키마에서 구조화된 재사용 가능한 방식으로 데이터를 설명할 수 있습니다. 다음을 수행합니다 [B2B 네임스페이스 및 스키마 자동 생성 유틸리티 설명서](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) 설정 프로세스에 대한 완전한 참조.

Adobe Experience Platform UI에서 상위 마케터가 선택합니다 **[!UICONTROL 스키마]** 왼쪽 레일에서 를 차례로 **[!UICONTROL 찾아보기]** 탭. Marketo Engage 자동 생성 유틸리티를 사용하기 때문에 새 빈 스키마가 목록에 나타나고 모두 &quot;B2B&quot;라는 접두어가 있습니다.

![스키마 작업 공간 찾아보기 탭](./assets/b2b-tutorial/empty-b2b-schemas.png)

자동 생성 유틸리티는 표준 XDM B2B 클래스(예: )를 사용하여 스키마에 대한 데이터 모델 구조를 정의했습니다 [XDM 비즈니스 계정](../xdm/classes/b2b/business-account.md) 및 [XDM 비즈니스 기회](../xdm/classes/b2b/business-opportunity.md))에 대해 지속 기간을 한 번의 방문으로 설정해야 합니다. 또한 이러한 클래스에 빌드된 자동 생성 B2B 스키마에는 고급 세그멘테이션 사용 사례를 허용하는 미리 설정된 관계가 있습니다. 데이터 구조에 필요한 모든 추가 필드 그룹은 UI를 통해 여기에서 쉽게 만들 수 있습니다. 자세한 내용은 [XDM UI 안내서, 스키마 섹션에 필드 그룹 추가](../xdm/ui/resources/schemas.md#add-field-groups) 추가 정보.

>[!NOTE]
> 
>자동 생성 유틸리티를 사용하지 않거나 새 관계를 만들어야 하는 경우에는 다음 자습서를 참조하십시오 [B2B 스키마 간 관계 만들기](../xdm/tutorials/relationship-b2b.md).

실시간 고객 프로필은 서로 다른 소스의 데이터를 병합하여 주요 B2B 엔티티의 통합 프로필을 만듭니다. 프로필은 단일 클래스를 기반으로 생성되므로 자동 생성 유틸리티는 일반적인 비즈니스 사용 사례에 따라 스키마 간의 관계를 설정합니다. 따라서 Bodea 팀은 이제 B2B 스키마를 기반으로 데이터를 수집할 준비가 되었습니다.

>[!NOTE]
> 
>자동 생성 유틸리티로 스키마에 대해 생성된 기본 ID 네임스페이스, 기본 키 및 관계는 스키마 작업 공간에서 쉽게 검색할 수 있습니다.
>
>![기본 스키마 ID 및 관계 UI 표시](./assets/b2b-tutorial/schema-identity-relationship.png)

## 데이터를 Experience Platform에 수집

다음으로, 보데아 마케터는 [Marketo Engage 커넥터](../sources/connectors/adobe-applications/marketo/marketo.md) 다운스트림 서비스에서 사용할 데이터를 Platform으로 수집할 수 있습니다. Real-Time CDP B2B Edition에 대해 승인된 소스 중 하나를 사용하여 데이터를 수집할 수도 있습니다.

>[!NOTE]
> 
>조직에서 사용할 수 있는 소스 커넥터를 학습하기 위해 플랫폼 UI에서 소스 카탈로그를 볼 수 있습니다. 카탈로그에 액세스하려면 다음을 선택합니다 **소스** 왼쪽 탐색에서 를 선택하고 **카탈로그**.

Marketo 계정과 플랫폼 간에 연결을 만들려면 인증 자격 증명을 획득해야 합니다. 자세한 내용은 [Marketo 소스 커넥터 인증 자격 증명 획득에 대한 안내서](../sources/connectors/adobe-applications/marketo/marketo-auth.md) 자세한 지침

인증 자격 증명을 획득한 후 목표 마케터는 Marketo 계정과 해당 플랫폼 IMS 조직 간에 연결을 만듭니다. 에 대한 지침은 설명서를 참조하십시오. [플랫폼 UI를 사용하여 Marketo 계정을 연결하는 방법](../sources/tutorials/ui/create/adobe-applications/marketo.md).

Marketo Engage 소스 커넥터는 모든 데이터 필드를 새로 만든 스키마에 매핑하는 프로세스를 훨씬 쉽게 하기 위한 자동 매핑 기능을 제공합니다.

>[!NOTE]
> 
>XDM 스키마에서 사용자 지정 필드 그룹을 만든 경우 이 프로세스 단계에서 연결되지 않은 필드가 있을 수 있습니다. 사용자 지정 필드 그룹을 채우는 모든 값을 확인해야 합니다.

목표 마케터는 모든 필드 그룹이 적절하게 매핑되는지 확인하고 데이터 흐름을 초기화하여 소스 설정 프로세스를 계속합니다. Marketo 데이터를 가져올 데이터 흐름을 만들어 다운스트림 Platform 서비스에서 들어오는 데이터를 사용할 수 있습니다. 초기 수집 프로세스 중에 데이터가 Experience Platform으로 배치됩니다. 그런 다음 수집된 이후에 수집된 데이터는 거의 실시간으로 업데이트되는 프로필로 스트리밍됩니다.

## 데이터를 평가할 세그먼트 만들기

다음 작업은 소스 데이터에 있는 관련 엔티티의 특정 특성을 기반으로 Bodea의 새 이메일 마케팅 캠페인에 대한 대상을 만드는 것입니다. Platform UI에서 상위 마케터가 먼저 선택합니다 **[!UICONTROL 세그먼트]** 왼쪽 탐색 영역에서 다음을 수행합니다. **[!UICONTROL 세그먼트 만들기]**.

이 예에서는 세그먼트가 영업 부서에서 근무하며 영업 기회가 하나 이상 있는 모든 계정과 관련된 모든 직원을 찾습니다. 이 세그먼트에는 XDM 개별 프로필 클래스, XDM 비즈니스 계정 클래스 및 XDM 비즈니스 기회 클래스 간의 링크가 필요합니다.

![사용 사례 세그먼트](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>데이터를 평가할 세그먼트를 만드는 방법에 대한 지침은 [세그먼트 빌더 UI 안내서](../segmentation/ui/segment-builder.md). 구체적인 B2B 세그멘테이션 사용 사례는 다음을 참조하십시오. [Real-Time CDP B2B Edition에 대한 세그멘테이션 개요](./segmentation/b2b.md).

세그먼트 빌더 를 사용하면 실시간 고객 프로필 데이터에서 마케팅 가능한 대상을 만들고 정의한 속성, 이벤트 및 기존 대상의 조합을 기반으로 예상 대상의 예측을 볼 수 있습니다.

## 평가된 데이터를 대상으로 활성화

세그먼트가 성공적으로 만들어지면 의 [!UICONTROL 세부 사항] 섹션을 참조하십시오. 현재 세그먼트에 대해 활성화된 대상이 없으므로 목표 마케터는 해당 대상을 액세스 및 작업할 수 있는 데이터 세트로 내보내야 합니다.

내 [!UICONTROL 세그먼트] 플랫폼 UI의 작업 영역에서 상위 마케터가 선택합니다 **[!UICONTROL 대상에 활성화]**.

![대상에 세그먼트 활성화](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>다음에서 자습서를 참조하십시오. [대상에 세그먼트 활성화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) 를 참조하십시오.

상위 마케터는 Marketo 대상에 대한 세그먼트를 활성화하여 세그먼트 데이터를 정적 목록 형태로 Platform에서 Marketo Engage으로 푸시할 수 있습니다. 의 안내서를 참조하십시오. [Marketo 대상](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) 추가 정보.

## 다음 단계

이 자습서를 따라 Real-Time CDP B2B Edition에서 사용하는 다양한 Adobe Experience Platform 서비스를 성공적으로 활용했습니다. 그 결과, 다양한 채널에서 참여할 수 있는 실행 가능한 대상으로 B2B 데이터를 수집, 세그먼트화, 평가 및 내보내는 방법을 학습했습니다.
