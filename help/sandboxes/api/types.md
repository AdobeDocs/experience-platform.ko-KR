---
keywords: Experience Platform;홈;인기 항목;목록 샌드박스
solution: Experience Platform
title: 샌드박스 유형 API 엔드포인트
description: /sandboxTypes 끝점에 GET 요청을 하여 조직에서 지원되는 샌드박스 유형 목록을 검색할 수 있습니다.
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%

---

# 샌드박스 유형 엔드포인트

에 GET 요청을 하여 조직에서 지원되는 샌드박스 유형 목록을 검색할 수 있습니다. `/sandboxTypes` 엔드포인트.

## 시작하기

이 안내서에 사용된 API 끝점은 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크, 이 문서의 샘플 API 호출 읽기에 대한 안내서 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보입니다.

## 지원되는 샌드박스 유형 목록 검색

에 GET 요청을 하여 조직에서 지원되는 샌드박스 유형 목록을 검색할 수 있습니다. `/sandboxTypes` 엔드포인트.

**API 형식**

```http
GET /sandboxTypes
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**응답**

성공적인 응답은 조직에 대해 지원되는 샌드박스 유형 목록을 반환합니다.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
