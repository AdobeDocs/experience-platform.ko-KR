---
keywords: Experience Platform;home;popular topics;DULE;dule
solution: Experience Platform
title: 정책 서비스 API 시작하기
topic: developer guide
description: 정책 서비스 API를 사용하면 Adobe Experience Platform 데이터 거버넌스와 관련된 다양한 리소스를 만들고 관리할 수 있습니다. 이 문서에서는 Policy Service API를 호출하기 전에 알아야 할 핵심 개념을 소개합니다.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Getting started with the [!DNL Policy Service] API

API를 [!DNL Policy Service] 사용하면 Adobe Experience Platform과 관련된 다양한 리소스를 만들고 관리할 수 있습니다 [!DNL Data Governance]. 이 문서에서는 [!DNL Policy Service] API를 호출하기 전에 알아야 할 핵심 개념을 소개합니다.

## 전제 조건

개발자 가이드를 사용하려면 데이터 거버넌스 기능 사용과 관련된 다양한 [!DNL Experience Platform] 서비스에 대한 충분한 지식이 필요합니다. 을(를) 사용하여 작업하기 전에 다음 서비스 [!DNL Policy Service API]에 대한 설명서를 검토하십시오.

* [[!DNL Data Governance]](../home.md):데이터 사용 규정 준수를 [!DNL Experience Platform] 적용하는 프레임워크입니다.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
* [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 샘플 API 호출 읽기

API 설명서는 요청의 서식을 지정하는 방법을 시연하기 위한 예제 API 호출을 제공합니다. [!DNL Policy Service] 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

## 필요한 헤더

또한 API 설명서에서는 끝점을 성공적으로 호출하려면 [인증 자습서를](../../tutorials/authentication.md) 완료해야 [!DNL Platform] 합니다. 인증 자습서를 완료하면 아래와 같이 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Data Governance]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## 코어와 사용자 정의 리소스

API 내 [!DNL Policy Service] 에서 모든 정책 및 마케팅 작업을 `core` 또는 `custom` 리소스라고 합니다.

`core` 리소스는 Adobe에 의해 정의되고 유지 관리되는 리소스인 반면 `custom` 리소스는 조직에서 만들고 유지 관리하는 리소스이므로 IMS 조직에서만 고유하고 볼 수 있습니다. 따라서 목록 및 조회 작업(`GET`)은 `core` 자원에 대해 허용되는 유일한 작업이지만 목록 작성, 조회 및 업데이트 작업(`POST`, `PUT``PATCH`및 `DELETE`)은 `custom` 리소스에 사용할 수 있습니다.

## 다음 단계

정책 서비스 API를 사용하여 호출을 시작하려면 사용 가능한 끝점 가이드 중 하나를 선택합니다.