---
title: Privacy Service 우수 사례
description: 이러한 최적의 사용 지침을 따라 개인 정보 보호 요청을 완료할 때 조직에 발생하는 비용과 처리 시간을 줄이는 방법을 알아봅니다.
exl-id: 1333d6c6-5ca0-41c1-9f9e-aa2a5a8b8a9c
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Privacy Service 우수 사례

고객이 데이터 저장소에서 개인 데이터에 액세스하거나 삭제하려는 경우 Privacy Service을 사용하여 데이터 개인정보 보호 규정 준수를 자동화합니다. 이러한 진화하는 비즈니스 요구 사항을 해결하기 위해 Privacy Service은 Adobe Experience Cloud 애플리케이션에서 고객 데이터에 대한 액세스 및 삭제 요청을 제출할 수 있는 RESTful API 및 UI를 제공합니다.

이 안내서에서는 고객 데이터 요청을 관리할 때 개인 정보 요청을 효율적으로 처리하고 완료 응답 시간을 최적화하는 모범 사례에 대해 간략하게 설명합니다.

## 시작하기 {#getting-started}

이 안내서를 사용하려면 [Privacy Service](./home.md)과, 이 안내서를 통해 Adobe Experience Cloud 응용 프로그램에서 데이터 주체(고객)의 액세스를 관리하고 요청을 삭제하는 방법에 대해 이해해야 합니다. 또한 [UI에서 개인 정보 보호 작업 요청 만들기](./ui/user-guide.md#create-a-new-privacy-job-request) 또는 [API](./api/overview.md)에 대한 안내서를 읽고 프로그래밍 방식으로 이러한 작업을 수행하는 방법을 이해하는 것이 좋습니다.

## 전제 조건 {#prerequisites}

Adobe Experience Platform Privacy Service에 대한 액세스는 Adobe Admin Console에서 세분화된 역할 기반 권한을 통해 제어됩니다. Privacy Service UI 및 API의 특정 기능을 사용하려면 제품 프로필에 관련 권한이 있어야 합니다. 추가 권한이 필요한 경우 시스템 관리자에게 문의하십시오.

관리자는 [Privacy Service에 대한 권한 관리](./permissions.md)에 대한 안내서를 참조하십시오.

## 개인 정보 작업 생성 지침 {#creation-guidelines}

요청 처리를 간소화하고 응답 시간을 향상시키려면 개인 정보 작업을 만들 때 다음 지침을 고려하십시오. 이는 API 및 UI 메서드 모두에 적용됩니다.

1. **요청당 데이터 주체 최대화:** 요청당 최대 1000개의 데이터 주체를 가능한 한 많이 포함합니다.
2. **효율성을 위한 그룹 ID:** 각 요청의 단일 데이터 주체(최대 9개)에 대해 여러 ID를 그룹화합니다. **ID는 동일한 요청의 다른 Adobe 서비스에서 가져올 수 있습니다**.
3. **액세스 및 삭제 작업 결합:** 데이터 주체에서 필요한 경우 단일 요청에 &quot;액세스&quot; 및 &quot;삭제&quot; 작업 유형을 모두 포함하십시오.
4. **필요한 제품만 포함:** 필수 또는 라이선스가 부여된 제품만 포함합니다. 추가 제품은 처리 시간을 늘리고 비용을 증가시킬 수 있습니다.

## 개인 정보 작업 상태 모니터링 {#monitor-status}

개인 정보 작업을 효과적으로 모니터링하고 상태를 확인하기 위해 Privacy Service에서는 세 가지 방법을 제공합니다. 사용 가능한 방법은 효율성 및 생산성 모니터링 순서로 아래에 나열되어 있습니다. 각 방법에는 경험을 개선하기 위한 모범 사례 지침이 포함되어 있으며 그 뒤에는 모든 접근 방식을 결합하는 이상적인 시나리오 예제가 제공됩니다.

### 실시간 알림 수신 {#real-time-notifications}

**I/O 이벤트**&#x200B;는 상태 이벤트를 통해 거의 실시간으로 상태 모니터링을 제공합니다. 이 방법은 폴링 메커니즘을 구현할 필요가 없고 추가 API 트래픽을 발생시키므로 가장 효율적인 방법입니다.

**Recommendations:**

- **웹후크 설정:** 제출된 작업의 상태가 변경되면 푸시 알림을 받도록 웹후크를 설정합니다. 이렇게 하면 실시간 모니터링에 도움이 됩니다.
- **알림:** 작업 및 제품 수준에서 알림을 사용하여 요청 진행 상황을 모니터링할 수 있습니다.

Privacy Service 알림에 대한 이벤트 등록 설정 및 알림 페이로드를 해석하는 방법에 대한 지침은 [Privacy Service 이벤트 구독](./privacy-events.md)에 대한 설명서를 참조하십시오.

### 필터를 기반으로 모든 작업 검색 {#retrieve-filtered-responses-for-all-jobs}

지정된 필터를 기반으로 모든 개인 정보 작업 데이터를 검색하려면 **`/jobs` 끝점에 대한 GET 요청을 수행**&#x200B;하십시오. 이 API 호출은 단일 요청으로 큰 작업 ID 집합에 대한 현재 작업 상태를 자세히 볼 수 있도록 하는 데 유용합니다. 자세한 제품 응답이 없지만 [`/jobs/{jobID}` 끝점](#retrieve-detailed-responses-for-specific-jobs)을 사용하여 찾을 수 있습니다.

`/jobs` 끝점에 대한 GET 요청은 대규모 작업 ID 집합의 상태 데이터를 수집하거나 비교하는 데 가장 적절하게 사용되지만 일반 폴링 유형 활동에 대한 **not**&#x200B;입니다.

**Recommendations:**

- **쿼리 매개 변수:** 데이터 범위, 규정 유형 및 상태(처리, 완료 등)와 같은 특정 필터를 사용하여 결과를 좁힐 수 있습니다.

Privacy Service UI를 통해 조직의 모든 현재 개인 정보 보호 작업 목록을 볼 수 있습니다. 작업 요청 목록을 필터링하는 방법에 대한 자세한 내용은 [UI 설명서의 개인 정보 작업 관리](./ui/user-guide.md#job-requests)를 참조하십시오. 또는 [Privacy Service API에서 /job 끝점을 사용](./api/privacy-jobs.md)하는 방법에 대한 설명서를 참조하십시오.

Privacy Service API 설명서에는 [사용 가능한 쿼리 매개 변수 필터](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs)에 대한 세부 정보가 포함되어 있습니다.

### 단일 작업에 대한 자세한 응답 검색 {#retrieve-detailed-responses-for-specific-jobs}

단일 작업에 대한 자세한 응답을 검색하려면 **/jobs/{jobID} 엔드포인트에 대한 GET 요청을 수행하십시오**. 이 방법은 제품별 응답 및 성공 메시지와 같은 심층적인 정보 수집을 위한 것입니다. 이 끝점에 대한 호출은 일반 폴링 활동을 위한 **은(는) 아니지만 응답한 제품과 아직 보류 중인 제품을 확인하는 가장 좋은 방법입니다.**

[특정 작업의 상태를 확인하는 방법](./api/privacy-jobs.md#check-status)에 대한 자세한 내용은 `/jobs/{JOB_ID}` 끝점 설명서를 참조하십시오.

### 이상적인 시나리오 예 {#ideal-scenario}

웹후크를 사용하면 요청에서 ID 그룹이 완료될 때 시스템에서 레코드를 자동으로 업데이트하고 보고 또는 경고를 제공할 수 있습니다. 작업이 아직 해결되지 않은 경우 시스템은 Privacy Service API `/jobs` 끝점에 대한 GET 요청과 함께 이러한 작업 상태를 검색하고 목록의 높은 수준의 업데이트를 제공합니다.

특정 작업이 아직 보류 중이거나 오류를 반환한 경우 `/job/{jobId}` 끝점에 대한 GET 요청으로 자세한 응답을 검색할 수 있습니다.

## 액세스 요청 데이터 {#access-request-data}

데이터 주체 정보가 요청되면 각 서비스는 해당 데이터를 저장하고 사용하는 방식과 일치하는 형식으로 데이터를 반환합니다. 모든 서비스가 요청을 완료하면 이 데이터를 다운로드할 수 있도록 작업 세부 사항에 .ZIP 아카이브 파일 URL이 제공됩니다. [개인 정보 작업 결과를 다운로드하는 방법](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=ko#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F)에 대한 자세한 내용은 문제 해결 안내서를 참조하십시오.

다음은 데이터 아카이브 관리와 관련된 주요 참고 항목입니다.

- 모든 아카이브 파일은 30일 후 Experience Platform 서버에서 삭제됩니다. 30일 이전의 고객 데이터는 쿼리할 수 없습니다.
- 아카이브 파일의 구조는 요청에 포함된 각 제품별 폴더와 그 안에 포함된 데이터 파일을 포함한다. 지정된 ID에 대한 데이터가 없으면 보관 파일 또는 폴더가 비어 있을 수 있습니다.
- 이전에 생성된 작업의 데이터는 완료 날짜 후 30일 동안만 액세스할 수 있습니다. 그 시간이 지나면 데이터가 시스템에서 제거되고 새로운 요청을 수행해야 합니다.

**Recommendations:**

- **Protect 데이터 보관 파일:** URL 및 .ZIP 파일에는 데이터 주체의 PII(개인 식별 정보)가 포함될 수 있으므로 모두 보호해야 합니다.

## 기술 고려 사항 {#technical-considerations}

Privacy Service 요청을 완료할 때 알아 두어야 할 특정 기술 고려 사항이 있습니다.

- **데이터 보존 기간:** 최대 전환 확인 기간은 모든 작업 그룹의 경우 60일이며 쿼리의 최대 기간은 30일(시작/종료 날짜)입니다.
- **게이트웨이 시간 초과:** 60초를 초과하는 경우 게이트웨이에서 요청을 삭제할 수 있다는 점에 유의하십시오.
- **오류 처리:** 오류 메시지를 자세히 검토하고 필요한 경우 요청을 다시 제출합니다. Privacy Service은 오류 발생 후 작업을 자동으로 재처리하지 않습니다.
- **HTTP 429 오류 이해:** HTTP 429 오류 메시지와 문제를 완화하는 데 필요한 단계를 숙지하십시오. HTTP 429 오류는 &#39;요청이 너무 많음&#39;의 결과입니다. 문제 해결 방법에 대한 자세한 내용은 문제 해결 안내서의 [일반적인 오류 메시지](./troubleshooting-guide.md#common-error-messages) 섹션을 참조하십시오.

## 다음 단계

이 문서를 읽으면 이제 Privacy Service을 효율적이고 효과적으로 사용하는 데 필요한 지식과 사례를 얻을 수 있습니다. 다음으로 Privacy Service에 대한 FAQ에 대한 답변과 API에서 일반적으로 발생하는 오류에 대한 정보는 [문제 해결 안내서](./troubleshooting-guide.md)를 참조하십시오.
