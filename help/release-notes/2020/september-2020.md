---
title: Adobe Experience Platform 릴리스 정보
description: 'Experience Platform 릴리스 노트: 2020년 9월 9일'
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 23c7a0d82cb849568d6411c1a09c7a16b86d4954
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 5%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 9월 9일**

Adobe Experience Platform의 기존 기능 업데이트:

* [[!DNL 데이터 거버넌스]](#governance)
* [[!DNL 대상]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL 소스]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform 데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략과 기술입니다. 카탈로그 작성, 데이터 계보, 데이터 사용 표시, 데이터 액세스 정책, 마케팅 작업을 위한 데이터 액세스 제어 등 다양한 [!DNL Experience Platform] 수준에서 핵심적인 역할을 합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 세트 레이블 지정 UI 개선 사항 | 큰 스키마 작업을 더 쉽게 하기 위해 데이터 세트 레이블 지정 UI에 새로운 정렬 및 필터링 컨트롤이 추가되었습니다. <ul><li>전체 스키마 경로를 기준으로 필드를 알파벳순으로 정렬합니다.</li><li>필드 경로 이름에 대해 부분 검색을 수행합니다.</li><li>레이블, 선택된 레이블 또는 레이블 카테고리가 없는 필드를 필터링합니다.</li></ul> |

서비스에 대한 자세한 내용은 [데이터 거버넌스](../../data-governance/home.md) 개요를 참조하십시오.

## 대상 {#destinations}

Adobe의 실시간 고객 데이터 플랫폼 [](../../rtcdp/overview.md)에서 대상은 대상 플랫폼과 사전 구축된 통합으로 이러한 파트너에게 데이터를 원활하게 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 향상된 UX | 사용자는 인라인 테이블 작업에 액세스하여 데이터 추가, 예약 편집 및 세그먼트 추가와 같은 기본 작업에 쉽게 액세스할 수 있습니다. 자세한 내용은 [대상 작업 공간](../../rtcdp/destinations/destinations-workspace.md) 문서를 참조하십시오. |

자세한 내용은 [대상 개요를 참조하십시오](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Privacy Service] {#privacy}

여러 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 자신의 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service] 는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 를 [!DNL Privacy Service]사용하면 Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터를 액세스 및 삭제하기 위한 요청을 제출하여 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| LGPD 지원(브라질) | 이제 브라질의 [!DNL Lei Geral de Proteção de Dados] (LGPD) 규정에 따라 개인 정보 일자리를 창출할 수 있다. 이 일자리들은 규제 규정에 따라 추적된다 `lgpd_bra`. |

서비스에 대한 자세한 내용은 [Privacy Service 개요를](../../privacy-service/home.md) 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 자동 매핑 | [!DNL Platform] 사용자가 선택한 대상 스키마 또는 데이터 세트를 기반으로 데이터 통합 워크플로우 동안 자동 매핑에 대한 지능적인 권장 사항을 제공합니다. 사용 사례에 맞게 유연한 자동 매핑 규칙을 수동으로 조정할 수 있습니다. |
| 향상된 UX | 사용자는 인라인 테이블 작업에 액세스하여 데이터 추가, 예약 편집 및 세그먼트 추가와 같은 기본 작업에 쉽게 액세스할 수 있습니다. 자세한 내용은 데이터 흐름 [모니터링](../../sources/tutorials/ui/monitor.md) 문서를 참조하십시오. |

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).
