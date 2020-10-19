---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: IdentityMap mixin
topic: overview
description: 이 문서에서는 XDM 개별 프로필 클래스에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: fd5bd4134bd35d5d87c79bf1e75bc88c67511b2b
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# [!UICONTROL IdentityMap] mixin

[!UICONTROL IdentityMap] 은 [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md)의 표준 혼합입니다. 이 혼합은 네임스페이스별로 입력되는 사용자 ID 집합을 포함하는 단일 맵 필드를 제공합니다.

>[!WARNING]
>
>ID 데이터가 수집되면 시스템에서 이 `IdentityMap` 필드를 자동으로 업데이트합니다. 실시간 고객 프로필에 이 필드를 [적절히 활용하려면 데이터](../../../profile/home.md)작업에서 필드 내용을 수동으로 업데이트하지 마십시오.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

사용 사례에 대한 자세한 내용은 스키마 구성 [의 기본 사항에](../../schema/composition.md#identityMap) 있는 ID 맵에 대한 섹션을 참조하십시오.