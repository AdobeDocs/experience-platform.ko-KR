---
title: 데이터 위생 API 안내서
description: Adobe Experience Platform에서 고객의 저장된 개인 데이터를 프로그래밍 방식으로 수정하거나 삭제하는 방법을 알아봅니다.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# 데이터 위생 API 안내서

데이터 위생 API를 사용하면 Adobe Experience Platform에서 고객의 저장된 개인 데이터를 프로그래밍 방식으로 수정하거나 삭제할 수 있을 뿐만 아니라 데이터 세트의 만료 날짜를 예약할 수 있습니다. 이 안내서에서는 API 사용에 대한 사전 요구 사항을 다루고 더 많은 끝점별 설명서에 대한 링크를 제공합니다.

## 시작하기

다음 루트 경로를 통해 데이터 위생 API에 액세스할 수 있습니다. `https://platform.adobe.io/data/core/hygiene/`

아래 섹션에서는 API를 호출하기 전에 알아야 하는 핵심 개념에 대해 간략히 설명합니다.

### 필수 헤더에 대한 값 수집

데이터 위생 API를 호출하려면 먼저 인증 자격 증명을 수집해야 합니다. 다음 [API 인증 안내서](../../landing/api-authentication.md) 아래와 같이 데이터 위생 API의 필수 각 헤더에 대한 값을 생성하려면 다음을 수행합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

### 샘플 API 호출 읽기

이 문서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/api-guide.md#sample-api) Experience Platform API 시작 안내서에서 확인할 수 있습니다.

## 데이터 세트 만료

데이터 세트 만료는 시간이 지연된 &quot;데이터 세트 삭제&quot; 작업입니다. 데이터 세트 만료를 만들면 해당 데이터 세트를 삭제해야 하는 향후 시간을 지정할 수 있습니다. 다음을 참조하십시오. [데이터 세트 만료 끝점 안내서](./dataset-expiration.md) api의 데이터 세트 만료 예약에 대한 자세한 내용.

## 레코드 삭제

>[!IMPORTANT]
>
>레코드 삭제 요청은 구입한 조직에 대해서만 사용할 수 있습니다. **Adobe 헬스케어 실드**.
>
>
>레코드 삭제는 데이터 정리, 익명 데이터 제거 또는 데이터 최소화에 사용됩니다. 다음과 같습니다 **아님** GDPR(일반 데이터 보호 규정)과 같은 개인 정보 보호 규정에 관한 데이터 주체 권한 요청(준수)에 사용됩니다. 모든 규정 준수 사용 사례에 대해 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 대신,

데이터 위생 API를 사용하면 하나 또는 모든 데이터 세트에서 ID와 관련된 모든 레코드를 삭제할 수 있습니다. ID를 삭제하는 모든 데이터 라이프사이클 작업은 작업 순서라는 구문을 통해 표시됩니다. 다음을 참조하십시오. [작업 주문 끝점 안내서](./workorder.md) api의 레코드 삭제 작업에 대한 자세한 내용을 보려면 를 클릭하십시오.

## 할당량

조직은 각 데이터 라이프사이클 작업 유형에 대해 사전 결정된 월별 작업 할당량으로 제한되며, 이는 라이선스에 따라 달라질 수 있습니다. 다음을 참조하십시오. [할당량 끝점 안내서](./quota.md) 데이터 라이프사이클 프로세스의 현재 할당량 상태를 보는 방법에 대한 자세한 내용

## 다음 단계

이 안내서에서는 API 호출을 사용하여 데이터 라이프사이클 요청을 관리하는 방법을 다룹니다. Platform UI에서 이러한 작업을 수행하는 방법에 대한 자세한 내용은 [data lifecycle UI 안내서](../ui/overview.md).
