---
keywords: Experience Platform;홈;인기 항목;Audience Manager 커넥터;Audience Manager;audience manager
solution: Experience Platform
title: Audience Manager Source 개요
description: Adobe Audience Manager 소스는 Audience Manager에서 수집된 자사 데이터를 Adobe Experience Platform으로 스트리밍합니다.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 1%

---

# Audience Manager 소스

>[!IMPORTANT]
>
>초기 설정에서 Adobe Audience Manager 소스는 지정된 `namespaceCode={VALUE}`의 ID 네임스페이스가 없음을 설명하는 오류 메시지를 반환합니다. **참고**: 백 엔드에서 `namespaceCode`은(는) ID 기호를 참조하는 데 사용됩니다. 통합을 완료하려면 다음을 수행해야 합니다.
>
>- [지정된 ID 기호(`VALUE`)를 사용하여 ID 서비스에서 사용자 지정 네임스페이스를 만듭니다](../../../identity-service/features/namespaces.md#create-custom-namespaces).
>- 데이터를 다시 수집합니다.

Adobe Audience Manager 소스는 Adobe Experience Platform 활성화를 위해 Adobe Audience Manager에서 수집된 자사 데이터를 스트리밍합니다. Audience Manager 소스는 두 가지 유형의 데이터를 Experience Platform에 수집합니다.

- **실시간 데이터:** Audience Manager의 데이터 수집 서버에서 실시간으로 캡처된 데이터입니다. 이 데이터는 Audience Manager에서 규칙 기반 트레이트를 채우는 데 사용되며 가장 짧은 지연 시간 내에 Experience Platform에 표시됩니다.
- **프로필 데이터:** Audience Manager은 실시간 및 온보딩된 데이터를 사용하여 고객 프로필을 파생합니다. 이러한 프로필은 세그먼트 실현에서 ID 그래프 및 트레이트를 채우는 데 사용됩니다.

Audience Manager 소스는 이러한 데이터 유형을 XDM(Experience Data Model) 스키마에 매핑한 다음 Experience Platform에 보냅니다. 실시간 데이터는 XDM ExperienceEvent 데이터로 전송되고 프로필 데이터는 XDM 개별 프로필 데이터로 전송됩니다.

자세한 내용은 [UI에서 Audience Manager 소스 연결 만들기](../../tutorials/ui/create/adobe-applications/audience-manager.md)에 대한 안내서를 참조하십시오.

## XDM(경험 데이터 모델)이란 무엇입니까?

XDM은 Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 고객 경험 데이터를 균일하게 통합할 수 있으므로 데이터를 더 쉽게 전달하고 정보를 수집할 수 있습니다.

Experience Platform에서 XDM을 사용하는 방법에 대한 자세한 내용은 [XDM 시스템 개요](../../../xdm/home.md)를 참조하십시오. 프로필과 이벤트 간에 XDM 스키마를 구조화하는 방법에 대한 자세한 내용은 [스키마 구성 기본 사항](../../../xdm/schema/composition.md)을 참조하세요.

## XDM 스키마 예

다음은 Experience Platform의 XDM ExperienceEvent 및 XDM 개인 프로필에 매핑된 Audience Manager 구조의 예입니다.

### ExperienceEvent - 실시간 데이터 및 온보딩된 데이터용

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM 개인 프로필 - 프로필 데이터용

![](images/aam-profile-xdm-for-profile-data.png)

필드를 Audience Manager에서 XDM으로 매핑하는 방법에 대한 자세한 내용은 [Audience Manager 매핑 필드](./mapping/audience-manager.md)에 대한 설명서를 참조하십시오.

## Experience Platform에서 데이터 관리

### 데이터 세트

데이터 집합은 스키마(열) 및 필드(행)를 포함하며 데이터 연결에서 사용할 수 있는 데이터 수집을 위한 저장소 및 관리 구성으로서, 일반적으로 테이블입니다. Audience Manager 데이터는 실시간 데이터, 인바운드 데이터 및 프로필 데이터로 구성됩니다. Audience Manager 데이터 세트를 찾으려면 각 데이터 유형에 대해 제공된 이름 지정 규칙과 함께 UI의 검색 기능을 사용하십시오.

Audience Manager 데이터 세트는 기본적으로 프로필에 대해 비활성화되며 사용자는 사용 사례에 따라 데이터 세트를 활성화 또는 비활성화할 수 있습니다. 프로필의 세그먼트 멤버십에 사용할 데이터 세트를 비활성화하지 않는 것이 좋습니다.

>[!NOTE]
>
>AAM 실시간 은 데이터 레이크로 이동하는 유일한 데이터 세트입니다. 다른 모든 Audience Manager 데이터 세트가 [!DNL Profile]에 대해 활성화된 경우 [!DNL Profile]&#x200B;(으)로 이동합니다. [!DNL Profile]에 대해 활성화되지 않은 경우 데이터가 수신되지 않으며 비어 있는 것으로 표시됩니다.

| 데이터 세트 이름 | 설명 | 클래스 |
| --- | --- | --- |
| AAM 실시간 | 이 데이터 세트에는 Audience Manager DCS 종단점 및 Audience Manager 프로필에 대한 ID 맵에서 직접 히트에 의해 수집된 데이터가 포함되어 있습니다. 프로필 수집을 위해 이 데이터 세트를 활성화 상태로 유지합니다. | 경험 이벤트 |
| AAM 실시간 프로필 업데이트 | 이 데이터 세트를 사용하면 Audience Manager 트레이트 및 세그먼트를 실시간으로 타깃팅할 수 있습니다. 여기에는 Edge 지역 라우팅, 트레이트 및 세그먼트 멤버십에 대한 정보가 포함됩니다. 프로필 수집을 위해 이 데이터 세트를 활성화 상태로 유지합니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. **[!UICONTROL 프로필]** 토글을 활성화하여 데이터를 프로필로 직접 수집할 수 있습니다. | 레코드 |
| AAM 장치 데이터 | Audience Manager에서 집계된 ECID 및 해당 세그먼트 실현이 있는 장치 데이터. 데이터는 데이터 세트에 배치로 표시되지 않습니다. **[!UICONTROL 프로필]** 토글을 활성화하여 데이터를 프로필로 직접 수집할 수 있습니다. | 레코드 |
| AAM 장치 프로필 데이터 | Audience Manager 커넥터 진단에 사용됩니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. **[!UICONTROL 프로필]** 토글을 활성화하여 데이터를 프로필로 직접 수집할 수 있습니다. | 레코드 |
| AAM 인증된 프로필 | 이 데이터 세트에는 Audience Manager 인증된 프로필이 포함되어 있습니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. **[!UICONTROL 프로필]** 토글을 활성화하여 데이터를 프로필로 직접 수집할 수 있습니다. | 레코드 |
| AAM 인증된 프로필 메타데이터 | Audience Manager 커넥터 진단에 사용됩니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. **[!UICONTROL 프로필]** 토글을 활성화하여 데이터를 프로필로 직접 수집할 수 있습니다. | 레코드 |
| AAM 장치 데이터 채우기 | 이전 장치 데이터를 가져올 때의 데이터 세트입니다. 여기에는 Audience Manager에서 집계된 ECID 및 해당 세그먼트 실현이 포함됩니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. **[!UICONTROL 프로필]** 전환을 활성화하여 데이터를 프로필로 직접 수집할 수 있습니다. | 레코드 |
| AAM 인증된 프로필 채우기 | 과거 인증된 데이터를 가져올 때의 데이터 세트입니다. 여기에는 Audience Manager 인증된 프로필이 포함됩니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. **[!UICONTROL 프로필]** 전환을 활성화하여 데이터를 프로필로 직접 수집할 수 있습니다. | 레코드 |

### 연결

Adobe Audience Manager은 카탈로그에 하나의 연결(Audience Manager 연결)을 만듭니다. 카탈로그는 Adobe Experience Platform 내의 데이터 위치와 계보에 대한 레코드 시스템입니다. 연결은 커넥터의 고객별 인스턴스인 카탈로그 개체입니다. 카탈로그, 연결 및 커넥터에 대한 자세한 내용은 [카탈로그 서비스 개요](../../../catalog/home.md)를 참조하십시오.

### 세그먼트 모집단과 프로필 영향

세그먼트 모집단 크기는 처음 Audience Manager 세그먼트를 Experience Platform으로 보낼 때 프로필 번호에 직접적인 영향을 줍니다. 즉, 모든 세그먼트를 선택하면 라이선스 사용 권한을 초과하는 프로필 초과가 발생할 수 있습니다. Experience Platform은 또한 프로필 수집을 위해 새 데이터와 이전 데이터를 구별합니다. 자사 기반 ID가 100개인 세그먼트는 100개의 프로필을 만듭니다. 그러나 동일한 세그먼트의 모집단을 150명으로 늘리고 Experience Platform에 수집한 경우 새 프로필이 50개뿐이므로 프로필 수는 50개만 증가합니다.

[라이선스 사용 대시보드](../../../dashboards/guides/license-usage.md)를 통해 계정의 사용 가능한 프로필 사용을 확인할 수도 있습니다.

## Experience Platform에서 Audience Manager 데이터의 예상 대기 시간은 어떻게 됩니까?

| Audience Manager 데이터 | 유형 | 지연 | 참고 |
| --- | --- | --- | --- |
| 실시간 데이터 | 이벤트 | &lt;25분 | Audience Manager Edge 노드에서 캡처되어 데이터 레이크에 표시되기까지의 시간입니다. |
| 실시간 데이터 | 프로필 업데이트 | &lt;10분 | 실시간 고객 프로필에 도착하는 시간입니다. |
| 실시간 및 온보딩된 데이터 | 프로필 업데이트 | 24-36시간 | DCS/PCS Edge 데이터 및 온보딩된 데이터를 통해 캡처되어 사용자 프로필로 처리된 후 실시간 고객 프로필에 나타나는 시간. 현재 이 데이터는 데이터 레이크에 직접 도달하지 않습니다. Audience Manager 프로필 데이터 세트에 대해 프로필 토글을 활성화하여 이 데이터를 실시간 고객 프로필로 직접 수집할 수 있습니다. |
