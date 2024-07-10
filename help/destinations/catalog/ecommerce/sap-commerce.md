---
title: SAP Commerce 연결
description: SAP Commerce 대상 커넥터를 사용하여 SAP 계정의 고객 레코드를 업데이트합니다.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 3bd1a2a7-fb56-472d-b9bd-603b94a8937e
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 3%

---

# [!DNL SAP Commerce] 연결

[!DNL SAP Commerce], 이전에 [[!DNL Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html)는 B2B 및 B2C 기업을 위한 클라우드 기반 전자 상거래 플랫폼 솔루션이며 SAP Customer Experience 포트폴리오의 일부로 제공됩니다. [[!DNL SAP] 구독 청구](https://www.sap.com/products/financial-management/subscription-billing.html) 는 포트폴리오의 제품이며 표준화된 통합을 통해 간소화된 판매 및 결제 경험을 통해 완전한 구독 라이프사이클 관리를 가능하게 합니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 를 사용합니다. [[!DNL SAP Subscription Billing] 고객 관리 API](https://api.sap.com/api/BusinessPartner_APIs/path/PUT_customers-customerNumber)을 클릭하여 다음 기간 내에 고객 세부 사항을 업데이트합니다. [!DNL SAP Commerce] 활성화 후 기존 Experience Platform 대상으로부터.

에 대한 인증 지침 [!DNL SAP Commerce] 인스턴스는 다음보다 아래에 있습니다. [대상에 인증](#authenticate) 섹션.

## 사용 사례 {#use-cases}

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL SAP Commerce] destination은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

[!DNL SAP Commerce] 고객은 비즈니스와 상호 작용하는 개인 또는 조직 엔터티에 대한 정보를 저장합니다. 귀하의 팀은에 있는 고객을 사용합니다. [!DNL SAP Commerce] Experience Platform 대상자를 빌드합니다. 이 대상자를 (으)로 보낸 후 [!DNL SAP Commerce], 해당 정보가 업데이트되고, 각 고객에게 해당 값이 고객이 속한 대상을 나타내는 대상 이름으로 된 속성이 할당됩니다.

## 전제 조건 {#prerequisites}

Experience Platform 및 에서 설정해야 하는 사전 요구 사항에 대해서는 아래 섹션을 참조하십시오. [!DNL SAP Commerce] 및 를 사용하기 전에 수집해야 하는 정보의 경우 [!DNL SAP Commerce] 대상.

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

에 대한 데이터를 활성화하기 전에 [!DNL SAP Commerce] 대상, 다음 항목이 있어야 합니다. [스키마](/help/xdm/schema/composition.md), a [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html), 및 [대상](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) 생성 위치 [!DNL Experience Platform].

다음에 대한 Experience Platform 설명서 참조: [대상자 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md) 대상 상태에 대한 지침이 필요한 경우.

### 사전 요구 사항 [!DNL SAP Commerce] 대상 {#prerequisites-destination}

Platform에서 로 데이터를 내보내려면 다음 전제 조건을 참고하십시오. [!DNL SAP Commerce] 계정:

#### 다음 항목이 있어야 합니다. [!DNL SAP Subscription Billing] account {#prerequisites-account}

Platform에서 로 데이터를 내보내려면 [!DNL SAP Commerce] 계정, 다음 권한이 필요합니다. [!DNL SAP Subscription Billing] 계정입니다. 유효한 청구 계정이 없는 경우 다음으로 문의하십시오. [!DNL SAP] 계정 관리자. 다음을 참조하십시오. [[!DNL SAP] 플랫폼 구성](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) 자세한 내용은 문서를 참조하십시오.

#### 서비스 키 생성 {#prerequisites-service-key}

* 다음 [!DNL SAP Commerce] 서비스 키를 사용하면 [!DNL SAP Subscription Billing] Experience Platform을 통한 API. 다음을 참조하십시오. [!DNL SAP Commerce] [클라이언트 ID 및 클라이언트 암호를 사용하여 서비스 키 만들기](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/87c11a0f5dc3494eaf3baa355925c030.html#create-a-service-key-with-client-id-and-client-secret) 서비스 키를 만듭니다. [!DNL SAP Commerce]를 사용하려면 다음 요구 사항을 충족해야 합니다.
   * 클라이언트 ID
   * 클라이언트 암호
   * URL. URL 패턴은 다음과 같습니다. `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. 이 값은 나중에 값을 얻는 데 사용됩니다. `Region` 및 `Endpoint`.

+++서비스 키의 예를 보려면 선택

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

#### 에서 사용자 정의 참조 만들기 [!DNL SAP Subscription Billing] {#prerequisites-custom-reference}

에서 Experience Platform 대상자 상태를 업데이트하려면 [!DNL SAP Subscription Billing], 플랫폼에서 선택한 각 대상자에 대한 사용자 지정 참조 필드가 필요합니다.

사용자 지정 참조를 만들려면 [!DNL SAP Subscription Billing] 계정 및 다음으로 이동 **[기본 데이터 및 구성]** > **[사용자 지정 참조]** 페이지를 가리키도록 업데이트하는 중입니다. 그런 다음 을 선택합니다. **[!UICONTROL 만들기]** 플랫폼에서 선택한 각 대상에 대해 새 참조를 추가합니다. 다음에 이러한 참조 필드 이름이 필요합니다 [대상자 내보내기 예약 및 예제](#schedule-segment-export-example) 단계.

사용자 지정 항목을 만드는 방법의 예 **[!UICONTROL 참조 유형]** 다음 범위 내 [!DNL SAP Subscription Billing] 다음이 표시됩니다.
![SAP 구독 청구에서 사용자 정의 참조를 만들 위치를 보여 주는 이미지.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

자세한 지침은 [!DNL SAP Subscription Billing] [사용자 지정 참조](https://help.sap.com/docs/CLOUD_TO_CASH_OD/80d121f216af43648e79664efe5595f7/85696a63c8d8453a934e86c9413a25cf.html?version=2023-11-27) 설명서를 참조하십시오.

### 필요한 자격 증명 수집 {#gather-credentials}

연결하려면 [!DNL SAP Commerce] Experience Platform을 수행하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 클라이언트 ID | 값: `clientId` 서비스 키에서. |
| 클라이언트 암호 | 값: `clientSecret` 서비스 키에서. |
| 엔드포인트 | 값: `url` 서비스 키에서 와 유사합니다. `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| 지역 | 데이터 센터 위치. 영역은 다음 위치에 있습니다. `url` 와 유사한 값을 갖습니다. `eu10` 또는 `us10`. 예를 들어 `url` 은(는) `https://eu10.revenue.cloud.sap/api` 필요 사항 `eu10`. |

## 가드레일 {#guardrails}

에 대한 API 요청 [!DNL SAP Cloud Management service] 다음에 해당됨: [비율 제한](https://help.sap.com/docs/btp/sap-business-technology-platform/account-administration-rate-limiting). 요금 제한을 초과하면 `HTTP 429 Too Many Requests` 응답 상태 코드 .

## 지원되는 ID {#supported-identities}

[!DNL SAP Commerce] 는 아래 표에 설명된 id 업데이트를 지원합니다. 자세히 알아보기 [id](/help/identity-service/features/namespaces.md).

| 대상 ID | 설명 | 고려 사항 |
| --- | --- | --- |
| `customerNumberSAP` | 에 이미 있는 개인 또는 법인 고객의 고객 식별자 [!DNL SAP Commerce] 계정입니다. | 필수 |

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 모든 대상에 대해 설명합니다.

이 대상은 Experience Platform을 통해 생성된 모든 대상의 활성화를 지원합니다 [세분화 서비스](../../../segmentation/home.md).

이 대상은 아래 표에 설명된 대상의 활성화도 지원합니다.

| 대상자 유형 | 지원됨 | 설명 |
| ------------- | --------- | ----------- |
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ 덧신 | 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>원하는 스키마 필드와 함께 대상의 모든 구성원을 내보냅니다 *(예: 이메일 주소, 전화번호, 성)*&#x200B;를 입력합니다.</li><li> 플랫폼에서 선택한 각 대상에 대해 [!DNL SAP Commerce] 추가 속성은 Platform에서 대상 상태로 업데이트됩니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | <ul><li>스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필을 업데이트하면 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

다음 범위 내 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**, 검색 [!DNL SAP Commerce]. 또는 아래에서 찾을 수 있습니다 **[!UICONTROL 전자 상거래]** 범주.

### 대상으로 인증 {#authenticate}

아래의 필수 필드를 입력하십시오. 다음을 참조하십시오. [서비스 키 생성](#prerequisites-service-key) 섹션에 자세히 설명되어 있습니다.

| 필드 | 설명 |
| --- | --- |
| **[!UICONTROL 클라이언트 ID]** | 값: `clientId` 서비스 키에서. |
| **[!UICONTROL 클라이언트 암호]** | 값: `clientSecret` 서비스 키에서. |
| **[!UICONTROL 엔드포인트]** | 값: `url` 서비스 키에서 와 유사합니다. `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| **[!UICONTROL 지역]** | 데이터 센터 위치. 영역은 다음 위치에 있습니다. `url` 와 유사한 값을 갖습니다. `eu10` 또는 `us10`. 예를 들어 `url` 은(는) `https://eu10.revenue.cloud.sap/api` 필요 사항 `eu10`. |

대상에 인증하려면 다음을 선택합니다. **[!UICONTROL 대상에 연결]**.
![대상에 인증하는 방법을 보여 주는 Platform UI의 이미지입니다.](../../assets/catalog/ecommerce/sap-commerce/authenticate-destination.png)

제공된 세부 정보가 유효한 경우 UI에 **[!UICONTROL 연결됨]** 녹색 확인 표시가 있는 상태. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![인증 후 채워질 대상 세부 사항을 표시하는 플랫폼 UI의 이미지.](../../assets/catalog/ecommerce/sap-commerce/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 고객 유형]**: 다음 중 하나를 선택합니다. ***개인*** 또는 ***기업*** 대상 내의 엔티티에 따라 다릅니다. 다음 [!DNL SAP Subscription Billing] [스키마](https://api.sap.com/api/BusinessPartner_APIs/schema) 에 매핑된 이 선택 사항에 따라 필수 필드를 전환합니다. `customerType` 특성. 선택 항목이 ***기업***&#x200B;를 클릭한 다음 과 같은 필수 매핑 `firstName` 및 `lastName` 개별 고객에 대해 필요한 사항은 무시되고 `company` 는 필수가 되며, 그 반대의 경우도 마찬가지입니다.

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

대상 데이터를 Adobe Experience Platform에서 로 올바르게 보내려면 [!DNL SAP Commerce] 대상, 필드 매핑 단계를 거쳐야 합니다. 매핑은 Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 필드 간에 링크를 만드는 것으로 구성됩니다. XDM 필드를 [!DNL SAP Commerce] 대상 필드에서 아래 단계를 수행합니다.

#### 매핑 `customerNumberSAP` 신원

다음 `customerNumberSAP` id는 이 대상의 필수 매핑입니다. 매핑하려면 아래 단계를 따르십시오.
1. 다음에서 **[!UICONTROL 매핑]** 단계, 선택 **[!UICONTROL 새 매핑 추가]**. 이제 새 매핑 행이 화면에 표시됩니다.
   ![새 매핑 추가 버튼이 강조 표시된 Platform UI 스크린샷](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. 다음에서 **[!UICONTROL 소스 필드 선택]** 창에서 다음을 선택합니다. **[!UICONTROL ID 네임스페이스 선택]** 및 선택 `customerNumberSAP`.
   ![ID로 매핑할 소스 속성으로 이메일을 선택하는 Platform UI 스크린샷입니다.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-identity.png)
1. 다음에서 **[!UICONTROL 대상 필드 선택]** 창에서 다음을 선택합니다. **[!UICONTROL ID 네임스페이스 선택]** 및 선택 `customerNumber` 신원.
   ![ID로 매핑할 타겟 속성으로 이메일을 선택하는 Platform UI 스크린샷입니다.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-identity.png)

| 소스 필드 | 대상 필드 | 필수 |
| --- | --- | --- |
| `IdentityMap: customerNumberSAP` | `Identity: customerNumber` | 예 |

다음은 ID 매핑의 예입니다.
![customerNumber ID 매핑의 예를 보여 주는 플랫폼 UI의 이미지.](../../assets/catalog/ecommerce/sap-commerce/mapping-identities.png)

#### 속성 매핑

XDM 프로필 스키마와 XDM 프로필 스키마 사이에 업데이트할 다른 속성을 추가하려면 [!DNL SAP Subscription Billing] account, 아래 단계를 반복합니다.
1. 다음에서 **[!UICONTROL 매핑]** 단계, 선택 **[!UICONTROL 새 매핑 추가]**. 이제 새 매핑 행이 화면에 표시됩니다.
   ![새 매핑 추가 버튼이 강조 표시된 Platform UI 스크린샷](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. 다음에서 **[!UICONTROL 소스 필드 선택]** 창에서 다음을 선택합니다. **[!UICONTROL 속성 선택]** 범주를 선택한 다음 XDM 속성을 선택합니다.
   ![성 을 소스 속성으로 선택하는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-attribute.png)
1. 다음에서 **[!UICONTROL 대상 필드 선택]** 창, 선택 **[!UICONTROL 사용자 지정 속성 선택]** 범주 및 이름 입력 [!DNL SAP Subscription Billing] 고객 목록의 속성 [스키마](https://api.sap.com/api/BusinessPartner_APIs/schema) 속성.
   ![lastName이 타겟 속성으로 정의되는 Platform UI 스크린샷입니다.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-attribute.png)

>[!IMPORTANT]
>
> 대상 필드 이름은 대소문자를 구분하며 [!DNL SAP Subscription Billing] 속성 이름. 이에 대한 유일한 예외는 다음과 같습니다. `country` 를 사용해야 하는 위치 `countryCode` 대신, [!DNL SAP Subscription Billing] 는 알파 2(ISO 3166) 국가 코드를 지원합니다. 값은 대/소문자를 구분하며 0~3자 사이여야 합니다. 따라서 정의한 대로 정확하게 제공하면 오류가 발생합니다. `The country code {} does not exist` 또는 `size must be between 0 and 3`.

#### 맵 `mandatory` 선택한 고객 유형에 대한 속성

필수 속성 매핑은 **[!UICONTROL 고객 유형]** 선택하셨습니다. 필수 속성을 매핑하려면 아래에서 을(를) 선택합니다.

>[!BEGINTABS]

>[!TAB 개인 사용자]

| 소스 필드 | 대상 필드 | 필수 |
| --- | --- | --- |
| `xdm: person.lastName` | `Attribute: lastName` | 예 |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | 예 |

>[!TAB 기업 고객]

| 소스 필드 | 대상 필드 | 필수 |
| --- | --- | --- |
| `xdm: b2b.companyName` | `Attribute: company` | 예 |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | 예 |

>[!ENDTABS]

#### 추가 속성 매핑

그런 다음 XDM 프로필 스키마와 XDM 프로필 스키마 사이에 매핑을 추가할 수 있습니다. [!DNL SAP Subscription Billing] [스키마](https://api.sap.com/api/BusinessPartner_APIs/schema) 아래 표시된 것처럼 고객에 대한 속성:

>[!BEGINTABS]

>[!TAB 개인 사용자]

| 소스 필드 | 대상 필드 | 필수 |
| --- | --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstName` | 아니요 |
| `xdm: workAddress.street1` | `Attribute: street` | 아니요 |
| `xdm: workAddress.city` | `Attribute: city` | 아니요 |

고객이 개인인 필수 및 선택적 속성 매핑의 예가 아래에 나와 있습니다.
![고객이 개인인 경우 필수 및 선택적 속성 매핑의 예를 보여 주는 Platform UI의 이미지입니다.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-individual.png)

>[!TAB 기업 고객]

| 소스 필드 | 대상 필드 | 필수 |
| --- | --- | --- |
| `xdm: workAddress.street1` | `Attribute: street` | 아니요 |
| `xdm: workAddress.city` | `Attribute: city` | 아니요 |

고객이 법인인 경우 필수 및 선택적 속성 매핑이 모두 포함된 예는 다음과 같습니다.
![고객이 법인인 경우 필수 및 선택적 속성 매핑이 모두 있는 예를 보여 주는 Platform UI의 이미지입니다.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-corporate.png)

>[!ENDTABS]

대상 연결에 대한 매핑 제공을 마치면 을(를) 선택합니다 **[!UICONTROL 다음]**.

### 대상자 내보내기 예약 및 예제 {#schedule-segment-export-example}

다음을 수행할 때 [대상자 내보내기 예약](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 단계: 플랫폼 대상자를 [속성](#prerequisites-attribute) 위치: [!DNL SAP Subscription Billing].

대상 내보내기 예약 단계의 예이며 위치는 입니다. [!DNL SAP Commerce] **[!UICONTROL 매핑 ID]** 강조 표시된 이(가) 아래에 표시됩니다.
![매핑 ID가 채워진 대상자 내보내기 일정을 표시하는 플랫폼의 이미지입니다.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export.png)

이렇게 하려면 각 세그먼트를 선택한 다음 사용자 정의 참조 이름을 입력합니다. [!DNL SAP Subscription Billing] 다음에서 [!DNL SAP Commerce] **[!UICONTROL 매핑 ID]** 대상 커넥터 필드. 사용자 지정 참조 만들기에 대한 지침은 [에서 사용자 정의 참조 만들기 [!DNL SAP Subscription Billing]](#prerequisites-custom-reference) 섹션.

>[!IMPORTANT]
>
> 사용자 지정 참조 레이블을 값으로 사용하지 마십시오.
>![매핑에 사용자 지정 참조 레이블 값을 사용하지 말아야 함을 나타내는 이미지입니다.](../../assets/catalog/ecommerce/sap-commerce/custom-reference-dont-use-label-for-mapping.png)

예를 들어 선택한 Experience Platform 대상이 `sap_audience1` 그리고 상태를 [!DNL SAP Subscription Billing] 사용자 지정 참조 `SAP_1`에서 이 값을 지정합니다. [!DNL SAP_Commerce] **[!UICONTROL 매핑 ID]** 필드.

예 **[!UICONTROL 참조 유형]** 출처: [!DNL SAP Subscription Billing] 다음이 표시됩니다.
![SAP 구독 청구에서 사용자 정의 참조를 만들 위치를 보여 주는 이미지.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

대상이 선택되고 해당하는 경우 대상자 내보내기 단계 예약의 예 [!DNL SAP Commerce] **[!UICONTROL 매핑 ID]** 강조 표시된 이(가) 아래에 표시됩니다.
![매핑 ID가 채워진 대상자 내보내기 일정을 표시하는 플랫폼의 이미지입니다.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export-example.png)

다음 내에 있는 값을 표시함: **[!UICONTROL 매핑 ID]** 필드는 과 정확히 일치해야 합니다. [!DNL SAP Subscription Billing] **[!UICONTROL 참조 유형]** 값 .

활성화된 각 Platform 대상에 대해 이 섹션을 반복합니다.

두 대상을 선택한 위에 표시된 이미지에 따라 매핑은 다음과 같습니다. | [!DNL SAP Commerce] 대상자 이름 | [!DNL SAP Subscription Billing] **[!UICONTROL 참조 유형]** | [!DNL SAP Commerce] **[!UICONTROL 매핑 ID]** 값 | | — | — | — | | sap_audience1 | `SAP_1` | `SAP_1` | | SAP 대상2 | `SAP_2` | `SAP_2` |

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

에 로그인합니다 [!DNL SAP Subscription Billing] 계정을 찾은 다음 **[!UICONTROL 연락처]** 대상자 상태를 확인할 페이지입니다. 사용자 지정 참조에 대한 열을 표시하고 해당 대상 상태를 표시하도록 목록을 구성할 수 있습니다.
![대상자 이름 및 셀 대상자 상태를 표시하는 열 헤더가 있는 고객 개요 페이지를 표시하는 SAP 구독 청구 이미지](../../assets/catalog/ecommerce/sap-commerce/customer-overview.png)

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 오류 및 문제 해결 {#errors-and-troubleshooting}

다음을 참조하십시오. [[!DNL SAP Subscription Billing] 오류 유형](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/1a6a0dd6129c48e8b235190a1b5409fa.html) 가능한 오류 유형 및 해당 응답 코드 목록에 대한 설명서 페이지입니다.

## 추가 리소스 {#additional-resources}

에서 제공하는 추가 유용한 정보 [!DNL SAP] 설명서는 아래에 있습니다.
* [온보드 SAP 구독 청구](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/e4b8badf7d124026991e4ab6b57d2a33.html)

### 변경 로그

이 섹션에서는 이 대상 커넥터에 대한 기능 및 중요 설명서 업데이트를 캡처합니다.

+++ 변경 로그 보기

| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2024년 1월 | 초기 릴리스 | 초기 대상 릴리스 및 설명서 게시. |

{style="table-layout:auto"}

+++
