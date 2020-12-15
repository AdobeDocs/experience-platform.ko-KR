---
keywords: Experience Platform;attribution ai;access scores;popular topics;download scores;attribution ai scores;export;Export
solution: Experience Platform, Intelligent Services
title: Attribution AI에서 점수 액세스
topic: Accessing scores
description: 이 문서는 Attribution AI의 스코어 다운로드 안내서 역할을 합니다.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 2%

---


# Attribution AI에서 스코어 다운로드

이 문서는 Attribution AI의 스코어 다운로드 안내서 역할을 합니다.

## 시작하기

Attribution AI을 사용하면 점수가 쪽모이 세공 마루 파일 형식으로 다운로드됩니다. 이 자습서에서는 시작하기 안내서에서 다운로드 Attribution AI 스코어 섹션을 [읽고 완료해야](./getting-started.md) 합니다.

또한 Attribution AI에 대한 점수에 액세스하려면 성공적인 실행 상태의 서비스 인스턴스를 사용할 수 있어야 합니다. 새 서비스 인스턴스를 만들려면 [Attribution AI 사용 안내서를 참조하십시오](./user-guide.md). 최근에 서비스 인스턴스를 만들었는데 여전히 트레이닝과 점수 지정 중이라면 24시간 후에 실행을 완료하십시오.

## Find your dataset ID {#dataset-id}

Attribution AI 인사이트를 위한 서비스 인스턴스 내에서 오른쪽 위 탐색 *에서 추가 작업* 드롭다운 메뉴를 클릭한 다음 **[!UICONTROL 액세스 점수를 선택합니다]**.

![추가 작업](./images/download-scores/more-actions.png)

다운로드 점수 설명서 및 현재 인스턴스의 데이터 세트 ID에 대한 링크가 포함된 새 대화 상자가 나타납니다. 데이터 세트 ID를 클립보드에 복사하고 다음 단계로 진행합니다.

![데이터 집합 ID](../customer-ai/images/download-scores/access-scores.png)

## 배치 ID 검색 {#retrieve-your-batch-id}

이전 단계에서 데이터 세트 ID를 사용하여 일괄 처리 ID를 검색하려면 카탈로그 API를 호출해야 합니다. 조직에 속한 배치 목록 대신 최근 성공적인 배치를 반환하기 위해 이 API 호출에 추가 쿼리 매개 변수가 사용됩니다. 추가 배치를 반환하려면 `limit` 쿼리 매개 변수의 숫자를 반환하려는 금액으로 늘리십시오. 사용 가능한 쿼리 매개 변수 유형에 대한 자세한 내용은 쿼리 매개 변수를 사용하여 카탈로그 데이터 [필터링 안내서를 참조하십시오](../../catalog/api/filter-data.md).

**API 형식**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{DATASET_ID}` | &quot;액세스 점수&quot; 대화 상자에서 사용할 수 있는 데이터 집합 ID. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 배치 ID 객체를 포함하는 페이로드를 반환합니다. 이 예에서 반환되는 객체에 대한 키 값은 일괄 처리 ID입니다 `01E5QSWCAASFQ054FNBKYV6TIQ`. 다음 API 호출에 사용할 배치 ID를 복사합니다.

>[!NOTE]
>
> 다음 응답에 가독성을 위해 `tags` 개체가 수정되었습니다.

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5e8f81cf7a4ecb28a8d85b22"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## 배치 ID로 다음 API 호출 검색 {#retrieve-the-next-api-call-with-your-batch-id}

배치 ID가 있으면 새 GET 요청을 만들 수 있습니다 `/batches`. 요청은 다음 API 요청으로 사용되는 링크를 반환합니다.

**API 형식**

```http
GET batches/{BATCH_ID}/files
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 이전 단계에서 검색한 배치 ID는 [배치 ID를 검색합니다](#retrieve-your-batch-id). |

**요청**

자신의 배치 ID를 사용하여 다음 요청을 수행합니다.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 객체가 포함된 페이로드를 `_links` 반환합니다. 객체 내 `_links` 는 새로운 API `href` 호출이 해당 값으로 되어 있습니다. 다음 단계로 진행하려면 이 값을 복사합니다.

```json
{
    "data": [
        {
            "dataSetFileId": "01E5QSWCAASFQ054FNBKYV6TIQ-1",
            "dataSetViewId": "5e8f81cf7a4ecb28a8d85b22",
            "version": "1.0.0",
            "created": "1586715582571",
            "updated": "1586715582571",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## 파일 검색 {#retrieving-your-files}

이전 단계에서 `href` 받은 값을 API 호출로 사용하여 파일 디렉토리를 검색할 새 GET 요청을 만듭니다.

**API 형식**

```http
GET files/{DATASETFILE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID는 `href` 이전 단계 [의](#retrieve-the-next-api-call-with-your-batch-id)값으로 반환됩니다. 객체 유형 아래의 `data` 배열에서 액세스할 수도 있습니다 `dataSetFileId`. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 단일 항목이 있거나 해당 디렉토리에 속하는 파일 목록이 있는 데이터 배열이 포함됩니다. 아래 예제는 파일 목록을 포함하며 가독성을 위해 압축되었습니다. 이 시나리오에서는 파일에 액세스하려면 각 파일의 URL을 따라야 합니다.

```json
{
    "data": [
        {
            "name": "part-00000-tid-5614147572541837832-908bd66a-d856-47fe-b7da-c8e7d22a4097-1370467-1.c000.snappy.parquet",
            "length": "2380211",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `_links.self.href` | 디렉토리에 파일을 다운로드하는 데 사용되는 GET 요청 URL입니다. |


배열에 `href` 있는 모든 파일 객체의 값을 `data` 복사한 다음 다음 다음 단계로 진행합니다.

## 파일 데이터 다운로드

파일 데이터를 다운로드하려면 이전 단계에서 복사한 `"href"` 값에 대해 GET을 요청하여 파일을 [검색합니다](#retrieving-your-files).

>[!NOTE]
>
>이 요청을 명령줄에서 직접 수행하는 경우 요청 헤더 뒤에 출력을 추가하라는 메시지가 표시될 수 있습니다. 다음 요청 예제에서는 를 사용합니다 `--output {FILENAME.FILETYPE}`.

**API 형식**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID는 `href` 이전 단계의 [값으로](#retrieve-the-next-api-call-with-your-batch-id)반환됩니다. |
| `{FILE_NAME}` | 파일의 이름입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>GET 요청을 하기 전에 파일을 저장할 디렉토리 또는 폴더에 있는지 확인합니다.

**응답**

그러면 요청한 파일이 현재 디렉토리에 다운로드됩니다. 이 예제에서 파일 이름은 &quot;file.portailed&quot;입니다.

![터미널](./images/download-scores/terminal-output.png)

다운로드한 점들은 쪽모이 세공 마룻바닥으로 되어 있으며, 점수를 보려면 [!DNL Spark]쉘 또는 쪽모이 세공 마루 판독기가 필요합니다. Raw 점수를 보려면 [쪽모이 세공된 도구를 사용할 수 있습니다](https://github.com/apache/parquet-mr/tree/master/parquet-tools). 쪽모이 세공된 도구는 데이터를 분석할 수 있습니다 [!DNL Spark].

## 다음 단계

이 문서에서는 Attribution AI 점수를 다운로드하는 데 필요한 단계를 간략하게 설명합니다. 점수 출력에 대한 자세한 내용은 [특성 AI 입력 및 출력](./input-output.md) 설명서를 참조하십시오.

## Snowflake을 사용하여 점수 액세스

>[!IMPORTANT]
>
>Snowflake을 사용하여 스코어에 액세스하는 방법에 대한 자세한 내용은 attributionai-support@adobe.com으로 문의하십시오.

Snowflake을 통해 집계된 Attribution AI 점수를 이용할 수 있습니다. 현재 Snowflake에 대한 자격 증명을 설정하고 Reader 계정에 수신하려면 attributionai-support@adobe.com에서 Adobe 지원을 이메일로 보내야 합니다.

Adobe 지원 기능이 요청을 처리하면 Snowflake에 대한 리더 계정의 URL과 아래 해당 자격 증명을 제공할 수 있습니다.

- Snowflake URL
- 사용자 이름
- 암호

>[!NOTE]
>
>reader 계정은 JDBC 커넥터를 지원하는 SQL 클라이언트, 워크시트 및 BI 솔루션을 사용하여 데이터를 쿼리하는 데 사용됩니다.

자격 증명과 URL이 있으면 터치포인트 날짜 또는 전환 날짜별로 집계된 모델 테이블을 쿼리할 수 있습니다.

### Snowflake에서 스키마 찾기

제공된 자격 증명을 사용하여 Snowflake에 로그인합니다. 왼쪽 **위** 주 탐색 메뉴에서 워크시트 탭을 클릭한 다음 왼쪽 패널에서 데이터베이스 디렉터리로 이동합니다.

![워크시트 및 탐색](./images/download-scores/edited_snowflake_1.png)

그런 다음 **화면** 오른쪽 상단 모서리에서 스키마 선택을 클릭합니다. 팝업 창에서 올바른 데이터베이스를 선택했는지 확인합니다. 그런 다음 *스키마* 드롭다운을 클릭하고 나열된 스키마 중 하나를 선택합니다. 선택한 스키마 아래에 나열된 점수 테이블에서 직접 쿼리할 수 있습니다.

![스키마 찾기](./images/download-scores/edited_snowflake_2.png)

## Snowflake에 PowerBI 연결(선택 사항)

Snowflake 자격 증명을 사용하여 PowerBI Desktop 및 Snowflake 데이터베이스 간의 연결을 설정할 수 있습니다.

먼저 *서버* 상자 아래에 Snowflake URL을 입력합니다. 그런 다음 *웨어하우스*&#x200B;아래에 &quot;XSMALL&quot;을 입력합니다. 그런 다음 사용자 이름과 암호를 입력합니다.

![POWERBI 예](./images/download-scores/powerbi-snowflake.png)

연결이 설정되면 Snowflake 데이터베이스를 선택한 다음 적절한 스키마를 선택합니다. 이제 모든 테이블을 로드할 수 있습니다.
