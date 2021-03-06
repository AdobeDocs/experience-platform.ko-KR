---
keywords: Experience Platform;홈;인기 항목;Audience Manager 커넥터;Audience Manager;audience manager
solution: Experience Platform
title: Audience Manager 소스 커넥터 개요
topic-legacy: overview
description: Adobe Audience Manager 소스 커넥터는 Audience Manager에 수집된 자사 데이터를 Adobe Experience Platform으로 스트리밍합니다.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: d0b6885b6e8606692cfe1173b75c7d3537800a5f
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Audience Manager 커넥터

Adobe Audience Manager 데이터 커넥터는 Adobe Audience Manager에 수집된 자사 데이터를 Adobe Experience Platform으로 스트리밍합니다. Audience Manager 커넥터는 Platform에 두 가지 데이터 카테고리를 수집합니다.

- **실시간 데이터:** Audience Manager의 데이터 수집 서버에서 실시간으로 캡처된 데이터. 이 데이터는 Audience Manager에서 규칙 기반 트레이트를 채우는 데 사용되며 지연 시간이 가장 짧습니다.
- **프로필 데이터:** Audience Manager은 실시간 및 온보딩된 데이터를 사용하여 고객 프로필을 유도합니다. 이러한 프로필은 세그먼트 실현에서 ID 그래프와 트레이트를 채우는 데 사용됩니다.

Audience Manager 커넥터는 이러한 데이터 카테고리를 XDM(Experience Data Model) 스키마에 매핑하여 Platform으로 보냅니다. 실시간 데이터는 XDM ExperienceEvent 데이터로 전송되고 프로필 데이터는 XDM 개별 프로필로 전송됩니다.

플랫폼 UI를 사용하여 Adobe Audience Manager과 연결을 만드는 방법에 대한 지침은 [Audience Manager 커넥터 자습서](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## XDM(Experience Data Model)이란 무엇입니까?

XDM은 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 고객 경험 데이터를 균일하게 통합할 수 있으므로 데이터를 쉽게 전달하고 정보를 수집할 수 있습니다.

Experience Platform에서 XDM을 사용하는 방법에 대한 자세한 내용은 [XDM 시스템 개요](../../../xdm/home.md). 프로필 및 ExperienceEvent와 같은 XDM 스키마 구성 방법에 대한 자세한 내용은 다음을 참조하십시오. [스키마 구성 기본 사항](../../../xdm/schema/composition.md).

## XDM 스키마 예

다음은 Platform의 XDM ExperienceEvent 및 XDM 개별 프로필에 매핑된 Audience Manager 구조의 예입니다.

### ExperienceEvent - 실시간 데이터 및 온보딩된 데이터용

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM 개별 프로필 - 프로필 데이터용

![](images/aam-profile-xdm-for-profile-data.png)

## Adobe Audience Manager에서 XDM으로 필드를 매핑하려면 어떻게 해야 합니까?

다음에 대한 설명서를 참조하십시오. [Audience Manager 매핑 필드](./mapping/audience-manager.md) 추가 정보.

## 플랫폼의 데이터 관리

### 데이터 세트

데이터 세트는 스키마(열) 및 필드(행)를 포함하고 데이터 연결에서 사용할 수 있는 데이터 수집을 위한 저장소 및 관리 구성입니다. Audience Manager 데이터는 실시간 데이터, 인바운드 데이터 및 프로필 데이터로 구성됩니다. Audience Manager 데이터 세트를 찾으려면 UI에서 각 데이터 유형에 대해 제공된 이름 지정 규칙과 함께 검색 함수를 사용합니다.

Audience Manager 데이터 세트는 기본적으로 프로필에 대해 비활성화되며 사용자는 사용 사례를 기반으로 데이터 세트를 활성화 또는 비활성화할 수 있습니다. 프로필에서 세그먼트 멤버십에 사용할 데이터 세트를 비활성화하지 않는 것이 좋습니다.

>[!NOTE]
>
>AAM 실시간 은 [!DNL Data Lake]. 다른 모든 Audience Manager 데이터 세트는 [!DNL Profile]에 대해 활성화되어 있을 경우 [!DNL Profile]. 활성화되지 않은 경우 [!DNL Profile]로 설정되면 데이터가 수신되지 않고 빈 것으로 표시됩니다.

| 데이터 집합 이름 | 설명 | 클래스 |
| --- | --- | --- |
| AAM 실시간 | 이 데이터 세트에는 Audience Manager DCS 끝점의 직접 히트에서 수집한 데이터와 Audience Manager 프로필의 ID 맵이 포함되어 있습니다. 이 데이터 세트를 프로필 통합에 사용하도록 설정합니다. | 경험 이벤트 |
| AAM 실시간 프로필 업데이트 | 이 데이터 세트를 사용하면 Audience Manager 트레이트 및 세그먼트를 실시간 타깃팅할 수 있습니다. 여기에는 Edge 지역 라우팅, 트레이트 및 세그먼트 멤버십에 대한 정보가 포함되어 있습니다. 이 데이터 세트를 프로필 통합에 사용하도록 설정합니다. 데이터는 데이터 집합에 배치로 표시되지 않습니다. 을(를) 활성화할 수 있습니다 **[!UICONTROL 프로필]** 를 전환하여 데이터를 프로필에 직접 수집할 수 있습니다. | 레코드 |
| AAM 장치 데이터 | ECID 및 해당 세그먼트 실현을 Audience Manager에서 집계한 상태로 사용하는 장치 데이터. 데이터는 데이터 집합에 배치로 표시되지 않습니다. 을(를) 활성화할 수 있습니다 **[!UICONTROL 프로필]** 를 전환하여 데이터를 프로필에 직접 수집할 수 있습니다. | 레코드 |
| AAM 장치 프로필 데이터 | Audience Manager 커넥터 진단에 사용됩니다. 데이터는 데이터 집합에 배치로 표시되지 않습니다. 을(를) 활성화할 수 있습니다 **[!UICONTROL 프로필]** 를 전환하여 데이터를 프로필에 직접 수집할 수 있습니다. | 레코드 |
| AAM 인증된 프로필 | 이 데이터 세트에는 Audience Manager 인증된 프로필이 포함되어 있습니다. 데이터는 데이터 집합에 배치로 표시되지 않습니다. 을(를) 활성화할 수 있습니다 **[!UICONTROL 프로필]** 를 전환하여 데이터를 프로필에 직접 수집할 수 있습니다. | 레코드 |
| AAM 인증된 프로필 메타데이터 | Audience Manager 커넥터 진단에 사용됩니다. 데이터는 데이터 집합에 배치로 표시되지 않습니다. 을(를) 활성화할 수 있습니다 **[!UICONTROL 프로필]** 를 전환하여 데이터를 프로필에 직접 수집할 수 있습니다. | 레코드 |
| AAM 장치 데이터 채우기 | 데이터 세트가 이전 장치 데이터를 가져올 수 없습니다. 여기에는 Audience Manager에서 집계된 ECID 및 해당 세그먼트 실현을 포함합니다. 데이터는 데이터 집합에 배치로 표시되지 않습니다. 을(를) 활성화할 수 있습니다 **[!UICONTROL 프로필]** 데이터를 프로필에 직접 수집하도록 전환합니다. | 레코드 |
| AAM 인증된 프로필 채우기 | 데이터 세트가 이전에 인증된 데이터를 가져올 수 없습니다. 여기에는 Audience Manager 인증된 프로필이 포함되어 있습니다. 데이터는 데이터 집합에 배치로 표시되지 않습니다. 을(를) 활성화할 수 있습니다 **[!UICONTROL 프로필]** 데이터를 프로필에 직접 수집하도록 전환합니다. | 레코드 |

### 연결

Adobe Audience Manager은 카탈로그에서 하나의 연결을 만듭니다. Audience Manager 연결. 카탈로그는 Adobe Experience Platform 내의 데이터 위치 및 계열에 대한 레코드 시스템입니다. 연결은 Connectors의 고객별 인스턴스인 Catalog 개체입니다. 자세한 내용은 [카탈로그 서비스 개요](../../../catalog/home.md) 카탈로그, 연결 및 커넥터에 대한 자세한 정보.

## 플랫폼에서 Audience Manager 데이터의 예상 대기 시간은 얼마입니까?

| Audience Manager 데이터 | 지연 | 참고 |
| --- | --- | --- |
| 실시간 데이터 | &lt; 35분. | Audience Manager 에지 노드에서 Platform Data Lake에 나타나는 데 걸리는 시간입니다. |
| 프로필 데이터 | &lt; 2일 | DCS/PCS Edge 데이터 및 온보딩된 데이터를 통해 캡처되고 사용자 프로필로 처리되고 프로필에 표시되는 시간입니다. 이 데이터는 현재 Platform Data Lake에 직접 도착하지 않습니다. Audience Manager 프로필 데이터 세트에 대해 프로필 전환을 활성화하여 이 데이터를 프로필에 직접 수집할 수 있습니다. |
