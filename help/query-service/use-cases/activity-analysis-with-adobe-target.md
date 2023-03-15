---
title: Adobe Target을 사용한 Activity Analysis
description: 이 문서에서는 쿼리 서비스를 사용하여 Adobe Target 데이터로 만든 데이터 세트에서 실행 가능한 통찰력을 만드는 방법을 설명합니다.
exl-id: a5181ee2-1e1c-405d-8dfe-5a32c28ac9f1
source-git-commit: d573c01a0aa9989f581796a0be4aec6904ffc569
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Adobe Target을 사용한 활동 분석

Adobe Experience Platform을 사용하면 XDM(Experience Data Model) 필드를 사용하여 Adobe Target에서 데이터를 수집하여 쿼리 서비스에 사용할 데이터 세트를 만들 수 있습니다. Adobe Target은 콘텐츠를 사용자 정의하고 사용자 경험을 개인화하기 위해 설계되었으므로, 이러한 데이터 세트에서 실행되는 쿼리는 SQL을 통해 사용자 활동을 분석하여 고도로 개인화되고 집중된 통찰력을 얻을 수 있습니다.

이 문서에서는 고객의 동작 및 특성에 따라 일반적인 사용 사례를 보여 주는 다양한 샘플 SQL 쿼리를 제공합니다.

## 시작하기

다음 각 사용 사례에 대해 사용자 정의할 템플릿으로 매개 변수가 있는 SQL 쿼리 예제가 제공됩니다. 표시되는 모든 위치에 매개 변수를 제공합니다. `{ }` 평가에 관심이 있는 SQL 예제에서 다음을 수행합니다.

## 높은 수준 부분 XDM 필드 매핑

다음 표에는 공통 Target 필드와 매핑되는 해당 XDM 필드가 나와 있습니다.

>[!NOTE]
>
>사용 `[ ]` xdm 필드 내에서는 배열을 나타냅니다.

| Target 필드 이름 | XDM 필드 이름 | 참고 |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | 해당 없음 |
| 활동 ID | `_experience.target.activities.activityID` | 해당 없음 |
| 경험 ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | 해당 없음 |
| 세그먼트 ID | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | 해당 없음 |
| 이벤트 범위 | `_experience.target.activities[].activityEvents[].eventScope` | 이 필드는 새 방문자 및 방문을 추적합니다. |
| 단계 ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | 이 필드는 Adobe Campaign에 대한 사용자 지정 단계 ID입니다. |
| 가격 합계 | commerce.order.priceTotal | 해당 없음 |

>[!IMPORTANT]
>
>Target 데이터를 사용하여 자동으로 생성되는 데이터 세트의 이름은 &quot;Adobe Target Experience Events&quot;입니다. 쿼리에서 이 데이터 세트를 사용할 때 다음 이름을 사용하십시오. `adobe_target_experience_events`.

## 목표

사용자 활동을 분석하여 특정 대상에 대한 콘텐츠를 개인화하고 개별 엔티티에 대한 콘텐츠의 다양한 버전을 테스트할 수 있습니다. 나아가 특정 활동을 일정 기간 동안 또는 개별 사용자에 대해 분석함으로써 각 개별 활동의 성과를 보다 명확하게 파악할 수 있다. 이러한 결합된 분석의 결과는 각 개별 활동의 성과를 이해하는 데 활용될 수 있다.

다음 개인화 사용 사례는 Adobe Target 데이터를 사용하여 작성되며 비즈니스 애플리케이션에 대한 고객의 행동에 대한 중요한 통찰력을 만드는 사용자 활동에 중점을 둡니다.

이 안내서에서는 사용 사례 예제를 통해 다음 주요 개념을 설명합니다.

* 카운트, 세부 정보 및 관련 경험 ID와 같이 지정된 날의 활동 ID에 대한 성과를 파악합니다.
* 활동에 대한 방문자 및 이벤트 범위를 결정합니다.
* 경험 ID, 세그먼트 ID 및 활동 ID에 대한 방문자 수, 방문 횟수 및 노출 정보를 수집하기 위해.

### 지정된 날의 시간별 활동 수 생성

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

### 특정 항목에 대한 시간별 세부 정보 생성

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

### 지정된 날의 특정 활동에 대한 경험 ID 목록을 결정합니다

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

### 지정된 날짜 동안 활동 ID당 인스턴스별 이벤트 범위(방문자, 방문, 노출) 목록을 반환합니다

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

### 주어진 일에 대한 활동당 방문자 수, 방문 횟수 및 노출 횟수를 결정합니다

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

### 지정된 날의 경험 ID, 세그먼트 ID 및 EventScope에 대한 방문자, 방문 횟수 및 노출 횟수를 결정합니다

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

### 지정된 날짜의 mbox 이름 및 레코드 수 반환

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
