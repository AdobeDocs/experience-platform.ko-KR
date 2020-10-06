---
keywords: text classification;Text classification
solution: Experience Platform
title: 텍스트 분류 API 끝점
topic: Developer guide
description: 텍스트 분류 서비스는 텍스트 조각이 주어지면 하나 이상의 레이블로 분류할 수 있습니다. 분류는 단일 레이블, 다중 레이블 또는 계층일 수 있습니다.
translation-type: tm+mt
source-git-commit: 09200be6eb078ecbefc91c6449373f811b602797
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 4%

---


# 텍스트 분류

>[!NOTE]
>
>Content and Commerce AI가 베타 버전입니다. 설명서는 변경될 수 있습니다.

텍스트 분류 서비스는 텍스트 조각이 주어지면 하나 이상의 레이블로 분류할 수 있습니다. 분류는 단일 레이블, 다중 레이블 또는 계층일 수 있습니다.

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 요청은 페이로드에서 제공하는 입력 매개 변수를 기반으로 조각에서 텍스트를 분류합니다. 표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래 표를 참조하십시오.

>[!CAUTION]
>
>`analyzer_id` 사용할 항목 [!DNL Sensei Content Framework] 을 결정합니다. 요청하기 `analyzer_id` 전에 적절한 것이 있는지 확인하십시오. 이 서비스를 받으려면 콘텐츠 및 커머스 AI 베타 팀 `analyzer_id` 에 문의하십시오.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\", 
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"Server and Workstation Processors, Microcode Update is a self-extracting executable file containing the latest beta microcode updates (System Configuration Data) and software license agreement.\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
         "parameters": {}
    }]
}'
```

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `analyzer_id` | 요청이 배포된 [!DNL Sensei] 서비스 ID. 이 ID는 어떤 것이 사용되는지 [!DNL Sensei Content Frameworks] 를 결정합니다. 사용자 지정 서비스의 경우 콘텐츠 및 커머스 AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 만든 응용 프로그램의 ID입니다. | 예 |
| `data` | 문서를 나타내는 배열에 각 개체가 있는 JSON 개체가 포함된 배열입니다. 이 배열의 일부로 전달되는 모든 매개 변수는 배열 외부에 지정된 전역 매개 변수를 `data` 무시합니다. 이 표에 나와 있는 나머지 속성은 내에서 재정의할 수 있습니다 `data`. | 예 |
| `language` | 입력 텍스트 언어 기본값은 `en`입니다. | 아니요 |
| `content-type` | 입력이 요청 본체의 일부인지 또는 S3 버킷에 대해 서명된 URL인지 나타내는 데 사용됩니다. 이 속성의 기본값은 입니다 `inline`. | 아니요 |
| `encoding` | 입력 텍스트의 인코딩 형식입니다. 이것은 `utf-8` 또는 `utf-16`. 이 속성의 기본값은 입니다 `utf-8`. | 아니요 |
| `threshold` | 결과를 반환해야 하는 상단의 점수(0-1)입니다. 값을 사용하여 모든 결과 `0` 를 반환합니다. 이 속성의 기본값은 입니다 `0`. | 아니요 |
| `top-N` | 반환할 결과 수(음수일 수 없음) 값을 사용하여 모든 결과 `0` 를 반환합니다. 이와 함께 사용할 경우 반환되는 결과 `threshold`의 수가 두 제한 중 더 적습니다. 이 속성의 기본값은 입니다 `0`. | 아니요 |
| `custom` | 전달할 사용자 지정 매개 변수입니다. 이 속성을 사용하려면 유효한 JSON 개체가 있어야 합니다. | 아니요 |
| `content-id` | 응답에서 반환된 데이터 요소의 고유 ID. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 텍스트 분류 서비스에서 사용하는 컨텐츠입니다. 컨텐츠는 원시 텍스트(&#39;인라인&#39; 컨텐츠 유형)일 수 있습니다. <br> 컨텐츠가 S3(&#39;s3-bucket&#39; content-type)에 있는 파일인 경우 서명된 url을 전달합니다. | 예 |

**응답**

성공적인 응답으로 분류된 텍스트를 응답 배열로 반환합니다.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_name": "abc123",
            "feature_value": [
              {
                "feature_value": [
                  {
                    "feature_value": 0.6899315714836121,
                    "feature_name": "Embedded & IoT"
                  }
                ],
                "feature_name": "labels"
              },
              {
                "feature_name": "status",
                "feature_value": "success"
              }
            ]
          }
        ]
      }
    }
  ],
  "error": []
}
```
