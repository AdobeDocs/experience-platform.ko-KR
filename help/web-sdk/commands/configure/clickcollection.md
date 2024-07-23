---
title: clickCollection
description: 클릭 컬렉션 설정을 미세 조정합니다.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# `clickCollection`

`clickCollection` 개체에는 자동으로 수집된 링크 데이터를 제어하는 데 도움이 되는 여러 변수가 포함되어 있습니다. 데이터 수집에서 링크 유형을 포함하거나 제외하려면 다음 변수를 사용하십시오.

[`clickCollectionEnabled`](clickcollectionenabled.md)을(를) 사용하도록 설정해야 합니다.

웹 SDK 2.25.0 이상에서 지원됩니다.

`clickCollection` 개체에서 다음 변수를 사용할 수 있습니다.

* **`clickCollection.internalLinkEnabled`**: 현재 도메인 내의 링크가 자동으로 추적되는지 여부를 결정하는 부울입니다. 예: `https://example.com/index.html`에서 `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: 라이브러리가 [`downloadLinkQualifier`](downloadlinkqualifier.md) 속성을 기반으로 다운로드로 적합한 링크를 추적하는지 여부를 결정하는 부울입니다.
* **`clickCollection.externalLinkEnabled`**: 외부 도메인에 대한 링크가 자동으로 추적되는지 여부를 결정하는 부울입니다. 예: `https://example.com`에서 `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: 라이브러리가 다음 페이지에서 링크 추적 데이터를 보낼 때까지 대기하는지 여부를 결정하는 부울입니다. 다음 페이지가 로드되면 링크 추적 데이터를 페이지 로드 이벤트와 결합합니다. 이 옵션을 활성화하면 Adobe으로 전송하는 이벤트 수가 줄어듭니다. `internalLinkEnabled`이(가) 비활성화되어 있으면 이 변수는 아무 작업도 하지 않습니다.
* **`clickCollection.sessionStorageEnabled`**: 링크 추적 데이터가 로컬 변수 대신 세션 저장소에 저장되어 있는지 여부를 결정하는 부울입니다. `internalLinkEnabled` 또는 `eventGroupingEnabled`이(가) 비활성화된 경우 이 변수는 아무 작업도 하지 않습니다.

  Adobe 단일 페이지 응용 프로그램 외부에서 `eventGroupingEnabled`을(를) 사용할 때는 이 변수를 사용하도록 설정하는 것이 좋습니다. `sessionStorageEnabled`이(가) 비활성화되어 있는 동안 `eventGroupingEnabled`이(가) 활성화된 경우 새 페이지를 클릭하면 링크 추적 데이터가 세션 저장소에 유지되지 않으므로 손실됩니다. 단일 페이지 애플리케이션은 일반적으로 새 페이지로 이동하지 않으므로 SPA 페이지에는 세션 저장소가 필요하지 않습니다.
* **`filterClickDetails`**: 수집한 링크 추적 데이터에 대한 전체 제어를 제공하는 콜백 함수입니다. 이 콜백 함수를 사용하여 링크 추적 데이터 전송을 변경, 난독화 또는 중단할 수 있습니다. 이 콜백은 링크 내의 개인 식별 정보와 같은 특정 정보를 생략하려는 경우 유용합니다.

## 웹 SDK 태그 확장을 사용하여 컬렉션 설정 클릭

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 다음 옵션 중 하나를 선택하십시오.

* [!UICONTROL 내부 링크 수집]
   * [!UICONTROL 이벤트 그룹화 옵션]:
      * [!UICONTROL 이벤트 그룹화 없음]
      * [!UICONTROL 세션 저장소를 사용하여 이벤트 그룹화]
      * [!UICONTROL 로컬 개체를 사용한 이벤트 그룹화]
* [!UICONTROL 외부 링크 수집]
* [!UICONTROL 다운로드 링크 수집]
* [!UICONTROL 클릭 속성 필터링]

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL 데이터 수집] 섹션까지 아래로 스크롤한 다음 원하는 클릭 수집 설정을 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

[!UICONTROL 필터 클릭 속성] 콜백에서는 원하는 코드를 삽입할 수 있는 사용자 지정 코드 편집기가 열립니다. 코드 편집기 내에서 다음 변수에 액세스할 수 있습니다.

* **`content.clickedElement`**: 클릭한 DOM 요소입니다.
* **`content.pageName`**: 클릭이 발생했을 때의 페이지 이름입니다.
* **`content.linkName`**: 클릭한 링크의 이름입니다.
* **`content.linkRegion`**: 클릭한 링크의 영역입니다.
* **`content.linkType`**: 링크 유형(종료, 다운로드 또는 기타)입니다.
* **`content.linkURL`**: 클릭한 링크의 대상 URL.
* **`return true`**: 현재 변수 값이 있는 콜백을 즉시 종료합니다.
* **`return false`**: 콜백을 즉시 종료하고 데이터 수집을 중단합니다.

`content`의 외부에서 정의된 모든 변수를 사용할 수 있지만, Adobe으로 전송되는 페이로드에는 포함되지 않습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 컬렉션 설정 을 클릭합니다

[`configure`](overview.md) 명령을 실행할 때 `clickCollection` 개체 내에서 원하는 변수를 설정하십시오. 설정하지 않으면 이 개체의 기본 설정은 [`clickCollectionEnabled`](clickcollectionenabled.md) 값에 따라 다릅니다.

* `internalLinkEnabled`: `clickCollectionEnabled`과(와) 일치
* `downloadLinkEnabled`: `clickCollectionEnabled`과(와) 일치
* `externalLinkEnabled`: `clickCollectionEnabled`과(와) 일치
* `eventGroupingEnabled`: 기본값은 `false`입니다. 명시적으로 사용하도록 설정해야 합니다.
* `sessionStorageEnabled`: 기본값은 `false`입니다. 명시적으로 사용하도록 설정해야 합니다.
* `filterClickDetails`: 함수를 포함하지 않습니다. 명시적으로 등록해야 합니다.

>[!TIP]
>Adobe은 계약상 사용에 포함되는 이벤트 수를 줄이기 때문에 `internalLinkEnabled`이(가) 활성화된 경우 `eventGroupingEnabled`을(를) 활성화할 것을 권장합니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```
