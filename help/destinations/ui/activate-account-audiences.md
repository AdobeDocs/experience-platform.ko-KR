---
title: 대상에 대한 계정 대상자 활성화
type: Tutorial
description: 대상에 대한 계정 대상을 활성화하는 방법을 알아봅니다
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ko#rtcdp-editions newtab=true"
badgeB2P: label="B2P 버전" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ko#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 4afb2c76f2022423e8f1fa29c91d02b43447ba90
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# 계정 대상자 활성화

>[!AVAILABILITY]
>
>Real-Time Customer Data Platform의 [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) 및 [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) 에디션을 구매하는 회사는 계정 대상자를 대상으로 활성화하는 기능을 사용할 수 있습니다.

이 문서에서는 [계정 대상자](/help/segmentation/types/account-audiences.md)를 Adobe Experience Platform에서 원하는 대상으로 내보내는 데 필요한 워크플로에 대해 설명합니다.

## 지원되는 대상 {#supported-destinations}

**[!UICONTROL 연결]** > **[!UICONTROL 대상]**(으)로 이동한 다음 **[!UICONTROL 카탈로그]** 탭을 선택합니다. **[!UICONTROL 데이터 형식]** 필터를 사용하고 **[!UICONTROL 계정]**&#x200B;을 선택하여 계정 대상의 활성화를 지원하는 대상을 확인하십시오. 현재 계정 대상 내보내기는 특정 클라우드 저장소 대상([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Azure Blob 저장소](/help/destinations/catalog/cloud-storage/azure-blob.md), [데이터 랜딩 영역](/help/destinations/catalog/cloud-storage/data-landing-zone.md) 및 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md))과 [Demandbase](/help/destinations/catalog/advertising/demandbase.md) 및 [(회사) LinkedIn Matched Audiences](/help/destinations/catalog/social/linkedin-b2b.md) 스트리밍 대상에만 사용할 수 있습니다.

계정 대상을 지원하는 ![대상.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## 비디오 개요

계정 대상자 만들기 및 활성화에 대한 개요와 계정 대상자 활성화 시 지원되는 사용 사례에 대해서는 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## 전제 조건 {#prerequisites}

* 다운스트림 대상으로 활성화하려면 먼저 [계정 프로필](/help/rtcdp/accounts/account-profile-overview.md)을(를) 수집하고 [계정 대상자](/help/segmentation/types/account-audiences.md)를 만들어야 합니다.
* 대상에 계정 대상을 활성화하려면 대상에 성공적으로 연결해야 합니다. 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)(으)로 이동하여 지원되는 대상을 탐색하고 사용할 대상을 구성합니다. 자세한 내용은 [대상에 연결](./connect-destination.md)에 대한 UI 자습서를 참조하십시오.

### 필요한 권한 {#permissions}

계정 대상을 활성화하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

계정 대상을 활성화하는 데 필요한 권한이 있는지 확인하려면 대상 카탈로그를 확인하십시오. 대상에 **[!UICONTROL Activate]** 컨트롤이 있으면 적절한 사용 권한이 있습니다.

## 대상 선택 {#select-destination}

지침에 따라 데이터 세트를 내보낼 수 있는 대상을 선택합니다.

1. **[!UICONTROL 연결 > 대상]**(으)로 이동하여 **[!UICONTROL 카탈로그]** 탭을 선택합니다.

   ![카탈로그 컨트롤이 강조 표시된 대상 카탈로그 탭.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 데이터 세트를 내보내려는 대상에 해당하는 카드에서 **[!UICONTROL 활성화]**&#x200B;를 선택합니다.

>[!TIP]
>
>계정 대상을 내보낼 수 있는 대상은 카드 오른쪽 상단에 아래에 강조 표시된 대상과 유사한 아이콘으로 표시되거나, 데이터 유형 필터를 사용하여 [페이지에 더 위에 표시된 대로](#supported-destinations) 계정 대상을 내보낼 수 있는 대상만 표시할 수 있습니다.

![강조 표시된 프로필 대상을 내보낼 수 있는 Demandbase 대상 페이지입니다.](/help/destinations/assets/ui/activate-account-audiences/demandbase-icon-activate-account-audiences.png)

1. **[!UICONTROL 데이터 형식 계정]**&#x200B;을 선택한 후 데이터 집합을 내보낼 대상 연결을 선택한 후 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

>[!TIP]
> 
>계정 대상을 활성화하기 위해 새 대상을 설정하려면 **[!UICONTROL 새 대상 구성]**&#x200B;을 선택하여 [대상에 연결](/help/destinations/ui/connect-destination.md) 워크플로우를 트리거하고 [데이터 형식으로 계정을 선택](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports)합니다.

![계정 컨트롤이 강조 표시된 대상 활성화 워크플로우입니다.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. 다음 섹션으로 이동하여 [내보낼 계정 대상을 선택](#select-profile-audiences)합니다.

## 계정 대상자 선택 {#select-account-audiences}

계정 대상 이름 왼쪽에 있는 확인란을 사용하여 대상으로 내보낼 대상을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다. 이 보기에는 *계정 대상자*&#x200B;만 표시되며 다른 대상자 유형은 표시되지 않습니다.

![내보낼 계정 대상을 선택할 수 있는 대상 선택 단계를 표시하는 데이터 집합 내보내기 워크플로우입니다.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## 예약 및 다음 단계

계정 대상을 내보내는 활성화 워크플로의 나머지 부분에 대해서는 파일 기반 대상으로 데이터 활성화에 대한 자습서를 참조하십시오. [대상자 내보내기 예약 단계](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)에서 계속합니다. **[!UICONTROL (회사) LinkedIn Matched Audiences]** 대상으로 계정 대상을 활성화하는 경우 스트리밍 대상 활성화에 대한 자습서를 읽어 보십시오. [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)에서 계속합니다.

>[!NOTE]
>
>예약 단계에서 계정 대상을 클라우드 저장소 대상으로 내보낼 때 계정 대상을 활성화하는 워크플로에서는 [전체 파일](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _을(를) 매일 일정_&#x200B;에 내보낼 수만 있습니다. 시간별 내보내기는 지원되지 않습니다. 또한 **[!UICONTROL 대상 평가 후]**&#x200B;만 지원되는 평가 유형입니다.

## 중요한 콜아웃 및 알려진 제한 사항 {#important-callouts-known-limitations}

계정 대상을 활성화하는 기능의 일반 가용성 릴리스에 대한 다음의 중요한 콜아웃 및 알려진 제한을 참조하십시오.

### 계정 대상을 **[!UICONTROL (회사) LinkedIn 일치하는 대상]** 대상으로 활성화할 때 매핑 단계에서 필요한 매핑 쌍 {#required-mappings}

**[!UICONTROL (회사) LinkedIn Matched Audiences]** 대상으로 계정 대상을 활성화할 때 데이터를 성공적으로 내보내려면 다음 두 매핑 쌍이 필요합니다.

![LinkedIn 매핑 필수 필드입니다.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| 소스 필드 | 대상 필드 |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId`(**[!UICONTROL 대상 필드]**&#x200B;를 선택할 때 **[!UICONTROL ID 네임스페이스 선택]** 보기에서 이 필드 선택). <br> ![워크플로에서 강조 표시된 ID 네임스페이스를 선택하여 계정 대상자를 대상으로 활성화합니다.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "대상에 대한 계정 대상을 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"} |

### 데이터 거버넌스 적용 {#data-governance-enforcement}

*고객 및 잠재 고객 대상*&#x200B;에 대한 개인 또는 프로필 수준에서 동의가 시행됩니다. 따라서 계정 대상을 대상으로 활성화할 때 현재 [동의 정책 평가](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)가 지원되지 않습니다. 활성화 워크플로의 검토 단계에서 **[!UICONTROL 적용 가능한 동의 정책 보기]**&#x200B;에 대한 컨트롤이 회색으로 표시됩니다.

![동의 적용 제어가 회색으로 표시된 계정 대상자 활성화 워크플로의 검토 단계입니다.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

[데이터 사용 정책 확인](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 및 [특성 기반 액세스 제어](/help/destinations/home.md#attribute-based-access)와 같은 Real-Time CDP의 다른 데이터 거버넌스 메커니즘이 지원됩니다.
