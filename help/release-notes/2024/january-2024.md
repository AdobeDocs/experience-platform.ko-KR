---
title: Adobe Experience Platform 릴리스 노트 2024년 1월
description: Adobe Experience Platform의 2024년 1월 릴리스 정보.
source-git-commit: 7b694ad1b064279fcc0dd09bd1e8761e734e7556
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 27%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2024년 1월 30일 수요일**

Adobe Experience Platform의 새로운 기능:

- [사용 사례 플레이북](#use-case-playbooks)

Experience Platform의 기존 기능 업데이트:

- [속성 기반 액세스 제어](#abac)
- [데이터 준비](#data-prep)
- [대시보드](#dashboards)
- [대상](#destinations)
- [ID 서비스](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [실시간 고객 프로필](#profile)
- [소스](#sources)

## 사용 사례 플레이북 {#use-case-playbooks}

다음 [!UICONTROL 사용 사례 플레이북] 이제 모든 Real-Time CDP 및 Adobe Journey Optimizer 고객이 기능을 사용할 수 있습니다. [!UICONTROL 사용 사례 플레이북] 는 Real-time Customer Data Platform 또는 Adobe Journey Optimizer으로 시작할 때 사용자가 문제를 극복하도록 지원하기 위해 설계되었습니다. 어디서부터 시작할지 또는 원하는 사용 사례에 적합한 에셋을 제작하는 방법을 잘 모를 때 사용 사례 플레이북을 통해 영감을 얻고 다른 에셋을 제작하여 준비가 되면 프로덕션 환경에 테스트하고 가져올 수 있습니다.

시작하려면 [!UICONTROL 사용 사례 플레이북], 다음 설명서 페이지를 참조하십시오.

- 읽기 [개요 페이지](/help/use-case-playbooks/playbooks/overview.md) 목적, 가용성 정보를 이해하고 플레이북이 검색에서 인스턴스 생성, 생성된 에셋을 다른 샌드박스 환경으로 가져오는 방법에 대해 전체적인 데모를 받습니다.
- 모든 항목 목록 가져오기 [이용할 수 있는 플레이북](/help/use-case-playbooks/playbooks/playbooks-list.md), 제품별로 그룹화됨(Real-Time CDP 또는 Journey Optimizer)
- 모든 항목에 대한 정보 가져오기 [필수 권한](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) 플레이북과 플레이북에서 생성된 에셋을 사용합니다.
- 이해 [데이터 인식 기능](/help/use-case-playbooks/playbooks/data-awareness.md) 생성된 에셋을 다른 샌드박스 환경으로 복사할 수 있습니다
- Get [문제 해결 팁](/help/use-case-playbooks/playbooks/troubleshooting.md) 사용 사례 플레이북을 사용할 때 오류나 문제가 발생하는 경우.

## 속성 기반 액세스 제어 {#abac}

속성 기반 액세스 제어는 Adobe Experience Platform의 기능으로, 개인 정보 보호를 고려한 브랜드에게 사용자 액세스를 더 유연하게 관리할 수 있습니다. 스키마 필드 및 세그먼트와 같은 개별 객체를 사용자 역할에 할당할 수 있습니다. 이 기능을 사용하면 조직의 특정 Platform 사용자에 대해 개별 객체에 대한 액세스 권한을 부여하거나 취소할 수 있습니다.

조직 관리자는 속성 기반 액세스 제어를 통해 모든 플랫폼 워크플로 및 리소스에서 중요한 개인 데이터(SPD), 개인 식별 정보(PII) 및 기타 사용자 지정된 유형의 데이터에 대한 사용자의 액세스를 제어할 수 있습니다. 관리자는 특정 필드 및 해당 필드에 해당하는 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.

**신규 또는 업데이트된 설명서**

| 설명서 업데이트 | 설명 |
| --- | --- |
| 속성 기반 액세스 제어에 대해 문서화된 새 API 엔드포인트 | 다음 [액세스 제어 API 참조 설명서](https://developer.adobe.com/experience-platform-apis/references/access-control/) 에는 이제 속성 기반 액세스 제어 API 역할, 정책 및 제품 끝점이 포함됩니다. 이러한 엔드포인트는 지정된 샌드박스의 지정된 리소스에서 사용자에 대한 관련 역할, 정책 및 제품을 검색하는 데 사용할 수 있습니다. |

{style="table-layout:auto"}

속성 기반 액세스 제어에 대한 자세한 내용은 [속성 기반 액세스 제어 개요](../../access-control/abac/overview.md). 속성 기반 액세스 제어 워크플로에 대한 포괄적인 안내서는 [속성 기반 액세스 제어 엔드투엔드 안내서](../../access-control/abac/end-to-end-guide.md).

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 XDM(Experience Data Model)과의 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 새로운 매퍼 함수 | <ul><li>`object_to_map`: 사용 `object_to_map` 맵 데이터 유형을 만드는 함수입니다. 이 함수는 여러 가지 다른 구문을 지원합니다. 자세한 내용은 의 안내서를 참조하십시오. [계층 함수 - 객체](../../data-prep/functions.md#objects). </li><li>`to_map`: 사용 `to_map` 개체를 사용하여 주어진 필드 이름과 값 쌍을 사용하여 맵을 만드는 함수입니다. 자세한 내용은 의 안내서를 참조하십시오. [계층 함수 - 맵](../../data-prep/functions.md#map). </li><li>`array_to_map`: 사용 `array_to_map` 개체 배열을 사용하여 지정된 필드 이름 및 값 쌍으로 맵을 만드는 함수입니다. 자세한 내용은 의 안내서를 참조하십시오. [계층 함수 - 맵](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md).

## 대시보드 {#dashboards}

Adobe Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| SQL 보기 | 이제 SQL 보기 토글을 사용하여 프로필, 대상, 대상 및 맞춤화된 인사이트 뒤에 있는 SQL을 본 다음 쿼리 편집기를 통해 요청 시 쿼리를 실행할 수 있습니다. Real-time Customer Data Platform 통찰력을 제공하는 SQL에 액세스하면 데이터 모델 분석의 논리를 이해할 수 있습니다. 이러한 투명성은 Adobe 실시간 CDP 데이터를 보다 쉽게 액세스하고 이해할 수 있도록 하며 의사 결정에 영향을 줍니다.<br>40개 이상의 기존 인사이트의 SQL에서 영감을 얻어 비즈니스 요구 사항에 따라 플랫폼 데이터에서 고유한 인사이트를 도출하는 새로운 쿼리를 만들 수 있습니다. SQL은 [프로필](../../dashboards/insights/profiles.md), [대상](../../dashboards/insights/audiences.md), 및 [대상](../../dashboards/insights/destinations.md) Experience League 설명서의 insights. 이 문서에서는 표준 인사이트로 답할 수 있는 비즈니스 사용 사례를 강조합니다. 자세한 내용은 의 안내서를 참조하십시오. [insight SQL 보기](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [치골 연결](../../destinations/catalog/advertising/pubmatic.md) | 이 대상을 사용하여 대상 데이터를 [!DNL PubMatic Connect] 플랫폼. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 신규 **가정된 역할** Amazon S3 대상에 대한 인증 유형 | Experience Platform과 Experience Platform 키 및 비밀 키를 공유하지 않으려면 Amazon S3 버킷에 계정을 연결할 때 새로운 가설 역할 인증 유형을 사용하십시오. 의 새 인증 방법에 대해 자세히 알아보십시오. [인증 섹션](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) Amazon S3 설명서의 |

{style="table-layout:auto"}

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## ID 서비스 {#identity-service}

Adobe Experience Platform ID 서비스는 여러 디바이스 및 시스템에 걸쳐 ID를 연결하여 고객과 고객의 행동을 종합적으로 파악할 수 있으므로, 실시간으로 효과적인 개인 디지털 환경을 제공할 수 있습니다.

**신규 또는 업데이트된 설명서**

| 설명서 업데이트 | 설명 |
| --- | --- |
| 문서 재구성 | Identity Service 설명서는 Identity Service 내 개념의 표시 및 명확성을 개선하기 위해 재구성되었습니다.<ul><li>다음 방문: [ID 서비스 개요 페이지](../../identity-service/home.md) 확장된 용어 안내서의 경우 일반적인 고객 여정을 자세히 설명하는 사용 사례 예, Identity Service가 ID를 함께 연결하는 방법에 대한 분류 및 Identity Service가 Experience Platform 생태계 내에서 수행하는 역할에 대한 요약이 제공됩니다.</li><li>의 안내서 읽기 [identity 서비스와 실시간 고객 프로필 간의 관계 이해](../../identity-service/identity-and-profile.md) 두 서비스가 함께 작동하는 방식과 목적, 프로세스, 입력 및 출력 간의 차이에 대한 자세한 요약 정보.</li><li>다음을 참조하십시오. [ID 서비스 연결 논리 안내서](../../identity-service/features/identity-linking-logic.md) id 그래프가 다양한 시나리오 및 타임스탬프를 부여받아 동작하는 방식에 대한 설명 및 시각화용.</li></ul> |

{style="table-layout:auto"}

ID 서비스에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Experience Platform을 기반으로 구축된 Real-Time Customer Data Platform([!DNL Real-Time CDP])으로 기업은 알려진 데이터와 알 수 없는 데이터를 수집하여 고객 여정 전반에 걸쳐 지능적인 의사 결정을 통해 고객 프로필을 활성화할 수 있습니다. [!DNL Real-Time CDP]는 여러 기업의 데이터 소스를 결합하여 실시간으로 고객 프로필을 생성합니다. 이러한 프로필에서 구축된 세그먼트는 다운스트림 대상으로 전송되어 모든 채널과 디바이스에서 일대일로 개인 설정된 고객 경험을 제공할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 업데이트: [Real-Time CDP 홈 페이지](https://experience.adobe.com) | <ul><li>**프로필 위젯**: 이제 프로필 위젯을 사용하여 프로필 개요 페이지로 이동하고 조직의 프로필 지표를 볼 수 있습니다.</li><li>**프로필 지표 카드**: 이제 홈 페이지 대시보드의 프로필 지표 카드에 각 병합 정책에 따라 조직의 총 프로필 수가 표시됩니다.</li><li>**스키마 위젯**: 이제 스키마 위젯을 사용하여 UI에서 스키마 생성 워크플로우로 이동할 수 있습니다.</li></ul> |

{style="table-layout:auto"}

**신규 또는 업데이트된 설명서**

| 설명서 업데이트 | 설명 |
| --- | --- |
| 새 Real-Time CDP 설명서 홈 페이지 | 다음 방문: [새 Real-Time CDP 설명서 홈 페이지](/help/rtcdp/home.md) 제품, 가드레일, 샘플 사용 사례 등을 시작하는 방법에 대한 정보를 한눈에 살펴볼 수 있습니다. |
| 샘플 Real-Time CDP 사용 사례 개요 | 다음 방문: [새로운 샘플 사용 사례 개요 페이지](/help/rtcdp/use-case-guides/overview.md) 조직에서 Real-Time CDP을 통해 달성할 수 있는 샘플 사용 사례 컬렉션. |

{style="table-layout:auto"}

Real-Time CDP에 대해 자세히 알아보려면 [Real-Time CDP 개요](../../rtcdp/overview.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객의 상호 작용에 대해 실행 가능한 타임스탬프가 지정된 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 프로필 뷰어의 기본 대시보드 카드 현지화 개선 사항 | 이제 기본 프로필 카드에 동적으로 현지화된 이름이 표시됩니다. 사용자 정의 프로필 카드는 편집할 수 있는 사용자 정의 이름을 계속 가질 수 있습니다. |

{style="table-layout:auto"}

실시간 고객 프로필에 대한 자세한 내용은 [프로필 개요](../../profile/home.md)

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL Oracle NetSuite] 소스 | 사용 [!DNL Oracle NetSuite] 소스 카탈로그의 통합을 통해 다음에서 데이터 가져오기 [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) 및 [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) Experience Platform 계정. |
| [!BADGE Beta]{type=Informative}[!DNL Braze Currents] 소스 | 사용 [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) 소스 카탈로그의 통합을 통해 다음에서 데이터 가져오기 [!DNL Braze] Experience Platform 계정. |
| 에 대한 키 쌍 인증 지원 [!DNL Snowflake] 일괄 처리 소스 | 이제 새로 만들 때 키 쌍 인증을 사용할 수 있습니다 [!DNL Snowflake] 배치 데이터 계정. 자세한 내용은 의 안내서를 참조하십시오. [만들기 [!DNL Snowflake] API를 사용하는 계정](../../sources/tutorials/api/create/databases/snowflake.md) 또는 의 안내서 [만들기 [!DNL Snowflake] UI를 사용하는 계정](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요 ](../../sources/home.md)를 참조하십시오.