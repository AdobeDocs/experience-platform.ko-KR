---
title: Pinterest 고객 목록 연결
description: 고객 목록, 사이트를 방문한 사람 또는 Pinterest에서 콘텐츠와 이미 상호 작용한 사람에서 대상을 만듭니다.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 8a48ce4185f8044b8563d0435dcec17030b90830
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 4%

---

# [!DNL Pinterest Customer List] 연결

## 개요 {#overview}

고객 목록, 사이트를 방문한 사람 또는 Pinterest에서 콘텐츠와 이미 상호 작용한 사람에서 대상을 만듭니다.

>[!IMPORTANT]
>
>이 대상은 Pinterest 팀이 빌드했습니다. 문의 사항이나 업데이트 요청은 https://help.pinterest.com/en/contact으로 직접 문의하시기 바랍니다.

## 전제 조건 {#prerequisites}

* 사용자는 대상을 추가하려는 광고주 계정에 액세스할 수 있는 Pinterest 계정을 사용하여 인증해야 합니다. 광고주 계정 공유에 대한 자세한 내용은 [여기](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts)에서 확인할 수 있습니다. 특히, 사용자는 &quot;대상&quot; 액세스 수준이 필요합니다.
* 고객 목록 ID 형식에 대한 자세한 내용은 [여기](https://help.pinterest.com/en/business/article/audience-targeting)를 참조하십시오.

## 지원되는 ID {#supported-identities}

[!DNL Pinterest Customer List] 대상은 아래 표에 설명된 ID 활성화를 지원합니다. [ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started)에 대해 자세히 알아보세요.

대상 활성화 워크플로의 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)에서 원하는 ID를 대상 필드 *pinterest_audience*&#x200B;에 매핑합니다. ID는 Pinterest으로 데이터를 수집할 때 구분되고 해결됩니다.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | *GAID* 소스 ID 네임스페이스를 대상 ID 필드 *pinterest_audience*&#x200B;에 매핑합니다. ID는 Pinterest으로 데이터를 수집할 때 구분되고 해결됩니다. |
| IDFA | [!DNL Apple ID for Advertisers] | *IDFA* 소스 ID 네임스페이스를 대상 ID 필드 *pinterest_audience*&#x200B;에 매핑합니다. ID는 Pinterest으로 데이터를 수집할 때 구분되고 해결됩니다. |
| EMAIL | 이메일 주소(텍스트 지우기 또는 SHA256 알고리즘으로 해시됨) | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. <br> *Email* 또는 *Email_LC_SHA256* 소스 ID 네임스페이스를 대상 ID 필드 *pinterest_audience*&#x200B;에 매핑합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | pinterest 고객 목록 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 사용 사례 {#use-cases}

[!DNL Pinterest Customer List] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

### 사용 사례 #1

고객 목록, 사이트를 방문한 사람 또는 Pinterest에서 콘텐츠와 이미 상호 작용한 사람에서 대상을 만듭니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개변수 {#parameters}

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 광고 계정 ID]**: Pinterest 광고주 ID.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko)를 참조하십시오.

## 추가 리소스 {#additional-resources}

자세한 내용은 [Pinterest 도움말 센터 페이지](https://help.pinterest.com/en/business/article/audience-targeting)를 참조하십시오.

+++ 변경 로그 보기


| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2023년 11월 | 기능 및 설명서 업데이트 | 이제 Real-Time CDP의 Pinterest 대상은 v5 Advertiser API를 사용합니다. |

{style="table-layout:auto"}


+++
