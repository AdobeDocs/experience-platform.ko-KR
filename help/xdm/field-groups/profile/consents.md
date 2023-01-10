---
solution: Experience Platform
title: 동의 및 기본 설정 스키마 필드 그룹
description: 이 문서에서는 동의 및 기본 설정 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# [!UICONTROL 동의 및 기본 설정] 필드 그룹

[!UICONTROL 동의 및 기본 설정] 는 의 표준 필드 그룹입니다. [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md) 은(는) 개별 고객에 대한 동의 및 기본 설정 정보를 캡처합니다.

>[!NOTE]
>
>이 필드 그룹은 [!DNL XDM Individual Profile]에는 사용할 수 없습니다 [!DNL XDM ExperienceEvent] 스키마. 경험 이벤트 스키마에 동의 및 기본 설정 데이터를 포함하려면 [[!UICONTROL 개인 정보, 개인화 및 마케팅 환경 설정에 대한 동의] 데이터 유형](../../data-types/consents.md) 를 사용하여 스키마로 [사용자 지정 필드 그룹](../../ui/resources/field-groups.md#create) 을 가리키도록 업데이트하는 것이 좋습니다.

## 필드 그룹 구조 {#structure}

다음 [!UICONTROL 동의 및 기본 설정] 필드 그룹은 단일 객체 유형 필드를 제공합니다. `consents`: 동의 및 기본 설정 정보를 캡처합니다. 이 필드는 [[!UICONTROL 개인 정보, 개인화 및 마케팅 환경 설정에 대한 동의] 데이터 유형](../../data-types/consents.md), 제거 `adID` 필드 및 추가 `idSpecific` 맵 필드.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>다음 안내서를 참조하십시오. [xdm 리소스 탐색](../../ui/explore.md) XDM 리소스를 검색하고 Platform UI에서 해당 구조를 검사하는 방법에 대한 단계를 설명합니다.

다음 JSON은 [!UICONTROL 동의 및 기본 설정] 필드 그룹이 처리할 수 있습니다. 필드 그룹에서 제공하는 대부분의 필드를 사용하는 방법에 대한 자세한 내용은 [동의 및 환경 설정 데이터 유형](../../data-types/consents.md). 아래 하위 섹션에서는 필드 그룹이 데이터 유형에 추가하는 고유한 속성에 중점을 둡니다.

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
>고객 동의 및 기본 설정 데이터를 매핑하는 방법을 시각화하는 데 도움이 되도록 Experience Platform에서 정의하는 모든 XDM 스키마에 대한 샘플 JSON 데이터를 생성할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.
>
>* [UI에서 샘플 데이터 생성](../../ui/sample.md)
>* [API에서 샘플 데이터 생성](../../api/sample-data.md)


### `idSpecific`

`idSpecific` 특정 동의 또는 기본 설정이 고객에게 일반적으로 적용되지 않지만 단일 장치 또는 ID로 제한되는 경우 사용할 수 있습니다. 예를 들어 고객이 한 주소로 전자 메일 수신을 옵트아웃하는 동시에 다른 주소로 이메일을 보낼 수 있습니다.

>[!IMPORTANT]
>
>채널 수준 동의 및 환경 설정(즉, `consents` 외부 `idSpecific`)가 해당 채널 내의 모든 ID에 적용됩니다. 따라서, 모든 채널 수준 동의 및 환경 설정은 등가 ID 또는 장치별 설정이 적용되는지 여부에 직접 영향을 줍니다.
>
>* 고객이 채널 수준에서 옵트아웃한 경우, `idSpecific` 은 무시됩니다.
>* 채널 수준 동의 또는 기본 설정이 설정되지 않았거나 고객이 옵트인한 경우, 다음과 같은 동의나 환경 설정이 `idSpecific` 명예가 됩니다.


의 각 키 `idSpecific` 개체는 Adobe Experience Platform Identity 서비스에서 인식하는 특정 id 네임스페이스를 나타냅니다. 고유한 사용자 지정 네임스페이스를 정의하여 서로 다른 식별자를 분류할 수 있지만, Identity 서비스에서 제공하는 표준 네임스페이스 중 하나를 사용하여 실시간 고객 프로필의 저장소 크기를 줄이는 것이 좋습니다. ID 네임스페이스에 대한 자세한 내용은 [id 네임스페이스 개요](../../../identity-service/namespaces.md) ( ID 서비스 설명서) 아래에 그룹화됩니다.

각 네임스페이스 개체의 키는 고객이 기본 설정을 지정한 고유한 ID 값을 나타냅니다. 각 ID 값에는 와 같은 방식으로 형식이 지정된 전체 동의 및 환경 설정 세트가 포함될 수 있습니다 `consents`.

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

내 `marketing` 에 제공된 객체 `idSpecific` 섹션, `any` 및 `preferred` 필드는 지원되지 않습니다. 이러한 필드는 사용자 수준에서만 구성할 수 있습니다. 또한 `idSpecific` 마케팅 환경 설정 `email`, `sms`, 및 `push` 지원 안 함 `subscriptions` 필드.

또한, `idSpecific` 섹션: `adID`. 이 필드는 아래 하위 섹션에서 다룹니다.

#### `adID`

다음 `adID` 동의는 광고주 ID(IDFA 또는 GAID)를 사용하여 이 장치의 앱 간에 고객을 연결할 수 있는지 여부에 대한 고객의 동의를 나타냅니다. 이 값은 `ECID` id 네임스페이스의 `idSpecific` 다른 네임스페이스에 대해 또는 이 필드 그룹의 사용자 수준에서 설정할 수 없습니다.

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
>Adobe Experience Platform Mobile SDK는 적절할 때 자동으로 설정하므로 이 값을 직접 설정하지 않아도 됩니다.

## 필드 그룹을 사용하여 데이터 수집 {#ingest}

를 사용하려면 [!UICONTROL 동의 및 기본 설정] 고객으로부터 동의 데이터를 수집하려면 해당 필드 그룹을 포함하는 스키마를 기반으로 데이터 세트를 만들어야 합니다.

다음에서 자습서를 참조하십시오. [UI에서 스키마 만들기](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 을 참조하십시오. 필드를 포함하는 스키마를 만들면 [!UICONTROL 동의 및 기본 설정] 필드 그룹에서는 [데이터 집합 만들기](../../../catalog/datasets/user-guide.md#create) 데이터 세트 사용 안내서에서 기존 스키마로 데이터 세트를 만드는 단계에 따릅니다.

>[!IMPORTANT]
>
>동의 데이터를에 보내려면 [!DNL Real-Time Customer Profile]를 지정하는 경우, [!DNL Profile]사용 가능한 스키마 [!DNL XDM Individual Profile] 를 포함하는 클래스 [!UICONTROL 동의 및 기본 설정] 필드 그룹. 해당 스키마를 기반으로 만드는 데이터 집합도 활성화해야 합니다 [!DNL Profile]. 관련 특정 단계에 대해서는 위에 링크된 자습서 를 참조하십시오 [!DNL Real-Time Customer Profile] 스키마 및 데이터 세트에 대한 요구 사항.
>
>또한 고객 프로필을 올바르게 업데이트하려면 병합 정책이 최신 동의 및 기본 설정 데이터가 포함된 데이터 세트에 우선 순위를 지정하도록 구성되어 있는지 확인해야 합니다. 다음 사항에 대한 개요를 참조하십시오. [정책 병합](../../../rtcdp/profile/merge-policies.md) 추가 정보.

## 동의 및 기본 설정 변경 처리

고객이 웹 사이트에서 동의 또는 환경 설정을 변경할 경우 이러한 변경 사항을 수집하고 즉시 [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). 고객이 데이터 수집을 거부하는 경우 모든 데이터 수집은 즉시 중지되어야 합니다. 고객이 개인화를 옵트아웃하는 경우 방문하는 다음 페이지에 개인화가 존재하지 않아야 합니다.

## 다음 단계

이 문서에서는 [!UICONTROL 동의 및 기본 설정] 필드 그룹. 필드 그룹에서 제공하는 다른 필드에 대한 자세한 내용은 [[!UICONTROL 개인 정보, 개인화 및 마케팅 환경 설정에 대한 동의] 데이터 유형](../../data-types/consents.md).
