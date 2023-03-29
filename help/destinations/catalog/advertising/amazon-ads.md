---
title: Amazon 광고
description: Amazon 광고는 등록된 판매자, 공급업체, 도서 공급업체, KDP(Kindle Direct Publishing) 작성자, 앱 개발자 및/또는 에이전시에 대한 광고 목표를 달성하는 데 도움이 되는 다양한 옵션을 제공합니다. Adobe Experience Platform과 Amazon Ads 통합은 Amazon DSP(ADSP)을 비롯한 Amazon 광고 제품에 대한 턴키 통합을 제공합니다. Adobe Experience Platform에서 Amazon 광고 대상을 사용하여 Amazon DSP에서 타깃팅 및 활성화를 위한 광고주 대상을 정의할 수 있습니다.
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 732e6d3d53d983f3390941f4694d2c542d882004
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---


# (베타) Amazon 광고 연결 {#amazon-ads}

## 개요 {#overview}

Amazon 광고는 등록된 판매자, 공급업체, 도서 공급업체, KDP(Kindle Direct Publishing) 작성자, 앱 개발자 및/또는 에이전시에 대한 광고 목표를 달성하는 데 도움이 되는 다양한 옵션을 제공합니다.

Adobe Experience Platform과 Amazon Ads 통합은 Amazon DSP(ADSP)을 비롯한 Amazon 광고 제품에 대한 턴키 통합을 제공합니다. Adobe Experience Platform에서 Amazon 광고 대상을 사용하여 Amazon DSP에서 타깃팅 및 활성화를 위한 광고주 대상을 정의할 수 있습니다.

이 연결은 다음 Amazon Marketplace에서 대상 만들기를 지원합니다. `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>이 설명서 페이지는 *Amazon 광고* 팀 현재 베타 제품이며 변경될 수 있습니다. 문의 사항이나 업데이트 요청에 대해서는 *`amc-support@amazon.com`.*

## 사용 사례 {#use-cases}

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 *Amazon 광고* 대상, Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례는 다음과 같습니다.

### 활성화 및 타겟팅 {#activation-and-targeting}

Amazon DSP과 통합하면 Amazon Ads 광고주가 Adobe Experience Platform에서 Amazon의 DSP으로 광고주 CDP 세그먼트를 전달하여 광고 타깃팅을 위한 광고주 대상을 만들 수 있습니다. Amazon DSP 내에서 타겟팅뿐만 아니라 부정적 타겟팅(제외)을 위해 대상을 선택할 수 있습니다. 또한 Amazon Marketing Cloud을 통해 생성된 신호를 사용하여 광고주는 대상 변경 사항을 Amazon DSP과 동기화하는 광고주 대상을 최적화할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

Adobe Experience Platform과 Amazon Ads 연결을 사용하려면 사용자가 먼저 Amazon DSP Advertiser 계정에 액세스할 수 있어야 합니다.  이러한 인스턴스를 제공하려면 Amazon 광고 웹 사이트의 다음 페이지를 방문하십시오.

* [Amazon DSP 시작](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## 지원되는 ID {#supported-identities}

다음 *Amazon 광고* 연결은 아래 표에 설명된 id의 활성화를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md). Amazon 광고에서 지원하는 ID에 대한 자세한 내용은 [Amazon DSP 지원 센터](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| phone_sha256 | SHA256 알고리즘으로 해시된 전화 번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 에서 사용되는 식별자(이름, 전화 번호 또는 기타 식별자)로 세그먼트의 모든 멤버(대상)를 내보내고 있습니다 *Amazon 광고* 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상에 인증 {#authenticate}

대상을 인증하려면 필요한 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**.

연결할 광고주 계정을 먼저 선택하는 Amazon 광고 연결 인터페이스로 이동합니다.  연결되면 선택한 광고주 계정의 ID와 함께 새 연결을 사용하여 Adobe Experience Platform으로 다시 리디렉션됩니다. 대상 구성 화면에서 적절한 광고주 계정을 선택하여 계속 진행합니다.

* **[!UICONTROL 베어러 토큰]**: 대상을 인증하려면 베어러 토큰을 입력합니다.

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Amazon 광고 Advertiser ID]**: 대상에 사용된 Target Amazon 광고 계정의 ID를 선택합니다.

참고: 이 Amazon Ads Advertiser ID를 선택하면 새 대상을 만들어 이 ID를 변경해야 합니다. OAuth 자격 증명을 다시 인증하고 새 광고주 ID를 선택하는 경우 변경 사항이 적용되지 않습니다.

![새 대상 구성](../../assets/catalog/advertising/amazon_ads_image_1.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 특성 및 ID 매핑 {#map}

Amazon Ads 연결은 ID 일치 목적으로 해시된 이메일 주소와 해시된 전화 번호를 지원합니다.  아래 스크린샷에서는 Amazon Ads 연결과 호환되는 예는 를 제공합니다.

![Amazon 광고에 대한 Adobe 매핑](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 해시된 이메일 주소를 매핑하려면 `Email_LC_SHA256` id 네임스페이스를 소스 필드로 사용합니다.
* 해시된 전화 번호를 매핑하려면 `Phone_SHA256` id 네임스페이스를 소스 필드로 사용합니다.
* 해시되지 않은 이메일 주소 또는 전화 번호를 매핑하려면 해당 ID 네임스페이스를 소스 필드로 선택하고 `Apply Transformation` 활성화 시 Platform에서 ID를 해시하도록 하는 옵션.

가능한 한 많은 필드를 매핑하는 것이 좋습니다. 하나의 소스 속성만 사용할 수 있는 경우 단일 필드를 매핑할 수 있습니다.  Amazon 광고 대상은 매핑 용도로 매핑된 모든 필드를 사용하므로, 더 많은 필드가 제공되는 경우 더 높은 일치율을 제공합니다. 허가한 식별자에 대한 자세한 내용은 [Amazon Ads 해시된 대상 도움말 페이지](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## 내보낸 데이터 / 데이터 내보내기 유효성 검사 {#exported-data}

대상이 업로드되면 다음 단계를 사용하여 대상이 생성되어 올바르게 업로드되었는지 확인할 수 있습니다.

**Amazon DSP용**

광고주 ID → 대상 → 광고주 대상으로 이동합니다. 대상이 성공적으로 만들어지고 최소 대상 구성원 수를 충족하는 경우, 상태 가 표시됩니다. `Active`.  대상 크기 및 도달 범위에 대한 자세한 내용은 Amazon DSP 사용자 인터페이스 오른쪽의 예측 도달 패널에서 찾을 수 있습니다.

![Amazon DSP 대상 만들기 유효성 검사](../../assets/catalog/advertising/amazon_ads_image_3.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 읽기 [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

추가 도움말 설명서는 다음 Amazon Ads 도움말 리소스를 참조하십시오.

* [Amazon DSP 도움말 센터](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
