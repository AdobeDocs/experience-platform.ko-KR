---
title: Adobe Experience Platform 릴리스 노트 - 2022년 10월
description: Adobe Experience Platform에 대한 2022년 10월 릴리스 노트입니다.
source-git-commit: d046c17a7b376f5c2e2f25c38fac0916ed2dba73
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 4%

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

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| (베타) 데이터 집합 내보내기 | 다음 [데이터 집합에서 베타 기능을 내보냅니다](/help/destinations/ui/export-datasets.md) 의 [Real-time Customer Data Platform 제품 설명](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) 대상 사용자 인터페이스를 통해 고유한 외부 고객 시스템에 Adobe Experience Platform 외부에서 가져옵니다. 이를 통해 분석 및 규정 준수 사용 사례를 위해 코드 없음/낮은 코드 워크플로우를 통해 데이터를 6개의 클라우드 스토리지 대상(아래 표에 나열됨)으로 Experience Platform 밖으로 가져올 수 있습니다. |
| (베타) 향상된 파일 내보내기 기능 | 이제 Experience Platform에서 파일을 내보낼 때 향상된 사용자 지정 기능을 활용할 수 있습니다. <br><ul><li>추가 [파일 이름 지정 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>를 통해 내보낸 파일에서 사용자 지정 파일 헤더를 설정할 수 있습니다. [매핑 단계 개선](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[내보낸 CSV 데이터 파일의 형식을 사용자 지정하는 기능](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> 이 기능은 아래 표에 나열된 6개의 새로운 베타 클라우드 스토리지 카드에서 지원됩니다. |

{style=&quot;table-layout:auto&quot;}

**새 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line 은 사용자, 서비스 및 정보를 연결하는 인기 있는 통신 플랫폼으로, 채팅 앱에서 엔터테인먼트, 소셜 및 일상적인 활동을 위한 허브로 성장했습니다. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365는 ERP(Enterprise Resource Planning)와 CRM(Customer Relationship Management)을 생산성 애플리케이션 및 AI 도구와 결합하여 종단 간 더욱 원활하고 제어된 운영, 향상된 성장 가능성 및 비용 절감을 제공하는 클라우드 기반 비즈니스 애플리케이션 플랫폼입니다. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | 다음 [!DNL (Beta) Adobe Commerce] 대상 커넥터를 사용하면 하나 이상의 Real-Time CDP 세그먼트를 선택하여 원하는 위치에 활성화할 수 있습니다 [!DNL Adobe Commerce] 고객을 위한 동적 개인화된 경험을 제공하기 위한 계정입니다. 내 [!DNL Adobe Commerce]그런 다음 이러한 Real-Time CDP 세그먼트를 선택하여 장바구니에서 &#39;buy 2 get 1 free&#39; 등의 고유한 오퍼를 개인화할 수 있습니다. Adobe Real-Time CDP 세그먼트에 맞게 사용자 지정된 프로모션 오퍼를 통해 대표 배너를 표시하고 제품 가격을 수정할 수도 있습니다. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 에 대한 라이브 아웃바운드 연결을 만듭니다. [!DNL Azure Data Lake Storage Gen2] Adobe Experience Platform의 데이터 파일을 주기적으로 자체 저장소 위치로 내보냅니다. 이 새로운 베타 대상은 향상된 파일 내보내기 기능을 제공하고 데이터 세트 내보내기를 지원합니다. |
| [[!DNL (Beta) Azure Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] is [!DNL Azure Blob] Adobe Experience Platform에서 프로비저닝한 스토리지 인터페이스로, Platform에서 파일을 내보낼 수 있는 안전한 클라우드 기반 파일 저장소 기능에 대한 액세스 권한을 부여합니다. 이 새로운 베타 대상은 향상된 파일 내보내기 기능을 제공하고 데이터 세트 내보내기를 지원합니다. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 에 대한 라이브 아웃바운드 연결을 만듭니다. [!DNL Google Cloud Storage] 를 통해 Adobe Experience Platform의 데이터 파일을 고유한 버킷으로 주기적으로 내보냅니다. 이 새로운 베타 대상은 향상된 파일 내보내기 기능을 제공하고 데이터 세트 내보내기를 지원합니다. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | 베타 참가자에게 이제 두 명이 표시됩니다. [!DNL Amazon S3] 대상 카탈로그의 대상 카드를 나란히 표시합니다. 새로운 베타 대상은 향상된 파일 내보내기 기능을 제공하고 데이터 세트 내보내기를 지원합니다. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | 베타 참가자에게 이제 두 명이 표시됩니다. [!DNL Azure Blob] 대상 카탈로그의 대상 카드를 나란히 표시합니다. 새로운 베타 대상은 향상된 파일 내보내기 기능을 제공하고 데이터 세트 내보내기를 지원합니다. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | 베타 참가자에게 이제 두 명이 표시됩니다. [!DNL SFTP] 대상 카탈로그의 대상 카드를 나란히 표시합니다. 새로운 베타 대상은 향상된 파일 내보내기 기능을 제공하고 데이터 세트 내보내기를 지원합니다. |

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
| 플랫폼 UI를 통해 쿼리 모니터링 | 쿼리 서비스 [!UICONTROL 예약된 쿼리] 탭은 UI를 통해 모든 쿼리 작업 상태에 대한 가시성을 개선합니다. 이제 오류 메시지와 코드가 실패할 경우 쿼리 실행 상태에 대한 중요한 정보를 찾을 수 있습니다. [!UICONTROL 예약된 쿼리] 탭. UI를 통해 해당 상태에 따라 이러한 쿼리에 대한 경고를 구독할 수도 있습니다. 자세한 내용은 [쿼리 모니터링 문서](../../query-service/monitor-queries.md) 이 기능에 대해 자세히 알아보십시오. |
| 쿼리 가속 보고 통찰력 데이터 모델 | Data Distiller SKU의 일부로 쿼리 가속 스토어를 사용하면 데이터를 통해 중요한 통찰력을 얻는 데 필요한 시간과 처리 능력을 줄일 수 있습니다. 쿼리 가속 스토어를 사용하여 사용자 지정 데이터 모델을 만들거나 기존 Adobe Real-time Customer Data Platform 데이터 모델을 확장하여 보고 통찰력과 시각화를 향상시킬 수 있습니다. 자세한 내용은 [쿼리 가속 저장소 보고 통찰력 문서](../../query-service/query-accelerated-store/reporting-insights-data-model.md) 이 기능에 대해 자세히 알아보십시오. |

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
