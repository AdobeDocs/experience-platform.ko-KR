---
title: Adobe Experience Platform 릴리스 노트 - 2021년 8월
description: Adobe Experience Platform에 대한 2021년 8월 릴리스 노트입니다.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 8월 25일**

Adobe Experience Platform의 기존 기능 업데이트:

- [대상](#destinations)
- [가시성 통찰력](#observability)
- [실시간 고객 프로필](#profile)
- [소스](#sources)

## 대상 {#destinations}

대상은 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | 이전에 베타 버전으로 제공되는 Airship Attributes 대상은 이제 일반적으로 사용할 수 있습니다. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | 이전에 베타에 있는 Airship 태그 대상을 이제 일반적으로 사용할 수 있습니다. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | 이전 베타에 있는 브레이즈 대상을 이제 일반적으로 사용할 수 있습니다. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | pinterest 고객 목록 대상을 사용하면 고객 목록, 사이트를 방문한 사람 또는 Pinterest의 콘텐츠와 이미 상호 작용한 사람에서 대상을 만들 수 있습니다. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Twitter에서 기존 팔로워와 고객을 Target하고 Adobe Experience Platform 내에 내장된 대상을 활성화하여 적절한 리마케팅 캠페인을 만듭니다. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX는 Verizon Media/Yahoo가 안전하고 자동화된 확장 가능한 방식으로 외부 파트너와 데이터를 교환할 수 있도록 하는 다양한 구성 요소를 호스팅하는 종합적인 Verizon Media/Yahoo 인프라입니다. |

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK은 선택한 데이터 및 인증 형식에 따라 Experience Platform이 대상 및 프로필 데이터를 종단점에 제공할 대상 통합 패턴을 구성할 수 있도록 해주는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며, 추가 업데이트를 위해 API를 통해 검색할 수 있습니다. |
| [대상에 대한 유용성 개선](../../destinations/ui/activation-overview.md) | 대상에 대한 유용성 개선 사항을 통해 마케터는 세그먼트를 기존 대상에 원활하게 활성화할 수 있습니다. |

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## Observability Insights {#observability}

가시성 통찰력을 사용하면 통계 지표 및 이벤트 알림을 사용하여 플랫폼 활동을 모니터링할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 경고 | 이제 Platform에서 실행되는 워크플로우와 관련된 중요한 경고를 구독할 수 있습니다. 특정 경고 규칙을 구독하면 중요한 라이프사이클 이벤트가 발생할 때(예: 성공적인 데이터 섭취) 또는 주의가 필요한 문제(예: 수집 흐름 실패 또는 세그먼트 작업 예상 보다 오래 걸리는 경우)가 발생하면 UI 내 알림 및 이메일을 받게 됩니다. 자세한 내용은 [경고 개요](../../observability/alerts/overview.md). |

자세한 내용은 [가시성 통찰력 개요](../../observability/home.md) 를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 위치와 시기에 관계없이 고객을 위해 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객을 전체적으로 확인할 수 있습니다. 프로필을 사용하면 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 고객 데이터를 통합할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 병합 정책 또는 ID로 프로필 찾아보기 | 이제 Experience Platform에서 프로필을 검색할 때 병합 정책별로 검색하여 선택한 병합 정책을 기반으로 20개의 샘플 프로필을 미리 볼 수 있습니다. ID 네임스페이스와 관련 ID 값을 사용하여 특정 프로필을 검색하기 위해 ID별로 검색할 수도 있습니다. 자세한 내용은 [실시간 고객 프로필 UI 안내서](../../profile/ui/user-guide.md). |

프로필 데이터 작업에 대한 자습서 및 모범 사례 등 실시간 고객 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 로컬 파일 업로드 소스 커넥터 | 파일 수집 범주의 이름이 로컬 시스템으로 변경되었으므로 로컬 파일 업로드 커넥터를 사용하여 로컬 파일을 Platform으로 직접 가져올 수 있습니다. 이 커넥터를 통해 수집된 데이터는 모니터링 대시보드를 통해 모니터링할 수 있습니다. 자세한 내용은 [로컬 파일 업로드 소스 개요](../../sources/connectors/local-system/local-file-upload.md) 추가 정보. |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
