---
keywords: 이벤트 전달 확장;mixpanel;mixpanel 이벤트 전달 확장
title: Mixpanel 추적 이벤트 API 이벤트 전달 확장
description: 이 Adobe Experience Platform 이벤트 전달 확장은 Edge Network 이벤트를 Mixpanel로 보냅니다.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API 이벤트 전달 확장

[[!DNL Mixpanel]](https://www.mixpanel.com)은(는) 사용자가 디지털 제품과 상호 작용하는 방식에 대한 데이터를 캡처할 수 있는 제품 분석 도구입니다. 몇 번의 클릭만으로 데이터를 쿼리하고 시각화할 수 있는 간단한 대화형 보고서를 사용하여 제품 데이터를 분석할 수 있습니다. [!DNL Mixpanel]은(는) 모든 사람이 실시간으로 사용자 데이터를 분석하여 트렌드를 식별하고, 사용자 행동을 이해하고, 제품에 대한 결정을 내릴 수 있도록 함으로써 팀을 보다 효율적으로 만들 수 있도록 설계되었습니다.

[!DNL Mixpanel]은(는) 각 상호 작용을 단일 사용자에게 연결하는 이벤트 기반 사용자 중심 모델을 사용합니다. [!DNL Mixpanel] 데이터 모델은 사용자, 이벤트 및 속성의 개념을 기반으로 합니다.

>[!NOTE]
>
>[!DNL Mixpanel]이(가) 이벤트를 병합하여 ID 클러스터를 만드는 방법을 이해하려면 [ID 관리](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management)에 대한 [!DNL Mixpanel] 설명서를 참조하세요. 또한 [고유 ID](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-)에 대한 문서를 검토하여 이러한 ID가 이벤트 데이터에서 사용자를 식별하는 데 사용되는 방법을 이해하는 것이 좋습니다.

## 사용 사례

[!DNL Mixpanel]에 있는 Edge Network의 데이터를 사용하여 제품 분석 기능을 이용하려면 이 확장을 사용해야 합니다.

예를 들어, 다중 채널 존재(웹 사이트 및 모바일)가 있는 소매 조직을 고려해 보십시오. 조직은 트랜잭션 또는 대화 입력을 해당 플랫폼에서 이벤트 데이터로 캡처하고 이벤트 전달 확장을 사용하여 [!DNL Mixpanel]에 로드합니다.

그런 다음 분석 팀은 [!DNL Mixpanel's] 기능을 활용하여 데이터 세트를 처리하고 비즈니스 인사이트를 도출할 수 있습니다. 이 인사이트는 그래프, 대시보드 또는 비즈니스 이해 당사자에게 알리는 다른 시각화를 생성하는 데 사용할 수 있습니다.

[!DNL Mixpanel]과(와) 관련된 사용 사례에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [새로 만들기 [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [ [!DNL Mixpanel] (이)란?](https://developer.mixpanel.com/docs)
* [12개의 필수 [!DNL Mixpanel] 기능](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel]개 필수 구성 요소 {#prerequisites-mixpanel}

이 확장을 사용하려면 올바른 [!DNL Mixpanel] 계정이 있어야 합니다. 아직 계정이 없는 경우 [[!DNL Mixpanel] 등록 페이지](https://mixpanel.com/register/)(으)로 이동하여 등록하고 계정을 만드십시오.

프로젝트에 대해 [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) 설정이 활성화되어 있는지 확인하십시오. **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]**(으)로 이동하여 설정을 전환합니다.

### [!DNL Mixpanel]의 ID 클러스터 이해

[!DNL Mixpanel]에서 ID 클러스터에는 개별 사용자에 연결하는 `distinct_id` 값의 컬렉션이 포함되어 있습니다. [!DNL Mixpanel]은(는) 각 사용자에 대한 ID 클러스터를 처리하며 보고에 사용할 각 클러스터의 단일 표준 `distinct_id`을(를) 확인합니다. 사용자 ID 이벤트 전에 발생하는 익명 이벤트에 대해 고유한 식별자(로컬 `distinct_id`이라고 함)를 포함할 수도 있습니다.

[!DNL Mixpanel]은(는) 다음 두 가지 방법을 통해 ID 클러스터를 확인합니다.

* **식별** : [!DNL Mixpanel]은(는) 선택한 식별자를 익명 `distinct_id`에 연결합니다. 웹 사이트에서 [!DNL Mixpanel] SDK를 사용하도록 설정한 경우 Platform은 현재 로그인한 사용자에게 할당된 `distinct_id`을(를) 사용합니다.
* **별칭**: [!DNL Mixpanel]은(는) 추가 병합 기준이 충족되는 경우 익명이 아닌 두 개의 `distinct id`을(를) 결합합니다.

>[!NOTE]
>
>이 메서드에 대한 자세한 내용은 [ID 관리](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification)의 [!DNL Mixpanel] 문서를 참조하십시오.
>
>ID 클러스터가 적절하게 확인되도록 [[!DNL Mixpanel] ID 병합 기능](#prerequisites-mixpanel)을 사용하도록 설정했는지 확인하십시오.

### 필요한 구성 세부 정보 수집 {#configuration-details}

Experience Platform을 [!DNL Mixpanel]에 연결하려면 다음 입력이 있어야 합니다.

| 키 유형 | 설명 | 예 |
| --- | --- | --- |
| 프로젝트 토큰 | [!DNL Mixpanel] 계정과 연결된 프로젝트 토큰입니다. 지침은 [프로젝트 토큰 찾기](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-)에 대한 [!DNL Mixpanel] 설명서를 참조하십시오. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## [!DNL Mixpanel] 확장 설치 및 구성 {#install}

확장을 설치하려면 [이벤트 전달 속성을 만들거나](../../../ui/event-forwarding/overview.md#properties) 대신 편집할 기존 속성을 선택하십시오.

왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다. **[!UICONTROL 카탈로그]** 탭에서 [!DNL Mixpanel] 확장의 카드에서 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![[!DNL Mixpanel] 확장을 설치하는 중](../../../images/extensions/server/mixpanel/install-extension.png)

## [!DNL Send Event] 규칙 만들기

이벤트 전달 속성에서 새 규칙 만들기를 시작합니다. **[!UICONTROL 작업]**&#x200B;에서 새 작업을 추가하고 확장을 **[!UICONTROL Mixpanel]**(으)로 설정합니다. 그런 다음 작업 유형을 **[!UICONTROL 이벤트 추적]**(으)로 설정하여 Edge Network 이벤트를 [!DNL Mixpanel](으)로 보냅니다.

| 입력 | 설명 | 필수 여부 |
| --- | --- | --- |
| [!UICONTROL 프로젝트 토큰] | 이 필드는 [!DNL Mixpanel] 계정과 연결된 프로젝트 토큰에 매핑되어야 합니다. | 예 |
| [!UICONTROL 이벤트 유형] | 이벤트 이름. | 예 |
| [!UICONTROL 이벤트 시간] | 이벤트 시간. | |
| [!UICONTROL Mixpanel 고유 ID] | 이벤트를 수행한 사용자의 고유 식별자입니다. | |
| [!UICONTROL ID 삽입] | 중복 제거에 사용되는 이벤트의 고유 식별자입니다. | |
| [!UICONTROL 이벤트 속성] | 이벤트의 사용자 지정 속성이 포함된 JSON 개체입니다. 원시 JSON을 제공하거나 간소화된 키-값 입력 세트를 사용하여 선택하십시오. | |

>[!NOTE]
>
>[!DNL Mixpanel] 이벤트의 표준 필드에 대한 자세한 내용은 [공식 설명서](https://developer.mixpanel.com/reference/import-events#event)를 참조하세요.

![이벤트 전달 규칙 작업 구성을 추가합니다.](../../../images/extensions/server/mixpanel/track-event-action.png)

[!UICONTROL 이벤트 추적] 작업이 규칙에 추가되면 특정 이벤트에 대해서만 실행되도록 규칙 조건을 구성하거나, 모든 이벤트에 대해 규칙이 실행되도록 조건 섹션을 비워 둘 수 있습니다.

>[!IMPORTANT]
>
>웹 사이트에서 [!DNL Mixpanel] SDK를 사용하는 경우 [내에서 데이터 유효성 검사 [!DNL Mixpanel]](#validate)의 다음 단계를 계속할 수 있습니다. [!DNL Mixpanel] SDK를 사용하지 않는 경우 사용자 식별 이벤트가 발생할 때 적절한 이벤트와 `distinct_id` 값이 [!DNL Mixpanel](으)로 전송되도록 하려면 [별도의 ID 추적 규칙을 만들기](#create-an-identity-tracking-rule)해야 합니다.

## [!DNL Mixpanel] 내의 데이터 유효성 검사 {#validate}

구현이 성공하고 이벤트가 수집되면 [[!DNL Mixpanel] 콘솔](https://help.mixpanel.com/hc/en-us/articles/4402837164948)에서 이벤트가 표시됩니다.

[!DNL Mixpanel]이(가) 전자 메일 값으로 채워진 게시물 로그인 이벤트와 **[!UICONTROL 이벤트 보내기]**&#x200B;를 사용할 때 만들어진 이벤트를 병합했는지 확인하십시오. 올바르게 구현되면 [!DNL Mixpanel]이(가) 단일 [사용자 프로필](https://help.mixpanel.com/hc/en-us/articles/115004501966)과(와) 연결합니다.

## 다음 단계

이 안내서에서는 이벤트 전달을 사용하여 전환 이벤트를 [!DNL Mixpanel]에 보내는 방법에 대해 설명합니다. 이 이벤트 전달 확장은 [!DNL Mixpanel] SDK 및 JavaScript API를 활용합니다. 이러한 기본 기술에 대한 자세한 내용은 공식 설명서를 참조하십시오.

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md)를 참조하세요.
