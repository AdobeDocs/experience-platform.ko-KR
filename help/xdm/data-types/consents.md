---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consent;Consent
title: 동의 및 기본 설정 데이터 유형
description: 개인 정보/마케팅 기본 설정(동의) 데이터 유형은 CMP(Consent Management Platforms) 및 기타 데이터 작업에서 생성된 고객 권한 및 기본 설정의 수집을 지원하기 위한 것입니다.
topic: guide
translation-type: tm+mt
source-git-commit: 1a4dd167ecd4f4f61ffe26af786b355e4561b30d
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 1%

---


# [!DNL Consents & Preferences] 데이터 유형

데이터 [!DNL Privacy/Marketing Preferences (Consent)] 유형(이하 &quot;데이터 유형&quot;이라[!DNL Consents & Preferences] 함)은 [!DNL Experience Data Model] (CMP(Consent Management Platform) 및 데이터 작업에서 생성된 기타 소스 및 고객의 권한 및 환경 설정을 수집하기 위한 XDM(Data Type)의 데이터 유형입니다.

이 문서에서는 [!DNL Consents & Preferences] 데이터 유형이 제공하는 필드의 구조와 용도에 대해 설명합니다.

## 전제 조건 {#prerequisites}

이 문서는 XDM에 대한 작업 이해와 스키마 사용을 필요로 합니다 [!DNL Experience Platform]. 계속하기 전에 다음 문서를 검토하십시오.

* [XDM 시스템 개요](http://www.adobe.com/go/xdm-home-en)
* [스키마 컴포지션의 기본 사항](http://www.adobe.com/go/xdm-schema-best-practices-en)

## 데이터 유형 구조 {#structure}

>[!IMPORTANT]
>
>데이터 유형은 [!DNL Consents & Preferences] 동의 및 기본 설정 관리 사용 사례를 포함하도록 설계되었습니다. 그 결과, 이 문서에서는 데이터 유형의 필드를 일반 용어로 사용하는 방법에 대해 설명하고 이러한 필드의 사용을 해석하는 방법에 대한 제안만 합니다. 조직에서 이러한 동의 및 환경 설정을 어떻게 해석하고 고객에게 제시하는 방법에 따라 데이터 유형의 구조를 정렬하려면 개인 정보 법률 팀과 상의하십시오.

데이터 [!DNL Consents & Preferences] 유형은 **동의** 및 **기본 설정** 정보를 캡처하는 데 사용되는 여러 필드를 제공합니다.

동의는 고객이 데이터의 사용 방법을 지정할 수 있는 옵션입니다. 대부분의 동의는 특정 방식으로 데이터를 사용하기 전에 승인을 받아야 하거나, 적극적 동의가 필요하지 않은 경우 해당 사용을 중지하기 위한 선택(수신 거부)이 있어야 한다는 점에서 법적 측면이 있습니다.

환경 설정은 고객이 브랜드에 대한 경험의 다양한 측면을 처리하는 방법을 지정할 수 있는 옵션입니다. 다음 두 카테고리 내에 속합니다.

* **개인화 환경 설정**:브랜드가 고객에게 제공하는 경험을 개인화하는 방법에 대한 기본 설정
* **마케팅 기본 설정**:브랜드가 다양한 채널을 통해 고객에게 연락할 수 있는지 여부에 대한 기본 설정

다음 JSON은 데이터 유형이 처리할 수 있는 데이터 유형의 예를 [!DNL Consents & Preferences] 보여줍니다. 이러한 각 필드의 특정 사용에 대한 정보는 다음 섹션에 제공됩니다.

```json
{
  "xdm:consents": {
    "xdm:collect": {
      "xdm:val": "y",
    },
    "xdm:adID": {
      "xdm:val": "VI"
    },
    "xdm:share": {
      "xdm:val": "y",
    },
    "xdm:personalize": {
      "xdm:any": {
        "xdm:val": "y",
      },
      "xdm:content": {
        "xdm:val": "y"
      }
    },
    "xdm:marketing": {
      "xdm:preferred": "email",
      "xdm:any": {
        "xdm:val": "u"
      },
      "xdm:push": {
        "xdm:val": "n",
        "xdm:reason": "Too Frequent",
        "xdm:time": "2019-01-01T15:52:25+00:00"
      }
    },
    "xdm:idSpecific": {
      "email": {
        "jdoe@example.com": {
          "xdm:marketing": {
            "xdm:email": {
              "xdm:val": "n"
            }
          }
        }
      }
    }
  },
  "xdm:metadata": {
    "xdm:time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>위의 예제는 데이터 유형을 [!DNL Platform] [!DNL Consents & Preferences] 통해 전송된 데이터의 구조를 설명하기 위한 것으로, 이 문서의 나머지 부분에 컨텍스트를 제공하여 데이터 유형이 제공하는 주요 필드를 설명합니다. 데이터 형식 구조에 대한 전체 스키마는 참조할 수 있도록 [부록에](#full-schema) 있습니다.

## xdm:동의 {#choices}

`xdm:consents` 고객의 동의 및 기본 설정을 설명하는 여러 필드가 포함되어 있습니다. 이러한 필드는 아래 하위 섹션에서 자세히 설명합니다.

```json
"xdm:consents": {
  "xdm:collect": {
    "xdm:val": "y",
  },
  "xdm:adID": {
    "xdm:val": "VI"
  },
  "xdm:share": {
    "xdm:val": "y",
  },
  "xdm:personalize": {
    "xdm:any": {
      "xdm:val": "y",
    },
    "xdm:content": {
      "xdm:val": "y"
    }
  },
  "xdm:marketing": {
    "xdm:preferred": "email",
    "xdm:any": {
      "xdm:val": "u"
    },
    "xdm:email": {
      "xdm:val": "n",
      "xdm:reason": "Too Frequent",
      "xdm:time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### xdm:collect

`xdm:collect` 데이터를 수집하기 위한 고객의 동의를 나타냅니다.

```json
"xdm:collect" : {
  "xdm:val": "y"
}
```

| 속성 | 설명 |
| --- | --- |
| `xdm:val` | 이 사용 사례에 대해 고객이 제공한 동의 선택 사항입니다. 허용되는 값 및 정의는 [부록을](#choice-values) 참조하십시오. |

### xdm:adID

`xdm:adID` 광고주 ID(IDFA 또는 GAID)를 사용하여 이 장치의 앱 간에 고객을 연결할 수 있는지 여부에 대한 고객의 동의를 나타냅니다.

```json
"xdm:adID" : {
  "xdm:val": "y"
}
```

| 속성 | 설명 |
| --- | --- |
| `xdm:val` | 이 사용 사례에 대해 고객이 제공한 동의 선택 사항입니다. 허용되는 값 및 정의는 [부록을](#choice-values) 참조하십시오. |

### xdm:공유

`xdm:share` 데이터를 제휴 또는 제3자와 공유(또는 판매)할 수 있는지 여부에 대한 고객의 동의를 나타냅니다.

```json
"xdm:share" : {
  "xdm:val": "y"
}
```

| 속성 | 설명 |
| --- | --- |
| `xdm:val` | 이 사용 사례에 대해 고객이 제공한 동의 선택 사항입니다. 허용되는 값 및 정의는 [부록을](#choice-values) 참조하십시오. |

### xdm:개인 설정 {#personalize}

`xdm:personalize` 개인화에 데이터를 사용할 수 있는 방법에 대한 고객 선호도를 캡처합니다. 고객은 특정 개인화 사용 사례를 거부하거나 개인화를 완전히 거부할 수 있습니다.

>[!IMPORTANT]
>
>`xdm:personalize` 은 마케팅 사례를 포함하지 않습니다. 예를 들어 고객이 모든 채널에 대한 개인화를 거부하는 경우 이러한 채널을 통해 커뮤니케이션의 수신을 중지해서는 안 됩니다. 대신, 받는 메시지는 프로필을 기반으로 하지 않고 일반적이어야 합니다.
>
>동일한 예를 들어, 고객이 모든 채널( `xdm:marketing`다음 섹션 [](#marketing)에서 설명)에 대해 직접 마케팅을 이용하지 않는 경우, 개인화가 허용된 경우에도 해당 고객은 어떠한 메시지도 받지 않아야 합니다.

```json
"xdm:personalize": {
  "xdm:content": {
    "xdm:val": "y",
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `xdm:content` | 웹 사이트 또는 애플리케이션에서 개인화된 컨텐츠에 대한 고객의 선호 사항을 나타냅니다. |
| `xdm:val` | 지정된 사용 사례에 대한 고객 제공 개인화 기본 설정. 고객에게 동의 요청을 받을 필요가 없는 경우, 이 필드의 값은 개인화를 수행해야 하는 기준을 나타내야 합니다. 허용되는 값 및 정의는 [부록을](#choice-values) 참조하십시오. |

### xdm:마케팅 {#marketing}

`xdm:marketing` 데이터를 사용할 수 있는 마케팅 용도에 대한 고객 기본 설정을 캡처합니다. 고객은 특정 마케팅 사례를 거부하거나 다이렉트 마케팅을 완전히 거부할 수 있습니다.

```json
"xdm:marketing": {
  "xdm:preferred": "email",
  "xdm:any": {
    "xdm:val": "u"
  },
  "xdm:email": {
    "xdm:val": "n",
    "xdm:reason": "Too Frequent"
  },
  "xdm:push": {
    "xdm:val": "y"
  },
  "xdm:sms": {
    "xdm:val": "y"
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `xdm:preferred` | 고객이 선호하는 통신 수신 채널을 나타냅니다. 허용된 값은 [부록을](#preferred-values) 참조하십시오. |
| `xdm:any` | 전체 다이렉트 마케팅을 위한 고객의 선호도를 나타냅니다. 이 필드에 제공된 동의 기본 설정은 아래에 제공된 추가 하위 필드로 대체되지 않는 한 마케팅 채널에 대한 &quot;기본&quot; 기본 설정으로 간주됩니다 `xdm:marketing`. 보다 세부적인 동의 옵션을 사용할 계획인 경우 이 필드를 제외하는 것이 좋습니다.<br><br>값이 로 설정된 경우 `n`더 구체적인 개인화 설정은 모두 무시됩니다. 값이 로 설정된 경우 `y`명시적으로 설정되지 않은 경우 모든 미세한 개인화 옵션도 `y`으로 취급해야 합니다 `n`. 값이 설정되지 않은 경우 각 개인화 옵션에 대한 값이 지정된 대로 적용되어야 합니다. |
| `xdm:email` | 고객이 이메일 메시지를 수신하기로 동의하는지 여부를 나타냅니다. |
| `xdm:push` | 고객이 푸시 알림 수신을 허용하는지 여부를 나타냅니다. |
| `xdm:sms` | 고객이 문자 메시지를 수신하기로 동의하는지 여부를 나타냅니다. |
| `xdm:val` | 지정된 사용 사례에 대해 고객이 제공한 환경 설정. 고객에게 동의 요청을 받을 필요가 없는 경우, 이 필드의 값은 마케팅 사용 사례의 기초가 되어야 합니다. 허용되는 값 및 정의는 [부록을](#choice-values) 참조하십시오. |
| `xdm:time` | 해당되는 경우 마케팅 기본 설정이 변경된 ISO 8601 타임스탬프 개별 기본 설정에 대한 타임스탬프가 아래에 제공된 타임스탬프와 동일하면 이 필드 `xdm:metadata`가 해당 기본 설정에 대해 설정되지 않습니다. |
| `xdm:reason` | 고객이 마케팅 사용 사례를 옵트아웃할 때 이 문자열 필드는 고객이 옵트아웃한 이유를 나타냅니다. |

### xdm:idSpecific

`xdm:idSpecific` 특정 동의 또는 기본 설정이 일반적으로 고객에게 적용되지 않지만 단일 장치 또는 ID로 제한될 때 사용할 수 있습니다. 예를 들어, 한 고객은 한 주소로 이메일을 받는 것을 거부할 수 있으며 다른 주소로 이메일을 보낼 수도 있습니다.

>[!IMPORTANT]
>
>채널 동의 및 기본 설정(즉, 외부에서 제공된 것 `xdm:consents` )은 해당 채널 내의 ID에 `xdm:idSpecific`적용됩니다. 따라서 모든 채널 수준의 동의 및 기본 설정은 등가 ID 또는 디바이스별 설정이 적용되는지 여부에 직접적인 영향을 줍니다.
>
>* 고객이 채널 수준에서 선택한 경우 이에 해당하는 동의 또는 환경 설정은 `xdm:idSpecific` 무시됩니다.
>* 채널 수준 동의 또는 기본 설정이 설정되지 않거나 고객이 선택한 경우 동의나 기본 설정이 `xdm:idSpecific` 적용됩니다.


개체의 각 키는 `xdm:idSpecific` Adobe Experience Platform ID 서비스에서 인식하는 특정 ID 네임스페이스를 나타냅니다. 고유한 사용자 정의 네임스페이스를 정의하여 서로 다른 식별자를 분류할 수 있지만, Identity Service가 제공하는 표준 네임스페이스 중 하나를 사용하여 실시간 고객 프로필의 저장소 크기를 줄이는 것이 좋습니다. ID 네임스페이스에 대한 자세한 내용은 ID 서비스 설명서의 [ID 네임스페이스 개요를](../../identity-service/namespaces.md) 참조하십시오.

각 네임스페이스 개체의 키는 고객이 기본설정을 지정한 고유한 ID 값을 나타냅니다. 각 ID 값에는 동일한 방식으로 형식이 지정된 전체 동의 및 환경 설정이 포함될 수 있습니다 `xdm:consents`.

```json
"xdm:idSpecific": {
  "email": {
    "jdoe@example.com": {
      "xdm:marketing": {
        "xdm:email": {
          "xdm:val": "n"
        }
      }
    }
  }
}
```

## xdm:메타데이터

`xdm:metadata` 고객의 동의 및 기본 설정에 대한 일반 메타데이터를 마지막으로 업데이트할 때마다 캡처합니다.

```json
"xdm:metadata": {
  "xdm:time": "2019-01-01T15:52:25+00:00",
}
```

| 속성 | 설명 |
| --- | --- |
| `xdm:time` | 고객의 동의 및 기본 설정이 마지막으로 업데이트된 타임스탬프 로드 및 복잡성을 줄이기 위해 타임스탬프를 개별 환경 설정에 적용하는 대신 이 필드를 사용할 수 있습니다. 개별 환경 설정에서 `xdm:time` 값을 제공하면 해당 특정 환경 설정에 대한 `xdm:metadata` 타임스탬프가 무시됩니다. |

## 데이터 유형을 사용하여 데이터 인제스트 {#ingest}

고객의 동의 데이터를 수집하기 위해 [!DNL Consents & Preferences] 데이터 형식을 사용하려면 해당 데이터 유형이 포함된 스키마를 기반으로 데이터 세트를 만들어야 합니다.

필드에 데이터 유형을 할당하는 [방법에 대한 단계는 UI에서](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) 스키마를 만드는 방법에 대한 자습서를 참조하십시오. 데이터 형식이 있는 필드가 포함된 스키마를 만들었으면 데이터 세트 사용자 안내서 [!DNL Consents & Preferences] 에서 데이터 세트 [](../../catalog/datasets/user-guide.md#create) 생성 섹션을 참조하고 기존 스키마를 사용하여 데이터 세트를 만드는 단계를 따릅니다.

>[!IMPORTANT]
>
>동의 데이터를 보내려는 경우 [!DNL Real-time Customer Profile]데이터 형식을 포함하는 [!DNL Profile]클래스를 기반으로 [!DNL XDM Individual Profile] 활성화된 스키마를 만들어야 [!DNL Consents & Preferences] 합니다. 해당 스키마를 기반으로 만드는 데이터 집합도 활성화해야 합니다 [!DNL Profile]. 스키마 및 데이터 세트에 대한 요구 사항과 관련된 특정 단계는 위에 링크된 자습서를 참조하십시오. [!DNL Real-time Customer Profile]
>
>또한, 고객 프로필을 올바로 업데이트하려면 병합 정책이 최신 동의 및 기본 설정 데이터가 포함된 데이터 세트에 우선 순위를 지정하도록 구성되어 있어야 합니다. See the overview on [merge policies](../../rtcdp/profile/merge-policies.md) for more information.

## 동의 및 선호도 변경 처리

고객이 웹 사이트에서 동의 또는 기본 설정을 변경할 경우 이러한 변경 사항을 수집하여 [Adobe Experience Platform 웹 SDK를 사용하여 즉시 적용해야 합니다](../../edge/consent/supporting-consent.md). 고객이 데이터 수집을 옵트아웃하는 경우 모든 데이터 수집은 즉시 중단되어야 합니다. 고객이 개인화를 거부하는 경우 다음 페이지에서 개인화가 존재하지 않아야 합니다.

## 부록 {#appendix}

아래 섹션에서는 [!DNL Consents & Preferences] 데이터 유형에 대한 추가 참조 정보를 제공합니다.

### xdm:val에 허용된 값 {#choice-values}

다음 표에서는 `xdm:val`

| 값 | Title | 설명 |
| --- | --- | --- |
| `y` | 예 | 고객이 동의 또는 선호에 동의한 경우 다시 말해, 그들은 문제의 동의 또는 선호도에 의해 표시된 대로 그들의 데이터의 사용에 **동의를 한다** . |
| `n` | 아니요 | 고객은 동의 또는 선호에 동의하지 않기로 결정했다. 다시 말해, 그들은 문제의 동의 또는 선호도에 의해 표시된 대로 그들의 데이터의 사용에 동의하지 **않습니다** . |
| `p` | 보류 중인 확인 | 시스템은 아직 최종 동의 또는 선호도 값을 받지 못했다. 이것은 2단계 확인이 필요한 동의의 일부로서 가장 자주 사용됩니다. 예를 들어, 고객이 이메일 수신을 거부하는 경우, 이메일 링크를 선택하여 이메일 주소가 올바른지 확인할 `p` 때까지 해당 동의를 설정합니다. 이때 동의를 다음으로 업데이트해야 합니다 `y`.<br><br>이 동의 또는 기본 설정이 두 가지 인증 프로세스를 사용하지 않는 경우, 고객이 아직 동의 프롬프트에 응답하지 않았다는 사실을 나타내기 위해 대신 이 `p` 선택 사항을 사용할 수 있습니다. 예를 들어 고객이 동의 프롬프트에 응답하기 전에 웹 사이트 `p` 의 첫 페이지에 값을 자동으로 설정할 수 있습니다. 명시적 동의가 필요하지 않은 관할 지역에서는 고객이 명시적으로 선택하지 않았음을 나타내는 데 사용할 수도 있습니다(즉, 동의로 간주됨). |
| `u` | 알 수 없음 | 고객의 동의 또는 선호도 정보는 알 수 없습니다. |
| `LI` | 합법적인 관심 | 특정 목적을 위해 이러한 데이터를 수집 및 처리하는 합법적인 비즈니스 이익은 개인에게 미칠 수 있는 잠재적인 해악을 능가합니다. |
| `CT` | 계약 | 특정 목적을 위한 데이터 수집은 개인 사용자와 계약 의무를 충족해야 합니다. |
| `CP` | 법적 의무 준수 | 기업의 법적 책임을 충족하기 위해서는 특정 목적을 위한 데이터를 수집해야 합니다. |
| `VI` | 개인의 중요한 관심 | 특정 목적을 위한 데이터를 수집하여 개인의 중요한 이익을 보호해야 합니다. |
| `PI` | 공익성 | 특정 목적을 위한 자료의 수집은 공익상 또는 공권력의 행사에 필요한 것이다. |

### xdm:preferred에 대해 허용된 값 {#preferred-values}

다음 표에서는 `xdm:preferred`

| 값 | 설명 |
| --- | --- |
| `email` | 이메일 메시지. |
| `push` | 푸시 알림. |
| `inApp` | 인앱 메시지. |
| `sms` | SMS 메시지. |
| `phone` | 전화 통화 상호 작용 |
| `phyMail` | 우편. |
| `inVehicle` | 차량 내 메시지 |
| `inHome` | 집에서 보내는 메시지 |
| `iot` | 사물(IoT) 메시지 인터넷 |
| `social` | 소셜 미디어 컨텐츠 |
| `other` | 표준 카테고리에 맞지 않는 채널. |
| `none` | 기본 채널 없음 |
| `unknown` | 기본 채널을 알 수 없습니다. |

### 전체 [!DNL Consents & Preferences] 스키마 {#full-schema}

데이터 유형에 대한 전체 스키마를 [!DNL Consents & Preferences] 보려면 [공식 XDM 저장소를 참조하십시오](https://github.com/adobe/xdm/blob/master/components/datatypes/consentpreferences.schema.json).