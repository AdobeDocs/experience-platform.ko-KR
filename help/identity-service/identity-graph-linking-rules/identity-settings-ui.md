---
title: ID 설정 UI
description: ID 설정 사용자 인터페이스를 사용하는 방법을 알아봅니다.
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: 7596a87309105897a2727faa8e22b06cdf5547c3
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 4%

---

# ID 설정 UI

>[!IMPORTANT]
>
>이제 [!DNL Identity Graph Linking Rules]을 일반적으로 사용할 수 있습니다. ID 설정을 활성화한 후 축소된 그래프의 축소 취소(&quot;고정&quot;)를 요구하는 기존 샌드박스가 있는 경우 Adobe 계정 팀 또는 Adobe 지원 센터에 문의하십시오.

ID 설정은 고유한 네임스페이스를 지정하고 네임스페이스 우선 순위를 구성하는 데 사용할 수 있는 Adobe Experience Platform ID 서비스 UI의 기능입니다.

ID 서비스 UI 작업 영역에서 [!DNL Graph Simulation] 인터페이스를 사용하는 방법에 대한 자세한 내용은 다음 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops)

UI에서 ID 설정을 구성하는 방법을 배우려면 이 안내서를 참조하십시오.

## 전제 조건

ID 설정 작업을 시작하기 전에 다음 문서를 참조하십시오.

* [[!DNL Identity Graph Linking Rules]](./overview.md)
* [ID 최적화 알고리즘](./identity-optimization-algorithm.md)
* [구현 안내서](./implementation-guide.md)
* [그래프 구성의 예](./example-configurations.md)
* [네임스페이스 우선순위](./namespace-priority.md)
* [그래프 시뮬레이션](./graph-simulation.md)

### 권한 설정 {#set-permissions}

다음으로, 계정이 다음 권한으로 프로비저닝되었는지 확인해야 합니다.

* **[!UICONTROL ID 설정 보기]**: ID 네임스페이스 찾아보기 페이지에서 고유한 네임스페이스 및 네임스페이스 우선 순위를 볼 수 있도록 이 권한을 적용합니다.
* **[!UICONTROL ID 설정 편집]**: ID 설정을 편집하고 저장하려면 이 권한을 적용하세요.

이러한 권한이 없는 경우 관리자에게 문의하십시오. 자세한 내용은 [사용 권한 안내서](../../access-control/abac/ui/permissions.md)를 참조하십시오.

## ID 설정 구성

ID 설정에 액세스하려면 Adobe Experience Platform UI에서 ID 서비스 작업 영역으로 이동한 다음 **[!UICONTROL 설정]**&#x200B;을 선택하십시오.

![&quot;설정&quot; 단추가 선택된 ID 대시보드 인터페이스입니다.](../images/rules/dashboard.png)

ID 설정 페이지는 [!UICONTROL 개인 네임스페이스] 및 [!UICONTROL 장치 또는 쿠키 네임스페이스]의 두 섹션으로 나뉩니다. 개인 네임스페이스는 단일 개인에 대한 식별자입니다. 장치 간 ID, 이메일 주소 및 전화 번호일 수 있습니다. 디바이스 또는 쿠키 네임스페이스는 디바이스 및 웹 브라우저에 대한 식별자이며 개인 네임스페이스보다 높은 우선 순위를 부여할 수 없습니다. 장치 또는 쿠키 네임스페이스를 고유한 네임스페이스로 지정할 수도 없습니다.

### 네임스페이스 우선 순위 구성

네임스페이스 우선 순위를 구성하려면 ID 설정 메뉴에서 네임스페이스를 선택한 다음 해당 네임스페이스를 원하는 순서로 드래그 앤 드롭합니다. 높은 우선 순위를 부여하려면 네임스페이스를 목록에 높게 배치하고, 낮은 우선 순위를 부여하려면 네임스페이스를 목록에 낮게 배치하십시오. 우선 순위가 가장 높은 네임스페이스도 고유한 네임스페이스로 지정해야 합니다.

![개인 네임스페이스가 강조 표시된 ID 설정 작업 영역입니다.](../images/rules/namespace-priority.png)

### 고유한 네임스페이스 지정

고유한 네임스페이스를 지정하려면 해당 네임스페이스에 해당하는 [!UICONTROL 그래프당 고유] 확인란을 선택하십시오. ID 설정 구성에 대해 **최대 3개의 고유한 네임스페이스**&#x200B;를 선택할 수 있습니다.

고유한 네임스페이스가 설정되면 그래프에서 더 이상 고유한 네임스페이스를 포함하는 여러 ID를 가질 수 없습니다. 예를 들어 CRMID를 고유 네임스페이스로 지정한 경우 그래프는 CRMID 네임스페이스와 함께 하나의 ID만 가질 수 있습니다. 자세한 내용은 [ID 최적화 알고리즘 개요](./identity-optimization-algorithm.md#unique-namespace)를 참조하십시오.

구성을 마쳤으면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속 진행하십시오.

![고유한 네임스페이스로 두 개의 네임스페이스가 선택되었습니다.](../images/rules/unique-namespace.png)

여기에서 마지막 단계로 진행하기 전에 다음 사항을 확인해야 합니다.

1. 선택한 고유한 네임스페이스입니다.
2. 알려진 각 프로필에서 우선 순위가 가장 높은 고유 네임스페이스를 가진 ID의 존재
3. 네임스페이스 우선 순위.

![확인 창에서 &quot;확인&quot; 단추를 선택했습니다.](../images/rules/confirmation.png)

### 설정 확인 {#confirm-your-settings}

>[!IMPORTANT]
>
>* 마지막 단계는 설정을 저장한 후 그래프가 업데이트되는 경우에만 그래프 알고리즘 **의 영향을 받는 기존 그래프와 네임스페이스 우선 순위를 변경한 후에도 실시간 고객 프로필에 있는 이벤트 조각의 기본 ID가 업데이트되지 않는다는 다른 확인 메시지입니다.**
>
>* 새 설정 또는 업데이트된 설정을 적용하려면 최대 **24시간**&#x200B;이 걸립니다. 확인하려면 샌드박스 이름을 입력한 다음 **[!UICONTROL 확인]**&#x200B;을 선택하세요.
>
>* ID 설정을 저장할 때까지 데이터가 변경되지 않습니다.

![구성을 처리하기 전에 24시간 지연에 대한 경고를 표시하는 확인 창입니다.](../images/rules/complete.png)

## 다음 단계

[!DNL Identity Graph Linking Rules]에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [[!DNL Identity Graph Linking Rules] 개요](./overview.md)
* [ID 최적화 알고리즘](./identity-optimization-algorithm.md)
* [구현 안내서](./implementation-guide.md)
* [그래프 구성의 예](./example-configurations.md)
* [문제 해결 및 FAQ](./troubleshooting.md)
* [네임스페이스 우선순위](./namespace-priority.md)
* [그래프 시뮬레이션 UI](./graph-simulation.md)