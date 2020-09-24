---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: 실시간 고객 프로필 자습서
topic: tutorial
type: Tutorial
description: 이 문서에서는 관련 단계에 대해 설명하고 각 개별 워크플로우를 완료하기 위한 자습서에 대한 링크를 제공합니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# 구성 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service]

조직에 대해 구성하려면 여러 개의 별도 워크플로우 [!DNL Real-time Customer Profile] 를 완료해야 합니다. 이 문서에서는 관련 단계에 대해 설명하고 각 개별 워크플로우를 완료하기 위한 자습서에 대한 링크를 제공합니다. 자세한 내용 [!DNL Real-time Customer Profile]은 프로필 [개요를 읽으십시오](../profile/home.md).

## 및 [!DNL Profile] 에 대한 스키마 활성화 [!DNL Identity]

데이터를 Adobe Experience Platform으로 인제스트하여 데이터 생성 시 사용하려면 인제스트할 데이터 구조를 제공하고 이 스키마를 [!DNL Real-time Customer Profiles]및 Adobe Experience Platform에서 사용하도록 설정해야 합니다 [!DNL Profile] [!DNL Identity Service]. 스키마 레지스트리 API를 사용하여 스키마 [!DNL Profile] 를 [!DNL Identity Service]생성하거나 스키마 빌더 UI를 사용하여 스키마 [를](../xdm/tutorials/create-schema-api.md) 만드는 방법에 대한 단계별 지침을 참조하십시오 [](../xdm/tutorials/create-schema-ui.md).

## 데이터 세트 구성 [!DNL Profile] 및 [!DNL Identity]

데이터 인제스트를 시작하려면 및 [!DNL Profile]과 함께 사용할 수 있도록 적절하게 구성된 데이터 세트 [!DNL Real-time Customer Profile] 가 있어야 합니다 [!DNL Identity Service]. 시작하려면 프로필 및 ID용 데이터 세트 [구성을 따르십시오](../profile/tutorials/dataset-configuration.md).

## 병합 정책 구성

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 취합하여 개별 고객의 전체 상황을 파악할 수 있습니다. 이 데이터를 취합할 때 병합 정책은 데이터의 우선 순위를 매기는 방법과 데이터를 결합하여 통합 뷰를 생성하는 데 [!DNL Platform] 사용하는 규칙입니다. RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. UI에서 병합 정책을 [!DNL Platform] 사용하려면 [병합 정책 사용 안내서를 참조하십시오](../profile/ui/merge-policies.md). 실시간 고객 프로필 API를 사용하여 병합 정책을 사용하려면 [병합 정책 개발자 안내서를 참조하십시오](../profile/api/merge-policies.md).

## 에지 예측 구성

여러 채널에서 실시간으로 고객의 기대에 부응하는 개인화된 경험을 제공하기 위해서는 변경 사항이 발생하면 즉시 정확한 데이터를 제공하고 지속적으로 업데이트해야 합니다. Adobe [!DNL Experience Platform] 를 사용하면 가장자리라고 하는 요소를 사용하여 데이터에 대한 실시간 액세스를 구현할 수 있습니다. Edge는 데이터를 저장하고 애플리케이션에서 쉽게 액세스할 수 있도록 하는 지리적으로 배치된 서버입니다. 데이터는 투영에 의해 모서리로 라우팅되고, 투영 대상은 데이터가 전송될 가장자리를 정의하며, 가장자리에서 사용할 특정 정보를 정의하는 투영 구성이 있습니다. 자세한 내용을 살펴보고 가장자리 예상 [!DNL Real-time Customer Profile] 부분에 대한 [API](../profile/api/edge-projections.md)하위 안내서를 참조하십시오.

## 다음 단계

조직 [!DNL Real-time Customer Profile] 에 대해 구성한 후에는 개별 고객 프로필에 데이터를 추가하고 특정 고객 특성을 기반으로 고객 세그먼트를 만들 수 있습니다. 시작하려면 다음 자습서를 참조하십시오.

* [실시간 고객 프로필에 데이터 추가](../profile/tutorials/add-profile-data.md)
* [세그먼트 만들기](../segmentation/tutorials/create-a-segment.md)