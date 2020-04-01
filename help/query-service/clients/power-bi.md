---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Power BI와 연결
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Power BI(PC)와 연결

PC 사용자는 https://powerbi.microsoft.com/en-us/desktop/에서 Power BI를 설치할 수 [있습니다](https://powerbi.microsoft.com/en-us/desktop/).

## Power Bi 설정

Power BI를 설치한 후 PostgreSQL 커넥터를 지원하는 데 필요한 구성 요소를 설정해야 합니다. 다음 단계를 따르십시오.

- PowerBI에 연결하는 공식 방법인 PostgreSQL용 .NET 드라이버 패키지를 찾아 설치합니다. `npgsql`

- v4.0.10을 선택합니다(최신 버전이 있으면 오류가 발생합니다).

- [사용자 정의 설정] 화면의 &quot;Npgsql GAC 설치 설치&quot;에서 **[로컬 하드 드라이브에**&#x200B;설치됨]을 선택합니다. GAC를 설치하지 않으면 나중에 Power BI가 실패합니다.

- Windows를 다시 시작합니다.

- PowerBI Desktop 평가 버전을 찾습니다.

## 쿼리 서비스에 Power BI 연결

이러한 준비 단계를 수행한 후 Power BI를 쿼리 서비스에 연결할 수 있습니다.

- Power BI를 엽니다.

- 상단 **메뉴** 리본에서 데이터 가져오기를 클릭합니다.

- PostgreSQL **데이터베이스를**&#x200B;선택한 다음 Connect를 **클릭합니다**.

- 서버 및 데이터베이스의 값을 입력합니다. **서버가** 접속 세부 사항 아래에 있는 호스트입니다. 프로덕션의 경우 호스트 문자열 `:80` 끝에 포트를 추가합니다. **데이터베이스는** &quot;모두&quot; 또는 데이터 집합 테이블 이름을 사용할 수 있습니다. (CTAS 파생 데이터 집합 중 하나를 시도하십시오.)

- 고급 **옵션을**&#x200B;클릭한 다음 관계 열 **포함의 선택을 취소합니다**. 전체 계층을 **사용하여**&#x200B;탐색하지 마십시오.

- *(선택 사항이지만 데이터베이스에 대해 &quot;all&quot;을 선언하는 경우 권장)* SQL 문을 입력합니다.

>[!NOTE] SQL 문이 제공되지 않으면 Power BI가 데이터베이스의 모든 테이블을 미리 봅니다. 계층 데이터의 경우 사용자 지정 SQL 문을 사용해야 합니다. 테이블 스키마가 평평하면 사용자 지정 SQL 문과 함께 또는 없이 작동합니다. 복합 형식은 아직 Power BI에서 지원되지 않습니다. 복합 형식에서 원시 형식을 가져오려면 SQL 문을 작성하여 파생해야 합니다.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- DirectQuery **또는 가져오기** 모드를 **선택합니다** . 가져오기 **모드에서** 데이터를 Power BI로 가져옵니다. DirectQuery **모드에서는** 모든 쿼리가 실행을 위해 쿼리 서비스로 전송됩니다.

- **확인**&#x200B;을 클릭합니다. 이제 Power BI는 쿼리 서비스에 연결하여 오류가 없을 경우 미리 보기를 생성합니다. 미리 보기 렌더링 숫자 열에 알려진 문제가 있습니다. 다음 단계로 진행합니다.

- 로드를 **클릭하여** 데이터 세트를 Power BI로 가져옵니다.
