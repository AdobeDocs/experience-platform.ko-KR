---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;api;
solution: Experience Platform
title: 세그멘테이션 서비스 API 시작하기
topic-legacy: developer guide
description: 다음 설명서는 세그멘테이션 API를 성공적으로 사용하기 위해 알고 있어야 하는 추가 정보를 제공합니다.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# 세그멘테이션 서비스 API 시작 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] 세그먼트를 작성하고 사용자의 [!DNL Real-Time Customer Profile] 데이터.

개발자 가이드는 다양한 [!DNL Experience Platform] 사용과 관련된 서비스 [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): 대상 세그먼트를 [!DNL Real-Time Customer Profile] 데이터.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다. 세그멘테이션을 가장 잘 사용하려면 데이터가 [데이터 모델링 우수 사례](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 를 사용하여 성공적으로 작업하기 위해 알고 있어야 하는 추가 정보를 제공합니다. [!DNL Segmentation] API.

## 샘플 API 호출 읽기

다음 [!DNL Segmentation Service] API 설명서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

## 필수 헤더

API 설명서를 사용하려면 를 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 을 성공적으로 호출하기 위해 [!DNL Platform] 엔드포인트. 인증 자습서를 완료하면에서 필요한 각 헤더에 대한 값을 제공합니다. [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스 작업에 대한 자세한 내용은 [!DNL Experience Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

## 다음 단계

를 사용하여 호출을 하는 방법 [!DNL Segmentation Service] API를 사용하려면 왼쪽 탐색 또는 내에서 사용 가능한 엔드포인트 가이드 중 하나를 선택합니다 [개발자 안내서 개요](./overview.md)
