---
title: Twitter 사용자 지정 대상 연결
description: Twitter에서 기존 팔로우어 및 고객을 타겟팅하고 Adobe Experience Platform 내에 구축된 대상을 활성화하여 관련 리마케팅 캠페인을 만듭니다
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: ef1b0b704d1299282995068a0de330d52884bb95
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 6%

---

# [!DNL Twitter Custom Audiences] 연결

## 개요 {#overview}

Twitter에서 기존 팔로우어 및 고객을 타겟팅하고 Adobe Experience Platform 내에 구축된 대상을 활성화하여 관련 리마케팅 캠페인을 만듭니다.

## 전제 조건 {#prerequisites}

[!DNL Twitter Custom Audiences] 대상을 구성하기 전에 충족해야 하는 다음 Twitter 필수 구성 요소를 검토하십시오.

1. [!DNL Twitter Ads] 계정은 광고를 할 수 있어야 합니다. 새 [!DNL Twitter Ads] 계정은 만들어진 후 처음 2주 동안은 광고할 수 없습니다.
2. [!DNL Twitter Audience Manager]에서 액세스 권한을 부여한 Twitter 사용자 계정에 *[!DNL Partner Audience Manager]* 권한이 활성화되어 있어야 합니다.

## 지원되는 ID {#supported-identities}

[!DNL Twitter Custom Audiences]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google GAID(Advertising ID) 및 IDFA(Apple ID for Advertisers)는 Adobe Experience Platform에서 지원됩니다. 대상 활성화 워크플로의 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)에서 원본 스키마의 이러한 네임스페이스 및/또는 특성을 적절하게 매핑하십시오. |
| 이메일 | 사용자의 이메일 주소 | 일반 텍스트 이메일 주소와 SHA256 해시된 이메일 주소를 이 필드에 매핑하십시오. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다. Adobe Experience Platform에 업로드하기 전에 고객 이메일 주소를 해시하는 경우 이러한 ID는 소금 없이 SHA256을 사용하여 해시해야 합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 예 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 기타 모든 대상 원본 | 아니요 | 이 범주에는 [!DNL Segmentation Service]을(를) 통해 생성된 대상 외부의 모든 대상 출처가 포함됩니다. [다양한 대상 원본](/help/segmentation/ui/audience-portal.md#customize)에 대해 읽어 보십시오. 예를 들면 다음과 같습니다. <ul><li> CSV 파일에서 Experience Platform으로 사용자 지정 업로드 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience),</li><li> 유사 대상, </li><li> 페더레이션 대상, </li><li> Adobe Journey Optimizer과 같은 다른 Experience Platform 앱에서 생성된 대상자 </li><li> 등. </li></ul> |

{style="table-layout:auto"}



대상 데이터 유형별 지원되는 대상:

| 대상 데이터 유형 | 지원됨 | 설명 | 사용 사례 |
|--------------------|-----------|-------------|-----------|
| [사람 대상](/help/segmentation/types/people-audiences.md) | 예 | 고객 프로필을 기반으로 마케팅 캠페인을 위해 특정 사용자 그룹을 타깃팅할 수 있습니다. | 빈번한 구매자, 장바구니 포기 |
| [계정 대상자](/help/segmentation/types/account-audiences.md) | 아니요 | 계정 기반 마케팅 전략을 위해 특정 조직 내의 개인을 타깃팅합니다. | B2B 마케팅 |
| [잠재 고객](/help/segmentation/types/prospect-audiences.md) | 아니요 | 아직 고객이 아니지만 타겟 대상자와 특성을 공유하는 개인을 타겟팅합니다. | 타사 데이터를 이용한 잠재 고객 확보 |
| [데이터 집합 내보내기](/help/catalog/datasets/overview.md) | 아니요 | Adobe Experience Platform 데이터 레이크에 저장된 구조화된 데이터의 컬렉션입니다. | 보고, 데이터 과학 워크플로 |

{style="table-layout:auto"}


## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Audience export]** | Twitter 사용자 지정 대상 대상에서 사용된 식별자를 사용하여 대상의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 사용 사례 {#use-cases}

[!DNL Twitter Custom Audiences] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

### 사용 사례 #1

Twitter에서 기존 팔로워와 고객을 타겟팅하고 Twitter에서 [!DNL List Custom Audiences]&#x200B;(으)로 Adobe Experience Platform 내에 빌드된 대상을 활성화하여 관련 리마케팅 캠페인을 만드십시오.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

1. 대상 카탈로그에서 [!DNL Twitter Custom Audiences] 대상을 찾은 다음 **[!UICONTROL Set Up]**&#x200B;을(를) 선택하십시오.
2. **[!UICONTROL Connect to destination]**를 선택합니다.
   ![LinkedIn 인증](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Twitter 자격 증명을 입력하고 **로그인**&#x200B;을 선택합니다.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="계정 ID"
>abstract="Twitter Ads 계정 ID. 계정 ID는 Twitter Ads 설정에서 찾을 수 있습니다."

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Account ID]**: [!DNL Twitter Ads] 계정 ID입니다. [!DNL Twitter Ads] 설정에서 찾을 수 있습니다.

>[!IMPORTANT]
>
>특수 문자(+ &amp; , % : ; @ / = ? $ \n) 대상, 설명 및 대상 매핑 이름. Experience Platform 대상 이름에 이러한 문자가 포함되어 있는 경우 대상을 Twitter 대상에 매핑하기 전에 해당 문자를 제거하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 매핑 고려 사항 {#mapping-considerations}

Twitter에 대상을 매핑할 때 사람이 읽을 수 있는 대상 매핑 이름을 제공합니다. Experience Platform 세그먼트에 사용한 것과 동일한 이름을 사용하는 것이 좋습니다.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko)를 참조하십시오.

## 추가 리소스 {#additional-resources}

Twitter의 [!DNL List Custom Audiences]에 대한 자세한 내용은 [Twitter 설명서](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html)를 참조하십시오.
