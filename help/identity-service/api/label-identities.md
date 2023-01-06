---
keywords: Experience Platform;홈;인기 항목;레이블 ID
solution: Experience Platform
title: 필드에 ID로 레이블 지정
description: PII(개인 식별 정보)가 포함된 필드는 ID 필드로 레이블이 지정될 수 있습니다. ID 필드에 제공된 값은 ID 서비스에 의한 ID로 해석됩니다. ID의 네임스페이스는 필드에 레이블을 지정하는 일부로 지정됩니다.
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# 필드에 ID로 레이블 지정

PII(개인 식별 정보)가 포함된 필드는 ID 필드로 레이블이 지정될 수 있습니다. ID 필드에 제공된 값은 [!DNL Identity Service]. ID의 네임스페이스는 필드에 레이블을 지정하는 일부로 지정됩니다.

필드에 ID로 레이블을 지정하려면 다음 기준을 충족해야 합니다.

- ID에는 문자열 유형 필드만 사용할 수 있습니다
- ID는 레코드 및 시계열 데이터에서만 인식됩니다
- PII 필드만 ID로 표시되어야 합니다. 보다 일반적인 데이터를 나타내는 필드를 선택하면 보다 정밀한 관계가 제거되고 ID 그래프에서 관련 ID에 액세스하는 오류가 발생할 수 있습니다

스키마 레지스트리 API를 사용하여 필드를 ID로 레이블을 지정하는 방법에 대한 지침은 를 참조하십시오. [엔드포인트 가이드](../../xdm/api/descriptors.md#create).

## 다음 단계

다음 자습서로 진행하여 [클러스터 ID 목록](./list-cluster-identites.md)
