---
title: 타사 쿠키 사용
description: 서드파티 쿠키를 사용하여 방문자를 식별할 수 있습니다.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: bc48f45bd6b9b7f7cc446ae84d712376292718d2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

>[!IMPORTANT]
>
>Google [발표](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) 는 2024년 하반기에 서드파티 쿠키에 대한 Chrome 지원을 중단할 예정입니다. 따라서 타사 쿠키는 더 이상 주요 브라우저에서 지원되지 않습니다.
>
>이 변경 사항이 구현되면 Adobe은 다음에 대한 지원을 중단합니다. `demdex` 현재 웹 SDK에서 지원되는 쿠키입니다.


다음 `thirdPartyCookiesEnabled` 속성은 웹 SDK가 서드파티 컨텍스트에서 쿠키를 설정하는지 여부를 결정하는 부울입니다. 이 옵션을 활성화하면 조직이 소유하는 하위 도메인 또는 도메인 간 방문자를 식별하려는 경우 유용합니다. 그러나 많은 최신 브라우저는 서드파티 쿠키의 설정 및 만료를 제한합니다.

이 옵션이 활성화되면 웹 SDK는 Adobe Audience Manager을 사용하여 방문자를 식별합니다. 이 옵션이 비활성화되면 Audience Manager 호출이 비활성화됩니다. 다음을 참조하십시오 [Demdex 도메인에 대한 호출 이해](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=ko-KR) 자세한 내용은 Audience Manager 사용 안내서를 참조하십시오.

## Web SDK 태그 확장을 사용하여 서드파티 쿠키 활성화

다음 항목 선택 **[!UICONTROL 서드파티 쿠키 사용]** 다음과 같은 경우 확인란 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 신원] 섹션을 선택한 다음 확인란을 선택합니다 **[!UICONTROL 서드파티 쿠키 사용]**.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 서드파티 쿠키 활성화

설정 `thirdPartyCookiesEnabled` 를 실행할 때 부울 `configure` 명령입니다. Web SDK를 구성할 때 이 속성을 생략하면 기본값이 로 설정됩니다. `true`. 이 값을 다음으로 설정 `false` 웹 SDK에서 방문자를 식별하는 데 Audience Manager을 사용하지 않도록 하려는 경우.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
