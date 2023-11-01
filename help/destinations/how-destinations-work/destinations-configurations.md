---
title: 대상의 구성 가능한 공통 내보내기 설정
description: 대상 수준에서 구성할 수 있는 대상 내보내기 설정과 수정되어 편집할 수 없는 대상을 알아봅니다.
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 1%

---

# 대상의 구성 가능한 공통 내보내기 설정

Experience Platform 대상으로 내보내기 동작을 고려할 때 구성이 작동하는 세 가지 개별 수준을 고려해야 합니다.

* 첫 번째 수준에서 프로필 내보내기 동작과 관련된 일부 설정 및 구성 설정은 대상 유형에 속하는 모든 대상에서 공통입니다. 이러한 설정은 대상 내보내기를 트리거하는 항목과 내보내기에 포함되어 대상 개발자나 Real-Time CDP 사용자가 편집할 수 없는 항목을 참조합니다.
* 두 번째 수준에서 Destination SDK을 사용하여 대상을 작성할 때 대상 개발자가 일부 설정을 대상 수준에서 사용자 지정할 수 있습니다.
* 세 번째 수준에는 Real-Time CDP 사용자가 활성화 워크플로에서 설정할 수 있는 구성 설정이 있습니다.

![대상에 대한 일반 내보내기 설정과 구성 가능한 내보내기 설정 간의 상호 작용을 보여 주는 다이어그램](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

이 페이지에서는 위에 설명된 세 가지 수준에서 대상에 대한 모든 일반 및 구성 가능한 내보내기 설정을 설명하거나 연결합니다.

## 대상 유형 간의 공통 내보내기 설정 {#common-settings-across-destination-types}

대상 내보내기 동작은 대상 유형에 속한 대상 간에 일관됩니다. *대상 내보내기를 트리거하는 것* 및 *대상 내보내기에 포함된 사항*. 대상 내보내기는 대상 서비스가에서 수신하는 알림에 의해 트리거됩니다 [업스트림 실시간 고객 프로필 서비스](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

대상 내보내기에 포함된 내용은 대상 유형 간에 약간 다릅니다. 자세한 내용 [대상 유형별 일반적인 내보내기 동작 패턴](/help/destinations/how-destinations-work/profile-export-behavior.md). 대상 개발자 또는 Real-Time CDP 사용자는 이러한 설정을 편집할 수 없습니다.

## 대상 개발자가 사용자 정의 가능한 내보내기 설정 {#customizable-settings-by-destination-developers}

대상 개발자는 [Destination SDK](/help/destinations/destination-sdk/overview.md) 사용자 지정 또는 프로덕션(비공개 또는 공개) 대상을 만듭니다. Destination SDK은 개발자가 API 끝점 및 파일 수신 시스템의 다운스트림 기능을 기반으로 대상을 구성할 수 있는 뛰어난 유연성을 제공합니다. 다운스트림 기능을 기반으로, 대상 개발자는 Destination SDK을 사용하여 대상을 구성할 때 다음과 같은 구성 옵션을 사용할 수 있습니다.

* Experience Platform 외부에서 대상으로 내보낼 수 있는 속성 및 ID를 결정합니다. 성공적인 데이터 내보내기를 위해 대상에 필요한 ID도 결정합니다.
* API 통합으로 전송될 HTTP 메시지를 집계할 때 Experience Platform이 대기하는 시간을 결정하는 집계 정책을 설정합니다. 대상 개발자는 다양한 집계 유형을 구성하여 발신 HTTP 메시지에 포함되어야 하는 프로필의 수와 HTTP 메시지를 발송할 때까지 Experience Platform이 대기해야 하는 시간을 결정할 수 있습니다. 다음에 대한 광범위한 정보 찾기 [집계 정책 구성 옵션](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) Destination SDK 설명서에서 대상 개발자가 사용할 수 있습니다.
* HTTP 메시지 내보내기에 세그먼트에 적합한 프로필, 세그먼트에서 제거된 프로필 또는 둘 다를 포함해야 하는지 여부를 결정합니다.
* 파일을 내보낼 때 사용자가 사용할 수 있는 파일 이름 및 파일 형식 구성을 결정합니다.

## 사용자가 사용자 지정할 수 있는 데이터 흐름 수준의 설정 {#settings-on-dataflow-level}

대상 유형 및 대상 개발자가 구성한 설정에 따라 편집할 수 없는 설정 외에도 활성화 워크플로에서 사용자가 구성할 수 있는 특정 내보내기 설정이 있습니다. 이러한 설정은 특정 데이터 흐름을 대상으로 내보내기 일정, 데이터 흐름으로 내보내야 하는 속성 및 ID 필드 또는 내보낸 파일의 파일 형식 옵션과 관련됩니다.

대상에 연결할 때 사용자가 사용할 수 있는 설정은 대상 개발자가 대상을 구성한 방법과 사용자가 사용할 수 있도록 한 설정에 따라 다릅니다.

예를 들어 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations), 대상 개발자는 대상에서 허용하는 id를 구성할 수 있으며 그러한 id만 사용자에게 표시됩니다. [활성화 워크플로의 매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), 아래와 같이 표시됩니다.

![활성화 워크플로의 매핑 단계에서 대상 필드에 대한 ID 선택의 화면 기록입니다. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

마찬가지로, 대상 [파일 기반 대상](/help/destinations/destination-types.md#file-based), 대상 개발자는 다음을 결정할 수 있습니다. [파일 이름 추가 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 목적지에 사용할 수 있게 하거나 [파일 서식 옵션](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) 이러한 사용자는 사용 가능하게 하려고 하며, 사용자는 아래와 같이 이러한 옵션에서만 선택할 수 있습니다.

![파일 기반 대상에 연결할 때 파일 형식 옵션의 화면 기록입니다.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![활성화 워크플로의 예약 단계에서 파일 이름 추가 옵션의 화면 기록입니다. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

활성화 워크플로에서 사용할 수 있는 다양한 옵션 및 단계에 대해 자세히 알아보십시오.

* [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](/help/destinations/ui/activate-batch-profile-destinations.md)
* [엔터프라이즈 대상으로 대상 데이터 활성화](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [주문형 파일을 배치 대상으로 내보내기](/help/destinations/ui/export-file-now.md)
* [(베타) 클라우드 스토리지 대상으로 데이터 세트 내보내기](/help/destinations/ui/export-datasets.md)

## 다음 단계 {#next-steps}

이제 이 문서를 읽고 대상 유형에 대해 공통적인 내보내기 설정을 알고, 이를 개발자가 개별 대상 수준에서 구성할 수 있고, 활성화 워크플로에서 사용자가 편집할 수 있는 설정을 지정할 수 있습니다.

다음으로, 다음에 대한 자세한 정보를 읽을 수 있습니다. [대상 유형별 일반적인 내보내기 동작 패턴](/help/destinations/how-destinations-work/profile-export-behavior.md).

대상 개발자의 경우 다음 작업을 수행할 수 있습니다 [시작하기](/help/destinations/destination-sdk/getting-started.md) Destination SDK. 데이터를 활성화하려는 사용자의 경우 [카탈로그](/help/destinations/catalog/overview.md).
