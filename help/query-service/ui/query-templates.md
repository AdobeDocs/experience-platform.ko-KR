---
title: 쿼리 템플릿
description: 쿼리 템플릿은 다른 사용자가 재사용하여 시간과 노력을 절약할 수 있는 재사용 가능한 저장된 SQL 쿼리입니다. 쿼리 편집기 또는 쿼리 서비스 API를 사용하여 만들 수 있으며, 모든 Experience Platform 데이터 세트에서 사용할 수 있습니다.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# 쿼리 템플릿

Adobe Experience Platform Query Service를 사용하면 SQL 코드를 쿼리 템플릿 형식으로 저장하고 재사용할 수 있습니다. 템플릿은 일반적으로 수행되는 작업이 반복되지 않도록 하여 노력을 절약합니다. 조직 내에서 템플릿을 공유하고 기본 SQL에 액세스하거나 이해할 필요 없이 쿼리 값을 쉽게 변경할 수 있습니다.

이 문서에서는 쿼리 서비스에서 쿼리 템플릿을 만드는 데 필요한 정보를 제공합니다.

## 전제 조건

쿼리 편집기에 액세스하고 Experience Platform UI 내에서 쿼리 대시보드를 보려면 [!UICONTROL 쿼리 관리] 권한을 활성화해야 합니다. 권한은 Adobe [Admin Console](https://adminconsole.adobe.com/)을 통해 사용할 수 있습니다. 이 권한을 활성화하기 위한 관리자 권한이 없는 경우 조직의 관리자에게 문의하십시오. Admin Console을 통해 권한을 추가하는 방법에 대한 [전체 지침](../../access-control/home.md)은 액세스 제어 설명서를 참조하십시오.

## 쿼리 템플릿 만들기

쿼리 서비스 API `query-templates` 끝점에 대한 POST 요청을 수행하거나 쿼리 편집기를 통해 쿼리를 작성, 이름 지정 및 저장하는 두 가지 방법을 통해 쿼리 템플릿을 만들 수 있습니다.

### 쿼리 편집기를 사용하여 쿼리를 템플릿으로 작성 및 저장

쿼리 편집기를 사용하여 [작성](./user-guide.md#query-authoring) 및 [쿼리 저장](./user-guide.md#saving-queries)하는 방법에 대한 지침은 설명서를 참조하세요. 쿼리의 이름을 지정하고 저장하면 [!UICONTROL 템플릿] 탭에서 쿼리 템플릿으로 다시 사용할 수 있습니다.

>[!TIP]
>
>쿼리 편집기에 쿼리를 저장하면 성공 작업을 알리는 확인 메시지가 표시됩니다. 이 팝업 메시지에는 쿼리 예약 작업 공간으로 편리하게 이동할 수 있는 방법을 제공하는 링크가 포함되어 있습니다. 사용자 지정 케이던스에서 쿼리를 실행하는 방법은 [쿼리 예약 설명서](./query-schedules.md)를 참조하세요.

## 쿼리 템플릿 찾아보기 {#browse}

Experience Platform UI의 쿼리 작업 영역에서 **[!UICONTROL 템플릿]**&#x200B;을(를) 선택하여 사용 가능한 저장된 쿼리 목록을 표시합니다.

![템플릿 탭이 강조 표시된 쿼리 작업 영역입니다.](../images/ui/query-templates/query-templates.png)

관련 템플릿 정보를 찾으려면 사용 가능한 목록에서 쿼리 템플릿을 선택하여 세부 정보 패널을 엽니다.

![쿼리 ID가 강조 표시된 쿼리 작업 영역의 세부 정보 패널입니다.](../images/ui/query-templates/details-panel.png)

세부 정보 패널에서 다음 작업을 실행할 수 있습니다.

* 기존 테이블에서 데이터를 선택하여 새 테이블을 만들려면 **[!UICONTROL CTAS로 실행]**&#x200B;을 선택하십시오. 이 옵션은 SELECT 쿼리가 있는 경우에만 사용할 수 있습니다.
* 쿼리 템플릿에 대한 일정 편집을 시작하려면 **[!UICONTROL 일정 추가]**&#x200B;를 선택하십시오.
* **[!UICONTROL 일정 보기]**&#x200B;를 선택하여 쿼리 편집기의 [!UICONTROL 일정] 탭으로 이동합니다. 이 보기에는 쿼리와 관련된 모든 일정 정보가 포함됩니다.
* 템플릿을 삭제하려면 **[!UICONTROL 쿼리 삭제]**&#x200B;를 선택하십시오.
* 템플릿 이름을 선택하여 편집할 SQL이 미리 채워진 쿼리 편집기로 이동합니다.

### 쿼리 서비스 API를 사용하여 템플릿 만들기

쿼리 서비스 API를 사용하여 [쿼리 템플릿을 만드는 방법](../api/query-templates.md#create-a-query-template)에 대한 지침은 설명서를 참조하세요. 새로 만든 쿼리 템플릿에 대한 세부 정보는 응답 본문에 포함됩니다.

>[!NOTE]
>
>API를 사용하여 만든 템플릿은 Experience Platform UI 쿼리 서비스 템플릿 탭에도 표시됩니다.

## 다음 단계

이제 이 문서를 읽고 Query Service에서 쿼리 템플릿을 만드는 방법을 더 잘 이해할 수 있습니다. 쿼리 서비스 기능에 대한 자세한 내용은 [UI 개요](./overview.md) 또는 [쿼리 서비스 API 안내서](../api/getting-started.md)를 참조하십시오.

API를 사용하여 쿼리를 예약하는 방법을 알아보려면 [예약된 쿼리 끝점 안내서](../api/scheduled-queries.md)를 참조하거나 UI에 대한 [쿼리 편집기 안내서](./user-guide.md#scheduled-queries)를 참조하십시오.
