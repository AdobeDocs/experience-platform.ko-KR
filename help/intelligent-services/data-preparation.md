---
keywords: Experience Platform;홈;지능형 서비스;인기 항목;지능형 서비스;지능형 서비스
solution: Experience Platform
title: Intelligent Services에서 사용할 데이터 준비
description: 인텔리전트 서비스가 마케팅 이벤트 데이터에서 통찰력을 발견하려면 데이터를 의미론적으로 보강하고 표준 구조로 유지 관리해야 합니다. Intelligent Services는 이를 위해 XDM(Experience Data Model) 스키마를 사용합니다.
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: 87a8ad253abb219662034652b5f8c4fabfa40484
workflow-type: tm+mt
source-wordcount: '2823'
ht-degree: 0%

---

# [!DNL Intelligent Services]에서 사용할 데이터 준비

[!DNL Intelligent Services]이(가) 마케팅 이벤트 데이터에서 통찰력을 발견하려면 데이터를 의미상 보강하고 표준 구조로 유지 관리해야 합니다. [!DNL Intelligent Services]은(는) [!DNL Experience Data Model](XDM) 스키마를 활용하여 이를 달성합니다. 특히 [!DNL Intelligent Services]에서 사용되는 모든 데이터 세트는 CEE(Consumer ExperienceEvent) XDM 스키마를 준수하거나 Adobe Analytics 커넥터를 사용해야 합니다. 또한 Customer AI는 Adobe Audience Manager 커넥터를 지원합니다.

이 문서에서는 여러 채널의 마케팅 이벤트 데이터를 CEE 스키마에 매핑하는 방법에 대한 일반적인 지침을 제공하며, 스키마 내의 중요한 필드에 대한 정보를 요약하여 데이터를 해당 구조에 효과적으로 매핑하는 방법을 결정합니다. Adobe Analytics 데이터를 사용할 계획이라면 [Adobe Analytics 데이터 준비](#analytics-data) 섹션을 참조하십시오. Adobe Audience Manager 데이터(Customer AI만 해당)를 사용할 계획이라면 [Audience Manager 데이터 준비 Adobe](#AAM-data) 섹션을 참조하십시오.

## 데이터 요구 사항

[!DNL Intelligent Services]에는 사용자가 만든 목표에 따라 다른 양의 내역 데이터가 필요합니다. 관계없이 **모두** [!DNL Intelligent Services]에 대해 준비하는 데이터에는 양수 및 음수 고객 여정/이벤트가 모두 포함되어야 합니다. 음수와 양수 이벤트가 모두 있으면 모델 정밀도와 정확도가 향상됩니다.

예를 들어, 고객 AI를 사용하여 제품 구매 성향을 예측하는 경우 고객 AI 모델은 성공적인 구매 경로의 예제와 실패한 경로의 예가 모두 필요합니다. 모델 교육 중에 고객 AI는 어떤 이벤트와 여정이 구매로 이어지는지 파악하기 위해 살펴보기 때문입니다. 여기에는 장바구니에 항목을 추가할 때 여정을 중단한 개인과 같이 구매하지 않은 고객이 수행한 작업도 포함됩니다. 이러한 고객은 유사한 행동을 보일 수 있지만, Customer AI는 통찰력을 제공하고 성향 점수를 높이는 주요 차이점과 요인을 드릴다운할 수 있습니다. 마찬가지로, 터치 포인트 효율성, 상위 전환 경로 및 터치 포인트 위치별 분류와 같은 지표를 표시하려면 Attribution AI에 두 유형의 이벤트와 여정이 모두 필요합니다.

이전 데이터 요구 사항에 대한 자세한 예제와 정보는 입력/출력 설명서의 [고객 AI](./customer-ai/data-requirements.md#data-requirements) 또는 [Attribution AI](./attribution-ai/input-output.md#data-requirements) 이전 데이터 요구 사항 섹션을 참조하십시오.

### 데이터 결합 지침

가능하면 공통 ID에 사용자 이벤트를 연결하는 것이 좋습니다. 예를 들어 10개의 이벤트에 걸쳐 &quot;id1&quot;인 사용자 데이터가 있을 수 있습니다. 나중에 동일한 사용자가 쿠키 id를 삭제하고 다음 20개의 이벤트에 걸쳐 &quot;id2&quot;로 기록됩니다. id1과 id2가 동일한 사용자에 해당한다는 것을 알고 있는 경우, 가장 좋은 방법은 30개의 모든 이벤트를 공통 id로 연결하는 것입니다.

불가능한 경우 모델 입력 데이터를 생성할 때 각 이벤트 세트를 다른 사용자로 처리해야 합니다. 이렇게 하면 모델 교육 및 채점 중에 최상의 결과를 얻을 수 있습니다.

## 워크플로우 요약

준비 프로세스는 데이터가 Adobe Experience Platform에 저장되는지 또는 외부에 저장되는지에 따라 달라집니다. 이 섹션에서는 시나리오 중 하나에 따라 수행해야 하는 필수 단계를 요약합니다.

### 외부 데이터 준비

데이터가 Experience Platform 외부에 저장된 경우 데이터를 [소비자 ExperienceEvent 스키마](#cee-schema)의 필수 및 관련 필드에 매핑해야 합니다. 이 스키마를 사용자 정의 필드 그룹으로 추가하여 고객 데이터를 더 잘 캡처할 수 있습니다. 매핑되면 소비자 ExperienceEvent 스키마를 사용하여 데이터 세트를 만들고 [데이터를 플랫폼으로 수집](../ingestion/home.md)할 수 있습니다. [!DNL Intelligent Service]을(를) 구성할 때 CEE 데이터 세트를 선택할 수 있습니다.

사용하려는 [!DNL Intelligent Service]에 따라 다른 필드가 필요할 수 있습니다. 데이터를 사용할 수 있는 경우 필드에 데이터를 추가하는 것이 좋습니다. 필수 필드에 대한 자세한 내용은 [Attribution AI](./attribution-ai/input-output.md) 또는 [고객 AI](./customer-ai/data-requirements.md) 데이터 요구 사항 안내서를 참조하십시오.

### Adobe Analytics 데이터 준비 {#analytics-data}

고객 AI 및 Attribution AI은 기본적으로 Adobe Analytics 데이터를 지원합니다. Adobe Analytics 데이터를 사용하려면 설명서에 설명된 단계에 따라 [Analytics 소스 커넥터](../sources/tutorials/ui/create/adobe-applications/analytics.md)를 설정하십시오.

소스 커넥터가 데이터를 Experience Platform으로 스트리밍하면 인스턴스 구성 중에 Adobe Analytics을 데이터 소스로 선택한 다음 데이터 세트를 선택할 수 있습니다. 모든 필수 스키마 필드 그룹 및 개별 필드는 연결 설정 중에 자동으로 생성됩니다. 데이터 세트를 CEE 형식으로 ETL(추출, 변환, 로드)할 필요가 없습니다.

Adobe Analytics 소스 커넥터를 통해 Adobe Experience Platform으로 전송되는 데이터와 Adobe Analytics 데이터를 비교하는 경우 몇 가지 불일치가 표시될 수 있습니다. Analytics Source 커넥터는 XDM(경험 데이터 모델) 스키마로 변환하는 동안 행을 삭제할 수 있습니다. 타임스탬프 누락, 개인 ID 누락, 유효하지 않거나 큰 개인 ID, 잘못된 분석 값 등을 포함하여 전체 행이 변환에 적합하지 않은 이유는 여러 가지가 있을 수 있습니다.

자세한 내용과 예를 보려면 [Adobe Analytics과 Customer Journey Analytics 데이터 비교](https://www.adobe.com/go/compare-aa-data-to-cja-data)에 대한 설명서를 참조하십시오. 이 문서는 귀하와 귀하의 팀이 데이터 무결성에 대한 우려로 방해받지 않고 Intelligent Services용 Adobe Experience Platform 데이터를 사용할 수 있도록 이러한 차이점을 진단하고 해결하는 데 도움이 되도록 설계되었습니다.

Adobe Experience Platform Query Services에서 channel.typeAtSource 쿼리별로 시작 타임스탬프와 종료 타임스탬프 사이의 다음 Total Records를 실행하여 마케팅 채널별 카운트를 찾습니다.

```SELECT channel.typeAtSource as typeAtSource,
       Count(_id) AS Records 
FROM  df_hotel
WHERE timestamp>=from_utc_timestamp('2021-05-15','UTC')
        AND timestamp<from_utc_timestamp('2022-01-10','UTC')
        AND timestamp IS NOT NULL
        AND enduserids._experience.aaid.id IS NOT NULL
GROUP BY channel.typeAtSource
```

>[!IMPORTANT]
>
>Adobe Analytics 커넥터는 데이터를 채우는 데 최대 4주가 소요됩니다. 최근 연결을 설정한 경우 데이터 세트에 고객 또는 Attribution AI에 필요한 최소 데이터 길이가 있는지 확인해야 합니다. [고객 AI](./customer-ai/data-requirements.md#data-requirements) 또는 [Attribution AI](./attribution-ai/input-output.md#data-requirements)의 내역 데이터 섹션을 검토하고 예측 목표에 적합한 데이터가 있는지 확인하십시오.

### Adobe Audience Manager 데이터 준비(고객 AI만 해당) {#AAM-data}

고객 AI는 기본적으로 Adobe Audience Manager 데이터를 지원합니다. Audience Manager 데이터를 사용하려면 설명서에 설명된 단계에 따라 [Audience Manager 원본 커넥터](../sources/tutorials/ui/create/adobe-applications/audience-manager.md)를 설정하십시오.

소스 커넥터가 데이터를 Experience Platform으로 스트리밍하면 고객 AI 구성 중에 Adobe Audience Manager을 데이터 소스로 선택한 다음 데이터 세트를 선택할 수 있습니다. 연결 설정 중에 모든 스키마 필드 그룹 및 개별 필드가 자동으로 생성됩니다. 데이터 세트를 CEE 형식으로 ETL(추출, 변환, 로드)할 필요가 없습니다.

>[!IMPORTANT]
>
>최근에 커넥터를 설정한 경우 데이터 세트에 필요한 최소 데이터 길이가 있는지 확인해야 합니다. 고객 AI에 대한 [입력/출력 설명서](./customer-ai/data-requirements.md)의 내역 데이터 섹션을 검토하고 예측 목표에 적합한 데이터가 있는지 확인하십시오.

### [!DNL Experience Platform] 데이터 준비

데이터가 이미 [!DNL Platform]에 저장되어 있고 Adobe Analytics 또는 Adobe Audience Manager(Customer AI만 해당) 소스 커넥터를 통해 스트리밍하지 않는 경우 아래 단계를 따르십시오. CEE 스키마를 이해하는 것이 좋습니다.

1. [소비자 경험 이벤트 스키마](#cee-schema)의 구조를 검토하고 데이터를 해당 필드에 매핑할 수 있는지 여부를 확인합니다.
2. Adobe Consulting 서비스에 문의하여 데이터를 스키마에 매핑하고 [!DNL Intelligent Services]에 수집하거나, 데이터를 직접 매핑하려면 [이 안내서의 단계를 따르세요](#mapping).

## CEE 스키마 이해 {#cee-schema}

Consumer ExperienceEvent 스키마는 디지털 마케팅 이벤트(웹 또는 모바일)뿐만 아니라 온라인 또는 오프라인 상거래 활동과 관련된 개인의 행동을 설명합니다. 이 스키마는 의미상 잘 정의된 필드(열) 때문에 [!DNL Intelligent Services]에 사용해야 합니다. 그렇지 않으면 데이터를 덜 명확하게 만드는 알 수 없는 이름을 사용하지 않습니다.

CEE 스키마는 모든 XDM ExperienceEvent 스키마와 마찬가지로 시점 및 관련 주체의 ID를 포함하여 이벤트(또는 이벤트 세트)가 발생한 경우 시스템의 시계열 기반 상태를 캡처합니다. 경험 이벤트는 발생한 사항에 대한 팩트 레코드이므로 변경할 수 없으며 집계나 해석 없이 발생한 사항을 나타냅니다.

[!DNL Intelligent Services]은(는) 이 스키마 내의 여러 키 필드를 활용하여 마케팅 이벤트 데이터에서 통찰력을 생성합니다. 이러한 통찰력은 모두 루트 수준에서 찾을 수 있으며, 필요한 하위 필드를 표시하도록 확장됩니다.

![](./images/data-preparation/schema-expansion.gif)

모든 XDM 스키마와 마찬가지로 CEE 스키마 필드 그룹은 확장 가능합니다. 즉, CEE 필드 그룹에 추가 필드를 추가할 수 있고, 필요한 경우 다른 변형을 여러 스키마에 포함할 수 있습니다.

필드 그룹의 전체 예는 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)에서 찾을 수 있습니다. 또한 CEE 스키마를 준수하도록 데이터를 구조화하는 방법의 예를 보려면 다음 [JSON 파일](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)을 보고 복사할 수 있습니다. 아래 섹션에 설명된 키 필드에 대해 학습할 때 이 두 예 모두를 참조하여 자신의 데이터를 스키마에 매핑하는 방법을 확인하십시오.

## 주요 필드

CEE 필드 그룹 내에는 [!DNL Intelligent Services]에서 유용한 통찰력을 생성하기 위해 사용해야 하는 몇 가지 키 필드가 있습니다. 이 섹션에서는 이러한 필드의 사용 사례와 예상 데이터에 대해 설명하고 추가 예를 위한 참조 설명서에 대한 링크를 제공합니다.

### 필수 필드

모든 키 필드를 사용하는 것이 좋지만 [!DNL Intelligent Services]이(가) 작동하려면 두 개의 필드가 **필수**&#x200B;입니다.

* [기본 ID 필드](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel)(Attribution AI 전용)

#### 기본 ID {#identity}

스키마의 필드 중 하나를 기본 ID 필드로 설정해야 합니다. 이 필드를 통해 [!DNL Intelligent Services]은(는) 각 시계열 데이터 인스턴스를 개별 사용자에게 연결할 수 있습니다.

데이터의 소스 및 특성을 기반으로 기본 ID로 사용할 최상의 필드를 결정해야 합니다. ID 필드에는 필드에 값으로 필요한 ID 데이터의 형식을 나타내는 **ID 네임스페이스**&#x200B;가 포함되어야 합니다. 일부 유효한 네임스페이스 값은 다음과 같습니다.

>[!NOTE]
>
>ECID(Experience Cloud ID)는 MCID라고도 하며 네임스페이스에서 계속 사용됩니다.

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(Adobe Audience Manager ID용)
* &quot;aaid&quot; (Adobe Analytics ID용)

기본 ID로 사용해야 하는 필드를 잘 모르는 경우 Adobe Consulting 서비스에 문의하여 최상의 솔루션을 확인하십시오. 기본 ID가 설정되지 않은 경우 Intelligent Service 응용 프로그램은 다음 기본 동작을 사용합니다.

| 기본 | 기여도 AI | 고객 AI |
| --- | --- | --- |
| ID 열 | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| 네임스페이스 | AAID | ECID |

기본 ID를 설정하려면 **[!UICONTROL 스키마]** 탭에서 스키마로 이동한 후 스키마 이름 하이퍼링크를 선택하여 **[!DNL Schema Editor]**&#x200B;을(를) 엽니다.

![스키마로 이동](./images/data-preparation/navigate_schema.png)

다음으로 기본 ID로 사용할 필드로 이동하여 선택합니다. 해당 필드에 대한 **[!UICONTROL 필드 속성]** 메뉴가 열립니다.

![필드 선택](./images/data-preparation/find_field.png)

**[!UICONTROL 필드 속성]** 메뉴에서 **[!UICONTROL ID]** 확인란이 발견될 때까지 아래로 스크롤합니다. 확인란을 선택하면 선택한 ID를 **[!UICONTROL 기본 ID]**(으)로 설정하는 옵션이 나타납니다. 이 상자도 선택하십시오.

![확인란 선택](./images/data-preparation/set_primary_identity.png)

그런 다음 드롭다운의 미리 정의된 네임스페이스 목록에서 **[!UICONTROL ID 네임스페이스]**&#x200B;를 제공해야 합니다. 이 예제에서는 Adobe Audience Manager ID `mcid.id`이(가) 사용되고 있으므로 ECID 네임스페이스가 선택됩니다. **[!UICONTROL 적용]**&#x200B;을 선택하여 업데이트를 확인한 다음 오른쪽 상단에서 **[!UICONTROL 저장]**&#x200B;을 선택하여 스키마에 변경 내용을 저장합니다.

![변경 내용 저장](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

이 필드는 이벤트가 발생한 날짜/시간을 나타냅니다. 이 값은 ISO 8601 표준에 따라 문자열로 제공해야 합니다.

#### xdm:channel {#channel}

>[!NOTE]
>
>이 필드는 Attribution AI 사용 시에만 필수입니다.

이 필드는 ExperienceEvent 와 관련된 마케팅 채널을 나타냅니다. 필드에는 채널 유형, 미디어 유형 및 위치 유형에 대한 정보가 포함됩니다.

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

`xdm:channel`의 각 필수 하위 필드에 대한 자세한 내용은 [경험 채널 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) 사양을 참조하십시오. 매핑의 예를 보려면 아래 [표](#example-channels)를 참조하십시오.

#### 채널 매핑 예 {#example-channels}

다음 표에서는 `xdm:channel` 스키마에 매핑된 마케팅 채널의 몇 가지 예를 제공합니다.

| 채널 | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 유료 검색 | https:/<span>/ns.adobe.com/xdm/channel-types/search | 유료 | 클릭수 |
| 소셜 - 마케팅 | https:/<span>/ns.adobe.com/xdm/채널 유형/social | 소득 | 클릭수 |
| 표시 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 유료 | 클릭수 |
| 이메일 | https:/<span>/ns.adobe.com/xdm/channel-types/email | 유료 | 클릭수 |
| 내부 레퍼러 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 소유 | 클릭수 |
| 뷰스루 표시 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 유료 | 노출 횟수 |
| QR 코드 리디렉션 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 소유 | 클릭수 |
| 모바일 | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | 소유 | 클릭수 |

### 추천 필드

나머지 키 필드는 이 섹션에 설명되어 있습니다. [!DNL Intelligent Services]이(가) 작동하는 데 이러한 필드가 반드시 필요한 것은 아니지만, 더 풍부한 통찰력을 얻기 위해 가능한 한 많은 필드를 사용하는 것이 좋습니다.

#### xdm:productListItems

이 필드는 제품 SKU, 이름, 가격 및 수량을 포함하여 고객이 선택한 제품을 나타내는 항목 배열입니다.

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

`xdm:productListItems`의 각 필수 하위 필드에 대한 자세한 내용은 [상거래 세부 정보 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 사양을 참조하십시오.

#### xdm:commerce

이 필드에는 구매 주문 번호 및 결제 정보를 포함하여 ExperienceEvent에 대한 상거래 관련 정보가 포함됩니다.

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

`xdm:commerce`의 각 필수 하위 필드에 대한 자세한 내용은 [상거래 세부 정보 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 사양을 참조하십시오.

#### xdm:web

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

`xdm:productListItems`의 각 필수 하위 필드에 대한 자세한 내용은 [ExperienceEvent 웹 세부 사항 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) 사양을 참조하십시오.

#### xdm:marketing

이 필드에는 터치포인트로 활성 상태인 마케팅 활동과 관련된 정보가 포함됩니다.

![](./images/data-preparation/marketing.png)

**예제 스키마**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

`xdm:productListItems`의 각 필수 하위 필드에 대한 자세한 내용은 [마케팅 스키마](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) 사양을 참조하십시오.

## 데이터 매핑 및 수집 {#mapping}

마케팅 이벤트 데이터를 CEE 스키마에 매핑할 수 있는지 여부를 확인했으면 다음 단계에서 [!DNL Intelligent Services]에 가져올 데이터를 결정합니다. [!DNL Intelligent Services]에 사용된 모든 내역 데이터는 4개월 데이터의 최소 시간 범위와 전환 확인 기간으로 의도된 일 수에 포함되어야 합니다.

전송하려는 데이터 범위를 결정한 후 Adobe Consulting 서비스에 문의하여 데이터를 스키마에 매핑하고 서비스에 수집하십시오.

[!DNL Adobe Experience Platform] 구독이 있고 직접 데이터를 매핑하고 수집하려는 경우 아래 섹션에 설명된 단계를 따르십시오.

### Adobe Experience Platform 사용

>[!NOTE]
>
>아래 단계는 Experience Platform에 대한 구독이 필요합니다. 플랫폼에 액세스할 수 없는 경우 [다음 단계](#next-steps) 섹션으로 건너뛰십시오.

이 섹션에서는 [!DNL Intelligent Services]에서 사용할 수 있도록 데이터를 Experience Platform에 매핑하고 수집하는 워크플로에 대해 간략하게 설명합니다. 여기에는 자세한 단계를 위한 자습서 링크가 포함되어 있습니다.

#### CEE 스키마 및 데이터 세트 만들기

수집을 위해 데이터 준비를 시작할 준비가 되면 첫 번째 단계는 CEE 필드 그룹을 사용하는 새 XDM 스키마를 만드는 것입니다. 다음 튜토리얼에서는 UI 또는 API에서 새 스키마를 만드는 프로세스를 설명합니다.

* [UI에서 스키마 만들기](../xdm/tutorials/create-schema-ui.md)
* [API에서 스키마 만들기](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>위의 튜토리얼은 스키마 만들기에 대한 일반적인 워크플로를 따릅니다. 스키마에 대한 클래스를 선택할 때는 **XDM ExperienceEvent 클래스**&#x200B;을(를) 사용해야 합니다. 이 클래스를 선택하면 CEE 필드 그룹을 스키마에 추가할 수 있습니다.

스키마에 CEE 필드 그룹을 추가한 후 데이터 내의 추가 필드에 필요에 따라 다른 필드 그룹을 추가할 수 있습니다.

스키마를 만들고 저장하면 해당 스키마를 기반으로 새 데이터 세트를 만들 수 있습니다. 다음 튜토리얼에서는 UI 또는 API에서 새 데이터 세트를 만드는 프로세스를 설명합니다.

* [UI에서 데이터 집합을 만듭니다](../catalog/datasets/user-guide.md#create)(기존 스키마를 사용하려면 워크플로를 따르세요)
* [API에서 데이터 세트 만들기](../catalog/datasets/create.md)

데이터 세트가 만들어지면 **[!UICONTROL 데이터 세트]** 작업 영역의 Platform UI에서 찾을 수 있습니다.

![](images/data-preparation/dataset-location.png)

#### 데이터 세트에 ID 필드 추가

[!DNL Adobe Audience Manager], [!DNL Adobe Analytics] 또는 다른 외부 소스에서 데이터를 가져오는 경우 스키마 필드를 ID 필드로 설정할 수 있습니다. 스키마 필드를 ID 필드로 설정하려면 스키마를 만들기 위한 [UI 튜토리얼](../xdm/tutorials/create-schema-ui.md#identity-field) 또는 [API 튜토리얼](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor)에서 ID 필드 설정에 대한 섹션을 확인하십시오.

로컬 CSV 파일에서 데이터를 수집하는 경우 [데이터 매핑 및 수집](#ingest)의 다음 섹션으로 건너뛸 수 있습니다.

#### 데이터 매핑 및 수집 {#ingest}

CEE 스키마 및 데이터 세트를 만든 후 데이터 테이블을 스키마에 매핑하고 해당 데이터를 Platform에 수집할 수 있습니다. UI에서 이 작업을 수행하는 방법에 대한 단계는 [XDM 스키마에 CSV 파일 매핑](../ingestion/tutorials/map-csv/overview.md)에 대한 자습서를 참조하십시오. 다음 [샘플 JSON 파일](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)을 사용하여 데이터를 사용하기 전에 수집 프로세스를 테스트할 수 있습니다.

데이터 세트가 채워지면 동일한 데이터 세트를 사용하여 추가 데이터 파일을 수집할 수 있습니다.

데이터가 지원되는 타사 애플리케이션에 저장되어 있는 경우 [소스 커넥터](../sources/home.md)를 만들어 마케팅 이벤트 데이터를 실시간으로 [!DNL Platform](으)로 수집하도록 선택할 수도 있습니다.

## 다음 단계 {#next-steps}

이 문서는 [!DNL Intelligent Services]에서 사용할 데이터를 준비하는 방법에 대한 일반적인 지침을 제공합니다. 사용 사례에 따라 추가 컨설팅이 필요한 경우 Adobe Consulting 지원 센터에 문의하십시오.

고객 경험 데이터로 데이터 세트를 성공적으로 채운 후에는 [!DNL Intelligent Services]을(를) 사용하여 인사이트를 생성할 수 있습니다. 시작하려면 다음 문서를 참조하십시오.

* [Attribution AI 개요](./attribution-ai/overview.md)
* [고객 AI 개요](./customer-ai/overview.md)
