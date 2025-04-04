---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;API;API;삭제;데이터 흐름 삭제
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 데이터 흐름 삭제
type: Tutorial
description: 흐름 서비스 API를 사용하여 일괄 처리 및 스트리밍 데이터 흐름을 삭제하는 방법을 알아봅니다.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 2%

---

# 흐름 서비스 API를 사용하여 데이터 흐름 삭제

오류가 있거나 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)을(를) 사용하여 더 이상 사용되지 않는 일괄 처리 및 스트리밍 데이터 흐름을 삭제할 수 있습니다.

이 자습서에서는 [!DNL Flow Service]을(를) 사용하여 일괄 처리와 스트리밍 소스로 만들어진 데이터 흐름을 삭제하는 단계를 다룹니다.

## 시작하기

이 자습서를 사용하려면 유효한 흐름 ID가 있어야 합니다. 올바른 흐름 ID가 없는 경우 [소스 개요](../../home.md)에서 선택한 커넥터를 선택하고 이 자습서를 시도하기 전에 설명된 단계를 따르십시오.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [원본](../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 데이터 흐름 삭제

기존 흐름 ID를 사용하면 [!DNL Flow Service] API에 대한 DELETE 요청을 수행하여 데이터 흐름을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /flows/{FLOW_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 삭제할 데이터 흐름의 고유한 `id` 값입니다. |

**요청**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다. 데이터 흐름에 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. API가 데이터 흐름이 삭제되었음을 나타내는 HTTP 404(찾을 수 없음) 오류를 반환합니다.

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 기존 데이터 흐름을 삭제했습니다.

사용자 인터페이스를 사용하여 이러한 작업을 수행하는 방법에 대한 단계는 [UI에서 데이터 흐름 삭제](../../tutorials/ui/delete.md)에 대한 자습서를 참조하십시오.
