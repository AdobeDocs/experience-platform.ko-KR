---
solution: Experience Platform
title: 동의 및 환경 설정 스키마 필드 그룹
description: 이 문서에서는 동의 및 환경 설정 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# [!UICONTROL 동의 및 환경 설정] 필드 그룹

[!UICONTROL 동의 및 환경 설정] 는 의 표준 필드 그룹입니다. [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md) 개별 고객에 대한 동의 및 환경 설정 정보를 캡처합니다.

>[!NOTE]
>
>이 필드 그룹은 다음과만 호환됩니다. [!DNL XDM Individual Profile], 다음에 사용할 수 없음: [!DNL XDM ExperienceEvent] 스키마. 경험 이벤트 스키마에 동의 및 환경 설정 데이터를 포함하려면 [[!UICONTROL 개인 정보, 개인화 및 마케팅 환경 설정에 대한 동의] 데이터 유형](../../data-types/consents.md) 를 사용하여 스키마에 추가 [사용자 정의 필드 그룹](../../ui/resources/field-groups.md#create) 대신,

## 필드 그룹 구조 {#structure}

다음 [!UICONTROL 동의 및 환경 설정] 필드 그룹은 단일 개체 유형 필드를 제공합니다. `consents`을 클릭하여 동의 및 환경 설정 정보를 캡처합니다. 이 필드는 [[!UICONTROL 개인 정보, 개인화 및 마케팅 환경 설정에 대한 동의] 데이터 유형](../../data-types/consents.md), 제거 `adID` 필드 및 추가 `idSpecific` 맵 필드.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>다음 안내서를 참조하십시오 [xdm 리소스 살펴보기](../../ui/explore.md) 에서 모든 XDM 리소스를 조회하고 Platform UI에서 해당 구조를 검사하는 방법에 대한 절차를 확인할 수 있습니다.

다음 JSON은 [!UICONTROL 동의 및 환경 설정] 필드 그룹이 처리할 수 있습니다. 필드 그룹에서 제공하는 대부분의 필드를 사용하는 방법에 대한 자세한 내용은 [동의 및 환경 설정 데이터 유형](../../data-types/consents.md). 아래 하위 섹션에서는 필드 그룹이 데이터 유형에 추가하는 고유한 속성에 중점을 둡니다.

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
>Experience Platform에서 정의하는 모든 XDM 스키마에 대한 샘플 JSON 데이터를 생성하여 고객 동의 및 환경 설정 데이터가 매핑되는 방법을 시각화할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.
>
>* [UI에서 샘플 데이터 생성](../../ui/sample.md)
>* [API에서 샘플 데이터 생성](../../api/sample-data.md)


### `idSpecific`

`idSpecific` 특정 동의 또는 환경 설정이 고객에게 보편적으로 적용되지 않고 단일 장치 또는 ID로 제한된 경우 사용할 수 있습니다. 예를 들어 고객이 한 주소에 대한 이메일 수신을 거부하는 동시에 다른 주소에 대한 이메일을 허용할 수 있습니다.

>[!IMPORTANT]
>
>채널 수준 동의 및 환경 설정 (즉, 아래에 제공된 동의) `consents` 의 외부 `idSpecific`)는 해당 채널 내의 모든 ID에 적용됩니다. 따라서 모든 채널 수준 동의 및 환경 설정은 동등한 ID 또는 디바이스별 설정을 적용할지 여부에 직접 영향을 줍니다.
>
>* 고객이 채널 수준에서 옵트아웃한 경우 의 동등한 동의 또는 환경 설정 `idSpecific` 무시합니다.
>* 채널 수준 동의 또는 환경 설정이 되어 있지 않거나 고객이 옵트인한 경우 `idSpecific` 영광입니다.


의 각 키 `idSpecific` 개체는 Adobe Experience Platform ID 서비스에서 인식하는 특정 ID 네임스페이스를 나타냅니다. 사용자 정의 네임스페이스를 정의하여 다른 식별자를 분류할 수 있지만 Identity Service에서 제공하는 표준 네임스페이스 중 하나를 사용하여 실시간 고객 프로필의 스토리지 크기를 줄이는 것이 좋습니다. ID 네임스페이스에 대한 자세한 내용은 [id 네임스페이스 개요](../../../identity-service/namespaces.md) 을 참조하십시오.

각 네임스페이스 개체에 대한 키는 고객이 기본 설정으로 지정한 고유한 ID 값을 나타냅니다. 각 ID 값에는 와 동일한 방식으로 형식이 지정된 전체 동의 및 환경 설정 세트가 포함될 수 있습니다. `consents`.

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
  "ECID": {
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

다음 범위 내 `marketing` 에 제공된 개체 `idSpecific` 섹션, `any` 및 `preferred` 필드는 지원되지 않습니다. 이러한 필드는 사용자 수준에서만 구성할 수 있습니다. 또한 `idSpecific` 마케팅 환경 설정 `email`, `sms`, 및 `push` 지원 안 함 `subscriptions` 필드.

에만 제공할 수 있는 동의도 있습니다. `idSpecific` 섹션: `adID`. 이 필드는 아래 하위 섹션에 설명되어 있습니다.

#### `adID`

다음 `adID` 동의는 광고주 ID(IDFA 또는 GAID)를 사용하여 해당 디바이스의 앱에서 고객을 연결할 수 있는지 여부에 대한 고객의 동의를 나타냅니다. 이 값은 다음에만 구성할 수 있습니다. `ECID` 의 ID 네임스페이스 `idSpecific` 이 필드 그룹의 다른 네임스페이스에 대해 또는 사용자 수준에서 섹션 및 을(를) 설정할 수 없습니다.

```json
"idSpecific": {
  "ECID": {
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
>Adobe Experience Platform Mobile SDK는 적절할 때 이 값을 자동으로 설정하므로 이 값을 직접 설정할 필요는 없습니다.

## 필드 그룹을 사용하여 데이터 수집 {#ingest}

를 사용하려면 [!UICONTROL 동의 및 환경 설정] 필드 그룹 고객의 동의 데이터를 수집하려면 해당 필드 그룹을 포함하는 스키마를 기반으로 데이터 세트를 만들어야 합니다.

다음 튜토리얼 참조: [ui에서 스키마 만들기](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 필드에 필드 그룹을 할당하는 방법에 대한 단계입니다. 를 사용하는 필드가 포함된 스키마를 만든 경우 [!UICONTROL 동의 및 환경 설정] 필드 그룹은에서 섹션을 참조하십시오. [데이터 세트 만들기](../../../catalog/datasets/user-guide.md#create) 데이터 세트 사용 안내서에서 기존 스키마로 데이터 세트를 만드는 단계를 따릅니다.

>[!IMPORTANT]
>
>동의 데이터를 (으)로 전송하려는 경우 [!DNL Real-Time Customer Profile], 다음을 생성해야 합니다. [!DNL Profile]를 기반으로 한 스키마 활성화됨 [!DNL XDM Individual Profile] 을 포함하는 클래스 [!UICONTROL 동의 및 환경 설정] 필드 그룹입니다. 해당 스키마를 기반으로 하여 만드는 데이터 세트도 활성화해야 합니다. [!DNL Profile]. 관련된 특정 단계는 위에 연결된 튜토리얼을 참조하십시오 [!DNL Real-Time Customer Profile] 스키마 및 데이터 세트에 대한 요구 사항입니다.
>
>또한 고객 프로필을 올바르게 업데이트하려면 최신 동의 및 환경 설정 데이터가 포함된 데이터 세트의 우선 순위를 지정할 수 있도록 병합 정책이 구성되어 있는지 확인해야 합니다. 의 개요 보기 [병합 정책](../../../rtcdp/profile/merge-policies.md) 추가 정보.

## 동의 및 환경 설정 변경 처리

고객이 웹 사이트에서 동의 또는 환경 설정을 변경할 경우 이러한 변경 사항을 수집하여 를 사용하여 즉시 적용해야 합니다. [Adobe Experience Platform 웹 SDK](../../../edge/consent/supporting-consent.md). 고객이 데이터 수집을 옵트아웃하면 모든 데이터 수집을 즉시 중단해야 합니다. 고객이 개인화를 옵트아웃하는 경우 방문하는 다음 페이지에 개인화가 없어야 합니다.

## 다음 단계

이 문서에서는 의 구조와 사용에 대해 다룹니다. [!UICONTROL 동의 및 환경 설정] 필드 그룹입니다. 필드 그룹에서 제공하는 다른 필드에 대한 자세한 내용은 [[!UICONTROL 개인 정보, 개인화 및 마케팅 환경 설정에 대한 동의] 데이터 유형](../../data-types/consents.md).
