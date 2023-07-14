---
title: TikTok 연결
description: 광고 캠페인의 타겟팅용 데이터로 TikTok에서 맞춤형 대상자를 구축합니다. 이러한 대상은 웹 사이트를 방문하거나 콘텐츠와 상호 작용한 사람일 수 있습니다. Adobe과 TikTok Ads Manager의 실시간 통합을 사용하여 원하는 대상을 Adobe Experience Platform에서 TikTok으로 빠르고 안전하게 푸시할 수 있습니다.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 5%

---

# TikTok 연결

## 개요 {#overview}

광고 캠페인의 타겟팅용 데이터로 TikTok에서 맞춤형 대상자를 구축합니다. 이러한 대상은 웹 사이트를 방문하거나 콘텐츠와 상호 작용한 사람일 수 있습니다. Adobe과 TikTok Ads Manager의 실시간 통합을 사용하여 원하는 대상을 Adobe Experience Platform에서 TikTok으로 빠르고 안전하게 푸시할 수 있습니다. 방문 [TikTok 비즈니스 도움말 센터](https://ads.tiktok.com/help/article/audiences?lang=en) 추가 정보.

>[!IMPORTANT]
>
>이 설명서 페이지는 TikTok 팀에서 만들었습니다. 문의 사항이나 업데이트 요청은 다음 주소로 직접 문의하십시오. [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## 사용 사례 {#use-cases}

TikTok 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객을 위한 샘플 사용 사례를 소개합니다.

### 사용 사례 {#use-case-1}

한 스포츠 의류 브랜드는 자신의 소셜 미디어 계정을 통해 기존 고객에게 도달하기를 원합니다. 의류 브랜드는 자체 CRM에서 Adobe Experience Platform으로 이메일 주소를 수집하고, 자체 오프라인 데이터에서 대상을 만들고, 이러한 대상을 TikTok으로 보내 고객의 소셜 미디어 피드에 광고를 표시할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

에 데이터를 보내기 전 [!DNL TikTok Ads Manager] 계정, 다음에 대한 광고 계정에 액세스하려면 Adobe Experience Platform에 권한을 부여해야 합니다. `Audience Management`. 이 권한은 Experience Platform에 광고주 ID를 입력하고 리디렉션에 따라 권한을 부여하여 제공할 수 있습니다. 자세한 지침은 [TikTok API 설명서](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## 지원되는 ID {#supported-identities}

TikTok은 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| TARGET ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| 전화번호 | SHA256 알고리즘으로 해시된 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원되며 E.164 형식이어야 합니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| 이메일 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | TikTok 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상에 인증 {#authenticate}

대상에 인증하려면 다음으로 로그인하도록 리디렉션됩니다. [!DNL TikTok Ads Manager] 귀하를 대신하여 대상을 관리할 Adobe을 계정 및 승인합니다.

![TikTok 권한 선택](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "권한 선택을 위한 TikTok UI 이미지")

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 연결 세부 정보](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "채울 대상 연결 세부 사항을 표시하는 Platform UI의 이미지")

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL TikTok Ads Manager ID]**: 사용자 [!DNL TikTok Ads Manager ID]. 다음에서 찾을 수 있습니다. [!DNL TikTok Ads manager] 계정입니다.

![TikTok Ads Manager ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "TikTok Ads Manager ID를 가져오는 방법을 보여 주는 TikTok Ads Manager UI 이미지")

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [스트리밍 대상자 내보내기 대상으로 프로필 및 대상자 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### ID 매핑 {#map}

다음은 TikTok Ads Manager로 대상을 내보낼 때 올바른 ID 매핑의 예입니다.

소스 필드 선택:

* 식별자 선택(예:` Email_LC_SHA256`)를 Adobe Experience Platform에서 프로필을 고유하게 식별하고 [!DNL TikTok Ads Manager].

대상 필드 선택:

* 이메일 네임스페이스를 대상 ID로 선택합니다.

![ID 매핑](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Platform UI 이미지, ID 매핑")

## 내보낸 데이터 {#exported-data}

다음을 확인: [!DNL TikTok Ads Manager] 계정(아래) **에셋 > 대상**)을 클릭하여 Experience Platform 대상을 성공적으로 내보냈는지 확인합니다. 대상자는 대상자 유형으로 채워집니다. `Partner Audience`.

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

다음을 참조하십시오. [TikTok 도움말 센터 페이지](https://ads.tiktok.com/help/article/audiences?lang=en) 추가 정보.
