---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service 문제 해결 안내서
description: 이 문서에서는 Privacy Service에 대해 자주 묻는 질문에 대한 답변과 API에서 일반적으로 발생하는 오류에 대한 정보를 제공합니다.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---

# [!DNL Privacy Service] 문제 해결 안내서

Adobe Experience Platform [!DNL Privacy Service] 는 회사가 고객 데이터 개인 정보 보호 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 사용 [!DNL Privacy Service]을(를) 사용하면 개인 또는 개인 고객 데이터에 대한 액세스 및 삭제 요청을 제출할 수 있으므로, 조직 및 법적 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

이 문서에서는 [!DNL Privacy Service]뿐만 아니라 API에서 일반적으로 발생하는 오류에 대한 정보도 제공합니다.

## API에서 개인 정보 요청을 수행할 때 사용자와 사용자 ID의 차이점은 무엇입니까? {#user-ids}

API에서 새 개인 정보 작업을 수행하려면 요청의 JSON 페이로드에 가 포함되어야 합니다 `users` 개인 정보 보호 요청이 적용되는 각 사용자의 특정 정보를 나열하는 배열입니다. 의 각 항목 `users` 배열은 로 식별되는 특정 사용자를 나타내는 객체입니다 `key` 값.

각 사용자 개체(또는 `key`)에는 자체 포함되어 있습니다 `userIDs` 배열입니다. 이 배열에 특정 ID 값이 나열됩니다 **해당 특정 사용자**.

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

이 배열에는 두 개의 객체가 포함되어 있으며, 이 두 개의 객체는 각 객체가 식별한 개별 사용자를 나타냅니다 `key` 값(&quot;DavidSmith&quot; 및 &quot;user12345&quot;). &quot;DavidSmith&quot;에는 한 개의 나열된 ID(해당 이메일 주소)만 있지만 &quot;user12345&quot;에는 두 개의(이메일 주소와 ECID)가 있습니다.

사용자 ID 정보 제공에 대한 자세한 내용은 [개인 정보 보호 요청에 대한 id 데이터](identity-data.md).


## 사용할 수 있나요 [!DNL Privacy Service] 에 실수로 전송된 데이터를 정리하려면 [!DNL Platform]?

Adobe이 [!DNL Privacy Service] 실수로 제품에 제출된 데이터를 지우는 데 사용됩니다. [!DNL Privacy Service] 는 데이터 주체(또는 소비자) 액세스 또는 삭제 요청에 대한 의무를 충족하도록 지원하기 위해 고안되었습니다. 데이터 정리 또는 유지 관리에 대한 다른 Privacy Service 사용은 지원되거나 허용되지 않습니다.

개인 정보 보호 요청은 시간에 따라 처리되며, 해당 개인 정보 보호법과 관련하여 완료됩니다. 데이터 주체/소비자 액세스 또는 삭제 요청이 아닌 요청 제출은 모든 영향을 줍니다. [!DNL Privacy Service] 고객 및 [!DNL Privacy Service] 적절한 법적 일정을 지원하기 위해 서비스 남용을 방지하기 위해 이제 하루 동안 하드 업로드 제한이 적용됩니다.

PII 또는 데이터 문제를 제거하기 위한 노력을 조정하고 제공하려면 Adobe 계정 팀에 문의하십시오.

## 개인 정보 보호 요청 또는 작업의 상태에 대한 정보를 가져오려면 어떻게 해야 합니까?

를 사용하여 특정 작업에 대한 세부 사항을 검색할 수 있습니다 [!DNL Privacy Service] API 또는 사용자 인터페이스.

### API 사용

를 사용하여 특정 작업의 상태를 검색하려면 [!DNL Privacy Service] API, 루트에 요청(`GET /`) 종단점에 도달합니다. 자세한 내용은 [작업 상태 확인](api/privacy-jobs.md#check-the-status-of-a-job) 에서 [!DNL Privacy Service] API 안내서.

### UI 사용

모든 활성 작업 요청은 **[!UICONTROL 작업 요청]** 위젯 [!DNL Privacy Service] UI 대시보드. 각 작업 요청의 상태는 **[!UICONTROL 상태]** 열. UI에서 작업 요청을 보는 방법에 대한 자세한 내용은 [Privacy Service 사용 안내서](ui/user-guide.md).

## 완료된 개인 정보 작업의 결과는 어떻게 다운로드합니까?

다음 [!DNL Privacy Service] API와 사용자 인터페이스는 모두 완료된 작업 결과를 ZIP 형식으로 다운로드하는 방법을 제공합니다.

### API 사용

루트에 요청(`GET /`) 종단점 [!DNL Privacy Service] 요청 경로에 결과를 다운로드할 작업의 ID를 사용하는 API입니다. 작업 상태가 완료되면 API에 `downloadURL` 속성을 반환합니다. 이 속성에는 ZIP 파일을 다운로드할 수 있도록 브라우저의 주소 표시줄에 붙여넣을 수 있는 URL이 포함되어 있습니다.

자세한 내용은 [해당 ID로 작업 조회](api/privacy-jobs.md#check-the-status-of-a-job) 에서 [!DNL Privacy Service] API 안내서.

### UI 사용

설정 [!DNL Privacy Service] UI 대시보드에서 다운로드할 작업을 찾습니다 **작업 요청** 위젯. 작업의 ID를 선택하여 [작업 세부 정보] 페이지를 엽니다. 여기에서 을 선택합니다. **다운로드** 오른쪽 상단 모서리에서 ZIP 파일을 다운로드합니다. 자세한 내용은 [Privacy Service 사용 안내서](ui/user-guide.md) 를 참조하십시오.

## 일반 오류 메시지

다음 표에서는 일반적인 [!DNL Privacy Service], 각각의 문제를 해결하는 데 도움이 되는 설명 포함.

| 오류 메시지 | 설명 |
| --- | --- |
| 사용자 ID를 찾을 수 없습니다. | 요청에 제공된 일부 사용자 ID를 찾을 수 없으며 건너뛰었습니다. 요청 페이로드에서 올바른 네임스페이스 및 ID 값을 사용하고 있는지 확인하십시오. 다음 문서를 참조하십시오. [id 데이터 제공](./identity-data.md) 자세한 설명을 위해 |
| 잘못된 네임스페이스 | 사용자 ID에 대해 제공된 ID 네임스페이스가 잘못되었습니다. 의 섹션을 참조하십시오. [표준 id 네임스페이스](./api/appendix.md#standard-namespaces) 에서 [!DNL Privacy Service] 허용되는 네임스페이스 목록은 API 안내서 부록 을 참조하십시오. 사용자 지정 네임스페이스를 사용하는 경우 ID의 `type` 속성을 &quot;custom&quot;에 추가합니다. |
| 부분적으로 완료됨 | 작업이 완료되었지만 일부 데이터는 지정된 요청에 적용할 수 없으며 건너뛰었습니다. |
| 데이터가 필요한 형식이 아닙니다. | 지정한 응용 프로그램의 데이터 값 중 하나 이상의 형식이 잘못되었습니다. 자세한 내용은 작업 세부 사항을 확인하십시오. |
| IMS 조직이 프로비저닝되지 않았습니다. | 이 메시지는 조직이 프로비저닝되지 않은 경우에 발생합니다 [!DNL Privacy Service]. 자세한 내용은 관리자에게 문의하십시오. |
| 액세스 및 권한이 필요합니다. | 사용하려면 액세스 및 권한이 필요합니다 [!DNL Privacy Service]. 액세스 권한을 얻으려면 관리자에게 문의하십시오. |
| 액세스 데이터를 업로드하고 보관하는 동안 문제가 발생했습니다. | 이 오류가 발생하면 액세스 데이터를 다시 업로드하고 다시 시도하십시오. |
| 현재 문서 비율 제한에 대해 작업 로드가 초과되었습니다. | 이 오류가 발생하면 제출 속도를 줄이고 다시 시도하십시오. |
