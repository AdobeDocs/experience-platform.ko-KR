---
keywords: Experience Platform;홈;인기 항목;ID 서비스;ID 서비스;공유 장치;공유 장치
solution: Experience Platform
title: 공유 장치 개요(베타)
topic-legacy: tutorial
description: 공유 장치 감지는 동일한 장치의 서로 다른 인증된 사용자를 식별하므로 ID 그래프에서 고객 데이터를 보다 정확하게 표현할 수 있습니다
hide: true
hidefromtoc: true
source-git-commit: 205d9a8d0d5759e978604bef2b05664b1376d835
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# 공유 장치 탐지 개요(베타)

>[!IMPORTANT]
>
>[!DNL Shared Device Detection] 기능은 베타에 있습니다. 해당 기능과 설명서는 변경될 수 있습니다.

Adobe Experience Platform [!DNL Identity Service]은(는) 장치 및 시스템 전반에서 ID를 브리징하여 고객 및 그 행동을 더 잘 볼 수 있도록 해주므로, 효과적이고 개인화된 디지털 경험을 실시간으로 제공할 수 있습니다.

[!DNL Shared Device Detection] 둘 이상의 개인이 사용하는 장치를 참조하십시오. 공유 장치의 예로는 태블릿, 라이브러리 컴퓨터 및 키오스크가 있습니다. [!DNL Shared Device Detection] 을 통해 동일한 장치의 서로 다른 사용자가 하나의 ID로 병합되지 않도록 하여 보다 정확한 표현을 제공할 수 있습니다.

[!DNL Shared Device Detection]을 사용하면 다음 작업을 수행할 수 있습니다.

* 동일한 장치의 다른 사용자에 대해 별도의 ID 그래프를 만듭니다.
* 동일한 장치를 사용하는 서로 다른 개인으로부터 데이터가 혼합되지 않도록 합니다.
* 고객에 대한 보다 정확하고 깨끗한 뷰를 생성합니다.

>[!TIP]
>
>더 이상 설정을 개정하지 않으므로 데이터 세트에 대해 [!DNL Shared Device Detection]에 대한 구성을 완료해야 합니다. 데이터가 [!DNL Identity Service]로 유입되기 시작하면 이 설정을 다시 수정해야 합니다.[!DNL Profile]

## 시작하기

[!DNL Shared Device Detection]을(를) 사용하려면 관련된 다양한 플랫폼 서비스를 이해해야 합니다. [!DNL Shared Device Detection] 작업을 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL Identity Service]](../home.md): 여러 장치와 시스템에서 ID를 브리징하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
   * [ID 그래프 뷰어](./identity-graph-viewer.md): ID 그래프 뷰어를 시각화하고 상호 작용하여 고객 ID가 어떻게 서로 결합되는지, 그리고 어떤 방식으로 결합되는지 더 잘 이해할 수 있습니다.
   * [ID 네임스페이스](../namespaces.md): 정규화된 ID의 구성 요소 및 ID 네임스페이스를 통해 ID의 컨텍스트와 유형을 구별하는 방법을 참조하십시오.

### 용어

다음 표에는 [!DNL Shared Device Detection]을 이해하는 데 필요한 용어 목록이 포함되어 있습니다.

| 용어 | 정의 |
| --- | --- |
| 공유 장치 | 공유 장치는 둘 이상의 개인이 사용하는 모든 장치입니다. 공유 장치의 예로는 태블릿, 라이브러리 컴퓨터 및 키오스크가 있습니다. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] 는 동일한 장치의 다른 사용자의 데이터를 서로 분리할 수 있도록 하는 구성 설정을 나타냅니다. |
| [!UICONTROL 공유 ID 네임스페이스] | [!UICONTROL 공유 ID 네임스페이스]는 여러 다른 사용자가 공유하는 단일 장치를 나타내는 데 사용됩니다. |
| [!UICONTROL 사용자 ID 네임스페이스] | [!UICONTROL 사용자 ID 네임스페이스]는 공유 장치의 인증된 사용자 또는 로그인한 사용자를 나타내는 데 사용됩니다. |

## 공유 장치 UI

Platform UI의 왼쪽 탐색에서 **[!UICONTROL ID]**&#x200B;를 선택한 다음 **[!UICONTROL ID 설정]**&#x200B;을 선택합니다.

![identity-dashboard](../images/shared-device/identity-dashboard.png)

[!UICONTROL 공유 장치 설정] 페이지가 나타나고, 데이터에 대한 공유 장치 설정을 구성할 수 있는 인터페이스를 제공합니다. 공유 장치 설정은 기본적으로 비활성화됩니다.

공유 장치 설정을 사용하면 동일한 장치의 다른 사용자의 데이터를 서로 분리할 수 있습니다. 이 구성 설정을 사용하면 동일한 장치의 사용자 ID가 함께 결합되지 않는 ID 그래프를 보다 정확하고 깨끗하게 표현할 수 있습니다.

**[!UICONTROL 활성화]**&#x200B;를 선택하여 공유 장치 설정 수정을 시작합니다.

![enable-shared-device](../images/shared-device/enable-shared-device.png)

[!UICONTROL 공유 ID 네임스페이스] 및 [!UICONTROL 사용자 ID 네임스페이스] 구성 옵션이 표시되어 사용할 ID 네임스페이스를 수정할 수 있습니다.

![네임스페이스 설정](../images/shared-device/set-namespaces.png)

[!UICONTROL 공유 ID ] 네임스페이스 는 여러 다른 사용자가 사용하는 단일 장치를 나타냅니다. 모든 플랫폼 사용자가 **[!UICONTROL ECID]**&#x200B;를 웹 브라우저 식별자로 사용하므로 이 네임스페이스는 항상 **[!UICONTROL ECID]**&#x200B;로 설정됩니다.

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

[!UICONTROL 사용자 ID 네임스페이스]를 사용하면 동일한 장치의 다른 사용자를 식별하고 데이터가 동일한 ID 그래프로 결합되지 않도록 할 수 있습니다.

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

**[!UICONTROL 사용자 ID 네임스페이스]** 검색 막대를 선택하고 ID 네임스페이스를 입력하거나 드롭다운 메뉴에서 ID 네임스페이스를 선택합니다.

>[!TIP]
>
>[!UICONTROL 사용자 ID 네임스페이스]는 최종 사용자의 로그인 ID에 해당하는 ID 네임스페이스에 매핑해야 합니다. 옵션에는 고객 ID, 이메일 및 해시된 이메일이 있습니다.

![이메일](../images/shared-device/emails.png)

[!UICONTROL 공유 장치 설정을 구성했으면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.]

![저장](../images/shared-device/save.png)

선택 내용을 확인하라는 팝업 창이 나타납니다. **[!UICONTROL 예]**&#x200B;를 선택하여 구성 설정을 완료합니다.

![confirm](../images/shared-device/confirm.png)
