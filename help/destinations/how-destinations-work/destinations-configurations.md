---
title: 대상의 구성 및 공통 내보내기 설정
description: 대상 수준에서 구성할 수 있는 대상의 내보내기 설정과 수정되어 편집할 수 없는 설정을 알아봅니다.
source-git-commit: 372231ab4fc1148c1c2c0c5fdbfd3cd5328b17cc
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---


# 대상의 구성 및 공통 내보내기 설정

Experience Platform 대상으로 내보내기 동작을 생각할 때 어떤 구성이 작동하는지 세 가지 개별 수준을 고려해야 합니다.

* 첫 번째 수준에서 프로필 내보내기 동작 및 구성 설정과 관련된 일부 설정은 대상 유형에 속하는 모든 대상에서 공통됩니다. 이러한 설정은 대상 내보내기를 트리거하는 항목 및 내보내기에 포함된 항목을 말하며 대상 개발자나 실시간 CDP 사용자가 편집할 수 없습니다.
* 두 번째 수준에서, Destination SDK을 사용하여 대상을 작성할 때 대상 개발자가 대상 수준에서 일부 설정을 사용자 지정할 수 있습니다.
* 세 번째 단계에서는 활성화 워크플로우에서 실시간 CDP 사용자가 설정할 수 있는 구성 설정이 있습니다.

![대상에 대한 공통 및 구성 가능한 내보내기 설정 간의 상호 작용을 보여주는 다이어그램](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

이 페이지에서는 위에 요약된 세 가지 수준에서 대상에 대한 모든 공통 및 구성 가능한 내보내기 설정에 대해 설명하거나 연결합니다.

## 대상 유형 간의 공통 내보내기 설정 {#common-settings-across-destination-types}

대상 내보내기 동작은 대상 유형에 속하는 대상 간에 *대상 내보내기를 트리거하는 항목* 및 *대상 내보내기에 포함된 사항*. 대상 내보내기는 대상 서비스가 [업스트림 실시간 고객 프로필 서비스](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

대상 내보내기에 포함된 내용은 대상 유형에 따라 약간 다릅니다. 자세한 내용 [대상 유형별 일반 내보내기 동작 패턴](/help/destinations/how-destinations-work/profile-export-behavior.md). 대상 개발자나 실시간 CDP 사용자는 이러한 설정을 편집할 수 없습니다.

## 대상 개발자의 사용자 지정 가능한 내보내기 설정 {#customizable-settings-by-destination-developers}

대상 개발자는 [Destination SDK](/help/destinations/destination-sdk/overview.md) 사용자 지정 또는 생성(비공개 또는 공개) 대상을 만들 수 있습니다. Destination SDK은 개발자에게 API 엔드포인트 및 파일 수신 시스템의 다운스트림 기능을 기반으로 대상을 구성할 수 있는 탁월한 유연성을 제공합니다. 다운스트림 기능을 기반으로 대상 개발자는 Destination SDK을 사용하여 대상을 구성할 때 다음과 같은 구성 옵션을 사용할 수 있습니다.

* Experience Platform에서 대상으로 내보낼 수 있는 속성과 ID를 결정합니다. 성공적인 데이터 내보내기를 위해 해당 대상에 필요한 ID도 결정합니다.
* API 통합으로 전송할 HTTP 메시지를 집계할 때 Experience Platform이 대기하는 시간을 결정하는 집계 정책을 설정합니다. 대상 개발자는 다른 집계 유형을 구성하여 보내는 HTTP 메시지에 포함해야 하는 프로필의 수와 HTTP 메시지를 발송할 때까지 Experience Platform이 기다리는 시간을 결정할 수 있습니다. 에 대한 다양한 정보 찾기 [집계 정책 구성 옵션](/help/destinations/destination-sdk/destination-configuration.md#aggregation) Destination SDK 설명서에서 대상 개발자가 사용할 수 있습니다.
* HTTP 메시지 내보내기에 세그먼트를 사용할 수 있는 프로필, 세그먼트에서 제거된 프로필 또는 둘 다 포함해야 하는지 확인합니다.
* 파일을 내보낼 때 사용자가 사용할 수 있어야 하는 파일 이름 및 파일 형식 구성을 결정합니다.

## 사용자가 사용자 지정할 수 있는 데이터 흐름 수준의 설정 {#settings-on-dataflow-level}

대상 유형 및 대상 개발자가 구성한 설정에 따라 편집할 수 없는 설정 위에 활성화 워크플로우에서 사용자가 구성할 수 있는 특정 내보내기 설정이 있습니다. 이러한 설정은 특정 데이터 흐름을 대상으로 내보내기 일정, 데이터 플로에서 내보내야 하는 속성 및 ID 필드 또는 내보낸 파일의 파일 형식 지정 옵션과 관련이 있습니다.

대상에 연결할 때 사용자가 사용할 수 있는 설정은 대상 개발자가 대상을 구성한 방법과 사용자가 사용할 수 있도록 설정한 설정에 따라 다릅니다.

예, 예 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations), 대상 개발자는 대상이 허용하는 ID를 구성할 수 있으며 그러한 ID만 사용자에게 표시됩니다 [활성화 워크플로우의 매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)를 아래와 같이 표시합니다.

![활성화 워크플로우의 매핑 단계에서 대상 필드에 대한 ID 선택 사항의 화면 기록. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

마찬가지로, 용 [파일 기반 대상](/help/destinations/destination-types.md#file-based)를 지정하는 경우 대상 개발자가 [파일 추가 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 목적지 또는 목적지에 사용할 수 있도록 [파일 서식 옵션](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) 사용자는 아래 표시된 대로 이 옵션에서만 선택할 수 있습니다.

![파일 기반 대상에 연결할 때 파일 형식 옵션의 화면 기록](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![활성화 워크플로우의 예약 단계에서 파일 이름 추가 옵션의 화면 녹화를 참조하십시오. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

활성화 워크플로우에서 사용할 수 있는 다양한 옵션 및 단계에 대해 자세히 알아보십시오.

* [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](/help/destinations/ui/activate-batch-profile-destinations.md)
* [엔터프라이즈 대상으로 대상 데이터 활성화](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [배치 대상으로 온디맨드 파일 내보내기](/help/destinations/ui/export-file-now.md)
* [(베타) 클라우드 스토리지 대상으로 데이터 세트 내보내기](/help/destinations/ui/export-datasets.md)

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 개발자가 개별 대상 수준에서 구성할 수 있는 대상 유형에 공통되는 대상에 대한 내보내기 설정과 활성화 워크플로우에서 사용자가 편집할 수 있는 설정을 알고 있습니다.

다음으로, [대상 유형별 일반 내보내기 동작 패턴](/help/destinations/how-destinations-work/profile-export-behavior.md).

대상 개발자의 경우 다음을 수행할 수 있습니다 [시작하기](/help/destinations/destination-sdk/getting-started.md) Destination SDK 사용. 데이터를 활성화하려는 사용자의 경우, [카탈로그](/help/destinations/catalog/overview.md).