---
title: ECID 액세스
description: 태그에서 ECID를 활용하는 Adobe Experience Platform 웹 SDK 확장
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 5%

---

# ECID 액세스

다음 [!DNL Experience Cloud Identity (ECID)] 는 웹 사이트 방문자의 영구 식별자입니다. 특정 상황에서는 ECID에 액세스(예: 서드파티에 보내기 위해)하는 것이 좋을 수 있습니다.

태그 내의 ECID에 액세스하려면 Adobe은 다음을 권장합니다.

1. 속성이 다음으로 구성되었는지 확인합니다. [규칙 구성 요소 시퀀싱](../../tags/ui/managing-resources/rules.md#sequencing) 활성화되었습니다.
1. 새 규칙을 만듭니다.
1. 추가 [!UICONTROL 라이브러리가 로드됨] 이벤트를 규칙에 추가합니다.
1. 추가 [!UICONTROL 사용자 지정 조건] 다음 코드를 사용하여 규칙에 대한 작업(SDK 인스턴스에 대해 구성한 이름이 이라고 가정) `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 규칙을 저장합니다.

그런 다음 을 사용하여 후속 규칙의 ECID에 액세스할 수 있습니다. `%ECID%` 또는 `_satellite.getVar("ECID")` 다른 데이터 요소를 사용하는 것과 같습니다.
