---
title: 스트리밍 대상자 모니터링
description: 모니터링 대시보드를 사용하여 스트리밍 세분화를 사용하여 평가되는 대상을 모니터링하는 방법에 대해 알아봅니다
hide: true
hidefromtoc: true
source-git-commit: 6fe0a36a8f2ac2cb954935ee8fe64432442b6e84
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 6%

---


# 스트리밍 대상자 모니터링

intro blurb

## 시작하기

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [데이터 흐름](../home.md): 데이터 흐름은 Experience Platform에서 정보를 전송하는 데이터 작업을 나타냅니다. ID 서비스, 실시간 고객 프로필 및 대상뿐만 아니라 소스 커넥터에서 대상 데이터 세트로 데이터를 쉽게 이동할 수 있도록 다양한 서비스에 걸쳐 구성됩니다.
* [세그먼테이션 서비스](../../segmentation/home.md):
* [기능](../../landing/license-usage-and-guardrails/capacity.md): Experience Platform에서 기능은 조직이 보호 기능을 초과했는지 여부를 알려주고 이러한 문제를 해결하는 방법에 대한 정보를 제공합니다.

## 스트리밍 대상에 대한 지표 모니터링 {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="평가율"
>abstract="이 지표는 초당 평가된 레코드 수를 나타냅니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="P95 수집 지연"
>abstract="이 지표는 대상자에 대한 성공적인 평가를 위해 Adobe Experience Platform에 도착하는 이벤트의 95번째 백분위수 지연을 측정합니다."
>text="Learn more in documentation"

다음 표는 스트리밍 대상에 사용되는 지표에 대한 자세한 정보를 제공합니다.

| 지표 | 설명 | 차원 |
| ------ | ----------- | ---------- |
| 평가율 | 초당 처리된 대상 평가 수입니다. | 샌드박스, 데이터 세트 |
| P95 수집 지연 | 대상에 성공적으로 도착한 이벤트의 95백분위수 대기 시간입니다. | 샌드박스, 데이터 세트 |
| 레코드 수신됨 | 선택한 기간 동안 스트리밍 세분화를 위해 스트리밍 수집에서 받은 총 레코드 수입니다. | 데이터 세트 |
| 평가된 레코드 | 선택한 기간 동안 스트리밍 세분화를 사용하여 **성공**&#x200B;이(가) 평가한 총 레코드 수입니다. | 데이터 세트 |
| 레코드 실패 | 선택한 기간 동안 오류로 인해 스트리밍 세분화에서 **실패**&#x200B;한 총 레코드 수입니다. | 데이터 세트, 흐름 실행 |
| 생략된 레코드 | 선택한 기간 동안 오류로 인해 스트리밍 세분화에서 **건너뜀**&#x200B;된 총 레코드 수입니다. | 데이터 세트, 흐름 실행 |
| 적격 프로필 | 선택한 기간 동안 대상자에 적합한 프로필의 수입니다. | 샌드박스, 대상 |
| 프로필이 실격됨 | 선택한 기간 동안 대상에서 자격을 잃은 프로필 수입니다. | 샌드박스, 대상 |

{style="table-layout:auto"}

## 스트리밍 대상에 대한 모니터링 대시보드 사용 {#monitoring-dashboard}

스트리밍 대상의 모니터링 대시보드에 액세스하려면 Experience Platform UI로 이동하여 왼쪽 탐색에서 **[!UICONTROL 모니터링]**&#x200B;을 선택한 다음 **[!UICONTROL 전체 스트리밍]**&#x200B;을 선택하십시오.

이미지

대시보드 맨 위에는 **[!UICONTROL 대상]** 지표 카드가 있습니다. 대상의 **평가 비율**&#x200B;에 대한 정보가 표시됩니다.