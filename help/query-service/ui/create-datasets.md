---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;데이터 세트 생성;데이터 세트 생성;데이터 세트 생성;
solution: Experience Platform
title: 쿼리 서비스의 결과에서 데이터 세트 생성
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform 쿼리 서비스를 통해 UI에서 데이터 세트를 만들 수 있습니다. 데이터 세트를 만든 후에는 데이터 레이크에서 다른 데이터 세트와 같이 액세스할 수 있고, 다양한 사용 사례에 사용할 수 있습니다.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Query Service의 결과에서 데이터 세트 생성

의 진정한 힘 [!DNL Query Service] 은 쿼리가 의 데이터 세트를 생성하는 데 사용될 때 표시됩니다. [!DNL Data Lake] 더 많은 쿼리나 기타 서비스(예: [!DNL Data Science Workspace], [!DNL Real-time Customer Profile], 또는 [!DNL Analysis Workspace].

[!DNL Query Service] UI에서 데이터 세트를 만들 수 있습니다. 다음 단계를 수행합니다.

1. 연결된 클라이언트를 사용하여 쿼리를 작성하고 출력의 유효성을 확인합니다.
2. 에 로그인합니다. [!DNL Platform] UI를 입력하고 쿼리로 이동합니다.
3. 목록에서 쿼리를 찾아 행 위로 마우스를 가져갑니다.
4. 선택 **[!UICONTROL 데이터 집합 만들기]**. ![이미지](../images/ui/create-datasets/output-dataset.png)
5. LDAP ID 앞에 데이터 집합 이름을 입력합니다(고유해야 하거나 SQL 안전할 필요가 없음). 여기서 지정한 이름을 기반으로 &quot;테이블 이름&quot;을 생성합니다.
6. 데이터 집합 설명을 입력하고 을(를) 선택합니다 **[!UICONTROL 쿼리 실행]**.![이미지](../images/ui/create-datasets/run-query.png)
7. 쿼리 완료를 시청한 다음 데이터 세트 목록 페이지로 이동하여 방금 만든 데이터 세트를 확인합니다.

데이터 세트를 만든 후에는 데이터 세트에 있는 다른 데이터 세트처럼 액세스할 수 있습니다 [!DNL Data Lake] 다양한 사용 사례에 사용됩니다.

>[!NOTE]
>
>라이브 구현에서는 데이터 세트가 만들어진 후 데이터 거버넌스 레이블을 적용해야 합니다.

## 사전 정의된 데이터 세트 생성 [!DNL Experience Data Model] 스키마

사전 정의된 데이터 세트를 생성하기 위해 [!DNL Experience Data Model] (XDM) 스키마에서는 SQL 구문을 사용해야 합니다. 사용해야 하는 구문에 대한 자세한 내용은 [SQL 구문 안내서](../sql/syntax.md#create-table-as-select).

## 출력 데이터 세트

이 기능을 통해 생성된 데이터 세트는 SQL 문에 정의된 출력 데이터의 구조와 일치하는 임시 스키마로 생성됩니다. 일부 다운스트림 서비스에는 특정 데이터 세트가 필요합니다 [!DNL Experience Data Model] (XDM) 스키마. 쿼리를 쓰기 전에 다운스트림 서비스에 대한 데이터 형식 요구 사항을 확인합니다.
