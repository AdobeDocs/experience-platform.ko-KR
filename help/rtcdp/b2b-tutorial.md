---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;실시간 고객 데이터 플랫폼;실시간 cdp;b2b;cdp
solution: Experience Platform
title: Real-Time Customer Data Platform B2B edition 시작하기
description: Adobe Real-Time Customer Data Platform B2B edition 구현을 설정할 때 이 샘플 시나리오를 예로 사용하십시오.
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---

# Real-Time Customer Data Platform B2B edition 시작하기

이 문서에서는 주요 개념을 설명하는 예제 사용 사례를 사용하여 Real-Time Customer Data Platform(CDP) B2B edition을 시작하기 위한 높은 수준의 종단 간 워크플로우를 제공합니다.

기술 회사 Bodea는 새로운 제품에 대한 이메일 및 LinkedIn 광고 캠페인으로 고객을 효과적으로 공략하기 위해 다른 사일로 데이터 소스의 개인과 계정 데이터를 결합하려고 합니다. Bodea는 Marketo Engage을 마케팅 자동화 플랫폼으로 사용하며 고객 데이터가 포함된 여러 CRM에서 B2B별 대상을 세그먼트화해야 합니다.

## 시작하기

이 자습서 워크플로우는 데모의 일부로서 여러 Adobe Experience Platform 서비스를 사용합니다. 다음을 따라가려면 다음 서비스를 잘 이해하는 것이 좋습니다.

- [경험 데이터 모델 (XDM)](../xdm/home.md)
- [소스](../sources/home.md)
- [세그먼테이션](../segmentation/home.md)
- [대상](../destinations/home.md)

## 데이터에 대한 스키마 만들기

초기 설정의 일부로, Bodea의 IT 부서에서는 데이터가 Experience Platform으로 가져올 때 표준 형식을 따르고 다양한 Experience Platform 서비스 및 Adobe Experience Cloud 제품(예: Adobe Analytics 및 Adobe Target)에서 조치를 취할 수 있도록 XDM 스키마를 만들어야 합니다.

>[!WARNING]
>
>이 자습서 전체에 연결된 관련 소스 설명서에 설명된 대로 수집 패턴을 따라야 합니다. 다른 필드 매핑 방법은 작동하지 않을 수 있습니다.

Adobe Experience Platform을 사용하면 B2B 데이터 소스에 필요한 스키마 및 네임스페이스를 자동으로 생성할 수 있습니다. 이 도구는 생성된 스키마가 구조화된 재사용 가능한 방식으로 데이터를 설명하도록 합니다. 설정 프로세스에 대한 전체 참조를 보려면 [B2B 네임스페이스 및 스키마 자동 생성 유틸리티 설명서](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)를 따르십시오.

Adobe Experience Platform UI 내에서 Bodea 마케터는 왼쪽 레일에서 **[!UICONTROL 스키마]**&#x200B;를 선택한 다음 **[!UICONTROL 찾아보기]** 탭을 선택합니다. Marketo Engage 자동 생성 유틸리티를 사용했으므로 새 빈 스키마가 목록에 표시되며 모두 &quot;B2B&quot;라는 접두어가 있습니다.

![스키마 작업 영역 찾아보기 탭](./assets/b2b-tutorial/empty-b2b-schemas.png)

자동 생성 유틸리티는 기본 B2B 데이터 엔터티를 캡처하는 표준 XDM B2B 클래스(예: [XDM 비즈니스 계정](../xdm/classes/b2b/business-account.md) 및 [XDM 비즈니스 영업 기회](../xdm/classes/b2b/business-opportunity.md))를 사용하여 스키마에 대한 데이터 모델 구조를 정의했습니다. 또한 이러한 클래스에 구축된 자동 생성된 B2B 스키마에는 고급 세분화 사용 사례를 허용하는 사전 설정된 관계가 있습니다. 데이터 구조에 필요한 모든 추가 필드 그룹은 UI를 통해 여기에서 쉽게 만들 수 있습니다. 자세한 내용은 [XDM UI 안내서, 스키마 섹션에 필드 그룹 추가](../xdm/ui/resources/schemas.md#add-field-groups)를 참조하십시오.

>[!NOTE]
> 
>자동 생성기 유틸리티를 사용하지 않거나 새 관계를 만들어야 하는 경우 [B2B 스키마 간의 관계 만들기](../xdm/tutorials/relationship-b2b.md)에 대한 자습서를 참조하십시오.

Real-Time Customer Profile은 서로 다른 소스의 데이터를 병합하여 주요 B2B 엔티티의 통합 프로필을 만듭니다. 프로필은 단일 클래스를 기반으로 생성되므로 자동 생성 유틸리티는 일반적인 비즈니스 사용 사례를 기반으로 스키마 간의 관계를 설정합니다. 따라서 Bodea 팀은 이제 B2B 스키마를 기반으로 데이터를 수집할 준비가 되었습니다.

>[!NOTE]
> 
>자동 생성 유틸리티로 스키마에 대해 생성된 기본 ID 네임스페이스, 기본 키 및 관계는 스키마 작업 영역 내에서 쉽게 검색할 수 있습니다.
>
>![기본 스키마 ID 및 관계 UI 표시](./assets/b2b-tutorial/schema-identity-relationship.png)

## Experience Platform에 데이터 수집

다음으로 Bodea 마케터는 [Marketo Engage 커넥터](../sources/connectors/adobe-applications/marketo/marketo.md)를 사용하여 다운스트림 서비스에 사용할 데이터를 Experience Platform에 수집합니다. Real-Time CDP B2B edition에 대해 승인된 소스 중 하나를 사용하여 데이터를 수집할 수도 있습니다.

>[!NOTE]
> 
>조직에서 사용할 수 있는 소스 커넥터를 알려면 Experience Platform UI에서 소스 카탈로그를 볼 수 있습니다. 카탈로그에 액세스하려면 왼쪽 탐색에서 **소스**&#x200B;를 선택한 다음 **카탈로그**&#x200B;를 선택하십시오.

Marketo 계정과 Experience Platform 간에 연결을 만들려면 인증 자격 증명을 획득해야 합니다. 자세한 지침은 [Marketo 소스 커넥터 인증 자격 증명 달성에 대한 안내서](../sources/connectors/adobe-applications/marketo/marketo-auth.md)를 참조하십시오.

인증 자격 증명을 획득한 후 Bodea 마케터는 Marketo 계정과 해당 Experience Platform 조직 간의 연결을 만듭니다. [Experience Platform UI를 사용하여 Marketo 계정을 연결하는 방법](../sources/tutorials/ui/create/adobe-applications/marketo.md)에 대한 지침은 설명서를 참조하십시오.

Marketo Engage 소스 커넥터는 모든 데이터 필드를 새로 만든 스키마의 데이터 필드에 매핑하는 프로세스를 훨씬 쉽게 할 수 있는 자동 매핑 기능을 제공합니다.

>[!NOTE]
> 
>XDM 스키마에서 사용자 정의 필드 그룹을 만든 경우 이 프로세스 단계에서 연결되지 않은 필드가 있을 수 있습니다. 사용자 정의 필드 그룹을 채우는 모든 값을 확인하십시오.

Bodea 마케터는 모든 필드 그룹이 적절하게 매핑되었는지 확인하고 데이터 흐름을 초기화하여 소스 설정 프로세스를 계속합니다. Marketo 데이터를 가져오는 데이터 흐름을 만들어 들어오는 데이터를 다운스트림 Experience Platform 서비스에서 사용할 수 있습니다. 초기 수집 프로세스 동안 데이터가 배치로 Experience Platform에 전송됩니다. 이후, 이후에 수집된 데이터는 실시간에 가까운 업데이트로 프로필에 스트리밍됩니다.

## 데이터를 평가할 대상 만들기

다음 작업은 소스 데이터의 관련 엔티티의 특정 속성을 기반으로 Bodea의 새 이메일 마케팅 캠페인에 대한 대상을 만드는 것입니다. Experience Platform UI 내에서 Bodea 마케터는 먼저 왼쪽 탐색에서 **[!UICONTROL 세그먼트]**&#x200B;를 선택한 다음 **[!UICONTROL 세그먼트 만들기]**&#x200B;를 선택합니다.

이 예에서 대상은 판매 부서에서 근무하며 최소 하나 이상의 영업 기회가 있는 모든 계정과 관련된 모든 인력을 찾습니다. 이 대상에는 XDM 개인 프로필 클래스, XDM 비즈니스 계정 클래스 및 XDM 비즈니스 영업 기회 클래스 간의 링크가 필요합니다.

![사용 사례 세그먼트](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>데이터를 평가할 대상을 만드는 방법에 대한 지침은 [세그먼트 빌더 UI 안내서](../segmentation/ui/segment-builder.md)를 참조하세요. 자세한 B2B 세그멘테이션 사용 사례는 [Real-Time CDP B2B edition에 대한 세그멘테이션 개요](./segmentation/b2b.md)를 참조하십시오.

세그먼트 빌더를 사용하면 실시간 고객 프로필 데이터에서 마케팅 가능한 대상을 만들고 속성, 이벤트 및 정의한 기존 대상의 조합을 기반으로 예상 대상의 예상 예상 크기를 볼 수 있습니다.

## 평가된 데이터를 대상에 활성화

대상자가 만들어지면 작업 영역의 [!UICONTROL 세부 정보] 섹션에 요약이 제공됩니다. 세그먼트 정의에 대해 현재 활성화된 대상이 없으므로 Bodea 마케터는 대상자를 액세스 및 작업을 수행할 수 있는 데이터 세트로 내보내야 합니다.

Experience Platform UI의 [!UICONTROL 세그먼트] 작업 영역에서 Bodea 마케터는 **[!UICONTROL 대상에 활성화]**&#x200B;를 선택합니다.

![대상에 대상 활성화](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>이를 수행하는 방법에 대한 포괄적인 단계를 보려면 [대상자를 대상으로 활성화](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=ko)에 대한 자습서를 참조하십시오.

Bodea 마케터는 대상을 Marketo 대상으로 활성화하여 대상 데이터를 정적 목록의 형태로 Experience Platform에서 Marketo Engage으로 푸시할 수 있습니다. 자세한 내용은 [Marketo 대상](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html?lang=ko)의 안내서를 참조하십시오.

## 다음 단계

이 자습서를 따라 Real-Time CDP B2B edition에서 사용하는 다양한 Adobe Experience Platform 서비스를 성공적으로 활용했습니다. 따라서 B2B 데이터를 여러 채널에서 참여할 수 있는 실행 가능한 대상으로 수집, 세그먼트화, 평가 및 내보내는 방법을 배웠습니다.
