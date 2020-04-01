---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 샘플 쿼리
topic: queries
translation-type: tm+mt
source-git-commit: 33282b1c8ab1129344bd4d7054e86fed75e7b899

---


# Adobe Target 데이터에 대한 샘플 쿼리

Adobe Target의 데이터는 Experience Event XDM 스키마로 변환되고 데이터 세트로 Experience Platform로 인제스트됩니다. 이 데이터를 사용하는 쿼리 서비스에 대해 많은 사용 사례가 있으며 다음 샘플 쿼리는 Adobe Target 데이터 세트와 함께 작동해야 합니다.

>[!NOTE]
>다음 예에서는 평가하려는 데이터 세트, 변수 또는 기간을 기반으로 쿼리에 대해 예상되는 매개 변수를 채우려면 SQL을 편집해야 합니다. SQL에 있는 모든 위치에 매개 변수를 `{ }` 제공합니다.

## 플랫폼의 Target 데이터 소스에 대한 표준 데이터 세트 이름:

Adobe Target 경험 이벤트(친숙한 이름) <br>`adobe_target_experience_events` (쿼리에 사용할 이름)

## 고급 부분 XDM 필드 매핑

의 `[ ]` 사용은

| 이름 | XDM 필드 | 참고 |
| ---- | --------- | ----- |
| mboxName | `_experience.target.mboxname` |  |
| 활동 ID | `_experience.target.activities.activityID` |  |
| 경험 ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` |  |
| 세그먼트 ID | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` |  |
| 이벤트 범위 | `_experience.target.activities[].activityEvents[].eventScope` | 새 방문자 및 방문 추적 |
| 단계 ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | 캠페인에 대한 사용자 지정 단계 ID |
| 가격 합계 | `commerce.order.priceTotal` |  |

## 지정된 날의 시간별 활동 수

```sql
SELECT
  Hour,
  ActivityID,
  COUNT(ActivityID) AS Instances
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities.activityID) AS ActivityID
  FROM adobe_target_experience_events
  WHERE
    _ACP_YEAR = {target_year} AND 
    _ACP_MONTH = {target_month} AND 
    _ACP_DAY = {target_day} AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

## 지정된 날의 특정 활동에 대한 시간별 세부 사항

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
  _ACP_YEAR = {target_year} AND 
  _ACP_MONTH = {target_month} AND 
  _ACP_DAY = {target_day} AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

## 지정된 날의 특정 활동에 대한 경험 ID

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      _ACP_YEAR = {target_year} AND 
      _ACP_MONTH = {target_month} AND 
      _ACP_DAY = {target_day} AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

## 지정된 날의 활동 ID당 인스턴스별로 이벤트 범위(방문자, 방문, 노출) 목록 반환

```sql
SELECT
  Day,
  Activities.activityID,
  EventScope,
  COUNT(EventScope) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents.eventScope) AS EventScope
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      _ACP_YEAR = {target_year} AND 
      _ACP_MONTH = {target_month} AND 
      _ACP_DAY = {target_day} AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

## 지정된 날짜에 대한 방문자 수, 방문 횟수, 활동당 노출 횟수

```sql
SELECT
  Hour,
  Activities.activityid,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visitor' ) THEN 1 END) as Visitors,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visit' ) THEN 1 END) as Visits,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'impression' ) THEN 1 END) as Impressions
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities) AS Activities
  FROM adobe_target_experience_events
  WHERE
    _ACP_YEAR = {target_year} AND 
    _ACP_MONTH = {target_month} AND 
    _ACP_DAY = {target_day} AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

## 지정된 날짜에 대한 재방문자, 방문, 경험 ID, 세그먼트 ID 및 EventScope에 대한 노출 횟수

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  SegmentID._id,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visitor' THEN 1 END) as Visitors,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visit' THEN 1 END) as Visits,
  SUM(CASE WHEN ActivityEvent.eventScope = 'impression' THEN 1 END) as Impressions
FROM
(
  SELECT
    Day,
    Activities,
    ActivityEvent,
    ActivityEvent._experience.target.activity.activityevent.context.experienceID AS ExperienceID,
    EXPLODE(ActivityEvent.segmentEvents.segmentID) AS SegmentID
  FROM
  (
    SELECT
      Day,
      Activities,
      EXPLODE(Activities.activityEvents) AS ActivityEvent
    FROM
    (
      SELECT
        date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
        EXPLODE(_experience.target.activities) AS Activities
      FROM adobe_target_experience_events
      WHERE 
        _ACP_YEAR = {target_year} AND
        _ACP_MONTH = {target_month} AND 
        _ACP_DAY = {target_day} AND 
        _experience.target.activities IS NOT NULL
      LIMIT 1000000
    )
    LIMIT 1000000
  )
  LIMIT 1000000
)
GROUP BY Day, Activities.activityID, ExperienceID, SegmentID._id
ORDER BY Day DESC, Activities.activityID, ExperienceID ASC, SegmentID._id ASC, Visitors DESC
LIMIT 20
```

## 지정된 날짜에 대한 mbox 이름 및 레코드 수 반환

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  _ACP_YEAR= {target_year} AND 
  _ACP_MONTH= {target_month} AND 
  _ACP_DAY= {target_day}
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
