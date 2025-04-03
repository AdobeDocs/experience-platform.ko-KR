---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼테이션;세그먼테이션 서비스;api;
solution: Experience Platform
title: 세분화 서비스 API 시작하기
description: 다음 설명서는 Segmentation API를 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다.
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 7%

---

# 세분화 서비스 API 시작하기 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service]을(를) 사용하면 [!DNL Real-Time Customer Profile] 데이터에서 Adobe Experience Platform의 세그먼트 정의나 다른 소스를 통해 대상자를 만들 수 있습니다.

개발자 안내서를 사용하려면 [!DNL Segmentation Service] 사용과 관련된 다양한 [!DNL Experience Platform] 서비스에 대한 작업 이해가 필요합니다.

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): [!DNL Real-Time Customer Profile] 데이터에서 대상을 만들 수 있습니다.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다. 세그먼테이션을 최대한 활용하려면 [데이터 모델링 모범 사례](../../xdm/schema/best-practices.md)에 따라 데이터가 프로필 및 이벤트로 수집되는지 확인하십시오.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Segmentation] API를 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

[!DNL Segmentation Service] API 설명서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

## 필수 헤더

또한 API 설명서를 사용하려면 [!DNL Experience Platform] 끝점을 성공적으로 호출하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 [!DNL Experience Platform] API 호출의 각 필수 헤더에 대한 값이 제공됩니다.

- 인증: `Bearer {ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Experience Platform] API에 대한 모든 요청에는 작업을 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스 작업에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하세요.

## 다음 단계

[!DNL Segmentation Service] API를 사용하여 호출하려면 왼쪽 탐색 또는 [개발자 안내서 개요](./overview.md)에서 사용 가능한 끝점 안내서 중 하나를 선택하십시오
