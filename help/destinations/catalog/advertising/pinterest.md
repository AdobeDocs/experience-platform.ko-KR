---
title: Pinterest 고객 목록 연결
description: 고객 목록, 사이트를 방문한 사람 또는 Pinterest에서 콘텐츠와 이미 상호 작용한 사람에서 대상을 만듭니다.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 4%

---

# [!DNL Pinterest Customer List] 연결

## 개요 {#overview}

고객 목록, 사이트를 방문한 사람 또는 Pinterest에서 콘텐츠와 이미 상호 작용한 사람에서 대상을 만듭니다.

>[!IMPORTANT]
>
>이 대상은 Pinterest 팀이 빌드했습니다. 문의 사항이나 업데이트 요청은 https://help.pinterest.com/en/contact으로 직접 문의하십시오.

## 전제 조건 {#prerequisites}

* 사용자는 대상을 추가하려는 광고주 계정에 액세스할 수 있는 Pinterest 계정을 사용하여 인증해야 합니다. 광고주 계정 공유에 대한 자세한 내용은 [여기](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts)에서 확인할 수 있습니다. 특히, 사용자는 &quot;대상&quot; 액세스 수준이 필요합니다.
* 고객 목록 ID 형식에 대한 자세한 내용은 [여기](https://help.pinterest.com/en/business/article/audience-targeting)를 참조하십시오.

## 지원되는 ID {#supported-identities}

[!DNL Pinterest Customer List] 대상은 아래 표에 설명된 ID 활성화를 지원합니다. [ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=ko#getting-started)에 대해 자세히 알아보세요.

대상 활성화 워크플로의 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)에서 원하는 ID를 대상 필드 *pinterest_audience*&#x200B;에 매핑합니다. ID는 Pinterest으로 데이터를 수집할 때 구분되고 해결됩니다.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | *GAID* 소스 ID 네임스페이스를 대상 ID 필드 *pinterest_audience*&#x200B;에 매핑합니다. |
| IDFA | [!DNL Apple ID for Advertisers] | *IDFA* 원본 ID 네임스페이스를 대상 ID 필드 *pinterest_audience*&#x200B;에 매핑합니다. |
| EMAIL | 이메일 주소(텍스트 지우기 또는 SHA256 알고리즘으로 해시됨) | [!DNL Adobe Experience Platform]은(는) 일반 텍스트와 SHA256 해시된 전자 메일 주소를 모두 지원합니다. <br> *Email* 또는 *Email_LC_SHA256* 소스 ID 네임스페이스를 대상 ID 필드 *pinterest_audience*&#x200B;에 매핑합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 예 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 기타 모든 대상 원본 | 예 | 이 범주에는 [!DNL Segmentation Service]을(를) 통해 생성된 대상 외부의 모든 대상 출처가 포함됩니다. [다양한 대상 원본](/help/segmentation/ui/audience-portal.md#customize)에 대해 읽어 보십시오. 예를 들면 다음과 같습니다. <ul><li> CSV 파일에서 Experience Platform으로 사용자 지정 업로드 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience),</li><li> 유사 대상, </li><li> 페더레이션 대상, </li><li> Adobe Journey Optimizer과 같은 다른 Experience Platform 앱에서 생성된 대상자 </li><li> 등. </li></ul> |

{style="table-layout:auto"}

대상 데이터 유형별 지원되는 대상:

| 대상 데이터 유형 | 지원됨 | 설명 | 사용 사례 |
|--------------------|-----------|-------------|-----------|
| [사람 대상](/help/segmentation/types/people-audiences.md) | 예 | 고객 프로필을 기반으로 마케팅 캠페인을 위해 특정 사용자 그룹을 타깃팅할 수 있습니다. | 빈번한 구매자, 장바구니 포기 |
| [계정 대상자](/help/segmentation/types/account-audiences.md) | 아니요 | 계정 기반 마케팅 전략을 위해 특정 조직 내의 개인을 타깃팅합니다. | B2B 마케팅 |
| [잠재 고객](/help/segmentation/types/prospect-audiences.md) | 아니요 | 아직 고객이 아니지만 타겟 대상자와 특성을 공유하는 개인을 타겟팅합니다. | 타사 데이터를 이용한 잠재 고객 확보 |
| [데이터 집합 내보내기](/help/catalog/datasets/overview.md) | 아니요 | [!DNL Adobe Experience Platform] 데이터 레이크에 저장된 구조화된 데이터의 컬렉션입니다. | 보고, 데이터 과학 워크플로 |

{style="table-layout:auto"}


## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Audience export]** | Pinterest 고객 목록 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 사용 사례 {#use-cases}

[!DNL Pinterest Customer List] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL Adobe Experience Platform] 고객이 이 대상을 사용하여 해결할 수 있는 사용 사례의 예제를 소개합니다.

### 사용 사례 #1 {#use-case-1}

고객 목록, 사이트를 방문한 사람 또는 Pinterest에서 콘텐츠와 이미 상호 작용한 사람에서 대상을 만듭니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개변수 {#parameters}

이 대상을 [설정](../../ui/connect-destination.md)할 때 다음 정보를 제공해야 합니다.

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Ad Account ID]**: Pinterest 광고주 ID입니다.

### 인증 자격 증명 새로 고침 {#refresh-authentication-credentials}

Pinterest 토큰은 30일마다 만료됩니다. **[!UICONTROL Account expiration date]** 또는 **[[!UICONTROL Accounts]](../../ui/destinations-workspace.md#accounts)** 탭의 **[[!UICONTROL Browse]](../../ui/destinations-workspace.md#browse)** 열에서 토큰 만료 날짜를 모니터링할 수 있습니다.

토큰이 만료되면 대상으로의 데이터 내보내기가 더 이상 작동하지 않습니다. 이러한 상황을 방지하려면 다음 단계를 수행하여 다시 인증하십시오.

1. **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**(으)로 이동
2. (선택 사항) 페이지에서 사용할 수 있는 필터를 사용하여 Pinterest 계정만 표시합니다.
   ![Pinterest 계정만 표시하도록 필터링](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-filters.png)
3. 새로 고침할 계정을 선택하고 줄임표를 선택한 다음 **[!UICONTROL Edit details]**을(를) 선택하십시오.
   ![세부 정보 편집 컨트롤 선택](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-edit-details.png)
4. 모달 창에서 **[!UICONTROL Reconnect OAuth]**을(를) 선택하고 Pinterest 자격 증명으로 다시 인증합니다.
   ![다시 연결 OAuth 옵션이 있는 모달 창](/help/destinations/assets/catalog/advertising/pinterest-customer-list/reconnect-oauth-control.png)

>[!SUCCESS]
>
>인증 자격 증명이 새로 고쳐지고 만료 시간이 30일로 재설정됩니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
>
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko)를 참조하십시오.

## 추가 리소스 {#additional-resources}

자세한 내용은 [Pinterest 도움말 센터 페이지](https://help.pinterest.com/en/business/article/audience-targeting)를 참조하세요.

+++ 변경 로그 보기


| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2023년 11월 | 기능 및 설명서 업데이트 | 이제 [!DNL Real-Time CDP]의 Pinterest 대상에서 v5 Advertiser API를 사용합니다. |

{style="table-layout:auto"}


+++
