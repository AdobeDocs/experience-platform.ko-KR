---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 셀프 서비스 소스(배치 SDK)에 대한 탐색 사양 구성
description: 이 문서에서는 셀프 서비스 소스(배치 SDK)를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 셀프 서비스 소스(배치 SDK)에 대한 탐색 사양 구성

탐색 사양은 소스에 포함된 객체를 탐색하고 검사하는 데 필요한 매개변수를 정의합니다. 또한 탐색 사양은 객체를 탐색하고 검사할 때 반환되는 응답 형식을 정의합니다.

>[!TIP]
>
>탐색 사양은 하드 코딩되어 있으며, 아래의 페이로드를 연결 사양이 있는 위치에 복사하여 붙여넣으면 됩니다.

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "format": {
        "type": "string"
      },
      "schema": {
        "type": "object",
        "properties": {
          "columns": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                },
                "type": {
                  "type": "string"
                }
              }
            }
          }
        }
      },
      "data": {
        "type": "array",
        "items": {
          "type": "object"
        }
      }
    }
  }
}
```

| 사양 탐색 | 설명 | 예 |
| --- | --- | --- |
| `name` | 탐색 사양의 이름 또는 식별자를 정의합니다. | `Resource` |
| `type` | 탐색 사양의 유형을 정의합니다. | `Resource` |
| `requestSpec` | 연결에서 개체를 탐색하는 데 필요한 매개 변수를 포함합니다. |
| `requestSpec.type` | 요청 사양의 데이터 유형을 정의합니다. | `object` |
| `responseSpec` | 탐색 호출에 대해 반환되는 응답 메시지의 형식을 정의하는 매개 변수를 포함합니다. |
| `responseSpec.type` | 응답 사양의 데이터 유형을 정의합니다. | `object` |
| `responseSpec.properties` | 응답 메시지 포맷 방법과 관련된 정보를 포함합니다. |
| `responseSpec.properties.format` | 응답 스키마의 형식을 정의합니다. | `object` |
| `responseSpec.properties.format.type` | 속성의 데이터 유형을 정의합니다. | `string` |
| `responseSpec.schema` | 응답 스키마의 형식 지정 방식에 대한 정보를 포함합니다. |
| `responseSpec.schema.type` | 스키마의 데이터 유형을 정의합니다. | `object` |
| `responseSpec.schema.properties` | 스키마 내에 있는 열, 유형 및 항목에 대한 정보를 포함합니다. |
| `responseSpec.schema.properties.columns.items.properties.name` | 파일 이름을 표시합니다. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | 파일 이름의 데이터 유형을 정의합니다. | `string` |

{style=&quot;table-layout:auto&quot;}

## 다음 단계

탐색 세부 항목이 채워지면 을 사용하여 전체 연결 사양을 만들 수 있습니다. [!DNL Flow Service] API. 자세한 내용은 [셀프 서비스 소스(배치 SDK) API 안내서](../api/api-overview.md) 추가 정보.
