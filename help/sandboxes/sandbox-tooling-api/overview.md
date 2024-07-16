---
title: 샌드박스 도구 API 안내서
description: Adobe Experience Platform의 샌드박스 도구 를 사용하면 샌드박스 간에 샌드박스 구성의 스냅샷을 내보내고 가져올 수 있습니다.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---

# [!DNL Sandbox] 도구 API 안내서

[!DNL Sandbox] 도구 API는 조직 내에서 사용할 수 있는 샌드박스 간에 스냅숏을 내보내고 가져올 수 있는 여러 끝점을 제공합니다. 모든 상호 작용은 HTTP 끝점을 통해 발생합니다. 스냅샷을 내보내기 전에 소스 샌드박스에서 패키지에 포함된 객체인 아티팩트가 있는지 확인합니다. 가져오기 요청이 수행되면 [!DNL Azure Blob] 스냅숏을 가져와 템플릿으로 사용하여 대상 샌드박스에 대해 거의 유사한 아티팩트를 생성합니다. 지원되는 개체 및 제한 사항에 대한 목록은 [샌드박스 도구](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) 설명서를 참조하십시오.

이러한 엔드포인트는 아래에 요약되어 있습니다. 자세한 내용은 개별 엔드포인트 안내서를 참조하고 필수 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보는 [시작 안내서](./getting-started.md)를 참조하십시오.

## 패키지 {#packages}

샌드박스 도구 패키지 끝점을 사용하면 패키지를 관리할 수 있습니다. 샌드박스 도구 패키지는 패키지 ID, 이름, 설명, 조직 ID 및 작성자 ID를 포함하는 아티팩트 정의의 컬렉션입니다. API의 패키지 작업에 대한 자세한 내용은 [패키지 끝점 안내서](./packages.md)를 참조하십시오.

## 도구 {#tools}

샌드박스 도구 끝점을 사용하면 작업 JSON 데이터를 독립적으로 가져올 수 있습니다. API에서 작업 JSON 데이터를 검색하는 방법에 대한 자세한 내용은 [도구 끝점 안내서](./tools.md)를 참조하십시오.

## 다음 단계 {#next-steps}

샌드박스 도구 API를 사용하여 호출을 시작하려면 [시작 안내서](./getting-started.md)를 읽은 다음 끝점 안내서 중 하나를 선택하여 특정 끝점을 사용하는 방법을 알아보세요.
