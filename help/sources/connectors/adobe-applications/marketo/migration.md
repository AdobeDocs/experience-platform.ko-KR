---
title: Marketo Engage 소스를 사용하여 ECID 매핑을 개인에서 활동으로 마이그레이션
description: Marketo Engage 소스를 사용하여 ECID 매핑을 개인 데이터 세트에서 활동 데이터 세트로 마이그레이션하는 방법에 대해 알아봅니다.
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 에서 ECID 매핑 마이그레이션 [!DNL Person] 데이터 세트 대상 [!DNL Activity] 데이터 세트

에서 ECID 매핑을 마이그레이션할 수 있습니다. [!DNL Marketo Engage Person] 데이터 세트를 [!DNL Activity] 데이터 수집 및 ID 관리의 안정적인 동작을 제공하기 위한 데이터 세트. 또한 이 마이그레이션은 다음 문제를 해결합니다.

| 문제 | 솔루션 |
| --- | --- |
| 다음의 경우 [!DNL Marketo Person] 데이터 세트에 여러 ECID에 대한 링크가 있지만, [XDM(경험 데이터 모델) 레코드의 총 ID 수가 20개를 초과합니다.](../../../../identity-service/guardrails.md). | ECID 필드 매핑을 로 마이그레이션 [!DNL Activity], 의 id 수를 확인할 수 있습니다. [!DNL Marketo Person] 데이터 흐름은 제한 내에 있으므로 데이터 수집이 성공할 수 있도록 합니다. |
| 다음 기간 동안 [!DNL Marketo Person] 데이터 세트는 ECID(모든 ECID의 타임스탬프)와 함께 수집됩니다. [!DNL Marketo Person] 데이터 세트는 개인 레코드의 마지막으로 업데이트된 타임스탬프로 업데이트됩니다. 이 경우 다음이 발생할 수 있습니다. [id 그래프에서 최근 id를 잘못 삭제](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | ECID 필드 매핑을 로 마이그레이션 [!DNL Activity], Identity Service는 ECID의 타임스탬프를 올바르게 반영할 수 있으며 Identity Service의 &quot;선입, 선출&quot; 메커니즘은 보다 안정적인 동작을 제공합니다. |
| ECID가 다음을 통해 수집되는 경우 [!DNL Marketo Person] 데이터 흐름, 새로 추가된 ECID는 다음에 대한 업데이트가 없는 한 Experience Platform에 수집되지 않습니다. [!DNL Person] 에 기록 [!DNL Marketo]. | 새 ECID가 [!DNL Person] 에 기록 [!DNL Marketo]를 통해 해당 ECID 데이터를 수집할 수 있습니다 [!DNL Marketo Activity] 데이터 흐름에서 Experience Platform 시 id 그래프를 즉시 업데이트합니다. |

기본적으로 다음을 수행해야 합니다.

* 업데이트 [!DNL Marketo Activity] 데이터 흐름.
* 업데이트 [!DNL Marketo Person] 데이터 흐름.

## 업데이트 [!DNL Marketo Activity] 데이터 흐름 {#update-activity-dataflow}

아래 단계에 따라 을(를) 업데이트하십시오. [!DNL Marketo Activity] 데이터 흐름:

* Experience Platform UI에서 *소스* 작업 공간 및 기존 데이터 흐름 찾기 [!DNL Marketo Activity] 데이터.
* 데이터 흐름이 활성화되면 줄임표(`...`) 데이터 흐름 이름 옆의 를 선택한 다음 를 선택합니다. **[!UICONTROL 데이터 흐름 업데이트]**.
* 그런 다음 을 선택합니다. **[!UICONTROL 다음]** 다음 위치에 도달할 때까지 *매핑* 인터페이스.
* 다음에서 *매핑* 인터페이스, 선택 **[!UICONTROL 새 필드]** 다음을 선택합니다. **[!UICONTROL 계산된 필드 추가]**. 여기에서 다음을 추가해야 합니다.

| 소스 데이터 세트 | XDM 타겟 필드 |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>기존 (으)로 업데이트하는 경우 [!DNL Marketo] 데이터 흐름은 ECID 매핑 필드 추가 또는 제거로만 구성된 경우, 데이터 흐름은 내역 채우기 작업을 자동으로 건너뜁니다. 새 데이터 수집은 &quot;웹 페이지 방문&quot; 및 &quot;웹 페이지 클릭&quot;과 같은 활동 유형이 발생하는 경우에만 발생합니다.

## 업데이트 [!DNL Marketo Person] 데이터 흐름 {#update-person-dataflow}

아래 단계에 따라 을(를) 업데이트하십시오. [!DNL Marketo Person] 데이터 흐름:

* Experience Platform UI에서 *소스* 작업 공간 및 기존 데이터 흐름 찾기 [!DNL Marketo Person] 데이터.
* 데이터 흐름이 활성화되면 줄임표(`...`) 데이터 흐름 이름 옆의 를 선택한 다음 를 선택합니다. **[!UICONTROL 데이터 흐름 업데이트]**.
* 그런 다음 을 선택합니다. **[!UICONTROL 다음]** 다음 위치에 도달할 때까지 *매핑* 인터페이스.
* 다음에서 *매핑* 인터페이스, 매핑되는 계산된 필드를 제거합니다. `identityMap` 다음을 선택합니다. **[!UICONTROL 다음]** 및 **[!UICONTROL 저장 및 수집]**.

>[!NOTE]
>
>기존 (으)로 업데이트하는 경우 [!DNL Marketo] 데이터 흐름은 ECID 매핑 필드 추가 또는 제거로만 구성된 경우, 데이터 흐름은 내역 채우기 작업을 자동으로 건너뜁니다. 이전에 수집된 ECID의 타임스탬프는 동일하게 유지됩니다. 기존 ECID에 해당하는 새 데이터를 수집할 때만 업데이트됩니다.

## 다음 단계

이제 이 문서를 읽고 ECID 매핑을 마이그레이션하는 방법을 이해할 수 있습니다. [!DNL Marketo Person] 데이터 세트 대상 [!DNL Marketo Activity] 데이터 세트. 자세한 내용은 다음을 참조하십시오 [!DNL Marketo] 문서:

* [수집할 데이터 흐름 만들기 [!DNL Marketo] Experience Platform 데이터](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [필드 매핑 안내서](../mapping/marketo.md).