---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 쿼리 결과에서 데이터 집합 생성
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 쿼리 결과에서 데이터 집합 생성

쿼리 서비스의 진정한 장점은 쿼리가 데이터 레이크에서 데이터 세트를 생성하는 데 사용되어 데이터 과학 작업 공간, 실시간 고객 프로필 또는 분석 작업 공간과 같은 다른 서비스에 입력될 때 표시됩니다.

쿼리 서비스를 사용하면 UI에서 데이터 집합을 만들 수 있습니다. 다음 단계를 따르십시오.

1. 연결된 클라이언트를 사용하여 쿼리를 작성하고 출력물의 유효성을 확인합니다.
2. 플랫폼 UI 파섹
3. 목록에서 쿼리를 찾아 행 위에 마우스를 놓습니다.
4. 데이터 **세트 만들기를 클릭합니다**. ![이미지](../images/queries/create-datasets/click-create-dataset.png)
5. LDAP ID 앞에 데이터 세트 이름을 입력합니다(고유하거나 SQL-safe가 아니어야 함).시스템은 여기에 지정된 이름을 기반으로 &quot;테이블 이름&quot;을 생성합니다.
6. 데이터 집합 설명을 입력하고 쿼리 **실행을 클릭합니다**.![이미지](../images/queries/create-datasets/run-query.png)
7. 전체 쿼리를 본 다음 데이터 집합 목록 페이지로 이동하여 방금 만든 데이터 집합을 확인합니다.

데이터 세트를 만든 후 데이터 레이크의 다른 데이터세트처럼 액세스할 수 있으며 다양한 사용 사례에 사용할 수 있습니다.

>[!NOTE] 라이브 구현에서는 데이터 세트를 만든 후 데이터 거버넌스 레이블을 적용해야 합니다.

## 사전 정의된 경험 데이터 모델 스키마를 사용하여 데이터 집합 생성

XDM(Experience Data Model) 스키마를 사용하여 데이터 집합을 생성하려면 SQL 구문을 사용해야 합니다. 사용해야 하는 구문에 대한 자세한 내용은 SQL 구문 [안내서를](../sql/syntax.md#create-table-as-select)참조하십시오.

## 데이터 집합 출력

이 기능을 통해 생성된 데이터 집합은 SQL 문에 정의된 대로 출력 데이터의 구조와 일치하는 임시 스키마를 사용하여 생성됩니다. 일부 다운스트림 서비스에는 특정 XDM(Experience Data Model) 스키마를 사용하는 데이터 집합이 필요합니다. 쿼리를 쓰기 전에 다운스트림 서비스에 대한 데이터 서식 요구 사항을 확인합니다.