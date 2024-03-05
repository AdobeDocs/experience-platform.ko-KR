---
title: 데이터
description: XDM이 아닌 데이터를 Adobe으로 보내는 방법을 알아봅니다.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# 데이터

다음 `data` 속성을 사용하면 XDM 스키마와 일치하지 않는 Adobe에 데이터를 보낼 수 있습니다. 이 변수는 XDM이 아닌 시나리오(예: 업데이트)에서 유용합니다. [Adobe Target 프로필](/help/web-sdk/personalization/adobe-target/target-overview.md). 데이터가 Adobe에 도달하면 데이터스트림 매핑 도구를 사용하여 의 각 필드에 XDM 필드를 할당할 수 있습니다. `data` 속성.

>[!IMPORTANT]
>
>이 속성 내의 데이터에는 다음 작업 중 하나 이상이 있어야 합니다.
>
>* 데이터스트림의 특정 속성에서 데이터를 검색하도록 데이터스트림의 서비스를 구성해야 합니다. `data` 오브젝트
>* 각 속성은 XDM 필드에 매핑되어야 합니다.
>
>지정된 필드가 XDM 필드에 매핑되지 않거나 구성된 서비스에서 사용되지 않으면 해당 데이터가 영구적으로 손실됩니다.

## Web SDK 태그 확장을 사용하여 데이터 속성 사용

에 데이터 요소를 제공합니다. **[!UICONTROL 데이터]** 태그 규칙 작업 내의 필드

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 작업]를 클릭하고 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL 이벤트 보내기]**.
1. 에서 원하는 개체가 포함된 데이터 요소를 제공합니다. **[!UICONTROL 데이터]** 필드.
1. 클릭 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 데이터 속성 사용

설정 `data` 의 매개 변수 내에서 JSON 개체의 일부로 속성이 `sendEvent` 명령입니다. 데이터스트림에 매핑할 데이터의 경우 원하는 대로 이 속성을 구성할 수 있습니다. 특정 서비스에서 사용하는 데이터의 경우 개체 계층 구조가 서비스가 기대하는 것과 일치하는지 확인하십시오. 다음 두 가지를 모두 포함할 수 있습니다. `data` 오브젝트 및 [`xdm`](xdm.md) 같은 오브젝트 `sendEvent` 명령입니다.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```
