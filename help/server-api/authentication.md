---
title: 인증
description: Adobe Experience Platform Edge Network Server API에 대한 인증을 구성하는 방법을 알아봅니다.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# 인증 {#authentication}

## 개요

다음 [!DNL Edge Network Server API] 는 이벤트 소스 및 API 수집 도메인에 따라 인증되고 인증되지 않은 데이터 수집을 모두 처리합니다.

각 요청에 대해 [!DNL Server API] 데이터 스트림 확인 [!DNL access type] 설정 이 설정을 사용하여 고객은 인증된 데이터 또는 인증된 데이터와 인증되지 않은 데이터를 모두 허용하도록 데이터 스트림을 구성할 수 있습니다. 기본적으로 두 유형의 데이터는 모두 허용됩니다.

데이터 스트림 액세스 유형 구성에 대한 자세한 내용은 다음 방법에 대한 설명서를 참조하십시오 [데이터 스트림 만들기 및 구성](../edge/datastreams/overview.md#create).

다음은 데이터 스트림을 기반으로 한 동작 요약입니다 [!DNL Access Type] 구성 및 요청을 받은 끝점입니다.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| 혼합(기본값) | 요청을 인증하지 않음 | 요청 인증 |
| 인증됨 | 요청 인증 | 요청 인증 |

의 개인 서버에서 오는 API 호출 `server.adobedc.net` 항상 인증되어야 합니다.

## 사전 요구 사항 {#prerequisites}

를 호출하기 전에 [!DNL Server API], 다음 전제 조건을 충족하는지 확인하십시오.

* Adobe Experience Platform에 액세스할 수 있는 조직 계정이 있습니다.
* Experience Platform 계정에는 `developer` 및 `user` Adobe Experience Platform API 제품 프로필에 대해 활성화된 역할. 다음 사항에 문의하십시오. [Admin Console](../access-control/home.md) 관리자가 계정에 대해 이러한 역할을 사용할 수 있도록 설정
* Adobe ID이 있습니다. Adobe ID이 없는 경우 [Adobe Developer 콘솔](https://developer.adobe.com/console) 새 계정을 만듭니다.

## 자격 증명 수집 {#credentials}

플랫폼 API를 호출하려면 먼저 를 완료해야 합니다 [인증 자습서](../landing/api-authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform의 리소스는 특정 가상 샌드박스로 분리할 수 있습니다. Platform API에 대한 요청에서 작업을 수행할 샌드박스의 이름 및 ID를 지정할 수 있습니다. 선택적 매개 변수입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Experience Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

## 데이터 집합 쓰기 권한 구성 {#dataset-write-permissions}

데이터 집합 쓰기 권한을 구성하려면 다음 위치로 이동하십시오. [Admin Console](https://adminconsole.adobe.com)에서 API 키에 첨부된 제품 프로필을 찾아 다음 권한을 설정합니다.

* 에서 [!UICONTROL 샌드박스] 섹션에서 데이터 스트림 샌드박스를 선택합니다.
* 에서 [!UICONTROL 데이터 관리] 섹션에서 **[!UICONTROL 데이터 세트 관리]** 권한.

## 인증 오류 문제 해결 {#troubleshooting-authorization}

| 오류 코드 | 오류 메시지 | 설명 |
| --- | --- | --- |
| `EXEG-0500-401` | 잘못된 인증 토큰 | 이 오류 메시지는 다음 중 한 경우에 표시됩니다.  <ul><li>다음 `authorization` 헤더 값이 없습니다.</li><li>다음 `authorization` 헤더 값은 필수 값을 포함하지 않습니다 `Bearer` 토큰.</li><li>제공된 인증 토큰의 형식이 잘못되었습니다.</li><li>데이터 스트림에 인증이 필요하지만 요청에 필요한 헤더가 없습니다.</li></ul> |
| `EXEG-0501-401` | 잘못된 사용자 인증 토큰 | 이 오류 메시지는 다음 중 한 경우에 표시됩니다. <ul><li>API 호출에 필요한 가 없습니다 `x-user-token` 헤더.</li><li>제공된 사용자 토큰의 형식이 잘못되었습니다.</li></ul> |
| `EXEG-0502-401` | 잘못된 인증 토큰 | 제공된 인증 토큰에 유효한 형식(JWT)이 있지만 해당 서명이 유효하지 않은 경우 이 오류 메시지가 표시됩니다. 을(를) 확인합니다. [인증 자습서](../landing/api-authentication.md) 유효한 JWT 토큰을 가져오는 방법을 알아봅니다. |
| `EXEG-0503-401` | 잘못된 인증 토큰 | 제공된 인증 토큰이 만료되면 이 오류 메시지가 표시됩니다. 를 통해 [인증 자습서](../landing/api-authentication.md) 새 토큰을 생성하기 위해 |
| `EXEG-0504-401` | 필요한 제품 컨텍스트가 없습니다. | 이 오류 메시지는 다음 중 한 경우에 표시됩니다.  <ul><li>개발자 계정에 Adobe Experience Platform 제품 컨텍스트에 대한 액세스 권한이 없습니다.</li><li>회사 계정에 아직 Experience Platform Adobe 권한이 없습니다.</li></ul> |
| `EXEG-0505-401` | 필요한 인증 토큰 범위가 없습니다. | 이 오류는 서비스 계정 인증에만 적용됩니다. 호출에 포함된 서비스 인증 토큰이 액세스 권한이 없는 서비스 계정에 속하면 오류 메시지가 표시됩니다 `acp.foundation` IMS 범위. |
| `EXEG-0506-401` | 샌드박스를 쓰기 위해 액세스할 수 없음 | 이 오류 메시지는 개발자 계정에 `WRITE` 데이터 스트림이 정의된 Experience Platform 샌드박스에 대한 액세스 권한. |
