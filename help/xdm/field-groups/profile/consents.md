---
solution: Experience Platform
title: 동의 및 환경 설정 스키마 필드 그룹
description: 동의 및 환경 설정 스키마 필드 그룹에 대해 알아봅니다.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: be35c5398cd96cdfe424c5088db288ba4061ac4a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# [!UICONTROL 동의 및 환경 설정] 필드 그룹

[!UICONTROL 동의 및 환경 설정]은(는) 개별 고객에 대한 동의 및 환경 설정 정보를 캡처하는 [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md)의 표준 필드 그룹입니다.

>[!NOTE]
>
>이 필드 그룹은 [!DNL XDM Individual Profile]과만 호환되므로 [!DNL XDM ExperienceEvent] 스키마에 사용할 수 없습니다. 경험 이벤트 스키마에 동의 및 환경 설정 데이터를 포함하려면 대신 [사용자 지정 필드 그룹](../../ui/resources/field-groups.md#create)을 사용하여 [[!UICONTROL 개인 정보, Personalization 및 마케팅 환경 설정에 대한 동의] 데이터 형식](../../data-types/consents.md)을(를) 스키마에 추가하십시오.

## 필드 그룹 구조 {#structure}

[!UICONTROL 동의 및 환경 설정] 필드 그룹은 동의 및 환경 설정 정보를 캡처할 수 있는 단일 개체 유형 필드 `consents`을(를) 제공합니다. 이 필드는 [[!UICONTROL 개인 정보, Personalization 및 마케팅 환경 설정에 대한 동의] 데이터 형식](../../data-types/consents.md)을(를) 확장하여 `adID` 필드를 제거하고 `idSpecific` 맵 필드를 추가합니다.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>XDM 리소스를 검색하고 Platform UI에서 해당 구조를 검사하는 방법에 대한 단계는 [XDM 리소스 살펴보기](../../ui/explore.md)에 대한 안내서를 참조하십시오.

다음 JSON은 동의 및 환경 설정] 필드 그룹 그룹이 처리할 수 있는 [!UICONTROL 데이터 유형의 예를 보여 줍니다. 필드 그룹 에서 제공하는 대부분의 필드를 사용하는 방법에 대한 자세한 내용은 동의 및 환경 설정 데이터 유형에](../../data-types/consents.md) 대한 [안내서 를 참조하십시오. 필드 그룹 그룹이 데이터 형식에 추가하는 고유한 특성에 대한 포커스 아래의 하위 섹션입니다.

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
>고객 동의 및 기본 설정 데이터를 매핑하는 방법을 시각화하기 위해 Experience Platform 에서 정의한 XDM 스키마에 대한 샘플 JSON 데이터를 생성할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.
>
>* [UI 에서 샘플 데이터 생성](../../ui/sample.md)
>* [API에서 샘플 데이터 생성](../../api/sample-data.md)

### `idSpecific`

`idSpecific` 특정 동의 또는 기본 설정이 고객에게 보편적으로 적용되지 않고 단일 디바이스 또는 ID로 제한되는 경우에 사용할 수 있습니다. 예를 들어 고객이 한 주소에 대한 이메일 수신을 거부하는 동시에 다른 주소에 대한 이메일을 허용할 수 있습니다.

>[!IMPORTANT]
>
>채널 수준의 동의 및 기본 설정(즉, 외부`idSpecific`에서 제공되는 `consents` 동의 및 기본 설정은 해당 채널 내의 모든 ID에 적용됩니다. 따라서 모든 채널 수준의 동의 및 기본 설정은 동등한 ID 또는 디바이스별 설정이 적용되는지 여부에 직접적인 영향을 미칩니다.
>
>* 고객이 채널 수준에서 옵트아웃한 경우 의 `idSpecific` 동등한 동의 또는 기본 설정은 무시됩니다.
>* 채널 수준의 동의 또는 기본 설정이 설정되지 않았거나 고객이 선택한 경우 동등한 동의 또는 기본 설정이 `idSpecific` 적용됩니다.

개체의 각 키는 `idSpecific` Adobe Experience Platform ID 서비스에서 인식하는 특정 ID 네임스페이스를 나타냅니다. 사용자 정의 네임스페이스를 정의하여 다른 식별자를 분류할 수 있지만 Identity Service에서 제공하는 표준 네임스페이스 중 하나를 사용하여 실시간 고객 프로필의 스토리지 크기를 줄이는 것이 좋습니다. ID 네임스페이스에 대한 자세한 내용은 ID 서비스 설명서의 [ID 네임스페이스 개요](../../../identity-service/features/namespaces.md)를 참조하십시오.

각 네임스페이스 개체에 대한 키는 고객이 기본 설정으로 지정한 고유한 ID 값을 나타냅니다. 각 ID 값에는 `consents`과(와) 동일한 형식의 전체 동의 및 환경 설정 집합이 포함될 수 있습니다.

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

`idSpecific` 섹션에 제공된 `marketing` 개체 내에서는 `any` 및 `preferred` 필드가 지원되지 않습니다. 이러한 필드는 사용자 수준에서만 구성할 수 있습니다. 또한 `email`, `sms` 및 `push`에 대한 `idSpecific` 마케팅 환경 설정은 `subscriptions` 필드를 지원하지 않습니다.

`idSpecific` 섹션에서만 제공할 수 있는 동의도 있습니다. `adID`. 이 필드는 아래 하위 섹션에 설명되어 있습니다.

#### `adID`

`adID` 동의는 광고주 ID(IDFA 또는 GAID)를 사용하여 이 장치의 앱 간에 고객을 연결할 수 있는지 여부에 대한 고객의 동의를 나타냅니다. 이 값은 `idSpecific` 섹션의 `ECID` ID 네임스페이스 아래에서만 구성할 수 있으며 다른 네임스페이스에 대해 또는 이 필드 그룹의 사용자 수준에서 설정할 수 없습니다.

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
>Adobe Experience Platform Mobile SDK은 적절할 때 이 값을 자동으로 설정하므로 이 값을 직접 설정할 필요는 없습니다.

## 필드 그룹을 사용하여 데이터 수집 {#ingest}

[!UICONTROL 동의 및 환경 설정] 필드 그룹을 사용하여 고객의 동의 데이터를 수집하려면 해당 필드 그룹을 포함하는 스키마를 기반으로 데이터 집합을 만들어야 합니다.

필드에 필드 그룹을 할당하는 방법에 대한 단계는 UI](https://www.adobe.com/go/xdm-schema-editor-tutorial-en)에서 스키마 만들기에 대한 [튜토리얼을 참조하십시오. 동의 및 환경 설정] 필드 그룹 사용하여 [!UICONTROL 필드가 포함된 스키마를 만든 후에는 기존 스키마를 사용하여 데이터 세트 만드는 절차에 따라 데이터 세트 사용자 안내서에서 데이터 세트](../../../catalog/datasets/user-guide.md#create) 만드는 섹션을 [참조하십시오.

>[!IMPORTANT]
>
>동의 데이터를 [!DNL Real-Time Customer Profile]로 보내려면 동의 및 환경 설정] 필드 그룹 포함하는 [!UICONTROL 클래스를 기반으로 [!DNL XDM Individual Profile] 사용 스키마를 만들어야 [!DNL Profile]합니다. 해당 스키마를 기반으로 만든 데이터 세트 역시 에 대해 [!DNL Profile]활성화되어 있어야 합니다. 스키마 및 데이터 세트에 대한 요구 사항과 [!DNL Real-Time Customer Profile] 관련된 특정 단계에 대해서는 위에 연결된 자습서를 참조하십시오.
>
>또한 고객 프로필이 올바르게 업데이트되도록 최신 동의 및 기본 설정 데이터가 포함된 데이터 세트 우선 순위를 지정하도록 병합 정책이 구성되어 있는지 확인해야 합니다. 자세한 내용은 병합 정책에](../../../rtcdp/profile/merge-policies.md) 대한 [개요를 참조하세요.

## 동의 및 기본 설정 변경 처리

고객이 웹 사이트에서 동의 또는 기본 설정을 변경하면 이러한 변경 사항을 수집하고 Adobe Experience Platform 웹 SDK](../../../web-sdk/commands/setconsent.md)를 [사용하여 즉시 적용해야 합니다. 고객이 데이터 수집을 옵트아웃하는 경우 모든 데이터 수집을 즉시 중단해야 합니다. 고객이 개인화를 옵트아웃하면 로드하는 다음 페이지에 개인화가 없어야 합니다.

## 다음 단계

이 문서에서는 동의 및 환경 설정] 필드 그룹 구성과 사용에 [!UICONTROL 대해 설명했습니다. 필드 그룹 에서 제공하는 다른 필드에 대한 자세한 내용은 개인 정보 보호, 개인 설정 및 마케팅 환경 설정] 데이터 유형에](../../data-types/consents.md) 대한 [[!UICONTROL 동의 문서를 참조하십시오.
