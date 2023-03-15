---
keywords: Experience Platform;홈;인기 항목;DULE;dule
solution: Experience Platform
title: Policy Service API 시작하기
description: Policy Service API 를 사용하면 Adobe Experience Platform 데이터 거버넌스와 관련된 다양한 리소스를 생성하고 관리할 수 있습니다. 이 문서에서는 Policy Service API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# 시작하기 [!DNL Policy Service] API

다음 [!DNL Policy Service] API를 사용하면 Adobe Experience Platform 데이터 거버넌스와 관련된 다양한 리소스를 만들고 관리할 수 있습니다. 이 문서에서는 을 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다. [!DNL Policy Service] API.

## 전제 조건

개발자 안내서를 사용하려면 다양한 을(를) 이해하고 있어야 합니다 [!DNL Experience Platform] 데이터 거버넌스 기능 작업과 관련된 서비스입니다. 을(를) 사용하여 작업을 시작하기 전에 [!DNL Policy Service API], 다음 서비스에 대한 설명서를 검토하십시오.

* [데이터 거버넌스](../home.md): 다음에 사용되는 프레임워크 [!DNL Experience Platform] 데이터 사용 규정 준수를 시행합니다.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

## 샘플 API 호출 읽기

다음 [!DNL Policy Service] API 설명서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

## 필수 헤더

API 설명서를 사용하려면 를 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 을(를) 성공적으로 호출하기 위해 [!DNL Platform] 엔드포인트. 인증 자습서를 완료하면에 있는 각 필수 헤더에 대한 값을 제공합니다. [!DNL Experience Platform] 아래와 같이 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

의 모든 리소스 [!DNL Experience Platform]데이터 거버넌스에 속하는 을 포함하여 은 특정 가상 샌드박스로 분리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## 핵심 및 사용자 지정 리소스 비교

다음 범위 내 [!DNL Policy Service] API, 모든 정책 및 마케팅 작업은 다음 중 하나로 지칭됩니다. `core` 또는 `custom` 리소스.

`core` 리소스는 Adobe에 의해 정의되고 유지되는 리소스이며, `custom` 리소스는 조직에서 만들고 유지 관리하는 리소스이며, 따라서 고유하고 IMS 조직에서만 볼 수 있습니다. 목록 및 조회 작업(`GET`)에 허용된 유일한 작업입니다 `core` 리소스를 나타내는 반면 목록, 조회 및 업데이트 작업(`POST`, `PUT`, `PATCH`, 및 `DELETE`)을 사용할 수 있습니다. `custom` 리소스.

## 다음 단계

정책 서비스 API를 사용하여 호출을 시작하려면 사용 가능한 끝점 안내서 중 하나를 선택합니다.
