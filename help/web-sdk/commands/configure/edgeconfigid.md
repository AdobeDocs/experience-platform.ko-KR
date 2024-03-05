---
title: edgeConfigId
description: 데이터를 보낼 데이터 스트림 ID를 결정합니다.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

다음 `edgeConfigId` 속성은 다음 항목을 결정하는 문자열입니다. [데이터스트림](../../../datastreams/overview.md) Adobe Experience Platform에서 데이터를 (으)로 전송하려고 합니다. 이 속성은 Adobe으로 데이터를 전송할 때 필요합니다.

데이터 스트림 ID를 찾으려면 다음을 수행하십시오.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 데이터스트림]**.
1. 검색 필드를 사용하여 원하는 데이터 스트림을 찾은 다음 를 선택합니다 **[!UICONTROL 복사]** ![복사](../../assets/copy.png) 데이터 스트림 ID 옆에 있습니다.

원하는 데이터 스트림 이름을 선택할 수도 있고 데이터 스트림 ID가 복사할 수 있도록 오른쪽 열에 나타납니다.

## 웹 SDK 태그 확장을 사용하여 데이터 스트림 ID 선택

사용 가능한 데이터스트림 목록에서 선택하거나, 다음과 같은 경우 데이터스트림 ID를 직접 입력합니다 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 를 찾습니다. [!UICONTROL 데이터스트림] 그런 다음 원하는 데이터 스트림 결정 방법을 선택합니다.
   * 목록에서 선택하는 경우 각 드롭다운 목록에서 샌드박스 및 데이터스트림을 선택합니다.
   * 값을 입력하는 경우 원하는 데이터 스트림 ID를 입력합니다.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

프로덕션, 스테이징 및 개발 태그 환경을 위해 데이터를 다른 데이터스트림으로 보낼 수 있습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 데이터 스트림 ID 선택

설정 `edgeConfigId` 문자열 속성을 사용하여 `configure` 명령입니다. 이 속성은 모든 웹 SDK 구현에 필요합니다. 이 속성을 생략하면 Web SDK는 데이터를 전송할 데이터 스트림을 알 수 없으므로 해당 데이터가 영구적으로 손실됩니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

단일 페이지에서 웹 SDK의 여러 인스턴스를 구성하는 경우 다른 인스턴스를 구성해야 합니다 `edgeConfigId` 각 인스턴스에 대해
