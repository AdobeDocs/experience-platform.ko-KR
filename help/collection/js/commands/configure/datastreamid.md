---
title: datastreamId
description: 데이터를 보낼 데이터 스트림 ID를 결정합니다.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: b9fea4833c4fe869b27c1270aafd3f7ed62d59db
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# `datastreamId`

`datastreamId` 속성은 데이터를 보낼 Adobe Experience Platform의 [데이터스트림](/help/datastreams/overview.md)을(를) 결정하는 문자열입니다. 이 속성은 Adobe으로 데이터를 전송할 때 필요합니다. 웹 SDK 버전 2.20.0 이하에서는 대신 `edgeConfigId`을(를) 사용합니다.

데이터 스트림 ID를 찾으려면 다음을 수행하십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**(으)로 이동합니다.
1. 검색 필드를 사용하여 원하는 데이터 스트림을 찾은 다음 데이터 스트림 ID 옆에 있는 **[!UICONTROL Copy]** ![복사](../../assets/copy.png)를 선택합니다.

또는 원하는 데이터 스트림 이름을 선택할 수 있으며 데이터 스트림 ID가 복사할 오른쪽 열에 나타납니다.

## 코드 예

`datastreamID` 명령을 실행할 때 `configure` 문자열 속성을 설정하십시오. 이 속성은 모든 웹 SDK 구현에 필요합니다. 이 속성을 생략하면 웹 SDK이 데이터를 전송할 데이터 스트림을 알 수 없으므로 해당 데이터가 영구적으로 손실됩니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>한 페이지에서 웹 SDK의 여러 인스턴스를 구성하는 경우 각 인스턴스에 대해 다른 `datastreamId`을(를) 구성해야 합니다.

## 웹 SDK 태그 확장을 사용하여 데이터 스트림 ID 선택

태그를 사용하여 각 환경에 대해 원하는 데이터스트림을 설정하는 방법에 대한 자세한 내용은 웹 SDK 태그 확장 설명서의 [데이터스트림 구성 설정](/help/tags/extensions/client/web-sdk/configure/datastreams.md)을 참조하십시오. 프로덕션, 스테이징 및 개발 태그 환경을 위해 데이터를 다른 데이터스트림으로 보낼 수 있습니다.
