---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service FAQ
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---


# [!DNL Privacy Service] 문제 해결 안내서

Adobe Experience Platform [!DNL Privacy Service] 는 회사가 고객 데이터 개인 정보 보호 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 를 [!DNL Privacy Service]사용하면 개인 또는 개인 고객 데이터를 액세스하고 삭제하도록 요청하는 요청을 제출할 수 있으므로 조직 및 법률 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

이 문서에서는 API에서 자주 발생하는 오류에 대한 정보 [!DNL Privacy Service]및 FAQ에 대한 답변을 제공합니다.

## API에서 개인 정보 요청을 할 때 사용자와 사용자 ID의 차이점은 무엇입니까? {#user-ids}

API에서 새로운 개인정보 보호 작업을 수행하기 위해 요청의 JSON 페이로드에는 개인 정보 요청이 적용되는 각 사용자에 대한 특정 정보가 나열된 `users` 배열이 포함되어야 합니다. 배열의 각 항목 `users` 은 특정 사용자를 나타내는 개체로서, 해당 `key` 값으로 식별됩니다.

따라서 각 사용자 객체(또는 `key`)에는 자체 `userIDs` 배열이 포함됩니다. 이 배열은 특정 사용자 **에 대한 특정 ID 값을 나열합니다**.

Consider the following example `users` array:

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

이 배열에는 값(&quot;DavidSmith&quot; 및 &quot;user12345&quot;)으로 식별된 개별 사용자를 나타내는 두 개의 개체가 포함되어 있습니다. `key` &quot;DavidSmith&quot;에는 하나의 ID(이메일 주소)만 있는 반면 &quot;user12345&quot;에는 두 개의 ID(이메일 주소와 ECID)가 있습니다.

사용자 ID 정보를 제공하는 방법에 대한 자세한 내용은 개인 정보 요청에 대한 [ID 데이터에 대한 가이드를 참조하십시오](identity-data.md).


## 실수로 전송된 데이터 [!DNL Privacy Service] 를 정리할 수 있습니까 [!DNL Platform]?

Adobe은 실수로 제품에 제출된 데이터 [!DNL Privacy Service] 를 제거하는 데 사용하는 것을 지원하지 않습니다. [!DNL Privacy Service] 는 데이터 주체(또는 소비자) 액세스 또는 삭제 요청에 대한 귀하의 의무를 준수하도록 설계되었습니다. 이러한 요청은 시간에 따라 처리되며 해당 개인정보 보호법과 관련하여 완료됩니다. 데이터 주체/소비자 액세스 또는 삭제 요청이 아닌 요청을 제출하면 모든 [!DNL Privacy Service] 고객과 적절한 법정 일정 [!DNL Privacy Service] 을 지원할 수 있는 기능이 영향을 받습니다.

PII 또는 데이터 문제를 제거하기 위한 노력을 조정하고 제공하려면 계정 관리자(CDM)에 문의하십시오.

## 개인정보 보호 요청이나 일의 상태에 대한 정보는 어떻게 얻을 수 있습니까?

API 또는 사용자 인터페이스를 사용하여 특정 작업에 대한 세부 사항을 검색할 수 [!DNL Privacy Service] 있습니다.

### API 사용

API를 사용하여 특정 작업의 상태를 검색하려면 요청 경로에서 작업 ID를 사용하여 루트( [!DNL Privacy Service]`GET /`) 종단점에 요청을 하십시오. 자세한 내용은 개발자 안내서에서 작업 [상태](api/privacy-jobs.md#check-the-status-of-a-job) 확인 섹션을 [!DNL Privacy Service] 참조하십시오.

### UI 사용

모든 활성 작업 요청은 **[!UICONTROL UI 대시보드의]** 작업 요청 [!DNL Privacy Service] 위젯에 나열되어 있습니다. 각 작업 요청에 대한 상태가 **[!UICONTROL 상태]** 열 아래에 표시됩니다. UI에서 작업 요청을 보는 방법에 대한 자세한 내용은 [Privacy Service 사용 안내서를 참조하십시오](ui/user-guide.md).

## 완료된 개인 정보 보호 작업의 결과를 어떻게 다운로드합니까?

API와 [!DNL Privacy Service] 사용자 인터페이스는 완료된 작업 결과를 ZIP 형식으로 다운로드하는 방법을 제공합니다.

### API 사용

요청 경로에서 다운로드하려는 결과를 가진 작업의 ID를 사용하여`GET /`[!DNL Privacy Service] API의 루트() 끝점에 대한 요청을 수행하십시오. 작업의 상태가 완료되면 API는 응답 본문에 `downloadURL` 속성을 포함합니다. 이 속성에는 브라우저의 주소 표시줄에 붙여 넣어 ZIP 파일을 다운로드할 수 있는 URL이 포함되어 있습니다.

자세한 내용은 개발자 안내서에서 작업 [을 자신의 ID로](api/privacy-jobs.md#check-the-status-of-a-job) 조회하는 섹션 [!DNL Privacy Service] 을 참조하십시오.

### UI 사용

UI [!DNL Privacy Service] 대시보드에서 **작업 요청 위젯에서 다운로드할 작업을** 찾습니다. 작업 ID를 클릭하여 [작업 세부 정보] _페이지를_ 엽니다. 여기에서 오른쪽 **위** 모서리의 다운로드를 클릭하여 ZIP 파일을 다운로드합니다. 자세한 [단계는 Privacy Service 사용 안내서를](ui/user-guide.md) 참조하십시오.

## 일반적인 오류 메시지

다음 표에서는 해당 문제를 해결하는 데 도움이 되는 설명과 함께 몇 가지 일반적인 오류 [!DNL Privacy Service]에 대해 설명합니다.

| 오류 메시지 | 설명 |
| --- | --- |
| 사용자 ID를 찾을 수 없습니다. | 요청에 제공된 사용자 ID 중 일부를 찾을 수 없어 건너뛰었습니다. 요청 페이로드에서 올바른 네임스페이스 및 ID 값을 사용하고 있는지 확인합니다. 자세한 내용은 ID 데이터 [를](./identity-data.md) 제공하는 방법에 대한 문서를 참조하십시오. |
| 잘못된 네임스페이스 | 사용자 ID에 대해 제공된 ID 네임스페이스가 잘못되었습니다. 승인된 네임스페이스의 목록은 개발자 가이드 부칙의 [표준 ID 네임스페이스에](./api/appendix.md#standard-namespaces) 대한 섹션을 [!DNL Privacy Service] 참조하십시오. 사용자 지정 네임스페이스를 사용하는 경우 ID의 `type` 속성을 &quot;사용자 지정&quot;으로 설정해야 합니다. |
| 부분 완료 | 작업이 완료되었지만 일부 데이터는 지정된 요청에 적용되지 않아 건너뛰었습니다. |
| 데이터가 필요한 형식이 아닙니다. | 지정한 응용 프로그램의 데이터 값 중 하나 이상의 형식이 잘못되었습니다. 자세한 내용은 작업 세부 사항을 확인하십시오. |
| IMS 조직이 제공되지 않았습니다. | 이 메시지는 IMS 조직이 프로비저닝을 받지 않았을 때 발생합니다 [!DNL Privacy Service]. 자세한 내용은 관리자에게 문의하십시오. |
| 액세스 및 권한이 필요합니다. | 사용하려면 액세스 및 권한이 필요합니다 [!DNL Privacy Service]. 액세스 권한을 얻으려면 관리자에게 문의하십시오. |
| 액세스 데이터를 업로드하고 보관하는 데 문제가 있습니다. | 이 오류가 발생하면 액세스 데이터를 다시 업로드하고 다시 시도하십시오. |
| 현재 문서 속도 제한에 대한 작업 로드가 초과되었습니다. | 이 오류가 발생하면 제출 속도를 줄이고 다시 시도하십시오. |