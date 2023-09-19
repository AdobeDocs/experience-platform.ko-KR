---
keywords: 이벤트 전달 확장;mixpanel;mixpanel 이벤트 전달 확장
title: Mixpanel 추적 이벤트 API 이벤트 전달 확장
description: 이 Adobe Experience Platform 이벤트 전달 확장은 Edge Network 이벤트를 Mixpanel로 보냅니다.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API 이벤트 전달 확장

[[!DNL Mixpanel]](https://www.mixpanel.com) 는 사용자가 디지털 제품과 상호 작용하는 방법에 대한 데이터를 캡처할 수 있도록 하는 제품 분석 도구입니다. 몇 번의 클릭만으로 데이터를 쿼리하고 시각화할 수 있는 간단한 대화형 보고서를 사용하여 제품 데이터를 분석할 수 있습니다. [!DNL Mixpanel] 모든 사람이 실시간으로 사용자 데이터를 분석하여 트렌드를 식별하고, 사용자 행동을 이해하고, 제품에 대한 결정을 내릴 수 있도록 하여 팀을 보다 효율적으로 만들 수 있도록 설계되었습니다.

[!DNL Mixpanel] 에서는 각 상호 작용을 단일 사용자에게 연결하는 이벤트 기반의 사용자 중심 모델을 사용합니다. 다음 [!DNL Mixpanel] 데이터 모델은 사용자, 이벤트 및 속성의 개념을 기반으로 합니다.

>[!NOTE]
>
>다음을 참조하십시오. [!DNL Mixpanel] 설명서 [id 관리](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) 방법을 이해하려면 [!DNL Mixpanel] 이벤트를 병합하여 id 클러스터를 생성합니다. 또한 다음 문서를 검토하는 것이 좋습니다. [고유 ID](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) 이벤트 데이터에서 사용자를 식별하는 데 사용되는 방법을 이해합니다.

## 사용 사례

에서 Edge Network의 데이터를 사용하려면 이 확장 기능을 사용해야 합니다 [!DNL Mixpanel] 제품 분석 기능을 활용하십시오.

예를 들어, 다중 채널 존재(웹 사이트 및 모바일)가 있는 소매 조직을 고려해 보십시오. 조직은 트랜잭션 또는 대화 입력을 해당 플랫폼에서 이벤트 데이터로 캡처하여 로 로드합니다 [!DNL Mixpanel] 이벤트 전달 확장 사용.

그런 다음 분석 팀은 [!DNL Mixpanel's] 데이터 세트를 처리하고 비즈니스 통찰력을 도출하는 기능을 통해 그래프, 대시보드 또는 비즈니스 이해 당사자에게 알릴 수 있는 기타 시각화를 생성할 수 있습니다.

에만 해당되는 사용 사례에 대한 자세한 내용은 [!DNL Mixpanel], 다음 설명서를 참조하십시오.

* [새로 만들기 [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [ [!DNL Mixpanel]란?](https://developer.mixpanel.com/docs)
* [12개 필수 항목 [!DNL Mixpanel] 기능](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] 전제 조건 {#prerequisites-mixpanel}

유효한 권한이 있어야 합니다. [!DNL Mixpanel] 이 확장을 사용하려면 계정을 사용하십시오. 로 이동 [[!DNL Mixpanel] 등록 페이지](https://mixpanel.com/register/) 아직 계정이 없는 경우 등록하고 계정을 만듭니다.

다음을 확인합니다. [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) 설정이 프로젝트에 대해 활성화되어 있습니다. 다음으로 이동 **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** 설정을 전환합니다.

### 의 ID 클러스터 이해 [!DNL Mixpanel]

위치 [!DNL Mixpanel], id 클러스터는 다음 콜렉션을 포함합니다. `distinct_id` 개별 사용자에게 연결되는 값입니다. [!DNL Mixpanel] 는 각 사용자에 대한 id 클러스터를 처리하며 단일 표준 항목을 해결합니다 `distinct_id` 각 클러스터에서 보고에 사용할 수 있습니다. 고유 식별자( 로컬 라고 함)를 포함할 수도 있습니다 `distinct_id`)을 참조하십시오.

[!DNL Mixpanel] 다음 두 가지 방법을 통해 id 클러스터를 확인합니다.

* **식별** : [!DNL Mixpanel] 선택한 식별자를 익명으로 연결합니다. `distinct_id`. 웹 사이트에 [!DNL Mixpanel] SDK가 활성화되면 Platform은 `distinct_id` 현재 로그인되어 있는 사용자에게 할당됩니다.
* **별칭**: [!DNL Mixpanel] 두 개의 비익명 결합 `distinct id`추가 병합 기준이 충족되는 경우 함께 사용됩니다.

>[!NOTE]
>
>다음을 참조하십시오. [!DNL Mixpanel] 문서 날짜 [id 관리](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) 를 참조하십시오.
>
>를 활성화했는지 확인합니다. [[!DNL Mixpanel] id 병합 기능](#prerequisites-mixpanel) id 클러스터가 적절하게 확인되도록 합니다.

### 필요한 구성 세부 정보 수집 {#configuration-details}

Experience Platform을에 연결하려면 [!DNL Mixpanel] 다음 입력이 있어야 합니다.

| 키 유형 | 설명 | 예 |
| --- | --- | --- |
| 프로젝트 토큰 | 와(과) 연결된 프로젝트 토큰 [!DNL Mixpanel] 계정입니다. 다음을 참조하십시오. [!DNL Mixpanel] 설명서 [프로젝트 토큰 찾기](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) 지침을 참조하십시오. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## 설치 및 구성 [!DNL Mixpanel] 확장 {#install}

확장을 설치하려면 [이벤트 전달 속성 만들기](../../../ui/event-forwarding/overview.md#properties) 또는 편집할 기존 속성을 대신 선택하십시오.

선택 **[!UICONTROL 확장]** 왼쪽 탐색. 다음에서 **[!UICONTROL 카탈로그]** 탭, 선택 **[!UICONTROL 설치]** 카드 사용 [!DNL Mixpanel] 확장명.

![설치 [!DNL Mixpanel] 확장명.](../../../images/extensions/server/mixpanel/install-extension.png)

## 만들기 [!DNL Send Event] 규칙

이벤트 전달 속성에서 새 규칙 만들기를 시작합니다. 아래 **[!UICONTROL 작업]**, 새 작업을 추가하고 확장을 로 설정합니다. **[!UICONTROL Mixpanel]**. 그런 다음 작업 유형을 다음으로 설정합니다. **[!UICONTROL 이벤트 추적]** 에지 네트워크 이벤트를 (으)로 보내기 [!DNL Mixpanel].

| 입력 | 설명 | 필수 여부 |
| --- | --- | --- |
| [!UICONTROL 프로젝트 토큰] | 이 필드는 와(과) 연결된 프로젝트 토큰에 매핑되어야 합니다. [!DNL Mixpanel] 계정입니다. | 예 |
| [!UICONTROL 이벤트 유형] | 이벤트 이름. | 예 |
| [!UICONTROL 이벤트 시간] | 이벤트 시간. | |
| [!UICONTROL Mixpanel 고유 ID] | 이벤트를 수행한 사용자의 고유 식별자입니다. | |
| [!UICONTROL ID 삽입] | 중복 제거에 사용되는 이벤트의 고유 식별자입니다. | |
| [!UICONTROL 이벤트 속성] | 이벤트의 사용자 지정 속성이 포함된 JSON 개체입니다. 원시 JSON을 제공하거나 간소화된 키-값 입력 세트를 사용하여 선택하십시오. | |

>[!NOTE]
>
>의 표준 필드에 대한 자세한 내용은 [!DNL Mixpanel] 이벤트를 보려면 [공식 문서](https://developer.mixpanel.com/reference/import-events#event).

![이벤트 전달 규칙 작업 구성을 추가합니다.](../../../images/extensions/server/mixpanel/track-event-action.png)

한 번 [!UICONTROL 이벤트 추적] 작업이 규칙에 추가되고, 특정 이벤트에 대해서만 실행되도록 규칙의 조건을 구성하거나, 조건 섹션을 비워 두어 모든 이벤트에 대해 규칙이 실행되도록 할 수 있습니다.

>[!IMPORTANT]
>
>웹 사이트에서 [!DNL Mixpanel] SDK의 다음 단계를 계속할 수 있습니다. [내에서 데이터 유효성 검사 [!DNL Mixpanel]](#validate). 를 사용하지 않는 경우 [!DNL Mixpanel] SDK, 다음을 수행해야 합니다. [별도의 id 추적 규칙 만들기](#create-an-identity-tracking-rule) 적절한 이벤트 및 `distinct_id` 값이 (으)로 전송됩니다. [!DNL Mixpanel] 사용자 식별 이벤트가 발생하는 경우.

## 내에서 데이터 유효성 검사 [!DNL Mixpanel] {#validate}

구현이 성공하고 이벤트가 수집되면 [[!DNL Mixpanel] 콘솔](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

다음을 확인: [!DNL Mixpanel] 은 이메일 값으로 채워진 게시물 로그인 이벤트와 을 사용할 때 생성된 이벤트를 병합했습니다 **[!UICONTROL 이벤트 보내기]**. 올바르게 구현된 경우 [!DNL Mixpanel] 은(는) 이들을 싱글과 연결합니다. [사용자 프로필](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## 다음 단계

이 안내서에서는 전환 이벤트를에 보내는 방법을 다룹니다. [!DNL Mixpanel] 이벤트 전달을 사용합니다. 이 이벤트 전달 확장은 [!DNL Mixpanel] SDK 및 JavaScript API. 이러한 기본 기술에 대한 자세한 내용은 공식 설명서를 참조하십시오.

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md).
