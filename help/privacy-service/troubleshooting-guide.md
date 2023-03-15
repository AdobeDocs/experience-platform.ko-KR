---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service 문제 해결 안내서
description: 이 문서에서는 Privacy Service에 대해 자주 묻는 질문에 대한 답변과 API에서 일반적으로 발생하는 오류에 대한 정보를 제공합니다.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 1%

---

# [!DNL Privacy Service] 문제 해결 안내서

Adobe Experience Platform [!DNL Privacy Service] 는 회사가 고객 데이터 개인 정보 보호 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 포함 [!DNL Privacy Service], 개인 또는 개인 고객 데이터에 대한 액세스 및 삭제 요청을 제출하여 조직 및 법적 개인정보 보호 규정을 자동으로 준수할 수 있습니다.

이 문서에서는 다음에 대한 FAQ에 대한 답변을 제공합니다 [!DNL Privacy Service]: API에서 일반적으로 발생하는 오류에 대한 정보입니다.

## API에서 개인 정보 요청을 할 때 사용자와 사용자 ID의 차이점은 무엇입니까? {#user-ids}

API에서 새 개인 정보 작업을 수행하려면 요청의 JSON 페이로드에 `users` 개인 정보 보호 요청이 적용되는 각 사용자에 대한 특정 정보를 나열하는 배열입니다. 의 각 항목 `users` array는 특정 사용자를 나타내는 객체로, 해당 사용자에 의해 식별됩니다 `key` 값.

차례로 각 사용자 개체(또는 `key`) 자체 포함 `userIDs` 배열입니다. 이 배열에는 특정 ID 값이 나열됩니다. **특정 사용자 1명**.

다음 예를 생각해 보십시오 `users` 배열:

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

배열에는 개체로 식별되는 개별 사용자를 나타내는 두 개의 개체가 포함됩니다 `key` 값(&quot;DavidSmith&quot; 및 &quot;user12345&quot;). &quot;DavidSmith&quot;에는 하나의 나열된 ID(이메일 주소)만 있는 반면, &quot;user12345&quot;에는 두 개의 ID(이메일 주소 및 ECID)가 있습니다.

사용자 ID 정보 제공에 대한 자세한 내용은 [개인 정보 보호 요청에 대한 id 데이터](identity-data.md).


## 사용할 수 있습니까 [!DNL Privacy Service] 실수로 로 전송된 데이터를 정리하려면 [!DNL Platform]?

Adobe은 을 지원하지 않습니다. [!DNL Privacy Service] 실수로 제품에 제출된 데이터를 지웁니다. [!DNL Privacy Service] 는 데이터 주체(또는 소비자) 액세스 또는 삭제 요청에 대한 귀하의 의무를 준수하는 데 도움이 되도록 설계되었습니다. 이러한 요청은 시간에 민감하며 해당 개인정보 보호법과 관련하여 완료됩니다. 데이터 주체/소비자 액세스 또는 삭제 요청이 아닌 요청을 제출하면 모든 사용자에게 영향을 미칩니다. [!DNL Privacy Service] 고객 및 기능 [!DNL Privacy Service] 적절한 법적 기한 준수

계정 관리자에게 문의(CDM)하여 PII 또는 데이터 문제를 없애는 데 필요한 노력을 조율하고 제공하십시오.

## 개인 정보 보호 요청 또는 작업 상태에 대한 정보를 얻으려면 어떻게 해야 합니까?

다음을 사용하여 특정 작업에 대한 세부 정보를 검색할 수 있습니다. [!DNL Privacy Service] API 또는 사용자 인터페이스.

### API 사용

를 사용하여 특정 작업의 상태를 검색하려면 [!DNL Privacy Service] API, 루트(`GET /`) 엔드포인트, 요청 경로에 있는 작업의 ID 사용. 자세한 내용은 의 섹션을 참조하십시오. [작업 상태 확인](api/privacy-jobs.md#check-the-status-of-a-job) 다음에서 [!DNL Privacy Service] API 안내서.

### UI 사용

모든 활성 작업 요청이 **[!UICONTROL 작업 요청]** 의 위젯 [!DNL Privacy Service] UI 대시보드. 각 작업 요청의 상태는 아래에 표시됩니다. **[!UICONTROL 상태]** 열. UI에서 작업 요청을 보는 방법에 대한 자세한 내용은 [Privacy Service 사용 안내서](ui/user-guide.md).

## 완료된 개인 정보 작업의 결과를 다운로드하려면 어떻게 해야 합니까?

다음 [!DNL Privacy Service] API 및 사용자 인터페이스는 모두 완료된 작업의 결과를 ZIP 형식으로 다운로드하는 방법을 제공합니다.

### API 사용

루트에 요청(`GET /`)의 엔드포인트 [!DNL Privacy Service] 요청 경로에서 다운로드할 결과의 작업 ID를 사용하는 API. 작업 상태가 완료되면 API에 `downloadURL` 응답 본문의 속성입니다. 이 속성에는 브라우저의 주소 표시줄에 붙여넣어 ZIP 파일을 다운로드할 수 있는 URL이 포함되어 있습니다.

자세한 내용은 의 섹션을 참조하십시오. [ID로 작업 조회](api/privacy-jobs.md#check-the-status-of-a-job) 다음에서 [!DNL Privacy Service] API 안내서.

### UI 사용

다음에서 [!DNL Privacy Service] UI 대시보드에서 다운로드할 작업을 찾습니다. **작업 요청** 위젯. 작업 ID를 선택하여 [작업 세부 정보] 페이지를 엽니다. 여기에서 다음을 선택합니다. **다운로드** 오른쪽 상단 모서리에서 ZIP 파일을 다운로드합니다. 다음을 참조하십시오. [Privacy Service 사용 안내서](ui/user-guide.md) 을 참조하십시오.

## 일반 오류 메시지

다음 표에서 몇 가지 일반적인 오류를 간략하게 설명합니다. [!DNL Privacy Service], 각각의 문제를 해결하는 데 도움이 되는 설명 포함.

| 오류 메시지 | 설명 |
| --- | --- |
| 사용자 ID를 찾을 수 없습니다. | 요청에 입력한 사용자 ID 중 일부를 찾을 수 없어 건너뛰었습니다. 요청 페이로드에서 올바른 네임스페이스 및 ID 값을 사용하고 있는지 확인합니다. 다음에 대한 문서 보기: [id 데이터 제공](./identity-data.md) 더 자세한 설명을 위해 |
| 잘못된 네임스페이스 | 사용자 ID에 대해 입력한 ID 네임스페이스가 잘못되었습니다. 의 섹션을 참조하십시오. [표준 id 네임스페이스](./api/appendix.md#standard-namespaces) 다음에서 [!DNL Privacy Service] 허용되는 네임스페이스 목록에 대한 API 안내서 부록. 사용자 지정 네임스페이스를 사용하는 경우 ID를 `type` 속성을 &quot;custom&quot;으로 바꿉니다. |
| 부분적으로 완료됨 | 작업이 성공적으로 완료되었지만 일부 데이터가 해당 요청에 적용할 수 없어 건너뜁니다. |
| 데이터가 필수 포맷이 아닙니다. | 지정한 응용 프로그램에 대한 하나 이상의 데이터 값의 형식이 잘못되었습니다. 자세한 내용은 작업 세부 사항을 확인하십시오. |
| IMS Org는 프로비저닝되지 않습니다. | 이 메시지는 IMS 조직이 프로비저닝되지 않은 경우에 발생합니다 [!DNL Privacy Service]. 자세한 내용은 관리자에게 문의하십시오. |
| 액세스 및 권한이 필요합니다. | 을 사용하려면 액세스 및 권한이 필요합니다. [!DNL Privacy Service]. 액세스 권한을 얻으려면 관리자에게 문의하십시오. |
| 액세스 데이터를 업로드하고 보관하는 도중 문제가 발생했습니다. | 이 오류가 발생하면 액세스 데이터를 다시 업로드하고 다시 시도하십시오. |
| 작업량이 현재 문서 속도 제한을 초과했습니다. | 이 오류가 발생하면 전송 속도를 줄이고 다시 시도하십시오. |
