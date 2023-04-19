---
keywords: Experience Platform;시작하기;컨텐츠;컨텐츠 태깅 ai;키워드 태깅;키워드 태깅
solution: Experience Platform
title: 컨텐츠 태깅 API의 키워드 태깅
description: 키워드 태깅 서비스는 텍스트 문서가 지정된 경우 문서의 주제를 가장 잘 설명하는 키워드 또는 키워드 구문을 자동으로 추출합니다. 키워드를 추출하기 위해 명명된 엔티티 인식(NER) 및 비감독 키워드 태그 지정 알고리즘의 조합이 사용됩니다.
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: 7c8c1d69f4c4e0a1374603d541b634ac7f64ab38
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 5%

---

# 키워드 태깅

텍스트 문서가 지정된 경우 키워드 태그 지정 서비스는 문서의 주제를 가장 잘 설명하는 키워드 또는 키 구문을 자동으로 추출합니다. 키워드를 추출하기 위해 명명된 엔티티 인식(NER) 및 비감독 키워드 태그 지정 알고리즘의 조합이 사용됩니다.

다음 표에는 [!DNL Content Tagging] 다음을 식별할 수 있습니다.

| 엔티티 이름 | 설명 |
| --- | --- |
| 개인 | 허구적인 사람들을 포함해서 |
| GPE | 국가, 도시 및 주. |
| LOC | GPE가 아닌 위치, 산맥, 물의 시체. |
| FAC | 건물, 공항, 고속도로, 다리 등 |
| 조직 | 회사, 기관, 기관 등 |
| 제품 | 물체, 차량, 식품 등 (서비스 아님) |
| 이벤트 | 이름이 허리케인, 전투, 전쟁, 스포츠 행사 등입니다. |
| WORK_OF_ART | 책, 노래 등의 제목 |
| 법률 | 법으로 만들어진 명명된 문서. |
| 언어 | 이름이 지정된 언어 |

**API 형식**

```http
POST /services/v2/predict
```

**요청**

다음 요청은 페이로드에 제공된 입력 매개 변수를 기반으로 문서에서 키워드를 추출합니다.

표시된 입력 매개 변수에 대한 자세한 내용은 예제 페이로드 아래의 표를 참조하십시오.

이 [샘플 pdf](../pdf-files/simple-text.pdf) 이 문서에 표시된 예제에서 파일이 사용되었습니다.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "test",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-ner:Service-1e9081c865214d1e8bace51dd918b5c0"
      },
      "sensei:inputs": {
        "documents": [
          {
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "application/pdf"
          }
        ]
      },
      "sensei:params": {
        "application-id": "1234",
        "min_key_phrase_length": 1,
        "max_key_phrase_length": 3,
        "top_n": 5,
        "last_semantic_unit_type": "concept"
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@simple-text.pdf'
```

**입력 매개 변수**

| 속성 | 설명 | 필수입니다 |
| --- | --- | --- |
| `top_n` | 반환할 결과 수입니다. 0, 모든 결과를 반환합니다. 임계값과 함께 사용하는 경우 반환되는 결과 수가 두 제한 값보다 작습니다. | 아니요 |
| `min_relevance` | 결과를 반환해야 하는 점수 임계값입니다. 모든 결과를 반환하려면 매개 변수를 제외하십시오. | 아니요 |
| `min_key_phrase_length` | 주요 구문에 필요한 최소 단어 수입니다. | 아니요 |
| `max_key_phrase_length` | 주요 구문에 필요한 최대 단어 수입니다. | 아니요 |
| `last_semantic_unit_type` | 계층 응답에서 지정된 수준까지 의미 단위만 반환합니다. &quot;key_phrase&quot;는 키 구문만 반환하고, &quot;linked_entity&quot;는 키 구문과 해당 연결된 엔티티만 반환하고, &quot;concept&quot;는 키 구문, 연결된 엔티티 및 개념을 반환합니다. | 아니요 |
| `entity_types` | 주요 구문으로 반환될 엔티티 유형입니다. | 아니요 |

**문서 객체**

| 이름 | 데이터 형식 | 필수 여부 | 기본값 | 값 | 설명 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 문자열 | - | - | - | 키 구문을 추출할 문서의 사전 서명된 URL입니다. |
| `sensei:repoType` | 문자열 | - | - | HTTPS | 문서가 저장되는 리포지토리 유형입니다. |
| `sensei:multipart_field_name` | 문자열 | - | - | - | 사전 서명된 URL을 사용하는 대신 문서를 다중 부분 인수로 전달할 때 이를 사용합니다. |
| `dc:format` | 문자열 | 예 | - | &quot;text/plain&quot;,<br>&quot;application/pdf&quot;,<br>&quot;text/pdf&quot;,<br>&quot;text/html&quot;,<br>&quot;text/rtf&quot;,<br>&quot;application/rtf&quot;,<br>&quot;application/msword&quot;,<br>&quot;application/vnd.openxmlformats-office.wordprocessingml.document&quot;,<br>&quot;application/mspowerpoint&quot;,<br>&quot;application/vnd.ms-powerpoint&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.presentationml&quot; | 문서 인코딩은 처리 전에 허용되는 입력 인코딩 유형에 대해 확인됩니다. |

**응답**

성공적인 응답은 `response` 배열입니다.

```json
{
  [
  {
    "key_phrases": [
      {
        "name": "Canada",
        "type": "GPE",
        "relevance": 0.9525035277863068,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Canada",
          "id": "b27a82e6-e963-45de-add8-dc4f3f0dd399",
          "confidence": 1.0,
          "relevance": 0.9706433035237365,
          "concepts": [
            {
              "name": "Commonwealth realm",
              "relationship": "instance_of",
              "id": "f5354ab6-ad25-406a-b289-9209db0db8ea",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "sovereign state",
              "relationship": "instance_of",
              "id": "10c24191-beef-43cc-a823-c170f217fe12",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "dominion of the British Empire",
              "relationship": "instance_of",
              "id": "4ffabaee-e6ab-422d-b121-145dcdbcf427",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "country",
              "relationship": "instance_of",
              "id": "6e8f43cb-7e64-41fc-93b4-119adfe87926",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "North America",
              "relationship": "part_of",
              "id": "0f4b1f78-9681-414a-91c6-576ed643941a",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            }
          ]
        }
      },
      {
        "name": "Sherlock Homles",
        "type": "ENTITY_UNKNOWN_TYPE",
        "relevance": 0.9516463011782174,
        "confidence": 1.0,
        "linked_entity": null
      },
      {
        "name": "Albert Einstein",
        "type": "PERSON",
        "relevance": 0.95080732382989,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Albert Einstein",
          "id": "0fdb37f6-f575-4b4d-91e9-fbff57eae0ab",
          "confidence": 1.0,
          "relevance": 0.9695742180192723,
          "concepts": [
            {
              "name": "pedagogue",
              "relationship": "occupation",
              "id": "1439eb14-2988-43cc-865d-ad5a60d3ea62",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "philosopher of science",
              "relationship": "occupation",
              "id": "eefb9bbf-e617-4434-abb2-56b5853abd3a",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "university teacher",
              "relationship": "occupation",
              "id": "bb2c4745-4116-46ef-a122-c28c2f902026",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "science writer",
              "relationship": "occupation",
              "id": "5084431d-9073-45cb-be82-4a6898becd5b",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "non-fiction writer",
              "relationship": "occupation",
              "id": "57cc1f7b-5391-458b-9303-ec35b3ba01a4",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "patent examiner",
              "relationship": "occupation",
              "id": "d3f10fc5-ca81-4049-8c48-3d935552d9e7",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "philosopher",
              "relationship": "occupation",
              "id": "04d3cd32-68ad-4b71-9231-bdf3acfb09b2",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "scientist",
              "relationship": "occupation",
              "id": "dc8c068b-aa75-4ece-acd7-06fa304964fb",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "physicist",
              "relationship": "occupation",
              "id": "56ac942c-12a2-42c1-b10c-d1394a7971af",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "teacher",
              "relationship": "occupation",
              "id": "c70301bd-bcf4-47ab-b958-b983f0b0a6bd",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "human",
              "relationship": "instance_of",
              "id": "ead8a1d7-f901-44e6-b80f-63ebbbca4ffe",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "professor",
              "relationship": "occupation",
              "id": "c6d691f2-1e26-49fd-8481-58cb2d64d3e9",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "mathematician",
              "relationship": "occupation",
              "id": "23bf46db-a69a-4546-b18a-690a41144caa",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "theoretical physics",
              "relationship": "field_of_work",
              "id": "d6c03027-4efd-49d6-a7e5-ac4994c9143e",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "theoretical physicist",
              "relationship": "occupation",
              "id": "eedb6531-c2bf-4d05-af92-6f21751bc894",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "inventor",
              "relationship": "occupation",
              "id": "7baf322e-5913-4e2a-997a-90a039b0ff5c",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "writer",
              "relationship": "occupation",
              "id": "4c4c287c-0d83-4da3-b8c7-26df5adc9b33",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            }
          ]
        }
      },
      {
        "name": "Toronto",
        "type": "GPE",
        "relevance": 0.9370046727951885,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Toronto",
          "id": "762db630-b272-4828-b1af-e7c65334e1d3",
          "confidence": 1.0,
          "relevance": 0.9608202651283239,
          "concepts": [
            {
              "name": "provincial or territorial capital city in Canada",
              "relationship": "instance_of",
              "id": "d7447629-e940-43b1-a726-4ac3f675410c",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "city",
              "relationship": "instance_of",
              "id": "d9d95c34-a2ce-4098-bd9d-3616b85620a8",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "big city",
              "relationship": "instance_of",
              "id": "68275742-3451-40af-8f5a-84211953a438",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "single-tier municipality",
              "relationship": "instance_of",
              "id": "a0f67ef3-52bb-44d9-bc52-9059d37c6d0c",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "city with millions of inhabitants",
              "relationship": "instance_of",
              "id": "b08def76-4b71-4545-9efb-f4858aaf253d",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            }
          ]
        }
      },
      {
        "name": "vacation",
        "type": "KEY_PHRASE",
        "relevance": 0.933964522339908,
        "confidence": 1.0,
        "linked_entity": null
      }
    ],
    "detected_languages": [
      {
        "language": "en",
        "confidence": 0.9999951616458576
      }
    ],
    "word_count": 183
  }
]   
}
```
