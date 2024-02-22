---
title: 대상에 대한 계정 대상자 활성화
type: Tutorial
description: 대상에 대한 계정 대상을 활성화하는 방법을 알아봅니다
badgeB2B: label="B2B 버전" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P 버전" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: f07eb12b4625bce117e1fe524727c00b7188aa5e
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# 계정 대상자 활성화

>[!AVAILABILITY]
>
>을(를) 구매하는 회사는 대상에 대한 계정 대상을 활성화할 수 있습니다. [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) 및 [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2b) Real-time Customer Data Platform 에디션.

이 문서에서는 내보내기에 필요한 워크플로에 대해 설명합니다 [계정 대상자](/help/segmentation/ui/account-audiences.md) Adobe Experience Platform에서 원하는 대상으로 이동합니다.

## 지원되는 대상 {#supported-destinations}

다음으로 이동 **[!UICONTROL 연결]** > **[!UICONTROL 대상]**&#x200B;을(를) 클릭하고 **[!UICONTROL 카탈로그]** 탭. 사용 **[!UICONTROL 데이터 유형]** 필터링 및 선택 **[!UICONTROL 계정]** 계정 대상자 활성화를 지원하는 대상을 확인합니다. 현재 계정 대상자 내보내기는 특정 클라우드 스토리지 대상([Amazon](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS 세대 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Azure Blob 저장소](/help/destinations/catalog/cloud-storage/azure-blob.md), [데이터 랜딩 영역](/help/destinations/catalog/cloud-storage/data-landing-zone.md), 및 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) 및 [(회사) LinkedIn 일치 대상](/help/destinations/catalog/social/linkedin.md) 대상.

![계정 대상을 지원하는 대상.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## 전제 조건 {#prerequisites}

* 먼저 수집해야 합니다. [계정 프로필](/help/rtcdp/accounts/account-profile-overview.md) 및 만들기 [계정 대상자](/help/segmentation/ui/account-audiences.md) 다운스트림 대상으로 활성화하기 전에
* 대상에 계정 대상을 활성화하려면 대상에 성공적으로 연결해야 합니다. 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)에서 지원되는 대상을 탐색하고 사용할 대상을 구성합니다. 의 UI 튜토리얼 읽기 [대상에 연결](./connect-destination.md) 추가 정보.

### 필요 권한 {#permissions}

계정 대상자를 활성화하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

계정 대상을 활성화하는 데 필요한 권한이 있는지 확인하려면 대상 카탈로그를 확인하십시오. 대상에 다음 항목이 있는 경우 **[!UICONTROL 활성화]** 을 제어한 다음 적절한 사용 권한을 갖습니다.

## 대상 선택 {#select-destination}

지침에 따라 데이터 세트를 내보낼 수 있는 대상을 선택합니다.

1. 다음으로 이동 **[!UICONTROL 연결 > 대상]**&#x200B;을(를) 클릭하고 **[!UICONTROL 카탈로그]** 탭.

   ![카탈로그 컨트롤이 강조 표시된 대상 카탈로그 탭.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 선택 **[!UICONTROL 활성화]** 데이터 세트를 내보낼 대상에 해당하는 카드에서 다음을 수행합니다.

>[!TIP]
>
>계정 대상을 내보낼 수 있는 대상은 카드 오른쪽 상단에 아래에 강조 표시된 대상과 유사한 아이콘으로 표시되거나, 데이터 유형 필터를 사용하여 계정 대상을 내보낼 수 있는 대상만 표시할 수 있습니다. [페이지 상단에 표시](#supported-destinations).

![강조 표시된 프로필 대상을 내보낼 수 있는 Amazon S3 대상 페이지입니다.](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. 선택 **[!UICONTROL 데이터 유형 계정]**&#x200B;을 클릭한 다음 데이터 세트를 내보낼 대상 연결이 옵니다. 그런 다음 을 선택합니다. **[!UICONTROL 다음]**.

>[!TIP]
> 
>계정 대상을 활성화하기 위해 새 대상을 설정하려면 다음을 선택합니다. **[!UICONTROL 새 대상 구성]** 을(를) 트리거하려면 [대상에 연결](/help/destinations/ui/connect-destination.md) 워크플로우 및 [데이터 유형으로 계정 선택](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![계정 컨트롤이 강조 표시된 대상 활성화 워크플로우입니다.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. 다음 섹션으로 이동하여 [계정 대상자 선택](#select-profile-audiences) 내보내기입니다.

## 계정 대상자 선택 {#select-account-audiences}

계정 대상자 이름의 왼쪽에 있는 확인란을 사용하여 대상으로 내보낼 대상자를 선택한 다음 을 선택합니다 **[!UICONTROL 다음]**. 참고 사항만 *계정 대상자* 이 보기에 표시되며, 다른 대상자 유형은 표시되지 않습니다.

![내보낼 계정 대상을 선택할 수 있는 대상 선택 단계를 표시하는 데이터 세트 내보내기 워크플로.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## 예약 및 다음 단계

계정 대상을 내보내는 활성화 워크플로의 나머지 부분에 대해서는 파일 기반 대상으로 데이터 활성화에 대한 자습서를 참조하십시오. 다음 항목에서 계속 [대상자 내보내기 단계 예약](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). 에 대한 계정 대상을 활성화하는 경우 **[!UICONTROL (회사) LinkedIn 일치 대상]** 대상, 스트리밍 대상 활성화에 대한 자습서를 참조하십시오. 다음 항목에서 계속 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>예약 단계에서 계정 대상을 클라우드 스토리지 대상으로 내보낼 때 계정 대상을 활성화하는 워크플로에서는 내보내기만 할 수 있습니다 [전체 파일](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _일별 일정으로_. 시간별 내보내기는 지원되지 않습니다. 참고 사항 **[!UICONTROL 대상 평가 후]** 는 유일하게 지원되는 평가 유형입니다.

## 중요한 콜아웃 및 알려진 제한 사항 {#important-callouts-known-limitations}

계정 대상을 활성화하는 기능의 일반 가용성 릴리스에 대한 다음의 중요한 콜아웃 및 알려진 제한을 참조하십시오.

### 에 대한 계정 대상을 활성화할 때 매핑 단계에서 필요한 매핑 쌍 **[!UICONTROL (회사) LinkedIn 일치 대상]** 대상 {#required-mappings}

계정 대상자를 활성화할 때 **[!UICONTROL (회사) LinkedIn 일치 대상]** 대상: 데이터를 성공적으로 내보내려면 다음 두 매핑 쌍이 필요합니다.

![LinkedIn 매핑 필수 필드.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| 소스 필드 | 대상 필드 |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (다음에서 이 필드 선택: **[!UICONTROL ID 네임스페이스 선택]** 보기, 선택 시 **[!UICONTROL 대상 필드]**). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 계정 대상자를 활성화합니다.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 계정 대상자를 활성화합니다."){width="100" zoomable="yes"} |

### 데이터 거버넌스 적용 {#data-governance-enforcement}

다음에 대한 개인 또는 프로필 수준에서 동의가 시행됩니다. *고객 및 잠재 고객*. 따라서  [동의 정책 평가](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 은(는) 계정 대상자를 대상으로 활성화할 때 현재 지원되지 않습니다. 활성화 워크플로의 검토 단계에서에 대해 회색으로 표시된 컨트롤을 볼 수 있습니다. **[!UICONTROL 해당 동의 정책 보기]**.

![동의 적용 제어가 회색으로 표시된 계정 대상자 활성화 워크플로의 검토 단계입니다.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

다음과 같은 Real-Time CDP의 기타 데이터 거버넌스 메커니즘 [데이터 사용 정책 확인](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 및 [속성 기반 액세스 제어](/help/destinations/home.md#attribute-based-access) 이 지원됩니다.
