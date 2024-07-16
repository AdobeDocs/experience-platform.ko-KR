---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;ABAC
title: 속성 기반 액세스 제어 관리 레이블
description: 이 문서에서는 Adobe Experience Cloud의 권한 인터페이스를 통해 레이블을 관리하는 방법에 대한 정보를 제공합니다
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 5810a7778d86db2720a0372ace33278348d1ffdf
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 10%

---

# 레이블 관리

>[!NOTE]
>
>지정된 레이블이 포함된 필드가 있는 계산된 속성을 만들거나 보려면 해당 레이블에 대한 액세스 권한이 있어야 합니다.

레이블을 사용하면 해당 데이터에 적용되는 사용 및 액세스 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터를 제어하는 방법을 유연하게 선택할 수 있습니다. 우수 사례는 데이터가 Platform에 수집되는 즉시 또는 데이터를 Platform에서 사용할 수 있게 되는 즉시 데이터에 레이블을 지정하는 것을 권장합니다.

## 새 레이블 만들기 {#create-new-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="레이블 사용"
>abstract="사용자 정의 레이블을 사용하여 데이터에 데이터 거버넌스 및 액세스 제어 구성을 적용할 수 있습니다."

>[!NOTE]
>
>전체 조직에 대해 하나의 레이블 목록이 있습니다. 사용자 지정 레이블을 만들려면 프로덕션 샌드박스에서 **[!UICONTROL 사용 레이블 관리]** 권한이 필요합니다. 레이블 삭제는 현재 지원되지 않습니다.

새 레이블을 만들려면 사이드바에서 **[!UICONTROL 레이블]** 탭을 선택하고 **[!UICONTROL 레이블 만들기]**&#x200B;를 선택하십시오.

![flac-new-label](../../images/flac-ui/create-label.png)

**[!UICONTROL 새 레이블 만들기]** 대화 상자가 나타나고 이름, 알기 쉬운 이름(선택 사항) 및 설명을 입력하라는 메시지가 표시됩니다.

![new-label-info](../../images/flac-ui/new-label-info.png)

완료되면 **[!UICONTROL 확인]**&#x200B;을 선택합니다.
