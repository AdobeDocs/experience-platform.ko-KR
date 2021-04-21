---
keywords: Experience Platform;시작하기;컨텐트 ai;커머스 ai;컨텐트 및 커머스 ai;키워드 추출;키워드 추출;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;keyword extraction
solution: Experience Platform, Intelligent Services
title: 컨텐츠 및 상거래 AI API의 키워드 추출
topic-legacy: Developer guide
description: 키워드 추출 서비스는 텍스트 문서가 지정된 경우 문서의 제목을 가장 잘 설명하는 키워드 또는 키구를 자동으로 추출합니다. 키워드를 추출하기 위해 명명된 엔티티 인식(NER) 및 비감독 키워드 추출 알고리즘의 조합이 사용됩니다.
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 3%

---

# 키워드 추출

>[!NOTE]
>
>[!DNL Content and Commerce AI] 베타 버전임 설명서는 변경될 수 있습니다.

키워드 추출 서비스는 텍스트 문서가 지정된 경우 문서의 제목을 가장 잘 설명하는 키워드 또는 키구를 자동으로 추출합니다. 키워드를 추출하기 위해 명명된 엔티티 인식(NER) 및 비감독 키워드 추출 알고리즘의 조합이 사용됩니다.

[!DNL Content and Commerce AI]에서 인식하는 명명된 엔티티는 다음 표에 나열되어 있습니다.

| 엔티티 이름 | 설명 |
| --- | --- |
| 개인 | 허구까지 포함해서 |
| NORP | 국적 또는 종교 또는 정치 집단. |
| GPE | 국가, 도시 및 주. |
| LOC | 비GPE 위치, 산간, 물의 신체. |
| FAC | 건물, 공항, 고속도로, 다리 등 |
| ORG | 회사, 기관, 기관 등 |
| 제품 | 물체, 차량, 식품 등 (서비스 아님) |
| EVENT | 이름이 허리케인, 전투, 전쟁, 스포츠 행사 등입니다. |
| WORK_OF_ART | 책, 노래 등의 제목 |
| 법률 | 법으로 지정된 문서 |
| 언어 | 이름이 지정된 언어 |

>[!NOTE]
>
>PDF 처리를 계획하는 경우 이 문서 내의 [PDF 키워드 추출](#pdf-extraction)에 대한 지침에 따릅니다. 또한 docx, ppt, amd xml과 같은 추가 파일 유형에 대한 지원은 나중 날짜에 해제되도록 설정됩니다.

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 요청은 페이로드에서 제공하는 입력 매개 변수를 기반으로 문서에서 키워드를 추출합니다.

입력 파일의 간소화된 JSON:

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래 표를 참조하십시오.

>[!CAUTION]
>
>`analyzer_id` 사용할 항목 [!DNL Sensei Content Framework] 을 결정합니다. 요청을 하기 전에 적절한 `analyzer_id`이 있는지 확인하십시오. 키워드 추출 서비스의 경우 `analyzer_id` ID는 다음과 같습니다.
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

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
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
         "parameters": {}
    }]
}'
```

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `analyzer_id` | 요청이 배포된 [!DNL Sensei] 서비스 ID. 이 ID는 [!DNL Sensei Content Frameworks] 중 어느 것이 사용되는지 결정합니다. 사용자 지정 서비스의 경우 콘텐츠 및 상거래 AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 만든 응용 프로그램의 ID. | 예 |
| `data` | 문서를 나타내는 배열에 각 객체가 포함된 JSON 객체가 포함된 배열입니다. 이 배열의 일부로 전달되는 모든 매개 변수는 `data` 배열 외부에 지정된 전역 매개 변수를 무시합니다. 이 표에 나와 있는 나머지 속성은 `data` 내에서 재정의할 수 있습니다. | 예 |
| `language` | 입력 텍스트 언어 기본값은 `en`입니다. | 아니요 |
| `content-type` | 입력이 요청 본문과 S3 버킷에 대한 서명된 URL인지 여부를 나타내는 데 사용됩니다. 이 속성의 기본값은 `inline`입니다. | 예 |
| `encoding` | 입력 텍스트의 인코딩 형식입니다. 이것은 `utf-8` 또는 `utf-16`일 수 있습니다. 이 속성의 기본값은 `utf-8`입니다. | 아니요 |
| `threshold` | 결과를 반환해야 하는 점수(0~1)의 임계값. 모든 결과를 반환하려면 `0` 값을 사용합니다. 이 속성의 기본값은 `0`입니다. | 아니요 |
| `top-N` | 반환할 결과 수입니다(음수가 될 수 없음). 모든 결과를 반환하려면 `0` 값을 사용합니다. `threshold`과 함께 사용할 경우 반환되는 결과 수가 두 제한 중 하나 보다 적습니다. 이 속성의 기본값은 `0`입니다. | 아니요 |
| `custom` | 전달할 사용자 지정 매개 변수입니다. 이 속성을 사용하려면 유효한 JSON 개체가 있어야 합니다. 사용자 지정 매개 변수에 대한 자세한 내용은 [부록](#appendix)을 참조하십시오. | 아니요 |
| `content-id` | 응답에서 반환된 데이터 요소의 고유 ID. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 키워드 추출 서비스에서 사용되는 컨텐츠. 컨텐츠는 원시 텍스트(&#39;인라인&#39; 컨텐츠 유형)일 수 있습니다. <br> 내용이 S3(&#39;s3-bucket&#39; content-type)의 파일인 경우, 서명된 URL을 전달합니다. 컨텐츠가 요청 본문의 일부인 경우 데이터 요소 목록에는 하나의 객체만 있어야 합니다. 두 개 이상의 객체가 전달되면 첫 번째 객체만 처리됩니다. | 예 |

**응답**

성공적인 응답은 `response` 배열에 추출된 키워드를 포함하는 JSON 개체를 반환합니다.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## PDF 키워드 추출 {#pdf-extraction}

키워드 추출 서비스는 PDF를 지원하지만 PDF 파일에 새로운 AnalyzerID를 사용하고 문서 유형을 PDF로 변경해야 합니다. 자세한 내용은 아래 예를 참조하십시오.

**API 형식**

```http
POST /services/v1/predict
```

**요청**

다음 요청은 페이로드에서 제공하는 입력 매개 변수를 기반으로 PDF 문서에서 키워드를 추출합니다.

>[!CAUTION]
>
>`analyzer_id` 사용할 항목 [!DNL Sensei Content Framework] 을 결정합니다. 요청을 하기 전에 적절한 `analyzer_id`이 있는지 확인하십시오. PDF 키워드 추출의 경우 `analyzer_id` ID:
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `analyzer_id` | 요청이 배포된 [!DNL Sensei] 서비스 ID. 이 ID는 [!DNL Sensei Content Frameworks] 중 어느 것이 사용되는지 결정합니다. 사용자 지정 서비스의 경우 콘텐츠 및 상거래 AI 팀에 문의하여 사용자 지정 ID를 설정하십시오. | 예 |
| `application-id` | 만든 응용 프로그램의 ID. | 예 |
| `data` | 문서를 나타내는 배열에 각 객체가 포함된 JSON 객체가 포함된 배열입니다. 이 배열의 일부로 전달되는 모든 매개 변수는 `data` 배열 외부에 지정된 전역 매개 변수를 무시합니다. 이 표에 나와 있는 나머지 속성은 `data` 내에서 재정의할 수 있습니다. | 예 |
| `language` | 입력 언어. 기본값은 `en`(영어)입니다. | 아니요 |
| `content-type` | 입력 내용 유형을 나타내는 데 사용됩니다. 이 값은 `file`으로 설정해야 합니다. | 예 |
| `encoding` | 입력의 인코딩 형식입니다. 이 값은 `pdf`으로 설정해야 합니다. 더 많은 인코딩 유형은 나중에 지원되도록 설정됩니다. | 예 |
| `threshold` | 결과를 반환해야 하는 점수(0~1)의 임계값. 모든 결과를 반환하려면 `0` 값을 사용합니다. 이 속성의 기본값은 `0`입니다. | 아니요 |
| `top-N` | 반환할 결과 수입니다(음수가 될 수 없음). 모든 결과를 반환하려면 `0` 값을 사용합니다. `threshold`과 함께 사용할 경우 반환되는 결과 수가 두 제한 중 하나 보다 적습니다. 이 속성의 기본값은 `0`입니다. | 아니요 |
| `custom` | 전달할 사용자 지정 매개 변수입니다. 이 속성을 사용하려면 유효한 JSON 개체가 있어야 합니다. 사용자 지정 매개 변수에 대한 자세한 내용은 [부록](#appendix)을 참조하십시오. | 아니요 |
| `content-id` | 응답에서 반환된 데이터 요소의 고유 ID. 이 값이 전달되지 않으면 자동 생성된 ID가 할당됩니다. | 아니요 |
| `content` | 이 값은 `file`으로 설정해야 합니다. | 예 |

**응답**

성공적인 응답은 `response` 배열에 추출된 키워드를 포함하는 JSON 개체를 반환합니다.

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
                  }
                ],
                "feature_name": "abc123"
              }
            ]
          }
        }
      ],
      "error": []
    }
  }
}
```

AEM 클라우드 서비스의 설정, 배포 및 통합 방법에 대한 지침이 포함된 PDF 추출 사용에 대한 자세한 내용 및 샘플을 보려면 [CCAI PDF 추출 작업자 github](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract)를 방문하십시오.

## 부록 {#appendix}

다음 표에는 `custom` 내에서 사용할 수 있는 매개 변수가 포함되어 있습니다.

| 이름 | 설명 | 필수입니다 |
| --- | --- | --- |
| `min-n` | 키워드에 필요한 최소 단어 수입니다. | 아니요 |
| `entity-types` | 반환할 엔티티 유형. 이 문서의 시작 부분에 있는 명명된 엔티티 인식 표를 참조하십시오. | 아니요 |
