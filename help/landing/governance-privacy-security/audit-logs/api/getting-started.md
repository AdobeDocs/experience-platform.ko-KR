---
title: 감사 쿼리 API 시작
description: 감사 쿼리 API를 사용하면 다양한 Adobe Experience Platform 기능에 대한 지표 데이터를 검색할 수 있습니다. 이 문서에서는 Audit Query API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# 감사 쿼리 API 시작

Adobe Experience Platform을 사용하면 감사 이벤트 로그 형식에서 다양한 서비스 및 기능에 대한 사용자 활동을 감사할 수 있습니다. 로그에 기록된 각 작업에는 작업 유형, 날짜 및 시간, 작업을 수행한 사용자의 이메일 ID 및 작업 유형과 관련된 추가 속성을 나타내는 메타데이터가 포함됩니다.

감사 쿼리 API를 사용하면 감사 이벤트 로그 형식의 다양한 서비스 및 기능에 대한 사용자 활동을 감사할 수 있습니다. 이 문서에서는 Audit Query API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.

## 전제 조건

감사 이벤트를 관리하려면 **[!UICONTROL 사용자 활동 로그 보기]** 액세스 제어 권한이 부여됨( [!UICONTROL 데이터 거버넌스] 카테고리). 플랫폼 기능에 대한 개별 권한을 관리하는 방법에 대한 자세한 내용은 [액세스 제어 설명서](../../../../access-control/home.md).

### 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에서 사용되는 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 을 참조하십시오.

### 필수 헤더에 대한 값을 수집합니다

이 안내서를 사용하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 를 호출하여 플랫폼 API를 성공적으로 호출했습니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다. 샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT 및 PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형: application/json

## 다음 단계

를 사용하여 호출을 시작하려면 [!DNL Audit Query] API는 [이벤트 끝점 안내서](./events.md) 그리고 [끝점 내보내기 안내서](./export.md).
