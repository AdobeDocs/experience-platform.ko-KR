---
keywords: Experience Platform;home;popular topics;query service;Query Service;sample queries;sample query;adobe target
solution: Experience Platform
title: Adobe Target 데이터에 대한 샘플 쿼리
topic-legacy: queries
description: Adobe Target의 데이터는 Experience Event XDM 스키마로 변환되고 데이터 세트로 Experience Platform으로 수집됩니다. 이 문서에는 Adobe Target 데이터 집합에 쿼리 서비스를 사용하기 위한 샘플 쿼리가 포함되어 있습니다.
exl-id: 0ab3cd6e-25ed-43dc-b8f0-a2b71621ae50
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 1%

---

# Adobe Target 데이터에 대한 샘플 쿼리

Adobe Target의 데이터는 Experience Event XDM 스키마로 변환되고 데이터 세트로 Adobe Experience Platform으로 수집됩니다. 이 데이터를 사용하는 Adobe Experience Platform Query Service에 대한 사용 사례가 많이 있으며 다음 샘플 쿼리는 Adobe Target 데이터 세트에서 작동해야 합니다.

Experience Platform에서 자동 생성된 데이터 세트의 이름은 &quot;Adobe Target Experience Events&quot;입니다. 쿼리와 함께 이 데이터 세트를 사용할 때는 `adobe_target_experience_events` 이름을 사용해야 합니다.

## 상위 레벨 부분 XDM 필드 매핑

다음 목록은 해당 XDM 필드에 매핑되는 Target 필드를 보여줍니다.

>[!NOTE]
>
> XDM 필드 내에서 `[ ]`을 사용하면 배열이 표시됩니다.

- mboxName:`_experience.target.mboxname`
- 활동 ID: `_experience.target.activities.activityID`
- 경험 ID: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID`
- 세그먼트 ID:`_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id`
- 이벤트 범위:`_experience.target.activities[].activityEvents[].eventScope`
   - 이 필드는 새 방문자 및 방문을 추적합니다.
- 단계 ID:`_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID`
   - 이 필드는 Adobe Campaign의 사용자 지정 단계 ID입니다.
- 가격 합계:`commerce.order.priceTotal`

## 샘플 쿼리

다음 쿼리는 Adobe Target에서 일반적으로 사용되는 쿼리의 예를 보여줍니다.

다음 예제에서는 평가할 데이터 세트, 변수 또는 기간을 기준으로 쿼리의 예상 매개 변수를 채우도록 SQL을 편집해야 합니다. SQL에 `{ }`이 표시되는 모든 위치에서 매개 변수를 제공합니다.

### 지정된 날짜에 대한 시간별 활동 수

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
  WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

### 지정된 일의 특정 활동에 대한 시간별 세부 사항

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

### 특정 날짜에 대한 특정 활동에 대한 경험 ID

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
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### 특정 날짜에 대한 활동 ID당 인스턴스별로 이벤트 범위(방문자, 방문, 노출 수) 목록 반환

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
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

### 지정된 날짜에 대한 방문자, 방문, 활동당 노출 횟수 재방문 횟수

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
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

### 주어진 날에 대한 경험 ID, 세그먼트 ID 및 EventScope에 대한 재방문자, 방문, 노출 횟수

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
        TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
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

### 지정된 날짜에 대한 mbox 이름 및 레코드 수 반환

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
