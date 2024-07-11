---
title: clickCollection
description: 클릭 컬렉션 설정을 미세 조정합니다.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# `clickCollection`

다음 `clickCollection` 개체에는 자동으로 수집된 링크 데이터를 제어하는 데 도움이 되는 몇 가지 변수가 포함되어 있습니다. 데이터 수집에서 링크 유형을 포함하거나 제외하려면 다음 변수를 사용하십시오.

이를 위해서는 [`clickCollectionEnabled`](clickcollectionenabled.md) 활성화되었습니다.

웹 SDK 2.25.0 이상에서 지원됩니다.

에서 사용할 수 있는 변수는 다음과 같습니다. `clickCollection` 개체:

* **`clickCollection.internalLinkEnabled`**: 현재 도메인 내의 링크가 자동으로 추적되는지 여부를 결정하는 부울입니다. 예를 들어, `https://example.com/index.html` 끝 `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: 라이브러리가 를 기반으로 다운로드로 적합한 링크를 추적하는지 여부를 결정하는 부울입니다. [`downloadLinkQualifier`](downloadlinkqualifier.md) 속성.
* **`clickCollection.externalLinkEnabled`**: 외부 도메인에 대한 링크가 자동으로 추적되는지 여부를 결정하는 부울입니다. 예를 들어, `https://example.com` 끝 `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: 라이브러리가 다음 페이지에서 링크 추적 데이터를 보낼 때까지 기다리는지 여부를 결정하는 부울입니다. 다음 페이지가 로드되면 링크 추적 데이터를 페이지 로드 이벤트와 결합합니다. 이 옵션을 활성화하면 Adobe으로 전송하는 이벤트 수가 줄어듭니다. If `internalLinkEnabled` 이 비활성화되어 있으면 이 변수는 아무 작업도 하지 않습니다.
* **`clickCollection.sessionStorageEnabled`**: 링크 추적 데이터가 로컬 변수 대신 세션 저장소에 저장되어 있는지 여부를 결정하는 부울입니다. If `internalLinkEnabled` 또는 `eventGroupingEnabled` 이 비활성화되어 있으면 이 변수는 아무 작업도 하지 않습니다.

  Adobe은 을 사용할 때 이 변수를 활성화할 것을 강력히 권장합니다 `eventGroupingEnabled`. If `eventGroupingEnabled` 활성화 기간: `sessionStorageEnabled` 가 비활성화되어 있으므로 새 페이지를 클릭하면 링크 추적 데이터가 세션 저장소에 유지되지 않으므로 손실됩니다. 비활성화하는 것은 허용되지만 `sessionStorageEnabled` 단일 페이지 애플리케이션에서는 SPA이 아닌 페이지에 적합하지 않습니다.
* **`filterClickDetails`**: 수집한 링크 추적 데이터에 대한 전체 제어를 제공하는 콜백 함수입니다. 이 콜백 함수를 사용하여 링크 추적 데이터 전송을 변경, 난독화 또는 중단할 수 있습니다. 이 콜백은 링크 내의 개인 식별 정보와 같은 특정 정보를 생략하려는 경우 유용합니다.

## 웹 SDK 태그 확장을 사용하여 컬렉션 설정 클릭

다음 항목 선택 **[!UICONTROL 클릭 데이터 수집 활성화]** 다음과 같은 경우 확인란 [태그 확장 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 이 확인란을 활성화하면 클릭 컬렉션과 관련된 다음 옵션이 표시됩니다.

* [!UICONTROL 내부 링크]
   * [!UICONTROL 이벤트 그룹화 활성화]
   * [!UICONTROL 세션 저장소 활성화]
* [!UICONTROL 외부 링크]
* [!UICONTROL 다운로드 링크]
* [!UICONTROL 필터 클릭 속성]

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 확장]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 구성]** 다음에 있음 [!UICONTROL Adobe Experience Platform 웹 SDK] 카드.
1. 아래로 스크롤하여 [!UICONTROL 데이터 수집] 섹션을 선택한 다음 확인란을 선택합니다 **[!UICONTROL 클릭 데이터 수집 활성화]**.
1. 원하는 클릭 컬렉션 설정을 선택합니다.
1. 클릭 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 사항을 게시합니다.

다음 [!UICONTROL 필터 클릭 속성] callback은 원하는 코드를 삽입할 수 있는 사용자 지정 코드 편집기를 엽니다. 코드 편집기 내에서 다음 변수에 액세스할 수 있습니다.

* **`content.clickedElement`**: 클릭한 DOM 요소입니다.
* **`content.pageName`**: 클릭이 발생했을 때의 페이지 이름입니다.
* **`content.linkName`**: 클릭한 링크의 이름입니다.
* **`content.linkRegion`**: 클릭한 링크의 영역입니다.
* **`content.linkType`**: 링크 유형(종료, 다운로드 또는 기타)입니다.
* **`content.linkURL`**: 클릭한 링크의 대상 URL.
* **`return true`**: 현재 변수 값이 있는 콜백을 즉시 종료합니다.
* **`return false`**: 콜백을 즉시 종료하고 데이터 수집을 중단합니다.

의 외부에 정의된 모든 변수 `content` 을 사용할 수 있지만 Adobe으로 전송되는 페이로드에는 포함되지 않습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 컬렉션 설정 을 클릭합니다

내에서 원하는 변수를 설정합니다. `clickCollection` 개체를 실행할 때 [`configure`](overview.md) 명령입니다. 설정하지 않으면 이 객체의 기본 설정은 의 값에 따라 다릅니다. [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: 일치 `clickCollectionEnabled`
* `downloadLinkEnabled`: 일치 `clickCollectionEnabled`
* `externalLinkEnabled`: 일치 `clickCollectionEnabled`
* `eventGroupingEnabled`: 기본값은 입니다. `false`; 명시적으로 활성화되어야 함
* `sessionStorageEnabled`: 기본값은 입니다. `false`; 명시적으로 활성화되어야 함
* `filterClickDetails`: 함수를 포함하지 않습니다. 명시적으로 등록해야 합니다.

>[!TIP]
>Adobe은 활성화를 권장합니다. `eventGroupingEnabled`를 사용하면 계약상의 사용에 포함되는 이벤트 수를 줄일 수 있습니다.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
