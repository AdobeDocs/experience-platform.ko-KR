---
keywords: Experience Platform;홈;Intelligent Services;인기 항목;지능형 서비스;Intelligent Service
solution: Experience Platform, Intelligent Services
title: Intelligent Services에서 사용할 데이터 준비
topic-legacy: Intelligent Services
description: Intelligent Services에서 마케팅 이벤트 데이터에서 통찰력을 검색하려면 데이터를 표준 구조로 의미상 보강하고 유지 관리해야 합니다. Intelligent Services는 이를 위해 XDM(Experience Data Model) 스키마를 사용합니다.
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: aa73f8f4175793e82d6324b7c59bdd44bf8d20f9
workflow-type: tm+mt
source-wordcount: '2766'
ht-degree: 0%

---

# [!DNL Intelligent Services]에서 사용할 데이터 준비

[!DNL Intelligent Services] 마케팅 이벤트 데이터에서 인사이트를 검색하려면 데이터를 의미상 보강하고 표준 구조로 유지해야 합니다. [!DNL Intelligent Services] xdm( [!DNL Experience Data Model] XDM) 스키마를 활용하여 이를 달성합니다. 특히 [!DNL Intelligent Services]에 사용되는 모든 데이터 세트는 CEE(Consumer ExperienceEvent) XDM 스키마를 따르거나 Adobe Analytics 커넥터를 사용해야 합니다. 또한 Customer AI는 Adobe Audience Manager 커넥터를 지원합니다.

이 문서에서는 마케팅 이벤트 데이터를 여러 채널에서 CEE 스키마에 매핑하는 방법에 대한 일반적인 지침을 제공하며, 스키마 내의 중요한 필드에 대한 정보를 간략하게 설명함으로써 데이터를 해당 구조에 효과적으로 매핑하는 방법을 결정하는 데 도움이 됩니다. Adobe Analytics 데이터를 사용할 계획이라면 [Adobe Analytics 데이터 준비](#analytics-data)에 대한 섹션을 확인하십시오. Adobe Audience Manager 데이터(Customer AI만 해당)를 사용할 계획이라면 [Adobe Audience Manager 데이터 준비](#AAM-data)에 대한 섹션을 참조하십시오.

## 데이터 요구 사항

[!DNL Intelligent Services] 만드는 목표에 따라 서로 다른 양의 이전 데이터가 필요합니다. 어떻든 **모든** [!DNL Intelligent Services]에 준비하는 데이터는 양수 및 음수 고객 여정 / 이벤트를 모두 포함해야 합니다. 음수 이벤트와 양수 이벤트를 모두 사용하면 모델 정밀도와 정확도가 향상됩니다.

예를 들어 고객 AI를 사용하여 제품 구매 성향을 예측하는 경우 고객 AI 모델에는 성공적인 구매 경로 예와 실패한 경로의 예가 모두 필요합니다. 모델 교육 동안 고객 AI는 구매로 이어지는 이벤트와 여정을 이해하려고 하기 때문입니다. 여기에는 장바구니에 항목을 추가할 때 여정을 중지한 개인 등 구매하지 않은 고객이 수행한 작업도 포함됩니다. 이러한 고객은 유사한 행동을 보일 수 있지만 고객 AI는 통찰력을 제공하고 더 높은 성향 점수를 생성하는 주요 차이점과 요소를 드릴다운할 수 있습니다. 마찬가지로, Attribution AI에 터치 포인트 효율성, 최고 전환 경로 및 터치 포인트 위치별 분류와 같은 지표를 표시하기 위해 이벤트 유형과 여정의 유형이 모두 필요합니다.

이전 데이터 요구 사항에 대한 자세한 예와 정보는 입력/출력 설명서의 [Customer AI](./customer-ai/input-output.md#data-requirements) 또는 [Attribution AI](./attribution-ai/input-output.md#data-requirements) 이전 데이터 요구 사항 섹션을 참조하십시오.

### 데이터 결합 지침

가능하면 공통 ID에서 사용자의 이벤트를 결합하는 것이 좋습니다. 예를 들어 10개의 이벤트에 대해 &quot;id1&quot;이 있는 사용자 데이터가 있을 수 있습니다. 나중에 동일한 사용자가 쿠키 ID를 삭제하여 다음 20개 이벤트에서 &quot;id2&quot;로 기록됩니다. id1과 id2가 동일한 사용자에게 해당한다는 것을 알고 있는 경우 가장 좋은 방법은 30개의 이벤트를 모두 공통 ID로 결합하는 것입니다.

불가능한 경우 모델 입력 데이터를 만들 때 각 이벤트 세트를 다른 사용자로 처리해야 합니다. 따라서 모델 교육 및 점수 책정 중에 최상의 결과를 얻을 수 있습니다.

## 워크플로우 요약

준비 프로세스는 데이터가 Adobe Experience Platform에 저장되는지 또는 외부에서 저장하는지에 따라 다릅니다. 이 섹션에서는 두 시나리오 중 하나에 따라 수행해야 하는 필요한 단계를 요약합니다.

### 외부 데이터 준비

데이터가 Experience Platform 외부에 저장되는 경우 데이터를 [소비자 ExperienceEvent 스키마](#cee-schema)의 필수 및 관련 필드에 매핑해야 합니다. 이 스키마를 사용자 정의 필드 그룹으로 강화하여 고객 데이터를 보다 효율적으로 캡처할 수 있습니다. 매핑되면 소비자 ExperienceEvent 스키마 및 [데이터를 Platform](../ingestion/home.md)에 수집하여 데이터 세트를 만들 수 있습니다. 그런 다음 [!DNL Intelligent Service] 구성 시 CEE 데이터 세트를 선택할 수 있습니다.

사용하려는 [!DNL Intelligent Service]에 따라 다른 필드가 필요할 수 있습니다. 사용 가능한 데이터가 있는 경우 필드에 데이터를 추가하는 것이 가장 좋습니다. 필수 필드에 대한 자세한 내용은 [Attribution AI](./attribution-ai/input-output.md) 또는 [Customer AI](./customer-ai/input-output.md) 입력 / 출력 안내서를 참조하십시오.

### Adobe Analytics 데이터 준비 {#analytics-data}

고객 AI 및 Attribution AI은 기본적으로 Adobe Analytics 데이터를 지원합니다. Adobe Analytics 데이터를 사용하려면 설명서에 요약된 단계에 따라 [Analytics 소스 커넥터](../sources/tutorials/ui/create/adobe-applications/analytics.md)를 설정합니다.

소스 커넥터에서 데이터를 Experience Platform으로 스트리밍하면 인스턴스 구성 중에 Adobe Analytics을 데이터 소스로 선택하고 데이터 세트를 선택할 수 있습니다. 모든 필수 스키마 필드 그룹과 개별 필드는 연결 설정 중에 자동으로 생성됩니다. 데이터 세트를 CEE 형식으로 ETL(추출, 변환, 로드)할 필요가 없습니다.

>[!IMPORTANT]
>
>Adobe Analytics 커넥터를 사용하면 데이터를 채우는 데 최대 4주가 소요됩니다. 최근 연결을 설정하는 경우 데이터 세트에 고객 또는 Attribution AI에 필요한 최소 데이터 길이가 있는지 확인해야 합니다. [Customer AI](./customer-ai/input-output.md#data-requirements) 또는 [Attribution AI](./attribution-ai/input-output.md#data-requirements)에서 이전 데이터 섹션을 검토하고 예측 목표에 충분한 데이터가 있는지 확인하십시오.

### Adobe Audience Manager 데이터 준비(Customer AI만 해당) {#AAM-data}

Customer AI는 기본적으로 Adobe Audience Manager 데이터를 지원합니다. Audience Manager 데이터를 사용하려면 설명서에 요약된 단계에 따라 [Audience Manager 소스 커넥터](../sources/tutorials/ui/create/adobe-applications/audience-manager.md)를 설정합니다.

소스 커넥터가 데이터를 Experience Platform으로 스트리밍하면 고객 AI 구성 중에 Adobe Audience Manager을 데이터 소스로 선택하고 데이터 세트를 선택할 수 있습니다. 모든 스키마 필드 그룹과 개별 필드는 연결 설정 중에 자동으로 생성됩니다. 데이터 세트를 CEE 형식으로 ETL(추출, 변환, 로드)할 필요가 없습니다.

>[!IMPORTANT]
>
>최근에 커넥터를 설정하는 경우 데이터 세트에 필요한 최소 데이터 길이가 있는지 확인해야 합니다. 고객 AI용 [입력/출력 설명서](./customer-ai/input-output.md)에서 이전 데이터 섹션을 검토하고 예측 목표에 충분한 데이터가 있는지 확인하십시오.

### [!DNL Experience Platform] 데이터 준비

데이터가 이미 [!DNL Platform]에 저장되고 Adobe Analytics 또는 Adobe Audience Manager(Customer AI 전용) 소스 커넥터를 통해 스트리밍되지 않는 경우 아래 단계를 따르십시오. CEE 스키마를 이해하는 것이 좋습니다.

1. [소비자 ExperienceEvent 스키마](#cee-schema)의 구조를 검토하고 데이터를 해당 필드에 매핑할 수 있는지 확인합니다.
2. 데이터를 직접 매핑하려면 Adobe 컨설팅 서비스에 문의하여 데이터를 스키마에 매핑하고 [!DNL Intelligent Services]에 수집하거나, [이 안내서에 나와 있는 단계를 따르십시오.](#mapping)

## CEE 스키마 이해 {#cee-schema}

소비자 경험 이벤트 스키마는 온라인 또는 오프라인 상거래 활동뿐만 아니라 디지털 마케팅 이벤트(웹 또는 모바일)와 관련된 개인의 동작을 설명합니다. 이 스키마는 의미상 잘 정의된 필드(열) 때문에 [!DNL Intelligent Services]에 사용해야 하며, 그렇지 않으면 데이터를 덜 명확하게 하는 알 수 없는 이름은 사용하지 않습니다.

모든 XDM ExperienceEvent 스키마와 마찬가지로 CEE 스키마는 시간 및 관련된 주체의 ID를 포함하여 이벤트(또는 이벤트 세트)가 발생한 경우 시스템의 시간 시리즈 기반 상태를 캡처합니다. 경험 이벤트는 발생한 내용에 대한 팩트 레코드이므로 변경할 수 없으며 집계 또는 해석 없이 발생한 사항을 나타냅니다.

[!DNL Intelligent Services] 이 스키마 내의 여러 주요 필드를 활용하여 마케팅 이벤트 데이터에서 인사이트를 생성하십시오. 이 모든 정보는 루트 수준에서 찾을 수 있고 필요한 하위 필드를 표시하도록 확장됩니다.

![](./images/data-preparation/schema-expansion.gif)

모든 XDM 스키마와 마찬가지로 CEE 스키마 필드 그룹은 확장 가능합니다. 즉, CEE 필드 그룹에 추가 필드를 추가할 수 있으며 필요한 경우 여러 스키마에 다양한 변형을 포함할 수 있습니다.

필드 그룹의 전체 예는 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)에서 찾을 수 있습니다. 또한 CEE 스키마를 준수하도록 데이터를 구조화할 수 있는 방법에 대한 예를 보려면 다음 [JSON 파일](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)을 보고 복사할 수 있습니다. 자신의 데이터를 스키마에 매핑하는 방법을 결정하려면 아래 섹션에 요약된 주요 필드에 대해 알고 있을 때 이러한 두 예를 모두 참조하십시오.

## 주요 필드

CEE 필드 그룹 내에는 [!DNL Intelligent Services] 이 유용한 인사이트를 생성하기 위해 사용해야 하는 몇 가지 주요 필드가 있습니다. 이 섹션에서는 이러한 필드의 사용 사례와 예상 데이터를 설명하고 추가 예제에 대한 참조 설명서에 대한 링크를 제공합니다.

### 필수 필드

모든 키 필드를 사용하는 것이 좋지만 [!DNL Intelligent Services]가 작동하려면 **필수**&#x200B;인 두 개의 필드가 있습니다.

* [기본 ID 필드](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel)  (Attribution AI에 대해서만 필수)

#### 기본 ID {#identity}

스키마에 있는 필드 중 하나를 기본 ID 필드로 설정해야 합니다. 이 필드를 통해 [!DNL Intelligent Services]은(는) 시계열 데이터의 각 인스턴스를 개별 사용자에게 연결할 수 있습니다.

데이터의 소스와 특성을 기반으로 기본 ID로 사용할 최상의 필드를 결정해야 합니다. ID 필드에는 필드에 값으로 필요한 ID 데이터의 유형을 나타내는 **ID 네임스페이스**&#x200B;가 포함되어야 합니다. 일부 유효한 네임스페이스 값은 다음과 같습니다.

* &quot;이메일&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(Adobe Audience Manager ID용)
* &quot;aaid&quot;(Adobe Analytics ID용)

기본 ID로 사용해야 하는 필드를 잘 모르는 경우 Adobe 컨설팅 서비스에 문의하여 최상의 솔루션을 선택하십시오. 기본 ID가 설정되지 않은 경우 Intelligent Service 애플리케이션은 다음 기본 동작을 사용합니다.

| 기본값 | Attribution AI | 고객 AI |
| --- | --- | --- |
| ID 열 | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| 네임스페이스 | AAID | ECID |

기본 ID를 설정하려면 **[!UICONTROL 스키마]** 탭에서 스키마로 이동하고 스키마 이름 하이퍼링크를 선택하여 **[!DNL Schema Editor]** 를 엽니다.

![스키마로 이동](./images/data-preparation/navigate_schema.png)

그런 다음 기본 ID로 사용할 필드로 이동하여 선택합니다. **[!UICONTROL 필드 속성]** 메뉴가 해당 필드에 대해 열립니다.

![필드를 선택합니다](./images/data-preparation/find_field.png)

**[!UICONTROL 필드 속성]** 메뉴에서 **[!UICONTROL ID]** 확인란을 찾을 때까지 아래로 스크롤합니다. 상자를 선택한 후 선택한 ID를 **[!UICONTROL 기본 ID]**&#x200B;로 설정하는 옵션이 나타납니다. 이 상자도 선택하십시오.

![확인란 선택](./images/data-preparation/set_primary_identity.png)

다음으로, 드롭다운의 사전 정의된 네임스페이스 목록에서 **[!UICONTROL ID 네임스페이스]**&#x200B;를 제공해야 합니다. 이 예에서는 Adobe Audience Manager ID `mcid.id`을 사용하고 있으므로 ECID 네임스페이스 가 선택됩니다. **[!UICONTROL 적용]**&#x200B;을 선택하여 업데이트를 확인한 다음 오른쪽 상단 모서리에서 **[!UICONTROL 저장]**&#x200B;을 선택하여 스키마 변경 사항을 저장합니다.

![변경 사항을 저장합니다](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

이 필드는 이벤트가 발생한 날짜/시간을 나타냅니다. 이 값은 ISO 8601 표준에 따라 문자열로 제공해야 합니다.

#### xdm:channel {#channel}

>[!NOTE]
>
>이 필드는 Attribution AI을 사용하는 경우에만 필수입니다.

이 필드는 ExperienceEvent와 관련된 마케팅 채널을 나타냅니다. 이 필드에는 채널 유형, 미디어 유형 및 위치 유형에 대한 정보가 포함되어 있습니다.

![](./images/data-preparation/channel.png)

**예제 스키마**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

`xdm:channel`에 필요한 각 하위 필드에 대한 전체 정보는 [경험 채널 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) 사양을 참조하십시오. 매핑 예는 ](#example-channels) 아래의 [표를 참조하십시오.

#### 채널 매핑 예 {#example-channels}

다음 표에서는 `xdm:channel` 스키마에 매핑되는 마케팅 채널의 몇 가지 예를 제공합니다.

| 채널 | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 유료 검색 | https:/<span>/ns.adobe.com/xdm/channel-types/search | 유료 | 클릭 수 |
| 소셜 - 마케팅 | https:/<span>/ns.adobe.com/xdm/channel-types/social | 언드 | 클릭 수 |
| 표시 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 유료 | 클릭 수 |
| 이메일 | https:/<span>/ns.adobe.com/xdm/channel-types/email | 유료 | 클릭 수 |
| 내부 레퍼러 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 소유 | 클릭 수 |
| 뷰스루 표시 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 유료 | 노출 횟수 |
| QR 코드 리디렉션 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 소유 | 클릭 수 |
| 모바일 | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | 소유 | 클릭 수 |

### 권장 필드

주요 필드의 나머지 부분은 이 섹션에 요약되어 있습니다. 이러한 필드가 반드시 [!DNL Intelligent Services]에 필요한 것은 아니지만 더 많은 통찰력을 얻으려면 가능한 한 많은 필드를 사용하는 것이 좋습니다.

#### xdm:productListItems

이 필드는 제품 SKU, 이름, 가격 및 수량을 포함하여 고객이 선택한 제품을 나타내는 항목의 배열입니다.

![](./images/data-preparation/productListItems.png)

**예제 스키마**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

`xdm:productListItems`에 필요한 각 하위 필드에 대한 전체 정보는 [상거래 세부 정보 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 사양을 참조하십시오.

#### xdm:commerce

이 필드에는 구매 발주 번호 및 결제 정보를 포함하여 ExperienceEvent에 대한 상거래 관련 정보가 포함되어 있습니다.

![](./images/data-preparation/commerce.png)

**예제 스키마**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

`xdm:commerce`에 필요한 각 하위 필드에 대한 전체 정보는 [상거래 세부 정보 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 사양을 참조하십시오.

#### xdm:웹

이 필드는 상호 작용, 페이지 세부 사항 및 레퍼러 등 ExperienceEvent와 관련된 웹 세부 사항을 나타냅니다.

![](./images/data-preparation/web.png)

**예제 스키마**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

`xdm:productListItems`에 필요한 각 하위 필드에 대한 전체 정보는 [ExperienceEvent 웹 세부 사항 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) 사양을 참조하십시오.

#### xdm:마케팅

이 필드에는 터치 포인트에서 활성 상태인 마케팅 활동과 관련된 정보가 포함되어 있습니다.

![](./images/data-preparation/marketing.png)

**예제 스키마**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

`xdm:productListItems`에 필요한 각 하위 필드에 대한 전체 정보는 [마케팅 섹션](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) 사양을 참조하십시오.

## 데이터 매핑 및 수집 {#mapping}

마케팅 이벤트 데이터를 CEE 스키마에 매핑할 수 있는지 확인한 후 다음 단계를 수행하여 [!DNL Intelligent Services]에 가져올 데이터를 결정합니다. [!DNL Intelligent Services]에 사용된 모든 내역 데이터는 4개월 데이터의 최소 시간 내에 전환 확인 기간으로 사용할 일 수를 포함해야 합니다.

전송할 데이터 범위를 결정한 후 Adobe 컨설팅 서비스에 문의하여 데이터를 스키마에 매핑하고 서비스에 수집하십시오.

[!DNL Adobe Experience Platform] 구독이 있고 데이터를 직접 매핑하고 수집하려면 아래 섹션에 설명된 단계를 따르십시오.

### Adobe Experience Platform 사용

>[!NOTE]
>
>아래 단계에서는 Experience Platform 가입을 요구합니다. 플랫폼에 액세스할 수 없는 경우 [다음 단계](#next-steps) 섹션으로 이동하십시오.

이 섹션에서는 자세한 단계를 위한 자습서 링크를 포함하여 [!DNL Intelligent Services]에서 사용할 Experience Platform에 데이터를 매핑하고 수집하는 워크플로우에 대해 간략하게 설명합니다.

#### CEE 스키마 및 데이터 세트 만들기

데이터 수집 준비를 시작할 준비가 되면 첫 번째 단계는 CEE 필드 그룹을 사용하는 새 XDM 스키마를 만드는 것입니다. 다음 자습서에서는 UI 또는 API에서 새 스키마를 만드는 프로세스를 안내합니다.

* [UI에서 스키마 만들기](../xdm/tutorials/create-schema-ui.md)
* [API에서 스키마 만들기](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>위의 자습서는 스키마를 생성하기 위한 일반 워크플로우를 따릅니다. 스키마에 대한 클래스를 선택할 때는 **XDM ExperienceEvent 클래스**&#x200B;를 사용해야 합니다. 이 클래스를 선택한 후 스키마에 CEE 필드 그룹을 추가할 수 있습니다.

스키마에 CEE 필드 그룹을 추가한 후 데이터 내의 추가 필드에 필요에 따라 다른 필드 그룹을 추가할 수 있습니다.

스키마를 만들고 저장하면 해당 스키마를 기반으로 새 데이터 세트를 만들 수 있습니다. 다음 자습서에서는 UI 또는 API에서 새 데이터 세트를 만드는 프로세스를 안내합니다.

* [UI에서 데이터 세트 만들기](../catalog/datasets/user-guide.md#create) (기존 스키마를 사용하기 위한 워크플로우를 따릅니다.)
* [API에서 데이터 세트 만들기](../catalog/datasets/create.md)

데이터 세트가 만들어지면 **[!UICONTROL 데이터 세트]** 작업 공간 내의 플랫폼 UI에서 찾을 수 있습니다.

![](images/data-preparation/dataset-location.png)

#### 데이터 세트에 ID 필드 추가

[!DNL Adobe Audience Manager], [!DNL Adobe Analytics] 또는 다른 외부 소스에서 데이터를 가져오는 경우 스키마 필드를 ID 필드로 설정하는 옵션이 제공됩니다. 스키마 필드를 ID 필드로 설정하려면 스키마를 생성하기 위해 [UI 자습서](../xdm/tutorials/create-schema-ui.md#identity-field) 또는 [API 자습서](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) 내에서 ID 필드 설정에 대한 섹션을 봅니다.

로컬 CSV 파일에서 데이터를 수집하는 경우 [데이터 매핑](#ingest)의 다음 섹션으로 건너뛸 수 있습니다.

#### 데이터 매핑 및 수집 {#ingest}

CEE 스키마 및 데이터 집합을 만든 후 데이터 테이블을 스키마에 매핑하고 해당 데이터를 플랫폼으로 수집할 수 있습니다. UI에서 이 작업을 수행하는 방법에 대한 단계는 [XDM 스키마에 CSV 파일 매핑](../ingestion/tutorials/map-a-csv-file.md)의 자습서를 참조하십시오. 자체 데이터를 사용하기 전에 다음 [샘플 JSON 파일](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)을 사용하여 수집 프로세스를 테스트할 수 있습니다.

데이터 세트를 채운 후에는 동일한 데이터 세트를 사용하여 추가 데이터 파일을 수집할 수 있습니다.

데이터가 지원되는 타사 애플리케이션에 저장되는 경우, [소스 커넥터](../sources/home.md)를 만들어 마케팅 이벤트 데이터를 실시간으로 [!DNL Platform]로 수집할 수도 있습니다.

## 다음 단계 {#next-steps}

이 문서에서는 [!DNL Intelligent Services]에 사용할 데이터를 준비하는 방법에 대한 일반적인 지침을 제공합니다. 사용 사례에 따라 추가 컨설팅이 필요한 경우 Adobe 컨설팅 지원 센터에 문의하십시오.

데이터 세트에 고객 경험 데이터를 성공적으로 채운 후에는 [!DNL Intelligent Services] 을 사용하여 인사이트를 생성할 수 있습니다. 시작하려면 다음 문서를 참조하십시오.

* [Attribution AI 개요](./attribution-ai/overview.md)
* [Customer AI 개요](./customer-ai/overview.md)
