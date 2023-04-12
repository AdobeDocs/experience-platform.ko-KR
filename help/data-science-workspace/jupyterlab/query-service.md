---
keywords: Experience Platform;JupiterLab;노트북;데이터 과학 작업 공간;인기 항목;쿼리 서비스
solution: Experience Platform
title: Jupiter 전자 필기장의 쿼리 서비스
type: Tutorial
description: Adobe Experience Platform에서는 표준 기능으로 Query Service를 JupiterLab에 통합하여 데이터 과학 작업 공간에서 SQL(구조화된 쿼리 언어)을 사용할 수 있습니다. 이 자습서에서는 Adobe Analytics 데이터를 탐색, 변환 및 분석하는 일반적인 사용 사례에 대한 샘플 SQL 쿼리를 보여줍니다.
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---

# Jupiter 전자 필기장의 쿼리 서비스

[!DNL Adobe Experience Platform] 에서는 구조화된 쿼리 언어(SQL)를 사용할 수 있습니다 [!DNL Data Science Workspace] 통합 [!DNL Query Service] 변환 [!DNL JupyterLab] 를 표준 기능으로 사용합니다.

이 자습서에서는 일반적인 사용 사례를 탐색, 변환 및 분석하는 샘플 SQL 쿼리를 보여 줍니다 [!DNL Adobe Analytics] 데이터.

## 시작하기

이 자습서를 시작하기 전에 다음 전제 조건이 있어야 합니다.

- 액세스 권한 [!DNL Adobe Experience Platform]. 의 조직에 액세스할 수 없는 경우 [!DNL Experience Platform]을(를) 진행하기 전에 시스템 관리자에게 문의하십시오

- An [!DNL Adobe Analytics] 데이터 세트

- 이 자습서에서 사용되는 다음 주요 개념에 대한 작업 이해:
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## 액세스 [!DNL JupyterLab] 및 [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. in [[!DNL Experience Platform]](https://platform.adobe.com), 다음 위치로 이동합니다. **[!UICONTROL 노트북]** 왼쪽 탐색 열 JupiterLab이 로드될 때까지 잠시 기다려 주십시오.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >새 시작 관리자 탭이 자동으로 나타나지 않으면 을 클릭하여 새 시작 관리자 탭을 엽니다 **[!UICONTROL 파일]** 을(를) 선택합니다. **[!UICONTROL 새 시작 관리자]**.

2. 시작 관리자 탭에서 **[!UICONTROL 비어 있음]** 아이콘을 클릭하여 빈 전자 필기장을 엽니다.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >현재 Python 3은 전자 필기장에서 쿼리 서비스에 대해 지원되는 유일한 환경입니다.

3. 왼쪽 선택 레일에서 **[!UICONTROL 데이터]** 아이콘을 클릭하고 두 번 클릭합니다 **[!UICONTROL 데이터 세트]** 모든 데이터 세트를 나열할 디렉토리입니다.

   ![](../images/jupyterlab/query/dataset.png)

4. 찾기 [!DNL Adobe Analytics] 목록을 탐색하고 마우스 오른쪽 단추로 클릭할 데이터 세트 **[!UICONTROL 전자 필기장의 쿼리 데이터]** 빈 전자 필기장에서 SQL 쿼리를 생성하려면

5. 함수를 포함하는 첫 번째 생성된 셀을 클릭합니다 `qs_connect()` 재생 버튼을 클릭하여 실행합니다. 이 함수는 전자 필기장 인스턴스와 [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. 아래에 복사 [!DNL Adobe Analytics] 두 번째 생성된 SQL 쿼리의 데이터 세트 이름입니다. 다음 값이 됩니다 `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. 을 클릭하여 새 전자 필기장 셀을 삽입합니다. **+** 버튼을 클릭합니다.

   ![](../images/jupyterlab/query/insert_cell.gif)

8. 새 셀에서 다음 가져오기 구문을 복사, 붙여넣기 및 실행합니다. 다음 문은 데이터를 시각화하는 데 사용됩니다.

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. 그런 다음 다음 다음 변수를 복사하여 새 셀에 붙여넣습니다. 필요에 따라 값을 수정한 다음 실행합니다.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`: 사용자 이름 [!DNL Adobe Analytics] 데이터 세트.
   - `target_year`: 대상 데이터가 시작되는 특정 연도입니다.
   - `target_month`: 대상이 되는 특정 월입니다.
   - `target_day`: 대상 데이터가 시작되는 특정 날짜입니다.

   >[!NOTE]
   >
   >이러한 값은 언제든지 변경할 수 있습니다. 그렇게 할 때 적용할 변경 사항에 대한 변수 셀을 실행해야 합니다.

## 데이터 쿼리 {#query-your-data}

개별 전자 필기장 셀에 다음 SQL 쿼리를 입력합니다. 셀에서 선택한 다음 을(를) 선택하여 쿼리를 실행합니다 **[!UICONTROL play]** 버튼을 클릭합니다. 성공적인 쿼리 결과 또는 오류 로그가 실행된 셀 아래에 표시됩니다.

일정 기간 동안 노트북이 비활성 상태이면 노트북과 노트북의 연결이 [!DNL Query Service] 깨질 수 있습니다. 이러한 경우 를 다시 시작합니다 [!DNL JupyterLab] 다음을 선택하여 **다시 시작** 버튼 ![다시 시작 단추](../images/jupyterlab/user-guide/restart_button.png) 전원 단추 옆에 있는 오른쪽 위 모서리에 있습니다.

전자 필기장 커널이 재설정되지만 셀이 남아 있게 되고, 모든 셀을 다시 실행하여 사용자가 떠난 위치를 계속합니다.

### 시간별 방문자 수 {#hourly-visitor-count}

다음 쿼리는 지정된 날짜에 대한 시간별 방문자 수를 반환합니다.

#### 쿼리

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

위의 쿼리에서 `WHERE` 절은 의 값으로 설정되어 있습니다. `target_year`. 중괄호(`{}`).

쿼리의 첫 번째 줄에는 선택적 변수가 포함되어 있습니다 `hourly_visitor`. 쿼리 결과는 이 변수에 Pendder 데이터 프레임으로 저장됩니다. 결과를 데이터 프레임에 저장하여 나중에 원하는 결과를 사용하여 쿼리 결과를 시각화할 수 있습니다 [!DNL Python] 패키지. 다음을 실행합니다 [!DNL Python] 막대 그래프를 생성하기 위한 새 셀의 코드:

```python
trace = go.Bar(
    x = hourly_visitor['Hour'],
    y = hourly_visitor['Visit_Count'],
    name = "Visitor Count"
)
layout = go.Layout(
    title = 'Visit Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)
fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

### 시간별 활동 수 {#hourly-activity-count}

다음 쿼리는 지정된 날짜에 대한 시간별 작업 수를 반환합니다.

#### 쿼리 <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

위의 쿼리를 실행하면 결과를 `hourly_actions` 를 데이터 프레임으로 사용 새 셀에서 다음 함수를 실행하여 결과를 미리 봅니다.

```python
hourly_actions.head()
```

위의 쿼리를 수정하여 **위치** 절:

#### 쿼리 <!-- omit in toc -->

```sql
%%read_sql hourly_actions_date_range -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  timestamp >= TO_TIMESTAMP('2019-06-01 00', 'YYYY-MM-DD HH')
       AND timestamp <= TO_TIMESTAMP('2019-06-02 23', 'YYYY-MM-DD HH')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

수정된 쿼리를 실행하면 결과를 `hourly_actions_date_range` 를 데이터 프레임으로 사용 새 셀에서 다음 함수를 실행하여 결과를 미리 봅니다.

```python
hourly_actions_date_rage.head()
```

### 방문자 세션당 이벤트 수 {#number-of-events-per-visitor-session}

다음 쿼리는 지정된 날짜에 대한 방문자 세션당 이벤트 수를 반환합니다.

#### 쿼리 <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

다음을 실행합니다 [!DNL Python] 코드 : 방문당 세션 수의 이벤트에 대한 히스토그램을 생성합니다.

```python
data = [go.Histogram(x = events_per_session['Count'])]

layout = go.Layout(
    title = 'Histogram of Number of Events per Visit Session',
    xaxis = dict(title = 'Number of Events'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = data, layout = layout)
iplot(fig)
```

### 특정 날짜에 대한 방문 빈도가 높은 페이지 {#popular-pages-for-a-given-day}

다음 쿼리는 지정된 날짜에 대해 가장 방문 빈도가 높은 10개의 페이지를 반환합니다.

#### 쿼리 <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### 지정된 날의 활성 사용자 {#active-users-for-a-given-day}

다음 쿼리는 지정된 날짜에 대해 10명의 가장 활성 사용자를 반환합니다.

#### 쿼리 <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### 사용자 활동별 활성 도시 {#active-cities-by-user-activity}

다음 쿼리는 지정된 날짜에 대한 대부분의 사용자 활동을 생성하는 10개 도시를 반환합니다.

#### 쿼리 <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## 다음 단계

이 자습서에서는 을 활용하기 위한 몇 가지 샘플 사용 사례를 보여줍니다 [!DNL Query Service] in [!DNL Jupyter] 노트북. 다음을 수행합니다 [Jupiter 노트북을 사용하여 데이터 분석](./analyze-your-data.md) 데이터 액세스 SDK를 사용하여 유사한 작업을 수행하는 방법을 보기 위한 자습서입니다.
