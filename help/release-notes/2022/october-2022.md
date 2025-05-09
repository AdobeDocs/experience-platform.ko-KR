---
title: Adobe Experience Platform 릴리스 노트 2022년 10월
description: Adobe Experience Platform의 2022년 10월 릴리스 정보.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 32%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2022년 10월 26일 목요일**

- [고객 관리 키](#cmk)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [경험 데이터 모델](#xdm)
- [쿼리 서비스](#query-service)

## 고객 관리 키 {#cmk}

Adobe Experience Platform에 저장된 모든 데이터는 시스템 수준 키를 사용하여 사용하지 않을 때 암호화됩니다. Experience Platform 위에 구축된 애플리케이션을 사용하는 경우 이제 고유한 암호화 키를 대신 사용하도록 선택할 수 있으므로 데이터 보안을 보다 강력하게 제어할 수 있습니다.

기능에 대한 자세한 내용은 [고객 관리 키](../../landing/governance-privacy-security/customer-managed-keys/overview.md)에 대한 개요를 참조하십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터스트림에 대한 중요한 데이터 처리 | 이제 데이터 스트림은 여러 Experience Platform 기술을 활용하여 HIPAA(Health Insurance Portability and Accountability Act)와 같은 규정에 따라 중요한 데이터를 적절하게 처리합니다. 자세한 내용은 [데이터스트림의 민감한 데이터 처리](../../datastreams/overview.md#sensitive)에 대한 섹션을 참조하십시오. |
| 이벤트 전달을 위한 [!DNL Splunk] 확장 | 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Splunk]에 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL Splunk] 확장 기능 개요](../../tags/extensions/server/splunk/overview.md)를 참조하십시오. |
| 이벤트 전달을 위한 [!DNL Zendesk] 확장 | 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Zendesk]에 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL Zendesk] 확장 기능 개요](../../tags/extensions/server/zendesk/overview.md)를 참조하십시오. |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| (Beta) 데이터 세트 내보내기 | [데이터 집합 내보내기 Beta 기능](/help/destinations/ui/export-datasets.md)을(를) 사용하면 대상 사용자 인터페이스를 통해 Adobe Experience Platform의 1세대 데이터([Real-Time Customer Data Platform 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)에 정의된 대로)를 자체 외부 고객 시스템으로 내보낼 수 있습니다. 이를 통해 분석 및 규정 준수 사용 사례를 위해 6개의 클라우드 스토리지 대상(아래 표에 나열됨)에 대한 no-code/low-code 워크플로우를 통해 Experience Platform에서 데이터를 가져올 수 있습니다. |
| (Beta) 향상된 파일 내보내기 기능 | 이제 Experience Platform에서 파일을 내보낼 때 향상된 사용자 지정 기능을 사용할 수 있습니다. <br><ul><li>추가 [파일 이름 지정 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>[향상된 매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)를 통해 내보낸 파일에서 사용자 정의 파일 헤더를 설정하는 기능.</li><li>[내보낸 CSV 데이터 파일의 형식을 사용자 지정하는 기능](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> 이 기능은 아래 표에 나열된 6개의 새 Beta 클라우드 저장소 카드에서 지원됩니다. |

{style="table-layout:auto"}

**새로운 대상 또는 업데이트된 대상** {#new-or-updated-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | 라인은 사람, 서비스, 정보를 연결하는 대중적인 커뮤니케이션 플랫폼으로 채팅 앱에서 엔터테인먼트, 소셜, 일상 활동을 위한 허브로 성장했다. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365는 생산성 애플리케이션과 AI 도구와 함께 ERP(전사적 자원 관리) 및 CRM(고객 관계 관리)이 결합된 클라우드 기반의 비즈니스 애플리케이션 플랫폼으로, 더욱 원활하고 통제된 운영, 더 나은 성장 잠재력 및 비용 절감을 제공합니다. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | [!DNL (Beta) Adobe Commerce] 대상 커넥터를 사용하면 하나 이상의 Real-Time CDP 세그먼트를 선택하여 [!DNL Adobe Commerce] 계정에 활성화하여 쇼핑객에게 동적인 개인화된 환경을 제공할 수 있습니다. 그런 다음 [!DNL Adobe Commerce] 내에서 해당 Real-Time CDP 세그먼트를 선택하여 &#39;2개 구매 1 무료&#39; 등의 장바구니에서 고유한 오퍼를 개인화할 수 있습니다. 또한 Adobe Real-Time CDP 세그먼트에 맞춤화된 홍보용 오퍼를 통해 영웅 배너를 표시하고 제품 가격을 수정할 수 있습니다. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | [!DNL Azure Data Lake Storage Gen2]에 대한 실시간 아웃바운드 연결을 만들어 주기적으로 Adobe Experience Platform의 데이터 파일을 자체 스토리지 위치로 내보냅니다. 이 새로운 Beta 대상은 향상된 파일 내보내기 기능을 제공하며 데이터 세트 내보내기를 지원합니다. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone]은(는) Adobe Experience Platform에서 프로비저닝한 [!DNL Azure Blob] 저장소 인터페이스로서, Experience Platform에서 파일을 내보낼 수 있는 안전한 클라우드 기반 파일 저장소 기능에 대한 액세스 권한을 부여합니다. 이 새로운 Beta 대상은 향상된 파일 내보내기 기능을 제공하며 데이터 세트 내보내기를 지원합니다. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | [!DNL Google Cloud Storage]에 대한 실시간 아웃바운드 연결을 만들어 주기적으로 Adobe Experience Platform의 데이터 파일을 자체 버킷으로 내보냅니다. 이 새로운 Beta 대상은 향상된 파일 내보내기 기능을 제공하며 데이터 세트 내보내기를 지원합니다. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Beta 참가자가 이제 대상 카탈로그에 두 개의 [!DNL Amazon S3] 대상 카드를 나란히 보고 있습니다. 새로운 Beta 대상은 향상된 파일 내보내기 기능을 제공하며 데이터 세트 내보내기를 지원합니다. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Beta 참가자가 이제 대상 카탈로그에 두 개의 [!DNL Azure Blob] 대상 카드를 나란히 보고 있습니다. 새로운 Beta 대상은 향상된 파일 내보내기 기능을 제공하며 데이터 세트 내보내기를 지원합니다. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Beta 참가자가 이제 대상 카탈로그에 두 개의 [!DNL SFTP] 대상 카드를 나란히 보고 있습니다. 새로운 Beta 대상은 향상된 파일 내보내기 기능을 제공하며 데이터 세트 내보내기를 지원합니다. |

{style="table-layout:auto"}

**새로운 설명서 또는 업데이트된 설명서**

| 설명서 | 설명 |
| ----------- | ----------- |
| [대상 보호](../../destinations/guardrails.md) | 이 페이지에서는 활성화 동작과 관련된 기본 사용량 및 요금 제한을 제공합니다. |

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 데이터 유형 | [[!UICONTROL 세션 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `authorized` 필드를 부울 형식에서 문자열로 업데이트했습니다. `season` 및 `episode`이(가) 정수에서 문자열로 변경되었습니다. |
| 데이터 유형 | [[!UICONTROL 광고 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name`의 이름이 `friendlyName`(으)로 변경되고 `ID`의 이름이 `name`(으)로 변경되었습니다. |
| 데이터 유형 | [[!UICONTROL 오류 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` 이름이 `name`(으)로 바뀌었습니다. |

{style="table-layout:auto"}

Experience Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL로 Adobe Experience Platform [!DNL Data Lake]에서 데이터를 쿼리할 수 있습니다. [!DNL Data Lake]의 데이터 세트에 참여하고 쿼리 결과를 보고 또는 데이터 과학 작업 영역에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Experience Platform UI를 통해 쿼리 모니터링 | 쿼리 서비스 [!UICONTROL 예약된 쿼리] 탭에서는 UI를 통해 모든 쿼리 작업의 상태를 보다 잘 볼 수 있습니다. 이제 [!UICONTROL 예약된 쿼리] 탭에서 쿼리 실행 상태에 대한 중요한 정보(오류 메시지 및 실패 시 코드 포함)를 찾을 수 있습니다. UI를 통해 상태를 기반으로 이러한 쿼리에 대한 경고를 구독할 수도 있습니다. 이 기능에 대한 자세한 내용은 [쿼리 모니터링 문서](../../query-service/ui/monitor-queries.md)를 참조하세요. |
| 쿼리 가속화된 보고 통찰력 데이터 모델 | Data Distiller SKU의 일부로, 쿼리 가속 스토어를 사용하면 데이터에서 중요한 통찰력을 얻는 데 필요한 시간과 처리 능력을 줄일 수 있습니다. 쿼리 가속 저장소를 사용하면 사용자 지정 데이터 모델을 구축하거나 기존 Adobe Real-Time Customer Data Platform 데이터 모델에서 확장하여 보고 통찰력과 시각화를 향상시킬 수 있습니다. 이 기능에 대한 자세한 내용은 [쿼리 가속 저장소 보고 인사이트 문서](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md)를 참조하세요. |

{style="table-layout:auto"}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md)를 참조하세요.
Adobe Experience Platform의 새로운 기능:

