---
title: Amazon 광고
description: Amazon Ads는 등록된 판매자, 공급업체, 서적 공급업체, Kindle Direct Publishing(KDP) 작성자, 앱 개발자 및/또는 에이전시에 대한 광고 목표를 달성하는 데 도움이 되는 다양한 옵션을 제공합니다. Amazon Ads와 Adobe Experience Platform의 통합은 ADSP(Amazon DSP)를 비롯한 Amazon Ads 제품에 턴키 통합을 제공합니다. Adobe Experience Platform의 Amazon 광고 대상을 사용하면 Amazon DSP에서 타깃팅 및 활성화를 위해 광고주 대상을 정의할 수 있습니다.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 24f7463f7005f77f8d93e7cb2c04efc0fb4e3a0b
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# (베타) Amazon 광고 연결 {#amazon-ads}

## 개요 {#overview}

[!DNL Amazon Ads] 는 등록된 판매자, 공급업체, 서적 공급업체, Kindle Direct Publishing(KDP) 작성자, 앱 개발자 및/또는 에이전시에 대한 광고 목표를 달성하는 데 도움이 되는 다양한 옵션을 제공합니다.

다음 [!DNL Amazon Ads] Adobe Experience Platform과의 통합을 통해 [!DNL Amazon Ads] Amazon DSP(ADSP) 및 Amazon Marketing Cloud(AMC)를 포함한 제품.

사용 [!DNL Amazon Ads] 대상 Adobe Experience Platform에서 사용자는 Amazon DSP에서의 타겟팅 및 활성화를 위해 광고주 대상을 정의할 수 있습니다.  또한 사용자는 자신의 데이터를에 업로드할 수 있습니다 [!DNL Amazon Marketing Cloud] 대상자별 성능을 이해하기 위해 광고주가 제공한 차원, Amazon 세그먼트의 멤버십 또는 AMC에서 사용할 수 있는 기타 신호를 이해했습니다. 광고주 대상을 AMC에 업로드한 후 사용자는 [!DNL Amazon Marketing Cloud] 내에서 Amazon 신호를 사용하여 대상 구성원을 수정, 개선 또는 추가하려면 [!DNL Amazon Marketing Cloud].

AMC는 Amazon 소유 및 운영되는 속성에서 디스플레이, 비디오, 스트리밍 TV, 오디오 및 스폰서 광고를 비롯한 미디어 전반으로 확산되는 고유한 신호를 수집합니다. 사용자는 Adobe Experience Platform에서 AMC로 큐레이트된 세그먼트를 쉽게 전송하여 대상의 마켓 내 그룹, 라이프스타일 집단 및 브랜드 참여 패턴과 같은 학습을 향상시킬 수 있습니다. 그런 다음 증강된 세그먼트를 사용하여 Amazon DSP에서 미디어 활성화를 최적화할 수 있습니다.

>[!IMPORTANT]
>
>이 대상 커넥터 및 설명서 페이지는 *[!DNL Amazon Ads]* 팀. 현재 베타 제품이며 기능은 변경될 수 있습니다. 문의 사항이나 업데이트 요청은 다음 주소로 직접 문의하십시오. *`amc-support@amazon.com`.*

## 사용 사례 {#use-cases}

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 *[!DNL Amazon Ads]* 대상: 다음은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 활성화 및 타기팅 {#activation-and-targeting}

Amazon DSP과의 통합을 통해 다음과 같은 작업을 수행할 수 있습니다 [!DNL Amazon Ads] 광고주가 Adobe Experience Platform에서 Amazon의 DSP으로 advertiser CDP 대상을 전달하여 광고 타깃팅을 위한 광고주 대상을 만들 수 있습니다. 긍정적인 타겟팅과 부정적인 타겟팅(제외)을 위해 Amazon DSP 내에서 대상을 선택할 수 있습니다.

### Analytics 및 측정 {#analytics-and-measurement}

이 통합 대상 [!DNL Amazon Marketing Cloud] (AMC) 허용 [!DNL Amazon Ads] Adobe Experience Platform 양식의 CDP 세그먼트를 AMC에 전달하는 광고주. 그런 다음 광고주는 CDP 입력을 와 결합할 수 있습니다. [!DNL Amazon Ads] 는 개인정보 보호 준수 형식으로 미디어 영향, 대상 세그먼트 및 고객 여정과 같은 주제에 대한 사용자 지정 분석을 알리고 수행합니다. 예를 들어 광고주는 기존 고객 목록을 업로드하여 전체 광고 캠페인 성과 또는 제품 세부 사항 페이지 보기, 장바구니에 제품 추가 또는 제품 구매와 같은 Amazon 전환 이벤트의 집계된 통계를 파악할 수 있습니다.

### 광고 최적화:

이 통합 대상 [!DNL Amazon Marketing Cloud] (AMC)를 사용하면 광고주가 자신의 고객 목록을 업로드하고 [!DNL Amazon Marketing Cloud] SQL에서는 타깃팅을 위해 Amazon DSP에서 활성화 준비 대상을 만들기 전에 반복해서 대상에 중복 분석, 억제, 추가 또는 최적화를 수행합니다.

## 전제 조건 {#prerequisites}

을(를) 사용하려면 [!DNL Amazon Ads] Adobe Experience Platform에 연결하려면 먼저 사용자가 Amazon DSP 광고주 계정 또는 [!DNL Amazon Marketing Cloud] 인스턴스. 이러한 인스턴스를 프로비저닝하려면 [!DNL Amazon Ads] 웹 사이트:

* [Amazon DSP 시작](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Amazon Marketing Cloud 시작](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## 지원되는 ID {#supported-identities}

다음 *[!DNL Amazon Ads]* 연결은 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service//features/namespaces.md). 에서 지원하는 ID에 대한 자세한 내용 [!DNL Amazon Ads], 다음 방문: [Amazon DSP 지원 센터](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| phone_sha256 | SHA256 알고리즘으로 해시된 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원됩니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | 에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. *[!DNL Amazon Ads]* 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**.

다음으로 이동되었습니다. [!DNL Amazon Ads] 접속하고자 하는 광고주 계정을 먼저 선택하는 접속 인터페이스. 연결하면 선택한 광고주 계정의 ID가 제공된 새 연결로 Adobe Experience Platform으로 다시 리디렉션됩니다. 계속하려면 대상 구성 화면에서 적절한 광고주 계정을 선택하십시오.

* **[!UICONTROL 전달자 토큰]**: 대상에 인증할 전달자 토큰을 입력합니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Amazon 광고 연결]**: 대상의 ID를 선택합니다 [!DNL Amazon Ads] 대상에 사용되는 계정입니다.

>[!NOTE]
>
>대상 구성을 저장하면 을(를) 변경할 수 없습니다. [!DNL Amazon Ads] Amazon 계정을 통해 다시 인증하더라도 광고주 ID입니다. 다른 항목 사용하기 [!DNL Amazon Ads] 광고주 ID입니다. 새 대상 연결을 만들어야 합니다.

* **[!UICONTROL 광고주 영역]**: 광고주가 호스팅되는 적절한 영역을 선택합니다. 각 지역에서 지원하는 마켓플레이스에 대한 자세한 내용은 [Amazon 광고 설명서](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![새 대상 구성](../../assets/catalog/advertising/amazon_ads_image_4.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

읽기 [스트리밍 대상자 내보내기 대상으로 프로필 및 대상자 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### 속성 및 ID 매핑 {#map}

다음 [!DNL Amazon Ads] 연결은 id 일치를 위해 해시된 이메일 주소와 해시된 전화 번호를 지원합니다. 아래 스크린샷은 와 호환되는 예제 일치를 제공합니다. [!DNL Amazon Ads] 연결:

![Amazon 광고 매핑에 대한 Adobe](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 해시된 이메일 주소를 매핑하려면 `Email_LC_SHA256` 소스 필드로서의 id 네임스페이스.
* 해시된 전화 번호를 매핑하려면 `Phone_SHA256` 소스 필드로서의 id 네임스페이스.
* 해시되지 않은 이메일 주소 또는 전화번호를 매핑하려면 해당 ID 네임스페이스를 소스 필드로 선택하고 `Apply Transformation` 활성화 시 Platform이 ID를 해시하도록 하는 옵션입니다.

의 대상 구성에서 지정된 대상 필드를 한 번만 선택합니다. [!DNL Amazon Ads] 커넥터.  예를 들어 비즈니스 이메일을 제출하는 경우 동일한 대상 구성에서 개인 이메일을 매핑할 수도 없습니다.

가능한 많은 필드를 매핑하는 것이 좋습니다. 하나의 소스 속성만 사용할 수 있는 경우 단일 필드를 매핑할 수 있습니다. 다음 [!DNL Amazon Ads] 대상은 매핑 목적으로 매핑된 모든 필드를 사용하므로, 더 많은 필드가 제공되는 경우 더 높은 일치율을 산출합니다. 승인된 식별자에 대한 자세한 내용은 [Amazon Ads 해시된 대상 도움말 페이지](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

대상이 업로드되면 다음 단계를 통해 대상이 올바르게 생성 및 업로드되었는지 확인할 수 있습니다.

**Amazon DSP용**

다음으로 이동 **[!UICONTROL 광고주 ID]** > **[!UICONTROL 대상]** > **[!UICONTROL 광고주 대상]**. 대상자가 성공적으로 만들어지고 최소 대상자 구성원 수를 충족하면 상태가 다음과 같이 표시됩니다. `Active`. 대상자 크기 및 도달에 대한 자세한 내용은 Amazon DSP 사용자 인터페이스 오른쪽에 있는 예측 도달 패널에서 확인할 수 있습니다.

![Amazon DSP 대상 만들기 유효성 검사](../../assets/catalog/advertising/amazon_ads_image_3.png)

**대상[!DNL Amazon Marketing Cloud]**

왼쪽 스키마 브라우저에서 아래에 있는 대상자를 찾습니다. **[!UICONTROL 광고주 업로드됨]** > **[!UICONTROL aep_audiences]**. 그런 다음 AMC SQL 편집기에서 다음 절을 사용하여 대상자를 쿼리할 수 있습니다.

`select count(user_id) from aep_audiences where audienceId = '1234567'`

![Amazon Marketing Cloud 대상자 만들기 유효성 검사](../../assets/catalog/advertising/amazon_ads_image_5.png)


## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

추가 도움말 설명서를 보려면 다음을 참조하십시오. [!DNL Amazon Ads] 도움말 리소스:

* [Amazon DSP 도움말 센터](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## 변경 로그 {#changelog}

이 섹션에서는 이 대상 커넥터에 대한 기능 및 중요 설명서 업데이트를 캡처합니다.

+++ 변경 로그 보기

| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2024년 2월 | 기능 및 설명서 업데이트 | 에 사용할 대상자를 내보내는 옵션이 추가되었습니다. [!DNL Amazon Marketing Cloud] (AMC). |
| 2023년 5월 | 기능 및 설명서 업데이트 | <ul><li>에서 광고주 영역 선택에 대한 지원을 추가했습니다. [대상 연결 워크플로](#destination-details).</li><li>광고주 지역 선택 사항의 추가를 반영하도록 설명서를 업데이트했습니다. 올바른 광고주 영역 선택에 대한 자세한 내용은 [Amazon 설명서](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| 2023년 3월 | 초기 릴리스 | 초기 대상 릴리스 및 설명서가 게시되었습니다. |

{style="table-layout:auto"}

+++
