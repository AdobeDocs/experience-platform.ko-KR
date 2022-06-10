---
title: Adobe Target을 사용한 활동 분석
description: 이 문서에서는 Query Service를 사용하여 Adobe Target 데이터로 만든 데이터 세트에서 실행 가능한 인사이트를 만드는 방법을 설명합니다.
source-git-commit: 870626f25b1aabdcb5739bbb1ab85bdad44df195
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Adobe Target을 사용한 활동 분석

Adobe Experience Platform에서는 XDM(Experience Data Model) 필드를 사용하여 Adobe Target에서 데이터를 수집하여 Query Service에 사용할 데이터 세트를 만들 수 있습니다. Adobe Target은 컨텐츠를 사용자 지정하고 사용자 경험을 개인화하도록 설계되었으므로 이러한 데이터 세트에서 실행되는 쿼리를 사용하면 SQL을 통해 사용자 활동을 분석하여 고도로 개인화되고 포커스가 있는 통찰력을 얻을 수 있습니다.

이 문서에서는 고객의 행동과 특성에 따라 일반적인 사용 사례를 보여 주는 다양한 샘플 SQL 쿼리를 제공합니다.

## 시작하기

다음 각 사용 사례에 대해 매개 변수가 있는 SQL 쿼리 예는 사용자 정의할 수 있는 템플릿으로 제공됩니다. 표시되는 곳에 매개 변수를 제공합니다. `{ }` 을 참조하십시오.

## 높은 수준 부분 XDM 필드 매핑

다음 표에는 일반적인 Target 필드와 해당 XDM 필드가 매핑되어 있습니다.

>[!NOTE]
>
>의 사용 `[ ]` xdm 필드 내에서 는 배열을 나타냅니다.

| Target 필드 이름 | XDM 필드 이름 | 참고 |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | 해당 없음 |
| 활동 ID | `_experience.target.activities.activityID` | 해당 없음 |
| 경험 ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | 해당 없음 |
| 세그먼트 ID | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | 해당 없음 |
| 이벤트 범위 | `_experience.target.activities[].activityEvents[].eventScope` | 이 필드는 새 방문자 및 방문을 추적합니다. |
| 단계 ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | 이 필드는 Adobe Campaign의 사용자 지정 단계 ID입니다. |
| 가격 합계 | commerce.order.priceTotal | 해당 없음 |

>[!IMPORTANT]
>
>Target 데이터를 사용하여 자동으로 생성된 데이터 세트의 이름은 &quot;Adobe Target Experience Events&quot;입니다. 쿼리와 함께 이 데이터 세트를 사용할 때는 이름을 사용하십시오 `adobe_target_experience_events`.

## 목표

사용자 활동을 분석하여 특정 대상에 대한 콘텐츠를 개인화하고 개별 엔티티에 대해 다양한 버전의 콘텐츠를 테스트할 수 있습니다. 또한, 주어진 기간 또는 개별 사용자에 대한 특정 활동을 분석함으로써, 각 개별 활동의 성과를 보다 명확하게 이해할 수 있다. 이 결합된 분석의 결과를 사용하여 각 개별 활동의 성과를 이해할 수 있습니다.

다음 개인화 사용 사례는 Adobe Target 데이터를 사용하여 만들어지며 사용자 활동에 주력하여 비즈니스 애플리케이션에 대한 고객의 행동에 대한 중요한 통찰력을 제공합니다.

이 안내서에서는 사용 사례 예를 통해 다음과 같은 주요 개념을 보여줍니다.

* 카운트, 세부 사항 및 관련 경험 ID와 같이, 지정된 날짜의 활동 ID 성능을 이해하기 위해
* 활동에 대한 방문자 및 이벤트 범위를 판별하려면
* 방문자 수, 방문 횟수 및 경험 ID, 세그먼트 ID 및 활동 ID에 대한 노출 정보를 수집하기 위해

### 지정된 날짜에 대한 시간별 활동 수 생성

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

### 특정 특정 항목에 대한 시간별 세부 정보 생성

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

### 특정 날짜에 대한 경험 ID 목록을 확인합니다

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

### 지정된 날 동안 활동 ID당 인스턴스별 이벤트 범위(방문자, 방문, 노출 횟수) 목록을 반환합니다

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

### 특정 날짜에 대한 활동당 방문자 수, 방문 및 노출 횟수 확인

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

### 지정된 날짜의 경험 ID, 세그먼트 ID 및 EventScope에 대한 방문자, 방문 및 노출 횟수를 결정합니다

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
