---
title: 일반 Analytics 확장 개요
description: Adobe Experience Platform의 일반 Analytics 태그 확장에 대해 알아봅니다.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 77%

---

# 일반 Analytics 플러그인 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

일반 Analytics 플러그인 확장 프로그램 구성 및 이 확장 프로그램을 사용하여 [!DNL Adobe Analytics] 확장 프로그램을 늘릴 때 사용할 수 있는 옵션에 대한 정보를 보려면 이 참조를 사용하십시오.

## 일반 Analytics 플러그인 확장 프로그램 구성

이 섹션에서는 Adobe Analytics 확장 프로그램을 구성할 때 사용할 수 있는 옵션에 대한 참조를 제공합니다.

>[!IMPORTANT]
>
>일반 Analytics 플러그인 확장 프로그램은 [!DNL Adobe Analytics] 확장 프로그램을 늘립니다. 이 확장 프로그램이 작동하려면 속성에 [!DNL Adobe Analytics] 확장 프로그램이 설치되어 있어야 합니다. 또한 추적기가 [!DNL Adobe Analytics] 확장 프로그램에서 전체적으로 액세스할 수 있도록 해야 합니다.

확장 프로그램 수준에서 추가 구성이 필요하지 않습니다.

## [!DNL Adobe Analytics] 확장 프로그램에 플러그인 추가

이 확장 프로그램에서 제공되는 플러그인을 사용하려면 먼저 고유한 규칙에서 사용할 플러그인을 초기화해야 합니다.

1. 새 규칙을 만듭니다.
1. 코어 - 라이브러리 불러오기(페이지 상단) 이벤트를 추가합니다.
1. 아래의 초기화 방법 중 하나를 사용합니다.

## 일반적인 Analytics 플러그인 확장 프로그램 작업 유형

이 섹션에서는 일반 Analytics 플러그인 확장 프로그램에서 사용할 수 있는 작업 유형을 설명합니다.

일반 Analytics 플러그인 확장 프로그램은 다음 작업을 제공합니다.

* [초기화](#initialize)
* [플러그인 초기화](#initialize-plugin)

### 초기화

>[!IMPORTANT]
>
>이 작업을 쉽게 구현할 수 있지만 Adobe Consulting에서는 플러그인의 가중치를 늘리도록 이 작업을 사용할 것을 권장합니다.

이 작업에서는 구현에 포함할 각 플러그인을 선택하고 변경 내용을 저장할 수 있습니다. 구현 중에 사용할 만큼만 선택합니다.

### 플러그인 초기화

이러한 작업은 개별적으로 사용할 특정 플러그인을 초기화합니다. 속성에 사용할 플러그인을 모두 초기화하려면 해당 작업을 규칙에 추가하고 규칙을 저장하면 됩니다. 이러한 방식으로 확장 프로그램을 구성하는 데 약간 더 많은 작업이 필요하지만 코드 효율성이 향상됩니다. 따라서 이 방법을 사용하는 것이 좋습니다.

## 일반 Analytics 플러그인 확장 데이터 요소

다음 데이터 요소는 Analytics에서 해당 플러그인을 설정하고 구성하는 태그 기능을 활용하는 일반 Analytics 플러그인 확장에서 사용할 수 있습니다.

* `getGeoCoordinates`
* `getNewRepeat`
* `getPageName`
* `getResponsiveLayout`
* `getTimeParting`
* `getTimeSinceLastVisit`
* `getVisitDuration`
* `getVisitNum`

>[!NOTE]
>
>위의 플러그인에 대한 자세한 내용은 [Analytics 설명서](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html).
