---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments;multi-entity;multi-entity segmentation;multi-entity segments;
solution: Experience Platform
title: 다중 엔티티 세그먼테이션
topic: overview
description: 다중 엔티티 세그먼테이션은 제품, 스토어 또는 기타 비프로필 클래스에 따라 추가 데이터로 프로필 데이터를 확장하는 기능입니다. 연결되면 추가 클래스의 데이터를 프로필 스키마가 기본인 것처럼 사용할 수 있습니다.
translation-type: tm+mt
source-git-commit: 4dd5a91146b116953ba180e3f39d24b4e1ec289e
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# 다중 엔티티 세그먼테이션

다중 엔티티 세그먼테이션은 Adobe Experience Platform의 일부로 사용할 수 있는 고급 기능입니다 [!DNL Segmentation Service]. 이 기능을 사용하면 조직에서 정의할 수 있는 추가 &quot;비인적&quot; 데이터(예: 제품 또는 스토어와 관련된 데이터)로 [!DNL Real-time Customer Profile] 데이터를 확장할 수 있습니다. 다중 엔티티 세그먼테이션은 고유한 비즈니스 요구와 관련된 데이터를 기반으로 고객 세그먼트를 정의할 때 유연성을 제공하며, 데이터베이스 질의에 대한 전문 지식이 없어도 수행할 수 있습니다. 다중 엔티티 세그먼테이션을 사용하면 데이터 스트림을 많은 비용을 변경하거나 백엔드 데이터 병합을 기다릴 필요 없이 주요 데이터를 세그먼트에 추가할 수 있습니다.

## 시작하기

다중 엔티티 세그먼테이션을 사용하려면 세그멘테이션과 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 가이드를 계속 사용하려면 다음 설명서를 검토하십시오.

* [[!DNL Real-time Customer Profile]](../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 한 통합 소비자 프로필을 실시간으로 제공합니다.
   * [프로필 가설](../profile/guardrails.md):지원되는 데이터 모델을 만들기 위한 모범 사례 [!DNL Profile]를 참조하십시오.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):데이터를 사용하여 세그먼트를 만들 수 [!DNL Real-time Customer Profile] 있습니다.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../xdm/schema/composition.md#union):Experience Platform에서 사용할 스키마를 작성하기 위한 모범 사례를 알아봅니다.

## 사용 사례

다중 엔티티 세그먼테이션의 가치를 설명하려면 대부분의 마케팅 애플리케이션에서 발생하는 문제점을 나타내는 세 가지 표준 마케팅 사용 사례를 고려하십시오.

### 온라인 및 오프라인 구매 데이터 결합

이메일 캠페인을 빌드하는 마케터가 지난 3개월 이내에 최근 고객 스토어 구매를 사용하여 타겟 고객에 대한 세그먼트를 만들려고 시도했을 수 있습니다. 가장 좋은 방법은 이 세그먼트를 구매했던 스토어 이름과 항목 이름 모두를 필요로 하는 것입니다. 이전에는 구매 이벤트에서 스토어 식별자를 캡처하여 개별 고객 프로필에 할당해야 했습니다.

### 장바구니 포기에 대한 이메일 리타겟팅

장바구니 포기를 타깃팅하는 세그먼트로 사용자를 만들고 평가하는 것은 종종 복잡합니다. 개인화된 재타깃팅 캠페인에 포함할 제품을 파악하려면 각 개인이 포기한 제품과 관련된 데이터가 필요합니다. 이 데이터는 이전에 데이터를 모니터링하고 추출하기 어려웠던 상거래 이벤트와 연결되어 있습니다.

## 다중 엔티티 세그먼트 만들기

다중 엔티티 세그먼트를 만들려면 먼저 API 또는 세그먼트 빌더 UI를 사용하여 세그먼트 정의를 작성하기 전에 스키마 간의 관계를 정의해야 [!DNL Segmentation] 합니다.

### 관계 정의

XDM(경험 데이터 모델) 스키마 구조 내에서 관계를 정의하는 것은 다중 엔티티 세그먼트 생성의 필수 부분입니다. 관계의 경우 대상의 필드를 해당 스키마의 기본 ID로 표시해야 합니다. ID는 문자열에만 표시할 수 있으며 배열에 표시할 수 없습니다. 또한 여러 대상에 프로필 및 경험 이벤트를 연결할 수 있으므로 관계를 일대일로 지정할 필요는 없습니다.

관계를 정의하는 작업은 스키마 레지스트리 API 또는 스키마 편집기를 사용하여 수행할 수 있습니다. 두 스키마 간의 관계를 정의하는 방법을 보여주는 자세한 단계는 다음 자습서에서 선택하십시오.

* [API를 사용하여 두 스키마 간의 관계 정의](../xdm/tutorials/relationship-api.md)
* [스키마 편집기 UI를 사용하여 두 스키마 간의 관계 정의](../xdm/tutorials/relationship-ui.md)

### 다중 엔티티 세그먼트 만들기

필요한 XDM 관계를 정의했으면 다중 엔티티 세그먼트를 만들기 시작할 수 있습니다. 세그멘테이션 API 또는 세그먼트 빌더 UI를 사용하여 수행할 수 있습니다. 자세한 내용은 다음 안내서에서 선택하십시오.

* [세그멘테이션 API를 사용하여 세그먼트 만들기](./tutorials/create-a-segment.md)
* [세그먼트 빌더 UI를 사용하여 세그먼트 만들기](./ui/overview.md)

## 다중 엔티티 세그먼트 평가 및 액세스

세그먼트를 만든 후 세그멘테이션 API를 사용하여 세그먼트 결과를 평가하고 액세스할 수 있습니다. 다중 엔티티 세그먼트 평가는 표준 세그먼트 평가와 매우 유사합니다. 이 프로세스는 세그멘테이션 API를 사용해서만 수행할 수 있습니다. API를 사용하여 세그먼트를 평가하고 액세스하는 방법을 보여주는 자세한 안내서는 세그먼트 [평가 및 액세스 자습서를](./tutorials/evaluate-a-segment.md) 참조하십시오.
