---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼테이션;세그먼테이션 서비스;api;
solution: Experience Platform
title: 세분화 서비스 API 시작하기
description: 다음 설명서는 Segmentation API를 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# 세분화 서비스 API 시작하기 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] 을(를) 통해 Adobe Experience Platform에서 세그먼트를 작성하고 대상자를 생성할 수 있습니다. [!DNL Real-Time Customer Profile] 데이터.

개발자 안내서를 사용하려면 여러 가지 사항에 대한 작업 이해가 필요합니다 [!DNL Experience Platform] 사용과 관련된 서비스 [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): 다음에서 대상 세그먼트를 만들 수 있습니다. [!DNL Real-Time Customer Profile] 데이터.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다. 세그먼테이션을 최대한 활용하려면 데이터에 따라 프로필 및 이벤트가 수집되는지 확인하십시오. [데이터 모델링 우수 사례](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 를 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다. [!DNL Segmentation] API.

## 샘플 API 호출 읽기

다음 [!DNL Segmentation Service] API 설명서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

## 필수 헤더

API 설명서를 사용하려면 를 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 을(를) 성공적으로 호출하기 위해 [!DNL Platform] 엔드포인트. 인증 자습서를 완료하면에 있는 각 필수 헤더에 대한 값을 제공합니다. [!DNL Experience Platform] 아래와 같이 API 호출:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스 작업에 대한 자세한 정보 [!DNL Experience Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

## 다음 단계

를 사용하여 전화를 걸려면 [!DNL Segmentation Service] API에서 왼쪽 탐색 또는 내에서 사용 가능한 엔드포인트 안내서 중 하나를 선택합니다. [개발자 안내서 개요](./overview.md)
