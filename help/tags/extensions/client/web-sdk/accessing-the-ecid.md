---
title: ECID 액세스
description: 데이터 준비 또는 태그에서 Experience Cloud ID에 액세스하는 방법 알아보기
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# ECID 액세스

다음 [!DNL Experience Cloud Identity (ECID)] 는 사용자가 웹 사이트를 방문할 때 할당되는 영구 식별자입니다. 특정 상황에서는 [!DNL ECID] (예: 서드파티로 보내기). 또 다른 사용 사례는 [!DNL ECID] 사용자 지정 XDM 필드의 경우, ID 맵에 보유할 수도 있습니다.

다음 중 하나를 통해 ECID에 액세스할 수 있습니다. [데이터 수집을 위한 데이터 준비](../../../../datastreams/data-prep.md) (권장) 또는 태그를 통해.

## 데이터 준비를 통해 ECID에 액세스(기본 방법) {#accessing-ecid-data-prep}

ID 맵에 보유할 뿐만 아니라 사용자 지정 XDM 필드에서 ECID를 설정하려면 다음을 설정할 수 있습니다. `source` 다음 경로로 이동합니다.

```js
xdm.identityMap.ECID[0].id
```

그런 다음 타겟을 필드가 유형인 XDM 경로로 설정합니다 `string`.

![](./assets/access-ecid-data-prep.png)

## 태그

에 액세스해야 하는 경우 [!DNL ECID] 클라이언트측에서는 아래 설명된 대로 태그 접근 방식을 사용합니다.

1. 속성이 다음으로 구성되었는지 확인합니다. [규칙 구성 요소 시퀀싱](../../../ui/managing-resources/rules.md#sequencing) 활성화되었습니다.
1. 새 규칙을 만듭니다.
1. 추가 [!UICONTROL 라이브러리가 로드됨] 이벤트를 규칙에 추가합니다.
1. 추가 [!UICONTROL 사용자 지정 조건] 다음 코드를 사용하여 규칙에 대한 작업(SDK 인스턴스에 대해 구성한 이름이 이라고 가정) `alloy`):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 규칙을 저장합니다.

그러면 다음에 액세스할 수 있습니다. [!DNL ECID] 를 사용하는 후속 규칙에서 `%ECID%` 또는 `_satellite.getVar("ECID")`: 다른 데이터 요소에 액세스할 수 있습니다.
