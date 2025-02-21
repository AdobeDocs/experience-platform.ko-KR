---
title: (회사) LinkedIn 연결
description: 이 대상을 사용하여 Account-Based Marketing(ABM) 사용 사례에 대한 계정 대상자를 활성화할 수 있습니다. 해시된 이메일을 기반으로 대상자 타겟팅, 개인화 및 억제에 대한 LinkedIn 캠페인에 대한 프로필을 활성화합니다.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P 버전" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 68d2cca3-952b-49d0-8ea2-e776a233b752
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 5%

---

# (회사) LinkedIn Match 대상 연결 {#companies-linkedin}

>[!AVAILABILITY]
>
>(회사) LinkedIn 대상에 대한 계정 대상을 활성화하는 기능은 Real-Time Customer Data Platform의 [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) 및 [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) 에디션을 구매하는 회사에서 사용할 수 있습니다.

이 대상을 사용하여 Account-Based Marketing(ABM) 사용 사례에 대해 [계정 대상](/help/segmentation/types/account-audiences.md)을 활성화하십시오. **[!UICONTROL (회사) LinkedIn]** Business-to-Business 대상을 통해 대상 계정의 관련 담당자 및 역할에 알립니다. LinkedIn 설명서를 방문하여 [LinkedIn 플랫폼에서 계정 타깃팅에 대해 자세히 알아보세요](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting).

>[!TIP]
>
>Adobe 개인 수준(또는 비즈니스 대 소비자) 사용 사례의 경우 [LinkedIn 일치하는 대상](/help/destinations/catalog/social/linkedin.md) 대상을 사용하는 것이 좋습니다.

![Experience Platform UI에 LinkedIn 계정 대상이 표시되었습니다.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | X | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-and-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|--------------|-----------|---------------------------|
| 내보내기 유형 | 대상자 내보내기 | 모든 대상 멤버는 이름, 전화번호 등과 같은 키 식별자와 함께 내보내집니다. |
| 빈도 | 스트리밍 | &quot;상시 설정&quot; API 기반 연결. 업데이트는 프로필 변경 후 즉시 다운스트림으로 전송됩니다. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

계정 대상을 LinkedIn으로 내보내려면 아래 사전 요구 사항을 충족해야 합니다.

### LinkedIn 계정 사전 요구 사항 {#LinkedIn-account-prerequisites}

[!UICONTROL (회사) LinkedIn Matched Audience] 대상을 사용하려면 먼저 [!DNL LinkedIn Campaign Manager] 계정에 [!DNL Creative Manager] 권한 수준 이상이 있는지 확인하십시오.

[!DNL LinkedIn Campaign Manager] 사용자 권한을 편집하는 방법에 대해 알아보려면 LinkedIn 설명서에서 [Advertising 계정에 대한 사용자 권한 추가, 편집 및 제거](https://www.linkedin.com/help/lms/answer/5753)를 참조하십시오.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

1. 대상 카탈로그에서 [!DNL (Companies) LinkedIn Matched Audiences] 대상을 찾은 다음 **[!UICONTROL 설정]**&#x200B;을 선택합니다.
2. **[!UICONTROL 대상에 연결]**을 선택합니다.
   ![LinkedIn 인증](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. LinkedIn 자격 증명을 입력하고 **로그인**&#x200B;을 선택합니다.

LinkedIn으로 로그인 프로세스를 완료한 후 다음 단계를 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 내 [!DNL LinkedIn Campaign Manager Account ID]. 이 ID는 [!DNL LinkedIn Campaign Manager] 계정에서 찾을 수 있습니다.

이제 LinkedIn에 계정 대상을 활성화할 준비가 되었습니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![워크플로에서 강조 표시된 ID 네임스페이스를 선택하여 계정 대상자를 대상으로 활성화합니다.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "대상에 대한 계정 대상을 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 계정 대상을 활성화하는 방법에 대한 지침은 [계정 대상 활성화](/help/destinations/ui/activate-account-audiences.md)를 참조하십시오.

## 계정 대상을 **[!UICONTROL (회사) LinkedIn 일치하는 대상]** 대상으로 활성화할 때 매핑 단계에서 필요한 매핑 쌍 {#required-mappings}

**[!UICONTROL (회사) LinkedIn Matched Audiences]** 대상으로 계정 대상을 활성화할 때 데이터를 성공적으로 내보내려면 다음 두 매핑 쌍이 필요합니다.

![LinkedIn 매핑 필수 필드입니다.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| 소스 필드 | 대상 필드 |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId`(**[!UICONTROL 대상 필드]**&#x200B;를 선택할 때 **[!UICONTROL ID 네임스페이스 선택]** 보기에서 이 필드 선택). <br> ![워크플로에서 강조 표시된 ID 네임스페이스를 선택하여 계정 대상자를 대상으로 활성화합니다.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "대상에 대한 계정 대상을 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## 내보낸 데이터 {#exported-data}

활성화가 성공하면 [!DNL LinkedIn] 사용자 지정 대상자가 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)에서 프로그래밍 방식으로 만들어집니다. 사용자가 활성화된 대상에 대해 자격이 부여되거나 자격을 상실함에 따라 대상 멤버십이 조정됩니다.
