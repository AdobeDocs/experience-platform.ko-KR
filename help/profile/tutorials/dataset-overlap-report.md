---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;보고;데이터 세트 중복 보고서;프로필 데이터
title: 데이터 집합 Overlap Reports 생성
type: Tutorial
description: 이 자습서에서는 실시간 고객 프로필 API를 사용하여 데이터 집합 겹치기 보고서를 생성하는 데 필요한 단계를 설명합니다.
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---

# 데이터 집합 중복 보고서 생성

데이터 집합 겹치기 보고서는 조직의 구성 요소에 대한 가시성을 제공합니다 [!DNL Profile] 는 대응 가능 대상(프로필)에 가장 많이 기여하는 데이터 세트를 노출하여 저장합니다.

이 보고서를 통해 데이터에 대한 통찰력을 제공할 수 있을 뿐만 아니라 특정 데이터의 수명 제한 설정과 같은 라이선스 사용을 최적화하는 작업을 수행할 수도 있습니다.

이 자습서에서는 [!DNL Real-Time Customer Profile] API를 사용하여 조직의 결과를 해석합니다.

## 시작하기

Adobe Experience Platform API를 사용하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en) 를 입력하여 필요한 헤더에 필요한 값을 수집합니다. Experience Platform API에 대한 자세한 내용은 [platform API 설명서 시작하기](../../landing/api-guide.md).

이 자습서의 모든 API 호출에 대한 필수 헤더는 다음과 같습니다.

* `Authorization: Bearer {ACCESS_TOKEN}`: 다음 `Authorization` 헤더에는 단어 앞에 액세스 토큰이 있어야 합니다 `Bearer`. 24시간마다 새 액세스 토큰 값을 생성해야 합니다.
* `x-api-key: {API_KEY}`: 다음 `API Key` 이라고도 합니다. `Client ID` 및 은(는) 한 번만 생성해야 하는 값입니다.
* `x-gw-ims-org-id: {ORG_ID}`: 다음 `IMS Org` 이라고도 합니다 `Organization ID` 한 번만 생성해야 합니다.

인증 자습서를 완료하고 필수 헤더에 대한 값을 수집한 후 실시간 고객 API를 호출할 준비가 되었습니다.

## 명령줄에서 데이터 집합 겹치기 보고서 생성

명령줄 사용에 익숙한 경우 다음 cURL 요청을 사용하여에 GET 요청을 수행하여 데이터 집합 겹침 보고서를 생성할 수 있습니다 `/previewsamplestatus/report/dataset/overlap`.

**요청**

다음 요청에서는 `date` 매개 변수를 사용하여 지정된 날짜에 대한 최신 보고서를 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| 매개 변수 | 설명 |
|---|---|
| `date` | 보고서 반환 날짜를 지정합니다. 날짜에 여러 개의 보고서가 실행된 경우 해당 날짜에 대한 최신 보고서가 반환됩니다. 지정된 날짜에 대한 보고서가 없으면 HTTP 상태 404(찾을 수 없음) 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. 형식: YYYY-MM-DD. 예: `date=2024-12-31` |

**응답**

요청이 성공하면 HTTP 상태 200(OK) 및 데이터 집합 겹치기 보고서를 반환합니다. 이 보고서에는 `data` 쉼표로 구분된 데이터 세트 목록과 각 프로필 수를 포함하는 개체. 보고서를 읽는 방법에 대한 자세한 내용은 [데이터 집합 중복 보고서 데이터 해석](#interpret-the-report) 이 자습서의 뒷부분에서 확인하십시오.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### Postman을 사용하여 데이터 집합 중복 보고서 생성

Postman은 API 개발을 위한 공동 작업 플랫폼이며 API 호출 시각화에 유용합니다. 에서 무료로 다운로드할 수 있습니다 [Postman 웹 사이트](https://www.postman.com) 및 는 API 호출을 수행하는 데 사용하기 쉬운 UI를 제공합니다. 다음 스크린샷에서는 Postman 인터페이스를 사용합니다.

**요청**

Postman을 사용하여 데이터 집합 중복 보고서를 요청하려면 다음 단계를 완료하십시오.

* 드롭다운을 사용하여 GET을 요청 유형으로 선택합니다.
* 에 필요한 헤더를 입력합니다. `KEY` 열:
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* 인증 중에 생성한 값을 `VALUE` 열, 중괄호 바꾸기(`{{ }}`)과 함께 사용할 수 있습니다.
* 선택 사항을 사용하거나 사용하지 않고 요청 경로를 입력합니다 `date` 매개 변수:
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   또는
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| 매개 변수 | 설명 |
|---|---|
| `date` | 보고서 반환 날짜를 지정합니다. 날짜에 여러 개의 보고서가 실행된 경우 해당 날짜에 대한 최신 보고서가 반환됩니다. 지정된 날짜에 대한 보고서가 없으면 HTTP 상태 404(찾을 수 없음) 오류가 반환됩니다. 날짜를 지정하지 않으면 가장 최근 보고서가 반환됩니다. <br/>형식: YYYY-MM-DD. 예: `date=2024-12-31` |

요청 유형, 헤더, 값 및 경로가 완료되면 을 선택합니다 **보내기** api 요청을 보내고 보고서를 생성합니다.

![](../images/dataset-overlap-report/postman-request.png)

**응답**

요청이 성공하면 HTTP 상태 200(OK) 및 데이터 집합 겹치기 보고서를 반환합니다. 이 보고서에는 `data` 쉼표로 구분된 데이터 세트 목록과 각 프로필 수를 포함하는 개체. 보고서를 읽는 방법에 대한 자세한 내용은 [데이터 집합 중복 보고서 데이터 해석](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## 데이터 집합 중복 보고서 데이터 해석 {#interpret-the-report}

생성된 데이터 세트 겹치기 보고서는 보고서의 날짜 및 시간을 표시하는 타임스탬프와 데이터 세트 ID의 고유한 조합을 쉼표로 구분된 목록으로 포함하는 데이터 개체를 제공합니다. 다음 섹션에서는 보고서 구성 요소에 대한 추가 정보를 제공합니다.

### 보고서 타임스탬프

다음 `reportTimestamp` API 요청에 제공된 날짜와 일치하거나 제공된 날짜가 없는 경우 가장 최근 보고서의 타임스탬프를 일치시킵니다.

### 데이터 세트 ID 목록

다음 `data` 개체에는 데이터 세트 ID의 고유한 조합이 포함되어 있으며, 해당 데이터 세트 조합에 대한 각 프로필 카운트가 있는 쉼표로 구분된 목록이 포함되어 있습니다.

>[!NOTE]
>
>데이터 집합 중복 보고서의 각 행과 연결된 모든 프로필 수의 합은 조직의 총 프로필 수와 같아야 합니다.

보고서의 결과를 해석하려면 다음 예를 생각해 보십시오.

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

이 보고서는 다음 정보를 제공합니다.

* 다음 데이터 세트에서 전송되는 데이터로 구성된 프로필이 123개 있습니다. `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* 다음 두 데이터 세트에서 전송되는 데이터로 구성된 454,412개의 프로필이 있습니다. `5d92921872831c163452edc8` 및 `5eb2cdc6fa3f9a18a7592a98`.
* 데이터 세트의 데이터만 포함된 107개의 프로필이 있습니다 `5eeda0032af7bb19162172a7`.
* 조직에 총 454,642개의 프로필이 있습니다.

## 다음 단계

이제 이 자습서를 완료한 후 실시간 고객 프로필 API를 사용하여 데이터 세트 겹치기 보고서를 생성할 수 있습니다. API와 Experience Platform UI 모두에서 프로필 데이터 작업에 대한 자세한 내용은 [프로필 개요 설명서](../home.md).
