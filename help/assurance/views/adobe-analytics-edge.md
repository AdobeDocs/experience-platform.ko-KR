---
title: Assurance의 Analytics Events 2.0
description: 이 안내서에서는 Adobe Experience Platform Assurance와 함께 Adobe Analytics 및 Analytics Edge 보기를 사용하는 방법을 설명합니다.
badgeBeta: label="Beta" type="Informative"
exl-id: faaa2c1d-3471-4d86-9a25-03265b996e31
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 19%

---

# Assurance의 Analytics Events 2.0

Analytics 이벤트 2.0에서는 사용자에게 Adobe Analytics 구현을 디버깅하고 확인하는 데 SDK 이벤트를 더 다양하게 볼 수 있습니다. 이 보기는 [Adobe Analytics Mobile SDK](https://developer.adobe.com/client-sdks/solution/adobe-analytics/)와 [Adobe Experience Platform Edge Network SDK](https://developer.adobe.com/client-sdks/edge/edge-network/)에서 Adobe Experience Platform으로 전송된 이벤트를 보여 줍니다. 또한 이 보기에는 장치에서 나간 후 업스트림 서비스와 클라이언트 SDK에서 이벤트를 처리한 방식에 대한 컨텍스트를 제공하는 세부 정보 패널이 포함되어 있습니다.

## 시작하기

이 보기를 사용하려면 다음 단계를 완료하십시오.

1. [Adobe Experience Platform 보증 설정](../tutorials/implement-assurance.md).
2. [보증 세션을 만들고 연결합니다](../tutorials/using-assurance.md).
3. 왼쪽 탐색 **홈** 보기 메뉴의 Assurance UI에서 **Analytics 이벤트 2.0(Beta)**&#x200B;을(를) 선택합니다. 이 옵션이 표시되지 않으면 창 왼쪽 하단에서 **구성**&#x200B;을 선택하고 **Analytics 이벤트 2.0(Beta)**&#x200B;을 추가한 다음 **저장**&#x200B;을 선택합니다.

## Analytics 이벤트 보기

**Adobe Analytics** 모바일 확장을 사용하는 경우 Analytics 이벤트 보기를 사용하십시오. 이 보기를 사용하면 추적 작업, 추적 상태 및 라이프사이클 이벤트를 포함하여 연결된 클라이언트에서 전송된 Analytics 이벤트를 쉽게 볼 수 있습니다. 표에서 Analytics 이벤트 중 하나를 선택하면 이벤트 처리 방법에 대한 세부 정보가 오른쪽 패널에 표시됩니다.

![Analytics 이벤트 보기에서 다른 구성 요소를 보여 주는 이미지입니다.](./images/adobe-analytics-edge/analytics-events.png)

### 후처리 상태

SDK가 Adobe Analytics을 사용하여 네트워크 요청을 수행하면 Assurance가 Adobe Analytics 요청에 대한 사후 처리 정보를 검색할 수 있는지 상태가 알려줍니다. 요청이 트리거된 후 사후 처리 상태가 작동 중인 경우 Analytics 이벤트 보기는 활성 상태를 유지해야 합니다.

후처리 정보를 검색하려면 로그인한 사용자에게 해당 보고서 세트에 대한 액세스 권한이 있어야 합니다.

| 상태 | 설명 |
| :----- | :---------- |
| `Queued` | 네트워크 요청이 후처리 정보를 가져오는 중입니다. |
| `Processed` | 네트워크 요청이 성공했으며 후처리 정보가 수신되었습니다. |
| `Delayed` | 후처리 정보를 가져오기 위한 최대 요청 재시도 횟수를 초과했습니다. |
| `Error` | 오류로 인해 네트워크 요청이 실패했습니다. 오류에 대한 자세한 내용은 이벤트 상세 보기에 표시됩니다. |
| `Unauthorized` | 사용자는 Adobe Analytics 보고서 세트에 액세스할 수 없습니다. |
| `Unavailable` | Adobe Analytics 요청에는 해당 `AnalyticsResponse` 이벤트가 없습니다. |
| `No Debug Flag` | 현재 Adobe Analytics 또는 Assurance SDK 버전은 Analytics 디버깅 기능을 지원하지 않을 수 있습니다. 자세한 내용은 [문제 해결 안내서](../troubleshooting.md)를 참조하십시오. |
| `Expired` | `AnalyticsTrack` 또는 `LifecycleStart` 이벤트는 24시간이 지났습니다. |

### 이벤트 상세 보기

Analytics 추적 이벤트의 경우 상세 보기에는 다음 부분이 포함됩니다.

- 원래 SDK Analytics 요청 이벤트입니다.
- 보고서 세트 ID, SDK 확장 버전 및 컨텍스트 데이터와 같은 요청의 메타데이터 및 컨텍스트 데이터.
- Post, evar 및 prop의 매핑이 포함된 Analytics 이벤트에 대한 Analytics 처리 정보입니다.

### Analytics 보기 유효성 검사

유효성 검사 보기를 사용하면 Analytics와 관련된 유효성 검사 스크립트에 대한 결과를 쉽게 볼 수 있습니다. 유효성 검사기에 표시되는 오류에는 수정해야 하는 위치에 대한 링크가 포함되어 있거나 오류 상태에 있는 이벤트가 표시될 수 있습니다.

![Analytics 보기에서 유효성 검사기 탭을 표시하는 이미지입니다.](./images/adobe-analytics-edge/analytics-validation-view.png)

## Analytics Edge 보기

**Edge Network** 또는 **Edge Bridge** 모바일 확장을 사용하는 경우 Analytics Edge 보기를 사용하십시오. 이 보기를 활성화하려면 오른쪽 상단의 &quot;Analytics Edge(Beta)&quot; 토글을 선택하여 현재 세션에서 Edge 네트워크를 통해 전송된 Analytics 이벤트를 확인합니다. 여기에는 추적 작업 및 추적 상태를 기반으로 라이프사이클 확장, Edge 요청 및/또는 Edge Bridge 이벤트에 의해 실행된 모든 이벤트가 포함됩니다.

![Analytics 보기와 Analytics Edge 보기 간에 전환하는 데 사용되는 토글을 표시하는 이미지입니다.](./images/adobe-analytics-edge/analytics-view-toggle.png)

Analytics Edge 보기에는 클라이언트가 발송한 Analytics 관련 Edge 요청 및 라이프사이클 메서드에 대한 정보가 포함되어 있습니다. 오른쪽 패널에는 목록에서 이벤트를 선택하여 클라이언트 SDK와 장치에서 나간 후 업스트림 서비스에서 처리한 이벤트가 표시되므로 호출로 인한 이벤트 체인을 쉽게 볼 수 있습니다.

![Analytics Edge 보기에서 다른 구성 요소를 보여 주는 이미지입니다.](./images/adobe-analytics-edge/edge-analytics-events.png)

### Analytics Edge 유효성 검사

Analytics Edge 유효성 검사 보기를 사용하면 Analytics Edge과 관련된 유효성 검사 스크립트에 대한 결과를 쉽게 볼 수 있습니다. 유효성 검사기에 표시되는 오류에는 수정해야 하는 위치에 대한 링크가 포함되어 있거나 오류 상태에 있는 이벤트가 표시될 수 있습니다.

![Analytics Edge 보기에서 유효성 검사기 탭을 표시하는 이미지입니다.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)
