---
title: Reddit 전환 API 확장
description: Reddit Ads Conversions API 확장을 사용하여 타깃팅된 광고를 위해 Reddit Ads에 사용자 상호 작용 이벤트를 전송하는 방법에 대해 알아봅니다.
last-substantial-update: 2025-05-1
source-git-commit: 603cc86892f518852552eaa2fe1bdeaa296137cf
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# [!DNL Reddit] 전환 API 확장 개요

Reddit는 다양한 사용자 기반을 갖춘 소셜 미디어 플랫폼으로 특정 대상을 타깃팅하는 광고주에게 이상적입니다.

[[!DNL Reddit] 전환 API 확장](https://ads-api.reddit.com/docs/v2/#tag/Conversions-API)을(를) 사용하여 Adobe Experience Platform Edge Network에서 캡처한 사용자 상호 작용 이벤트를 [!DNL Reddit Ads]&#x200B;(으)로 보냅니다. 이 확장 프로그램을 사용하여 귀하의 브랜드가 3억 7,900만 명이 넘는 주간 활성 사용자의 대상에 도달하고 사용자 행동을 더 잘 이해하며 타깃팅된 광고를 실행할 수 있도록 지원하십시오.

이벤트 전달 [규칙](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules)에서 [!DNL Reddit] 전환 API 확장을 설치, 구성 및 사용하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 주요 이점 {#benefits}

Reddit 전환 API 확장을 사용하여 다음을 수행할 수 있습니다.

- **대상에게 연결**: [!DNL Reddit]에서 3억 7천 9백만 명의 주별 활성 사용자와 협력하십시오.
- **사용자 동작 분석**: 사용자 상호 작용 데이터를 활용하여 동작을 이해하고 캠페인을 최적화합니다.
- **타깃팅된 광고 게재**: Adobe Experience Platform에서 캡처된 사용자 상호 작용을 기반으로 개인화된 광고를 실행합니다.

## 전제 조건 {#prerequisites}

이 확장을 사용하려면 유효한 Reddit Ads 계정이 있어야 합니다. 아직 계정이 없는 경우 [[!DNL Reddit Ads] 등록 페이지](https://business.reddithelp.com/s/article/Create-and-manage-your-Reddit-Ads-account)&#x200B;(으)로 이동하여 등록하고 계정을 만드십시오. 계정을 설정한 후에는 [Ads API에 대한 액세스를 요청](https://www.redditforbusiness.com/api-partnership)합니다.

### 필요한 구성 세부 정보 수집 {#configuration-details}

Experience Platform을 [!DNL Reddit]에 연결하려면 다음 입력이 필요합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 픽셀 ID | Pixel ID는 [!DNL Reddit Ads] 계정과 연결된 고유 식별자입니다. 웹 사이트 또는 앱에서 사용자 상호 작용 및 전환 이벤트를 추적하는 데 사용됩니다. 픽셀 ID는 [!DNL Reddit Ads] [계정](https://ads.reddit.com/accounts)에서 찾을 수 있습니다. | 123456789012 |
| 전환 액세스 토큰 | [!DNL Reddit] 전환 액세스 토큰입니다. 지침은 [[!DNL Reddit] 전환 API](https://business.reddithelp.com/s/article/conversion-access-token) 문서를 참조하십시오. <br> **토큰이 만료되지 않으므로 이 프로세스를 한 번만 수행하면 됩니다.** | {YOUR_REDDIT_BEARER_TOKEN} |

## [!DNL Reddit] 확장 설치 및 구성 {#install-configure}

[!DNL Reddit] 전환 API 확장을 설치하고 구성하려면 다음 단계를 따르십시오.

1. Experience Platform 데이터 수집 UI의 왼쪽 탐색에서 [!UICONTROL 확장]을(를) 선택하여 [!UICONTROL 확장] 카탈로그에 액세스합니다. 그런 다음 [새 이벤트 전달 속성을 만들거나](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview#properties) 기존 속성을 선택하십시오.
2. 왼쪽 탐색 패널에서 **[!UICONTROL 확장]**(으)로 이동합니다. **[!UICONTROL 카탈로그]**&#x200B;를 선택한 다음 **[!DNL Reddit]** 확장을 선택하십시오.
   ![Reddit 확장이 강조 표시된 Adobe Experience Platform 확장 카탈로그입니다.](../../../images/extensions/server/reddit/reddit-extension.png)
3. 다음 구성 세부 정보를 제공합니다.
   - **픽셀 ID**: [!DNL Reddit Ads] 픽셀 ID를 입력하십시오.
   - **전환 액세스 토큰**: [!DNL Reddit Ads] 계정에서 생성된 토큰을 입력하고 완료되면 **[!UICONTROL 저장]**을 선택합니다.
     ![Pixel ID 및 전환 액세스 토큰에 대한 필드를 포함하여 Reddit Conversions API 확장에 대한 구성 세부 정보입니다.](../../../images/extensions/server/reddit/reddit-capi-details.png)

## 이벤트 전달 규칙 구성 {#config-rule}

데이터 요소를 설정한 후 이벤트 전달 규칙을 만들어 이벤트가 [!DNL Reddit Ads]&#x200B;(으)로 전송되는 시기와 방법을 결정합니다.

1. 이벤트 전달 속성의 **규칙**(으)로 이동하여 새 [규칙](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules)을 만듭니다.
2. **작업**&#x200B;에서 새 작업을 추가하고 확장을 **[!DNL Reddit CAPI]**(으)로 설정합니다.
3. **작업 유형**&#x200B;을(를) **이벤트 보내기**(으)로 설정합니다.
   ![확장 및 작업 유형 필드가 강조 표시된 Reddit 전환 API 확장에 대한 이벤트 전달 규칙 구성 인터페이스입니다.](../../../images/extensions/server/reddit/reddit-rule.png)
4. 아래 표와 같이 이벤트에 대한 추가 컨트롤을 구성합니다.

   | 필드 이름 | 설명 | 예 |
   | --- | --- | --- |
   | `Event Name` | 전환 이벤트의 이름을 지정합니다. | `Purchase` |
   | `Event Type` | [지원되는 Reddit 전환 이벤트](https://business.reddithelp.com/s/article/supported-conversion-events#supported-conversion-events) 또는 사용자 지정 이벤트 유형일 수 있는 이벤트 유형을 정의합니다. | `SignUp`, `MyCustomEvent` |
   | `Timestamp` | 이벤트 시간을 ISO 형식 또는 epoch 시간으로 제공합니다. | `2025-04-15T16:01:00.000Z`, `1744742460000` |
   | `Client Dedupe ID` | 중복 제거를 위한 고유 ID를 추가합니다. | `abc123` |
   | `Match Keys` | 속성에 대한 사용자 및 디바이스 식별자를 포함합니다. | `{"email":"hashed_email@example.com", "phone":"hashed_phone"}` |
   | `Value` | 이벤트의 통화 값을 지정합니다. | `99.99` |
   | `Currency Code` | 통화에 ISO-4217 형식을 사용합니다. | `USD` |
   | `Units Sold` | 구매한 품목의 수량을 입력합니다. | `3` |
   | `Country Code` | 이벤트가 발생한 국가를 지정합니다. | `US` |
   | `Data Processing Options` | LDU(제한된 데이터 사용)와 같은 개인 정보 보호 플래그를 추가합니다. | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |
   | `Consent` | 광고 데이터 사용에 대한 사용자 동의를 나타냅니다. | `true` |

5. **변경 내용 유지**&#x200B;를 선택하여 규칙을 저장합니다.

## 이벤트 메타데이터 {#event-metadata}

이벤트 메타데이터 및 사용자 데이터 필드에 대한 자세한 분류를 알아보려면 이 섹션을 읽고 이벤트 구성에 필요한 매개 변수와 선택적 매개 변수를 이해합니다. 표시되는 필드는 선택한 이벤트 유형에 따라 달라질 수 있습니다.

>[!NOTE]
>
>전환 이벤트에서 최상의 결과를 얻으려면 [동적 제품 광고](https://business.reddithelp.com/s/article/dynamic-product-ads)를 설정할 때 모든 필드를 채우십시오.

### 이벤트 메타데이터 필드

![Pixel ID 및 전환 액세스 토큰에 대한 필드를 포함하여 Reddit Conversions API 확장에 대한 구성 세부 정보입니다.](../../../images/extensions/server/reddit/reddit-event-metadata.png)

| 필드 이름 | 설명 | 예 |
| --- | --- | --- |
| `Conversion ID`(필수) | 중복 제거에 사용되는 전환 이벤트에 대한 고유 ID입니다. | `abc123` |
| `Item Count` | 전환 이벤트에 대한 총 항목 수입니다. | `6` |
| `Currency` | 값의 통화가 [ISO-4217](https://www.iso.org/iso-4217-currency-codes.html) 형식으로 제공됩니다. | `USD` |
| `Value` | 소수를 포함한 전환 이벤트의 총 통화 값입니다. | `1.23` |
| `Products` | 이벤트와 연계된 제품에 대한 세부 정보가 포함된 개체의 JSON 배열입니다. 각 개체는 최소한 `id`을(를) 포함해야 합니다. | `[{"id":"SKU123","name":"ProductName","category":"CategoryName"},{"id":"SKU456","name":"ProductName","category":"CategoryName"}]` |

### 사용자 데이터 필드

다음 매개 변수는 선택 사항이지만 권장됩니다.

| 필드 이름 | 설명 | 예 |
| --- | --- | --- |
| `Email`(적극 권장) | 해시되거나 해시되지 않은 사용자 이메일. | `example@email.com` |
| `External ID` | 해시되거나 해시되지 않은 광고주가 할당한 사용자 ID입니다. | `customer12345` |
| `UUID`(적극 권장) | 웹 사이트의 Reddit 픽셀에서 생성한 ID입니다. | `1677712978045.b8f7eb7d-b357-437b-8bd3-e1c8166c7132` |
| `IP Address`(적극 권장) | 사용자의 장치 IP 주소입니다. | `192.168.0.1` |
| `User Agent`(적극 권장) | 사용자가 사용하는 브라우저 또는 앱입니다. | `Chrome/98.0.4758.102` |
| `IDFA` | 광고주를 위한 해시되거나 해시되지 않은 Apple 식별자. | `8A2E4F6D-0852-4B2A-B9D5-79334DE14B16` |
| `AAID` | 해시되거나 해시되지 않은 Android Advertising ID. | `38400000-8cf0-11bd-b23e-10b96e40000d` |
| `Screen Width` | 사용자 디스플레이의 폭. | `1920` |
| `Screen Height` | 사용자 디스플레이의 높이입니다. | `1080` |
| `Data Processing Options`(JSON 형식) | 사용자 개인 정보 설정. 는 LDU 만 지원합니다 (제한된 데이터 사용). | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |

### 중요한 고려 사항

데이터를 [!DNL Reddit Ads]에 보내기 전에 확장 프로그램은 `Email`, `External ID`, `IDFA` 및 `AAID` 필드의 값을 해시하고 표준화합니다. [!DNL SHA-256]에서 이미 해시된 경우 확장 프로그램에서 이 값을 다시 해시하지 않습니다.

## 유효성 검사 및 배포 {#validate-deploy}

확장 및 규칙을 구성한 후 [[!DNL Reddit Ads] 이벤트 관리자](https://business.reddithelp.com/s/article/Events-Manager)에서 이벤트 데이터를 확인하여 통합의 유효성을 검사합니다. [MQS(Match Quality Score)](https://business.reddithelp.com/s/article/match-quality-score)을(를) 사용하여 신호 통합의 정확성과 안정성을 평가합니다.

[!DNL Reddit Ads]에 대한 자세한 내용은 [Reddit Ads 설명서](https://ads.reddit.com/)를 참조하십시오.

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 이제 [!DNL Reddit] 전환 API 확장을 구성하고 사용하는 방법을 이해할 수 있습니다. Adobe Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md) 또는 다음 리소스를 참조하십시오.

- [일치 키 공유](https://business.reddithelp.com/s/article/about-attribution-matching-signals) 및 [이벤트 메타데이터](https://business.reddithelp.com/s/article/about-event-metadata): 일치 키와 이벤트 메타데이터를 효과적으로 공유하는 방법을 이해합니다.
- [이벤트 중복 제거](https://business.reddithelp.com/s/article/event-deduplication): 이벤트를 중복 제거하여 정확한 이벤트 추적을 보장합니다.
- [전환 액세스 토큰을 만듭니다](https://business.reddithelp.com/helpcenter/s/article/conversion-access-token): 보안 API 인증을 위한 전환 액세스 토큰을 만드는 단계를 수행합니다.
