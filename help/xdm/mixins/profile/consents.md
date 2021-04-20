---
solution: Experience Platform
title: 개인 정보/개인화/마케팅 기본 설정(동의) 혼합
topic: overview
description: 이 문서에서는 개인 정보/개인화/마케팅 기본 설정(동의) 믹싱에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: 8c5ab298bad69305358ae961ebaf7836a90a0eaa
workflow-type: tm+mt
source-wordcount: '2239'
ht-degree: 1%

---


# [!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] 믹싱

[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] (이하 &quot; [!DNL Privacy & Consents] 혼합물&quot;이라 한다)은 고객의 동의 및  [[!DNL XDM Individual Profile] 선호도 정보를 캡처하는 데 사용되는 ](../../classes/individual-profile.md)학급표준믹스이다.

>[!NOTE]
>
>이 믹스는 [!DNL XDM Individual Profile]과(와) 호환되므로 [!DNL XDM ExperienceEvent] 스키마에 사용할 수 없습니다. 사용자 경험 이벤트 스키마에 동의 및 기본 설정 데이터를 포함하려면 [사용자 지정 혼합](../../ui/resources/mixins.md#create)을 대신 사용하여 [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] 데이터 유형](../../data-types/consents.md)을 스키마에 추가합니다.

## 혼합 구조 {#structure}

>[!IMPORTANT]
>
>[!DNL Consents & Preferences] 혼합은 동의 및 기본 설정 관리 사용 사례 범위를 포함하도록 설계되었습니다. 따라서 이 문서에서는 믹스의 필드를 일반 용어로 사용하는 방법에 대해 설명하고 이러한 필드의 사용을 해석하는 방법에 대한 제안만 합니다. 귀하의 조직이 이러한 동의 및 선호 사항을 어떻게 해석하고 고객에게 이러한 선택 사항을 제시하는 방법에 따라 믹스의 구조를 정렬하려면 개인 정보 법률 팀과 상의하십시오.

[!DNL Consents & Preferences] 혼합은 **concepts** 및 **preference** 정보를 캡처하는 데 사용되는 여러 필드를 제공합니다.

동의는 고객이 데이터를 사용할 수 있는 방법을 지정할 수 있는 옵션입니다. 대부분의 동의는 법적 측면을 가지는데, 일부 사법관할 내에서는 데이터를 특정 방법으로 사용하기 전에 허가를 받아야 하거나, 적극적 동의가 요구되지 않는 경우 그러한 사용을 중지시킬(수신 거부) 옵션이 있어야 한다는 것입니다.

환경 설정은 고객이 브랜드에 대한 경험의 다양한 측면을 처리하는 방법을 지정할 수 있는 옵션입니다. 다음 두 카테고리 내에 있습니다.

* **개인화 환경 설정**:브랜드가 고객에게 전달된 경험을 개인화하는 방법에 대한 기본 설정
* **마케팅 기본 설정**:브랜드가 다양한 채널을 통해 고객에게 연락할 수 있는지 여부에 대한 기본 설정.

다음 스크린샷은 혼합 구조가 플랫폼 UI에서 어떻게 표시되는지 보여줍니다.

![](../../images/mixins/consent.png)

>[!TIP]
>
>XDM 리소스를 조회하고 플랫폼 UI에서 해당 구조를 검사하는 방법에 대한 자세한 내용은 [XDM 리소스](../../ui/explore.md)에 대한 가이드를 참조하십시오.

다음 JSON은 [!DNL Consents & Preferences] 믹싱이 처리할 수 있는 데이터 유형의 예를 보여줍니다. 이러한 각 필드의 특정 사용에 대한 정보는 다음 섹션에 제공됩니다.

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>Experience Platform에서 정의하는 모든 XDM 스키마에 대한 샘플 JSON 데이터를 생성하여 고객 동의 및 기본 설정 데이터를 매핑하는 방법을 시각화할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.
>
>* [UI에서 샘플 데이터 생성](../../ui/sample.md)
>* [API에서 샘플 데이터 생성](../../api/sample-data.md)


## 필드 사용 사례

이러한 각 필드에 대한 사용 방법은 아래 섹션에 있습니다.

### `collect`

`collect` 데이터를 수집하기 위한 고객의 동의를 나타냅니다.

```json
"collect" : {
  "val": "y"
}
```

| 속성 | 설명 |
| --- | --- |
| `val` | 이 사용 사례에 대해 고객이 제공한 동의 선택 사항입니다. 허용되는 값과 정의는 [부록](#choice-values)을 참조하십시오. |

### `share`

`share` 데이터를 제2자 또는 제3자와 공유(또는 판매)할 수 있는지 여부에 대한 고객의 동의를 나타냅니다.

```json
"share" : {
  "val": "y"
}
```

| 속성 | 설명 |
| --- | --- |
| `val` | 이 사용 사례에 대해 고객이 제공한 동의 선택 사항입니다. 허용되는 값과 정의는 [부록](#choice-values)을 참조하십시오. |

### `personalize` {#personalize}

`personalize` 개인화에 데이터를 사용할 수 있는 방법에 대한 고객 선호도를 캡처합니다. 고객은 특정 개인화 사용 사례를 배제하거나 개인화를 완전히 거부할 수 있습니다.

>[!IMPORTANT]
>
>`personalize` 는 마케팅 사례를 포함하지 않습니다. 예를 들어 고객이 모든 채널에 대한 개인화를 거부하는 경우 이러한 채널을 통해 커뮤니케이션의 수신을 중지해서는 안 됩니다. 대신, 받는 메시지는 프로필을 기반으로 하지 않고 일반적이어야 합니다.
>
>동일한 예를 들어 고객이 모든 채널([다음 섹션](#marketing)에 설명된 `marketing`을 통해)에 대한 직접 마케팅을 옵트아웃하는 경우 개인화가 허용되더라도 해당 고객은 어떠한 메시지도 받지 않아야 합니다.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `content` | 웹 사이트 또는 애플리케이션에서 개인화된 컨텐트에 대한 고객의 선호 사항을 나타냅니다. |
| `val` | 지정된 사용 사례에 대한 고객 제공 개인화 기본 설정입니다. 고객에게 동의 요청을 받을 필요가 없는 경우, 이 필드의 값은 개인화가 이루어져야 하는 기반을 나타내야 합니다. 허용되는 값과 정의는 [부록](#choice-values)을 참조하십시오. |

### `marketing` {#marketing}

`marketing` 데이터를 사용할 수 있는 마케팅 목적에 대한 고객 선호도를 캡처합니다. 고객은 특정 마케팅 사용 사례를 옵트아웃하거나 다이렉트 마케팅을 완전히 거부할 수 있습니다.

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `preferred` | 고객이 선호하는 통신 수신 채널을 나타냅니다. 허용되는 값은 [부록](#preferred-values)을 참조하십시오. |
| `any` | 다이렉트 마케팅을 전체적으로 선호하는 고객의 기호를 나타냅니다. 이 필드에 제공된 동의 환경 설정은 `marketing`에 제공된 추가 하위 필드로 대체되지 않는 한 모든 마케팅 채널에 대한 &quot;기본&quot; 환경 설정으로 간주됩니다. 더 세부적인 동의 옵션을 사용할 계획인 경우 이 필드를 제외하는 것이 좋습니다.<br><br>값을 로 설정하면 더  `n`구체적인 개인화 설정이 모두 무시됩니다. 값이 `y`으로 설정된 경우 명시적으로 `n`로 설정되지 않은 경우 모든 미세한 개인화 옵션도 `y`으로 취급해야 합니다. 값이 설정이 해제된 경우 각 개인화 옵션에 대한 값이 지정된 대로 적용됩니다. |
| `email` | 고객이 이메일 메시지를 수신하기로 동의하는지 여부를 나타냅니다. 또한 고객은 이 채널 내에서 개별 구독에 대한 환경 설정을 제공할 수 있습니다. 자세한 내용은 아래 [구독](#subscriptions)의 섹션을 참조하십시오. |
| `push` | 고객이 푸시 알림 수신을 허용하는지 여부를 나타냅니다. 또한 고객은 이 채널 내에서 개별 구독에 대한 환경 설정을 제공할 수 있습니다. 자세한 내용은 아래 [구독](#subscriptions)의 섹션을 참조하십시오. |
| `sms` | 고객이 문자 메시지를 수신하기로 동의하는지 여부를 나타냅니다. 또한 고객은 이 채널 내에서 개별 구독에 대한 환경 설정을 제공할 수 있습니다. 자세한 내용은 아래 [구독](#subscriptions)의 섹션을 참조하십시오. |
| `val` | 지정된 사용 사례에 대해 고객이 제공한 환경 설정. 고객에게 동의를 요청할 필요가 없는 경우, 이 필드의 값은 마케팅 사용 사례가 발생해야 하는 기반을 명시해야 합니다. 허용되는 값과 정의는 [부록](#choice-values)을 참조하십시오. |
| `time` | 해당되는 경우 마케팅 기본 설정이 변경된 시점의 ISO 8601 타임스탬프. 개별 환경 설정에 대한 타임스탬프가 `metadata`에 제공된 타임스탬프와 같은 경우 이 필드는 해당 기본 설정에 대해 설정되지 않습니다. |
| `reason` | 고객이 마케팅 사용 사례를 옵트아웃할 때 이 문자열 필드는 고객이 옵트아웃한 이유를 나타냅니다. |

#### `subscriptions` {#subscriptions}

`marketing` 개체의 `email`, `push` 및 `sms` 속성은 이러한 개별 채널에 대한 고객 구독을 나타낼 수 있습니다. 이 작업은 해당 마케팅 채널에 `subscriptions` 속성을 추가하여 수행됩니다.

```json
"marketing": {
  "email": {
    "val": "y",
    "subscriptions": {
      "daily-mail": {
        "val": "y",
        "type": "paid",
        "subscribers": {
          "john@xyz.com": {
            "time": "2019-01-01T15:52:25+00:00",
            "source": "website"
          }
        }
      },
      "shipped": {
        "val": "y",

        "subscribers": {
          "john@xyz.com": {
            "time": "2021-01-01T08:32:53+07:00",
            "source": "website"
          },
          "jane@xyz.com": {
            "time": "2020-02-03T07:54:21+07:00",
            "source": "call center",
          }
        }
      }
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `type` | 구독 유형입니다. 15자 이하일 경우 설명형 문자열일 수 있습니다. |
| `subscribers` | 특정 구독에 구독한 식별자 집합(예: 이메일 주소 또는 전화 번호)을 나타내는 선택적 맵 유형 필드입니다. 이 객체의 각 키는 해당 식별자를 나타내며 2개의 하위 속성을 포함합니다. <ul><li>`time`:해당되는 경우 ID가 가입된 시점의 ISO 8601 타임스탬프.</li><li>`source`:구독자가 생성한 소스입니다. 15자 이하일 경우 설명형 문자열일 수 있습니다.</li></ul> |


### `metadata`

`metadata` 마지막으로 업데이트될 때마다 고객의 동의 및 선호도에 대한 일반 메타데이터를 캡처합니다.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| 속성 | 설명 |
| --- | --- |
| `time` | 고객의 동의 및 기본 설정이 마지막으로 업데이트된 시간에 대한 ISO 8601 타임스탬프. 로드 및 복잡성을 줄이기 위해 이 필드를 개별 환경 설정에 타임스탬프를 적용하는 대신 사용할 수 있습니다. 개별 환경 설정 아래에 `time` 값을 제공하면 해당 특정 환경 설정에 대한 `metadata` 타임스탬프가 무시됩니다. |

### `idSpecific`

`idSpecific` 특정 동의 또는 기본 설정이 일반적으로 고객에게 적용되지 않지만 단일 장치 또는 ID로 제한되는 경우에 사용할 수 있습니다. 예를 들어, 고객은 한 주소로 이메일의 수신을 거부할 수 있으며 다른 주소로 이메일을 보낼 수도 있습니다.

>[!IMPORTANT]
>
>채널 수준의 동의 및 환경 설정(즉, `idSpecific` 외부의 `consents`에 제공된 것)은 해당 채널 내의 ID에 적용됩니다. 따라서 모든 채널 수준의 동의 및 기본 설정은 등가 ID 또는 디바이스별 설정이 적용되는지 여부에 직접적인 영향을 줍니다.
>
>* 고객이 채널 수준에서 선택한 경우 `idSpecific`에 명시된 동의 또는 기본 설정은 무시됩니다.
>* 채널 수준 동의 또는 기본 설정이 설정되지 않았거나 고객이 선택한 경우 `idSpecific`에 동의나 환경 설정이 적용됩니다.


`idSpecific` 개체의 각 키는 Adobe Experience Platform Identity Service에서 인식하는 특정 ID 네임스페이스를 나타냅니다. 고유한 사용자 정의 네임스페이스를 정의하여 서로 다른 식별자를 분류할 수 있지만, Identity Service에서 제공하는 표준 네임스페이스 중 하나를 사용하여 실시간 고객 프로필의 저장소 크기를 줄이는 것이 좋습니다. ID 네임스페이스에 대한 자세한 내용은 ID 서비스 문서의 [ID 네임스페이스 개요](../../../identity-service/namespaces.md)를 참조하십시오.

각 네임스페이스 객체의 키는 고객이 환경 설정을 지정한 고유한 ID 값을 나타냅니다. 각 ID 값에는 `consents`과 같은 방식으로 서식이 지정된 동의 및 기본 설정의 전체 세트가 포함될 수 있습니다.

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

`idSpecific` 섹션에 제공된 `marketing` 개체 내에서 `any` 및 `preferred` 필드는 지원되지 않습니다. 이러한 필드는 사용자 수준에서만 구성할 수 있습니다. 또한 `email`, `sms` 및 `push`에 대한 `idSpecific` 마케팅 기본 설정은 `subscriptions` 필드를 지원하지 않습니다.

또한 `idSpecific` 섹션에서만 제공할 수 있는 동의도 있습니다.`adID`. 이 필드는 아래 하위 섹션에 설명되어 있습니다.

#### `adID`

`adID` 동의는 광고주 ID(IDFA 또는 GAID)를 사용하여 이 장치의 앱 간에 고객을 연결할 수 있는지 여부에 대한 고객의 동의를 나타냅니다. 이 값은 `idSpecific` 섹션의 `ECID` ID 네임스페이스 아래에서만 구성할 수 있으며 다른 네임스페이스나 이 믹싱에 대한 사용자 수준에서 설정할 수 없습니다.

```json
"idSpecific": {
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
>
>Adobe Experience Platform Mobile SDK가 적절한 경우 자동으로 설정되므로 이 값을 직접 설정할 필요는 없습니다.

## {#ingest} 혼합을 사용하여 데이터 인제스트

고객의 동의 데이터를 인제스트하는 데 [!DNL Consents & Preferences] 조합을 사용하려면 해당 믹싱을 포함하는 스키마를 기반으로 데이터 세트를 만들어야 합니다.

필드에 혼합을 할당하는 방법에 대한 자세한 내용은 [UI](http://www.adobe.com/go/xdm-schema-editor-tutorial-en)에서 스키마 만들기에 대한 자습서를 참조하십시오. [!DNL Consents & Preferences] 혼합이 포함된 필드가 포함된 스키마를 만든 후 기존 스키마로 데이터 집합을 만드는 절차에 따라 데이터 집합 사용자 안내서의 [데이터 집합](../../../catalog/datasets/user-guide.md#create)에 있는 섹션을 참조하십시오.

>[!IMPORTANT]
>
>동의 데이터를 [!DNL Real-time Customer Profile]에 보내려면 [!DNL Consents & Preferences] 혼합이 포함된 [!DNL XDM Individual Profile] 클래스를 기반으로 [!DNL Profile] 사용 스키마를 만들어야 합니다. 해당 스키마를 기반으로 만드는 데이터 집합도 [!DNL Profile]에 대해 활성화되어 있어야 합니다. 스키마 및 데이터 집합에 대한 [!DNL Real-time Customer Profile] 요구 사항과 관련된 특정 단계는 위에 연결된 자습서를 참조하십시오.
>
>또한 고객 프로필을 올바로 업데이트하려면 병합 정책이 최신 동의 및 기본 설정 데이터가 포함된 데이터 세트에 우선 순위를 지정하도록 구성되어 있는지 확인해야 합니다. 자세한 내용은 [병합 정책](../../../rtcdp/profile/merge-policies.md)에 대한 개요를 참조하십시오.

## 동의 및 환경 설정 변경 처리

고객이 웹 사이트에서 동의 또는 기본 설정을 변경할 때 이러한 변경 사항을 수집하여 [Adobe Experience Platform 웹 SDK](../../../edge/consent/supporting-consent.md)를 사용하여 즉시 적용해야 합니다. 고객이 데이터 수집을 옵트아웃하는 경우 모든 데이터 수집은 즉시 중단되어야 합니다. 고객이 개인화를 거부하는 경우 다음 방문에서 개인화가 발생하지 않아야 합니다.

## 부록 {#appendix}

아래 섹션은 [!DNL Consents & Preferences] 혼합과 관련된 추가 참조 정보를 제공합니다.

### `val` {#choice-values}에 허용된 값

다음 표에서는 `val`에 대해 허용된 값에 대해 대략적으로 설명합니다.

| 값 | Title | 설명 |
| --- | --- | --- |
| `y` | 예 | 고객이 동의 또는 선호에 동의한 경우 즉, 해당 동의나 선호도에 의해 표시된 대로 **do**&#x200B;의 데이터 사용에 동의합니다. |
| `n` | 아니요 | 고객은 동의 또는 선호에 동의하지 않기로 결정했다. 즉, 해당 동의 또는 선호도에 의해 표시된 대로 **은(는) 해당 데이터의 사용에 동의하지 않습니다.** |
| `p` | 보류 중인 확인 | 이 시스템은 아직 최종 동의 또는 선호도 값을 받지 못했다. 이것은 2단계 확인이 필요한 동의의 일부로서 가장 자주 사용됩니다. 예를 들어 고객이 이메일 수신을 거부하는 경우, 해당 동의는 이메일 링크를 선택하여 올바른 이메일 주소를 제공했는지 확인할 때까지 `p`로 설정됩니다. 이 경우 동의는 `y`로 업데이트됩니다.<br><br>이 동의 또는 기본 설정이 2개의 확인 프로세스를 사용하지 않는 경우, 대신 고객이 아직 동의 프롬프트에 응답하지  `p` 않았음을 나타내는 옵션을 사용할 수 있습니다. 예를 들어 고객이 동의 프롬프트에 응답하기 전에 웹 사이트의 첫 페이지에서 값을 `p`으로 자동으로 설정할 수 있습니다. 명시적 동의가 필요하지 않은 관할 지역에서는 고객이 명시적으로 선택하지 않았음을 나타내기 위해 사용할 수도 있습니다(즉, 동의는 가정됨). |
| `u` | 알 수 없음 | 고객의 동의 또는 기호 정보를 알 수 없습니다. |
| `LI` | 합법적인 관심 | 특정 목적에 맞게 이 데이터를 수집 및 처리하는 합법적인 비즈니스 이익은 개인에게 미칠 수 있는 잠재적인 해를 초과합니다. |
| `CT` | 계약 | 특정 목적을 위해 데이터를 수집하려면 개인 사용자와 계약 의무를 충족해야 합니다. |
| `CP` | 법적 의무 준수 | 기업의 법적 책임을 충족하기 위해서는 특정 목적에 대한 데이터를 수집해야 합니다. |
| `VI` | 개인의 중요한 관심 | 특정 목적을 위해 데이터를 수집하여 개인의 중요한 이익을 보호해야 합니다. |
| `PI` | 공익 | 특정 목적을 위한 자료의 수집은 공익적 또는 공권력의 행사에 필요한 것이다. |

### `preferred` {#preferred-values}에 허용된 값

다음 표에서는 `preferred`에 대해 허용된 값에 대해 대략적으로 설명합니다.

| 값 | 설명 |
| --- | --- |
| `email` | 이메일 메시지. |
| `push` | 푸시 알림. |
| `inApp` | 인앱 메시지. |
| `sms` | SMS 메시지. |
| `phone` | 전화 통화 상호 작용 |
| `phyMail` | 실제 우편. |
| `inVehicle` | 차량 내 메시지 |
| `inHome` | 사내 메시지. |
| `iot` | 사물(IoT) 메시지 인터넷 |
| `social` | 소셜 미디어 컨텐츠. |
| `other` | 표준 카테고리에 맞지 않는 채널. |
| `none` | 기본 설정 채널 없음 |
| `unknown` | 기본 설정을 알 수 없습니다. |

### 전체 [!DNL Consents & Preferences] 스키마 {#full-schema}

[!DNL Consents & Preferences] 혼합에 대한 전체 스키마를 보려면 [공식 XDM 리포지토리](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json)를 참조하십시오.
