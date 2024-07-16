---
title: 태그 일관성 테스트 참조
description: Auditor가 Adobe Experience Platform Debugger에서 태그 일관성을 테스트하는 방법을 알아봅니다.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 38%

---

# 태그 일관성 테스트 참조

이 참조는 태그 일관성을 위한 Adobe Experience Platform Debugger 테스트에서 Auditor 기능이 어떻게 작동하는지 자세히 설명합니다.

>[!NOTE]
>
>Platform Debugger의 Auditor 테스트에 대한 자세한 내용은 [Auditor 기능 개요](./overview.md)를 참조하십시오.

태그 일관성 테스트는 검사한 모든 페이지에서 일치하지 않는 것을 찾습니다. 이는 정확한 데이터 수집을 위해 사이트의 모든 페이지에서 동일해야 하는 값 또는 구성입니다.

| 테스트 | 두께 | 기준 | 권장 사항 |
| --- | --- | --- | --- |
| Adobe Analytics - 일관된 코드 버전 | 5 | 둘 이상의 Analytics 코드 버전을 찾았습니다. | Analytics의 모든 인스턴스를 현재 버전으로 바꿉니다.<br><br>[추가 정보](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |

{style="table-layout:auto"}
