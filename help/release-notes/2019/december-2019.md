---
title: Adobe Experience Platform 릴리스 노트 2019년 12월
description: Adobe Experience Platform의 2019년 12월 릴리스 노트.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2019년 12월 11일**

Adobe Experience Platform의 기존 기능 업데이트:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform 세그멘테이션 서비스는 세그먼트를 빌드하고 대상에서 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. [!DNL Real-Time Customer Profile] 데이터. 이러한 세그먼트는에서 중앙 집중식으로 구성 및 유지 관리됩니다. [!DNL Platform]를 사용하여 모든 Adobe 애플리케이션에서 간편하게 액세스할 수 있습니다.

[!DNL Segmentation Service] 은 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계학적 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 의 병합된 대상자 탭 [!DNL Segment Builder] | 다음 [!UICONTROL 세그먼트] 및 [!UICONTROL 대상] 의 탭 [!DNL Segment Builder] 이(가) 하나로 결합되었습니다. [!UICONTROL 대상] 탭. 이 탭에서는 기존 대상을 찾아보고 검색할 수 있으며, 그런 다음 규칙 빌더 캔버스로 드래그하여 놓아 새 세그먼트 정의를 만들 수 있습니다. 대상을 참조하면 새 세그먼트 정의에 다음 규칙 논리 세트 중 하나를 추가할 수 있습니다. 대상 멤버십을 규칙으로, 참조된 대상을 정의한 전체 규칙 논리 세트. |
| 병합 정책 선택기의 새 위치 | 에서 병합 정책 선택기의 위치 [!DNL Segment Builder] 이(가) 변경되었습니다. 세그먼트 정의에 대한 병합 정책을 선택하려면 **[!UICONTROL 필드]** 탭을 클릭한 다음 **[!UICONTROL 병합 정책]** 드롭다운 메뉴를 사용하여 사용할 병합 정책을 선택합니다. |

**알려진 문제**

* None

자세한 내용은 다음을 참조하십시오. [세그먼테이션 서비스 개요](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] 에서는 지정된 개인에게 사용 가능한 옵션 세트에서 &quot;다음 최상의 경험&quot;을 프로그래밍 및 지능적으로 선택하고, 이를 모든 채널 또는 애플리케이션에 전달하고, 보고 및 분석을 수행하는 기능을 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| -----------| ---------- |
| 순위 함수 | 이제 프로필에 대한 오퍼 순서는 모든 프로필에서 고정된 오퍼 세트가 아니라 등급 함수를 통해 파생됩니다. |

**알려진 문제**

* None.

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. [!DNL Platform] 서비스. Adobe 솔루션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 스토리지 시스템 및 CRM 서비스를 인증하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ---------- | ------------ |
| 스트리밍 연결 | 스트리밍 수집을 사용하면 클라이언트 및 서버측 장치에서 로 데이터를 보낼 수 있습니다. [!DNL Experience Platform] 실시간으로. 릴리스에는 새로운 스트리밍 연결 사용자 인터페이스가 포함됩니다. |
| 커넥터 지원 [!DNL Google Cloud Store] | 에서 데이터 수집 지원 [!DNL Google Cloud Store]. |

**알려진 문제**

* None.

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md).

## [!DNL Experience Data Model] (XDM) 시스템 {#xdm}

표준화 및 상호 운용성은 핵심 개념입니다 [!DNL Experience Platform]. [!DNL Experience Data Model] Adobe을 기반으로 하는 (XDM)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.

XDM은 디지털 경험의 성능을 개선하기 위해 설계된 공개적으로 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신하는 모든 애플리케이션에 대한 일반적인 구조와 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 더 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 향상된 스키마 유효성 검사 | 참조가 예상대로 추가 필드로 확인되는지 확인하기 위한 새 검사가 수행됩니다. 오브젝트가 완전히 정의되었는지 확인하기 위해 오브젝트 배열로 정의된 필드에 추가 검사를 추가했습니다. 문제를 식별하고 해결하는 데 도움이 되는 오류 메시지가 개선되었습니다. |

**버그 수정**

* 액세스 제어 및 샌드박스와 관련된 유지 관리 및 개선 사항.
* 지원 대상 `eTag` 대상: `/descriptors` 의 엔드포인트 [!DNL Schema Registry] API.

**알려진 문제**

* None

를 사용하여 XDM 작업에 대해 자세히 알아보려면 [!DNL Schema Registry] API 및 [!DNL Schema Editor] 사용자 인터페이스입니다. [XDM 시스템 설명서](../../xdm/home.md).
