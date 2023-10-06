---
title: 데이터 세트 만료 관리
description: Adobe Experience Platform UI에서 데이터 세트 만료를 예약하는 방법을 알아봅니다.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 7931c8fe4a1ca5d255a80e7e6b0deb976d53c3de
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 20%

---

# 데이터 세트 만료 관리 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="원치 않거나 만료된 고객 레코드 및 데이터 세트 삭제"
>abstract="<h2>설명</h2><p>규정 준수와 관련 없는 Experience Platform 데이터의 수명 주기를 관리하기 위해 소비자 레코드를 삭제하고 데이터 세트의 만료 일자를 예약할 수 있습니다. 데이터 주체 요청을 만들거나 관리하려면 &#39;데이터 주체 개인 정보 보호 요청 준수&#39; 사용 사례 블록을 참조하시기 바랍니다.</p>"

다음 [[!UICONTROL 데이터 수명 주기] 작업 영역](./overview.md) Adobe Experience Platform UI에서 데이터 세트에 대한 만료를 예약할 수 있습니다. 데이터 세트가 만료 날짜에 도달하면 데이터 레이크, ID 서비스 및 실시간 고객 프로필은 각 서비스에서 데이터 세트의 콘텐츠를 제거하는 별도의 프로세스를 시작합니다. 세 서비스 모두에서 데이터가 삭제되면 만료는 완료된 것으로 표시됩니다.

>[!WARNING]
>
>데이터 세트가 만료되도록 설정된 경우 다운스트림 워크플로우가 부정적인 영향을 받지 않도록 데이터를 해당 데이터 세트로 수집할 수 있는 모든 데이터 흐름을 수동으로 변경해야 합니다.

이 문서에서는 Platform UI에서 데이터 세트 만료를 예약하고 관리하는 방법을 다룹니다.

>[!NOTE]
>
>데이터 세트 만료는 현재 Adobe Experience Platform Edge Network에서 데이터를 삭제하지 않습니다. 그러나 데이터 세트가 만료되도록 설정된 후에는 데이터가 Edge Network 내부에 남아 있을 가능성이 없습니다. 데이터 세트 만료에 대한 14일 서비스 라이선스 계약이 데이터가 삭제되기 전에 Edge Network 내부에 존재하는 14일 기간과 일치하기 때문입니다.

## 데이터 세트 만료 예약 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="지침"
>abstract="<ul><li>왼쪽 탐색 메뉴에서 <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=ko-KR">데이터 수명 주기</a>를 선택한 다음 <b>요청 만들기</b>를 선택합니다.</li><li>레코드 삭제를 원하는 경우:</li>   <li><b>레코드</b>를 선택합니다.</li>   <li>레코드를 삭제할 특정 데이터 세트를 선택하거나 모든 데이터 세트에서 레코드를 삭제하는 옵션을 선택합니다.</li>   <li>레코드를 삭제할 소비자의 ID를 입력합니다. <b>ID 추가</b>를 선택하여 한 번에 하나씩 ID를 입력하거나 <b>파일 선택</b>을 선택하여 대신에 ID의 JSON 파일을 업로드합니다.</li>   <li>필요한 경우 <b>템플릿</b>을 선택하여 JSON 파일의 예상 형식을 확인합니다.</li><li><a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=ko-KR#schedule-dataset-expiration">데이터세트의 만료 일자를 예약</a>하려는 경우 설명서에서 지침을 참조하십시오.</li></ul>"

요청을 만들려면 다음을 선택하십시오. **[!UICONTROL 요청 만들기]** 작업 공간의 기본 페이지에서 가져온 템플릿입니다.

>[!IMPORTANT]
>
동시에 예약된 데이터 세트가 최대 20개까지 만료될 수 있습니다. 즉, 한 번에 20개의 데이터 세트를 삭제하도록 예약할 수 있습니다. 이러한 만료일이 설정되는 시간 또는 연도에는 제한이 없습니다. 예를 들어 20개의 예약된 데이터 세트가 만료되고 내일 하나의 데이터 세트가 삭제되는 경우 해당 데이터 세트가 삭제될 때까지 더 이상 만료를 설정할 수 없습니다.

![다음 [!UICONTROL 데이터 수명 주기] 작업 공간 [!UICONTROL 요청 만들기] 강조 표시됨.](../images/ui/ttl/create-request-button.png)

요청 생성 워크플로가 나타납니다. 아래 [!UICONTROL 요청된 작업] 섹션, 선택 **[!UICONTROL 데이터 세트 삭제]** 데이터 세트 만료 예약에 대한 컨트롤을 업데이트하려면 다음을 수행하십시오.

![을(를) 사용한 요청 생성 워크플로 [!UICONTROL 데이터 세트 삭제] 강조 표시된 옵션입니다.](../images/ui/ttl/dataset-selected.png)

### 날짜 및 데이터 세트 선택 {#select-date-and-dataset}

아래 **[!UICONTROL 요청된 작업]** 섹션에서 데이터 세트를 삭제할 날짜를 선택합니다. 날짜를 형식으로 수동으로 입력할 수 있습니다 `mm/dd/yyyy`) 또는 달력 아이콘( )을 선택합니다.![달력 아이콘.](../images/ui/ttl/calendar-icon.png))을 클릭하여 대화 상자에서 날짜를 선택합니다.

![데이터 세트에 대해 만료 날짜가 선택되고 강조 표시된 달력 대화 상자.](../images/ui/ttl/select-date.png)

다음, 아래 **[!UICONTROL 데이터 세트 세부 정보]**&#x200B;데이터베이스 아이콘( )을 선택합니다.![데이터베이스 아이콘.](../images/ui/ttl/database-icon.png))을 클릭하여 데이터 세트 선택 대화 상자를 엽니다. 목록에서 만료를 적용할 데이터 세트를 선택한 다음 을 선택합니다. **[!UICONTROL 완료]**.

![다음 [!UICONTROL 데이터 세트 선택] 데이터 세트가 선택되어 있고 [!UICONTROL 완료] 강조 표시됨.](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
현재 샌드박스에 속하는 데이터 세트만 표시됩니다.

### 요청 제출 {#submit-request}

다음 [!UICONTROL 데이터 세트 세부 정보] 섹션 은 선택한 데이터 세트에 대한 기본 id 및 스키마를 포함하도록 채워집니다. 아래 **[!UICONTROL 요청 설정]**, 요청의 이름과 설명(선택 사항)을 입력한 다음 을 입력합니다. **[!UICONTROL 제출]**.

![이(가) 있는 완료된 데이터 세트 만료 요청 [!UICONTROL 요청 설정] 및 [!UICONTROL 제출] 버튼이 강조 표시되었습니다.](../images/ui/ttl/submit.png)

A [!UICONTROL 요청 확인] 대화 상자가 나타납니다. 데이터 세트 이름과 데이터 세트가 삭제될 날짜를 확인하는 메시지가 표시됩니다. 선택 **[!UICONTROL 제출]** 계속합니다.

요청이 제출되면 작업 주문이 만들어지고 의 메인 탭에 나타납니다. [!UICONTROL 데이터 수명 주기] 작업 영역. 여기에서 요청을 처리할 때 작업 주문의 상태를 모니터링할 수 있습니다.

>[!NOTE]
>
의 개요 섹션을 참조하십시오. [타임라인 및 투명도](../home.md#dataset-expiration-transparency) 데이터 세트 만료를 실행한 후 처리하는 방법에 대한 자세한 정보.

## 데이터 세트 만료 편집 또는 취소 {#edit-or-cancel}

데이터 세트 만료를 편집하거나 취소하려면 **[!UICONTROL 데이터 세트]** 작업 영역의 기본 페이지에서 목록에서 데이터 세트 만료를 선택합니다.

데이터 세트 만료의 세부 정보 페이지에서 오른쪽 레일에는 예약된 삭제를 편집하거나 취소할 수 있는 컨트롤이 표시됩니다.

## 다음 단계

이 문서에서는 Experience Platform UI에서 데이터 세트 만료를 예약하는 방법을 다룹니다. UI에서 다른 데이터 최소화 작업을 수행하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [데이터 라이프사이클 UI 개요](./overview.md).

데이터 위생 API를 사용하여 데이터 세트 만료를 예약하는 방법을 알아보려면 다음을 참조하십시오. [데이터 세트 만료 끝점 안내서](../api/dataset-expiration.md).
