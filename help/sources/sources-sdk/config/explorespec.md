---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 셀프서비스 소스에 대한 세부 항목 탐색(일괄 SDK)
description: 이 문서에서는 셀프서비스 소스(Batch SDK)를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# 셀프서비스 소스에 대한 세부 항목 탐색(일괄 SDK)

탐색 사양에서는 소스에 포함된 객체를 탐색하고 검사하는 데 필요한 매개변수를 정의합니다. 또한 Explore 사양은 개체를 탐색하고 검사할 때 반환되는 응답 형식을 정의합니다.

>[!TIP]
>
>탐색 사양은 하드 코딩되어 있으며 아래 페이로드를 복사하여 연결 사양에 붙여넣을 수 있습니다.

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

| 사양 살펴보기 | 설명 | 예 |
| --- | --- | --- |
| `name` | 탐색 사양의 이름 또는 식별자를 정의합니다. | `Resource` |
| `type` | 탐색 사양의 유형을 정의합니다. | `Resource` |
| `requestSpec` | 연결에서 개체를 탐색하는 데 필요한 매개 변수를 포함합니다. |
| `requestSpec.type` | 요청 사양의 데이터 유형을 정의합니다. | `object` |
| `responseSpec` | 탐색 호출에 대해 반환되는 응답 메시지의 형식을 정의하는 매개 변수를 포함합니다. |
| `responseSpec.type` | 응답 사양의 데이터 유형을 정의합니다. | `object` |
| `responseSpec.properties` | 응답 메시지의 형식 지정과 관련된 정보를 포함합니다. |
| `responseSpec.properties.format` | 응답 스키마의 형식을 정의합니다. | `object` |
| `responseSpec.properties.format.type` | 속성의 데이터 형식을 정의합니다. | `string` |
| `responseSpec.schema` | 응답 스키마 형식 지정 방법에 대한 정보를 포함합니다. |
| `responseSpec.schema.type` | 스키마의 데이터 유형을 정의합니다. | `object` |
| `responseSpec.schema.properties` | 스키마 내에 있는 열, 유형 및 항목에 대한 정보를 포함합니다. |
| `responseSpec.schema.properties.columns.items.properties.name` | 파일 이름을 표시합니다. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | 파일 이름의 데이터 형식을 정의합니다. | `string` |

{style="table-layout:auto"}

## 다음 단계

탐색 사양을 채운 상태에서 를 사용하여 전체 연결 사양을 생성할 수 있습니다. [!DNL Flow Service] API. 다음을 참조하십시오. [셀프서비스 소스(일괄 처리 SDK) API 안내서](../api/api-overview.md) 추가 정보.
