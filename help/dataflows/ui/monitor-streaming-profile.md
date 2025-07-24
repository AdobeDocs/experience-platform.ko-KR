---
title: 스트리밍 프로필 수집 모니터링
description: 모니터링 대시보드를 사용하여 스트리밍 프로필 수집을 모니터링하는 방법에 대해 알아봅니다
hide: true
hidefromtoc: true
source-git-commit: 2f78b70761ef676fe4ab61b89b6cbb261c99e9ca
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 3%

---

# 스트리밍 프로필 수집 모니터링

Adobe Experience Platform UI의 모니터링 대시보드를 사용하여 조직의 스트리밍 프로필 수집 비율을 실시간으로 모니터링할 수 있습니다. 이 기능을 사용하면 스트리밍 데이터와 관련된 처리량, 지연 및 데이터 품질 지표의 투명도를 향상시킬 수 있습니다. 또한 이 기능을 사용하여 사전 예방적 경고 및 실행 가능한 인사이트 검색을 통해 잠재적 용량 위반 및 데이터 수집 문제를 식별할 수 있습니다.

모니터링 대시보드를 사용하여 조직의 스트리밍 프로필 수집 작업 비율 및 지표를 모니터링하는 방법에 대해 알아보려면 다음 안내서를 참조하십시오.

## 스트리밍 프로필 수집 대시보드 이해

스트리밍 프로필 수집을 위해 모니터링 대시보드에서 [!UICONTROL 처리량], [!UICONTROL 수집], [!UICONTROL 대기 시간]의 세 가지 지표 범주를 사용할 수 있습니다.

* **처리량**: 구성된 기간 동안 Experience Platform에서 처리하는 데이터 양에 대한 정보를 보려면 **[!UICONTROL 처리량]**&#x200B;을(를) 선택하십시오. 이 지표를 참조하여 시스템의 효율성 및 용량을 평가하십시오.
   * **용량**: 정의된 조건에서 샌드박스가 처리할 수 있는 최대 데이터 양입니다.
   * **요청 처리량**: 수집 시스템에서 이벤트를 받는 비율(초당 이벤트 수)입니다.
   * **처리 처리량**: 시스템이 들어오는 이벤트 페이로드를 수집 및 처리하는 속도로서 초당 이벤트로 측정됩니다.
* **수집**: 샌드박스의 수집 작업에 대한 정보를 보려면 [!UICONTROL 수집]을 선택하십시오. 이러한 수집 작업은 세 가지 다른 지표로 측정됩니다.
   * **만들어진 레코드**: 지정된 기간 내에 만들어진 총 레코드 양입니다. 이 지표는 샌드박스의 성공적인 데이터 수집 프로세스를 나타냅니다.
   * **실패한 레코드**: 오류로 인해 수집되지 않은 총 레코드 수입니다.
   * **삭제된 레코드**: 용량 제한을 위반하여 삭제된 총 레코드 수입니다.
* **지연**: Experience Platform이 요청에 응답하거나 지정된 기간 내에 작업을 완료하는 데 걸리는 시간에 대한 정보를 보려면 [!UICONTROL 지연]을(를) 선택하십시오.

## 스트리밍 프로필 수집을 위한 지표 모니터링 {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="스트리밍 프로필 수집 모니터링"
>abstract="스트리밍 프로필에 대한 모니터링 대시보드에는 처리량, 수집 비율 및 지연 시간이 표시됩니다. 이 대시보드를 사용하여 데이터 처리 지표를 보고, 이해하고, 분석합니다. Experience Platform에 스트리밍 프로필."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="요청 처리량"
>abstract="이 지표는 초당 수집 시스템으로 들어오는 이벤트 수를 나타냅니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="처리 처리량"
>abstract="이 지표는 초당 시스템에서 성공적으로 수집한 이벤트 수를 나타냅니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="P95 수집 지연"
>abstract="이 지표는 이벤트가 Experience Platform에 도착하는 순간부터 프로필 스토어에 성공적으로 수집될 때까지의 95번째 백분위수 지연을 측정합니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="최대 처리량"
>abstract="이 지표는 스트리밍 프로필 수집을 시작하는 초당 최대 인바운드 요청 수를 나타냅니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="레코드 수집됨"
>abstract="이 지표는 구성된 기간 내에 프로필 저장소로 수집된 총 레코드 수를 나타냅니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="레코드 실패"
>abstract="이 지표는 구성된 기간 내에 오류로 인해 프로필 저장소로의 수집에 실패한 총 레코드 수를 나타냅니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="생략된 레코드"
>abstract="이 지표는 구성 또는 용량 위반으로 인해 구성된 기간 내에 삭제된 총 레코드 수를 나타냅니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="오류 세부 정보"
>abstract="이 지표는 오류로 인해 실패한 이벤트 수를 나타냅니다."
>text="Learn more in documentation"

| 지표 | 설명 | 차원 | 측정 빈도 |
| --- | --- | --- | --- |
| 요청 처리량 | 이 지표는 초당 수집 시스템으로 들어오는 이벤트 수를 나타냅니다. | 샌드박스/데이터 흐름 | 60초마다 데이터 새로 고침으로 실시간 모니터링. |
| 처리 처리량 | 이 지표는 초당 시스템에서 성공적으로 수집한 이벤트 수를 나타냅니다. | 샌드박스/데이터 흐름 | 60초마다 데이터 새로 고침으로 실시간 모니터링. |
| P95 수집 지연 | 이 지표는 이벤트가 Experience Platform에 도착하는 순간부터 프로필 스토어에 성공적으로 수집될 때까지의 95번째 백분위수 지연을 측정합니다. | 샌드박스/데이터 흐름 | 60초마다 데이터 새로 고침으로 실시간 모니터링. |
| 최대 처리량 |
| 레코드 수집됨 | 이 지표는 구성된 기간 내에 프로필 저장소로 수집된 총 레코드 수를 나타냅니다. | <ul><li>샌드박스/데이터 흐름</li><li>데이터 흐름 실행</li></ul> | <ul><li>샌드박스/데이터 흐름: 60초마다 데이터 새로 고침으로 실시간 모니터링.</li><li>데이터 흐름 실행: 15분 안에 그룹화됩니다.</li></ul> |
| 레코드 실패 | 이 지표는 구성된 기간 내에 오류로 인해 프로필 저장소로의 수집에 실패한 총 레코드 수를 나타냅니다. | <ul><li>샌드박스/데이터 흐름</li><li>데이터 흐름 실행</li></ul> | <ul><li>샌드박스/데이터 흐름: 60초마다 데이터 새로 고침으로 실시간 모니터링.</li><li>데이터 흐름 실행: 15분 안에 그룹화됩니다.</li></ul> |
| 생략된 레코드 | 이 지표는 구성 또는 용량 위반으로 인해 구성된 기간 내에 삭제된 총 레코드 수를 나타냅니다. | <ul><li>샌드박스/데이터 흐름</li><li>데이터 흐름 실행</li></ul> | <ul><li>샌드박스/데이터 흐름: 60초마다 데이터 새로 고침으로 실시간 모니터링.</li><li>데이터 흐름 실행: 15분 안에 그룹화됩니다.</li></ul> |
| 오류 세부 정보 | 이 지표는 오류로 인해 실패한 이벤트 수를 나타냅니다. | 데이터 흐름 실행 | 시간별 창에 그룹화됩니다. |

{style="table-layout:auto"}