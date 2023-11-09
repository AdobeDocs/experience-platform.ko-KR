---
title: Query Accelerated Store 보고 인사이트 안내서
description: 가속화된 스토어 데이터 및 사용자 정의 대시보드와 함께 사용할 수 있도록 쿼리 서비스를 통해 보고 인사이트 데이터 모델을 구축하는 방법에 대해 알아봅니다.
exl-id: 216d76a3-9ea3-43d3-ab6f-23d561831048
source-git-commit: 037ea8d11bb94e3b4f71ea301a535677b3cccdbd
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# 쿼리 가속화 스토어 보고 인사이트 안내서

쿼리 가속 저장소를 사용하면 데이터에서 중요한 통찰력을 얻는 데 필요한 시간과 처리 능력을 줄일 수 있습니다. 일반적으로 데이터는 집계 보기가 생성되고 보고되는 정기적인 간격(예: 시간별 또는 일별)으로 처리됩니다. 집계된 데이터에서 생성된 이러한 보고서를 분석하면 비즈니스 성과를 향상시키기 위한 통찰력을 도출합니다. 쿼리 가속 저장소는 캐시 서비스, 동시성, 대화형 경험 및 상태 비저장 API를 제공합니다. 단, 데이터는 원시 데이터 쿼리가 아닌 집계된 쿼리에 대해 사전 처리되고 최적화된다고 가정합니다.

쿼리 가속 저장소를 사용하면 사용자 지정 데이터 모델을 구축하거나 기존 Adobe Real-time Customer Data Platform 데이터 모델을 확장할 수 있습니다. 그런 다음 보고 통찰력을 참여하거나 선택한 보고/시각화 프레임워크에 포함할 수 있습니다. 다음 방법에 대해 알아보려면 Real-time Customer Data Platform 통찰력 데이터 모델 설명서 를 참조하십시오 [sql 쿼리 템플릿을 사용자 정의하여 마케팅 및 KPI(주요 성능 지표) 사용 사례에 대한 Real-Time CDP 보고서를 생성합니다.](../../../dashboards/cdp-insights-data-model.md).

Adobe Experience Platform의 Real-Time CDP 데이터 모델은 프로필, 대상 및 대상에 대한 인사이트를 제공하며 Real-Time CDP 인사이트 대시보드를 사용할 수 있습니다. 이 문서에서는 Reporting Insights 데이터 모델을 만드는 과정을 안내하고 필요에 따라 Real-Time CDP 데이터 모델을 확장하는 방법을 안내합니다.

## 전제 조건

이 자습서에서는 사용자 정의 대시보드를 사용하여 Platform UI 내에서 사용자 정의 데이터 모델의 데이터를 시각화합니다. 다음을 참조하십시오. [사용자 정의 대시보드 설명서](../../../dashboards/user-defined-dashboards.md) 이 기능에 대해 자세히 알아보십시오.

## 시작하기

Data Distiller SKU는 보고 통찰력에 대한 사용자 지정 데이터 모델을 구축하고 풍부한 플랫폼 데이터를 포함하는 Real-Time CDP 데이터 모델을 확장하는 데 필요합니다. 다음을 참조하십시오. [포장](../../packaging.md), [보호 기능](../../guardrails.md#query-accelerated-store), 및  [라이선스](../../data-distiller/license-usage.md) Data Distiller SKU와 관련된 설명서입니다. Data Distiller SKU가 없는 경우 Adobe 고객 서비스 담당자에게 자세한 내용을 문의하십시오.

## 보고 통찰력 데이터 모델 구축

이 자습서에서는 대상 통찰력 데이터 모델 구축의 예를 사용합니다. 한 개 이상의 광고주 플랫폼을 사용하여 대상자에게 도달하는 경우 광고주의 API를 사용하여 대상자의 대략적인 일치 수를 얻을 수 있습니다.

처음에는 소스(잠재적으로 광고주 플랫폼 API)의 초기 데이터 모델이 있습니다. 원시 데이터를 집계하여 보려면 아래 이미지에 설명된 대로 보고 통찰력 모델을 만드십시오. 이를 통해 하나의 데이터 세트가 대상 일치의 상한과 하한을 얻을 수 있습니다.

![Audience Insight 사용자 모델의 ERD(엔티티 관계형 다이어그램).](../../images/query-accelerated-store/audience-insight-user-model.png)

이 예에서는 `externalaudiencereach` 테이블/dataset는 ID를 기반으로 하며 일치 횟수의 하한과 상한을 추적합니다. 다음 `externalaudiencemapping` 차원 테이블/데이터 세트는 외부 ID를 플랫폼의 대상 및 대상에 매핑합니다.

## Data Distiller을 사용하여 보고 통찰력에 대한 모델 만들기

다음으로 보고 인사이트 모델(`audienceinsight` 이 예제에서는) 및 SQL 명령 사용 `ACCOUNT=acp_query_batch and TYPE=QSACCEL` 가속화된 저장소에서 만들어지는지 확인합니다. 그런 다음 쿼리 서비스를 사용하여 `audienceinsight.audiencemodel` 스키마 `audienceinsight` 데이터베이스.

>[!NOTE]
>
>데이터 Distiller SKU는 `ACCOUNT=acp_query_batch` 명령입니다. 이 기능이 없으면 데이터 레이크에 일반 데이터 모델이 만들어집니다.

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## 테이블, 관계 만들기 및 데이터 채우기

이제 을(를) 만들었습니다. `audienceinsight` 보고 인사이트 모델, 만들기 `externalaudiencereach` 및 `externalaudiencemapping` 테이블 및 테이블 간의 관계를 설정합니다. 그런 다음 를 사용합니다. `ALTER TABLE` 테이블 사이에 외래 키 제약 조건을 추가하고 관계를 정의하는 명령입니다. 다음 SQL 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.

```sql
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencereach
WITH ( DISTRIBUTION = REPLICATE ) AS
  SELECT cast(null as int) approximate_count_upper_bound,
         cast(null as string) deliverystatusdescription,
         cast(null as timestamp)  timeupdated ,
         cast(null as int) operationstatuscode ,
         cast(null as string) operationstatusdescription,
         cast(null as int) approximate_count_lower_bound,
         cast(null as timestamp)timecreated ,
         cast(null as timestamp)timecontentupdated ,
         cast(null as int) deliverystatuscode ,
         cast(null as int)  ext_custom_audience_id
   WHERE false;
 
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencemapping
WITH ( DISTRIBUTION = REPLICATE ) AS
SELECT cast(null as int) audience_id,
       cast(null as int) destination_id,
       cast(null as int) ext_custom_audience_id
 WHERE false;
 
ALTER TABLE externalaudiencereach ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES externalaudiencemapping (ext_custom_audience_id) NOT enforced;
```

두 가지를 성공적으로 실행한 후 `ALTER TABLE` 명령, 팩트 테이블과 차원 테이블 간의 관계가 형성됩니다.

명령문이 실행되면 `SHOW datagroups;` 가속화된 저장소에서 사용 가능한 데이터 세트 목록을 반환하는 명령 `audienceinsight.audiencemodel`. 표 작성된 결과는 아래 제공된 예와 유사해야 합니다.

>[!IMPORTANT]
>
>가속화된 저장소의 데이터만 쿼리 서비스 상태 비저장 API 끝점에서 액세스할 수 있습니다. `POST /data/foundation/query/accelerated-queries`.

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## 보고 통찰력 데이터 모델 쿼리

쿼리 서비스를 사용하여 `audiencemodel.externalaudiencereach` 차원 테이블. 예제 쿼리는 아래에 표시됩니다.

```sql
SELECT a.ext_custom_audience_id,
       a.approximate_count_upper_bound
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.externalaudiencemapping AS b
                    ON ( ( a.ext_custom_audience_id ) =
                         ( b.ext_custom_audience_id ) )
GROUP  BY a.ext_custom_audience_id,
          a.approximate_count_upper_bound
LIMIT  5000 ;
```

표로 정리된 결과에는 카운트와 ID가 포함됩니다.

```console
ext_custom_audience_id | approximate_count_upper_bound
------------------------+-------------------------------
 23850912218170554      |                          1000
 23850808585120554      |                       1012000
 23850808585220554      |                        100000
 23850814978560554      |                          1000
 23850808585180554      |                        421000
 23850814978510554      |                       3001000
 23850814978530554      |                        300000
 23850912218160554      |                        105000
 23850808584990554      |                          1000
 23850809520110554      |                          1000
(10 rows)
```

## Real-Time CDP 통찰력 데이터 모델을 사용하여 데이터 모델 확장

추가 세부 정보로 대상 모델을 확장하여 더 풍부한 차원 테이블을 만들 수 있습니다. 예를 들어 대상 이름 및 대상 이름을 외부 대상 식별자에 매핑할 수 있습니다. 이렇게 하려면 쿼리 서비스 를 사용하여 새 데이터 세트를 만들거나 새로 고친 후 대상 및 대상을 외부 ID와 결합하는 대상 모델에 추가하십시오. 아래 다이어그램은 이 데이터 모델 확장의 개념을 보여 줍니다.

![Real-Time CDP 인사이트 데이터 모델과 쿼리 가속 저장소 모델을 연결하는 ERD 다이어그램입니다.](../../images/query-accelerated-store/updatingAudienceInsightUserModel.png)

## 차원 테이블을 생성하여 보고 통찰력 모델 확장

쿼리 서비스를 사용하여 보강된 Real-Time CDP 차원 데이터 세트의 주요 설명 속성을 `audienceinsight` 데이터 모델을 만들고 팩트 테이블과 새 차원 테이블 간의 관계를 설정합니다. 아래 SQL에서는 기존 차원 테이블을 Reporting Insights 데이터 모델에 통합하는 방법을 보여 줍니다.

```sql
CREATE TABLE audienceinsight.audiencemodel.external_seg_dest_map AS
  SELECT ext_custom_audience_id,
         destination_name,
         audience_name,
         destination_status,
         a.destination_id,
         a.audience_id
  FROM   externalaudiencemapping AS a
         LEFT OUTER JOIN adwh_dim_audiences AS b
                      ON ( ( a.audience_id ) = ( b.audience_id ) )
         LEFT OUTER JOIN adwh_dim_destination AS c
                      ON ( ( a.destination_id ) = ( c.destination_id ) );
 
ALTER TABLE externalaudiencereach  ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES external_seg_dest_map (ext_custom_audience_id) NOT enforced;
```

사용 `SHOW datagroups;` 추가 만들기 확인 명령 `external_seg_dest_map` 차원 테이블.

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## 확장 가속 저장소 보고 통찰력 데이터 모델 쿼리

이제 `audienceinsight` 데이터 모델이 증강되어 쿼리할 준비가 되었습니다. 다음 SQL은 매핑된 대상 및 대상 목록을 보여 줍니다.

```sql
SELECT a.ext_custom_audience_id,
       b.destination_name,
       b.audience_name,
       b.destination_status,
       b.destination_id,
       b.audience_id
FROM   audiencemodel.externalaudiencereach1 AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
LIMIT  25; 
```

쿼리는 쿼리 가속 저장소의 모든 데이터 세트를 반환합니다.

```console
ext_custom_audience_id | destination_name |       audience_name        | destination_status | destination_id | audience_id 
------------------------+------------------+---------------------------+--------------------+----------------+-------------
 23850808595110554      | FCA_Test2        | United States             | enabled            |     -605911558 | -1357046572
 23850799115800554      | FCA_Test2        | Born in 1980s             | enabled            |     -605911558 | -1224554872
 23850799115790554      | FCA_Test2        | Born in 1970s             | enabled            |     -605911558 |  1899603869
 23850798177620554      | FCA_Test1        | Billionaires              | enabled            |      321720439 |  1401872665
 23850814978560554      | FCA_Test3        | Canada - Saskatchewan     | enabled            |     1182494936 | -1917996562
 23850808585180554      | FCA_Test3        | United States             | enabled            |     1182494936 | -1357046572
 23850814978530554      | FCA_Test3        | Canada - British Columbia | enabled            |     1182494936 |  -652840507
 23850808585120554      | FCA_Test3        | Canada - Quebec           | enabled            |     1182494936 |  -519557860
 23850809520110554      | FCA_Test3        | Born in 1960s             | enabled            |     1182494936 |   237824266
 23850808585220554      | FCA_Test3        | Western Canada            | enabled            |     1182494936 |  1075937528
 23850808584990554      | FCA_Test3        | Canada - Ontario          | enabled            |     1182494936 |  1593438041
 23850814978510554      | FCA_Test3        | Canada - Alberta          | enabled            |     1182494936 |  1862946783
 23850912218170554      | FCA_Test4        | Canada - Alberta          | enabled            |     1549248886 |  1862946783
 23850912218160554      | FCA_Test4        | Born in 1970s             | enabled            |     1549248886 |  1899603869
```

## 사용자 정의 대시보드를 사용하여 데이터 시각화

사용자 정의 데이터 모델을 만들었으므로 이제 사용자 정의 쿼리 및 사용자 정의 대시보드를 사용하여 데이터를 시각화할 준비가 되었습니다.

다음 SQL은 대상의 대상별 일치 카운트 분류와 대상의 대상별 각 대상 분류를 제공합니다.

```sql
SELECT b.destination_name,
       a.approximate_count_upper_bound,
       b.audience_name
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
GROUP  BY b.destination_name,
          a.approximate_count_upper_bound,
          b.audience_name
ORDER BY b.destination_name
LIMIT  5000
```

아래 이미지는 Reporting Insights 데이터 모델을 사용하여 가능한 사용자 지정 시각화의 예를 제공합니다.

![새 reporting insights 데이터 모델에서 만든 대상 및 대상 위젯별 일치 횟수입니다.](../../images/query-accelerated-store/user-defined-dashboard-widget.png)

사용자 지정 데이터 모델은 사용자 정의 대시보드 작업 영역의 사용 가능한 데이터 모델 목록에서 찾을 수 있습니다. 다음을 참조하십시오. [사용자 정의 대시보드 안내서](../../../dashboards/user-defined-dashboards.md) 사용자 지정 데이터 모델을 활용하는 방법에 대한 지침을 제공합니다.
