---
title: Adobe Experience Platform 릴리스 노트 2021년 8월
description: Adobe Experience Platform에 대한 2021년 8월 릴리스 정보입니다.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 35%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2021년 8월 25일 목요일**

Adobe Experience Platform의 기존 기능 업데이트:

- [대상](#destinations)
- [가시성 통찰력](#observability)
- [실시간 고객 프로필](#profile)
- [소스](#sources)

## 대상 {#destinations}

대상은 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과 미리 빌드된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | Airship Attributes 이전 베타 버전을 이제 일반적으로 사용할 수 있습니다. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | 이전 베타 버전이었던 Airship Tags 대상은 이제 일반적으로 사용할 수 있습니다. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | 이전 베타 버전이었던 Braze 대상을 이제 일반적으로 사용할 수 있습니다. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | pinterest 고객 목록 대상을 사용하면 고객 목록, 사이트를 방문한 사람 또는 Pinterest에서 콘텐츠와 이미 상호 작용한 사람에서 대상을 만들 수 있습니다. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Adobe Experience Platform 내에 구축된 대상을 활성화하여 Twitter에서 기존 팔로우어 및 고객을 타겟팅하고 관련 리마케팅 캠페인을 생성합니다. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX는 Verizon Media/Yahoo가 안전하고 자동화된 확장 가능한 방식으로 외부 파트너와 데이터를 교환할 수 있도록 하는 다양한 구성 요소를 호스팅하는 Verizon Media/Yahoo 인프라의 집합체입니다. |

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK은 선택한 데이터 및 인증 형식을 기반으로 Experience Platform에 대한 대상 통합 패턴을 구성하여 대상과 프로필 데이터를 엔드포인트에 전달할 수 있도록 하는 구성 API의 세트입니다. 구성은 Experience Platform에 저장되며 추가 업데이트를 위해 API를 통해 검색할 수 있습니다. |
| [대상에 대한 유용성 개선](../../destinations/ui/activation-overview.md) | 대상에 대한 사용성이 개선되어 마케터는 기존 대상에 대한 세그먼트를 원활하게 활성화할 수 있습니다. |

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## Observability Insights {#observability}

가시성 인사이트를 사용하면 통계 지표 및 이벤트 알림을 사용하여 플랫폼 활동을 모니터링할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 경고 | 이제 플랫폼에서 실행되는 워크플로와 관련된 중요한 알림을 구독할 수 있습니다. 특정 경고 규칙을 구독하면 중요한 라이프사이클 이벤트(예: 성공적인 데이터 수집)가 발생하거나 주의가 필요한 문제(예: 수집 흐름 실패 또는 세그먼트 작업이 예상보다 오래 걸리는 문제)가 발생하면 UI 내 알림 및 이메일을 받게 됩니다. 자세한 내용은 [경고 개요](../../observability/alerts/overview.md)를 참조하세요. |

서비스에 대한 자세한 내용은 [Observability Insights 개요](../../observability/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객의 상호 작용에 대해 실행 가능한 타임스탬프가 지정된 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 병합 정책 또는 ID별로 프로필 찾아보기 | 이제 Experience Platform에서 프로필을 찾아볼 때 병합 정책별로 탐색하여 선택한 병합 정책을 기반으로 하는 20개의 샘플 프로필을 미리 볼 수 있습니다. ID 네임스페이스 및 관련 ID 값을 사용하여 특정 프로필을 검색하기 위해 ID별로 검색할 수도 있습니다. 자세한 내용은 [실시간 고객 프로필 UI 안내서](../../profile/ui/user-guide.md)를 참조하십시오. |

프로필 데이터 작업에 대한 튜토리얼 및 모범 사례를 포함하여 실시간 고객 프로필에 대해 자세히 알아보려면 [실시간 고객 프로필 개요](../../profile/home.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 로컬 파일 업로드 소스 커넥터 | 파일 수집 범주의 이름이 로컬 시스템으로 변경되어 로컬 파일 업로드 커넥터를 사용하여 로컬 파일을 플랫폼으로 직접 가져올 수 있습니다. 이 커넥터를 통해 수집된 데이터는 모니터링 대시보드를 통해 모니터링할 수 있습니다. 자세한 내용은 [로컬 파일 업로드 원본 개요](../../sources/connectors/local-system/local-file-upload.md)를 참조하세요. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하세요.
