---
title: Privacy Console 개요
description: Adobe Experience Platform UI에서 개인 정보 보호 관련 워크플로우를 모니터링하는 방법을 알아봅니다.
feature: Privacy
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 4%

---

# Privacy Console 개요

Adobe Experience Platform UI의 [!UICONTROL 개인 정보 보호 콘솔] 탭은 데이터 위생 작업 주문, Privacy Service의 데이터 주체 요청 및 Experience Platform 사용자 활동에 대한 감사 로그를 포함하여 Experience Platform에서의 개인 정보 보호 관련 작업에 대한 대시보드 보기를 제공합니다.

대시보드에 액세스하려면 왼쪽 탐색에서 **[!UICONTROL 개인 정보 보호 콘솔]**&#x200B;을 선택하십시오.

![Experience Platform UI의 왼쪽 탐색에서 [!UICONTROL 개인 정보 보호 콘솔]을 선택하는 동안 표시되는 이미지](../images/governance-privacy-security/privacy-console/left-nav.png)

여기에서 콘솔에서 제공하는 사용 가능한 [모니터링 위젯](#widgets)을 검토하거나 Experience Platform의 개인 정보 보호 기능에 대한 여러 [사용 사례 안내서](#use-case-guides) 중 하나를 살펴볼 수 있습니다.

## 위젯

[!UICONTROL 개인 정보 보호 콘솔]에서는 개인 정보 보호 작업을 모니터링하는 데 도움이 되는 몇 가지 위젯을 제공합니다.

![Experience Platform UI의 왼쪽 탐색에서 [!UICONTROL 개인 정보 보호 콘솔]을 선택하는 동안 표시되는 이미지](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>조직에서 구입한 SKU에 따라 아래에 언급된 일부 위젯을 사용할 수 없습니다.

각 위젯의 기능은 아래에 설명되어 있습니다.

| 위젯 이름 | 설명 |
| --- | --- |
| 데이터 위생 작업 주문 상태 | 선택한 일정의 [데이터 위생](../../hygiene/home.md) 아래에 레코드 삭제 프로세스의 상태를 표시합니다. 드롭다운 메뉴를 사용하여 최근 7일, 14일 및 30일 사이의 시간대를 변경합니다. |
| 최근 데이터 위생 작업 주문 | 시스템에서 처리 중인 가장 최근 [데이터 위생](../../hygiene/home.md) 작업 주문을 표시합니다. 드롭다운을 사용하여 최근에 만든 작업 주문과 최근에 업데이트한 작업 주문 간을 전환할 수 있습니다. |
| 가장 빈번한 액션 | 선택한 기간 동안 [감사 로그](./audit-logs/overview.md)에서 캡처한 가장 빈번한 작업을 Experience Platform에서 표시합니다. 드롭다운 메뉴를 사용하여 최근 7일, 14일 및 30일 사이의 시간대를 변경합니다. |
| 대부분의 활성 사용자 | 선택한 기간 동안 [감사 로그](./audit-logs/overview.md)에서 캡처한 조직 내 가장 활동적인 Experience Platform 사용자를 표시합니다. 드롭다운 메뉴를 사용하여 최근 7일, 14일 및 30일 사이의 시간대를 변경합니다. |
| 데이터 주제 요청 | 지정된 날짜 동안 [Privacy Service](../../privacy-service/home.md)이(가) 제출하고 완료한 데이터 주체 요청 수를 표시합니다. |

{style="table-layout:auto"}

## 사용 사례 안내서

콘솔은 기본 구현을 설정하는 방법에 대한 간결한 지침을 포함하여 Experience Platform의 일반적인 개인 정보 보호 워크플로를 소개하는 여러 가지 제품 내 안내서를 제공합니다.

![Experience Platform UI의 왼쪽 탐색에서 [!UICONTROL 개인 정보 보호 콘솔]을 선택하는 동안 표시되는 이미지](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## 다음 단계

개인 정보 보호 사용 사례와 관련된 다양한 Experience Platform 서비스에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [속성 기반 액세스 제어](../../access-control/abac/overview.md)
* [감사 로그](./audit-logs/overview.md)
* [데이터 거버넌스](../../data-governance/home.md)
* [데이터 위생](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
