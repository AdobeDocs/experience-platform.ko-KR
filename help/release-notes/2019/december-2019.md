---
title: Adobe Experience Platform 릴리스 정보
description: Experience Platform 릴리스 노트
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 7%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜:2019년 12월 11일**

Adobe Experience Platform의 기존 기능 업데이트:

* [[!DNL 세그멘테이션 서비스]](#segmentation)
* [[!DNL 의사 결정 서비스]](#decisioning)
* [[!DNL 소스]](#sources)
* [[!DNL 경험 데이터 모델(XDM) 시스템]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform 세그멘테이션 서비스는 세그먼트를 작성하고 [!DNL Real-time Customer Profile] 데이터에서 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이러한 세그먼트는 중앙에서 구성 및 관리되므로 모든 Adobe 애플리케이션에서 쉽게 액세스할 수 [!DNL Platform]있습니다.

[!DNL Segmentation Service] 고객 기반 내에서 마케팅 가능한 사람들을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(인구 통계 정보 등) 또는 시간 시리즈 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 병합된 대상 탭( [!DNL Segment Builder] | 의 [!UICONTROL 세그먼트] 및 [!UICONTROL 대상] 탭 [!DNL Segment Builder] 이 단일 대상 [!UICONTROL 탭] 으로결합되었습니다. 이 탭에서는 기존 대상을 찾아 검색할 수 있습니다. 이렇게 하면 규칙 빌더 캔버스로 드래그하여 놓아 새 세그먼트 정의를 만들 수 있습니다. 대상을 참조하면 다음 규칙 논리 세트 중 하나를 새 세그먼트 정의에 추가할 수 있습니다.대상 멤버십을 규칙으로, 참조된 대상을 정의하는 전체 규칙 논리 세트입니다. |
| 병합 정책 선택기의 새 위치 | 병합 정책 선택기의 위치가 [!DNL Segment Builder] 변경되었습니다. 세그먼트 정의에 대한 병합 정책을 선택하려면 **[!UICONTROL 필드]** 탭에서 톱니바퀴 아이콘을 클릭한 다음 정책 **[!UICONTROL 병합]** 드롭다운 메뉴를 사용하여 사용할 병합 정책을 선택합니다. |

**알려진 문제**

* None

자세한 내용은 세그멘테이션 [서비스 개요를 참조하십시오](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] 는 특정 개인에 대해 사용 가능한 옵션 세트에서 &quot;다음 최상의 경험&quot;을 프로그래밍 방식으로 지능적으로 선택하고 채널 또는 애플리케이션에 전달하고 보고 및 분석을 수행할 수 있는 기능을 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| 등급 함수 | 이제 프로필에 대한 오퍼 순서는 모든 프로필에 대해 고정된 오퍼 세트가 아닌 등급 함수를 통해 파생됩니다. |

**알려진 문제**

* None.

서비스에 대한 [자세한 내용은 의사 결정 서비스 개요를](../../decisioning-service/home.md) 참조하십시오.

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 솔루션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 접속을 통해 스토리지 시스템 및 CRM 서비스에 대한 인증, 통합 실행 시간 설정, 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ---------- | ------------ |
| 스트리밍 연결 | 스트리밍 통합 기능을 사용하면 클라이언트 및 서버측 디바이스에서 실시간으로 데이터를 전송할 수 [!DNL Experience Platform] 있습니다. 새로운 스트리밍 연결 사용자 인터페이스가 출시됩니다. |
| 커넥터 지원 [!DNL Google Cloud Store] | 데이터 수집 지원 [!DNL Google Cloud Store]. |

**알려진 문제**

* None.

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).

## [!DNL Experience Data Model] (XDM) 시스템 {#xdm}

표준화와 상호 운용성은 그 이면의 핵심 개념입니다 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

XDM은 디지털 경험의 강력함을 향상시키도록 고안된 공개적으로 문서화된 사양입니다. 이 소프트웨어는 Adobe Experience Platform의 서비스와 통신하기 위해 모든 애플리케이션에 대한 공통 구조와 정의를 제공합니다. 모든 고객 경험 데이터는 XDM 표준을 준수하여 보다 빠르고 통합된 방식으로 인사이트를 제공하는 공통 표현에 통합할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고 세그먼트를 통해 고객 고객을 정의하며 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 향상된 스키마 유효성 검사 | 새 확인은 참조가 예상대로 추가 필드로 확인되는지 확인합니다. 개체가 완전히 정의되어 있는지 확인하기 위해 개체 배열로 정의된 필드에 추가 검사를 추가했습니다. 문제를 식별하고 수정하는 데 도움이 되는 오류 메시지가 개선되었습니다. |

**버그 수정**

* 액세스 제어 및 샌드박스와 관련된 유지 관리 및 개선 사항.
* API `eTag` 에서 `/descriptors` 종단점에 대한 [!DNL Schema Registry] 지원.

**알려진 문제**

* None

API 및 사용자 인터페이스를 사용하여 XDM을 사용하는 방법에 대한 자세한 내용은 [!DNL Schema Registry] XDM 시스템 설명서를 참조하십시오 [!DNL Schema Editor] [](../../xdm/home.md).