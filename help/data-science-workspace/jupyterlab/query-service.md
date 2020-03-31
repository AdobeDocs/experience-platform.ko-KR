---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Jupiter 전자 필기장의 쿼리 서비스
topic: Tutorial
translation-type: tm+mt
source-git-commit: d0596dc3c744e192c4d2ad04d6365846a0115371

---


# Jupiter 전자 필기장의 쿼리 서비스

Adobe Experience Platform을 사용하면 Query Service를 JupiterLab에 표준 기능으로 통합하여 데이터 과학 작업 공간에서 구조화된 쿼리 언어(SQL)를 사용할 수 있습니다.

이 자습서에서는 Adobe Analytics 데이터를 탐색, 변환 및 분석하는 일반적인 사용 사례를 위한 다음 샘플 SQL 쿼리를 보여 줍니다.

- [JupiterLab 및 쿼리 서비스 액세스](#access-jupyterlab-and-query-service)
- [데이터 쿼리](#query-your-data)
   - [시간별 방문자 수](#hourly-visitor-count)
   - [시간별 활동 수](#hourly-activity-count)
   - [방문자 세션당 이벤트 수](#number-of-events-per-visitor-session)
   - [특정 날짜의 인기 페이지](#popular-pages-for-a-given-day)
   - [지정된 날짜에 활성 사용자](#active-users-for-a-given-day)
   - [사용자 활동별 활성 도시](#active-cities-by-user-activity)

## 시작하기

이 튜토리얼을 시작하기 전에 다음 사전 요구 사항을 충족해야 합니다.

- Adobe Experience Platform 이용 Experience Platform에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자에게 문의하십시오.

- Adobe Analytics 데이터 세트

- 이 튜토리얼에서 사용되는 다음 주요 개념에 대한 작업 설명입니다.
   - [XDM(Experience Data Model) 및 XDM 시스템](../../xdm/home.md)
   - [쿼리 서비스](../../query-service/home.md)
   - [쿼리 서비스 SQL 구문](../../query-service/sql/overview.md)
   - Adobe Analytics

## JupiterLab 및 쿼리 서비스 액세스

1. 경험 [플랫폼에서](https://platform.adobe.com)왼쪽 탐색 **열에서** 모델로 이동합니다. 상단 **헤더에서** 공책을 클릭하여 JupiterLab을 엽니다. JupiterLab이 로드될 때까지 잠시 기다려 주십시오.

   ![](../images/jupyterlab/query/notebook_ui.png)

   > [!NOTE] 새 실행 프로그램 탭이 자동으로 나타나지 않으면 파일 > 새 실행 **관리자를 클릭하여 새 시작 탭을 엽니다**.

2. 론처 탭에서 Python **3** 환경의 빈 아이콘을 클릭하여 빈 전자 필기장을 엽니다.

   ![](../images/jupyterlab/query/blank_notebook.png)

   > [!NOTE] 현재 Python 3은 전자 필기장에서 쿼리 서비스에 대해 지원되는 유일한 환경입니다.

3. 왼쪽 선택 레일에서 데이터 **아이콘을 클릭하고** 데이터 집합 **디렉터리를 두 번 클릭하여** 모든 데이터 집합을 나열합니다.

   ![](../images/jupyterlab/query/dataset.png)

4. Adobe Analytics 데이터 세트를 찾아 목록을 마우스 오른쪽 버튼으로 클릭한 다음 노트북에서 **데이터** 쿼리를 클릭하여 빈 노트북에서 SQL 쿼리를 생성합니다.

5. 함수가 들어 있는 첫 번째 생성된 셀을 `qs_connect()` 클릭하고 재생 단추를 클릭하여 실행합니다. 이 함수는 전자 필기장 인스턴스와 쿼리 서비스 간에 연결을 만듭니다.

   ![](../images/jupyterlab/query/execute.png)

6. 두 번째 생성된 SQL 쿼리에서 Adobe Analytics 데이터 집합 이름을 복사하면 그 다음 값이 `FROM`됩니다.

   ![](../images/jupyterlab/query/dataset_name.png)

7. 단추를 클릭하여 새 전자 필기장 셀을 **삽입합니다** .

   ![](../images/jupyterlab/query/insert_cell.gif)

8. 새 셀에서 다음 가져오기 문을 복사, 붙여넣기 및 실행합니다. 다음 명령문은 데이터를 시각화하는 데 사용됩니다.

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. 그런 다음 다음 다음 변수를 복사하여 새 셀에 붙여 넣습니다. 필요에 따라 값을 수정한 다음 실행합니다.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table` :Adobe Analytics 데이터 세트 이름입니다.
   - `target_year` :대상 데이터가 있는 특정 연도입니다.
   - `target_month` :대상이 있는 특정 달
   - `target_day` :타겟 데이터의 특정 요일.
   >[!NOTE] 이러한 값은 언제든지 변경할 수 있습니다. 그렇게 할 때는 변경 사항을 적용할 변수 셀을 실행해야 합니다.

## 데이터 쿼리

개별 전자 필기장 셀에 다음 SQL 쿼리를 입력합니다. 셀을 클릭한 다음 **재생** 단추를 클릭하여 쿼리를 실행합니다. 성공적인 쿼리 결과 또는 오류 로그가 실행된 셀 아래에 표시됩니다.

전자 필기장이 장기간 비활성 상태인 경우 전자 필기장과 쿼리 서비스 간의 연결이 끊길 수 있습니다. 이러한 경우 오른쪽 상단 모서리에 있는 전원 **버튼을** 클릭하여 JupiterLab을 다시 시작합니다.

![](../images/jupyterlab/query/restart_button.png)

전자 필기장 커널은 재설정되지만 셀들은 그대로 유지되며, **모든** 셀을 다시 실행하여 중단된 부분을 계속 진행합니다.

### 시간별 방문자 수

다음 쿼리는 지정된 날짜에 대한 시간별 방문자 수를 반환합니다.

#### 쿼리

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

위의 쿼리에서 `_acp_year` 절의 `WHERE` 대상이 의 값으로 `target_year`설정됩니다. 중괄호(`{}`)에 포함시켜 SQL 쿼리에 변수를 포함시킵니다.

쿼리의 첫 번째 행에는 선택적 변수가 포함되어 `hourly_visitor`있습니다. 쿼리 결과는 이 변수에 Pendans 데이터 프레임으로 저장됩니다. 결과를 데이터 프레임에 저장하면 나중에 원하는 Python 패키지를 사용하여 쿼리 결과를 시각화할 수 있습니다. 새 셀에서 다음 Python 코드를 실행하여 막대 그래프를 생성합니다.

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

### 시간별 활동 수

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
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

위의 쿼리를 실행하면 결과가 데이터 `hourly_actions` 프레임으로 저장됩니다. 새 셀에서 다음 함수를 실행하여 결과를 미리 봅니다.

```python
hourly_actions.head()
```

위의 쿼리는 WHERE 절의 논리 연산자를 사용하여 지정된 날짜 범위에 대한 시간별 작업 개수를 반환하도록 수정할 **수** 있습니다.

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

수정된 쿼리를 실행하면 결과가 데이터 `hourly_actions_date_range` 프레임으로 저장됩니다. 새 셀에서 다음 함수를 실행하여 결과를 미리 봅니다.

```python
hourly_actions_date_rage.head()
```

### 방문자 세션당 이벤트 수

다음 쿼리는 지정된 날짜에 대해 방문자 세션당 이벤트 수를 반환합니다.

#### 쿼리 <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

다음 Python 코드를 실행하여 방문 세션당 이벤트 수에 대한 히스토그램을 생성합니다.

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

### 특정 날짜의 인기 페이지

다음 쿼리는 지정된 날짜에 대해 가장 많이 사용되는 10개의 페이지를 반환합니다.

#### 쿼리 <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### 지정된 날짜에 활성 사용자

다음 쿼리는 지정된 날짜에 대해 가장 활성화된 10명의 사용자를 반환합니다.

#### 쿼리 <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### 사용자 활동별 활성 도시

다음 쿼리는 지정된 날짜의 대부분의 사용자 활동을 생성하는 10개 도시를 반환합니다.

#### 쿼리 <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## 다음 단계 <!-- omit in toc -->

이 자습서에서는 Jupiter 전자 필기장에서 쿼리 서비스를 활용하는 몇 가지 샘플 사용 사례를 설명했습니다. Jupiter [Notebook을 사용하여 데이터 분석](./analyze-your-data.md) 자습서에 따라 데이터 액세스 SDK를 사용하여 유사한 작업이 수행되는 방식을 확인할 수 있습니다.