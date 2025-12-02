---
title: onBeforeLinkClickSend
description: 링크 추적 데이터가 전송되기 바로 전에 실행되는 콜백입니다.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>이 콜백은 더 이상 사용되지 않습니다. 대신 [`clickCollection.filterClickDetails`](clickcollection.md)을(를) 사용합니다.

`onBeforeLinkClickSend` 콜백을 사용하면 해당 데이터가 Adobe으로 전송되기 바로 전에 전송한 링크 추적 데이터를 변경할 수 있는 JavaScript 함수를 등록할 수 있습니다. 요소를 추가, 편집 또는 제거하는 기능을 포함하여 `xdm` 또는 `data` 개체를 조작할 수 있습니다. 감지된 클라이언트측 보트 트래픽과 같이 조건부로 데이터 전송을 모두 취소할 수도 있습니다.

이 콜백은 [`clickCollectionEnabled`](clickcollectionenabled.md)이(가) 활성화되어 있고 `filterClickDetails`에 등록된 함수가 없는 경우에만 실행됩니다.

[`onBeforeEventSend`](onbeforeeventsend.md)과(와) `onBeforeLinkClickSend`이(가) 모두 등록된 함수를 포함하는 경우 `onBeforeLinkClickSend`이(가) 먼저 실행됩니다.

>[!WARNING]
>
>이 콜백에서는 사용자 지정 코드를 사용할 수 있습니다. 콜백에 포함하는 코드에서 catch되지 않은 예외가 발생하면 이벤트 처리가 중지됩니다. 데이터가 Adobe으로 전송되지 않습니다.

## `onBeforeLinkClickSend` 및 `filterClickDetails`

[`clickCollection.filterClickDetails`](clickcollection.md) 콜백은 `onBeforeLinkClickSend`을(를) 대체하도록 디자인되었습니다. Adobe에서는 콜백 함수를 두 함수 모두에 동시에 할당하지 않는 것이 좋습니다. `filterClickDetails`과(와) `onBeforeLinkClickSend` 모두에 콜백 함수를 할당하면 라이브러리에서 다음 논리를 사용합니다.

* `filterClickDetails`만 실행되고 `onBeforeLinkClickSend`은(는) 실행되지 않습니다.
* `clickCollection.eventGroupingEnabled` 이벤트 그룹화가 작동하지 않습니다.
