---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 동의 및 기본 설정 데이터를 캡처하도록 데이터 세트 구성
topic: getting started
description: Adobe Experience Platform에서 동의 및 기본 설정 데이터를 캡처하기 위해 XDM(Experience Data Model) 스키마 및 데이터 집합을 구성하는 방법에 대해 알아보십시오.
translation-type: tm+mt
source-git-commit: 980bff169659d3ffc92a0678f8a0b153b3189906
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---


# 동의 및 기본 설정 데이터를 캡처하도록 데이터 세트 구성

Adobe Experience Platform에서 고객 동의/기본 설정 데이터를 처리하기 위해서는 해당 데이터를 스키마에는 동의 및 기타 권한과 관련된 필드가 포함되어 있는 데이터 세트에 보내야 합니다. 특히 이 데이터 집합은 [!DNL XDM Individual Profile] 클래스를 기반으로 하며 [!DNL Real-time Customer Profile]에서 사용하도록 활성화되어 있어야 합니다.

이 문서에서는 Experience Platform에서 동의 데이터를 처리하기 위해 데이터 세트를 구성하는 절차를 제공합니다. 플랫폼의 동의/기본 설정 데이터를 처리하기 위한 전체 작업 과정에 대한 개요는 [동의 처리 개요](./overview.md)를 참조하십시오.

>[!IMPORTANT]
>
>이 안내서의 예는 표준 필드 세트를 사용하여 [동의 및 기본 설정 XDM 데이터 유형](../../../../xdm/data-types/consents.md)에 의해 정의된 대로 고객 동의 값을 나타냅니다. 이러한 필드의 구조는 여러 일반적인 동의 수집 사용 사례를 처리하기 위해 효율적인 데이터 모델을 제공하기 위한 것입니다.
>
>그러나 고유한 데이터 모델에 따라 자신의 동의를 나타내기 위해 고유한 혼합을 정의할 수도 있습니다. 다음 옵션에 따라 비즈니스 요구에 맞는 동의 데이터 모델의 승인을 받으려면 법률 팀과 상의하십시오.
>
>* 표준화된 동의 혼합
>* 조직에서 만든 사용자 지정 동의 혼합
>* 사용자 정의 동의 혼합에 의해 제공되는 표준화된 동의 혼합과 추가 영역의 조합


## 전제 조건

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [경험 데이터 모델(XDM)](../../../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   * [스키마 컴포지션의 기본 사항](../../../../xdm/schema/composition.md):XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
* [실시간 고객 프로필](../../../../profile/home.md):서로 다른 소스의 고객 데이터를 하나의 완벽한 통합 보기로 통합하면서 모든 고객 인터랙션에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공합니다.

>[!IMPORTANT]
>
>이 자습서에서는 고객 속성 정보를 캡처하는 데 사용하려는 플랫폼의 [!DNL Profile] 스키마를 알고 있다고 가정합니다. 동의 데이터를 수집하는 데 사용하는 방법에 관계없이 이 스키마는 실시간 고객 프로필](../../../../xdm/ui/resources/schemas.md#profile)에 대해 [활성화되어야 합니다. 또한 스키마의 기본 ID는 이메일 주소와 같은 관심 기반 광고에 사용할 수 없는 직접 식별 가능한 필드가 될 수 없습니다. 어떤 분야가 제한되어 있는지 잘 모르는 경우 법률 자문을 구할 수 있습니다.

## 동의 및 환경 설정 혼합 구조 {#structure}

[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] 혼합(이하 &quot;동의 및 기본 설정 혼합&quot;이라 한다)은 스키마에 대한 표준 동의 필드를 제공합니다. 현재 이 믹스는 [!DNL XDM Individual Profile] 클래스를 기반으로 하는 스키마와만 호환합니다.

혼합은 표준 동의 필드 집합을 캡처하는 하위 속성의 단일 개체 유형 필드 `consents`를 제공합니다. 다음 JSON은 데이터 수집에 대해 `consents`이 예상하는 데이터 종류의 예입니다.

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
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
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>`consents`의 하위 속성의 구조와 의미에 대한 자세한 내용은 [동의 및 기본 설정 데이터 유형](../../../../xdm/data-types/consents.md)의 개요를 참조하십시오.

## 동의 및 환경 설정 믹스를 [!DNL Profile] 스키마 {#add-mixin}에 추가

플랫폼 UI의 왼쪽 탐색 영역에서 **[!UICONTROL Schemas]**&#x200B;을 선택한 다음 **[!UICONTROL Browse]** 탭을 선택하여 기존 스키마 목록을 표시합니다. 여기에서 동의 필드를 추가할 [!DNL Profile] 사용 스키마의 이름을 선택합니다. 이 섹션의 스크린샷은 [스키마 만들기 자습서](../../../../xdm/tutorials/create-schema-ui.md)에 내장된 &quot;충성도 구성원&quot; 스키마를 예로 사용합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>작업 공간의 검색 및 필터링 기능을 사용하여 스키마를 쉽게 찾을 수 있습니다. 자세한 내용은 [XDM 리소스](../../../../xdm/ui/explore.md)에 대한 가이드를 참조하십시오.

캔버스에서 스키마의 구조를 표시하는 [!DNL Schema Editor]이 나타납니다. 캔버스의 왼쪽에서 **[!UICONTROL Mixins]** 섹션 아래의 **[!UICONTROL Add]**&#x200B;을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-mixin.png)

**[!UICONTROL Add mixin]** 대화 상자가 나타납니다. 여기서 목록에서 **[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]**&#x200B;을 선택합니다. 선택적으로 검색 막대를 사용하여 결과의 범위를 좁혀 믹싱을 더 쉽게 찾을 수 있습니다. 믹스를 선택하고 나면 **[!UICONTROL Add mixin]**&#x200B;을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/mixin-dialog.png)

`consents` 객체가 스키마 구조에 추가되었음을 보여 주는 캔버스가 다시 나타납니다. 표준 혼합에서 캡처하지 않은 추가 동의 및 환경 설정 필드가 필요한 경우 [사용자 정의 동의 및 환경 설정 필드를 스키마](#custom-consent)에 추가하는 것을 참조하십시오. 그렇지 않은 경우 **[!UICONTROL Save]**&#x200B;을 선택하여 스키마 변경 내용을 완료합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

편집한 스키마가 플랫폼 웹 SDK 에지 구성에 지정된 [!UICONTROL Profile Dataset]에서 사용되는 경우 이제 해당 데이터 세트에 새 동의 필드가 포함됩니다. 이제 [동의 처리 안내서](./overview.md#merge-policies)로 돌아가 동의 데이터를 처리하도록 Experience Platform 구성 프로세스를 계속할 수 있습니다.

이 스키마에 대한 데이터 세트를 만들지 않은 경우 다음 섹션의 절차를 따르십시오.

## 동의 스키마 {#dataset}를 기반으로 데이터 집합 만들기

동의 필드가 있는 스키마를 만든 후 고객의 동의 데이터를 최종적으로 수집하는 데이터 세트를 만들어야 합니다. 이 데이터 집합은 [!DNL Real-time Customer Profile]에 대해 활성화되어 있어야 합니다.

시작하려면 왼쪽 탐색 메뉴에서 **[!UICONTROL Datasets]**&#x200B;을 선택하고 오른쪽 위 모서리에서 **[!UICONTROL Create dataset]**&#x200B;을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

다음 페이지에서 **[!UICONTROL Create dataset from schema]**&#x200B;을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

**[!UICONTROL Select schema]** 단계부터 **[!UICONTROL Create dataset from schema]** 워크플로우가 나타납니다. 제공된 목록에서 이전에 만든 동의 스키마 중 하나를 찾습니다. 검색 막대를 사용하여 검색 결과의 범위를 좁히고 스키마를 더 쉽게 찾을 수도 있습니다. 원하는 스키마 옆의 라디오 단추를 선택한 다음 **[!UICONTROL Next]**&#x200B;을 선택하여 계속합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

**[!UICONTROL Configure dataset]** 단계가 나타납니다. **[!UICONTROL Finish]**&#x200B;을 선택하기 전에 데이터 세트에 대한 고유하고 쉽게 식별할 수 있는 이름 및 설명을 제공합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

새로 만든 데이터 세트에 대한 세부 사항 페이지가 나타납니다. 데이터 세트가 시간 시리즈 스키마를 기반으로 하는 경우 프로세스가 완료됩니다. 데이터 세트가 레코드 스키마를 기반으로 하는 경우, 마지막 단계는 데이터 세트를 [!DNL Real-time Customer Profile]에서 사용하도록 설정하는 것입니다.

오른쪽 레일에서 **[!UICONTROL Profile]** 토글을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

마지막으로, 확인 팝업에서 **[!UICONTROL Enable]**&#x200B;을 선택하여 [!DNL Profile]에 대한 스키마를 활성화합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

이제 데이터 세트가 저장되고 [!DNL Profile]에서 사용할 수 있습니다. Platform Web SDK를 사용하여 프로필에 동의 데이터를 전송하려는 경우 [Edge 구성](../../../../edge/fundamentals/edge-configuration.md)을(를) 설정할 때 이 데이터 세트를 [!UICONTROL Profile Dataset]으로 선택해야 합니다.

## 다음 단계

이 자습서를 따라, 동의 필드를 플랫폼 웹 SDK 또는 직접 XDM 습성을 사용하여 동의 데이터를 수집하는 데 사용할 데이터세트를 포함하는 [!DNL Profile] 사용 스키마에 추가했습니다.

이제 [동의 처리 개요](./overview.md#merge-policies)로 돌아가 동의 데이터를 처리하도록 Experience Platform을 계속 구성할 수 있습니다.

## 부록

다음 섹션에서는 고객 동의 및 기본 설정 데이터를 수집하기 위한 데이터 세트를 만드는 방법에 대한 추가 정보를 제공합니다.

### 사용자 정의 동의 및 환경 설정 필드를 {#custom-consent} 스키마에 추가합니다.

표준 [!DNL Consents & Preferences] 혼합으로 표시되는 것과 다른 별도의 동의 신호를 캡처해야 하는 경우 사용자 지정 XDM 구성 요소를 사용하여 특정 비즈니스 요구에 맞게 동의 스키마를 향상시킬 수 있습니다. 이 섹션에서는 Adobe Experience Platform Mobile 및 웹 SDK에서 수행한 동의 변경 명령과 호환되는 방식으로 동의 스키마를 사용자 지정하는 방법에 대한 기본 원칙을 설명합니다.

>[!IMPORTANT]
>
>전체 구조를 처음부터 만드는 대신 [!DNL Consents & Preferences] 믹싱을 동의 데이터 구조의 기준선으로 사용하고 필요에 따라 추가 필드를 추가해야 합니다.

표준 믹스의 구조에 사용자 정의 필드를 추가하려면 먼저 사용자 정의 믹싱을 만들어야 합니다. 스키마에 [!DNL Consents & Preferences] 혼합을 추가한 후 **[!UICONTROL Mixins]** 섹션에서 **더하기(+)** 아이콘을 선택한 다음 **[!UICONTROL Create new mixin]**&#x200B;를 선택합니다. 혼합에 대한 이름 및 선택적 설명을 입력한 다음 **[!UICONTROL Add mixin]**&#x200B;을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-mixin.png)

왼쪽 레일에서 새 사용자 정의 믹서가 선택된 상태로 [!DNL Schema Editor]이 다시 나타납니다. 캔버스에서 사용자 정의 필드를 스키마 구조에 추가할 수 있는 컨트롤이 표시됩니다. 새 동의 또는 환경 설정 필드를 추가하려면 `consents` 개체 옆에 있는 **더하기(+)** 아이콘을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

`consents` 개체 내에 새 필드가 나타납니다. 표준 XDM 개체에 사용자 정의 필드를 추가하므로 새 필드가 테넌트 ID에 지정된 개체 아래에 생성됩니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

**[!UICONTROL Field properties]** 오른쪽 레일에서 필드에 대한 이름과 설명을 입력합니다. 필드의 **[!UICONTROL Type]**&#x200B;을 선택할 때 사용자 지정 동의 또는 기본 설정 필드에 적절한 표준 데이터 유형을 사용해야 합니다.

* [[!UICONTROL Generic Consent Field]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Generic Marketing Preference Field]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Generic Marketing Preference Field with Subscriptions]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Generic Personalization Preference Field]](../../../../xdm/data-types/personalization-field.md)

완료되면 **[!UICONTROL Apply]**&#x200B;을 선택합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

동의 또는 환경 설정 필드가 스키마 구조에 추가됩니다. 오른쪽 레일에 표시되는 [!UICONTROL Path]에는 `_tenantId` 네임스페이스가 포함되어 있습니다. 이 네임스페이스는 데이터 작업에서 이 필드의 경로를 참조할 때마다 포함되어야 합니다.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

필요한 동의 및 기본 설정 필드를 계속 추가하려면 위의 단계를 따르십시오. 완료되면 **[!UICONTROL Save]**&#x200B;을 선택하여 변경 내용을 확인합니다.

편집한 스키마가 플랫폼 웹 SDK 에지 구성에 지정된 [!UICONTROL Profile Dataset]에서 사용되는 경우 이제 해당 데이터 세트에 새 동의 필드가 포함됩니다. 이제 [동의 처리 안내서](./overview.md#merge-policies)로 돌아가 동의 데이터를 처리하도록 Experience Platform 구성 프로세스를 계속할 수 있습니다.

이 스키마에 대한 데이터 집합을 만들지 않은 경우 [데이터 집합 만들기](#dataset)의 섹션으로 계속하십시오.