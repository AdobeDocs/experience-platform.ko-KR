---
title: ECID 액세스
description: 데이터 준비 또는 태그에서 Experience Cloud ID에 액세스하는 방법을 알아봅니다
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: dee04f2cdeb9057ac10e27a17f9db3f065712618
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# ECID 액세스

다음 [!DNL Experience Cloud Identity (ECID)] 는 사용자가 웹 사이트를 방문할 때 사용자에게 할당된 영구 식별자입니다. 상황에 따라 [!DNL ECID] (예를 들어 타사에 보내려면) 다른 사용 사례에서는 [!DNL ECID] 사용자 지정 XDM 필드에 추가하여 id 맵에 나타낼 수도 있습니다.

를 통해 ECID에 액세스할 수 있습니다 [데이터 수집을 위한 데이터 준비](../datastreams/data-prep.md) (권장) 또는 태그를 통해 태깅합니다.

## 데이터 준비를 통해 ECID에 액세스(기본 방법) {#accessing-ecid-data-prep}

사용자 지정 XDM 필드에서 ECID를 설정하려는 경우 ID 맵에 ECID를 포함하는 것 외에도 다음을 설정하여 수행할 수 있습니다 `source` 다음 경로로 이동하십시오.

```js
xdm.identityMap.ECID[0].id
```

그런 다음 대상을 필드가 유형의 XDM 경로로 설정합니다 `string`.

![](./assets/access-ecid-data-prep.png)

## 태그

에 액세스해야 하는 경우 [!DNL ECID] 클라이언트측에서 아래에 설명된 대로 태그 접근 방식을 사용하십시오.

1. 속성이 [규칙 구성 요소 순서](../../tags/ui/managing-resources/rules.md#sequencing) 활성화되었습니다.
1. 새 규칙을 만듭니다.
1. 추가 [!UICONTROL 라이브러리가 로드됨] 이벤트를 규칙에 추가합니다.
1. 추가 [!UICONTROL 사용자 지정 조건] 다음 코드를 사용하여 규칙에 대한 작업(SDK 인스턴스에 대해 구성한 이름이 다음과 같다고 가정) `alloy`):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 규칙을 저장합니다.

그런 다음 [!DNL ECID] 다음 규칙을 사용하여 `%ECID%` 또는 `_satellite.getVar("ECID")`다른 데이터 요소에 액세스하는 것처럼
