---
title: 감사 쿼리 API 시작
description: 감사 쿼리 API를 사용하면 다양한 Adobe Experience Platform 기능에 대한 지표 데이터를 검색할 수 있습니다. 이 문서에서는 감사 쿼리 API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.
role: Developer
feature: Audits, API
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 11%

---

# 감사 쿼리 API 시작

Adobe Experience Platform을 사용하면 감사 이벤트 로그 형태로 다양한 서비스 및 기능에 대한 사용자 활동을 감사할 수 있습니다. 로그에 기록된 각 작업에는 작업 유형, 날짜 및 시간, 작업을 수행한 사용자의 이메일 ID 및 작업 유형과 관련된 추가 속성을 나타내는 메타데이터가 포함됩니다.

감사 쿼리 API를 사용하면 감사 이벤트 로그 형식으로 다양한 서비스 및 기능에 대한 사용자 활동을 감사할 수 있습니다. 이 문서에서는 감사 쿼리 API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.

## 전제 조건

감사 이벤트를 관리하려면 **[!UICONTROL 사용자 활동 로그 보기]** 액세스 제어 권한이 부여되어야 합니다([!UICONTROL 데이터 거버넌스] 범주 아래에 있음). Platform 기능에 대한 개별 권한을 관리하는 방법을 알아보려면 [액세스 제어 설명서](../../../../access-control/home.md)를 참조하십시오.

### 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

이 안내서를 사용하려면 Platform API를 호출하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더의 값이 제공됩니다.

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api 키: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다. [!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../../../sandboxes/home.md)를 참조하십시오.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT 및 PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* Content-Type: application/json

## 다음 단계

[!DNL Audit Query] API를 사용하여 호출을 시작하려면 [이벤트 끝점 안내서](./events.md) 및 [내보내기 끝점 안내서](./export.md)를 참조하십시오.
