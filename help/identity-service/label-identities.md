---
keywords: Experience Platform;홈;인기 항목;레이블 ID
title: UI에서 필드에 ID 레이블 지정
description: PII(개인 식별 정보)가 포함된 필드는 ID 필드로 레이블 지정할 수 있습니다. ID 필드에 제공된 값은 ID 서비스에서 ID로 해석됩니다. ID의 네임스페이스는 필드에 레이블을 지정하는 일부로 지정됩니다.
hide: true
hidefromtoc: true
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 0d111241658b4014d1ca2e6013d21a4782d81be9
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# UI에서 필드에 ID 레이블 지정

PII(개인 식별 정보)가 포함된 필드는 ID 필드로 레이블 지정할 수 있습니다. ID 필드에 입력한 값은 [!DNL Identity Service]에서 ID로 해석됩니다. ID의 네임스페이스는 필드에 레이블을 지정하는 일부로 지정됩니다.

필드가 ID로 레이블이 지정되려면 다음 기준을 충족해야 합니다.

* ID에는 문자열 유형 필드만 사용할 수 있습니다.
* ID는 레코드 및 시계열 데이터에서만 인식됩니다.
* PII 필드만 ID로 표시되어야 합니다. 더 일반적인 데이터를 나타내는 필드를 선택하면 관계의 정밀도가 떨어지고 ID 그래프에서 관련 ID에 액세스하는 동안 오류가 발생할 수 있습니다

UI에서 ID 필드에 레이블을 지정하는 방법에 대한 지침은 [UI에서 ID 필드 정의](../xdm/ui/fields/identity.md)에 대한 안내서를 참조하십시오.

## 다음 단계

[!DNL Identity Service]에 대한 자세한 내용은 [[!DNL Identity Service] 개요](./home.md)를 참조하십시오.
