---
keywords: Experience Platform;홈;인기 항목;옵트아웃;세그먼테이션;세그먼테이션 서비스;세그먼테이션 서비스;옵트아웃 적용;옵트아웃;옵트아웃;옵트아웃;옵트아웃;동의;공유;수집
solution: Experience Platform
title: 세그먼트에서 동의 준수
topic-legacy: overview
description: 개인 데이터 수집 및 세그먼트 작업에서 공유에 대한 고객 동의 환경 설정을 적용하는 방법을 알아봅니다.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 6d11a94d45b4a089ca6960aaf1ce78ae654ebc3f
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# 세그먼트에서 동의 준수

[!DNL California Consumer Privacy Act](CCPA)과 같은 법적 개인 정보 보호 규정은 소비자에게 개인 데이터를 수집하거나 제3자와 공유하지 않도록 선택할 수 있는 권한을 제공합니다. Adobe Experience Platform은 실시간 고객 프로필 데이터에서 이러한 고객 동의 환경 설정을 캡처하기 위한 표준 XDM(Experience Data Model) 구성 요소를 제공합니다.

고객이 개인 데이터를 공유하기 위한 동의를 철회하거나 보류한 경우 마케팅 활동에 대한 대상을 생성할 때 조직에서 해당 기본 설정을 수행하는 것이 중요합니다. 이 문서에서는 Experience Platform 사용자 인터페이스를 사용하여 세그먼트 정의에 고객 동의 값을 통합하는 방법을 설명합니다.

## 시작

고객 동의 값을 준수하려면 관련된 다양한 [!DNL Adobe Experience Platform] 서비스를 이해해야 합니다. 이 자습서를 시작하기 전에 다음 서비스를 숙지해야 합니다.

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Real-time Customer Profile]](../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 고객 프로필을 실시간으로 제공합니다.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):데이터에서 대상 세그먼트를 작성할 수  [!DNL Real-time Customer Profile] 있습니다.

## 동의 스키마 필드

고객 동의 및 환경 설정을 준수하려면 [!UICONTROL XDM 개별 프로필] 결합 스키마에 속하는 스키마 중 하나에 표준 필드 그룹 **[!UICONTROL 개인 정보/개인화/마케팅 환경 설정(동의)]**&#x200B;이 포함되어야 합니다.

필드 그룹에서 제공하는 각 속성의 구조 및 의도된 사용 사례에 대한 자세한 내용은 [동의 및 기본 설정 참조 안내서](../xdm/field-groups/profile/consents.md)를 참조하십시오. 스키마에 필드 그룹을 추가하는 방법에 대한 단계별 지침은 [XDM UI 안내서](../xdm/ui/resources/schemas.md#add-field-groups)를 참조하십시오.

필드 그룹이 [프로필 사용 스키마](../xdm/ui/resources/schemas.md#profile)에 추가되고 해당 필드가 경험 애플리케이션에서 동의 데이터를 수집하는 데 사용되면 세그먼트 규칙에서 수집된 동의 속성을 사용할 수 있습니다.

## 세그멘테이션에서 동의 처리

옵트아웃 프로필이 세그먼트에 포함되지 않도록 하려면, 기존 세그먼트에 특수 필드를 추가하고 새 세그먼트를 만들 때 포함해야 합니다.

아래 단계에서는 두 가지 유형의 옵트아웃 플래그에 적절한 필드를 추가하는 방법을 보여줍니다.

1. [!UICONTROL 데이터 수집]
1. [!UICONTROL 데이터 공유]

>[!NOTE]
>
>이 안내서는 위의 두 옵트아웃 플래그에 중점을 두는 반면, 추가 동의 신호를 포함하도록 세그먼트를 구성할 수 있습니다. [동의 및 환경 설정 참조 안내서](../xdm/field-groups/profile/consents.md)에서는 이러한 각 옵션 및 의도한 사용 사례에 대한 자세한 정보를 제공합니다.

UI에서 세그먼트를 작성할 때 **[!UICONTROL 속성]** 아래에서 **[!UICONTROL XDM 개별 프로필]**&#x200B;으로 이동한 다음 **[!UICONTROL 동의 및 환경 설정]**&#x200B;을 선택합니다. 여기에서 **[!UICONTROL 데이터 수집]** 및 **[!UICONTROL 데이터 공유]**&#x200B;에 대한 옵션을 볼 수 있습니다.

![](./images/opt-outs/consents.png)

먼저 **[!UICONTROL 데이터 수집]** 카테고리를 선택한 다음 **[!UICONTROL 선택 값]**&#x200B;을 세그먼트 빌더로 드래그합니다. 세그먼트에 속성을 추가할 때 포함 또는 제외해야 하는 [동의 값](../xdm/field-groups/profile/consents.md#choice-values)을 지정할 수 있습니다.

![](./images/opt-outs/consent-values.png)

한 가지 방법은 데이터를 수집하지 않는 고객을 제외하는 것입니다. 이렇게 하려면 연산자를 **[!UICONTROL 이(가)]**&#x200B;같지 않음을 설정하고 다음 값을 선택하십시오.

* **[!UICONTROL 아니요(옵트아웃)]**
* **[!UICONTROL 기본값은 아니요(옵트아웃)입니다.]**
* **[!UICONTROL 알 수 없음]** (알 수 없는 경우 동의가 보류된 것으로 추정되는 경우)

![](./images/opt-outs/collect.png)

왼쪽 레일의 **[!UICONTROL 속성]**&#x200B;에서 **[!UICONTROL 동의 및 환경 설정]** 섹션으로 돌아간 다음 **[!UICONTROL 데이터 공유]**&#x200B;를 선택합니다. 해당 **[!UICONTROL 선택 값]**&#x200B;을 캔버스로 드래그하고 [!UICONTROL 데이터 수집] 선택 값에 대해 동일한 값을 선택합니다. 두 특성 사이에 **[!UICONTROL Or]** 관계가 설정되어 있는지 확인합니다.

![](./images/opt-outs/share.png)

**[!UICONTROL 데이터 수집]** 및 **[!UICONTROL 데이터 공유]** 동의 값이 모두 세그먼트에 추가되면, 데이터 사용을 선택하지 않은 고객은 결과 대상에서 제외됩니다. 여기에서 **[!UICONTROL 저장]**&#x200B;을 선택하여 프로세스를 완료하기 전에 세그먼트 정의를 계속 사용자 지정할 수 있습니다.

## 다음 단계

이제 이 자습서를 따라 Experience Platform에서 세그먼트를 작성할 때 고객 동의 및 환경 설정을 준수하는 방법을 더 잘 이해할 수 있어야 합니다.

Platform에서 동의 관리에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Adobe 표준을 사용한 동의 처리](../landing/governance-privacy-security/consent/adobe/overview.md)
* [IAB TCF 2.0 표준을 사용한 동의 처리](../landing/governance-privacy-security/consent/iab/overview.md)