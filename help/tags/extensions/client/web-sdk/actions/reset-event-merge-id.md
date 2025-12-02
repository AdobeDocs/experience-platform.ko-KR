---
title: 병합 ID 재설정
description: 동일한 페이지에서 호출된 이벤트를 구분할 수 있도록 해주는 더 이상 사용되지 않는 작업입니다.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 병합 ID 재설정

>[!IMPORTANT]
>
>이 작업은 더 이상 사용되지 않습니다. 대신 [내부 링크 클릭 수 수집](../configure/data-collection.md#collect-internal-link-clicks) 설정을 사용하십시오.

**[!UICONTROL Reset merge ID]** 작업 유형을 사용하면 같은 페이지에서 호출된 이벤트를 구분할 수 있습니다. 일반적으로 Adobe에 전송하려는 페이로드가 여러 개 있을 수 있는 내부 링크 시나리오에서 사용됩니다. 이 작업을 사용하면 이벤트의 병합 ID를 재설정하여 Edge Network에 도착한 후 동일한 이벤트의 일부로 간주되지 않도록 할 수 있습니다.

동일한 페이지에서 여러 이벤트가 분리되거나 병합되는 방식을 제어하려면 태그 확장을 구성할 때 [내부 링크 클릭 수 수집](../configure/data-collection.md#collect-internal-link-clicks) 옵션을 사용하십시오.
