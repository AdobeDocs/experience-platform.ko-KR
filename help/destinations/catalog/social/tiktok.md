---
title: TikTok 연결
description: 광고 캠페인으로 타깃팅할 데이터를 사용하여 TikTok에서 사용자 지정 대상을 작성합니다. 이러한 대상은 웹 사이트를 방문하거나 콘텐츠와 상호 작용한 사람일 수 있습니다. Adobe과 TikTok Ads Manager의 실시간 통합을 사용하여 원하는 대상을 Adobe Experience Platform에서 TikTok으로 빠르고 안전하게 푸시할 수 있습니다.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 3%

---

# TikTok 연결

## 개요 {#overview}

광고 캠페인으로 타깃팅할 데이터를 사용하여 TikTok에서 사용자 지정 대상을 작성합니다. 이러한 대상은 웹 사이트를 방문하거나 콘텐츠와 상호 작용한 사람일 수 있습니다. Adobe과 TikTok Ads Manager의 실시간 통합을 사용하여 원하는 대상을 Adobe Experience Platform에서 TikTok으로 빠르고 안전하게 푸시할 수 있습니다. 자세한 내용은 [TikTok의 비즈니스 도움말 센터](https://ads.tiktok.com/help/article/audiences)를 참조하세요.

>[!IMPORTANT]
>
>이 대상 커넥터 및 설명서 페이지는 TikTok 팀에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/)로 직접 연락하십시오.

## 사용 사례 {#use-cases}

TikTok 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객을 위한 샘플 사용 사례를 소개합니다.

### 활용 사례 {#use-case-1}

한 스포츠 의류 브랜드는 자신의 소셜 미디어 계정을 통해 기존 고객에게 도달하기를 원합니다. 의류 브랜드는 자체 CRM에서 Adobe Experience Platform으로 이메일 주소를 수집하고, 자체 오프라인 데이터에서 대상을 만들고, 이러한 대상을 TikTok으로 보내 고객의 소셜 미디어 피드에 광고를 표시할 수 있습니다.

## 전제 조건 {#prerequisites}

대상자를 보낼 TikTok Ads Manager 계정에 대해 [!DNL Admin] 또는 [!DNL Operator] 액세스 권한이 있어야 합니다. 자세한 지침은 [TikTok 도움말 센터](https://ads.tiktok.com/help/article/add-users-tiktok-business-center)에서 확인할 수 있습니다.

TikTok Ads Manager 계정으로 데이터를 보내기 전에 `Audience Management`의 광고 계정에 액세스할 수 있는 Adobe Experience Platform 권한을 부여해야 합니다. 이 권한은 [Experience Platform UI에서 광고 관리자 ID를 입력](#authenticate)하고 TikTok 광고 관리자 계정으로 리디렉션된 후 권한을 부여하여 제공할 수 있습니다.

## 지원되는 ID {#supported-identities}

TikTok은 아래 표에 설명된 id 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| 전화번호 | SHA256 알고리즘으로 해시된 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원되며 E.164 형식이어야 합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 하십시오. |
| 이메일 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 하십시오. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |
| [!DNL Federated Audience Composition] | ✓ | [Federated Audience Composition](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/start/audiences)을(를) 통해 Experience Platform으로 가져온 대상입니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | TikTok 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 [!DNL TikTok Ads Manager] 계정에 로그인하도록 리디렉션되고 Adobe에서 사용자를 대신하여 대상자를 관리하도록 승인됩니다.

![TikTok 권한 선택](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "권한 선택을 위한 TikTok UI 이미지")

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 연결 세부 정보](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Experience Platform UI의 이미지로, 채울 대상 연결 세부 정보를 표시합니다")

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL TikTok 광고 관리자 ID]**: 내 [!DNL TikTok Ads Manager ID]. [!DNL TikTok Ads manager] 계정에서 찾을 수 있습니다.

![TikTok 광고 관리자 ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "TikTok 광고 관리자 ID를 가져오는 방법을 보여 주는 TikTok 광고 관리자 UI의 이미지")

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### ID 매핑 {#map}

다음은 TikTok Ads Manager로 대상을 내보낼 때 올바른 ID 매핑의 예입니다.

소스 필드 선택:

* Adobe Experience Platform 및 [!DNL TikTok Ads Manager]에서 프로필을 고유하게 식별하는 원본 ID로 식별자(예: ` Email_LC_SHA256`)를 선택하십시오.

대상 필드 선택:

* 이메일 네임스페이스를 대상 ID로 선택합니다.

![ID 매핑](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Experience Platform UI의 이미지, ID 매핑")

## 내보낸 데이터 {#exported-data}

[!DNL TikTok Ads Manager] 계정(**Assets > 대상** 아래)을 확인하여 Experience Platform 대상을 성공적으로 내보냈는지 확인하십시오. 대상은 대상 유형으로 채워집니다. `Partner Audience`.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 추가 리소스 {#additional-resources}

자세한 내용은 [TikTok 도움말 센터 페이지](https://ads.tiktok.com/help/article/audiences)를 참조하십시오.
