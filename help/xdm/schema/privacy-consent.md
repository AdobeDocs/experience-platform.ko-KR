---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consent;Consent
title: 개인 정보 혼합 개요
description: 개인 정보/마케팅 기본 설정(동의) 혼합은 CMP와 고객의 다른 소스에서 생성된 사용자 권한 및 기본 설정의 수집을 지원하기 위한 XDM(Experience Data Model) 혼합입니다. 이 문서에서는 믹싱에서 제공하는 다양한 필드의 구조와 용도에 대해 설명합니다.
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 1%

---


# [!DNL Privacy Consent] 믹싱 개요

이 [!DNL Privacy/Marketing Preferences (Consent)] 혼합(이하 &quot;[!DNL Privacy Consent] 믹신&quot;이라 한다)은 [!DNL Experience Data Model] (XDM) 믹스로서, CMP 및 기타 고객 소스에서 생성된 사용자 권한 및 선호도 모음을 지원하기 위한 것입니다. 이 문서에서는 믹싱에서 제공하는 다양한 필드의 구조와 용도에 대해 설명합니다.

## 전제 조건 {#prerequisites}

이 문서를 사용하려면 XDM [!DNL Experience Data Model] (Working Understanding)과 스키마를 사용해야 합니다 [!DNL Experience Platform]. 계속하기 전에 다음 문서를 검토하십시오.

* [XDM 시스템 개요](http://www.adobe.com/go/xdm-home-en)
* [스키마 컴포지션의 기본 사항](http://www.adobe.com/go/xdm-schema-best-practices-en)

## 스키마 예 {#schema}

>[!NOTE]
>
>아래 예제는 믹싱을 통해 전송되는 데이터의 구조를 보여 주기 위한 것으로, 이 문서의 다음 섹션에 컨텍스트를 제공함으로써 믹싱에서 제공하는 주요 필드를 설명합니다. [!DNL Platform] [!DNL Privacy Consent] 스키마 구조의 전체 예는 참조 목적으로 [부록에](#full-schema) 있습니다.

다음 JSON은 혼합이 처리할 수 있는 데이터 유형의 예를 [!DNL Privacy Consent] 보여줍니다. 이러한 각 필드의 특정 사용에 대한 정보는 다음 섹션에 제공됩니다.

```json
{
  "xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ],
  "xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  },
  "xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  },
  "xdm:version": "1.0.0",
  "xdm:timestamp": "2019-01-01T15:52:25+00:00",
  "xdm:userLocale": "UK",
  "xdm:localeSource": "ip"
}
```

## 필드 {#fields}

아래 섹션에서는 믹싱에서 제공하는 주요 필드 각각을 사용하는 방법과 하위 [!DNL Privacy Consent] 필드를 구성하는 방법을 다룹니다.

### xdm:privacyOptOut {#privacyOptOuts}

`xdm:privacyOptOuts` 고객이 선택한 일반적인 옵트아웃 설정을 나타내는 배열입니다. 이 배열에 여러 개의 객체를 포함할 수 있으며 각 객체는 특정 옵트아웃 유형과 고객이 해당 유형에 대해 선택한 기본 설정을 나타냅니다.

```json
"xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ]
```

| 속성 | 설명 |
| --- | --- |
| `xdm:optOutType` | 옵트아웃 유형. 허용되는 값 및 정의는 [부록을](#optOutType-values) 참조하십시오. |
| `xdm:optOutValue` | 이 특정 옵트아웃 유형에 대해 고객이 선택한 기본 설정 허용되는 값 및 정의는 [부록을](#choice-optOutValue-values) 참조하십시오. |
| `xdm:timestamp` | 해당되는 경우 옵트아웃 기본 설정이 변경된 시점의 ISO 8601 타임스탬프 |
| `xdm:basisOfProcessing` | 데이터를 수집 및 처리해야 하는 개인 정보 관련 기준을 나타냅니다. 기본적으로 이 필드는 로 설정되어 `consent`있으며, 이것은 사용자가 동의(반영된 것과 같이)를 제공한 경우에만 데이터가 처리되어야 함을 `xdm:optOutValue`나타냅니다.<br><br>일부 상황에서, 고객에게 데이터 처리에 대한 동의 여부를 묻는 메시지가 나타나지 않습니다. `xdm:basisOfProcessing` 이러한 경우 동의 메시지가 제공되지 않은 이유를 나타내는 옵트아웃 개체에 포함되어야 합니다. 허용되는 값 및 정의는 [부록을](#basisOfProcessing-values) 참조하십시오. |

### xdm:personalizationPreferences {#personalizationPreferences}

`xdm:personalizationPreferences` 개인화에 데이터를 사용할 수 있는 방법에 대한 고객 선호도를 캡처합니다. 사용자는 특정 개인화 사용 사례를 옵트아웃하거나 개인화를 완전히 거부할 수 있습니다.

>[!IMPORTANT]
>
>`xdm:personalizationPreferences` 은 마케팅 사례를 포함하지 않습니다. 예를 들어 고객이 이메일에 대한 개인화를 거부하는 경우 이메일 수신을 중단하지 않습니다. 대신, 고객이 받는 이메일은 프로필을 기반으로 하지 않고 일반적입니다.
>
>동일한 예를 들어, 고객이 이메일 마케팅( `xdm:marketingPreferences`다음 섹션에 [](#marketingPreferences)설명되어 있음)을 중단하면 이메일 개인화가 허용되더라도 해당 고객은 어떠한 이메일도 받지 않게 됩니다.

```json
"xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  }
```

| 속성 | 설명 |
| --- | --- |
| `xdm:default` | 이 개체에 제공된 데이터는 개인화에 대한 고객의 전체 선호도를 나타냅니다. |
| `xdm:details` | 고객이 선호하는 각 특정 개인화 유형에 대한 일련의 객체입니다. |
| `xdm:choice` | 개인화에 대한 고객 제공 동의 기본 설정 또는 개인화에 대한 특정 개인 설정(각 `xdm:default` 에 따라 제공되는지 또는 제공되는지에 따라 `xdm:details`다름) 허용되는 값 및 정의는 [부록을](#choice-optOutValue-values) 참조하십시오. |
| `xdm:type` | 스토리지 시스템의 개체는 `xdm:details` 고객이 동의 데이터를 제공하는 특정 개인화 사용 사례를 나타내기 위해 이 필드를 제공해야 합니다. 허용되는 값 및 정의는 [부록을](#type-values) 참조하십시오. |
| `xdm:timestamp` | 해당되는 경우 옵트아웃 기본 설정이 변경된 시점의 ISO 8601 타임스탬프 |
| `xdm:basisOfProcessing` | 데이터를 수집 및 처리해야 하는 개인 정보 관련 기준을 나타냅니다. 기본적으로 이 필드는 로 설정되어 `consent`있으며, 이것은 사용자가 동의(반영된 것과 같이)를 제공한 경우에만 데이터가 처리되어야 함을 `xdm:choice`나타냅니다.<br><br>일부 상황에서 고객에게 개인화에 대한 동의 여부를 묻는 메시지가 나타나지 않습니다. `xdm:basisOfProcessing` 이러한 경우 동의 메시지가 제공되지 않은 이유를 나타내는 옵트아웃 개체에 포함되어야 합니다. 허용되는 값 및 정의는 [부록을](#basisOfProcessing-values) 참조하십시오. |


### xdm:marketingPreferences {#marketingPreferences}

`xdm:marketingPreferences` 데이터를 사용할 수 있는 마케팅 용도에 대한 고객 기본 설정을 캡처합니다. 사용자는 특정 마케팅 사용 사례를 옵트아웃하거나 다이렉트 마케팅을 완전히 거부할 수 있습니다.

```json
"xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  }
```

| 속성 | 설명 |
| --- | --- |
| `xdm:default` | 이 개체에 제공된 데이터는 전체 다이렉트 마케팅을 위한 고객의 기본 설정을 나타냅니다. |
| `xdm:details` | 고객이 기본 설정을 제공한 각 특정 마케팅 사용 사례에 대해 하나씩, 일련의 개체입니다. |
| `xdm:choice` | 일반적으로 마케팅에 대한 고객 제공 동의 기본 설정 또는 마케팅 사용 사례의 경우, 각각 `xdm:default` 또는 `xdm:details`에 따라 제공됩니다. 허용되는 값 및 정의는 [부록을](#choice-optOutValue-values) 참조하십시오. |
| `xdm:subscriptions` | 메일링 목록 또는 뉴스레터와 같이, 키가 회사별 구독을 나타내는 개체입니다. 각 구독 객체에는 해당 구독에 대한 `xdm:choice` 값이 포함되어 있어야 합니다. |
| `xdm:type` | 이 `xdm:details` 배열의 개체는 고객이 동의 데이터를 제공하는 특정 마케팅 사용 사례를 나타내기 위해 이 필드를 제공해야 합니다. 허용되는 값 및 정의는 [부록을](#type-values) 참조하십시오. |
| `xdm:timestamp` | 해당되는 경우 옵트아웃 기본 설정이 변경된 시점의 ISO 8601 타임스탬프 |
| `xdm:basisOfProcessing` | 데이터를 수집 및 처리해야 하는 개인 정보 관련 기준을 나타냅니다. 기본적으로 이 필드는 로 설정되어 `consent`있으며, 이것은 사용자가 동의(반영된 것과 같이)를 제공한 경우에만 데이터가 처리되어야 함을 `xdm:choice`나타냅니다.<br><br>어떤 상황에서는 고객에게 다이렉트 마케팅에 대한 동의를 요청하지 않습니다. `xdm:basisOfProcessing` 이러한 경우 동의 메시지가 제공되지 않은 이유를 나타내는 옵트아웃 개체에 포함되어야 합니다. 허용되는 값 및 정의는 [부록을](#basisOfProcessing-values) 참조하십시오. |

## 믹싱을 사용한 동의 데이터 수집 {#ingest}

고객의 동의 데이터를 수집하기 위해 [!DNL Privacy Consent] 혼합을 사용하려면 새 스키마나 기존 스키마에 혼합을 추가하고 해당 스키마를 기반으로 데이터 세트를 만들어야 합니다.

스키마에 혼합을 추가하는 방법에 대한 단계는 UI [에서](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) 스키마를 만드는 방법에 대한 자습서를 참조하십시오. 이[!DNL  Privacy Consent] 혼합은 클래스 또는 [!DNL XDM Individual Profile] 를 기준으로 스키마와 호환됩니다 [!DNL XDM ExperienceEvent].

혼합이 포함된 스키마를 만든 후 데이터 세트 사용자 안내서 [!DNL Privacy Consent] 에서 데이터 [세트](../../catalog/datasets/user-guide.md#create) 를 만드는 단계에 따라 데이터 세트 사용자 안내서의 데이터 세트생성 섹션을 참조하십시오.

>[!IMPORTANT]
>
>동의 데이터를 보내려는 경우 [!DNL Real-time Customer Profile]혼합이 포함된 클래스를 기반으로 [!DNL Profile]사용 가능한 스키마를 만들어야 [!DNL XDM Individual Profile] [!DNL Privacy Consent] 합니다. 해당 스키마를 기반으로 만드는 데이터 집합도 활성화해야 합니다 [!DNL Profile]. 요구 사항과 관련된 특정 단계는 위의 자습서를 [!DNL Real-time Customer Profile] 참조하십시오.

## 부록 {#appendix}

아래 섹션에서는 혼합과 관련된 추가 참조 정보를 [!DNL Privacy Consent] 제공합니다.

### xdm:optOutType에 허용된 값 {#optOutType-values}

다음 표에서는 `xdm:optOutType`

| 값 | 설명 |
| --- | --- |
| `general_opt_out` | 데이터는 어떤 목적으로도 사용할 수 없습니다. 일반적으로 처리 기준이 &quot;동의&quot;가 아닌 경우를 제외하고 데이터 수집을 차단합니다.<br><br>이 옵트아웃 유형을 사용하는 경우 허용된 값 `in` 이 다음 컨텍스트 의미를 `out` 얻습니다.<ul><li>`in`:사용자 **는 데이터를 일반 처리에 사용하는 것에 대한 동의를** 제공했습니다.</li><li>`out`:사용자 **는 일반 처리에 사용되는 데이터에 동의하지** 않습니다.</li></ul>자세한 내용은 xdm:optOutValue의 [허용된 값에 대한](#choice-optOutValue-values) 표를 참조하십시오. |
| `anonymous_analysis` | 특정 페이지를 본 횟수와 같은 사용자 ID 유형이 필요하지 않은 일반 웹 지표에는 데이터를 사용할 수 없습니다. |
| `device_linking` | 방문자가 사용하는 한 장치의 데이터는 동일한 방문자가 사용하는 다른 장치의 데이터와 결합할 수 없습니다. 장치는 일반적인 사용자 이름 또는 이메일 주소와 같은 기술을 사용하여 연결되며, Adobe 장치 협력 또는 개인 장치 그래프를 통하기도 합니다. |
| `pseudonymous_analysis` | 이 데이터는 사용자가 웹 사이트를 통해 선택하는 경로(폴아웃 보고서 등)를 식별하고 세션을 설정하고 속성을 부여하기 위해 익명의 ID가 필요한 Adobe Analytics이 제공하는 웹 지표에 사용할 수 없습니다. |
| `sales_sharing_opt_out` | 데이터를 판매 목적으로 사용하거나 제3자와 공유할 수 없습니다.<br><br>이 옵트아웃 유형을 사용하는 경우 허용된 값 `in` 이 다음 컨텍스트 의미를 `out` 얻습니다.<ul><li>`in`:사용자 **는 데이터를 판매와 공유 목적으로 사용하기 위해 동의했습니다** .</li><li>`out`:사용자는 판매 및 공유 목적으로 사용되는 데이터에 **동의하지** 않습니다.</li></ul>자세한 내용은 xdm:optOutValue의 [허용된 값에 대한](#choice-optOutValue-values) 표를 참조하십시오. |

### xdm:basisOfProcessing에 허용된 값 {#basisOfProcessing-values}

다음 표에서는 `xdm:basisOfProcessing`

| 값 | 설명 |
| --- | --- |
| `consent` **(기본값)** | 개인이 명시적 권한을 제공했다면 지정된 용도에 대한 데이터 수집이 허용됩니다. 다른 값이 제공되지 `xdm:basisOfProcessing` 않는 경우 이 값이 기본값입니다. <br><br>**중요**:에 대한 값 `xdm:choice` 과 `xdm:optOutValue` 는 를 로 설정한 경우에만 `xdm:basisOfProcessing` 적용됩니다 `consent`. 이 표에 나와 있는 다른 값 중 하나를 `xdm:basisOfProcessing` 대신 사용하는 경우 개인의 동의 선택은 무시됩니다. |
| `compliance` | 기업의 법적 책임을 충족하기 위해서는 특정 목적을 위한 데이터를 수집해야 합니다. |
| `contract` | 특정 목적을 위한 데이터 수집은 개인 사용자와 계약 의무를 충족해야 합니다. |
| `legitimate_interest` | 특정 목적을 위해 이러한 데이터를 수집 및 처리하는 합법적인 비즈니스 이익은 개인에게 미칠 수 있는 잠재적인 해악을 능가합니다. |
| `public_interest` | 특정 목적을 위한 자료의 수집은 공익상 또는 공권력의 행사에 필요한 것이다. |
| `vital_interest` | 특정 목적을 위한 데이터를 수집하여 개인의 중요한 이익을 보호해야 합니다. |

### xdm:choice 및 xdm:optOutValue에 허용된 값 {#choice-optOutValue-values}

다음 표에서는 및 `xdm:choice` 에 대해 허용된 값에 대해 대략적으로 설명합니다 `xdm:optOutValue`.

| 값 | 설명 |
| --- | --- |
| `pending` | 시스템은 고객으로부터 아직 동의 기호 정보를 받지 못했다. 동의를 얻는 동안 웹 사이트의 첫 페이지에 사용할 수 있습니다. 또한 명시적으로 제공되지 않고 동의를 &quot;가정함&quot;으로 나타낼 수도 있습니다. |
| `in` | 사용자가 동의 환경 설정을 선택했습니다. 다시 말해, 그들은 **문제의 동의 선호도에 의해 명시된 자료 사용에 동의를 한다** . |
| `out` | 사용자가 동의 기본 설정에서 선택 해제했습니다. 다시 말해, 그들은 문제의 동의 선호도에 의해 명시된 자료 사용에 동의하지 **않습니다** . |
| `not_applicable` | 문제의 동의 기본 설정은 고객에게 적용되지 않습니다. |
| `not_provided` | 고객이 동의 기호 정보를 제공하지 않았습니다. |
| `unknown` | 고객의 동의 기호 정보는 알 수 없습니다. |

### xdm:type에 허용된 값 {#type-values}

다음 표에서는 `xdm:type`

| 값 | 설명 |
| --- | --- |
| `ads` | 관련 없는 웹 사이트에서 볼 수 있는 광고. |
| `content` | 웹 사이트에 나타나는 콘텐츠 |
| `customer_support` | 고객 지원과 관련된 데이터 |
| `email` | 이메일 메시지. |
| `iot` | &quot;사물 인터넷&quot;(IoT)과 관련된 데이터. |
| `in_app_messages` | 인앱 메시지. |
| `in_home` | 집에서 보내는 메시지 |
| `in_store` | 인스토어 메시지 |
| `in_vehicle` | 차량 내 메시지 |
| `offers` | 특별 프로모션. |
| `phone_calls` | 전화 통화 상호 작용과 관련된 데이터 |
| `push_notifications` | 푸시 알림. |
| `sms` | SMS 메시지. |
| `social_media` | 소셜 미디어 컨텐츠 |
| `snail_mail` | 일반 우편 배달을 통해 발송된 메시지. |
| `third_party_content` | 관련 없는 엔티티가 제공하는 웹 사이트에 표시되는 컨텐츠 또는 아티클입니다. |
| `third_party_offers` | 관련 없는 법인으로부터 웹 사이트 광고 서비스에 표시되는 제안이나 광고. |

### 전체 [!DNL Privacy Consent] 스키마 {#full-schema}

다음 JSON은 스키마 레지스트리에 표시되는 전체 [!DNL Privacy Consent] 스키마를 나타냅니다.

```json
{
  "meta:license": [
    "Copyright 2019 Adobe Systems Incorporated. All rights reserved.",
    "This work is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license",
    "you may not use this file except in compliance with the License. You may obtain a copy",
    "of the License at https://creativecommons.org/licenses/by/4.0/"
  ],
  "$id": "https://ns.adobe.com/xdm/context/consent-preferences",
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Privacy/Marketing Preferences (Consent)",
  "description": "This schema captures privacy, personalization and marketing preferences (consents).",
  "type": "object",
  "meta:extensible": true,
  "meta:abstract": true,
  "definitions": {
    "consentValue": {
      "type": "string",
      "enum": [
        "not_provided",
        "pending",
        "in",
        "out",
        "unknown",
        "not_applicable"
      ],
      "meta:enum": {
        "not_provided": "Not provided",
        "pending": "Pending verification",
        "in": "Opt-in",
        "out": "Opt-out",
        "unknown": "Unknown",
        "not_applicable": "Not Applicable"
      }
    },
    "basisOfProcessing": {
      "title": "Basis Of Processing",
      "type": "string",
      "description": "Basis of Processing",
      "enum": [
        "consent",
        "legitimate_interest",
        "contract",
        "vital_interest",
        "compliance",
        "public_interest"
      ],
      "meta:enum": {
        "consent": "User Consent",
        "legitimate_interest": "Legitimate Interest",
        "contract": "Contract",
        "vital_interest": "Vital Interest of the Individual",
        "compliance": "Compliance with a Legal Obligation",
        "public_interest": "Public Interest"
      }
    },
    "timestamp": {
      "title": "Preference timestamp",
      "description": "Timestamp of this specific opt out or preference.",
      "type": "string",
      "format": "date-time"
    },
    "consent-preferences": {
      "properties": {
        "xdm:privacyOptOuts": {
          "title": "Privacy Preferences",
          "description": "Encapsulates data privacy preferences.",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "xdm:optOutType": {
                "title": "Opt-out type",
                "type": "string",
                "description": "The type of user permission.",
                "enum": [
                  "general_opt_out",
                  "sales_sharing_opt_out",
                  "anonymous_analysis",
                  "pseudonymous_analysis",
                  "device_linking"
                ],
                "meta:enum": {
                  "general_opt_out": "General opt-out",
                  "sales_sharing_opt_out": "Sales/sharing opt-out",
                  "anonymous_analysis": "Anonymous Analysis",
                  "pseudonymous_analysis": "Pseudonymous Analysis",
                  "device_linking": "Device Linking"
                }
              },
              "xdm:optOutValue": {
                "title": "Opt Out Value",
                "description": "The value of the specific opt out.",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          }
        },
        "xdm:personalizationPreferences": {
          "title": "Personalization Preferences",
          "description": "User's Personalization Preferences",
          "type": "object",
          "properties": {
            "xdm:default": {
              "title": "Global Personalization Preferences",
              "description": "User's Default Personalization Preference",
              "type": "object",
              "properties": {
                "xdm:choice": {
                  "title": "Default Personalization Preferences Value",
                  "description": "The default value for personalization",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            },
            "xdm:details": {
              "title": "Itemized Personalization Preferences",
              "description": "Preferences for specific types of personalization",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "meta:enum": {
                    "content": "Personalize Content",
                    "in_app": "Personalize In App Messages",
                    "offers": "Personalize Offers",
                    "email": "Personalize eMail",
                    "snail_mail": "Personalize Regular Mail",
                    "phone_calls": "Personalize Phone Calls",
                    "push_notifications": "Personalize Push Notifications",
                    "sms": "Personalize SMS",
                    "customer_support": "Personalize Customer Support",
                    "in_store": "Personalize In Store",
                    "in_vehicle": "Personalize In Vehicle",
                    "in_home": "Personalize In Home",
                    "iot": "Personalize IoT",
                    "social_media": "Personalize Social Media",
                    "third_party_offers": "Personalize Third-party Offers",
                    "third_party_content": "Personalize Third-party Content",
                    "ads": "Personalize My Business's Ads on Other Sites"
                  }
                },
                "xdm:choice": {
                  "title": "Personalization Preference Value",
                  "description": "The value for this specific personalization preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            }
          }
        }
      },
      "xdm:marketingPreferences": {
        "title": "Marketing Preferences",
        "description": "User's Direct Marketing Preferences",
        "type": "object",
        "properties": {
          "xdm:default": {
            "title": "Default Direct Marketing Preference",
            "description": "User's Default Marketing Preference",
            "type": "object",
            "properties": {
              "xdm:choice": {
                "title": "Default Marketing Preferences Value",
                "description": "The default value for direct marketing preferences",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          },
          "xdm:details": {
            "title": "Itemized Direct Marketing Preferences",
            "description": "Preferences for specific types of direct marketing",
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "xdm:type": {
                  "title": "Marketing Preference",
                  "type": "string",
                  "description": "The specific marketing preference.",
                  "enum": [
                    "email",
                    "push_notifications",
                    "in_app_messages",
                    "sms",
                    "phone_calls",
                    "snail_mail",
                    "in_vehicle_messages",
                    "in_home_messages",
                    "iot",
                    "social_media"
                  ],
                  "meta:enum": {
                    "email": "Receive eMail",
                    "push_notifications": "Receive Push Notifications",
                    "in_app_messages": "Receive In App Messages",
                    "sms": "Receive SMS",
                    "phone_calls": "Receive Phone Calls",
                    "snail_mail": "Receive Regular Mail",
                    "in_vehicle_messages": "Receive In Vehicle Messages",
                    "in_home_messages": "Receive In Home Messages",
                    "iot": "Receive IoT",
                    "social_media": "Receive Social Media Messages"
                  }
                },
                "xdm:choice": {
                  "title": "Marketing Preference Value",
                  "description": "The value for this specific marketing preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                },
                "xdm:subscriptions": {
                  "title": "Company-specific subscriptions",
                  "description": "Company-specific subscriptions, such as mailing lists or newsletters",
                  "type": "object",
                  "meta:xdmType": "map",
                  "additionalProperties": {
                    "xdm:choice": {
                      "title": "Marketing Preference Value",
                      "description": "The value for this specific marketing preference",
                      "$ref": "#/definitions/consentValue"
                    },
                    "xdm:timestamp": {
                      "$ref": "#/definitions/timestamp"
                    }
                  }
                }
              }
            }
          }
        }
      },
      "xdm:timestamp": {
        "title": "Consent Preferences timestamp",
        "description": "Timestamp of the complete set of user consent preferences.",
        "type": "string",
        "format": "date-time"
      },
      "xdm:version": {
        "title": "Preferences Version",
        "description": "Version of the Privacy Preferences Standard",
        "type": "string"
      },
      "xdm:userLocale": {
        "title": "User Locale",
        "description": "User location or jurisdiction that applies to the consents for this user",
        "type": "string"
      },
      "xdm:localeSource": {
        "title": "Locale Source",
        "description": "Method used to determine the user's locale",
        "enum": [
          "ip",
          "gps",
          "user_provided",
          "website_location",
          "inferred",
          "other"
        ],
        "meta:enum": {
          "ip": "IP Address",
          "gps": "Device GPS",
          "user_provided": "User Provided",
          "website_location": "Website eTDL",
          "inferred": "Inferred",
          "other": "Other"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
    },
    {
      "$ref": "#/definitions/consent-preferences"
    }
  ],
  "meta:status": "experimental"
}
```
