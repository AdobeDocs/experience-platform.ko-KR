---
title: 사용자 지정 대상 연결 twitter
description: Adobe Experience Platform 내에 구축된 대상을 활성화하여 Twitter에서 기존 팔로우어 및 고객을 타겟팅하고 관련 리마케팅 캠페인을 생성합니다
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 5%

---

# [!DNL Twitter Custom Audiences] 연결

## 개요 {#overview}

Adobe Experience Platform 내에 구축된 대상을 활성화하여 Twitter에서 기존 팔로우어 및 고객을 타겟팅하고 관련 리마케팅 캠페인을 생성합니다.

## 전제 조건 {#prerequisites}

을(를) 구성하기 전에 [!DNL Twitter Custom Audiences] 대상, 충족해야 하는 다음 Twitter 사전 요구 사항을 검토하십시오.

1. 사용자 [!DNL Twitter Ads] 계정은 광고를 할 자격이 있어야 합니다. 신규 [!DNL Twitter Ads] 계정은 생성 후 처음 2주 동안은 광고할 수 없습니다.
2. 에 대한 액세스 권한을 부여한 Twitter 사용자 계정 [!DNL Twitter Audience Manager] 은(는) 을(를) 포함해야 합니다. *[!DNL Partner Audience Manager]* 사용 권한이 활성화되었습니다.

## 지원되는 ID {#supported-identities}

[!DNL Twitter Custom Audiences] 는 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google GAID(Advertising ID) 및 IDFA(Apple ID for Advertisers)는 Adobe Experience Platform에서 지원됩니다. 소스 스키마에서 이러한 네임스페이스 및/또는 속성을 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 대상 활성화 워크플로의 일부입니다. |
| 이메일 | 사용자의 이메일 주소 | 일반 텍스트 이메일 주소와 SHA256 해시된 이메일 주소를 이 필드에 매핑하십시오. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. Adobe Experience Platform에 업로드하기 전에 고객 이메일 주소를 해시하는 경우 이러한 ID는 소금 없이 SHA256을 사용하여 해시해야 합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ 덧신 | 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | twitter 사용자 지정 대상 대상에 사용된 식별자로 대상의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 사용 사례 {#use-cases}

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL Twitter Custom Audiences] 대상: 다음은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 사용 사례 #1

Adobe Experience Platform 내에 구축된 대상을 활성화하여 Twitter에서 기존 팔로우어 및 고객을 타겟팅하고 관련 리마케팅 캠페인을 생성합니다. [!DNL List Custom Audiences] twitter.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

1. 다음 찾기 [!DNL Twitter Custom Audiences] 대상 카탈로그의 대상 및 선택 **[!UICONTROL 설정]**.
2. 선택 **[!UICONTROL 대상에 연결]**.
   ![linkedIn 인증](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. twitter 자격 증명을 입력하고 선택 **로그인**.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="계정 ID"
>abstract="Twitter Ads 계정 ID. 계정 ID는 Twitter Ads 설정에서 찾을 수 있습니다."

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자 [!DNL Twitter Ads] 계정 ID. 이 은(는) 다음 위치에서 찾을 수 있습니다. [!DNL Twitter Ads] 설정.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

읽기 [스트리밍 대상자 내보내기 대상으로 프로필 및 대상자 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko).

## 추가 리소스 {#additional-resources}

대상을 Twitter에 매핑할 때 다음 대상 이름 지정 요구 사항을 충족해야 합니다.

1. 사람이 읽을 수 있는 대상 매핑 이름을 제공합니다. Experience Platform 세그먼트에 사용한 것과 동일한 이름을 사용하는 것이 좋습니다.
2. 특수 문자(+ &amp; , % : ; @ / = ? $) 대상 및 대상 매핑 이름. Experience Platform 대상 이름에 이러한 문자가 포함되어 있는 경우 대상을 Twitter 대상에 매핑하기 전에 해당 문자를 제거하십시오.

다음에 대한 추가 정보: [!DNL List Custom Audiences] twitter에서 찾을 수 있음 [Twitter 설명서](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
