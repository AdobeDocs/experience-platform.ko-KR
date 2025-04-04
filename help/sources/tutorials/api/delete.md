---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;계정 삭제;삭제;api
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 계정 삭제
type: Tutorial
description: 흐름 서비스 API를 사용하여 계정을 삭제하는 방법을 알아봅니다.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# 흐름 서비스 API를 사용하여 계정 삭제

오류가 있거나 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)을(를) 사용하여 더 이상 사용되지 않는 소스 계정을 삭제할 수 있습니다.

API를 사용하여 계정을 삭제하는 방법에 대한 절차는 다음 튜토리얼을 참조하십시오.

## 시작하기

이 자습서에서는 유효한 연결 ID가 있어야 합니다. 올바른 연결 ID가 없는 경우 [소스 개요](../../home.md)에서 선택한 커넥터를 선택하고 이 자습서를 시도하기 전에 설명된 단계를 따르십시오.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [원본](../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 계정 삭제

>[!TIP]
>
>소스 계정을 삭제하기 전에 먼저 소스 계정과 연결된 기존 데이터 흐름을 삭제해야 합니다. 기존 데이터 흐름을 삭제하려면 [소스 데이터 흐름 삭제](./delete-dataflows.md)에 대한 자습서를 참조하십시오.

계정을 삭제하려면 삭제할 계정에 해당하는 기본 연결 ID를 제공하면서 [!DNL Flow Service] API에 DELETE 요청을 합니다.

**API 형식**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 삭제하려는 소스 계정의 기본 연결 ID입니다. |

**요청**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

연결에 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다.

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 기존 계정을 삭제했습니다.

사용자 인터페이스를 사용하여 이러한 작업을 수행하는 방법에 대한 단계는 [UI에서 계정 삭제](../../tutorials/ui/delete-accounts.md)에 대한 자습서를 참조하십시오.
