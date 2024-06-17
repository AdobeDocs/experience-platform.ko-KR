---
title: appendIdentityToUrl
description: 앱, 웹 및 도메인 간에 개인화된 경험을 보다 정확하게 전달합니다.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 153c5bae42c027c25a38a8b63070249d1b1a8f01
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# `appendIdentityToUrl`

다음 `appendIdentityToUrl` 명령을 사용하면 URL에 사용자 식별자를 쿼리 문자열로 추가할 수 있습니다. 이 작업을 사용하면 도메인 간에 방문자의 ID를 전달할 수 있으므로 도메인 또는 채널을 모두 포함하는 데이터 세트에 대해 방문자 수가 중복되지 않도록 합니다. 웹 SDK 버전 2.11.0 이상에서 사용할 수 있습니다.

URL에 추가되고 생성된 쿼리 문자열은 `adobe_mc`. 웹 SDK에서 ECID를 찾을 수 없으면 `/acquire` 1을 생성할 끝점입니다.

>[!NOTE]
>
>동의를 제공하지 않은 경우 이 메서드의 URL은 변경되지 않은 상태로 반환됩니다. 이 명령은 즉시 실행되며 동의 업데이트를 기다리지 않습니다.

## 웹 SDK 확장을 사용하여 URL에 ID 추가 {#extension}

URL에 ID 추가는 Adobe Experience Platform 데이터 수집 태그 인터페이스의 규칙 내에서 작업으로 수행됩니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 작업]를 클릭하고 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL ID로 리디렉션]**.
1. 클릭 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

이 명령은 일반적으로 클릭을 수신하고 원하는 도메인을 확인하는 특정 규칙과 함께 사용됩니다.

+++규칙 이벤트 기준

가 있는 앵커 태그 지정 시 트리거됩니다. `href` 속성을 클릭합니다.

* **[!UICONTROL 확장]**: 코어
* **[!UICONTROL 이벤트 유형]**: 클릭
* **[!UICONTROL 사용자가 를 클릭할 때]**: 특정 요소
* **[!UICONTROL CSS 선택기와 일치하는 요소]**: `a[href]`

![규칙 이벤트](../assets/id-sharing-event-configuration.png)

+++

+++규칙 조건

원하는 도메인에서만 트리거됩니다.

* **[!UICONTROL 논리 유형]**: 일반
* **[!UICONTROL 확장]**: 코어
* **[!UICONTROL 조건 유형]**: 값 비교
* **[!UICONTROL 왼쪽 피연산자]**: `%this.hostname%`
* **[!UICONTROL 연산자]**: RegEx와 일치
* **[!UICONTROL 오른쪽 피연산자]**: 원하는 도메인과 일치하는 정규 표현식입니다. 예, `adobe.com$|behance.com$`

![규칙 조건](../assets/id-sharing-condition-configuration.png)

+++

+++규칙 작업

URL에 ID를 추가합니다.

* **[!UICONTROL 확장]**: Adobe Experience Platform 웹 SDK
* **[!UICONTROL 작업 유형]**: ID로 리디렉션

![규칙 작업](../assets/id-sharing-action-configuration.png)

+++

## 웹 SDK JavaScript 라이브러리를 사용하여 URL에 ID 추가

실행 `appendIdentityToUrl` url을 매개 변수로 사용하는 명령입니다. 이 메서드는 식별자가 추가된 URL을 쿼리 문자열로 반환합니다.

```js
alloy("appendIdentityToUrl",document.location);
```

페이지에서 받은 모든 클릭에 대한 이벤트 리스너를 추가하고 URL이 원하는 도메인과 일치하는지 확인할 수 있습니다. 이 경우 ID를 URL에 추가하고 사용자를 리디렉션합니다.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => {document.location = result.url;});
});
```

## 응답 개체

다음을 결정하시면 [응답 처리](command-responses.md) 이 명령을 사용하면 응답 개체에 다음이 포함됩니다. **`url`**: ID 정보가 포함된 새 URL이 쿼리 문자열 매개 변수로 추가됩니다.
