---
title: 자동화된 데이터 세트 만료
description: Adobe Experience Platform UI에서 데이터 세트 만료를 예약하는 방법을 알아봅니다.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 18%

---

# 자동화된 데이터 세트 만료 일정 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="원치 않거나 만료된 고객 레코드 및 데이터 세트 삭제"
>abstract="<h2>설명</h2><p>규정 준수와 관련 없는 Experience Platform 데이터 라이프사이클을 관리하기 위해 소비자 레코드를 삭제하고 데이터 세트의 만료 일자를 예약할 수 있습니다. 데이터 주체 요청을 만들거나 관리하려면 &#39;데이터 주체 개인정보 보호 요청 준수&#39; 사용 사례 블록을 참조하시기 바랍니다.</p>"

Adobe Experience Platform UI의 [[!UICONTROL 데이터 수명 주기] 작업 공간](./overview.md)을 통해 데이터 세트의 만료를 예약할 수 있습니다. 데이터 세트가 만료 날짜에 도달하면 데이터 레이크, ID 서비스 및 실시간 고객 프로필은 각 서비스에서 데이터 세트의 콘텐츠를 제거하는 별도의 프로세스를 시작합니다. 세 서비스 모두에서 데이터가 삭제되면 만료는 완료된 것으로 표시됩니다.

>[!WARNING]
>
>데이터 세트가 만료되도록 설정된 경우 다운스트림 워크플로우가 부정적인 영향을 받지 않도록 데이터를 해당 데이터 세트로 수집할 수 있는 모든 데이터 흐름을 수동으로 변경해야 합니다.

이 문서에서는 Experience Platform UI에서 데이터 세트 만료를 예약하고 자동화하는 방법을 다룹니다.

>[!NOTE]
>
>데이터 세트 만료는 현재 Adobe Experience Platform Edge Network에서 데이터를 삭제하지 않습니다. 그러나 데이터 세트가 만료되도록 설정된 후에는 데이터가 Edge Network 내에 남아 있을 가능성이 없습니다. 데이터 세트 만료에 대한 15일 서비스 라이선스 계약이 데이터가 삭제되기 전에 Edge Network 내에 존재하는 14일 기간과 겹치기 때문입니다.

Advanced Data Lifecycle Management는 [데이터 세트 만료 끝점](../api/dataset-expiration.md)을 통해 데이터 세트 삭제를 지원하고 [작업 주문 끝점](../api/workorder.md)을 통해 기본 ID를 사용하여 ID 삭제(행 수준 데이터)를 지원합니다. Experience Platform UI를 통해 데이터 세트 만료와 [레코드 삭제](./record-delete.md)를 관리할 수도 있습니다. 자세한 내용은 연결된 설명서 를 참조하십시오.

>[!NOTE]
>
>데이터 수명 주기는 일괄 삭제를 지원하지 않습니다.

## 데이터 세트 만료 일정 예약 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="지침"
>abstract="<ul><li>왼쪽 탐색 메뉴에서 <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=ko">데이터 라이프사이클</a>를 선택한 다음 <b>요청 만들기</b>를 선택합니다.</li><li>레코드 삭제를 원하는 경우:</li>   <li><b>레코드</b>를 선택합니다.</li>   <li>레코드를 삭제할 특정 데이터 세트를 선택하거나 모든 데이터 세트에서 레코드를 삭제하는 옵션을 선택합니다.</li>   <li>레코드를 삭제할 소비자의 ID를 입력합니다. <b>ID 추가</b>를 선택하여 한 번에 하나씩 ID를 입력하거나 <b>파일 선택</b>을 선택하여 대신에 ID의 JSON 파일을 업로드합니다.</li>   <li>필요한 경우 <b>템플릿</b>을 선택하여 JSON 파일의 예상 형식을 확인합니다.</li><li><a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=ko#schedule-dataset-expiration">데이터 세트의 만료 일자를 예약</a>하려는 경우 설명서에서 지침을 참조하십시오.</li></ul>"

요청을 만들려면 작업 영역의 기본 페이지에서 **[!UICONTROL 요청 만들기]**&#x200B;를 선택하십시오.

>[!IMPORTANT]
>
>Real-Time CDP, Adobe Journey Optimizer 및 Customer Journey Analytics 사용자에게는 20개의 보류 중인 예약 데이터 세트 만료 작업 주문이 있습니다. Healthcare Shield 및 Privacy and Security Shield 사용자는 50개의 보류 중인 데이터 세트 만료 작업 주문을 가지고 있습니다. 즉, 한 번에 20개 또는 50개의 데이터 세트를 삭제하도록 예약할 수 있습니다.<br>예를 들어 데이터 세트가 20번 만료되고 내일 한 데이터 세트가 삭제될 예정인 경우 해당 데이터 세트가 삭제될 때까지 더 이상 만료를 설정할 수 없습니다.

![[!UICONTROL 요청 만들기]가 강조 표시된 [!UICONTROL 데이터 주기] 작업 영역](../images/ui/ttl/create-request-button.png)

요청 생성 워크플로가 나타납니다. [!UICONTROL 요청된 작업] 섹션에서 **[!UICONTROL 데이터 집합 삭제]**&#x200B;를 선택하여 데이터 집합 만료 예약에 대한 컨트롤을 업데이트합니다.

![[!UICONTROL 데이터 세트 삭제] 옵션이 강조 표시된 요청 생성 워크플로우입니다.](../images/ui/ttl/dataset-selected.png)

### 날짜 및 데이터 세트 선택 {#select-date-and-dataset}

**[!UICONTROL 요청된 작업]** 섹션에서 데이터 집합을 삭제할 날짜를 선택합니다. 날짜를 `mm/dd/yyyy` 형식으로 수동으로 입력하거나 달력 아이콘(![달력 아이콘)을 선택할 수 있습니다.대화 상자에서 날짜를 선택하려면 ](/help/images/icons/calendar.png))

![데이터 집합에 대해 선택한 만료 날짜가 강조 표시된 일정 대화 상자입니다.](../images/ui/ttl/select-date.png)

그런 다음 **[!UICONTROL 데이터 집합 세부 정보]**&#x200B;에서 데이터베이스 아이콘(![데이터베이스 아이콘)을 선택합니다.](/help/images/icons/database.png))을 클릭하여 데이터 집합 선택 대화 상자를 엽니다. 목록에서 만료를 적용할 데이터 집합을 선택한 다음 **[!UICONTROL 완료]**&#x200B;를 선택하십시오.

![데이터 세트를 선택하고 [!UICONTROL 완료]를 강조 표시한 상태로 [!UICONTROL 데이터 세트 선택] 대화 상자가 표시됩니다.](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>현재 샌드박스에 속하는 데이터 세트만 표시됩니다.

### 요청 제출 {#submit-request}

[!UICONTROL 데이터 집합 세부 정보] 섹션이 선택된 데이터 집합에 대한 기본 ID 및 스키마를 포함하도록 채워집니다. **[!UICONTROL 요청 설정]**&#x200B;에서 요청에 대한 이름과 선택적 설명을 입력한 다음 **[!UICONTROL 제출]**&#x200B;을 입력합니다.

![데이터 세트 만료 요청이 완료되어 [!UICONTROL 요청 설정] 및 [!UICONTROL 제출] 버튼이 강조 표시되었습니다.](../images/ui/ttl/submit.png)

[!UICONTROL 요청 확인] 대화 상자가 나타납니다. 데이터 세트 이름과 데이터 세트가 삭제될 날짜를 확인하는 메시지가 표시됩니다. 계속하려면 **[!UICONTROL 제출]**&#x200B;을 선택하세요.

요청이 제출되면 작업 순서가 만들어지고 [!UICONTROL 데이터 주기] 작업 영역의 기본 탭에 나타납니다. 여기에서 요청을 처리할 때 작업 주문의 상태를 모니터링할 수 있습니다.

>[!NOTE]
>
>데이터 세트 만료가 실행되면 처리되는 방법에 대한 자세한 내용은 [타임라인 및 투명도](../home.md#dataset-expiration-transparency)에 대한 개요 섹션을 참조하십시오.

## 데이터 세트 만료 편집 또는 취소 {#edit-or-cancel}

데이터 집합 만료를 편집하거나 취소하려면 작업 영역의 기본 페이지에서 **[!UICONTROL 데이터 집합]**&#x200B;을(를) 선택하고 목록에서 데이터 집합 만료를 선택하십시오.

데이터 세트 만료의 세부 정보 페이지에서 오른쪽 레일에는 예약된 삭제를 편집하거나 취소할 수 있는 컨트롤이 표시됩니다.

## 다음 단계

이 문서에서는 Experience Platform UI에서 데이터 세트 만료를 예약하는 방법을 다룹니다. UI에서 다른 데이터 최소화 작업을 수행하는 방법에 대한 자세한 내용은 [데이터 수명 주기 UI 개요](./overview.md)를 참조하십시오.

데이터 위생 API를 사용하여 데이터 세트 만료를 예약하는 방법에 대해 알아보려면 [데이터 세트 만료 끝점 안내서](../api/dataset-expiration.md)를 참조하십시오.
