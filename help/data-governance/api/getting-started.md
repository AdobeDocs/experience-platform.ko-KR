---
keywords: Experience Platform;홈;인기 항목;DULE;dule
solution: Experience Platform
title: Policy Service API 시작하기
description: Policy Service API 를 사용하면 Adobe Experience Platform 데이터 거버넌스와 관련된 다양한 리소스를 생성하고 관리할 수 있습니다. 이 문서에서는 Policy Service API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.
role: Developer
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 8%

---

# [!DNL Policy Service] API 시작

[!DNL Policy Service] API를 사용하면 Adobe Experience Platform 데이터 거버넌스와 관련된 다양한 리소스를 만들고 관리할 수 있습니다. 이 문서에서는 [!DNL Policy Service] API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.

## 전제 조건

개발자 안내서를 사용하려면 데이터 거버넌스 기능 작업과 관련된 다양한 [!DNL Experience Platform] 서비스에 대한 작업 이해가 필요합니다. [!DNL Policy Service API] 작업을 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [데이터 거버넌스](../home.md): [!DNL Experience Platform]에서 데이터 사용 규정 준수를 적용하는 프레임워크입니다.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

## 샘플 API 호출 읽기

[!DNL Policy Service] API 설명서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

## 필수 헤더

또한 API 설명서를 사용하려면 [!DNL Platform] 끝점을 성공적으로 호출하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 [!DNL Experience Platform] API 호출의 각 필수 헤더에 대한 값이 제공됩니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

데이터 거버넌스에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## 핵심 및 사용자 지정 리소스 비교

[!DNL Policy Service] API에서 모든 정책 및 마케팅 작업은 `core` 또는 `custom` 리소스로 참조됩니다.

`core` 리소스는 Adobe에서 정의하고 유지 관리하는 리소스인 반면 `custom` 리소스는 조직에서 만들고 유지 관리하는 리소스이므로 고유하며 귀사에만 표시됩니다. 따라서 목록 및 조회 작업(`GET`)은 `core` 리소스에서 허용되는 유일한 작업이지만 목록, 조회 및 업데이트 작업(`POST`, `PUT`, `PATCH` 및 `DELETE`)은 `custom` 리소스에 사용할 수 있습니다.

## 다음 단계

정책 서비스 API를 사용하여 호출을 시작하려면 사용 가능한 끝점 안내서 중 하나를 선택합니다.
