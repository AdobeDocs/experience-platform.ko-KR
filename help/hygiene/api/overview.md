---
title: 데이터 위생 API 안내서
description: Adobe Experience Platform에서 고객의 저장된 개인 데이터를 프로그래밍 방식으로 수정하거나 삭제하는 방법을 알아봅니다.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 16eecb22a1bec89c7dbac2fcee566a2226cf897f
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 데이터 위생 API 안내서

>[!IMPORTANT]
>
>Adobe Experience Platform의 데이터 위생 기능은 현재 Healthcare Shield를 구입한 조직에서만 사용할 수 있습니다.

데이터 위생 API를 사용하면 데이터 세트에 대해 만료 날짜를 예약하고 Adobe Experience Platform에 고객의 저장된 개인 데이터를 프로그래밍 방식으로 수정하거나 삭제할 수 있습니다. 이 안내서에서는 API를 사용하기 위한 사전 요구 사항을 설명하고 더 엔드포인트별 설명서에 대한 링크를 제공합니다.

## 시작하기

다음 루트 경로를 통해 데이터 위생 API에 액세스할 수 있습니다. `https://platform.adobe.io/data/core/hygiene/`

아래 섹션에서는 API를 호출하기 전에 알아야 하는 핵심 개념에 대해 설명합니다.

### 필수 헤더에 대한 값을 수집합니다

데이터 위생 API를 호출하려면 먼저 인증 자격 증명을 수집해야 합니다. 다음을 수행합니다 [API 인증 안내서](../../landing/api-authentication.md) 데이터 위생 API에 필요한 각 헤더에 대한 값을 생성하려면 아래에 표시된 대로 다음을 수행합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

### 샘플 API 호출 읽기

이 문서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/api-guide.md#sample-api) Experience Platform API에 대한 시작 안내서에서 를 참조하십시오.

## 데이터 집합 만료

데이터 세트 만료는 시간 지연된 &quot;데이터 세트 삭제&quot; 작업입니다. 데이터 세트 만료일을 만들어 해당 데이터 세트를 삭제할 시간을 지정합니다. 자세한 내용은 [데이터 세트 만료 끝점 안내서](./dataset-expiration.md) 를 참조하십시오.

## 소비자 삭제

>[!NOTE]
>
>소비자 삭제는 Adobe Healthcare Shield 또는 Privacy Sheild를 구입한 조직에만 사용할 수 있습니다.

데이터 위생 API를 사용하면 한 데이터 세트 또는 모든 데이터 세트에서 소비자 ID와 연결된 모든 레코드를 삭제할 수 있습니다. 소비자 ID를 삭제하는 모든 데이터 위생 작업은 작업 순서라고 하는 구성에 의해 표시됩니다. 자세한 내용은 [work order endpoint 안내서](./workorder.md) api에서 소비자 삭제 작업에 대한 자세한 내용은 를 참조하십시오.

## 할당량

조직은 각 유형의 데이터 위생 작업에 대해 정해진 월별 작업 할당량으로 제한되어 있으며, 라이센스에 따라 달라질 수 있습니다. 자세한 내용은 [할당량 끝점 안내서](./quota.md) 데이터 위생 프로세스의 현재 할당량 상태 보기에 대한 자세한 정보.

## 다음 단계

이 안내서에서는 API 호출을 사용하여 데이터 위생 요청을 관리하는 방법을 다룹니다. Platform UI에서 이러한 작업을 수행하는 방법에 대한 자세한 내용은 [data warehouse UI 안내서](../ui/overview.md).
