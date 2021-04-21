---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;데이터 집합 생성;데이터 집합 생성;데이터 집합 만들기;;home;popular topics;
solution: Experience Platform
title: 쿼리 서비스의 결과에서 데이터 집합 생성
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform 쿼리 서비스를 사용하면 UI에서 데이터 세트를 만들 수 있습니다. 데이터 세트를 만든 후 Data Lake의 다른 데이터세트처럼 액세스하여 다양한 사용 사례에 사용할 수 있습니다.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 쿼리 서비스의 결과에서 데이터 집합 생성

[!DNL Query Service]의 진정한 힘은 쿼리가 더 많은 쿼리 또는 [!DNL Data Science Workspace], [!DNL Real-time Customer Profile] 또는 [!DNL Analysis Workspace]와 같은 다른 서비스에 입력하기 위해 [!DNL Data Lake]에서 데이터 세트를 생성하는 데 사용될 때 표시됩니다.

[!DNL Query Service] UI에서 데이터 세트를 만들 수 있습니다. 다음 단계를 수행합니다.

1. 연결된 클라이언트를 사용하여 쿼리를 작성하고 출력물의 유효성을 확인합니다.
2. [!DNL Platform] UI에 로그인하고 [쿼리]로 이동합니다.
3. 목록에서 쿼리를 찾아 행 위에 마우스를 놓습니다.
4. **[!UICONTROL Create Dataset]**&#x200B;을 클릭합니다. ![이미지](../images/ui/output-dataset.png)
5. LDAP ID 앞에 데이터 세트 이름을 입력합니다(고유 또는 SQL 안전일 필요는 없음).시스템은 여기에 지정된 이름을 기반으로 &quot;테이블 이름&quot;을 생성합니다.
6. 데이터 세트 설명을 입력하고 **[!UICONTROL Run Query]**&#x200B;을 클릭합니다.![이미지](../images/ui/run-query.png)
7. 전체 쿼리를 확인한 다음 데이터 세트 목록 페이지로 이동하여 방금 만든 데이터 세트를 확인합니다.

데이터 세트를 만든 후 [!DNL Data Lake]의 다른 데이터세트처럼 액세스할 수 있으며 다양한 사용 사례에 사용할 수 있습니다.

>[!NOTE]
>
>라이브 구현에서는 데이터 세트를 만든 후 [!DNL Data Governance] 레이블을 적용해야 합니다.

## 사전 정의된 [!DNL Experience Data Model] 스키마를 사용하여 데이터 집합 생성

사전 정의된 [!DNL Experience Data Model](XDM) 스키마를 사용하여 데이터 세트를 생성하려면 SQL 구문을 사용해야 합니다. 사용해야 하는 구문에 대한 자세한 내용은 [SQL 구문 안내서](../sql/syntax.md#create-table-as-select)를 참조하십시오.

## 데이터 세트 출력

이 기능을 통해 생성된 데이터 세트는 SQL 문에 정의된 대로 출력 데이터의 구조와 일치하는 임시 스키마를 사용하여 생성됩니다. 일부 다운스트림 서비스에는 특정 [!DNL Experience Data Model](XDM) 스키마가 있는 데이터 세트가 필요합니다. 쿼리를 쓰기 전에 다운스트림 서비스에 대한 데이터 서식 요구 사항을 확인합니다.
