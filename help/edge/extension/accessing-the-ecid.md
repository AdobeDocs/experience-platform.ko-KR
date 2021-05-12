---
title: 'ECID 액세스 '
description: Adobe Experience Platform Launch의 ECID를 활용하는 Adobe Experience Platform Web SDK Extension
source-git-commit: 3002036d7366e2f7310aa62e53c7c391d9ff7a07
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---


# ECID 액세스

[!DNL Experience Cloud Identity (ECID)]은 웹 사이트 방문자의 영구 식별자입니다. 특정 상황에서 ECID에 액세스하면(예: 제3자에게 보내기) 됩니다.

Adobe Experience Platform Launch 내의 ECID에 액세스하려면 Adobe에서 다음을 권장합니다.

1. 속성이 [규칙 구성 요소 시퀀싱](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing)이(가) 활성화된 상태로 구성되어 있는지 확인합니다.
1. 새 규칙을 만듭니다.
1. 규칙에 [!UICONTROL Library Loaded] 이벤트를 추가합니다.
1. 다음 코드로 [!UICONTROL Custom Condition] 작업을 규칙에 추가합니다(SDK 인스턴스에 대해 구성한 이름이 `alloy`이라고 가정함).

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 규칙을 저장합니다.

그런 다음 다른 데이터 요소와 마찬가지로 `%ECID%` 또는 `_satellite.getVar("ECID")`을 사용하여 후속 규칙에서 ECID에 액세스할 수 있어야 합니다.
