---
keywords: Experience Platform;쿼리 서비스;쿼리 서비스;중첩된 데이터 구조;중첩된 데이터;병합;중첩된 데이터 병합;
title: BI 도구에 사용할 중첩된 데이터 구조 평면화
description: 이 문서에서는 쿼리 서비스에서 타사 BI 도구를 사용할 때 세션 중에 모든 테이블 및 뷰에 대한 XDM 스키마를 병합하는 방법을 설명합니다.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 1c590350c9d519dba60375b92de7bbbbd77961dc
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 타사 BI 도구와 함께 사용할 중첩된 데이터 구조 평면화

Adobe Experience Platform 쿼리 서비스 는 `FLATTEN` 타사 BI 도구를 통해 데이터베이스에 연결할 때 설정. 이 기능은 타사 BI 도구의 중첩된 데이터 구조를 병합하여 사용성을 개선하고 데이터를 검색, 분석, 변환 및 보고하는 데 필요한 워크로드를 줄입니다.

다음과 같은 많은 BI 도구 [!DNL Tableau] 및 [!DNL Power BI] 중첩된 데이터 구조를 기본적으로 지원하지 않습니다. 다음 `FLATTEN` 를 설정하면 플랫 버전을 제공하거나 쿼리 서비스를 사용하기 위해 데이터 위에 SQL 보기를 만들 필요가 없습니다 `CTAS` 또는 `INSERT INTO` 임시 스키마를 사용할 때 데이터 세트를 플랫 버전으로 복제하는 작업.

다음 `FLATTEN` 를 설정하면 각 리프 필드의 구조가 테이블의 루트로 가져오고 원래 네임스페이스 뒤에 필드 이름이 지정됩니다. 이렇게 하면 필드의 컨텍스트를 유지하면서 점 표기법을 사용하여 필드를 해당 XDM(Experience Data Model) 경로와 일치시킬 수 있습니다.

## 전제 조건

사용 `FLATTEN` 설정을 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [XDM 시스템](../../xdm/home.md): Experience Platform에서의 XDM 및 그 구현에 대한 높은 수준의 개요입니다.

   * [애드혹 스키마 만들기](../../xdm/tutorials/ad-hoc.md): 단일 데이터 세트에서만 사용할 수 있도록 네임스페이스가 지정된 필드가 있는 XDM 스키마를 Ad Hoc 스키마라고 합니다. 임시 스키마는 특정 종류의 소스 연결을 Experience Platform 및 만들기 위한 다양한 데이터 수집 워크플로우에서 사용됩니다.

* [샌드박스](../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

* [중첩된 데이터 구조](./nested-data-structures.md): 이 문서에서는 중첩된 데이터 구조를 포함하여 복잡한 데이터 유형으로 데이터 세트를 생성, 처리 또는 변환하는 방법에 대한 예를 제공합니다.

## FLATTEN 설정을 사용하여 데이터베이스에 연결 {#connect-with-flatten}

다음 `FLATTEN` 를 설정하면 중첩된 데이터 구조가 속성 이름이 행 값을 포함하는 열 이름이 되는 별도의 열로 병합됩니다. 중첩된 데이터 구조를 지원하지 않는 BI 도구의 데이터로 작업할 때 이 설정은 Ad Hoc 스키마의 사용성을 개선하고 필요한 워크로드를 줄입니다.

선택한 타사 클라이언트와 쿼리 서비스에 연결할 때 `FLATTEN` 을 데이터베이스 이름으로 설정합니다. 특정 BI 도구를 연결하는 방법에 대한 자세한 내용은 [클라이언트를 Query Service에 연결 개요](../clients/overview.md). 연결 문자열에는 다음이 포함되어야 합니다.

* 샌드박스 이름.
* 결장 후 `all` 또는 특정 데이터 세트 ID, 보기 ID 또는 데이터베이스 이름을 입력합니다.
* 물음표(?) 뒤에 다음 `FLATTEN` 키워드.

입력은 다음 형식을 사용해야 합니다.

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

연결 문자열의 예는 다음과 같습니다.

```terminal
prod:all?FLATTEN
```

## 예 {#example}

이 안내서에 사용된 예제 스키마는 표준 필드 그룹을 사용합니다 [!UICONTROL 상거래 세부 정보], 다음을 활용 `commerce` 개체 구조 및 `productListItems` 배열입니다. 다음에 대한 XDM 설명서 참조: [다음에 대한 추가 정보: [!UICONTROL 상거래 세부 정보] 필드 그룹](../../xdm/field-groups/event/commerce-details.md). 스키마 구조의 표현은 아래 이미지에서 볼 수 있습니다.

![다음을 포함하는 상거래 세부 정보 필드 그룹의 스키마 다이어그램 `commerce` 및 `productListItems` 구조입니다.](../images/essential-concepts/commerce-details.png)

BI 도구가 중첩된 데이터 구조를 지원하지 않는 경우 중첩된 필드에 직렬화된 값이 포함되어 있으면 이 필드를 참조하기 어려울 수 있습니다(예: `commerce` 및 `productListItems` 예제 스키마에서). 이러한 값은 인코딩된 단일 의 일부로 표시될 수 있습니다 `commerce` 문자열 필드 및 는 실제로 사용할 수 없습니다.

다음 값은 `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180) 및 `commerce.purchases.value`(1.0) 형식이 잘못된 중첩 필드의 경우.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

를 사용하여 `FLATTEN` 을 설정하면 점 표기법과 원래 경로 이름을 사용하여 스키마 내의 개별 필드 또는 중첩된 데이터 구조의 전체 섹션에 액세스할 수 있습니다. 를 사용하는 이 형식의 예 `commerce` 필드 그룹은 아래에 나와 있습니다.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

다음 `FLATTEN` 설정은 다른 데이터 구조를 처리할 때 특정 제한을 갖습니다. 전체 세부 정보는 [제한 섹션](#limitations).

### 쿼리의 필드에 따옴표 사용 {#quotation-marks}

이제 병합된 루트 필드는 해당 XDM 경로와 일치하도록 점 표기법을 사용합니다. 쿼리에 사용할 경우 필드를 따옴표(&quot; &quot;)로 묶어야 합니다.

아래의 SQL 예는 중첩 쿼리의 원래 상태를 표시합니다.

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

병합된 데이터 필드를 사용할 때 쿼리는 점 표기법을 사용하여 작성되며 아래와 같이 따옴표로 묶여 있습니다.

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## 제한 사항 {#limitations}

다음 `FLATTEN` 설정은 현재 다음 데이터 구조를 병합하지 않습니다.

| 데이터 구조 | 제한 사항 |
|---|---|
| 배열 | 명시적 배열 인덱스 또는 `EXPLODE` 배열에 액세스하는 함수입니다. |
| 지도 | 문자열 키를 사용하여 맵 아래의 값에 액세스하여 맵에 액세스합니다. |

맵과 배열 제한을 모두 해결하려면 Power BI의 고급 옵션 -> SQL 문과 같은 BI 도구 원시 SQL 편집 기능을 사용해야 합니다.

맵 및 배열 제한 사항을 모두 해결하려면 원시 SQL 편집과 같은 BI 도구가 필요합니다. 방법은 안내서 참조 [Power BI 고급 옵션을 사용하여 사용자 지정 SQL 쿼리를 입력합니다.](../clients/power-bi.md#import-tables-using-custom-sql) SQL 문 섹션에서 참조할 수 있습니다.

## 다음 단계

이 문서에서는 타사 BI 도구와 함께 사용할 중첩된 데이터 구조를 병합하는 방법을 다룹니다. 클라이언트를 아직 연결하지 않은 경우 다음을 참조하십시오. [클라이언트 연결 개요](../clients/overview.md) 지원되는 타사 클라이언트 목록입니다.
