---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments
solution: Experience Platform
title: 다중 엔티티 세그먼테이션
topic: overview
description: 다중 엔티티 세그먼테이션은 제품, 스토어 또는 기타 비프로필 클래스에 따라 추가 데이터로 프로필 데이터를 확장하는 기능입니다. 연결되면 추가 클래스의 데이터를 프로필 스키마가 기본인 것처럼 사용할 수 있습니다.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# 다중 엔티티 세그먼테이션

다중 엔티티 세그먼테이션은 제품, 스토어 또는 기타 비프로필 클래스에 따라 추가 데이터로 [!DNL Profile] 데이터를 확장하는 기능입니다. 연결되면 추가 클래스의 데이터를 스키마 원본처럼 사용할 수 [!DNL Profile] 있게 됩니다.

다중 엔티티 세그먼테이션에 대한 자세한 내용을 보려면 설명서를 계속 읽고 아래 비디오를 보거나 세그멘테이션 개요를 [살펴보면서 학습 내용을 보완하십시오](./home.md).

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## 시작하기

이 자습서에서는 세그멘테이션 사용과 관련된 다양한 Adobe Experience Platform 서비스에 대해 작업해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL 실시간 고객 프로필]](../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 한 통합 소비자 프로필을 실시간으로 제공합니다.
- [Adobe Experience Platform 세그멘테이션 서비스](./home.md):실시간 고객 프로필에서 세그먼트를 만들 수 있습니다.
- [[!DNL 경험 데이터 모델(XDM)]](../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크

## XDM 관계를 정의하는 방법

XDM(스키마 구조) [!DNL Experience Data Model] 의 관계를 정의하는 것은 세그먼트 생성의 중요한 부분이며 중요한 부분입니다.

이 프로세스는 [!DNL Schema Registry] [!DNL Schema Editor]API 또는 API를 사용하여 두 스키마 간의 관계를 정의하는 방법에 대한 자세한 설명은 API를 사용하여 두 스키마 간 관계 [를 정의하는 자습서를 참조하십시오](../xdm/tutorials/relationship-api.md). 두 스키마 간 관계 [!DNL Schema Editor] 를 정의하는 데 사용하는 방법에 대한 자세한 설명은 스키마 편집기 [를 사용하여 두 스키마 간의 관계를 정의하는 자습서를 참조하십시오](../xdm/tutorials/relationship-ui.md).

## XDM 관계를 사용하는 세그먼트를 만드는 방법

XDM 관계를 정의한 후에는 API를 사용하여 세그먼트를 [!DNL Segmentation Service] 작성할 수 있습니다.

이 프로세스는 [!DNL Segmentation] API 또는 [!DNL Segment Builder] 사용자 인터페이스를 사용하여 수행할 수 있습니다. API를 사용하여 세그먼트를 만드는 방법에 대한 자세한 설명은 세그멘테이션 API [를 사용하여 세그먼트를 만드는 방법에 대한 자습서를 참조하십시오](./tutorials/create-a-segment.md). 세그먼트 빌더를 사용하여 세그먼트를 만드는 방법에 대한 자세한 설명은 세그먼트 빌더 사용자 가이드 [를 참조하십시오](./ui/overview.md).

## 다중 엔티티 세그먼트에 대한 세그먼트를 평가하고 액세스하는 방법

세그먼트를 만든 후 [!DNL Segmentation Service] API를 사용하여 세그먼트 결과를 평가하고 액세스할 수 있습니다. 다중 엔티티 세그먼트 평가는 일반 세그먼트 평가와 매우 유사합니다.

이 프로세스는 [!DNL Segmentation Service] API를 사용해서만 수행할 수 있습니다. API를 사용하여 세그먼트를 평가하고 액세스하는 방법에 대한 자세한 설명은 세그먼트 [평가 및 액세스에 대한 자습서를 참조하십시오](./tutorials/evaluate-a-segment.md).