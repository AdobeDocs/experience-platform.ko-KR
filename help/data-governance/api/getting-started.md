---
keywords: Experience Platform;홈;인기 항목;DULE;dule
solution: Experience Platform
title: 정책 서비스 API 시작
topic-legacy: developer guide
description: 정책 서비스 API를 사용하면 Adobe Experience Platform 데이터 거버넌스와 관련된 다양한 리소스를 만들고 관리할 수 있습니다. 이 문서에서는 정책 서비스 API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# 시작하기 [!DNL Policy Service] API

다음 [!DNL Policy Service] API를 사용하면 Adobe Experience Platform 데이터 거버넌스와 관련된 다양한 리소스를 만들고 관리할 수 있습니다. 이 문서에서는 을 호출하기 전에 알아야 하는 핵심 개념을 소개합니다 [!DNL Policy Service] API.

## 전제 조건

개발자 안내서를 사용하려면 다음과 같은 다양한 [!DNL Experience Platform] 데이터 거버넌스 기능 작업에 관련된 서비스. 를 사용하기 전에 [!DNL Policy Service API]다음 서비스에 대한 설명서를 검토하십시오.

* [데이터 거버넌스](../home.md): Adobe Analytics 인터페이스 [!DNL Experience Platform] 에서는 데이터 사용 규정을 적용합니다.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

## 샘플 API 호출 읽기

다음 [!DNL Policy Service] API 설명서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

## 필수 헤더

API 설명서를 사용하려면 를 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 을 성공적으로 호출하기 위해 [!DNL Platform] 엔드포인트. 인증 자습서를 완료하면에서 필요한 각 헤더에 대한 값을 제공합니다. [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

의 모든 리소스 [!DNL Experience Platform]는 데이터 거버넌스에 속하는 항목을 비롯하여 특정 가상 샌드박스에 고립됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## 코어 및 사용자 지정 리소스

내 [!DNL Policy Service] API, 모든 정책 및 마케팅 작업을 다음 중 하나라고 합니다 `core` 또는 `custom` 리소스 를 참조하십시오.

`core` 리소스는 Adobe에 의해 정의되고 유지 관리되는 리소스인 반면, `custom` 리소스는 조직에서 만들고 유지 관리하는 항목이며, 따라서 IMS 조직에서만 고유하며 볼 수 있습니다. 목록 및 조회 작업(`GET`)는에서 허용되는 유일한 작업입니다 `core` 리소스, 목록, 조회 및 업데이트 작업`POST`, `PUT`, `PATCH`, 및 `DELETE`)에 사용할 수 있습니다. `custom` 리소스 를 참조하십시오.

## 다음 단계

정책 서비스 API를 사용하여 호출을 시작하려면 사용 가능한 끝점 가이드 중 하나를 선택합니다.
