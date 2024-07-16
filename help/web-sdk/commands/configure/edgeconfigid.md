---
title: edgeConfigId
description: 데이터를 보낼 데이터 스트림 ID를 결정합니다.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

`edgeConfigId` 속성은 데이터를 보낼 Adobe Experience Platform의 [데이터스트림](../../../datastreams/overview.md)을(를) 결정하는 문자열입니다. 이 속성은 Adobe으로 데이터를 전송할 때 필요합니다.

데이터 스트림 ID를 찾으려면 다음을 수행하십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 데이터스트림]**&#x200B;으로 이동합니다.
1. 검색 필드를 사용하여 원하는 데이터 스트림을 찾은 다음 데이터 스트림 ID 옆에 있는 **[!UICONTROL 복사]** ![복사](../../assets/copy.png)를 선택합니다.

원하는 데이터 스트림 이름을 선택할 수도 있고 데이터 스트림 ID가 복사할 수 있도록 오른쪽 열에 나타납니다.

## 웹 SDK 태그 확장을 사용하여 데이터 스트림 ID 선택

사용 가능한 데이터 스트림 목록에서 선택하거나 [태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 데이터 스트림 ID를 직접 입력합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL 데이터스트림] 섹션을 찾은 다음 원하는 데이터스트림 결정 방법을 선택합니다.
   * 목록에서 선택하는 경우 각 드롭다운 목록에서 샌드박스 및 데이터스트림을 선택합니다.
   * 값을 입력하는 경우 원하는 데이터 스트림 ID를 입력합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

프로덕션, 스테이징 및 개발 태그 환경을 위해 데이터를 다른 데이터스트림으로 보낼 수 있습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 데이터 스트림 ID 선택

`configure` 명령을 실행할 때 `edgeConfigId` 문자열 속성을 설정하십시오. 이 속성은 모든 웹 SDK 구현에 필요합니다. 이 속성을 생략하면 Web SDK는 데이터를 전송할 데이터 스트림을 알 수 없으므로 해당 데이터가 영구적으로 손실됩니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

한 페이지에서 웹 SDK의 여러 인스턴스를 구성하는 경우 각 인스턴스에 대해 다른 `edgeConfigId`을(를) 구성해야 합니다.
