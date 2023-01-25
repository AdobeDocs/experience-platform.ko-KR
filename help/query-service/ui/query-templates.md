---
title: 쿼리 템플릿
description: 쿼리 템플릿은 다른 사용자가 시간과 노력을 절약하기 위해 다시 사용할 수 있는 재사용 가능한 저장된 SQL 쿼리입니다. 쿼리 편집기 또는 쿼리 서비스 API를 사용하여 만들 수 있으며 모든 Experience Platform 데이터 세트에서 사용할 수 있습니다.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: d5d69134627b1a162691bda95732d989bd6e3469
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# 쿼리 템플릿

Adobe Experience Platform Query Service를 사용하면 SQL 코드를 쿼리 템플릿 형식으로 저장하고 다시 사용할 수 있습니다. 템플릿은 일반적으로 수행되는 작업의 반복을 방지하여 노력을 절약합니다. 조직 내에서 템플릿을 공유하고 기본 SQL에 액세스하거나 이해할 필요 없이 쿼리 값을 쉽게 변경할 수 있습니다.

이 문서에서는 Query Service에서 쿼리 템플릿을 만드는 데 필요한 정보를 제공합니다.

## 전제 조건

다음 항목이 있어야 합니다. [!UICONTROL 쿼리 관리] 쿼리 편집기에 액세스하고 플랫폼 UI 내에서 쿼리 대시보드를 볼 수 있는 권한이 활성화되었습니다. Adobe을 통해 권한이 활성화됩니다 [Admin Console](https://adminconsole.adobe.com/). 이 권한을 활성화할 관리자 권한이 없는 경우 조직의 관리자에게 문의하십시오. 다음에 대한 액세스 제어 설명서를 참조하십시오. [Admin Console을 통한 권한 추가에 대한 전체 지침](../../access-control/home.md).

## 쿼리 템플릿 만들기

Query Service API에 POST 요청을 수행하여 두 가지 방법을 통해 쿼리 템플릿을 만들 수 있습니다 `query-templates` 쿼리 편집기를 통해 쿼리를 작성, 이름 지정 및 저장하여 종단점입니다.

### 쿼리 편집기를 사용하여 쿼리를 템플릿으로 작성 및 저장

쿼리 편집기를 사용하여 다음을 수행하는 방법에 대한 지침은 설명서를 참조하십시오 [쓰기](./user-guide.md#query-authoring) 및 [쿼리 저장](./user-guide.md#saving-queries). 쿼리를 이름을 지정하고 저장하면 [!UICONTROL 템플릿] 탭.

## 쿼리 템플릿 찾아보기 {#browse}

플랫폼 UI의 쿼리 작업 영역에서 을 선택합니다 **[!UICONTROL 템플릿]** 을 클릭하여 사용 가능한 저장된 질의 목록을 표시합니다.

![템플릿 탭이 강조 표시된 질의 작업 영역입니다.](../images/ui/query-templates/query-templates.png)

관련 템플릿 정보를 찾으려면 사용 가능한 목록에서 쿼리 템플릿을 선택하여 세부 정보 패널을 엽니다.

![쿼리 ID가 강조 표시된 쿼리 작업 공간의 세부 사항 패널.](../images/ui/query-templates/details-panel.png)

세부 정보 패널에서 다음 네 가지 개별 작업을 실행할 수 있습니다.

* 선택 **[!UICONTROL 출력 데이터 세트]** 을 눌러 선택한 템플릿의 출력 데이터 세트를 편집합니다.
* 선택 **[!UICONTROL 예약 보기]** 로 이동 [!UICONTROL 예약] 탭. 이 뷰에는 쿼리와 연결된 일정 정보가 포함되어 있습니다.
* 선택 **[!UICONTROL 쿼리 삭제]** 템플릿을 삭제하려면 다음을 수행하십시오.
* 템플릿 이름을 선택하여 편집을 위해 SQL이 미리 채워지는 쿼리 편집기로 이동합니다.

### 쿼리 서비스 API를 사용하여 템플릿을 만듭니다

에 대한 지침은 설명서를 참조하십시오. [쿼리 템플릿을 만드는 방법](../api/query-templates.md#create-a-query-template) 쿼리 서비스 API 사용. 새로 만든 쿼리 템플릿에 대한 세부 정보는 응답 본문에 포함됩니다.

>[!NOTE]
>
>API를 사용하여 만든 템플릿도 플랫폼 UI 쿼리 서비스 템플릿 탭에 표시됩니다.

## 다음 단계

이 문서를 읽은 후에는 Query Service에서 쿼리 템플릿을 만드는 방법을 더 잘 이해할 수 있습니다. 자세한 내용은 [UI 개요](./overview.md)또는 [Query Service API 안내서](../api/getting-started.md) 쿼리 서비스 기능에 대해 자세히 알아보십시오.

자세한 내용은 [예약된 쿼리 엔드포인트 가이드](../api/scheduled-queries.md) api 또는 [쿼리 편집기 안내서](./user-guide.md#scheduled-queries) 추가 정보.
