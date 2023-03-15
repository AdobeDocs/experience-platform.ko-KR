---
title: Privacy Console 개요
description: Adobe Experience Platform UI에서 개인 정보 보호 관련 워크플로우를 모니터링하는 방법을 알아봅니다.
source-git-commit: 1fac36a0fd767add92283cd256d8bcea783ecf3b
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 3%

---

# Privacy Console 개요

다음 [!UICONTROL 개인 정보 보호 콘솔] 탭 Adobe Experience Platform UI는 데이터 위생 작업 주문, Privacy Service의 데이터 주체 요청 및 플랫폼 사용자 활동에 대한 감사 로그를 포함하여 플랫폼에서의 개인 정보 보호 관련 작업에 대한 대시보드 보기를 제공합니다.

대시보드에 액세스하려면 를 선택합니다. **[!UICONTROL 개인 정보 보호 콘솔]** 왼쪽 탐색.

![이미지 표시 중 [!UICONTROL 개인 정보 보호 콘솔] Platform UI 내의 왼쪽 탐색에서 선택](../images/governance-privacy-security/privacy-console/left-nav.png)

여기에서 사용 가능한 을(를) 검토할 수 있습니다 [위젯 모니터링](#widgets) 콘솔에서 제공되거나 여러 개 중 하나를 탐색할 수 있습니다 [사용 사례 안내서](#use-case-guides) 플랫폼의 개인 정보 보호 기능에 대해 설명합니다.

## 위젯

[!UICONTROL 개인 정보 보호 콘솔] 은 개인 정보 보호 작업을 모니터링하는 데 도움이 되는 몇 가지 위젯을 제공합니다.

![이미지 표시 중 [!UICONTROL 개인 정보 보호 콘솔] Platform UI 내의 왼쪽 탐색에서 선택](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>조직에서 구입한 SKU에 따라 아래에 언급된 일부 위젯을 사용할 수 없습니다.

각 위젯의 기능은 아래에 설명되어 있습니다.

| 위젯 이름 | 설명 |
| --- | --- |
| 데이터 위생 작업 주문 상태 | 아래 레코드 삭제 프로세스의 상태를 표시합니다. [데이터 위생](../../hygiene/home.md) 선택한 시간대에 사용됩니다. 드롭다운 메뉴를 사용하여 최근 7일, 14일 및 30일 사이의 시간대를 변경합니다. |
| 최근 데이터 위생 작업 주문 | 가장 최근 항목 표시 [데이터 위생](../../hygiene/home.md) 시스템에서 처리 중인 작업 주문. 드롭다운을 사용하여 최근에 만든 작업 주문과 최근에 업데이트한 작업 주문 간을 전환할 수 있습니다. |
| 가장 빈번한 작업 | 에서 캡처한 대로 플랫폼에서 가장 빈번한 작업을 표시합니다. [감사 로그](./audit-logs/overview.md) 선택한 시간대에 사용됩니다. 드롭다운 메뉴를 사용하여 최근 7일, 14일 및 30일 사이의 시간대를 변경합니다. |
| 가장 활동적인 사용자 | 에서 캡처한 대로 조직 내에서 가장 활동적인 Platform 사용자를 표시합니다. [감사 로그](./audit-logs/overview.md) 선택한 시간대에 사용됩니다. 드롭다운 메뉴를 사용하여 최근 7일, 14일 및 30일 사이의 시간대를 변경합니다. |
| 데이터 주제 요청 | 이 제출하고 완료한 데이터 주체 요청 수를 표시합니다. [Privacy Service](../../privacy-service/home.md) 지정된 날을 위해. |

{style="table-layout:auto"}

## 사용 사례 안내서

콘솔은 기본 구현을 설정하는 방법에 대한 간결한 지침을 포함하여 플랫폼의 일반적인 개인 정보 보호 워크플로를 소개하는 여러 가지 제품 내 안내서를 제공합니다.

![이미지 표시 중 [!UICONTROL 개인 정보 보호 콘솔] Platform UI 내의 왼쪽 탐색에서 선택](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## 다음 단계

개인 정보 사용 사례와 관련된 다양한 플랫폼 서비스에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [속성 기반 액세스 제어](../../access-control/abac/overview.md)
* [감사 로그](./audit-logs/overview.md)
* [데이터 거버넌스](../../data-governance/home.md)
* [데이터 위생](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
