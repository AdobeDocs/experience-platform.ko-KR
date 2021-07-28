---
title: Adobe Experience Platform Web SDK Extension의 데이터 요소 유형
description: Adobe Experience Platform Web SDK 태그 확장에서 제공하는 다양한 데이터 요소 유형에 대해 알아봅니다.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 49%

---

# 데이터 요소 유형

[Adobe Experience Platform Web SDK 태그 확장](web-sdk-extension-configuration.md)에서 [작업 유형](action-types.md)을 설정한 후 데이터 요소 유형을 구성합니다.

이 페이지에서는 사용 가능한 데이터 요소 유형을 설명합니다.

## 이벤트 병합 ID

이 데이터 요소는 사용 시 이벤트 병합 ID를 제공합니다. 이 데이터 요소에는 구성이 필요하지 않습니다. 제공된 데이터 요소는 방문자가 페이지를 떠나거나 &quot;이벤트 병합 ID 재설정&quot; 작업 유형이 사용될 때까지 동일하게 유지됩니다.

## ID 맵

이 ID 맵 데이터 요소를 사용하면 다른 데이터 요소 또는 지정한 다른 값에서 ID를 만들 수 있습니다. 만드는 모든 ID는 해당 네임스페이스에 다시 연결해야 합니다. 이 데이터 요소는 모든 기본 네임스페이스와 사용자가 만든 모든 네임스페이스를 표시하는 드롭다운을 제공합니다.

![](./assets/identity-map-data-element.png)

## XDM 개체 {#xdm-object}

XDM 형식을 사용하여 데이터를 Adobe Experience Platform Web SDK에 보냅니다. XDM 개체 데이터 요소를 사용하면 데이터 형식을 보다 손쉽게 지정할 수 있습니다. 이 데이터 요소를 처음 열면 올바른 Adobe Experience Platform 샌드박스 및 스키마를 선택합니다. 스키마를 선택하면 쉽게 작성할 수 있는 스키마 구조가 표시됩니다.

![](./assets/XDM-object.png)

`web.webPageDetails.URL`과 같은 스키마의 특정 필드를 열면 일부 항목이 자동으로 수집됩니다. 여러 항목이 자동으로 수집되지만 필요한 경우 덮어쓸 수 있습니다. 모든 값은 수동으로 채우거나 다른 데이터 요소를 사용할 수 있습니다.

>[!NOTE]
>
>수집하고자 하는 사항만 작성하십시오. 이 채워지지 않은 모든 것은 데이터가 솔루션으로 전송될 때 생략됩니다.
