---
solution: Experience Platform
title: 구독 데이터 유형이 있는 일반 마케팅 기본 설정 필드
topic-legacy: overview
description: 이 문서에서는 구독 XDM 데이터 유형을 사용하는 일반 마케팅 기본 설정 필드에 대한 개요를 제공합니다.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 3%

---

# [!UICONTROL 구독, 데이터 유형이 ] 있는 일반 마케팅 기본 설정 필드

[!UICONTROL 구독이 있는 일반 마케팅 기본 ] 설정 필드는 특정 마케팅 기본 설정에 대한 고객의 선택을 설명하는 표준 XDM 데이터 유형을 나타냅니다.

>[!NOTE]
>
>이 데이터 유형은 [[!UICONTROL 동의 및 기본 설정] 필드 그룹](../field-groups/profile/consents.md)을 기준으로 사용하여 조직의 동의 스키마 구조를 사용자 지정하는 데 사용됩니다.
>
>특정 마케팅 기본 설정 필드에 `subscriptions` 맵이 필요하지 않으면 대신 [기본 마케팅 필드 데이터 유형](./marketing-field.md)을 사용할 수 있습니다.

![](../images/data-types/marketing-field-subscriptions.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `reason` | 문자열 | 고객이 마케팅 사용 사례를 옵트아웃하면 이 문자열 필드는 고객이 옵트아웃한 이유를 나타냅니다. |
| `subscriptions` | 맵 | 특정 가입에 대한 고객 마케팅 환경 설정 맵입니다. 자세한 내용은 [구독](#subscriptions)의 섹션을 참조하십시오. |
| `time` | DateTime | 마케팅 기본 설정이 변경된 경우 해당하는 ISO 8601 타임스탬프입니다. |
| `val` | 문자열 | 이 마케팅 사용 사례에 대해 고객이 제공한 환경 설정 선택입니다. 허용되는 값 및 정의는 [다음 섹션](#val)을 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

## `val` {#val}

다음 표에서는 `val`에 대해 허용되는 값에 대해 설명합니다.

| 값 | Title | 설명 |
| --- | --- | --- |
| `y` | 예 | 고객이 기본 설정을 선택했습니다. 즉, **은(는) 해당 기본 설정에서 지정한 대로 데이터 사용에 동의함을 의미합니다.** |
| `n` | 아니요 | 고객이 선호하는 항목을 선택하지 않았습니다. 즉, **은(는) 해당 기본 설정에서 지정한 대로 데이터 사용에 동의하지 않습니다.** |
| `p` | 검증 보류 중 | 시스템에 최종 기본 설정 값이 아직 수신되지 않았습니다. 이는 2단계 검증이 필요한 동의의 일부로서 가장 많이 사용됩니다. 예를 들어 고객이 이메일 수신을 거부하는 경우, 해당 동의는 이메일의 링크를 선택하여 올바른 이메일 주소를 제공했는지 확인할 때까지 `p`로 설정되며, 이때 동의가 `y`로 업데이트됩니다.<br><br>이 기본 설정에서 두 개의 확인 프로세스를 사용하지 않는 경우 대신  `p` 선택한 항목을 사용하여 고객이 아직 동의 프롬프트에 응답하지 않았음을 나타낼 수 있습니다. 예를 들어 고객이 동의 프롬프트에 응답하기 전에 웹 사이트의 첫 페이지에서 값을 `p` 로 자동으로 설정할 수 있습니다. 명시적인 동의가 필요하지 않은 관할권에서 고객이 명시적으로 옵트아웃하지 않았음을 나타내기 위해 사용할 수도 있습니다(즉, 동의가 가정됨). |
| `u` | 알 수 없음 | 고객의 선호도 정보를 알 수 없습니다. |
| `LI` | 합법적인 관심 | 지정된 용도로 이 데이터를 수집하고 처리하는 합법적인 비즈니스 이익은 개인에게 발생할 수 있는 잠재적인 피해를 가중시킵니다. |
| `CT` | 계약 | 지정된 목적으로 데이터를 수집하려면 개인과 계약 의무를 충족해야 합니다. |
| `CP` | 법적 의무 준수 | 지정된 목적으로 데이터를 수집하려면 비즈니스의 법적 의무를 충족해야 합니다. |
| `VI` | 개인의 중요한 관심 | 특정 목적을 위한 데이터 수집은 개인의 중요한 이익을 보호하기 위해 필요합니다. |
| `PI` | 공용 관심 | 특정 목적을 위한 자료의 수집은 공익상 또는 공권력의 행사에 따라 수행되어야 한다. |

{style=&quot;table-layout:auto&quot;}

## `subscriptions` {#subscriptions}

일부 기업에서는 고객이 특정 마케팅 채널과 연관된 서로 다른 가입을 선택할 수 있습니다. 예를 들어, 은행에서는 고객이 초과 인출된 계정에 대해 전화 경고를 가입하거나 충성도 프로그램 오퍼에 대한 판매 호출을 받을 수 있도록 할 수 있습니다.

다음 JSON은 `subscriptions` 맵이 포함된 전화 통화 마케팅 채널에 대한 예제 마케팅 필드를 나타냅니다. `subscriptions` 개체의 각 키는 마케팅 채널에 대한 개별 구독을 나타냅니다. 따라서 각 구독에는 옵트인 값(`val`)이 포함되어 있습니다.

```json
"phone-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "subscribers": {
        "123-555-0928": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "overdrawn-account": {
      "val": "y",
      "type": "issues",
      "subscribers": {
        "123-555-0928": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "301-555-1527": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `type` | 구독 유형입니다. 15자 이내인 경우 어떤 수사적 문자열일 수 있습니다. |
| `subscribers` | 특정 구독을 구독한 식별자 세트(예: 이메일 주소 또는 전화 번호)를 나타내는 선택적 맵 유형 필드입니다. 이 개체의 각 키는 해당 식별자를 나타내며 두 개의 하위 속성을 포함합니다. <ul><li>`time`: ID가 구독한 시간의 ISO 8601 타임스탬프입니다(해당하는 경우).</li><li>`source`: 구독자가 시작한 원본입니다. 15자 이내인 경우 어떤 수사적 문자열일 수 있습니다.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 추가 리소스

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
