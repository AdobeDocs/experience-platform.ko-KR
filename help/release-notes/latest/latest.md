---
title: Adobe Experience Platform 릴리스 노트 2024년 7월
description: Adobe Experience Platform의 2024년 7월 릴리스 정보.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c38f6845a4819b648abacea2c36a576dac61f38f
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 21%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2024년 7월 30일 수요일**

Adobe Experience Platform의 새로운 기능:

- [!BADGE 제한 공개]{type=Informative}[페더레이션 대상 구성](#federated-audience-composition)

Experience Platform의 기존 기능 및 설명서에 대한 업데이트:

- [고급 데이터 수명주기 관리](#advanced-data-lifecycle-management)
- [데이터 수집](#data-collection)
- [데이터 거버넌스](#data-governance)
- [대상](#destinations)
- [Segmentation Service](#segmentation)
- [소스](#sources)
- [통합 태그](#unified-tags)

## 페더레이션된 대상자 구성 {#federated-audience-composition}

Federated Audience Composition을 통해 기업은 다양한 사용 사례에서 더 나은 애플리케이션을 위해 데이터를 구성할 수 있습니다. Adobe Real-time Customer Data Platform 및/또는 Adobe Journey Optimizer 사용자는 이 새로운 접근 방식을 통해 기존 데이터 웨어하우스에서 직접 데이터 세트를 페더레이션하여 하나의 시스템에 Adobe Experience Platform 대상 및 속성을 모두 만들고 보강할 수 있습니다.

자세한 내용은 [Federated Audience Composition 설명서](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/home)를 참조하십시오.

## 고급 데이터 수명주기 관리 {#advanced-data-lifecycle-management}

Experience Platform은 소비자 레코드 및 데이터 세트에 대한 프로그래밍 방식 삭제를 통해 저장된 데이터를 관리할 수 있는 데이터 위생 기능 제품군을 제공합니다. UI에서 또는 데이터 위생 API 호출을 통해 데이터 라이프사이클 작업 영역을 사용하면 데이터 저장소를 효과적으로 관리할 수 있습니다. 이러한 기능을 사용하여 정보가 예상대로 사용되고, 잘못된 데이터를 수정해야 할 때 업데이트되고, 조직 정책에서 필요하다고 판단할 때 삭제되도록 하십시오.

**새 설명서**

| 새 설명서 | 설명 |
| --- | --- |
| [!DNL Data Hygiene API] 참조 | 데이터 위생 API를 사용하여 Experience Platform에서 데이터 저장소를 효과적으로 관리합니다. 이러한 기능을 사용하면 정보를 예상대로 사용하고, 잘못된 경우 업데이트하고, 조직 정책에서 필요하다고 판단할 경우 삭제할 수 있습니다.<br><br>API 사용 방법에 대한 자세한 내용은 [데이터 위생 API 참조 문서](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/)를 참조하십시오. 데이터 위생 API를 사용하여 데이터 세트 만료 날짜를 예약하고, 저장된 고객 개인 데이터를 프로그래밍 방식으로 수정 또는 삭제하고 데이터 위생 할당량을 확인할 수 있습니다. API 참조 문서에는 저장된 고객 데이터를 효율적으로 관리하는 데 도움이 되는 사용 가능한 엔드포인트, 요청 매개 변수 및 응답 형식이 포함되어 있습니다.</br></br> |

자세한 내용은 [고급 데이터 수명 주기 관리 개요](../../hygiene/home.md)를 참조하십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Experience Platform Edge Network으로 전송할 수 있는 기술 제품군을 제공합니다. 여기서 데이터 보강 및 변환, Adobe 또는 비 Adobe 대상으로 배포할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 유형 | 기능 | 설명 |
| --- | --- | --- |
| Web SDK | 제안 상호 작용 자동 추적 | 이제 Web SDK의 `autoTrackPropositionInteractionsEnabled` 속성을 사용하여 Web SDK가 제안 상호 작용을 자동으로 수집해야 하는지 확인할 수 있습니다. 자세한 내용은 [`autoTrackPropositionInteractionsEnabled`](../../web-sdk/commands/configure/autotrackpropositioninteractionsenabled.md) 설명서를 참조하십시오. |

{style="table-layout:auto"}

**새 설명서 또는 업데이트된 설명서**

| 신규 또는 업데이트된 설명서 | 설명 |
| --- | --- |
| Reactor API에 대해 문서화된 새로운 API 엔드포인트 | 확장 패키지 사용 승인 끝점은 이제 [Reactor API 참조 설명서](https://developer.adobe.com/experience-platform-apis/references/reactor/)에서 찾을 수 있습니다. 확장 소유자는 이러한 끝점을 사용하여 확장 패키지에 대한 패키지 승인을 추가, 제거 및 검색할 수 있습니다. |
| 새 확장 패키지 사용 권한 엔드포인트 문서 | 확장 패키지 소유자가 다른 회사에 Reactor API에서 개인 버전의 패키지를 사용하도록 권한을 부여하는 방법에 대한 개요는 [확장 패키지 사용 승인 끝점](/help/tags/api/endpoints/extension-package-usage-authorizations.md) 설명서에서 확인할 수 있습니다. |
| 새로운 공유 비공개 확장 안내서 | Reactor API의 확장 패키지 권한 부여 만들기, 승인 및 삭제 절차는 [비공개 확장 공유](/help/tags/api/guides/extension-packages.md) 설명서에 요약되어 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [데이터 수집 개요](../../collection/home.md)를 참조하십시오.

## 데이터 거버넌스 {#data-governance}

Adobe Experience Platform 데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략 및 기술입니다. 이 기능은 Experience Platform 내 카탈로그 작성, 데이터 계통 확인, 데이터 사용 라벨링, 데이터 액세스 정책, 마케팅 액션을 위한 데이터 액세스 제어 등 다양한 수준에서 주요 역할을 합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| mTLS 서비스 API | [mTLS 서비스 API](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/mtls-api/overview)은(는) 데이터 교환 보안을 강화하도록 설계되었습니다. 이 API를 사용하여 조직의 애플리케이션에 대해 Adobe이 발급한 공개 인증서를 안전하게 검색할 수 있습니다. 이러한 인증서는 모든 통신이 인증되고 암호화되도록 하며, 인증서의 신뢰성을 외부에서 확인하는 데 사용할 수 있습니다. 조직의 Adobe 응용 프로그램에 대한 공개 인증서를 안전하게 검색하는 방법을 알아보려면 [공개 인증서 끝점 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/mtls-api/public-certificate-endpoint)를 읽어 보십시오. |

{style="table-layout:auto"}

자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md)를 참조하세요.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [(Beta) Merkury Enterprise 연결](/help/destinations/catalog/data-partners/merkury-enterprise-connections.md) | [!DNL Merkury Enterprise Connections] 대상을 사용하여 대상자를 [!DNL Merkury]에 안전하게 전달하십시오. [!DNL Merkury]은(는) 마케터에게 개인 기반 대상자를 쉽게 일치시키고 [!DNL Merkury]의 80개 이상의 프리미엄 주소 지정 가능 TV/CTV, 게시자 및 광고 기술 연결로 배달할 수 있도록 합니다. [!DNL Merkury]은(는) 2억 6,800만 명 이상의 미국 성인 소비자 ID 그래프에서 제공됩니다. |
| [(Beta) Merkury Enterprise ID](/help/destinations/catalog/data-partners/merkury-enterprise-identity.md) | [!DNL Merkury Enterprise Identity] 대상을 사용하여 보다 정확하고 포괄적이며 통찰력 있는 소비자 프로필을 빌드합니다. 향상된 프로필 데이터를 통해 마케터는 더 나은 통찰력, 세그먼트 및 모델을 제공할 수 있으므로 보다 정확한 타겟팅 및 예측 모델링을 수행할 수 있습니다. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 대상 수준 데이터 흐름 모니터링 | 이전에는 대상별로 그룹화된 데이터 흐름 모니터링을 배치(파일 기반) 대상에만 사용할 수 있었습니다. 이번 릴리스부터 [(Beta) Google Customer Match + DV360 스트리밍 대상](/help/destinations/catalog/advertising/google-customer-match-dv360.md)에 대해서도 대상 수준 모니터링을 사용할 수 있습니다. Beta 프로그램에 참여하여 Google Customer Match + DV360 대상을 사용하려면 [대상 수준 모니터링](/help/dataflows/ui/monitor-destinations.md#segment-level-view)에 대해 자세히 알아보고 Adobe 담당자에게 문의하십시오. |
| Destination SDK에 대한 대상 메타데이터 매크로의 데이터 보강 속성 지원 | 이제 전용 매크로를 통해 [Destination SDK 대상 메타데이터 템플릿](../../destinations/destination-sdk/functionality/audience-metadata-management.md)에서 데이터 보강 특성에 액세스할 수 있습니다. 데이터 보강 특성은 [사용자 지정 업로드 대상자](../../destinations/destination-sdk/functionality/destination-configuration/schema-configuration.md#external-audiences)에만 사용할 수 있습니다. 데이터 보강 특성 선택이 어떻게 작동하는지 확인하려면 [일괄 대상자 활성화 가이드](../../destinations/ui/activate-batch-profile-destinations.md#select-enrichment-attributes)를 참조하세요. 자세한 내용은 대상 템플릿 [매크로 목록](../../destinations/destination-sdk/functionality/audience-metadata-management.md#macros)을 참조하세요. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하세요.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]를 사용하여 개인 사용자(예: 고객, 잠재 고객, 사용자 또는 조직)와 관련된 [!DNL Experience Platform]에 저장된 데이터를 대상자로 세분화할 수 있습니다. 세그먼트 정의 또는 [!DNL Real-Time Customer Profile] 데이터의 다른 소스를 통해 대상자를 만들 수 있습니다. 이러한 대상자는 [!DNL Platform]을 통해 중앙 집중식으로 구성 및 유지 관리되고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

**새 설명서**

| 새 설명서 | 설명 |
| ----------------- | ----------- | 
| [대상자 포털](../../segmentation/ui/audience-portal.md) | 중앙 집중식 허브의 Adobe Experience Platform 내에서 대상을 보고, 관리하고, 만들 수 있는 Audience Portal을 사용하는 방법을 알아봅니다. |

{style="table-layout:auto"}

## 소스

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션이나 타사 데이터 소스에서 데이터를 수집합니다.

**업데이트된 설명서**

| 업데이트된 설명서 | 설명 |
| --- | --- |
| [[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)에 대한 확장된 인증 가이드 | 인증을 위해 [계정 식별자](../../sources/connectors/databases/snowflake.md#retrieve-your-account-identifier) 및 [개인 키](../../sources/connectors/databases/snowflake.md#retrieve-your-private-key)를 검색하는 방법을 알아보려면 [!DNL Snowflake]의 확장된 인증 가이드를 읽어 보십시오. 또한 확장된 인증 가이드를 사용하여 [웨어하우스 및 역할 구성을 확인](../../sources/connectors/databases/snowflake.md#verify-configurations)하는 방법에 대한 단계를 확인하십시오. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.

## 통합 태그

통합 태그를 사용하여 Adobe Experience Platform 내에서 비즈니스 개체를 분류하고 관리할 수 있습니다. 통합 태그 API를 사용하면 폴더와 태그를 모두 만들어 대상이나 데이터 세트와 같은 Platform 개체를 보다 효율적으로 구성할 수 있습니다.

**새 설명서**

| 새 설명서 | 설명 |
| ----------------- | ----------- |
| [통합 태그 API 안내서](../../administrative-tags/api/overview.md) | 비즈니스 오브젝트를 정렬하기 위해 폴더 및 태그를 만드는 방법을 알아보려면 통합 태그 API 안내서 를 참조하십시오. |
| [통합 태그 API 참조](https://developer.adobe.com/experience-platform-apis/references/unified-tags/) | 통합 태그 API 참조를 사용하여 통합 태그 엔드포인트를 대화식으로 사용해 보십시오. |

{style="table-layout:auto"}

자세한 내용은 [통합 태그 개요](../../administrative-tags/overview.md)를 참조하세요.
