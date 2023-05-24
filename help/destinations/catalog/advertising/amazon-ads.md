---
title: Amazon 광고
description: Amazon Ads는 등록된 판매자, 공급업체, 서적 공급업체, Kindle Direct Publishing(KDP) 작성자, 앱 개발자 및/또는 에이전시에 대한 광고 목표를 달성하는 데 도움이 되는 다양한 옵션을 제공합니다. Amazon Ads와 Adobe Experience Platform의 통합은 ADSP(Amazon DSP)를 비롯한 Amazon Ads 제품에 턴키 통합을 제공합니다. Adobe Experience Platform의 Amazon 광고 대상을 사용하면 Amazon DSP에서 타깃팅 및 활성화를 위해 광고주 대상을 정의할 수 있습니다.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---

# (베타) Amazon 광고 연결 {#amazon-ads}

## 개요 {#overview}

Amazon Ads는 등록된 판매자, 공급업체, 서적 공급업체, Kindle Direct Publishing(KDP) 작성자, 앱 개발자 및/또는 에이전시에 대한 광고 목표를 달성하는 데 도움이 되는 다양한 옵션을 제공합니다.

Amazon Ads와 Adobe Experience Platform의 통합은 ADSP(Amazon DSP)를 비롯한 Amazon Ads 제품에 턴키 통합을 제공합니다. Adobe Experience Platform의 Amazon 광고 대상을 사용하면 Amazon DSP에서 타깃팅 및 활성화를 위해 광고주 대상을 정의할 수 있습니다.

이 연결은 다음 Amazon 마켓플레이스에서 대상 생성을 지원합니다. `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>이 설명서 페이지는 다음 사용자가 만들었습니다. *Amazon 광고* 팀. 현재 베타 제품이며 기능은 변경될 수 있습니다. 문의 사항이나 업데이트 요청은 다음 주소로 직접 문의하십시오. *`amc-support@amazon.com`.*

## 사용 사례 {#use-cases}

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 *Amazon 광고* 대상: 다음은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 활성화 및 타기팅 {#activation-and-targeting}

Amazon DSP과의 통합을 통해 Amazon 광고 광고주가 Adobe Experience Platform에서 Amazon의 DSP으로 advertiser CDP 세그먼트를 전달하여 광고 타깃팅을 위한 광고주 대상을 만들 수 있습니다. 긍정적인 타겟팅과 부정적인 타겟팅(제외)을 위해 Amazon DSP 내에서 대상을 선택할 수 있습니다. 또한 광고주는 Amazon Marketing Cloud을 통해 생성된 신호를 사용하여 광고주 대상을 최적화하고 대상 변경을 Amazon DSP과 동기화할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

Adobe Experience Platform과 Amazon Ads 연결을 사용하려면 먼저 사용자가 Amazon DSP Advertiser 계정에 액세스할 수 있어야 합니다.  이러한 인스턴스를 프로비저닝하려면 Amazon Ads 웹 사이트의 다음 페이지를 방문하십시오.

* [Amazon DSP 시작](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## 지원되는 ID {#supported-identities}

다음 *Amazon 광고* 연결은 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md). Amazon 광고에서 지원하는 ID에 대한 자세한 내용은 다음을 참조하십시오. [Amazon DSP 지원 센터](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| TARGET ID | 설명 | 고려 사항 |
|---|---|---|
| phone_sha256 | SHA256 알고리즘으로 해시된 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원됩니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 세그먼트(대상자)의 모든 구성원을 내보냅니다. *Amazon 광고* 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상에 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**.

연결하려는 광고주 계정을 먼저 선택하는 Amazon Ads 연결 인터페이스로 이동합니다.  연결 시 선택한 광고주 계정의 ID가 제공되는 새 연결을 사용하여 Adobe Experience Platform으로 다시 리디렉션됩니다. 계속하려면 대상 구성 화면에서 적절한 광고주 계정을 선택하십시오.

* **[!UICONTROL 전달자 토큰]**: 대상에 인증할 전달자 토큰을 입력합니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Amazon 광고 광고주 ID]**: 대상에 사용되는 대상 Amazon 광고 계정의 ID를 선택합니다.

참고: 이 Amazon Ads 광고주 ID를 선택하면 이를 변경하려면 새 대상을 만들어야 합니다. OAuth 자격 증명을 다시 인증하고 새 광고주 ID를 선택하는 경우 변경 사항이 적용되지 않습니다.

![새 대상 구성](../../assets/catalog/advertising/amazon_ads_image_1.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

### 속성 및 ID 매핑 {#map}

Amazon 광고 연결은 ID 일치를 위해 해시된 이메일 주소와 해시된 전화 번호를 지원합니다.  아래 스크린샷은 Amazon Ads 연결과 호환되는 예제 일치를 제공합니다.

![Amazon 광고 매핑에 대한 Adobe](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 해시된 이메일 주소를 매핑하려면 `Email_LC_SHA256` 소스 필드로서의 id 네임스페이스.
* 해시된 전화 번호를 매핑하려면 `Phone_SHA256` 소스 필드로서의 id 네임스페이스.
* 해시되지 않은 이메일 주소 또는 전화번호를 매핑하려면 해당 ID 네임스페이스를 소스 필드로 선택하고 `Apply Transformation` 활성화 시 Platform이 ID를 해시하도록 하는 옵션입니다.

가능한 많은 필드를 매핑하는 것이 좋습니다. 하나의 소스 속성만 사용할 수 있는 경우 단일 필드를 매핑할 수 있습니다.  Amazon 광고 대상은 매핑 목적으로 매핑된 모든 필드를 활용하므로, 더 많은 필드가 제공되는 경우 더 높은 일치율을 산출합니다. 승인된 식별자에 대한 자세한 내용은 [Amazon Ads 해시된 대상 도움말 페이지](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

대상이 업로드되면 다음 단계를 통해 대상이 올바르게 생성 및 업로드되었는지 확인할 수 있습니다.

**Amazon DSP용**

광고주 ID → 대상 → 광고주 대상으로 이동합니다. 대상자가 성공적으로 만들어지고 최소 대상자 구성원 수를 충족하면 상태가 다음과 같이 표시됩니다. `Active`.  대상자 크기 및 도달에 대한 자세한 내용은 Amazon DSP 사용자 인터페이스 오른쪽에 있는 예측 도달 패널에서 확인할 수 있습니다.

![Amazon DSP 대상 만들기 유효성 검사](../../assets/catalog/advertising/amazon_ads_image_3.png)

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

추가 도움말 설명서를 보려면 다음 Amazon Ads 도움말 리소스를 참조하십시오.

* [Amazon DSP 도움말 센터](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
