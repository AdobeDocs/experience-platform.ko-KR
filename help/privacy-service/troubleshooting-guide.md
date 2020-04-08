---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 개인 정보 서비스 FAQ
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 64cb2de507921fcb4aaade67132024a3fc0d3dee

---


# 개인 정보 서비스 FAQ

이 문서에서는 Adobe Experience Platform 개인 정보 보호 서비스에 대한 질문과 답변을 제공합니다.

개인정보 보호 서비스는 회사가 고객 데이터 개인 정보 보호 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 개인 정보 보호 서비스를 사용하면 개인 또는 개인 고객 데이터에 액세스하고 삭제할 것을 요청할 수 있으므로 조직 및 법적 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

## API 파섹 {#user-ids}

API에서 새로운 개인 정보 작업을 수행하기 위해 요청의 JSON 페이로드에 개인 정보 요청이 적용되는 각 사용자에 대한 특정 정보가 나열된 `users` 배열이 있어야 합니다. 배열의 각 항목은 해당 `users` `key` 값으로 식별된 특정 사용자를 나타내는 객체입니다.

따라서 각 사용자 객체(또는 `key`)에는 자체 `userIDs` 배열이 포함됩니다. 이 배열은 특정 사용자에 **대한 특정 ID 값을 나열합니다**.

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

이 배열에는 두 개의 개체가 포함되어 있으며, 이 개체는 `key` 값으로 식별된 개별 사용자를 나타냅니다(&quot;DavidSmith&quot; 및 &quot;user12345&quot;). &quot;DavidSmith&quot;에는 하나의 ID(이메일 주소)만 있는 반면 &quot;user12345&quot;에는 두 개의 ID(이메일 주소와 ECID)가 있습니다.

사용자 ID 정보를 제공하는 방법에 대한 자세한 내용은 개인 정보 요청에 [](identity-data.md)대한 ID 데이터에 대한 안내서를 참조하십시오.


## Privacy Service를 사용하여 실수로 Platform으로 전송된 데이터를 정리할 수 있습니까?

Adobe는 실수로 제품에 제출된 데이터를 지우는 데 개인정보 보호 서비스 사용을 지원하지 않습니다. 개인정보 보호 서비스는 데이터 주체(또는 소비자)의 액세스 또는 삭제 요청에 대한 귀하의 의무를 충족하도록 돕기 위해 고안되었습니다. 이러한 요청은 시간에 따라 처리되며 해당 개인정보 보호법과 관련하여 완료됩니다. 데이터 주체/소비자 액세스 또는 삭제 요청이 아닌 요청을 제출하면 모든 개인 정보 서비스 고객과 개인 정보 보호 서비스가 적절한 법적 일정을 지원할 수 있습니다.

CDM(계정 관리자)에 연락하여 PII 또는 데이터 문제를 해결하기 위한 노력을 조율하고 제공하십시오.

## 개인 정보 요청 또는 작업의 상태에 대한 정보는 어떻게 얻을 수 있습니까?

개인 정보 서비스 API 또는 사용자 인터페이스를 사용하여 특정 작업에 대한 세부 정보를 검색할 수 있습니다.

### API 사용

Privacy Service API를 사용하여 특정 작업의 상태를 검색하려면 요청 경로에서 작업 ID를 사용하여 루트(`GET /`) 끝점에 요청하십시오. 자세한 내용은 개인 정보 서비스 개발자 안내서의 작업 [상태](api/privacy-jobs.md#check-the-status-of-a-job) 확인 섹션을 참조하십시오.

### UI 사용

모든 활성 작업 요청은 개인정보 보호 서비스 **UI** 대시보드의 작업 요청 위젯에 나열됩니다. 각 작업 요청의 상태는 상태 **열 아래에** 표시됩니다. UI에서 작업 요청을 보는 방법에 대한 자세한 내용은 개인 정보 서비스 [사용 안내서를](ui/user-guide.md)참조하십시오.

## 완료된 개인 정보 보호 작업의 결과를 어떻게 다운로드합니까?

개인정보 보호 서비스 API와 사용자 인터페이스는 모두 완료된 작업의 결과를 ZIP 형식으로 다운로드하는 방법을 제공합니다.

### API 사용

요청 경로에서 다운로드할 결과의 ID를 사용하여 Privacy Service API의 루트(`GET /`) 끝점에 대한 요청을 합니다. 작업 상태가 완료되면 API는 응답 본문에 `downloadURL` 속성을 포함합니다. 이 속성에는 브라우저의 주소 표시줄에 붙여 넣어 ZIP 파일을 다운로드할 수 있는 URL이 포함되어 있습니다.

자세한 내용은 개인 정보 서비스 개발자 안내서의 해당 ID로 작업 [조회](api/privacy-jobs.md#check-the-status-of-a-job) 섹션을 참조하십시오.

### UI 사용

개인 정보 서비스 UI 대시보드에서 작업 요청 **위젯에서 다운로드할 작업을 찾습니다** . 작업 ID를 클릭하여 [작업 세부 정보] _페이지를 엽니다_ . 여기에서 오른쪽 **상단** 모서리의 다운로드를 클릭하여 ZIP 파일을 다운로드합니다. 자세한 [단계는 개인정보 보호 서비스 사용 안내서를](ui/user-guide.md) 참조하십시오.