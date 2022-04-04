---
title: 서비스 수준 계약 및 타겟
description: Edge Network Server API에 대한 인증을 구성하는 방법 알아보기
seo-description: Learn how to configure authentication for the Edge Network Server API
keywords: 데이터 수집;수집;에지 네트워크;api;sla;slt;서비스 수준
hide: true
hidefromtoc: true
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---


# 가드레일

## 개요 {#overview}

Adobe은 상업적으로 적절한 노력을 통해 [!DNL Server API] 월별 청구 주기 동안 각 지역에 대해 최소 99.9%의 월별 가동 시간 백분율 내에서 사용할 수 있습니다.

## 정의

* **사용 가능** 은(는) Experience Adobe Experience Platform Edge Network에서 처리한 요청에서 오류가 발생하지 않고 프로비저닝된 Adobe Experience Platform Edge Network API와 관련된 요청의 비율로 5분마다 계산됩니다. 테넌트가 지정된 5분 간격으로 요청을 하지 않은 경우 해당 간격은 100%를 사용할 수 있는 것으로 간주됩니다.
* **월별 가동 시간 비율** 특정 지역의 경우 한 달에 5분 간격 모두에 대한 가용성의 평균으로 계산됩니다.
* An **업스트림** Adobe Edge 네트워크 뒤의 서비스로서, Adobe 서버 측 전달, Adobe Edge 세그멘테이션 또는 Adobe Target과 같은 특정 데이터 스트림에 대해 활성화됩니다.
* A **요청** 서버 API로 전송되는 는 하나 이상의 요청 단위로 정의됩니다.
* A **요청 단위** 은 요청의 8KB 조각과 데이터 스트림에 대해 구성된 하나의 업스트림에 해당합니다.
* An **오류** 은 Adobe Experience Platform Edge Network로 인해 실패하는 모든 요청입니다 [내부 서비스 오류](error-handling.md).

## 내부 타겟

Adobe 엔지니어링 팀은 거의 실시간 원격 분석, 모니터링 및 확장 절차에 가까운 배포를 통해 다음 타겟을 보장합니다.

* HTTP 요청의 1% 미만 반환 `5xx` 지난 5분 동안의 오류
* 지난 5분 동안 업스트림 연결의 1% 미만 반환
* 임차인 용량은 제한에 도달하는 순간부터 10분 이내에 두 배가 됩니다.

## 서비스 수준 계약 제외

위에서 설명한 서비스 수준 약정은 다음 이벤트로 인해 발생하는 가용성 또는 성능 문제에 적용되지 않습니다.

* 인터넷 액세스 또는 Adobe의 인프라 이상의 관련 문제를 포함하여 합리적인 통제 범위를 벗어나는 요소.
* 모든 오용 [!DNL Server API]아래에 요약된 제한에 의해 정의되는 대로 입니다.

## 서비스 제한

모든 데이터 저장소는 특정 사용 제한을 강제 적용하며, 이는 주로 동시에 전송할 수 있는 이벤트 수, 이벤트 크기 및 해당 요청이 라우팅되는 업스트림 서비스 수를 제어합니다.

### 단위 요청

모든 한계는 **요청 단위(RU)**&#x200B;으로 정의되는 경우 **8KB 조각** 데이터 스트림에 구성된 하나의 업스트림 서비스로 이동하는 요청의 수입니다.

#### 예시

| 데이터 스트림당 구성된 업스트림 | 평균 요청 크기 | 단위 요청 |
| --- | --- | --- |
| 1(Adobe 플랫폼) | 8KB(조각 1개) | 1 |
| 2(Adobe 플랫폼, Adobe Target) | 8KB(조각 1개) | 2 |
| 2(Adobe 플랫폼, Adobe Target) | 16KB(조각 2개) | 4 |
| 2(Adobe 플랫폼, Adobe Target) | 64KB(조각 8개) | 16 |

### 단위 제한 요청

아래 표에는 기본 제한 값이 표시되어 있습니다. 더 높은 요청 단위 제한이 필요한 경우 계정 담당자에게 문의하십시오.

| 끝점 | 초당 요청 수 |
| --- | --- |
| `/v2/interact` | 4000년 |
| `/v2/collect` | 6000년 |


### HTTP 요청 크기 제한

| 페이로드 형식 | 요청에 대한 최대 크기 | 최대 8KB 요청 조각 |
| --- | --- | --- |
| JSON 일반 텍스트 | 64KB | 8 |


>[!NOTE]
>
>페이로드 자체에 따라, 이진 형식은 일반적으로 20~40% 더 작으므로 일반 텍스트 JSON보다 더 많은 데이터를 푸시할 수 있습니다. 데이터 세트에 대한 용량이 더 필요한 경우 고객 지원 담당자에게 문의하십시오.

