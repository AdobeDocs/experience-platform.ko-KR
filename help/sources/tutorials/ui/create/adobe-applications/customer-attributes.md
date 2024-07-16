---
keywords: Experience Platform;홈;인기 항목;고객 속성
solution: Experience Platform
title: UI에서 고객 속성 Source 연결 만들기
type: Tutorial
description: UI에서 소스 연결을 만들어 고객 속성 프로필 데이터를 Adobe Experience Platform으로 가져오는 방법을 알아봅니다.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# UI에서 고객 속성 소스 연결 만들기

이 자습서에서는 고객 속성 프로필 데이터를 Adobe Experience Platform으로 가져오기 위해 UI에서 소스 연결을 만드는 단계를 제공합니다. 고객 특성에 대한 자세한 내용은 [고객 특성 개요](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=ko-KR)를 참조하십시오.

>[!IMPORTANT]
>
>고객 특성 소스는 현재 데이터 흐름을 활성화 또는 비활성화하는 것을 지원하지 않습니다.

## 소스 연결 만들기

>[!NOTE]
>
>고객 속성 프로필 데이터에 대한 소스 연결을 이미 설정한 경우 소스와 연결하는 옵션이 비활성화됩니다.

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 연결을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 창을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL Adobe 응용 프로그램] 범주에서 **[!UICONTROL 고객 특성]**&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/customer-attributes/catalog.png)

### 고객 속성 데이터 소스 선택

[!UICONTROL 데이터 추가] 화면에 고객 특성에 사용할 수 있는 모든 데이터 원본이 나열됩니다. 고객 속성 소스 연결당 하나의 데이터 세트만 선택할 수 있습니다.

>[!NOTE]
>
>필드 그룹, 스키마 및 데이터 세트는 흐름 프로비저닝의 일부로 즉시 생성됩니다. 그대로 유지되며 필요한 경우 수동으로 삭제해야 합니다.

고객 특성 소스에서는 스키마 진화가 지원되지 않습니다. 고객 특성 데이터 소스의 스키마 입력이 변경되면 Platform과 호환되지 않게 됩니다. 해결 방법으로, 기존 고객 속성 데이터 흐름과 관련 데이터 세트, 스키마 및 필드 그룹을 삭제한 다음 업데이트된 스키마 및 데이터 소스로 새 데이터 흐름을 만들 수 있습니다.

>[!IMPORTANT]
>
>고객 속성 데이터 흐름을 삭제할 수 있지만 해당 데이터 흐름은 데이터 흐름을 삭제한 후에도 유지됩니다. 데이터 집합을 수동으로 삭제하는 방법에 대한 단계는 [데이터 집합 삭제](../../../../../catalog/datasets/user-guide.md)에 대한 안내서를 참조하십시오.

새 연결을 만들려면 목록에서 데이터 원본을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![데이터 추가](../../../../images/tutorials/create/customer-attributes/add-data.png)

### 데이터 흐름 세부 정보 제공

데이터 흐름의 이름과 간단한 설명을 입력할 수 있는 [!UICONTROL 데이터 흐름 세부 정보] 단계가 나타납니다. 이 프로세스 동안 [!UICONTROL 오류 진단], [!UICONTROL 부분 수집] 및 [!UICONTROL 경고]에 대한 설정을 구성할 수도 있습니다.

[!UICONTROL 오류 진단]을 사용하면 데이터 흐름에서 발생하는 모든 잘못된 레코드에 대해 자세한 오류 메시지를 생성할 수 있고, [!UICONTROL 부분 수집]을(를) 사용하면 수동으로 정의하는 특정 임계값까지 오류가 포함된 데이터를 수집할 수 있습니다. 자세한 내용은 [부분 일괄 처리 수집 개요](../../../../../ingestion/batch-ingestion/partial.md)를 참조하십시오.

경고를 활성화하여 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 소스 경고 구독](../../alerts.md)에 대한 안내서를 참조하십시오.

데이터 흐름에 세부 정보를 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![데이터 흐름-세부 정보](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### 데이터 흐름 검토

새 데이터 흐름을 만들기 전에 검토할 수 있는 [!UICONTROL 검토] 단계가 나타납니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

* **[!UICONTROL 연결]**: 원본 형식, 선택한 원본 파일의 관련 경로 및 해당 원본 파일에 있는 열의 수를 표시합니다.
* **[!UICONTROL 데이터 집합 및 맵 필드 할당]**: 데이터 집합이 준수하는 스키마를 포함하여 소스 데이터가 수집되는 데이터 집합을 표시합니다.

![검토](../../../../images/tutorials/create/customer-attributes/review.png)

## 다음 단계

연결이 만들어지면 들어오는 데이터를 포함하도록 대상 스키마와 데이터 세트가 자동으로 만들어집니다. 초기 수집이 완료되면 [!DNL Real-Time Customer Profile] 및 [!DNL Segmentation Service]과(와) 같은 다운스트림 플랫폼 서비스에서 고객 특성 프로필 데이터를 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-Time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 개요](../../../../../segmentation/home.md)
