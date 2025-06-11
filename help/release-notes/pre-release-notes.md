---
title: Experience Platform 프리릴리스 노트
description: Adobe Experience Platform의 최신 릴리스 정보 미리보기.
hide: true
hidefromtoc: true
source-git-commit: c34c41d384fbc4f309dffa8bba97a0f6f3468efc
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 42%

---


# Adobe Experience Platform 프리릴리스 노트

>[!IMPORTANT]
>
>이 문서는 이번 달 릴리스 정보의 **미리 보기**&#x200B;로 작성되었습니다. 릴리스 항목은 변경될 수 있으며 최종 릴리스에서 추가 또는 제거될 수 있습니다.

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/latest)
>- [페더레이션된 대상자 구성](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 일자: 2025년 6월 18일 목요일**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [액세스 제어](#access-control)
- [고급 데이터 라이프사이클 관리](#advanced-data-lifecycle-management)
- [대시보드](#dashboards)
- [데이터 거버넌스](#data-governance)
- [대상](#destinations)
- [페더레이션된 대상자 컴포지션](#fac)
- [Privacy Service](#privacy-service)
- [쿼리 서비스](#query-service)
- [샌드박스](#sandboxes)
- [소스](#sources)

## 액세스 제어 {#access-control}

Experience Platform은 [Adobe Admin Console](https://adminconsole.adobe.com) 제품 프로필을 활용하여 사용 권한 및 샌드박스를 사용자와 연결합니다. 권한은 데이터 모델링, 프로필 관리 및 샌드박스 관리를 포함하여 다양한 Experience Platform 기능에 대한 액세스를 제어합니다.

**주요 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 대시보드 데이터 내보내기 권한 | 이제 대시보드의 **[!UICONTROL CSV 다운로드]** 및 **[!UICONTROL 이메일로 보내기]** 옵션에는 **[!UICONTROL 대시보드 데이터 내보내기]** 권한이 필요합니다. 이 권한을 사용하면 권한이 있는 사용자만 탭으로 작성된 insight 데이터를 내보낼 수 있으므로 보다 엄격한 거버넌스 및 데이터 액세스 제어 정책을 지원할 수 있습니다. |

자세한 내용은 [액세스 제어 개요](../access-control/home.md)를 참조하십시오.

## 고급 데이터 라이프사이클 관리 {#advanced-data-lifecycle-management}

Experience Platform은 프로그램 수준에서 소비자 기록 및 데이터 세트를 삭제함으로써 저장 데이터를 관리할 수 있도록 해 주는 데이터 위생 기능 세트를 제공합니다. UI의 데이터 라이프사이클 작업 영역을 사용하거나 데이터 위생 API 호출을 통해 데이터 저장소를 효과적으로 관리할 수 있습니다. 이들 기능을 사용하면 정보를 의도대로 사용하고 정확하지 않은 데이터를 수정해야 할 때 업데이트하며 조직 정책에 따라 필요한 경우 삭제할 수 있습니다.

**새 설명서**

| 새 설명서 | 설명 |
| --- | --- |
| 레코드 삭제 일반 가용성 | 이제 UI 또는 API를 사용하여 ID 필드를 기반으로 개별 레코드를 삭제할 수 있습니다. 이 기능을 사용하면 단일 데이터 세트 또는 모든 데이터 세트에서 삭제할 수 있으므로 스토리지를 줄이고 거버넌스를 적용하며 데이터 위생 상태를 개선할 수 있습니다. 볼륨 제한 및 자격 요구 사항이 적용됩니다. |

자세한 내용은 [고급 데이터 라이프사이클 관리 개요](../hygiene/home.md)를 참조하십시오.

## 대시보드 {#dashboards}

Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 전자 메일로 보내기 내보내기 옵션 | 이제 **[!UICONTROL 자세히 보기]** 메뉴에서 **[!UICONTROL 이메일로 보내기]**&#x200B;를 선택하여 Query Pro 모드 대시보드에서 최대 10,000개의 레코드를 내보낼 수 있습니다. 이 옵션은 더 큰 내보내기를 위해 Adobe 관련 이메일에 다운로드 링크를 안전하게 보냅니다. |

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../dashboards/home.md)를 읽어 보십시오.

## 데이터 거버넌스 {#data-governance}

Adobe Experience Platform 데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략 및 기술입니다. 이 기능은 [!DNL Experience Platform] 내 카탈로그 작성, 데이터 계통 확인, 데이터 사용 라벨링, 데이터 액세스 정책, 마케팅 액션을 위한 데이터 액세스 제어 등 다양한 수준에서 주요 역할을 합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| Azure CMK 경고 및 IP 허용 목록 구성 | 이제 Azure Key에서 Adobe의 고정 IP 주소를 허용 목록 하여 네트워크 제한이 계속 액세스되도록 할 수 있습니다. 이렇게 하면 제한된 키 액세스로 인한 Platform 서비스 중단을 방지할 수 있습니다. |
| CMK 구성 경고 및 해결 방법 | 이제 Experience Platform에서 Adobe 서비스가 Azure 키 자격 증명 모음에 대한 액세스 권한을 상실하면(예: 제거된 IP 허용 목록 항목이나 비활성화된 키로 인해) 경고를 트리거합니다. 새로운 안내서는 각 경고를 이해하고 수정 조치를 취하는 데 도움이 됩니다. |

자세한 내용은 [데이터 거버넌스 개요](../data-governance/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상**

| 대상 | 설명 |
| --- | --- |
| Algolia 사용자 세그먼트 | 마케팅 전문가는 Algolia 사용자 세그먼트 대상을 통해 홈페이지에서 검색까지 사이트 간에 일관된 개인화를 제공할 수 있습니다. 타겟팅 전략 및 캠페인 개인화를 개선하기 위해 여러 데이터 소스에서 풍부한 대상을 작성하고 다양한 채널에서 공유합니다. |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| LinkedIn 계정 만료 정보 | 이제 [!UICONTROL 찾아보기] 및 [!UICONTROL 계정] 보기에서 LinkedIn 대상의 계정 만료 정보를 바로 사용할 수 있습니다. 이전에는 설명서에서만 이 정보를 사용할 수 있었습니다. 이러한 향상된 기능을 통해 LinkedIn 인증 상태 및 자격 증명 관리에 대한 가시성이 향상되었습니다. |
| Google Customer Match + DV360 일반 가용성 및 개선 사항 | 이제 모든 Experience Platform 사용자가 Google Customer Match + DV360 대상을 사용할 수 있습니다. 이제 설명서에는 Adobe 및 Google 광고 계정 간 계정 연결에 대한 자세한 지침이 포함되어 있습니다. |
| DLZ(Data Landing Zone) 대상 암호화 지원 | 데이터 랜딩 영역 대상에 대한 암호화 지원이 추가되었습니다. 이제 RSA 형식의 공개 키를 연결하여 내보낸 파일에 암호화를 추가할 수 있습니다. |
| 엔터프라이즈 대상에 대한 대상 수준 모니터링 | Enterprise 대상: [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md), [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)에 대해 대상 수준 모니터링을 사용할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../destinations/home.md)를 참조하십시오.

## 페더레이션된 대상자 컴포지션 {#fac}

페더레이션된 대상자 컴포지션을 통해 기업은 다양한 사용 사례에서 데이터를 더 잘 적용할 수 있습니다. 이 새로운 접근 방식을 사용하면 Adobe Real-Time CDP 및/또는 Adobe Journey Optimizer 사용자로서 기존 데이터 웨어하우스에서 직접 데이터 세트를 페더레이션하여 Adobe Experience Platform 대상자와 속성을 모두 하나의 시스템에 만들고 강화할 수 있습니다.

| 새로운 기능 | 설명 |
| ----------- | ----------- |
| HIPAA 준비 | Federated Audience Composition은 이제 HIPAA를 준수합니다. Federated Audience Composition의 개인 정보 및 보안 조치에 대한 자세한 내용은 Federated Audience Composition 개요[&#128279;](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/start/privacy-security)의 개인 정보 및 보안을 참조하십시오. 일반적으로 Experience Platform 제품에 대한 HIPAA 준수에 대한 자세한 내용은 [HIPAA 및 Adobe 제품 및 서비스 개요](https://www.adobe.com/trust/compliance/hipaa-ready.html)를 참조하십시오. |

자세한 내용은 [페더레이션된 대상자 컴포지션 설명서](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/home)를 참조하십시오.

## [!DNL Privacy Service] {#privacy}

일부 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service]는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. [!DNL Privacy Service]를 사용하면 Adobe Experience Cloud 애플리케이션에서 비공개 또는 개인 고객 데이터에 액세스하고 삭제하도록 요청할 수 있으므로, 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 테네시 및 미네소타 개인 정보 보호 법 지원 | Privacy Service은 이제 테네시 정보 보호법(`tipa_tn_usa`) 및 미네소타 소비자 데이터 개인정보 보호법(`mcdpa_mn_usa`)을 지원합니다. 이러한 새로운 주 수준 규정을 준수하여 액세스 및 삭제 요청을 처리할 수 있습니다. 자세한 내용은 [규정 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/privacy/regulations/overview)를 참조하세요. |

서비스에 대한 자세한 내용은 [Privacy Service 개요](../privacy-service/home.md)를 참조하십시오.

## 쿼리 서비스 {#query-service}

쿼리 서비스가 포함된 표준 SQL을 사용하여 Adobe Experience Platform 데이터 레이크에서 데이터를 쿼리합니다. 데이터 세트를 매끄럽게 결합하고 쿼리 결과에서 새 데이터 세트를 생성하여 보고를 향상하거나, 데이터 과학 워크플로를 활성화하거나, 실시간 고객 프로필로 수집을 용이하게 합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 고급 통계 함수 | **세타 스케치 교차**: 대략적인 개별 계산 및 집합 작업에 대해 세타 스케치를 사용하여 집합 교차를 계산하는 새로운 함수입니다. **KLL 히스토그램**: 분위수 추정 및 분포 분석을 위해 KLL(K번째 가장 작은 항목, L번째 가장 큰 항목) 스케치를 사용하여 히스토그램 기능이 향상되었습니다. 이러한 기능은 Data Distiller 고객이 사용할 수 있습니다. |
| SQL 템플릿 라이브러리 | 이제 일반적인 사용 사례를 위한 포괄적인 SQL 템플릿 라이브러리를 사용할 수 있습니다. 이 기능은 빈번한 분석 패턴에 대한 모범 사례 템플릿을 제공하여 쿼리 개발을 가속화하므로 데이터 Distiller 고객이 복잡한 분석을 보다 효율적으로 구현할 수 있습니다. |

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| RFM 모델링 예 | Data Distiller 고객을 위한 포괄적인 최신성, 빈도, 통화(RFM) 모델링 예를 추가했습니다. 여기에는 RFM 기법을 사용한 고객 세분화 및 가치 분석을 위한 자세한 설명서 및 구현 안내서가 포함되어 있습니다. |

{style="table-layout:auto"}

[!DNL Query Service]에 대한 자세한 내용은 [[!DNL Query Service] 개요](../query-service/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 구축 요건을 충족해야 합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 개체 구성 업데이트 마이그레이션 | 이제 초기 복제 후 샌드박스 간에 반복적인 객체 구성 업데이트를 마이그레이션할 수 있습니다. 이 개선 사항은 전체 샌드박스 설정을 다시 생성하지 않고 환경 간에 구성을 업데이트하고 전파해야 하는 개발 워크플로를 지원합니다. |

{style="table-layout:auto"}

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../sandboxes/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Azure Synapse Analytics]에 대한 새 인증 유형 지원 | 이제 [!DNL Azure Synapse Analytics]은(는) 기존 연결 문자열 인증 외에 서비스 사용자 인증도 지원합니다. |

**중요 인증 업데이트**

| 업데이트 | 설명 |
| --- | --- |
| [!DNL Salesforce] 기본 인증 사용 중단 | Salesforce CRM 및 Salesforce Service Cloud에 대한 기본 인증은 2026년 1월까지 더 이상 사용되지 않습니다. 고객은 OAuth 2.0 인증으로 마이그레이션해야 연결을 유지할 수 있습니다. 이 변경 사항은 소스 커넥터 모두에 영향을 미치며 향상된 보안과 Salesforce 인증 표준 준수를 보장합니다. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../sources/home.md)를 참조하십시오.
