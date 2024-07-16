---
title: edgeDomain
description: 데이터를 보낼 루트 도메인을 결정합니다.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

`edgeDomain` 속성을 사용하면 Web SDK에서 데이터를 보내는 도메인을 변경할 수 있습니다. 이 속성은 [자사 쿠키](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=ko-KR)를 사용하는 조직에서 자주 사용됩니다. 데이터가 조직의 자체 도메인으로 전송된 다음 CNAME 레코드가 해당 데이터를 Adobe으로 전달합니다.

조직에서 [자사 쿠키](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=ko-KR)를 설정할 때 이 속성에 대해 올바른 값을 결정합니다. 조직은 일반적으로 이러한 목적을 위해 전용 하위 도메인을 사용합니다. 예를 들어 도메인 `example.com`을(를) 사용하는 경우 `data.example.com`에 자사 쿠키를 설정할 수 있습니다.

## Web SDK 태그 확장을 사용하여 Edge 도메인 구성

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL Edge 도메인]** 텍스트 필드를 설정합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. 텍스트 필드 **[!UICONTROL Edge 도메인]**&#x200B;을(를) 찾은 다음 원하는 값을 입력하십시오.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 Edge 도메인 구성

`configure` 명령을 실행할 때 `edgeDomain` 문자열을 설정합니다. SDK를 구성할 때 이 속성을 생략하면 기본값은 `edge.adobedc.net`입니다. 웹 SDK에서 데이터를 전송하는 도메인을 재정의하려면 이 값을 설정하십시오.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
