---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;데이터 세트 생성;데이터 세트 생성;데이터 세트 만들기;
solution: Experience Platform
title: 쿼리 결과에서 출력 데이터 세트 생성
type: Tutorial
description: Adobe Experience Platform Query Service 를 사용하면 UI에서 데이터 세트를 만들 수 있습니다. 데이터 세트가 만들어지면 데이터 레이크의 다른 데이터 세트처럼 액세스하여 다양한 사용 사례에 사용할 수 있습니다.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 쿼리 결과에서 출력 데이터 세트 생성

[!DNL Query Service]을(를) 사용하면 쿼리를 사용하여 [!DNL Data Lake]의 데이터 세트를 생성할 수 있습니다. 그런 다음 이러한 데이터 세트를 추가 쿼리 또는 [!DNL Data Science Workspace], Real-Time Customer Profile 또는 [!DNL Analysis Workspace]과(와) 같은 다른 서비스에 대한 입력으로 사용할 수 있습니다.

## Adobe Experience Platform 사용자 인터페이스에서 데이터 세트 생성

Adobe Experience Platform UI(사용자 인터페이스)에서 데이터 세트를 만들려면 다음 단계를 수행하십시오.

1. 연결된 클라이언트를 사용하여 쿼리를 만들고 출력의 유효성을 검사합니다. [!DNL Query Editor]을(를) 사용하여 쿼리를 작성하는 방법에 대해 알아보려면 쿼리 작성에 대한 [!DNL Query Editor] UI 안내서 [을(를) 읽어보세요](./user-guide.md#writing-queries).

2. Experience Platform UI에서 **[!UICONTROL 쿼리]**, **[!UICONTROL 템플릿]** 탭으로 이동한 다음 만든 쿼리를 선택합니다. Experience Platform UI 내에서 조직에 대해 생성 및 저장된 쿼리를 보는 방법에 대한 자세한 내용은 [[!DNL Query Service] 개요](./overview.md#browse)를 참조하십시오.

3. 쿼리 세부 정보 패널에서 **[!UICONTROL CTAS로 실행]**&#x200B;을 선택합니다.

   ![Select [!UICONTROL CTAS로 실행]이 강조 표시된 쿼리 작업 영역 [!UICONTROL 템플릿] 탭.](../images/ui/create-datasets/run-as-ctas.png)

4. 표시되는 대화 상자에서 LDAP ID 앞에 데이터 세트 이름을 입력합니다. 데이터 세트 이름이 고유하거나 SQL 안전 상태일 필요는 없습니다. 데이터 세트에 대한 테이블 이름은 여기에서 만드는 데이터 세트 이름을 기반으로 생성됩니다.

5. 그런 다음 [!UICONTROL 설명] 필드에 데이터 집합에 대한 설명을 입력하고 **[!UICONTROL CTAS로 실행]**&#x200B;을 선택합니다.

   ![데이터 세트 세부 정보가 포함된 출력 데이터 세트 대화 상자 및 [!UICONTROL CTAS로 실행]이 강조 표시됨](../images/ui/create-datasets/run-query.png)

6. 쿼리 실행이 완료되면 **[!UICONTROL 데이터 세트]**(으)로 이동하여 만든 데이터 세트를 봅니다. Experience Platform UI 내에서 데이터 세트로 작업할 때 일반적인 작업을 수행하는 방법에 대한 자세한 내용은 [데이터 세트 UI 안내서](../../catalog/datasets/user-guide.md)를 참조하십시오.

데이터 세트를 만든 후에는 [!DNL Data Lake]의 다른 데이터 세트처럼 액세스하여 다양한 사용 사례에 사용할 수 있습니다.

>[!NOTE]
>
>라이브 구현에서는 데이터 세트를 만든 후 데이터 거버넌스 레이블을 적용해야 합니다. 데이터 세트에 데이터 사용 레이블을 적용하는 방법에 대한 자세한 내용은 [데이터 사용 레이블 개요](../../data-governance/labels/overview.md)를 참조하세요.

## 미리 정의된 [!DNL Experience Data Model] 스키마로 데이터 세트 생성

SQL 구문을 사용하여 미리 정의된 [!DNL Experience Data Model]&#x200B;(XDM) 스키마가 있는 데이터 집합을 생성합니다. [!DNL Query Service]에서 지원하는 구문에 대한 자세한 내용은 [SQL 구문 안내서](../sql/syntax.md#create-table-as-select)를 참조하십시오.

## 출력 데이터 세트

이 기능을 통해 생성된 데이터 세트는 SQL 문에 정의된 출력 데이터 구조와 일치하는 임시 스키마를 사용하여 생성됩니다. 일부 다운스트림 서비스에는 특정 XDM 스키마가 있는 데이터 세트가 필요합니다. 쿼리를 작성하기 전에 다운스트림 서비스에 대한 데이터 형식 요구 사항을 확인하십시오.

## 다음 단계

이 문서를 읽고 나면 이제 [!DNL Query Service]을(를) 사용하여 Experience Platform UI에서 데이터 세트를 생성하는 방법을 이해할 수 있습니다. Experience Platform UI에서 쿼리에 액세스하고, 쓰고, 실행하는 방법에 대한 자세한 내용은 [[!DNL Query Service] UI 개요](./overview.md)를 참조하십시오.
