---
title: Adobe Experience Platform 릴리스 노트 - 2023년 4월
description: Adobe Experience Platform에 대한 2023년 4월 릴리스 노트입니다.
source-git-commit: 9f50ca4b2a4c576af5ce8ee5c085a7603fed2560
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2023년 4월 26일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 준비](#data-prep)
- [소스](#sources)

## 데이터 준비 {#data-prep}

데이터 준비를 통해 데이터 엔지니어가 XDM(Experience Data Model) 간 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 비프로덕션 샌드박스의 Adobe Analytics 채우기 기간 업데이트 | 비프로덕션 샌드박스의 Adobe Analytics 채우기 기간이 3개월로 줄었습니다. 프로덕션 샌드박스의 채우기 기능은 13개월에서 동일하게 유지됩니다. 이 변경 사항은 새 흐름에만 적용되며 기존 흐름에 영향을 주지 않습니다. 자세한 내용은 [Adobe Analytics 개요](../../sources/connectors/adobe-applications/analytics.md). |
| FPID 문자열을 ECID로 변환하는 새 매퍼 함수 | 를 사용하십시오 `fpid_to_ecid` Experience Platform 및 Experience Cloud 애플리케이션에서 사용할 FPID 문자열을 ECID로 변환하는 함수입니다. 자세한 내용은 [데이터 준비 함수 안내서](../../data-prep/functions.md). |

{style="table-layout:auto"}

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Microsoft Dynamics, Salesforce CRM 및 Salesforce Marketing Cloud에 대한 행 수준 데이터 필터링을 위한 API 지원 | 논리 및 비교 연산자를 사용하여 Microsoft Dynamics, Salesforce CRM 및 Salesforce Marketing Cloud 소스에 대한 행 수준 데이터를 필터링합니다. 안내서 읽기 [API를 사용하여 소스에 대한 데이터 필터링](../../sources/tutorials/api/filter.md) 추가 정보. |
| Shopify 스트리밍 베타 가용성 | 다음 [Shopify 스트리밍 소스](../../sources/connectors/ecommerce/shopify-streaming.md) 이제 베타로 제공됩니다. Shopify 스트리밍 소스를 사용하여 Shopify 파트너 계정의 데이터를 Experience Platform으로 스트리밍합니다. |
| OneTrust 통합의 일반 공급 | 다음 [OneTrust 통합 소스](../../sources/connectors/consent-and-preferences/onetrust.md) 은 현재 GA입니다. OneTrust 통합 소스를 사용하여 OneTrust 통합 계정의 동의 및 환경 설정 데이터를 Experience Platform으로 가져옵니다. |
| oracle 서비스 클라우드의 일반 공급 | 다음 [Oracle 서비스 클라우드 소스](../../sources/connectors/customer-success/oracle-service-cloud.md) 은 현재 GA입니다. oracle 서비스 클라우드 소스를 사용하여 Oracle 서비스 클라우드 데이터를 Experience Platform으로 가져옵니다. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
