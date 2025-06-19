---
source-git-commit: 1ab56cf2495238385d726277f6409d2e0c0cb017
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---
# 스니펫

## 할당량 및 처리 타임라인 {#quotas}

레코드 삭제 요청은 조직의 라이선스 자격에 따라 결정되는 일별 및 월별 식별자 제출 제한을 따릅니다. 이러한 제한은 UI 및 API 기반 삭제 요청 모두에 적용됩니다.

>[!NOTE]
>
>하루에 최대 **1,000,000개의 식별자를 제출할 수 있습니다**. 단, 남은 월별 할당량이 허용하는 경우에만 제출합니다. 월별 상한이 100만 개 미만인 경우 일일 제출액은 해당 상한을 초과할 수 없습니다.

### 제품별 월별 제출 권한 {#quota-limits}

아래 표에는 제품 및 자격 수준별 식별자 제출 제한이 나와 있습니다. 각 제품에 대해 월간 상한은 고정 식별자 천장이나 사용 허가된 데이터 볼륨에 연결된 백분율 기반 임계값의 두 값 중 적은 값입니다.

| 제품 | 권한 설명 | 월별 상한(둘 중 더 작은 값) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP 또는 Adobe Journey Optimizer | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 식별자 2,000,000개 또는 대응 가능 대상의 5% |
| Real-Time CDP 또는 Adobe Journey Optimizer | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 식별자 15,000,000개 또는 대응 가능 대상의 10% |
| Customer Journey Analytics | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 2,000,000개의 식별자 또는 100개의 식별자/백만 CJA 권한 행당 |
| Customer Journey Analytics | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 15,000,000개의 식별자 또는 100만 개의 CJA 권한 행당 200개의 식별자 |

>[!NOTE]
>
> 대부분의 조직에서는 실제 대응 가능 대상 또는 CJA 행 권한에 따라 월별 제한이 내려집니다.

할당량은 매월 1일에 재설정됩니다. 사용되지 않은 할당량은 **이월되지 않습니다**.

>[!NOTE]
>
>할당량은 **제출된 식별자**&#x200B;에 대한 조직의 라이선스가 부여된 월별 권한을 기반으로 합니다. 이러한 기능은 시스템 가드레일에 의해 적용되지 않지만 모니터링 및 검토 할 수 있습니다.
>
>레코드 삭제는 **공유 서비스**&#x200B;입니다. 월간 캡은 Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics 및 적용 가능한 모든 Shield 추가 기능에 걸쳐 가장 높은 권한을 반영합니다.

### 식별자 제출을 위한 처리 타임라인 {#sla-processing-timelines}

제출 후 레코드 삭제 요청은 자격 수준에 따라 큐에 추가되고 처리됩니다.

| 제품 및 자격 설명 | 대기열 기간 | 최대 처리 시간(SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 최대 15일 | 30일 |
| Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 일반적으로 24시간 | 15일 |

조직에서 더 높은 제한을 필요로 하는 경우 Adobe 담당자에게 권한 검토를 문의하십시오.
