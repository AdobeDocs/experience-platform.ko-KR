---
title: ECID 액세스
description: Adobe Experience Platform 태그의 ECID(Experience Cloud ID)에 액세스하는 방법을 알아봅니다
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 5%

---


# ECID 액세스

다음 [!DNL Experience Cloud ID (ECID)] 는 웹 사이트 방문자를 식별하는 데 도움이 되는 영구 Experience Cloud 식별자입니다. 식별자를 타사 플랫폼으로 전송하는 것과 같은 특정 상황에서 [!DNL ECID].

에 액세스하려면 [!DNL ECID] 태그 내에서 아래 절차를 따르십시오.

1. 속성이 [규칙 구성 요소 순서](../../tags/ui/managing-resources/rules.md#sequencing) 활성화되었습니다.
2. 새 규칙을 만듭니다.
3. 추가 [!UICONTROL 라이브러리가 로드됨] 이벤트를 규칙에 추가합니다.
4. 추가 [!UICONTROL 사용자 지정 조건] 규칙에 대한 작업(SDK 인스턴스에 대해 구성한 이름이 다음과 같다고 가정함) `alloy`):

   ```javascript
   return alloy("getIdentity")
       .then(function(result) {
           _satellite.setVar("ECID", result.identity.ECID);
       });
   ```

5. 규칙을 저장합니다.

이제 [!DNL ECID] 다음 규칙에서, `%ECID%` 또는 `_satellite.getVar("ECID")`: 다른 데이터 요소에 액세스하는 방법과 유사합니다.
