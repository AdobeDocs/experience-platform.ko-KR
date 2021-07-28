---
title: 'ECID 액세스 '
description: 태그에서 ECID를 활용하는 Adobe Experience Platform Web SDK 확장
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 5%

---


# ECID 액세스

[!DNL Experience Cloud Identity (ECID)]은 웹 사이트 방문자가 사용할 수 있는 영구 식별자입니다. 특정 상황에서 ECID에 액세스하거나 예를 들어 타사에 보내는 것이 좋을 수 있습니다.

태그 내의 ECID에 액세스하려면 Adobe에서 다음을 권장합니다.

1. 속성이 [규칙 구성 요소 시퀀싱](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing)이 활성화된 상태에서 구성되었는지 확인합니다.
1. 새 규칙을 만듭니다.
1. [!UICONTROL Library Loaded] 이벤트를 규칙에 추가합니다.
1. 다음 코드를 사용하여 [!UICONTROL 사용자 지정 조건] 작업을 규칙에 추가합니다(SDK 인스턴스에 대해 구성한 이름이 `alloy`라고 가정).

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 규칙을 저장합니다.

그런 다음 다른 데이터 요소와 마찬가지로 `%ECID%` 또는 `_satellite.getVar("ECID")`을 사용하여 후속 규칙에서 ECID에 액세스할 수 있어야 합니다.
