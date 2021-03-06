---
keywords: Experience Platform;홈;인기 항목;데이터 세트;유지 시간;ttl;time-to-live;
solution: Experience Platform
title: 데이터 세트에 대한 Time-to-Live
description: 이 문서에서는 Adobe Experience Platform용 프로필 저장소의 데이터 세트에 대한 TTL(time-to-live)에 대한 일반적인 지침을 제공합니다.
source-git-commit: 878c04c688268f8cf1850c3e8d40f958a6d2d69b
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# 프로필 서비스 TTL(time-to-live)

프로필 서비스를 사용하여 사용자가 프로필 저장소의 데이터에 TTL(time-to-live)을 적용할 수 있습니다. TTL은 데이터가 데이터 세트 내에 있는 시간을 제한하는 메커니즘입니다. 이를 통해 더 이상 사용 사례에 유용하지 않은 프로필 저장소에서 데이터를 자동으로 제거할 수 있습니다.

현재, 프로필은 경험 이벤트 TTL만 지원합니다.

## 경험 이벤트 TTL

Experience Event TTL을 사용하면 실시간 고객 프로필 사용 데이터 세트에 TTL을 적용하여 더 이상 유효하지 않은 프로필 저장소에서 데이터를 제거할 수 있습니다.

>[!NOTE]
>
>데이터 세트에서 경험 이벤트 TTL을 사용하려면 지원 팀에 문의해야 합니다.

프로필 사용 데이터 세트에서 Experience Event TTL을 활성화하면 Platform은 두 단계 프로세스에서 경험 이벤트 데이터에 대한 TTL 만료 값을 자동으로 적용합니다.

1. 데이터 집합에 수집되는 모든 새 데이터에는 수집 시 TTL 만료 값이 적용됩니다.
2. 데이터 집합에 있는 모든 기존 데이터는 1회 채우기 시스템 작업으로 소급하여 TTL 만료 값이 적용됩니다. 데이터 세트에 TTL 만료 값이 배치되면 시스템 작업이 실행되는 즉시 TTL 만료 값보다 오래된 이벤트가 삭제됩니다. 다른 모든 이벤트는 이벤트 타임스탬프에서 TTL 만료 값에 도달하는 즉시 삭제됩니다.

>[!NOTE]
>
>TTL이 적용되면 TTL의 일 수보다 오래된 데이터는 **영구적으로 삭제되며 복원할 수 없습니다.**
> 
>또한 세그먼트의 전환 확인 기간이 TTL 경계 내에 있는지 확인합니다. 그렇지 않으면 TTL을 적용한 후 세그먼트 결과가 올바르지 않을 수 있습니다. 따라서 예를 들어 TTL(30일)을 적용했으며 최대 45일 전의 데이터를 보려는 세그먼트가 있는 경우 세그먼트에서 잘못된 프로필을 생성합니다.
> 
>따라서 가능하면 모든 데이터 세트에 대해 동일한 TTL을 유지하여 세그먼테이션 로직의 다른 데이터 세트에 다른 TTL 값이 영향을 주지 않도록 해야 합니다.

따라서 예를 들어, 5월 15일에 TTL 값을 30일로 적용했다면 다음 단계가 발생합니다.

1. 모든 새 이벤트는 섭취되는 동안 적용된 TTL 값 30일을 얻게 됩니다.
2. 4월 15일 이전의 타임스탬프가 있는 기존 이벤트는 시스템 작업으로 즉시 삭제됩니다.
3. 타임스탬프가 4월 15일보다 짧은 기존 이벤트는 이벤트 타임스탬프 이후 30일 후의 TTL 만료 값을 갖습니다. 따라서 이벤트에 4월 18일의 타임스탬프가 있는 경우 해당 타임스탬프의 날짜 이후 30일(5월 18일)이 삭제됩니다.

