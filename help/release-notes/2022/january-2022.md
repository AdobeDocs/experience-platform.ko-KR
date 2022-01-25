---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
source-git-commit: 641fcab89b849d91a075fa5058421950bc7fecd7
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 9%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 1월 26일**

Adobe Experience Platform의 기존 기능 업데이트:

- [경고](#alerts)
- [데이터 준비](#data-prep)
- [샌드박스](#sandboxes)
- [세분화 서비스](#segmentation)

## 경고 {#alerts}

Experience Platform을 사용하면 다양한 플랫폼 활동에 대한 이벤트 기반 경고를 구독할 수 있습니다. 을 통해 다른 경고 규칙에 가입할 수 있습니다 [!UICONTROL 경고] 플랫폼 사용자 인터페이스의 탭. 및 UI 자체 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 경고 규칙 | 이제 데이터 수집, ID, 프로필, 세그멘테이션 및 활성화와 관련된 워크플로우에 여러 가지 새로운 경고 규칙을 사용할 수 있습니다. 다음 사항에 대한 개요를 참조하십시오. [경고 규칙](../../observability/alerts/rules.md) 를 참조하십시오. |

Platform의 경고에 대한 자세한 내용은 [경고 개요](../../observability/alerts/overview.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 통합 매핑 경험 | Platform UI의 새로운 매핑 인터페이스는 지능형 매핑 권장 사항을 활용하고, 매핑 규칙을 수동으로 구성하고, 매핑 세트에 발생하는 모든 오류를 디버깅하는 일관된 매핑 경험을 제공합니다. 자세한 내용은 [[!DNL Data Prep] UI 안내서](../../data-prep/home.md). |

자세한 내용은 [!DNL Data Prep]를 보려면 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 디지털 경험 애플리케이션을 전 세계에 맞게 보강하기 위해 제작되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 운영하고 있으며 운영 규정을 준수하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 충족해야 합니다. 이러한 요구 사항을 해결하기 위해 Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스 를 제공합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 UI 개선 사항 | 이제 샌드박스 표시기가 모든 Platform UI 애플리케이션의 헤더 내에 통합됩니다. 샌드박스 표시기에는 샌드박스 이름, 영역 및 유형이 표시되며, 드롭다운 메뉴에 액세스하여 샌드박스 간을 전환할 수도 있습니다. 자세한 내용은 [sandbox UI 안내서](../../sandboxes/ui/user-guide.md). |

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md).

## 세분화 서비스 {#segmentation}

[!DNL Segmentation Service] 고객 기반 내의 마케팅 가능한 사람 그룹을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 세그먼트 일치 | 세그먼트 일치 는 두 명 이상의 플랫폼 사용자가 공통 식별자를 기반으로 데이터를 안전하고 제어되며 개인 정보를 보호하는 방식으로 교환할 수 있도록 해주는 데이터 공동 작업 서비스입니다. 자세한 내용은 [세그먼트 일치 개요](../../segmentation/ui/segment-match/overview.md). |

자세한 내용은 [!DNL Segmentation Service]를 보려면 [세그먼테이션 개요](../../segmentation/home.md).
