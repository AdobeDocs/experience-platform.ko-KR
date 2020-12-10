---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;destinations
description: Adobe Experience Platform의 소스 커넥터는 예약된 기준으로 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 소스 작업 영역에서 기존 데이터 흐름을 보는 단계를 제공합니다.
solution: Experience Platform
title: 데이터 흐름 모니터링
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 791ad61f2f28da03ef3e5cb5efdd89154e9b1a0b
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%

---


# UI의 대상에 대한 데이터 흐름 모니터링

대상을 사용하면 Adobe Experience Platform에서 수많은 외부 파트너에 이르는 데이터를 활성화할 수 있습니다. 이 자습서에서는 Experience Platform 사용자 인터페이스를 사용하여 대상에 대한 데이터 흐름을 모니터링하는 방법에 대한 지침을 제공합니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [대상](../../destinations/home.md):대상은 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 많은 사용 사례를 위해 플랫폼에서 데이터를 원활하게 활성화할 수 있도록 하는 일반적으로 사용되는 애플리케이션과의 사전 구축된 통합입니다.
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 데이터 흐름 모니터링

플랫폼 UI의 **[!UICONTROL 대상]** 작업 영역에서 **[!UICONTROL 찾아보기]** 탭으로 이동하여 보려는 대상의 이름을 선택합니다.

![](../assets/ui/monitor-destinations/select-destination.png)

기존 데이터 흐름 목록이 나타납니다. 이 페이지에서는 대상, 사용자 이름, 데이터 흐름 수 및 상태에 대한 정보를 비롯하여 볼 수 있는 데이터 흐름 목록이 있습니다.

상태에 대한 자세한 내용은 다음 표를 참조하십시오.

| 상태 | 설명 |
| ------ | ----------- |
| 활성화됨 | 상태는 데이터 흐름 `Enabled` 이 활성화되어 있고 제공된 일정에 따라 데이터를 인제스트하고 있음을 나타냅니다. |
| 비활성화됨 | 상태는 데이터 흐름 `Disabled` 이 비활성 상태이며 데이터를 인제스트하고 있지 않음을 나타냅니다. |
| 처리 중 | 상태는 데이터 흐름 `Processing` 이 아직 활성화되지 않았음을 나타냅니다. 이 상태는 종종 새 데이터 흐름 만들기 직후 발생합니다. |
| 오류 | 데이터 흐름 활성화 프로세스가 중단되었음을 `Error` 나타냅니다. |

## [!UICONTROL 데이터 흐름 실행]

데이터 흐름 [!UICONTROL 실행] 탭은 데이터 흐름 실행에 대한 지표 데이터를 일괄 처리 대상으로 제공합니다. 프로필 레코드에 대한 다음 합계와 함께 개별 실행 및 특정 지표 목록이 표시됩니다.

- **[!UICONTROL 프로필 레코드 활성화]**:활성화용으로 생성되었거나 업데이트된 프로필 레코드의 총 수입니다.
- **[!UICONTROL 건너뛴 프로필 레코드]**: 프로필 종료 또는 누락된 특성을 기반으로 활성화용으로 생략된 프로필 레코드의 총 수입니다.

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>Dataflow는 대상 데이터 프롤의 예약 빈도를 기반으로 생성됩니다. 세그먼트에 적용된 각 병합 정책에 대해 별도의 데이터 흐름 실행이 수행됩니다.

특정 데이터 흐름 실행에 대한 세부 정보를 보려면 목록에서 실행 시작 시간을 선택합니다. 데이터 흐름 실행을 위한 세부 정보 페이지에는 처리된 데이터 크기 및 오류 진단에 대한 세부 정보와 함께 발생한 오류 목록과 같은 추가 정보가 포함되어 있습니다.

![](../assets/ui/monitor-destinations/dataflow.png)