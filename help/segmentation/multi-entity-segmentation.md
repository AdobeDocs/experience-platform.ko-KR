---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 다중 엔티티 세그먼테이션
topic: overview
translation-type: tm+mt
source-git-commit: 7110be2654e55ea411580f8c9e2e92bb52badab5
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# 다중 엔티티 세그먼테이션

다중 엔티티 세그먼테이션은 제품, 스토어 또는 기타 비프로필 클래스에 따라 추가 데이터로 프로필 데이터를 확장하는 기능입니다. 연결되면 추가 클래스의 데이터를 프로필 스키마가 기본인 것처럼 사용할 수 있습니다.

다중 엔티티 세그먼테이션에 대한 자세한 내용을 보려면 설명서를 계속 읽고 아래 비디오를 시청하거나 세그멘테이션 개요를 [살펴보면서 학습 내용을 보완하십시오](./home.md).]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## 시작하기

이 자습서에서는 세그멘테이션 사용과 관련된 다양한 Adobe Experience Platform 서비스에 대해 작업해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [실시간 고객 프로필](../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 한 통합 소비자 프로필을 실시간으로 제공합니다.
- [Adobe Experience Platform 세그멘테이션 서비스](./home.md): 실시간 고객 프로필에서 세그먼트를 만들 수 있습니다.
- [XDM(Experience Data Model)](../xdm/home.md): Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

## XDM 관계를 정의하는 방법

XDM(Experience Data Model) 스키마 구조와의 관계를 정의하는 것은 세그먼트 생성의 중요한 부분이며 중요한 부분입니다.

이 프로세스는 스키마 레지스트리 API 또는 스키마 편집기를 사용하여 수행할 수 있습니다. API를 사용하여 두 스키마 간의 관계를 정의하는 방법에 대한 자세한 설명은 API를 사용하여 두 스키마 간 관계 [를 정의하는 자습서를 참조하십시오](../xdm/tutorials/relationship-api.md). 스키마 편집기를 사용하여 두 스키마 간의 관계를 정의하는 방법에 대한 자세한 지침은 스키마 편집기 [를 사용하여 두 스키마 간의 관계를 정의하는 방법에 대한 자습서를 참조하십시오](../xdm/tutorials/relationship-ui.md).

## XDM 관계를 사용하는 세그먼트를 만드는 방법

XDM 관계를 정의한 후에는 실시간 고객 프로필 API를 사용하여 세그먼트를 작성할 수 있습니다.

이 프로세스는 실시간 고객 프로필 API 또는 세그먼트 빌더를 사용하여 수행할 수 있습니다. API를 사용하여 세그먼트를 만드는 방법에 대한 자세한 설명은 실시간 고객 프로필 API [를 사용하여 세그먼트를 만드는 방법에 대한 자습서를 참조하십시오](./tutorials/create-a-segment.md). 세그먼트 빌더를 사용하여 세그먼트를 만드는 방법에 대한 자세한 설명은 세그먼트 빌더 사용자 가이드 [를 참조하십시오](./ui/overview.md).

## 다중 엔티티 세그먼트에 대한 세그먼트를 평가하고 액세스하는 방법

세그먼트를 만든 후 실시간 고객 프로필 API를 사용하여 세그먼트 결과를 평가하고 액세스할 수 있습니다. 다중 엔티티 세그먼트 평가는 일반 세그먼트 평가와 매우 유사합니다.

이 프로세스는 실시간 고객 프로필 API를 통해서만 수행할 수 있습니다. API를 사용하여 세그먼트를 평가하고 액세스하는 방법에 대한 자세한 설명은 세그먼트 [를 평가하고 액세스하는 방법에 대한 자습서를 참조하십시오](./tutorials/evaluate-a-segment.md).