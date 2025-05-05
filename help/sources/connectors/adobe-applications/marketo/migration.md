---
title: Marketo Engage 소스를 사용하여 ECID 매핑을 개인에서 활동으로 마이그레이션
description: Marketo Engage 소스를 사용하여 ECID 매핑을 개인 데이터 세트에서 활동 데이터 세트로 마이그레이션하는 방법에 대해 알아봅니다.
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# ECID 매핑을 [!DNL Person] 데이터 집합에서 [!DNL Activity] 데이터 집합으로 마이그레이션

ECID 매핑을 [!DNL Marketo Engage Person] 데이터 세트에서 [!DNL Activity] 데이터 세트로 마이그레이션하여 데이터 수집 및 ID 관리의 안정적인 동작을 제공할 수 있습니다. 또한 이 마이그레이션은 다음 문제를 해결합니다.

| 문제 | 솔루션 |
| --- | --- |
| [!DNL Marketo Person] 데이터 집합에 여러 ECID에 대한 링크가 있는 경우 XDM(Experience Data Model) 레코드의 [총 ID 수가 20](../../../../identity-service/guardrails.md)개를 초과하면 데이터 수집이 실패합니다. | ECID 필드 매핑을 [!DNL Activity] (으)로 마이그레이션하면 [!DNL Marketo Person] 데이터 흐름의 ID 수가 한도 내에 머물러 데이터 수집이 성공하도록 할 수 있습니다. |
| [!DNL Marketo Person] 데이터 집합이 ECID로 수집될 때마다 [!DNL Marketo Person] 데이터 집합의 모든 ECID에 대한 타임스탬프가 개인 레코드의 마지막으로 업데이트된 타임스탬프로 업데이트됩니다. 이로 인해 [ID 그래프에서 최근 ID가 잘못 삭제](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated)될 수 있습니다. | ECID 필드 매핑을 [!DNL Activity] (으)로 마이그레이션하면 Identity Service에서 ECID의 타임스탬프를 올바르게 반영할 수 있으며 Identity Service의 &quot;선입, 선출&quot; 메커니즘이 보다 안정적인 동작을 제공합니다. |
| ECID가 [!DNL Marketo Person] 데이터 흐름을 통해 수집되는 경우 [!DNL Marketo]에 [!DNL Person] 레코드에 대한 업데이트가 없으면 새로 추가된 ECID가 Experience Platform에 수집되지 않습니다. | 새 ECID가 [!DNL Marketo]의 [!DNL Person] 레코드에 연결되면 [!DNL Marketo Activity] 데이터 흐름을 통해 해당 ECID 데이터를 수집한 다음 Experience Platform 시 즉시 ID 그래프를 업데이트하라는 메시지를 표시할 수 있습니다. |

기본적으로 다음을 수행해야 합니다.

* [!DNL Marketo Activity] 데이터 흐름을 업데이트합니다.
* [!DNL Marketo Person] 데이터 흐름을 업데이트합니다.

## [!DNL Marketo Activity] 데이터 흐름 업데이트 {#update-activity-dataflow}

[!DNL Marketo Activity] 데이터 흐름을 업데이트하려면 아래 단계를 따르십시오.

* Experience Platform UI에서 *소스* 작업 영역으로 이동하여 [!DNL Marketo Activity] 데이터에 대한 기존 데이터 흐름을 찾습니다.
* 데이터 흐름이 활성화되어 있으면 데이터 흐름 이름 옆의 생략 부호(`...`)를 선택한 다음 **[!UICONTROL 데이터 흐름 업데이트]**&#x200B;를 선택합니다.
* *매핑* 인터페이스에 도달할 때까지 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.
* *매핑* 인터페이스에서 **[!UICONTROL 새 필드]**&#x200B;을(를) 선택한 다음 **[!UICONTROL 계산된 필드 추가]**&#x200B;를 선택하십시오. 여기에서 다음을 추가해야 합니다.

| Source 데이터 세트 | XDM 타겟 필드 |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>기존 [!DNL Marketo] 데이터 흐름에 대한 업데이트가 ECID 매핑 필드를 추가하거나 제거하는 것만으로 구성된 경우 데이터 흐름은 내역 채우기 작업을 자동으로 건너뜁니다. 새 데이터 수집은 &quot;웹 페이지 방문&quot; 및 &quot;웹 페이지 클릭&quot;과 같은 활동 유형이 발생하는 경우에만 발생합니다.

## [!DNL Marketo Person] 데이터 흐름 업데이트 {#update-person-dataflow}

[!DNL Marketo Person] 데이터 흐름을 업데이트하려면 아래 단계를 따르십시오.

* Experience Platform UI에서 *소스* 작업 영역으로 이동하여 [!DNL Marketo Person] 데이터에 대한 기존 데이터 흐름을 찾습니다.
* 데이터 흐름이 활성화되어 있으면 데이터 흐름 이름 옆의 생략 부호(`...`)를 선택한 다음 **[!UICONTROL 데이터 흐름 업데이트]**&#x200B;를 선택합니다.
* *매핑* 인터페이스에 도달할 때까지 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.
* *매핑* 인터페이스에서 `identityMap`에 매핑되는 계산된 필드를 제거한 다음 **[!UICONTROL 다음]** 및 **[!UICONTROL 저장 및 수집]**&#x200B;을(를) 선택하십시오.

>[!NOTE]
>
>기존 [!DNL Marketo] 데이터 흐름에 대한 업데이트가 ECID 매핑 필드를 추가하거나 제거하는 것만으로 구성된 경우 데이터 흐름은 내역 채우기 작업을 자동으로 건너뜁니다. 이전에 수집된 ECID의 타임스탬프는 동일하게 유지됩니다. 기존 ECID에 해당하는 새 데이터를 수집할 때만 업데이트됩니다.

## 다음 단계

이제 이 문서를 읽고 ECID 매핑을 [!DNL Marketo Person] 데이터 집합에서 [!DNL Marketo Activity] 데이터 집합으로 마이그레이션하는 방법을 알 수 있습니다. 자세한 내용은 다음 [!DNL Marketo] 문서를 참조하십시오.

* [수집할 데이터 흐름을 만듭니다 [!DNL Marketo] 데이터를 Experience Platform으로 만듭니다](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [필드 매핑 가이드](../mapping/marketo.md).
