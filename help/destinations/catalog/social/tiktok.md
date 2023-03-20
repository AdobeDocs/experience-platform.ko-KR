---
title: TikTok 연결
description: 광고 캠페인으로 타겟팅할 데이터를 사용하여 TikTok에서 사용자 지정 대상을 만듭니다. 이러한 대상은 웹 사이트를 방문하거나 콘텐츠와 상호 작용한 사람일 수 있습니다. TikTok Ads Manager와의 실시간 통합을 사용하여 Adobe Experience Platform에서 TikTok으로 원하는 세그먼트를 빠르고 안전하게 푸시할 수 있습니다.
last-substantial-update: 2023-03-20T00:00:00Z
source-git-commit: 7bfcd0132380f0c847742ff05c1f334542adfba2
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---


# TikTok 연결

## 개요 {#overview}

광고 캠페인으로 타겟팅할 데이터를 사용하여 TikTok에서 사용자 지정 대상을 만듭니다. 이러한 대상은 웹 사이트를 방문하거나 콘텐츠와 상호 작용한 사람일 수 있습니다. TikTok Ads Manager와의 실시간 통합을 사용하여 Adobe Experience Platform에서 TikTok으로 원하는 세그먼트를 빠르고 안전하게 푸시할 수 있습니다. 방문 [TikTok 비즈니스 도움말 센터](https://ads.tiktok.com/help/article/audiences?lang=en) 추가 정보.

>[!IMPORTANT]
>
>이 설명서 페이지는 TikTok 팀이 만들었습니다. 문의 사항이나 업데이트 요청에 대해서는 [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## 사용 사례 {#use-cases}

TikTok 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객을 위한 샘플 사용 사례입니다.

### 사용 사례 {#use-case-1}

스포츠 의류 브랜드는 기존 고객에게 소셜 미디어 계정을 통해 연결되기를 원한다. 의류 브랜드는 자체 CRM의 이메일 주소를 Adobe Experience Platform에 수집하고, 자체 오프라인 데이터에서 세그먼트를 작성하고, 이러한 세그먼트를 TikTok으로 보내 고객의 소셜 미디어 피드에 광고를 표시할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

데이터를 [!DNL TikTok Ads Manager] 계정에서에 대한 광고 계정에 액세스하려면 Adobe Experience Platform에 권한을 제공해야 합니다. `Audience Management`. 이 권한은 Experience Platform에 광고주 ID를 입력하고 리디렉션을 수행하여 권한을 부여하여 제공할 수 있습니다. 자세한 지침은 [TikTok API 설명서](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## 지원되는 ID {#supported-identities}

TikTok은 아래 표에 설명된 ID 활성화를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| 전화번호 | SHA256 알고리즘으로 해시된 전화 번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원하며 E.164 형식이어야 합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| 이메일 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | TikTok 대상에 사용되는 식별자(이름, 전화 번호 또는 기타 식별자)로 세그먼트(대상)의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상에 인증 {#authenticate}

대상을 인증하려면 다음에 로그인하도록 리디렉션됩니다 [!DNL TikTok Ads Manager] 고객을 대신하여 관리할 Adobe을 계정 및 승인합니다.

![TikTok 권한 선택](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "권한 선택을 위한 TikTok UI 이미지")

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 연결 세부 정보](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Platform UI의 이미지. 채울 대상 연결 세부 사항을 표시합니다")

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL TikTok 광고 관리자 ID]**: 사용자 [!DNL TikTok Ads Manager ID]. 다음 위치에서 찾을 수 있습니다 [!DNL TikTok Ads manager] 계정이 필요합니다.

![TikTok 광고 관리자 ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "TikTok Ads Manager ID를 가져오는 방법을 보여주는 TikTok Ads Manager UI의 이미지")

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### ID 매핑 {#map}

다음은 TikTok Ads Manager로 세그먼트를 내보낼 때 올바른 ID 매핑의 예입니다.

소스 필드 선택:

* 식별자를 선택합니다(예:` Email_LC_SHA256`) 를 Adobe Experience Platform 및 [!DNL TikTok Ads Manager].

대상 필드 선택:

* 이메일 네임스페이스를 타겟 ID로 선택합니다.

![ID 매핑](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Platform UI의 이미지, ID 매핑")

## 내보낸 데이터 {#exported-data}

다음 문서를 확인하십시오. [!DNL TikTok Ads Manager] 계정(아래) **자산 > 대상**) Experience Platform 세그먼트를 성공적으로 내보냈는지 확인합니다. 대상이 대상 유형으로 채워집니다. `Partner Audience`.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 읽기 [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

자세한 내용은 [TikTok 도움말 센터 페이지](https://ads.tiktok.com/help/article/audiences?lang=en) 추가 정보.
