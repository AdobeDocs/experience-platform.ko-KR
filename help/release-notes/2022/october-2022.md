---
title: Adobe Experience Platform 릴리스 노트 - 2022년 10월
description: Adobe Experience Platform에 대한 2022년 10월 릴리스 노트입니다.
source-git-commit: 021a0833941f250475786bb8629542c50229b238
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 10월 26일**

- [고객 관리 키](#cmk)

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [대상](#destinations)
- [XDM(경험 데이터 모델)](#xdm)
- [쿼리 서비스](#query-service)
- [소스](#sources)

## 고객 관리 키 {#cmk}

Adobe Experience Platform에 저장된 모든 데이터는 시스템 수준 키를 사용하여 나머지 위치에서 암호화됩니다. 플랫폼 위에 구축된 응용 프로그램을 사용하는 경우 이제 자체 암호화 키를 사용하도록 선택할 수 있으므로 데이터 보안을 더욱 강화할 수 있습니다.

다음 사항에 대한 개요를 참조하십시오. [고객 관리 키](../../landing/governance-privacy-security/customer-managed-keys.md) 를 참조하십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 세트에 대한 중요 데이터 처리 | 이제 데이터 저장소는 여러 플랫폼 기술을 활용하여 HIPAA(Health Insurance Portability and Accountability Act)와 같은 규정에 따라 적용되는 중요한 데이터를 적절하게 처리합니다. 의 섹션을 참조하십시오. [datstreams의 sendstive 데이터 처리](../../edge/datastreams/overview.md#sensitive) 추가 정보. |
| [!DNL Splunk] 이벤트 전달을 위한 확장 | 이제 데이터를에 보낼 수 있습니다 [!DNL Splunk] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장. 자세한 내용은 [[!DNL Splunk] 확장 개요](../../tags/extensions/web/splunk/overview.md) 추가 정보. |
| [!DNL Zendesk] 이벤트 전달을 위한 확장 | 이제 데이터를에 보낼 수 있습니다 [!DNL Zendesk] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장. 자세한 내용은 [[!DNL Zendesk] 확장 개요](../../tags/extensions/web/zendesk/overview.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line 은 사용자, 서비스 및 정보를 연결하는 인기 있는 통신 플랫폼으로, 채팅 앱에서 엔터테인먼트, 소셜 및 일상적인 활동을 위한 허브로 성장했습니다. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365는 ERP(Enterprise Resource Planning)와 CRM(Customer Relationship Management)을 생산성 애플리케이션 및 AI 도구와 결합하여 종단 간 더욱 원활하고 제어된 운영, 향상된 성장 가능성 및 비용 절감을 제공하는 클라우드 기반 비즈니스 애플리케이션 플랫폼입니다. |

{style=&quot;table-layout:auto&quot;}

**새 설명서 또는 업데이트된 설명서**

| 설명서 | 설명 |
| ----------- | ----------- |
| [대상 보호 기능](../../destinations/guardrails.md) | 이 페이지에서는 활성화 동작과 관련된 기본 사용량 및 비율 제한을 제공합니다. |

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 데이터 유형 | [[!UICONTROL 세션 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 업데이트 날짜: `authorized` 필드를 부울 형식에서 문자열로 가져옵니다. `season` 및 `episode` 가 정수에서 문자열로 변경되었습니다. |
| 데이터 유형 | [[!UICONTROL 광고 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` 의 이름이 `friendlyName`, 및 `ID` 의 이름이 `name`. |
| 데이터 유형 | [[!UICONTROL 오류 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID`의 이름이 `name`로 변경되었습니다.  |

{style=&quot;table-layout:auto&quot;}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 쿼리 서비스 {#query-service}

Query Service를 사용하면 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다 [!DNL Data Lake]. 에서 모든 데이터 세트에 가입할 수 있습니다 [!DNL Data Lake] 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새로운 데이터 세트로 캡처합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 쿼리 가속 보고 통찰력 데이터 모델 | Data Distiller SKU의 일부로 쿼리 가속 스토어를 사용하면 데이터를 통해 중요한 통찰력을 얻는 데 필요한 시간과 처리 능력을 줄일 수 있습니다. 쿼리 가속 스토어를 사용하여 사용자 지정 데이터 모델을 만들거나 기존 Adobe Real-time Customer Data Platform 데이터 모델을 확장하여 보고 통찰력과 시각화를 향상시킬 수 있습니다. 자세한 내용은 [쿼리 가속 저장소 보고 통찰력 문서](https://experienceleague.adobe.com/docs/experience-platform/query/query-accelerated-store/reporting-insights-data-model.html) 이 기능에 대해 자세히 알아보십시오. |

{style=&quot;table-layout:auto&quot;}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md).
Adobe Experience Platform의 새로운 기능:

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- | 
| Adobe Workfront 소스의 베타 가용성 | 를 사용하십시오 [Adobe Workfront 소스](../../sources/connectors/adobe-applications/workfront.md) Workfront 데이터를 Experience Platform에 가져와서 작업 레코드를 타사 데이터와 결합하고, 작업 레코드에 내역 및 시계열 분석을 적용하고, 표준 SQL을 사용하여 작업 데이터를 쿼리하는 등의 사용 사례를 수행할 수 있습니다. 자세한 내용은 다음 안내서를 참조하십시오. [UI에서 Workfront 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| oracle 서비스 클라우드 소스의 베타 가용성 | oracle 서비스 클라우드 소스를 사용하여 Oracle 서비스 클라우드 계정의 데이터를 Experience Platform으로 수집할 수 있습니다. 자세한 내용은 [Oracle 서비스 클라우드 소스](../../sources/connectors/customer-success/oracle-service-cloud.md). |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
