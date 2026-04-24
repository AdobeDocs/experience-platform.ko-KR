---
title: edgeDomain
description: 데이터를 보낼 도메인을 결정합니다.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 2d3c31e399989652a0472bbe2174ca8d8554ba30
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 3%

---

# `edgeDomain`

`edgeDomain` 속성을 사용하면 웹 SDK에서 데이터를 보내는 도메인을 변경할 수 있습니다. 사용자 정의 도메인을 사용하면 광고 차단기의 영향을 줄이는 데 도움이 될 수 있습니다.

>[!NOTE]
>
>이 속성은 쿠키가 설정되는 위치를 변경하지 않습니다. 웹 SDK은 궁극적으로 데이터를 보내는 위치에 관계없이 항상 [자사 쿠키](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=ko-KR)를 설정합니다.

`edgeDomain`에 사용하는 값은 [Adobe 관리 인증서 프로그램](https://experienceleague.adobe.com/ko/docs/core-services/interface/data-collection/adobe-managed-cert)에 대한 기여도에 따라 다릅니다.

**조직에서 Adobe 관리 인증서 프로그램에 참여하는 경우** 값을 인증서를 설정할 때 선택한 자사 도메인으로 설정하십시오. 일반적으로 이 값은 조직이 소유한 하위 도메인입니다. 예, `data.example.com`. 조직의 CNAME 레코드는 해당 데이터를 Adobe에 전달합니다.

**조직이 인증서 프로그램에 참여하지 않는 경우** 값을 `data.adobedc.net`의 하위 도메인으로 설정하십시오. Adobe에서는 일관성을 위해 조직의 Adobe 할당 IMS 회사 ID를 사용하는 것이 좋습니다. 예, `example.data.adobedc.net`. 다음 단계를 사용하여 IMS 회사 ID를 확인하십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. Experience Cloud 인터페이스의 모든 곳에서 `[Cmd]` + `[I]`(macOS) 또는 `[Ctrl]` + `[I]`(Windows)을 누릅니다.
1. **[!UICONTROL User data debugger]**&#x200B;이(가) 나타납니다. **[!UICONTROL Assigned orgs]** 탭을 선택합니다. 
1. 원하는 IMS 조직을 확장합니다.
1. **[!UICONTROL Tenant]** 필드를 찾습니다. 이 값은 `data.adobedc.net`의 권장 하위 도메인입니다.

`edgeDomain` 명령을 실행할 때 `configure` 문자열을 설정합니다. SDK을 구성할 때 이 속성을 생략하면 기본값은 `edge.adobedc.net`입니다. 기본값을 사용할 수 있지만 Adobe에서는 조직 특정 값을 설정하는 것이 모범 사례로 간주됩니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## 웹 SDK 태그 확장을 사용한 Edge 도메인

이 속성에 해당하는 태그 확장은 확장을 구성할 때 **[!UICONTROL Edge domain]** SDK 인스턴스 구성 설정[&#x200B; 아래의 &#x200B;](/help/tags/extensions/client/web-sdk/configure/general.md) 필드입니다.
