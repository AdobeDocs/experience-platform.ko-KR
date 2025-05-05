---
keywords: Experience Platform;쿼리 서비스;쿼리 서비스;중첩된 데이터 구조;중첩된 데이터;평면화;중첩된 데이터 평면화;
title: BI 도구에 사용할 중첩된 데이터 구조 평면화
description: 이 문서에서는 쿼리 서비스에서 타사 BI 도구를 사용할 때 세션 중에 모든 테이블 및 뷰에 대한 XDM 스키마를 병합하는 방법을 설명합니다.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# 타사 BI 도구와 함께 사용할 중첩된 데이터 구조 평면화

Adobe Experience Platform Query Service는 타사 BI 도구를 통해 데이터베이스에 연결할 때 `FLATTEN` 설정을 지원합니다. 이 기능은 타사 BI 도구의 중첩된 데이터 구조를 병합하여 사용성을 개선하고 데이터를 검색, 분석, 변환 및 보고하는 데 필요한 워크로드를 줄입니다.

[!DNL Tableau] 및 [!DNL Power BI]과(와) 같은 많은 BI 도구는 기본적으로 중첩된 데이터 구조를 지원하지 않습니다. `FLATTEN` 설정을 사용하면 임시 버전을 제공하기 위해 데이터 위에 SQL 보기를 만들거나 임시 스키마를 사용할 때 쿼리 서비스 `CTAS` 또는 `INSERT INTO` 작업을 사용하여 데이터 세트를 일반 버전으로 복제해야 하는 번거로움이 없습니다.

`FLATTEN` 설정은 각 리프 필드의 구조를 테이블의 루트로 가져오고 원래 네임스페이스 뒤에 필드 이름을 지정합니다. 이렇게 하면 필드의 컨텍스트를 유지하면서 점 표기법을 사용하여 필드를 해당 XDM(Experience Data Model) 경로와 일치시킬 수 있습니다.

## 전제 조건

`FLATTEN` 설정을 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대한 이해가 필요합니다.

* [XDM 시스템](../../xdm/home.md): Experience Platform에서의 XDM 및 해당 구현에 대한 높은 수준의 개요입니다.

   * [Ad Hoc 스키마 만들기](../../xdm/tutorials/ad-hoc.md): 단일 데이터 집합에서만 사용하도록 이름이 지정된 필드가 있는 XDM 스키마를 Ad Hoc 스키마라고 합니다. 임시 스키마는 Experience Platform의 다양한 데이터 수집 워크플로우에서 사용되며 특정 종류의 소스 연결을 만듭니다.

* [샌드박스](../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

* [중첩된 데이터 구조](./nested-data-structures.md): 이 문서에서는 중첩된 데이터 구조를 포함하여 복잡한 데이터 형식의 데이터 집합을 만들거나 처리하거나 변환하는 방법에 대한 예를 제공합니다.

## FLATTEN 설정을 사용하여 데이터베이스에 연결 {#connect-with-flatten}

`FLATTEN` 설정은 중첩된 데이터 구조를 별도의 열로 병합합니다. 여기서 특성 이름은 행 값을 포함하는 열 이름이 됩니다. 중첩된 데이터 구조를 지원하지 않는 BI 도구의 데이터로 작업할 때 이 설정은 Ad Hoc 스키마의 사용성을 개선하고 필요한 워크로드를 줄입니다.

선택한 타사 클라이언트를 사용하여 쿼리 서비스에 연결할 때 `FLATTEN` 설정을 데이터베이스 이름에 추가합니다. 특정 BI 도구를 연결하는 방법에 대한 자세한 내용은 [클라이언트를 Query Service에 연결 개요](../clients/overview.md)에서 해당 설명서를 참조하십시오. 연결 문자열에는 다음이 포함되어야 합니다.

* 샌드박스 이름.
* 콜론 뒤에 `all`이 있거나 특정 데이터 세트 ID, 보기 ID 또는 데이터베이스 이름이 있습니다.
* 물음표(?) 뒤에 `FLATTEN` 키워드가 옵니다.

입력은 다음 형식을 사용해야 합니다.

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

연결 문자열의 예는 다음과 같습니다.

```terminal
prod:all?FLATTEN
```

## 예 {#example}

이 안내서에 사용된 예제 스키마는 표준 필드 그룹 [!UICONTROL Commerce 세부 정보]를 사용합니다. 이 스키마는 `commerce` 개체 구조 및 `productListItems` 배열을 사용합니다. [!UICONTROL Commerce 세부 정보] 필드 그룹[&#128279;](../../xdm/field-groups/event/commerce-details.md)에 대한 자세한 내용은 XDM 설명서를 참조하세요. 스키마 구조의 표현은 아래 이미지에서 볼 수 있습니다.

![`commerce` 및 `productListItems` 구조를 포함하는 Commerce 세부 정보 필드 그룹의 스키마 다이어그램입니다.](../images/key-concepts/commerce-details.png)

BI 도구가 중첩된 데이터 구조를 지원하지 않는 경우 중첩된 필드에 직렬화된 값(예: 예제 스키마의 `commerce` 및 `productListItems`)이 포함되어 있으면 중첩된 필드를 참조하기 어려울 수 있습니다. 이러한 값은 인코딩된 단일 `commerce` 문자열 필드의 일부로 나타날 수 있으며 실제로 사용할 수 없습니다.

다음 값은 형식이 잘못 중첩된 필드의 `commerce.order.priceTotal`(3018.0), `commerce.order.purchaseID`(c9b5aff9-25de-450b-98f4-4484a2170180) 및 `commerce.purchases.value`(1.0)을(를) 나타냅니다.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

`FLATTEN` 설정을 사용하면 점 표기법과 원래 경로 이름을 사용하여 스키마 내의 개별 필드 또는 중첩된 데이터 구조의 전체 섹션에 액세스할 수 있습니다. `commerce` 필드 그룹을 사용하는 이 형식의 예는 아래에 나와 있습니다.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

다른 데이터 구조를 처리할 때 `FLATTEN` 설정에 특정 제한이 있습니다. [제한 섹션](#limitations)에 전체 세부 정보가 제공됩니다.

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

`FLATTEN` 설정이 현재 다음 데이터 구조를 병합하지 않습니다.

| 데이터 구조 | 제한 사항 |
|---|---|
| 배열 | 명시적 배열 인덱스 또는 `EXPLODE` 함수를 사용하여 배열에 액세스합니다. |
| 지도 | 문자열 키를 사용하여 맵 아래의 값에 액세스하여 맵에 액세스합니다. |

맵과 배열 제한을 모두 해결하려면 Power BI의 고급 옵션 -> SQL 문과 같은 BI 도구 원시 SQL 편집 기능을 사용해야 합니다.

맵 및 배열 제한 사항을 모두 해결하려면 원시 SQL 편집과 같은 BI 도구가 필요합니다. SQL 문 섹션에서 [Power BI 고급 옵션을 사용하여 사용자 지정 SQL 쿼리를 입력](../clients/power-bi.md#import-tables-using-custom-sql)하는 방법에 대한 안내서를 참조하세요.

## 다음 단계

이 문서에서는 타사 BI 도구와 함께 사용할 중첩된 데이터 구조를 병합하는 방법을 다룹니다. 아직 클라이언트를 연결하지 않은 경우 [클라이언트 연결 개요](../clients/overview.md)에서 지원되는 타사 클라이언트 목록을 참조하십시오.
