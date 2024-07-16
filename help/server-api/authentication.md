---
title: 인증
description: Adobe Experience Platform Edge Network 서버 API에 대한 인증을 구성하는 방법을 알아봅니다.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 7%

---

# 인증 {#authentication}

## 개요

[!DNL Edge Network Server API]은(는) 이벤트 원본 및 API 컬렉션 도메인에 따라 인증된 데이터 수집과 인증되지 않은 데이터 수집을 모두 처리합니다.

각 요청에 대해 [!DNL Server API]은(는) 데이터 스트림 [!DNL access type] 설정을 확인합니다. 이 설정을 사용하여 고객은 인증된 데이터 또는 인증된 데이터와 인증되지 않은 데이터 모두를 수락하도록 데이터 스트림을 구성할 수 있습니다. 기본적으로 두 유형의 데이터가 모두 허용됩니다.

데이터 스트림 액세스 유형 구성에 대한 자세한 내용은 [데이터 스트림을 만들고 구성하는 방법](../datastreams/overview.md#create)에 대한 설명서를 참조하십시오.

다음은 데이터 스트림 [!DNL Access Type] 구성 및 요청을 받은 끝점을 기반으로 하는 동작에 대한 요약입니다.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| 혼합(기본값) | 요청을 인증하지 않음 | 요청 인증 |
| 인증됨 | 요청 인증 | 요청 인증 |

`server.adobedc.net`의 개인 서버에서 오는 API 호출은 항상 인증되어야 합니다.

## 전제 조건 {#prerequisites}

[!DNL Server API]을(를) 호출하기 전에 다음 필수 구성 요소를 충족하는지 확인하십시오.

* Adobe Experience Platform에 액세스할 수 있는 조직 계정이 있습니다.
* Experience Platform 계정에 Adobe Experience Platform API 제품 프로필에 대해 `developer` 및 `user` 역할이 활성화되어 있습니다. [Admin Console](../access-control/home.md) 관리자에게 문의하여 계정에 대해 이러한 역할을 사용하도록 설정하십시오.
* Adobe ID이 있습니다. Adobe ID이 없는 경우 [Adobe Developer Console](https://developer.adobe.com/console)(으)로 이동하여 새 계정을 만드십시오.

## 자격 증명 수집 {#credentials}

Platform API를 호출하려면 먼저 [인증 자습서](../landing/api-authentication.md)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더의 값이 제공됩니다.

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api 키: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform의 리소스는 특정 가상 샌드박스로 격리될 수 있습니다. Platform API에 대한 요청에서 작업이 수행될 샌드박스의 이름과 ID를 지정할 수 있습니다. 이러한 매개 변수는 선택 사항입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Experience Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../sandboxes/home.md)를 참조하세요.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

## 데이터 세트 쓰기 권한 구성 {#dataset-write-permissions}

데이터 집합 쓰기 권한을 구성하려면 [Admin Console](https://adminconsole.adobe.com)(으)로 이동하여 API 키에 첨부된 제품 프로필을 찾은 다음 다음 권한을 설정하십시오.

* [!UICONTROL 샌드박스] 섹션에서 데이터 스트림 샌드박스를 선택합니다.
* [!UICONTROL 데이터 관리] 섹션에서 **[!UICONTROL 데이터 세트 관리]** 권한을 선택합니다.

## 인증 오류 문제 해결 {#troubleshooting-authorization}

| 오류 코드 | 오류 메시지 | 설명 |
| --- | --- | --- |
| `EXEG-0500-401` | 잘못된 인증 토큰 | 이 오류 메시지는 다음 상황 중 하나에 표시됩니다.  <ul><li>`authorization` 헤더 값이 없습니다.</li><li>`authorization` 헤더 값에 필요한 `Bearer` 토큰이 포함되어 있지 않습니다.</li><li>입력한 인증 토큰에 잘못된 포맷이 있습니다.</li><li>데이터 스트림에 인증이 필요하지만 요청에 필수 헤더가 없습니다.</li></ul> |
| `EXEG-0501-401` | 잘못된 사용자 인증 토큰 | 이 오류 메시지는 다음 상황 중 하나에 표시됩니다. <ul><li>API 호출에 필수 `x-user-token` 헤더가 없습니다.</li><li>입력한 사용자 토큰에 잘못된 포맷이 있습니다.</li></ul> |
| `EXEG-0502-401` | 잘못된 인증 토큰 | 입력한 인증 토큰에 유효한 형식(JWT)이 있지만 서명이 올바르지 않은 경우 이 오류 메시지가 표시됩니다. 올바른 JWT 토큰을 가져오는 방법에 대해 알아보려면 [인증 자습서](../landing/api-authentication.md)를 확인하십시오. |
| `EXEG-0503-401` | 잘못된 인증 토큰 | 입력한 인증 토큰이 만료되면 이 오류 메시지가 표시됩니다. 새 토큰을 생성하려면 [인증 자습서](../landing/api-authentication.md)를 수행하십시오. |
| `EXEG-0504-401` | 필수 제품 컨텍스트가 누락되었습니다. | 이 오류 메시지는 다음 상황 중 하나에 표시됩니다.  <ul><li>개발자 계정은 Adobe Experience Platform 제품 컨텍스트에 액세스할 수 없습니다.</li><li>회사 계정은 아직 Adobe Experience Platform을 사용할 수 없습니다.</li></ul> |
| `EXEG-0505-401` | 필수 인증 토큰 범위가 누락되었습니다. | 이 오류는 서비스 계정 인증에만 적용됩니다. 호출에 포함된 서비스 인증 토큰이 `acp.foundation` IMS 범위에 대한 액세스 권한이 없는 서비스 계정에 속하는 경우 오류 메시지가 표시됩니다. |
| `EXEG-0506-401` | 쓰기 위해 샌드박스에 액세스할 수 없음 | 이 오류 메시지는 개발자 계정에 데이터 스트림이 정의된 Experience Platform 샌드박스에 대한 `WRITE` 액세스 권한이 없을 때 표시됩니다. |
