---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;문제 해결 가이드;faq;문제 해결;
solution: Experience Platform
title: Query Service 문제 해결 안내서
topic-legacy: troubleshooting
description: 이 문서에는 Query Service와 관련된 일반적인 질문과 대답이 포함되어 있습니다. 항목에는 데이터, 내보내기, 타사 도구 및 PSQL 오류가 포함됩니다.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 491aadf161bd822cb40a5ef5dd107831bca1d2c4
workflow-type: tm+mt
source-wordcount: '4383'
ht-degree: 1%

---

# [!DNL Query Service] 문제 해결 안내서

이 문서에서는 Query Service에 대해 자주 묻는 질문에 대한 답변을 제공하며 Query Service를 사용할 때 자주 표시되는 오류 코드 목록을 제공합니다. Adobe Experience Platform의 다른 서비스와 관련된 질문 및 문제 해결은 다음을 참조하십시오. [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md).

FAQ에 대한 다음 목록은 다음 카테고리로 분류됩니다.

- [일반](#general)
- [데이터 내보내기](#exporting-data)
- [타사 도구](#third-party-tools)
- [PostgreSQL API 오류](#postgresql-api-errors)
- [REST API 오류](#rest-api-errors)

## 일반 쿼리 서비스 질문 {#general}

이 섹션에는 성능, 제한 및 프로세스에 대한 정보가 포함되어 있습니다.

### 쿼리 서비스 편집기에서 자동 완성 기능을 끌 수 있습니까?

+++아니요. 현재 편집기에서 자동 완성 기능을 끄면 안 됩니다.
+++

### 쿼리에 입력할 때 쿼리 편집기가 느려지는 이유는 무엇입니까?

+++답변 한 가지 잠재적인 원인은 자동 완성 기능입니다. 이 기능은 쿼리 편집 중에 간혹 편집기의 속도가 느려질 수 있는 특정 메타데이터 명령을 처리합니다.
+++

### 사용할 수 있나요 [!DNL Postman] Query Service API에 대해

+++답변 예, 를 사용하여 모든 Adobe API 서비스를 시각화하고 상호 작용할 수 있습니다 [!DNL Postman] (무료 타사 애플리케이션). 보기 [[!DNL Postman] 설정 안내서](https://video.tv.adobe.com/v/28832) Adobe Developer 콘솔에서 프로젝트를 설정하고 여기에 사용하는 데 필요한 모든 자격 증명을 획득하는 방법에 대한 단계별 지침입니다. [!DNL Postman]. 에 대한 공식 설명서를 참조하십시오. [시작, 실행 및 공유에 대한 지침 [!DNL Postman] 컬렉션](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### UI를 통해 쿼리에서 반환되는 최대 행 수에 제한이 있습니까?

+++답변 예, Query Service는 명시적 제한이 외부에서 지정되지 않는 한 내부적으로 50,000개 행 제한을 적용합니다. 다음 사항에 대한 지침을 참조하십시오 [대화형 쿼리 실행](./best-practices/writing-queries.md#interactive-query-execution) 자세한 내용
+++

### 쿼리를 사용하여 행을 업데이트할 수 있습니까?

+++답변 일괄 처리 쿼리에서 데이터 집합 내의 행을 업데이트할 수 없습니다.
+++

### 쿼리의 결과 출력에 데이터 크기 제한이 있습니까?

+++아니요. 데이터 크기에는 제한이 없지만 대화형 세션에서 10분의 쿼리 시간 제한 제한이 있습니다. 쿼리가 배치 CTAS로 실행되면 10분 시간 제한을 적용할 수 없습니다. 다음 사항에 대한 지침을 참조하십시오 [대화형 쿼리 실행](./best-practices/writing-queries.md#interactive-query-execution) 자세한 내용
+++

### SELECT 쿼리의 행 출력 수에 대한 제한을 무시하려면 어떻게 합니까?

+++응답 출력 행 제한을 무시하려면 쿼리에 &quot;LIMIT 0&quot;을 적용합니다. 예:

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### 10분 후에 쿼리가 시간 초과되지 않도록 하려면 어떻게 해야 합니까?

+++답변 쿼리 시간 제한 시 다음 솔루션 중 하나 이상이 권장됩니다.

- [쿼리를 CTAS 쿼리로 변환](./sql/syntax.md#create-table-as-select) 실행 일정을 지정합니다. 실행 예약은 다음 중 하나를 수행할 수 있습니다 [ui 사용](./ui/user-guide.md#scheduled-queries) 또는 [API](./api/scheduled-queries.md#create).
- 추가 내용을 적용하여 작은 데이터 청크에서 쿼리를 실행합니다 [조건 필터링](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [EXPLAIN 명령 실행](./sql/syntax.md#explain) 더 자세한 정보를 수집하기 위해
- 데이터 세트 내의 데이터 통계를 검토합니다.
- 쿼리를 간소화된 양식으로 전환한 다음 [준비된 설명](./sql/prepared-statements.md).
+++

### 여러 쿼리가 동시에 실행되는 경우 쿼리 서비스 성능에 문제가 있거나 영향을 줍니까?

+++아니요. 쿼리 서비스에는 동시 쿼리가 서비스 성능에 큰 영향을 주지 않도록 하는 자동 크기 조정 기능이 있습니다.
+++

### 예약된 키워드를 열 이름으로 사용할 수 있습니까?

+++답변: 열 이름으로 사용할 수 없는 특정 예약 키워드가 있습니다. `ORDER`, `GROUP BY`, `WHERE`, `DISTINCT`. 이러한 키워드를 사용하려면 이러한 열을 이스케이프 처리해야 합니다.
+++

### 계층 데이터 세트에서 열 이름은 어떻게 찾을 수 있습니까?

+++답변 다음 단계는 UI를 통해 데이터 집합에 대한 표 형식의 보기를 표시하는 방법(중첩된 모든 필드 및 병합된 양식의 열 포함)을 설명합니다.

- Experience Platform에 로그인한 후 **[!UICONTROL 데이터 세트]** 로 이동할 UI의 왼쪽 탐색 영역에서 [!UICONTROL 데이터 세트] 대시보드 .
- 데이터 세트 [!UICONTROL 찾아보기] 탭이 열립니다. 검색 창을 사용하여 사용 가능한 옵션을 세분화할 수 있습니다. 표시된 목록에서 데이터 세트를 선택합니다.

![검색 막대와 데이터 세트가 강조 표시된 Platform UI의 데이터 세트 대시보드.](./images/troubleshooting/dataset-selection.png)

- 다음 [!UICONTROL 데이터 세트 활동] 화면이 나타납니다. 선택 **[!UICONTROL 데이터 세트 미리 보기]** xdm 스키마의 대화 상자를 열고 선택한 데이터 집합에서 병합된 데이터의 테이블 보기를 엽니다. 자세한 내용은 [데이터 세트 설명서 미리 보기](../catalog/datasets/user-guide.md#preview-a-dataset)

![미리 보기 데이터 세트가 강조 표시된 데이터 세트 대시보드의 데이터 세트 활동 탭.](./images/troubleshooting/dataset-preview.png)

- 스키마에서 필드를 선택하여 병합된 열에 해당 내용을 표시합니다. 열 이름은 페이지 오른쪽의 해당 컨텐츠 위에 표시됩니다. 이 데이터 세트를 쿼리하는 데 사용할 이 이름을 복사해야 합니다.

![병합된 데이터의 XDM 스키마 및 테이블 형식 보기입니다. 중첩된 데이터 세트의 열 이름이 UI에서 강조 표시됩니다.](./images/troubleshooting/column-name.png)

에 대한 자세한 내용은 설명서 를 참조하십시오 [중첩 데이터 구조를 사용한 작업 방법](./best-practices/nested-data-structures.md) 쿼리 편집기 또는 타사 클라이언트 사용.
+++

### 배열이 포함된 데이터 세트에 대한 쿼리 속도를 높이는 방법

+++답변 배열이 포함된 데이터 세트에 대한 쿼리 성능을 향상하려면 다음을 수행해야 합니다 [어레이 분해](https://spark.apache.org/docs/latest/api/sql/index.html#explode) 로서의 [CTAS 쿼리](./sql/syntax.md#create-table-as-select) 런타임 시 검색한 후 처리 시간을 향상시킬 수 있는 기회를 확인하십시오.
+++

### 적은 수의 행에만 대해 몇 시간 후에도 내 CTAS 쿼리가 계속 처리되는 이유는 무엇입니까?

+++답변 매우 작은 데이터 세트에서 쿼리가 오래 걸리는 경우 고객 지원에 문의하십시오.

처리하는 동안 쿼리가 중단되는 이유는 다양할 수 있습니다. 정확한 원인을 규명하려면 사례별로 심층적인 분석이 필요합니다. [Adobe 고객 지원에 문의하십시오](#customer-support) 이 프로세스에 참여하도록
+++

### Adobe 고객 지원에 문의하려면 어떻게 해야 합니까? {#customer-support}

+++답변
[Adobe 고객 지원 전화 번호의 전체 목록](https://helpx.adobe.com/ca/contact/phone.html) Adobe 도움말 페이지에서 사용할 수 있습니다. 또는 다음 단계를 완료하여 도움말을 온라인으로 찾을 수 있습니다.

- 다음으로 이동 [https://www.adobe.com/](https://www.adobe.com/) 참조하십시오.
- 위쪽 탐색 막대의 오른쪽에서 을 선택합니다. **[!UICONTROL 로그인]**.

![로그인 이 강조 표시된 Adobe 웹 사이트입니다.](./images/troubleshooting/adobe-sign-in.png)

- Adobe 라이선스에 등록된 Adobe ID 및 암호를 사용하십시오.
- 선택 **[!UICONTROL 도움말 및 지원]** 상단 탐색 막대에서 을 클릭합니다.

![도움말 및 지원, 엔터프라이즈 지원 및 연락처 기능이 강조 표시된 위쪽 탐색 모음 드롭다운 메뉴](./images/troubleshooting/help-and-support.png)

다음을 포함하는 드롭다운 배너가 나타납니다 [!UICONTROL 도움말 및 지원] 섹션을 참조하십시오. 선택 **[!UICONTROL 문의]** Adobe 고객 지원 가상 도우미를 열려면 또는 **[!UICONTROL 엔터프라이즈 지원]** 대규모 조직을 위한 전담 도움말
+++

### 이전 작업이 성공적으로 완료되지 않으면 후속 작업을 실행하지 않고 순차적 일련의 작업을 구현하려면 어떻게 합니까?

+++답변 익명 블록 기능을 사용하면 순서대로 실행되는 하나 이상의 SQL 문을 체인 지정할 수 있습니다. 예외 처리 옵션도 허용합니다.

자세한 내용은 [익명 블록 설명서](./best-practices/anonymous-block.md) 자세한 내용
+++

### Query Service에서 사용자 지정 속성을 구현하려면 어떻게 해야 합니까?

+++답변 사용자 지정 속성을 구현하는 방법에는 두 가지가 있습니다.

1. 기존 [Adobe 정의 함수](./sql/adobe-defined-functions.md) 사용 사례의 요구 사항을 충족하는지 확인합니다.
1. 이전 제안이 사용 사례를 충족하지 않는 경우 [창 함수](./sql/adobe-defined-functions.md#window-functions). 창 함수는 시퀀스의 모든 이벤트를 봅니다. 또한 내역 데이터를 검토할 수 있으며 모든 조합에서 사용할 수 있습니다.
+++

### 쿼리를 쉽게 다시 사용할 수 있도록 템플릿을 설정할 수 있습니까?

+++Answer Yes, 준비된 문을 사용하여 쿼리를 템플릿을 설정할 수 있습니다. 준비된 문은 성능을 최적화하고 쿼리를 반복적으로 다시 구문 분석하지 않도록 할 수 있습니다. 자세한 내용은 [준비된 명세서 문서](./sql/prepared-statements.md) 자세한 내용
+++

### 쿼리에 대한 오류 로그를 검색하려면 어떻게 합니까? {#error-logs}

+++답변 특정 쿼리에 대한 오류 로그를 검색하려면 먼저 쿼리 서비스 API를 사용하여 쿼리 로그 세부 사항을 가져와야 합니다. HTTP 응답에는 쿼리 오류를 조사하는 데 필요한 쿼리 ID가 포함되어 있습니다.

여러 쿼리를 검색하려면 GET 명령을 사용합니다. API를 호출하는 방법에 대한 자세한 내용은 [샘플 API 호출 설명서](./api/queries.md#sample-api-calls).

응답에서 조사할 쿼리를 식별하고 이 응답을 사용하여 다른 GET 요청을 만듭니다 `id` 값. 전체 지침은 [id 설명서로 쿼리 검색](./api/queries.md#retrieve-a-query-by-id).

성공적인 응답은 HTTP 상태 200을 반환하고 를 포함합니다 `errors` 배열입니다. 간결성을 위해 응답이 줄었습니다.

```json
{
    "isInsertInto": false,
    "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
    "clientId": "8c2455819a624534bb665c43c3759877",
    "state": "SUCCESS",
    "rowCount": 0,
    "errors": [{
      'code': '58000', 
      'message': 'Batch query execution gets : [failed reason ErrorCode: 58000 Batch query execution gets : [Analysis error encountered. Reason: [sessionId: f055dc73-1fbd-4c9c-8645-efa609da0a7b Function [varchar] not defined.]]]', 
      'errorType': 'USER_ERROR'
      }],
    "isCTAS": false,
    "version": 1,
    "id": "343388b0-e0dd-4227-a75b-7fc945ef408a",
}
```

다음 [Query Service API 참조 설명서](https://www.adobe.io/experience-platform-apis/references/query-service/) 사용 가능한 모든 끝점에 대한 자세한 정보를 제공합니다.
+++

### &quot;스키마 유효성 검사 오류&quot;는 무엇을 의미합니까?

+++답변 &quot;스키마 유효성 검사 오류&quot; 메시지는 시스템에서 스키마 내의 필드를 찾을 수 없음을 의미합니다. 에 대한 모범 사례 문서를 읽어야 합니다. [Query Service에서 데이터 자산 구성](./best-practices/organize-data-assets.md) 다음에 [선택 항목으로 테이블 만들기 설명서](./sql/syntax.md#create-table-as-select).

다음 예제에서는 CTAS 구문 및 구조체 데이터 형식을 사용하는 방법을 보여 줍니다.

```sql
CREATE TABLE table_name WITH (SCHEMA='schema_name')

AS SELECT '1' as _id,

 STRUCT

  ('2021-02-17T15:39:29.0Z' AS taskActualCompletionDate,

    '2020-09-09T21:21:16.0Z' AS taskActualStartDate,

    'Consulting' AS taskdescription,

    '5f6527c10011e09b89666c52d9a8c564' AS taskguide,

    'Stakeholder Consulting Engagement' AS taskname, 

    '2020-09-09T15:00:00.0Z' AS taskPlannedStartDate,

    '2021-02-15T11:00:00.0Z' AS taskPlannedCompletionDate

  ) AS _workfront ;
```

+++

### 매일 시스템에 들어오는 새 데이터를 빠르게 처리하려면 어떻게 해야 합니까?

+++ [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) 절은 스냅샷 ID를 기반으로 테이블에서 데이터를 점진적으로 읽는 데 사용할 수 있습니다. 이 기능은 와 함께 사용하는 데 이상적입니다 [증분 로드](./best-practices/incremental-load.md) 마지막 로드 실행 이후 생성 또는 수정된 데이터 세트에 있는 정보만 처리하는 디자인 패턴입니다. 따라서 처리 효율을 높이고 스트리밍 및 배치 데이터 처리와 함께 사용할 수 있습니다.
+++

### 프로필 UI에 표시된 숫자와 프로필 내보내기 데이터 세트에서 계산된 숫자 간에 차이가 있는 이유는 무엇입니까?

+++답변 프로필 대시보드에 표시된 숫자는 마지막 스냅샷에서 정확합니다. 프로필 내보내기 테이블에서 생성된 숫자는 내보내기 쿼리에 전적으로 의존합니다. 따라서 특정 세그먼트에 적합한 프로필 수를 쿼리하는 것은 이러한 불일치를 위한 일반적인 원인입니다.

>[!NOTE]
>
>쿼리는 내역 데이터를 포함하지만 UI는 현재 프로필 데이터만 표시합니다.

+++

### 쿼리에서 빈 하위 집합을 반환한 이유는 무엇입니까?

+++답변 쿼리 범위가 너무 좁기 때문일 수 있습니다. 의 섹션을 체계적으로 제거해야 합니다 `WHERE` 절을 클릭하여 일부 데이터를 볼 수 있습니다.

다음과 같은 작은 쿼리를 사용하여 데이터 집합에 데이터가 포함되어 있는지 확인할 수도 있습니다.

```sql
SELECT count(1) FROM myTableName
```

+++

### 데이터를 샘플링할 수 있습니까?

+++답변 이 기능은 현재 진행 중입니다. 자세한 내용은 [릴리스 노트](../release-notes/latest/latest.md) 기능이 릴리스될 준비가 되면 플랫폼 UI 대화 상자를 통해 제공됩니다.
+++

### Query Service에서 지원하는 도우미 함수는 무엇입니까?

+++Answer Query Service에서는 SQL 기능을 확장하기 위한 몇 가지 기본 제공 SQL 도우미 함수를 제공합니다. 문서의 전체 목록을 보려면 문서를 참조하십시오 [쿼리 서비스에서 지원하는 SQL 함수](./sql/spark-sql-functions.md).
+++

### 모두 모국어입니까 [!DNL Spark SQL] 가 지원되거나 사용자가 래퍼로만 제한되는 함수 [!DNL Spark SQL] Adobe에서 제공하는 함수?

+++모든 오픈 소스는 아니지만 아직 답하십시오 [!DNL Spark SQL] 데이터 레이크 데이터에 대한 기능이 테스트되었습니다. 테스트 및 확인 후 지원되는 목록에 추가됩니다. 자세한 내용은 [지원되는 목록 [!DNL Spark SQL] 함수](./sql/spark-sql-functions.md) 를 눌러 특정 함수를 확인합니다.
+++

### 사용자가 다른 쿼리에서 사용할 수 있는 UDF(사용자 정의 함수)를 정의할 수 있습니까?

+++답변 데이터 보안 고려 사항으로 인해 UDF에 대한 사용자 정의 정의가 허용되지 않습니다.
+++

### 예약된 쿼리가 실패하면 어떻게 해야 합니까?

+++먼저 로그를 확인하여 오류 세부 정보를 확인하십시오. 의 FAQ 섹션 [로그 내에서 오류 찾기](#error-logs) 이 작업을 수행하는 방법에 대한 자세한 정보를 제공합니다.

수행 방법에 대한 지침도 설명서에서 확인해야 합니다 [UI에서 예약된 쿼리](./ui/user-guide.md#scheduled-queries) 및 [API](./api/scheduled-queries.md).

다음은 를 사용할 때 예약된 쿼리에 대한 고려 사항 목록입니다 [!DNL Query Editor]. 에는 적용되지 않습니다 [!DNL Query Service] API:<br/>이미 생성, 저장 및 실행된 쿼리에 예약만 추가할 수 있습니다.<br/>사용자 **사용할 수 없음** 매개 변수가 있는 쿼리에 일정을 추가합니다.<br/>예약된 쿼리 **사용할 수 없음** 익명 블록을 포함합니다.<br/>예약만 수행할 수 있습니다 **하나** UI를 사용하여 쿼리 템플릿. 쿼리 템플릿에 예약을 더 추가하려면 API를 사용해야 합니다. API를 사용하여 이미 일정을 추가한 경우 UI를 사용하여 추가 일정을 추가할 수 없습니다.
+++

### 세션 제한 도달 오류는 무엇을 의미합니까?

+++세션 제한에 도달했습니다.&quot;는 조직에 허용된 최대 쿼리 서비스 세션 수에 도달했음을 의미합니다. 조직의 Adobe Experience Platform 관리자에게 문의하십시오.
+++

### 쿼리 로그는 삭제된 데이터 집합에 대한 쿼리를 어떻게 처리합니까?

+++질의 서비스가 쿼리 내역을 삭제하지 않습니다. 즉, 삭제된 데이터 집합을 참조하는 모든 쿼리는 &quot;유효한 데이터 집합 없음&quot;을 결과적으로 반환합니다.
+++

### 쿼리의 메타데이터만 가져오려면 어떻게 해야 합니까?

+++답변 제로 행을 반환하는 쿼리를 실행하여 응답의 메타데이터만 가져올 수 있습니다. 이 예제 쿼리는 지정된 테이블의 메타데이터만 반환합니다.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### CTAS(Create Table As Select) 쿼리를 구체화하지 않고 빠르게 반복하려면 어떻게 해야 합니까?

+++답변 임시 테이블을 만들어 쿼리를 재현하기 전에 쿼리를 빠르게 반복 및 실험할 수 있습니다. 임시 테이블을 사용하여 쿼리가 작동하는지 확인할 수도 있습니다.

예를 들어 임시 테이블을 만들 수 있습니다.

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

그런 다음 임시 테이블을 다음과 같이 사용할 수 있습니다.

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

+++

### 시간대를 UTC 타임스탬프에서 및 로 변경하려면 어떻게 해야 합니까?

+++응답 Adobe Experience Platform은 UTC(Coordinated Universal Time) 타임스탬프 형식으로 데이터를 유지합니다. UTC 형식의 예는 다음과 같습니다 `2021-12-22T19:52:05Z`

Query Service는 지정된 타임스탬프를 UTC 형식으로 변환하기 위한 기본 제공 SQL 함수를 지원합니다. 둘 다 `to_utc_timestamp()` 그리고 `from_utc_timestamp()` 메서드는 두 가지 매개 변수를 사용합니다. timestamp 및 timezone.

| 매개 변수 | 설명 |
|-----------|---------------|
| 타임스탬프 | 타임스탬프는 UTC 형식 또는 간단한 형식으로 쓸 수 있습니다 `{year-month-day}` 형식 지정 시간을 제공하지 않으면 기본값은 지정된 날의 아침에 자정입니다. |
| 표준 시간대 | 시간대는 `{continent/city})` 형식 지정 이 코드에 있는 대로 인식된 시간대 코드 중 하나여야 합니다. [공용 도메인 TZ 데이터베이스](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### UTC 타임스탬프로 변환

다음 `to_utc_timestamp()` 메서드는 지정된 매개 변수를 해석하고 변환합니다 **로컬 시간대의 타임스탬프로** UTC 형식입니다. 예를 들어, 서울의 시간대는 대한민국 UTC/GMT +9시간입니다. 날짜 전용 타임스탬프를 제공하여 메서드는 오전 자정 기본값을 사용합니다. 타임스탬프 및 시간대는 해당 지역의 시간에서 로컬 지역의 UTC 타임스탬프로 변환됩니다.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

쿼리가 사용자의 현지 시간에 타임스탬프를 반환합니다. 이 경우 서울 전날인 3시 3분이 9시간 앞입니다.

```
2021-08-30 15:00:00
```

다른 예로, 주어진 타임스탬프가 `2021-07-14 12:40:00.0` 대상 `Asia/Seoul` 시간대, 반환된 UTC 타임스탬프는 `2021-07-14 03:40:00.0`

Query Service UI에 제공된 콘솔 출력은 사람이 읽을 수 있는 형식입니다.

```
8/30/2021, 3:00 PM
```

#### UTC 타임스탬프에서 변환

다음 `from_utc_timestamp()` 메서드는 지정된 매개 변수를 해석합니다 **로컬 시간대의 타임스탬프에서** 및 은 UTC 형식으로 원하는 영역의 상응하는 타임스탬프를 제공합니다. 아래 예에서 시간은 사용자의 로컬 시간대에서 오후 2시 40분입니다. 변수로 전달된 Seoul 시간대 는 로컬 시간보다 9시간 앞서 있습니다.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

쿼리는 매개 변수로 전달된 시간대의 UTC 형식 타임스탬프를 반환합니다. 결과는 쿼리를 실행한 시간대보다 9시간 빠릅니다.

```
8/31/2021, 11:40 PM
```

### 시계열 데이터를 필터링하려면 어떻게 해야 합니까?

+++답변 시계열 데이터를 사용하여 쿼리할 때 보다 정확한 분석을 위해 가능하면 타임스탬프 필터를 사용해야 합니다.

>[!NOTE]
>
> 날짜 문자열 **반드시** 형식을 사용해야 합니다. `yyyy-mm-ddTHH24:MM:SS`.

타임스탬프 필터 사용의 예는 다음과 같습니다.

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### 을 올바로 사용합니까? `CAST` 연산자를 사용하여 SQL 쿼리에서 내 타임스탬프를 변환하시겠습니까?

+++사용할 때 응답 `CAST` 연산자를 사용하여 타임스탬프를 변환하려면 날짜를 모두 포함해야 합니다 **및** 시간

예를 들어, 아래와 같이 시간 구성 요소가 없으면 오류가 발생합니다.

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

의 올바른 사용 `CAST` 연산자는 다음과 같습니다.

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### 와일드카드를 사용해야 합니까? 예: * 를 사용하여 데이터 세트에서 모든 행을 가져와야 합니까?

+++답변 쿼리 서비스를 **열 형식 저장소** 기존 행 기반 스토어 시스템 대신
+++

### 사용해야 합니까 `NOT IN` 내 SQL 쿼리에서?

+++ `NOT IN` 연산자는 다른 테이블이나 SQL 문에서 찾을 수 없는 행을 검색하는 데 종종 사용됩니다. 이 연산자는 성능 속도를 저하할 수 있으며 비교 중인 열이 수락되면 예기치 않은 결과를 반환할 수 있습니다 `NOT NULL`또는 레코드 수가 많습니다.

를 사용하는 대신 `NOT IN`, 다음 중 하나를 사용할 수 있습니다. `NOT EXISTS` 또는 `LEFT OUTER JOIN`.

예를 들어 다음 테이블을 생성한 경우

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

를 사용하는 경우 `NOT EXISTS` 연산자인 경우 `NOT IN` 다음 쿼리를 사용하여 연산자 사용:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

또는, `LEFT OUTER JOIN` 연산자인 경우 `NOT IN` 다음 쿼리를 사용하여 연산자 사용:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### UI에 표시된 것과 같은 이중 밑줄 이름을 사용하는 CTAS 쿼리를 사용하여 데이터 세트를 만들 수 있습니까? 예: `test_table_001`.

+++아니요. 이는 Query Service를 포함하여 모든 Adobe 서비스에 적용되는 Experience Platform 간에 의도적인 제한입니다. 밑줄이 두 개인 이름은 스키마와 데이터 세트 이름으로 사용할 수 있지만 데이터 집합에 대한 테이블 이름은 밑줄이 하나만 포함될 수 있습니다.
+++

### 한 번에 몇 개의 동시 쿼리를 실행할 수 있습니까?

+++응답 일괄 처리 쿼리가 백 엔드 작업으로 실행되므로 쿼리 동시성 제한은 없습니다. 그러나 쿼리 시간 제한 제한은 24시간으로 설정됩니다.
+++

### 쿼리 활동 및 상태를 볼 수 있는 활동 대시보드가 있습니까?

+++답변 쿼리 활동 및 상태를 확인하는 모니터링 및 경고 기능이 있습니다. 자세한 내용은 [Query Service 감사 로그 통합](./data-governance/audit-log-guide.md) 그리고 [쿼리 로그](./ui/overview.md#log) 문서 를 참조하십시오.
+++

### 업데이트를 롤백하는 방법이 있습니까? 예를 들어 Platform에 데이터를 다시 작성할 때 오류 또는 일부 계산을 다시 구성해야 하는 경우 해당 시나리오를 어떻게 처리해야 합니까?

+++답변 현재 Adobe에서는 이러한 방식으로 롤백 또는 업데이트를 지원하지 않습니다.
+++

### Adobe Experience Platform에서 쿼리를 어떻게 최적화합니까?

+++답변 시스템에 데이터베이스가 아니므로 인덱스가 없지만 데이터 저장소에 연결된 다른 최적화 기능이 있습니다. 다음 옵션을 사용하여 쿼리를 조정할 수 있습니다.

- 타임스탬프 데이터를 기반으로 하는 시간 기반 필터입니다.
- 구조체 데이터 형식에 대해 푸시다운이 최적화되었습니다.
- 어레이 및 맵 데이터 유형에 최적화된 비용 및 메모리 푸시다운.
- 스냅샷을 사용한 증분 처리
- 지속되는 데이터 형식입니다.
+++

### 로그인은 Query Service의 특정 측면으로 제한될 수 있습니까, 아니면 &quot;모두&quot; 솔루션입니까?

+++응답 쿼리 서비스는 &quot;모두 또는 없음&quot; 솔루션입니다. 부분 액세스를 제공할 수 없습니다.
+++

### Query Service에서 사용할 수 있는 데이터를 제한할 수 있습니까, 아니면 단순히 전체 Adobe Experience Platform 데이터 레이크에 액세스합니까?

+++예. 읽기 전용 액세스 권한이 있는 데이터 세트에 대한 쿼리를 제한할 수 있습니다.
+++

### Query Service에서 액세스할 수 있는 데이터를 제한하는 다른 옵션은 무엇입니까?

+++답변 액세스를 제한하는 세 가지 방법이 있습니다. 이러한 수정 사항은 다음과 같습니다.

- SELECT 전용 구문을 사용하고 데이터 세트에 읽기 전용 액세스 권한을 제공합니다. 또한 쿼리 관리 권한을 할당합니다.
- SELECT/INSERT/CREATE 문을 사용하고 데이터 세트에 쓰기 액세스 권한을 제공합니다. 또한 쿼리 관리 권한을 할당합니다.
- 위의 이전 제안 사항과 함께 통합 계정을 사용하고 쿼리 통합 권한을 지정하십시오.

+++

### Query Service에서 데이터를 반환하면 Platform에서 보호된 데이터를 반환하지 않았는지 확인하기 위해 실행할 수 있는 검사가 있습니까?

- 쿼리 서비스는 특성 기반 액세스 제어를 지원합니다. 열/리프 수준 및/또는 구조체 수준에서 데이터에 대한 액세스를 제한할 수 있습니다. 속성 기반 액세스 제어에 대한 자세한 내용은 설명서를 참조하십시오.

### 타사 클라이언트에 연결할 SSL 모드를 지정할 수 있습니까? 예를 들어 Power BI에서 &#39;verify-full&#39;을 사용할 수 있습니까?

+++예, SSL 모드가 지원됩니다. 자세한 내용은 [SSL 모드 설명서](./clients/ssl-modes.md) 사용 가능한 다양한 SSL 모드 및 보호 수준을 분류하기 위한 .
+++

### Power BI 클라이언트로부터 쿼리 서비스까지의 모든 연결에 TLS 1.2를 사용합니까?

+++예. 전송 중인 데이터는 항상 HTTPS를 준수합니다. 현재 지원되는 버전은 TLS1.2입니다.
+++

### 포트 80에서 연결된 경우 여전히 https를 사용합니까?

+++예, 포트 80에서 연결된 경우 여전히 SSL을 사용합니다. 포트 5432를 사용할 수도 있습니다.
+++

### 특정 연결에 대한 특정 데이터 세트 및 열에 대한 액세스를 제어할 수 있습니까? 어떻게 구성됩니까?

+++예, 구성된 경우 속성 기반 액세스 제어가 적용됩니다. 자세한 내용은 [속성 기반 액세스 제어 개요](../access-control/abac/overview.md) 추가 정보.
+++

### Query Service에서 &quot;INSERT OVERWRITE INTO&quot; 명령을 지원합니까?

+++아니요, Query Service는 &quot;INSERT OVERWRITE INTO&quot; 명령을 지원하지 않습니다.
+++

## 데이터 내보내기 {#exporting-data}

이 섹션에서는 데이터 및 제한 내보내기에 대한 정보를 제공합니다.

### 쿼리 처리 후 쿼리 서비스에서 데이터를 추출하고 결과를 CSV 파일에 저장하는 방법이 있습니까? {#export-csv}

+++예. 쿼리 서비스에서 데이터를 추출할 수 있으며 SQL 명령을 통해 결과를 CSV 형식으로 저장하는 옵션도 있습니다.

PSQL 클라이언트를 사용할 때 쿼리 결과를 저장하는 방법에는 두 가지가 있습니다. 를 사용할 수 있습니다 `COPY TO` 다음 형식을 사용하여 명령문을 만들거나 만듭니다.

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[의 사용에 대한 지침 `COPY TO` 명령](./sql/syntax.md#copy) 는 SQL 구문 참조 설명서에서 찾을 수 있습니다.
+++

### CTAS 쿼리를 통해 수집된 최종 데이터 세트의 컨텐츠를 추출할 수 있습니까(테라바이트와 같은 큰 데이터 양이 있다고 가정할 경우)?

+++아니요. 현재 수집된 데이터를 추출할 수 있는 기능이 없습니다.
+++

### Analytics 데이터 커넥터가 데이터를 반환하지 않는 이유는 무엇입니까?

+++답변 이 문제에 대한 일반적인 원인은 시간 필터 없이 시계열 데이터를 쿼리하는 것입니다. 예:

```sql
SELECT * FROM prod_table LIMIT 1;
```

다음 형식으로 작성해야 합니다.

```sql
SELECT * FROM prod_table
WHERE
timestamp >= to_timestamp('2022-07-22')
and timestamp < to_timestamp('2022-07-23');
```

+++

## 타사 도구 {#third-party-tools}

이 섹션에는 PSQL 및 Power BI과 같은 타사 도구 사용에 대한 정보가 포함되어 있습니다.

### 쿼리 서비스를 타사 도구에 연결할 수 있습니까?

+++예. 여러 타사 데스크탑 클라이언트를 Query Service에 연결할 수 있습니다. 다음 문서를 참조하십시오. [사용 가능한 클라이언트 및 Query Service에 연결하는 방법에 대한 전체 세부 정보](./clients/overview.md).
+++

### 타사 도구와 함께 계속 사용할 수 있도록 Query Service를 한 번 연결하는 방법이 있습니까?

+++예, 만료되지 않은 자격 증명을 1회 설정하여 타사 데스크탑 클라이언트를 Query Service에 연결할 수 있습니다. 만료되지 않은 자격 증명은 인증된 사용자가 생성하여 로컬 시스템에 자동으로 다운로드되는 JSON 파일에서 수신할 수 있습니다. 전체 [만료되지 않은 자격 증명을 만들고 다운로드하는 방법에 대한 지침](./ui/credentials.md#non-expiring-credentials) 는 설명서에서 찾을 수 있습니다.
+++

### 만료되지 않은 자격 증명이 작동하지 않는 이유는 무엇입니까?

+++답변 만료되지 않은 자격 증명의 값은 `technicalAccountID` 그리고 `credential` 구성 JSON 파일에서 가져옵니다. 암호 값은 다음 형식을 사용합니다. `{{technicalAccountId}:{credential}}`.
방법에 대한 자세한 내용은 설명서 를 참조하십시오 [자격 증명을 사용하여 외부 클라이언트에 연결](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### Query Service 편집기에 연결할 수 있는 타사 SQL 편집기는 무엇입니까?

+++PSQL 또는 [!DNL Postgres] 클라이언트 규격을 Query Service 편집기에 연결할 수 있습니다. 다음 문서를 참조하십시오. [클라이언트를 쿼리 서비스에 연결](./clients/overview.md) 사용 가능한 지침 목록
+++

### Power BI 도구를 Query Service에 연결할 수 있습니까?

+++예, Power BI을 Query Service에 연결할 수 있습니다. 다음 문서를 참조하십시오. [Power BI 데스크탑 앱을 Query Service에 연결하는 지침](./clients/power-bi.md).
+++

### Query Service에 연결할 때 대시보드를 로드하는 데 시간이 오래 걸리는 이유는 무엇입니까?

+++답변 시스템이 쿼리 서비스에 연결되면 대화형 또는 일괄 처리 엔진에 연결됩니다. 이렇게 하면 처리된 데이터를 반영하도록 로드 시간이 길어질 수 있습니다.

대시보드에 대한 응답 시간을 개선하려면 Query Service와 BI 도구 간에 Business Intelligence(BI) 서버를 캐싱 레이어로 구현해야 합니다. 일반적으로 대부분의 BI 도구에는 서버를 위한 추가 서비스가 있습니다.

캐시 서버 계층을 추가하는 목적은 쿼리 서비스에서 데이터를 캐시하고 이를 대시보드에 활용하여 응답 속도를 높이는 것입니다. 이는 실행되는 쿼리의 결과가 매일 BI 서버에 캐시되므로 가능합니다. 그런 다음 캐싱 서버는 동일한 쿼리를 가진 모든 사용자에게 이러한 결과를 제공하여 지연을 줄입니다. 이 설정에 대한 자세한 내용은 사용 중인 유틸리티 또는 타사 도구의 설명서를 참조하십시오.
+++

### pgAdmin 연결 도구를 사용하여 Query Service에 액세스할 수 있습니까?

+++아니요, pgAdmin 연결은 지원되지 않습니다. A [사용 가능한 타사 클라이언트 목록 및 Query Service에 연결하는 방법에 대한 지침](./clients/overview.md) 는 설명서에서 찾을 수 있습니다.
+++

## PostgreSQL API 오류 {#postgresql-api-errors}

다음 표에서는 PSQL 오류 코드 및 가능한 원인을 제공합니다.

| 오류 코드 | 연결 상태 | 설명 | 가능한 원인 |
|------------|---------------------------|-------------|----------------|
| **08P01** | 해당 없음 | 지원되지 않는 메시지 유형 | 지원되지 않는 메시지 유형 |
| **28P01** | 시작 - 인증 | 잘못된 암호 | 잘못된 인증 토큰 |
| **28000** | 시작 - 인증 | 잘못된 인증 유형 | 권한 부여 형식이 잘못되었습니다. 반드시 `AuthenticationCleartextPassword`. |
| **42P12** | 시작 - 인증 | 테이블을 찾을 수 없습니다. | 사용할 테이블을 찾을 수 없습니다. |
| **42601** | 쿼리 | 구문 오류 | 명령 또는 구문 오류가 잘못되었습니다. |
| **42P01** | 쿼리 | 테이블을 찾을 수 없음 | 쿼리에 지정된 테이블을 찾을 수 없습니다 |
| **42P07** | 쿼리 | 테이블이 존재함 | 이름이 같은 테이블이 이미 있습니다(CREATE TABLE). |
| **53400** | 쿼리 | LIMIT가 최대값을 초과합니다. | 사용자가 100,000보다 큰 LIMIT 절을 지정했습니다. |
| **53400** | 쿼리 | 문 시간 초과 | 제출된 라이브 명령문은 최대 10분 이상 걸렸습니다 |
| **58000** | 쿼리 | 시스템 오류 | 내부 시스템 장애 |
| **0A000** | 쿼리/명령 | 지원되지 않음 | 쿼리/명령의 기능/기능은 지원되지 않습니다 |
| **42501** | 테이블 쿼리 삭제 | 쿼리 서비스에서 만들지 않은 테이블 삭제 | 삭제되는 테이블이 `CREATE TABLE` statement |
| **42501** | 테이블 쿼리 삭제 | 인증된 사용자가 만들지 않은 테이블 | 삭제되는 테이블은 현재 로그인한 사용자가 만들지 않았습니다 |
| **42P01** | 테이블 쿼리 삭제 | 테이블을 찾을 수 없음 | 쿼리에 지정된 테이블을 찾을 수 없습니다 |
| **42P12** | 테이블 쿼리 삭제 | 에 대한 테이블을 찾을 수 없습니다. `dbName`: 확인 `dbName` | 현재 데이터베이스에 테이블이 없습니다. |

### 테이블에서 history_meta() 메서드를 사용할 때 58000 오류 코드가 표시되는 이유는 무엇입니까?

+++ `history_meta()` 메서드는 데이터 집합에서 스냅샷에 액세스하는 데 사용됩니다. 이전에는 ADLS(Azure Data Lake Storage)의 빈 데이터 집합에 대해 쿼리를 실행하려는 경우 데이터 세트가 없다는 58000 오류 코드가 표시됩니다. 이전 시스템 오류의 예가 아래에 표시됩니다.

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

쿼리에 대한 반환 값이 없으므로 이 오류가 발생했습니다. 이제 이 동작은 다음 메시지를 반환하도록 수정되었습니다.

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## REST API 오류 {#rest-api-errors}

다음 표는 HTTP 오류 코드 및 가능한 원인을 제공합니다.

| HTTP 상태 코드 | 설명 | 가능한 원인 |
|------------------|-----------------------|----------------------------|
| 400 | 잘못된 요청 | 잘못된 쿼리 또는 잘못된 쿼리 |
| 401 | 인증 실패 | 잘못된 인증 토큰 |
| 500 | 내부 서버 오류 | 내부 시스템 장애 |
