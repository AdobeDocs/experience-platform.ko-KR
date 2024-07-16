---
title: ECID 액세스
description: 데이터 준비 또는 태그에서 Experience Cloud ID에 액세스하는 방법 알아보기
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e01dfcf3cccea589083a23171f4b8d9ecad58233
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---


# ECID 액세스

[!DNL Experience Cloud Identity (ECID)]은(는) 사용자가 웹 사이트를 방문할 때 할당된 영구 식별자입니다. 경우에 따라 [!DNL ECID]에 액세스하여 서드파티로 보낼 수도 있습니다. 다른 사용 사례에서는 ID 맵에 보유할 뿐만 아니라 사용자 지정 XDM 필드에서 [!DNL ECID]을(를) 설정하는 것입니다.

[데이터 수집을 위한 데이터 준비](../../../../datastreams/data-prep.md)(권장) 또는 태그를 통해 ECID에 액세스할 수 있습니다.

## 데이터 준비를 통해 ECID에 액세스(기본 방법) {#accessing-ecid-data-prep}

ID 맵에 ECID를 보유하는 것 외에도 사용자 지정 XDM 필드에서 ECID를 설정하려면 `source`을(를) 다음 경로로 설정합니다.

```js
xdm.identityMap.ECID[0].id
```

그런 다음 대상을 필드가 `string` 유형인 XDM 경로로 설정합니다.

![](./assets/access-ecid-data-prep.png)

## 태그

클라이언트측의 [!DNL ECID]에 액세스해야 하는 경우 아래 설명된 대로 태그 접근 방식을 사용하십시오.

1. 속성이 [규칙 구성 요소 시퀀싱](../../../ui/managing-resources/rules.md#sequencing)을 사용하도록 구성되어 있는지 확인하십시오.
1. 새 규칙을 만듭니다. 이 규칙은 다른 중요한 작업 없이 [!DNL ECID]을(를) 캡처하는 데만 사용해야 합니다.
1. 규칙에 [!UICONTROL Library Loaded] 이벤트를 추가합니다.
1. 다음 코드를 사용하여 [!UICONTROL 사용자 지정 코드] 작업을 규칙에 추가합니다(SDK 인스턴스에 대해 구성한 이름이 `alloy`이고 같은 이름의 데이터 요소가 아직 없다고 가정).

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 규칙을 저장합니다.

그런 다음 다른 데이터 요소에 액세스하는 것처럼 `%ECID%` 또는 `_satellite.getVar("ECID")`을(를) 사용하여 후속 규칙의 [!DNL ECID]에 액세스할 수 있습니다.
