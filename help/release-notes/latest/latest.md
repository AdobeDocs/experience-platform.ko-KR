---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 2023년 8월 릴리스 정보입니다.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: bf4c4186ed9196e547620a91826f86aa09d683fd
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 37%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2023년 8월 23일**

Adobe Experience Platform의 기존 기능 업데이트:

- [Real-Time Customer Data Platform](#rtcdp)
- [속성 기반 액세스 제어](#abac)
- [대시보드](#dashboards)
- [데이터 수집](#data-collection)
- [데이터 수집](#data-ingestion)
- [데이터 준비](#data-prep)
- [경험 데이터 모델 (XDM)](#xdm)
- [ID 서비스](#identity-service)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## Real-Time Customer Data Platform {#rtcdp}

Experience Platform을 기반으로 구축된 Real-Time Customer Data Platform([!DNL Real-Time CDP])으로 기업은 알려진 데이터와 알 수 없는 데이터를 수집하여 고객 여정 전반에 걸쳐 지능적인 의사 결정을 통해 고객 프로필을 활성화할 수 있습니다.

[!DNL Real-Time CDP]는 여러 기업의 데이터 소스를 결합하여 실시간으로 고객 프로필을 생성합니다. 이러한 프로필에서 구축된 세그먼트는 다운스트림 대상으로 전송되어 모든 채널과 디바이스에서 일대일로 개인 설정된 고객 경험을 제공할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 지능형 재참여 사용 사례 안내서 | 다음 [지능형 재참여](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) 사용 사례 안내서에서는 지능적이고 책임 있는 방식으로 전환을 완료하기 전에 포기한 고객을 다시 참여시키는 방법에 대한 세부 정보를 제공합니다. 이 안내서에서는 다음 예제 여정을 사용하여 고객을 다시 참여시킵니다. <ul><li>재참여 여정 - 제품 탐색을 중단한 고객을 타깃팅합니다.</li><li>포기한 장바구니 여정 - 장바구니에 제품을 배치했지만 아직 구매를 완료하지 않은 고객을 타깃팅합니다.</li><li>주문 확인 여정 - 제품 구매에 초점</li></ul> 아래 부분에 있는 자세한 피드백 옵션 링크를 사용하십시오. [지능형 재참여 사용 사례 안내서](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) 피드백을 제공할 수 있습니다. |
| 파트너 데이터 지원 | 파트너 소스 잠재 고객 프로필 및 파트너 ID를 사용하여 Real-Time CDP에서 상위 단계 마케팅을 실행하여 신규 고객에게 도달하고 자사 데이터를 보강합니다. <ul><li>고객 확보 및 주소 지정 기능: 선택한 데이터 파트너의 쿠키 없는 식별자 및 해시된 PII를 활용하여 새로운 순 고객에게 도달하고 서드파티 쿠키 의존성을 줄입니다.</li><li>단일 시스템의 전체 단계 마케팅: 단일 시스템의 예상 및 알려진 고객을 위한 셀프서비스 세분화, 대상자 큐레이션 및 기본 활성화.</li><li>신뢰 기반: 특허를 획득한 데이터 사용, 레이블 지정, 액세스 제어 등을 통해 파트너 데이터 및 프로필을 책임감 있게 시장에 적용합니다. 자세한 내용은 다음 사용 사례 안내서를 참조하십시오. 이제 전망 사용 사례 안내서를 사용할 수 있습니다. 잠재 고객 활용 사례 안내서를 읽고 잠재 고객 활용 사례를 통해 신규 고객을 유치하는 방법을 알아보십시오.<ul><li>[전망](../../rtcdp/partner-data/prospecting.md)</li><li>[온사이트 개인화](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[자사 프로필 보완](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[잠재 고객 활성화](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

자세한 내용은 다음을 참조하십시오. [Real-Time CDP 개요](../../rtcdp/overview.md).

## 속성 기반 액세스 제어 {#abac}

속성 기반 액세스 제어는 Adobe Experience Platform의 기능으로, 개인 정보 보호를 고려한 브랜드에게 사용자 액세스를 더 유연하게 관리할 수 있습니다. 스키마 필드 및 세그먼트와 같은 개별 객체를 사용자 역할에 할당할 수 있습니다. 이 기능을 사용하면 조직의 특정 Platform 사용자에 대해 개별 객체에 대한 액세스 권한을 부여하거나 취소할 수 있습니다.

조직 관리자는 속성 기반 액세스 제어를 통해 모든 플랫폼 워크플로 및 리소스에서 중요한 개인 데이터(SPD), 개인 식별 정보(PII) 및 기타 사용자 지정된 유형의 데이터에 대한 사용자의 액세스를 제어할 수 있습니다. 관리자는 특정 필드 및 해당 필드에 해당하는 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 권한 정책 샌드박스 구성 | 새로운 [권한 정책 샌드박스 구성](../../access-control/abac/ui/policies.md) 이 기능을 사용하면 요구 사항과 요구 사항에 따라 모든 샌드박스 또는 선택한 수의 샌드박스에 속성 기반 액세스 제어 정책을 적용할 수 있습니다. |

{style="table-layout:auto"}

속성 기반 액세스 제어에 대한 자세한 내용은 [속성 기반 액세스 제어 개요](../../access-control/abac/overview.md). 속성 기반 액세스 제어 워크플로에 대한 포괄적인 안내서는 [속성 기반 액세스 제어 엔드투엔드 안내서](../../access-control/abac/end-to-end-guide.md).

## 대시보드 {#dashboards}

Adobe Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 동의 분석 및 추적 사용 사례 | 을(를) 사용하여 Real-Time CDP 데이터에 대한 다양한 마케팅 사용 사례에 대한 동의 대시보드를 작성하는 방법을 알아봅니다. [동의 분석 및 추적 문서](../../dashboards/insights-use-cases/consent-analysis.md). 비즈니스 요구에 적합한 속성으로 대상자를 만든 다음 Adobe Experience Platform UI에서 사전 구성된 위젯을 사용하여 통찰력을 소비하는 방법에 대해 자세히 설명합니다. 또한 사용자 정의 대시보드 기능을 사용하여 사용자 정의 위젯을 빌드하는 방법에 대한 지침을 제공합니다. 이 문서에서는 동의 트렌드 및 동의 중복 사용 사례를 다룹니다. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 유형 | 기능 | 설명 |
| --- | --- | --- |
| 태그 및 이벤트 전달 | [Experience Platform 태그(중국)](/help/tags/ui/publishing/premium-cdn.md) | 새로운 Experience Platform 태그(중국) 기능은 웹 사이트 안정성과 지연 시간을 향상시켜 중국의 웹 사이트에 태그를 배포하는 고객의 응답 시간을 단축합니다. 이제 고객은 중국에서 웹 사이트를 구현할 때 태그 라이브러리의 JavaScript 코드를 사용할 수 있습니다. 이 기능은 UPP(통합 프로비저닝 프로토콜)에도 추가되어 구매 후 제품 배포를 자동화할 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 다음을 참조하십시오. [데이터 컬렉션 개요](../../tags/home.md).

## 데이터 수집 {#data-ingestion}

Adobe Experience Platform은 데이터의 모든 유형과 지연 시간을 수집할 수 있는 다양한 기능 세트를 제공합니다. Adobe에서 구축한 소스, 데이터 통합 파트너 또는 Adobe Experience Platform UI를 사용하여 일괄 처리 또는 스트리밍 API로 수집할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 수집 워크플로 변경 사항 | 지정된 데이터 유형보다 큰 값을 포함하는 데이터 행(예: 정수 데이터 유형으로 전달된 긴 데이터)이 거부되고 오류 메시지가 보고됩니다. 이전에는 이러한 행이 경고 없이 거부되었습니다. |

자세한 내용은 다음을 참조하십시오. [데이터 수집 개요](../../ingestion/home.md).

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 XDM(Experience Data Model)과의 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 보조 ID 필터링 지원 | 이제 데이터 준비를 사용하여 AAID 및 AACUSTOMID와 같은 Adobe Analytics에서 전송되는 ID를 필터링할 수 있습니다. 필터링되면 이러한 ID가 실시간 고객 프로필에 수집되지 않습니다. 필터링되지 않은 데이터는 데이터 레이크로 계속 수집됩니다. |

{style="table-layout:auto"}

자세한 내용은 다음을 참조하십시오. [데이터 준비 개요](../../data-prep/home.md).

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL XDM 개별 잠재 고객 프로필]](https://github.com/adobe/xdm/pull/1758/files) | 이 클래스를 사용하여 데이터 공급업체의 단계 상단 고객 확보 사용 사례에서 소싱된 잠재 고객 프로필을 가져옵니다. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 업데이트 |
| --- | --- | --- |
| 확장([!UICONTROL Adobe Analytics ExperienceEvent 전체 확장]) | [[!UICONTROL 컨텍스트 데이터]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL 컨텍스트 데이터] 맵 개체가에 추가됨 [!UICONTROL Adobe Analytics ExperienceEvent 전체 확장] Adobe Analytics에 컨텍스트 데이터를 제공합니다. |
| 필드 그룹 | 다수 | 몇 개의 필드가에 추가됨 [[!UICONTROL 보강된 이벤트 세그먼트 세부 정보]](https://github.com/adobe/xdm/pull/1760/files). |

{style="table-layout:auto"}

자세한 내용은 다음을 참조하십시오. [XDM 시스템 개요](../../xdm/home.md).

## ID 서비스 {#identity-service}

Adobe Experience Platform ID 서비스는 여러 디바이스 및 시스템에 걸쳐 ID를 연결하여 고객과 고객의 행동을 종합적으로 파악할 수 있으므로, 실시간으로 효과적인 개인 디지털 환경을 제공할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| ID 그래프 제한 변경 | 9월 말까지 ID 그래프가 그래프당 50개의 ID로 변경되고 최신 ID가 수집됩니다. 따라서 가장 오래된 ID는 수집 타임스탬프 및 ID 유형에 따라 삭제되며 쿠키 ID 유형이 먼저 삭제됩니다. 현재 ID 그래프의 ID 제한은 그래프당 150개이며 이 제한에 도달하면 그래프가 더 이상 업데이트되지 않습니다. 프로덕션 샌드박스에 다음이 포함된 경우 계정 담당자에게 문의하여 ID 유형 변경을 요청하십시오. <ul><li>개인 식별자(예: CRM ID)가 쿠키/장치 ID 유형으로 구성되는 사용자 정의 네임스페이스입니다.</li><li>쿠키/장치 식별자가 교차 장치 ID 유형으로 구성된 사용자 지정 네임스페이스입니다.</li></ul> Adobe 엔지니어링에서 이러한 요청을 수동으로 처리합니다. 자세한 내용은 [id 서비스 데이터 보호](../../identity-service/guardrails.md). |

자세한 내용은 다음을 참조하십시오. [ID 서비스 개요](../../identity-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]를 사용하여 개인 사용자(예: 고객, 잠재 고객, 사용자 또는 조직)와 관련된 [!DNL Experience Platform]에 저장된 데이터를 대상자로 세분화할 수 있습니다. 세그먼트 정의 또는 [!DNL Real-Time Customer Profile] 데이터의 다른 소스를 통해 대상자를 만들 수 있습니다. 이러한 대상자는 [!DNL Platform]을 통해 중앙 집중식으로 구성 및 유지 관리되고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 유사 대상(제한된 가용성) | 유사 대상은 각 대상에 대한 지능적인 통찰력을 제공하며 머신 러닝 기반 통찰력을 활용하여 마케팅 캠페인을 통해 고부가가치 고객을 식별하고 타깃팅합니다. 유사 대상을 사용하면 성과가 좋은 대상과 유사한 고객을 타겟팅하거나 이전에 전환된 대상과 유사한 고객을 타겟팅하는 확장된 대상을 만들 수 있습니다. 유사 대상에 대한 자세한 내용은 [유사 대상 개요](../../segmentation/ui/lookalike-audiences.md). |

{style="table-layout:auto"}

자세한 내용은 다음을 참조하십시오. [세그먼테이션 개요](../../segmentation/home.md).

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 의 일반 가용성 [!DNL SugarCRM] | [!DNL SugarCRM] 이제 소스를 사용할 수 있습니다. [!DNL SugarCRM Accounts & Contacts] 및 [!DNL SugarCRM Events] 소스를 사용하여 데이터를 사용자의 [!DNL SugarCRM] 계정에서 Experience Platform으로 가져옵니다. 자세한 내용은 [[!DNL SugarCRM] 개요](../../sources/connectors/crm/sugarcrm.md)를 참조하십시오. |
| UI의 소스 데이터 흐름에 대한 온디맨드 수집 지원 | 이제 UI에서 기존 소스 데이터 흐름에 대한 주문형 흐름 실행을 만들 수 있습니다. 자세한 내용은 의 안내서를 참조하십시오. [ui를 사용하여 소스에 대한 온디맨드 플로우 실행 생성](../../sources/tutorials/ui/on-demand-ingestion.md). |
| 신규 지원 `correlationID` Adobe Analytics용 필드 | 다음 `_experience.decisioning.propositions.scopeDetails.correlationID` 이제 Adobe Analytics 소스 커넥터 스키마에서 필드를 사용할 수 있습니다. 이 필드는 A4T 분류 지원에 사용되며 2023년 9월부터 채워집니다. |

{style="table-layout:auto"}

자세한 내용은 다음을 참조하십시오. [소스 개요](../../sources/home.md).
