---
keywords: Experience Platform;홈;인기 항목;Audience Manager 커넥터;대상 관리자;대상 관리자
solution: Experience Platform
title: Audience Manager 소스 커넥터 개요
topic-legacy: overview
description: Adobe Audience Manager 소스 커넥터는 Audience Manager에서 수집한 자사 데이터를 Adobe Experience Platform으로 스트리밍합니다.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Audience Manager 커넥터

Adobe Audience Manager 데이터 커넥터는 Adobe Audience Manager에서 수집한 자사 데이터를 Adobe Experience Platform으로 스트리밍합니다. Audience Manager 커넥터는 두 가지 데이터 카테고리를 플랫폼으로 인제스트합니다.

- **실시간 데이터: Audience Manager의** 데이터 수집 서버에서 실시간으로 캡처되는 데이터. 이 데이터는 Audience Manager에서 규칙 기반 트레이트를 채우는 데 사용되며 짧은 지연 시간 내에 플랫폼에 표시됩니다.
- **프로필 데이터:** Audience Manager은 실시간 및 온보드 데이터를 사용하여 고객 프로필을 추출합니다. 이러한 프로필은 세그먼트 할당에서 ID 그래프와 트레이트를 채우는 데 사용됩니다.

Audience Manager 커넥터는 이러한 데이터 카테고리를 XDM(Experience Data Model) 스키마에 매핑하여 플랫폼으로 보냅니다. 실시간 데이터는 XDM ExperienceEvent 데이터로 전송되고 프로필 데이터는 XDM 개별 프로필로 전송됩니다.

플랫폼 UI를 사용하여 Adobe Audience Manager와의 연결을 만드는 방법에 대한 지침은 [Audience Manager 커넥터 자습서](../../tutorials/ui/create/adobe-applications/audience-manager.md)를 참조하십시오.

## XDM(Experience Data Model) 소개

XDM은 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 고객 경험 데이터를 일관되게 통합할 수 있으므로 데이터를 손쉽게 전달하고 정보를 수집할 수 있습니다.

Experience Platform에서 XDM을 사용하는 방법에 대한 자세한 내용은 [XDM 시스템 개요](../../../xdm/home.md)를 참조하십시오. 프로필 및 ExperienceEvent와 같은 XDM 스키마가 구조화되는 방법에 대한 자세한 내용은 스키마 구성](../../../xdm/schema/composition.md)의 [기본 사항을 참조하십시오.

## XDM 스키마 예

다음은 플랫폼의 XDM ExperienceEvent 및 XDM 개별 프로필에 매핑된 Audience Manager 구조의 예입니다.

### ExperienceEvent - 실시간 데이터 및 온보드 데이터

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM 개별 프로필 - 프로필 데이터

![](images/aam-profile-xdm-for-profile-data.png)

## Adobe Audience Manager에서 XDM으로 필드를 매핑하는 방법은 무엇입니까?

자세한 내용은 [Audience Manager 매핑 필드](./mapping/audience-manager.md)에 대한 설명서를 참조하십시오.

## 플랫폼의 데이터 관리

### 데이터 세트

데이터 집합은 스키마(열) 및 필드(행)를 포함하고 데이터 연결에 의해 사용 가능한 데이터 수집을 위한 저장 및 관리 구성체입니다. Audience Manager 데이터는 실시간 데이터, 인바운드 데이터 및 프로필 데이터로 구성됩니다. Audience Manager 데이터 세트를 찾으려면 UI에서 각 데이터 유형에 대해 제공된 이름 지정 규칙과 함께 검색 함수를 사용합니다.

Audience Manager 데이터 세트는 기본적으로 프로필에 대해 비활성화되며 사용자는 사용 사례에 따라 데이터 세트를 활성화하거나 비활성화할 수 있습니다. 프로필의 세그먼트 멤버십에 사용할 데이터 세트를 비활성화하는 것은 권장되지 않습니다.

| 데이터 세트 이름 | 설명 |
| ------------ | ----------- |
| AAM 실시간 | 이 데이터 집합은 Audience Manager DCS 끝점의 직접 히트 수 및 Audience Manager 프로필의 ID 맵에서 수집한 데이터를 포함합니다. 이 데이터 세트를 프로필 수집에 사용하도록 설정합니다. |
| AAM 실시간 프로필 업데이트 | 이 데이터 세트를 사용하면 Audience Manager 트레이트와 세그먼트를 실시간으로 타깃팅할 수 있습니다. 여기에는 Edge 지역 라우팅, 트레이트 및 세그먼트 멤버십에 대한 정보가 포함되어 있습니다. 이 데이터 세트를 프로필 수집에 사용하도록 설정합니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. 데이터를 프로필에 직접 인제스트하려면 **[!UICONTROL Profile]** 토글을 활성화할 수 있습니다. |
| AAM 장치 데이터 | Audience Manager에서 집계된 ECID 및 해당 세그먼트 합산이 있는 장치 데이터 데이터는 데이터 세트에 배치로 표시되지 않습니다. 데이터를 프로필에 직접 인제스트하려면 **[!UICONTROL Profile]** 토글을 활성화할 수 있습니다. |
| AAM 장치 프로파일 데이터 | Audience Manager 커넥터 진단에 사용됩니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. 데이터를 프로필에 직접 인제스트하려면 **[!UICONTROL Profile]** 토글을 활성화할 수 있습니다. |
| AAM 인증된 프로필 | 이 데이터 세트에 인증된 Audience Manager 프로필이 포함되어 있습니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. 데이터를 프로필에 직접 인제스트하려면 **[!UICONTROL Profile]** 토글을 활성화할 수 있습니다. |
| AAM 인증된 프로필 메타 데이터 | Audience Manager 커넥터 진단에 사용됩니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. 데이터를 프로필에 직접 인제스트하려면 **[!UICONTROL Profile]** 토글을 활성화할 수 있습니다. |
| AAM 장치 데이터 채우기 | 이전 디바이스 데이터를 가져올 수 없는 데이터 세트 여기에는 Audience Manager에서 집계된 ECID 및 해당 세그먼트 할당이 포함됩니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. 데이터를 프로필에 직접 인제스트하도록 **[!UICONTROL Profile]** 토글을 활성화할 수 있습니다. |
| AAM 인증된 프로필 채우기 | 인증된 이전 데이터를 가져올 수 없는 데이터 집합입니다. 여기에는 Audience Manager 인증 프로파일이 포함됩니다. 데이터는 데이터 세트에 배치로 표시되지 않습니다. 데이터를 프로필에 직접 인제스트하도록 **[!UICONTROL Profile]** 토글을 활성화할 수 있습니다. |

### 연결

Adobe Audience Manager은 카탈로그에서 하나의 연결을 만듭니다.Audience Manager 연결. Catalog는 Adobe Experience Platform 내의 데이터 위치 및 계열에 대한 레코드 시스템입니다. 연결은 Connectors의 고객별 인스턴스인 Catalog 객체입니다. 카탈로그, 연결 및 커넥터에 대한 자세한 내용은 [카탈로그 서비스 개요](../../../catalog/home.md)를 참조하십시오.

## 플랫폼의 Audience Manager 데이터에 대한 예상 지연은 무엇입니까?

| Audience Manager 데이터 | 지연 | 참고 |
| --- | --- | --- |
| 실시간 데이터 | &lt; 35분. | Audience Manager 에지 노드에서 캡처되는 시간에서부터 플랫폼 데이터 레이크에 나타나는 시간입니다. |
| 프로필 데이터 | &lt; 2일 | DCS/PCS Edge 데이터 및 온보드 데이터를 통해 캡처된 후 사용자 프로필로 처리된 후 프로필에 나타나는 시간 이 데이터는 현재 Platform Data Lake에 직접 포함되지 않습니다. 프로필 전환을 사용하여 Audience Manager 프로필 데이터 세트에서 이 데이터를 프로필에 직접 인제스트할 수 있습니다. |
