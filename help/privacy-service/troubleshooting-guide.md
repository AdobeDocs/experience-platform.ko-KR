---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service 문제 해결 안내서
description: 이 문서에서는 Privacy Service에 대해 자주 묻는 질문에 대한 답변과 API에서 일반적으로 발생하는 오류에 대한 정보를 제공합니다.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 4%

---

# [!DNL Privacy Service] 문제 해결 안내서

Adobe Experience Platform [!DNL Privacy Service]은(는) 회사가 고객 데이터 개인 정보 보호 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. [!DNL Privacy Service]을(를) 사용하면 개인 또는 개인 고객 데이터 액세스 및 삭제 요청을 제출하여 조직 및 법적 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

이 문서에서는 [!DNL Privacy Service]에 대해 자주 묻는 질문에 대한 답변과 API에서 일반적으로 발생하는 오류에 대한 정보를 제공합니다.

## API에서 개인 정보 요청을 할 때 사용자와 사용자 ID의 차이점은 무엇입니까? {#user-ids}

API에서 새 개인 정보 작업을 수행하려면 요청의 JSON 페이로드에 개인 정보 요청이 적용되는 각 사용자에 대한 특정 정보를 나열하는 `users` 배열이 포함되어 있어야 합니다. `users` 배열의 각 항목은 특정 사용자를 나타내는 개체로, 해당 `key` 값으로 식별됩니다.

각 사용자 개체(또는 `key`)에는 고유한 `userIDs` 배열이 포함되어 있습니다. 이 배열은 특정 사용자 **에 대한 특정 ID 값**&#x200B;을(를) 나열합니다.

다음 예제 `users` 배열을 고려하십시오.

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

배열에는 `key` 값으로 식별되는 개별 사용자(&quot;DavidSmith&quot; 및 &quot;user12345&quot;)를 나타내는 두 개의 개체가 포함되어 있습니다. &quot;DavidSmith&quot;에는 하나의 나열된 ID(이메일 주소)만 있는 반면, &quot;user12345&quot;에는 두 개의 ID(이메일 주소 및 ECID)가 있습니다.

사용자 ID 정보 제공에 대한 자세한 내용은 [개인 정보 요청을 위한 ID 데이터](identity-data.md)에 대한 안내서를 참조하십시오.


## [!DNL Privacy Service]을(를) 사용하여 실수로 [!DNL Platform]에 전송된 데이터를 정리할 수 있습니까?

Adobe은 실수로 제품에 제출된 데이터를 지우는 데 [!DNL Privacy Service]을(를) 사용할 수 없습니다. [!DNL Privacy Service]은(는) 데이터 주체(또는 소비자) 액세스 또는 삭제 요청에 대한 사용자의 의무를 준수하는 데 도움이 되도록 설계되었습니다. 데이터 정리 또는 유지 관리를 위한 다른 Privacy Service 사용은 지원되지 않거나 허용되지 않습니다.

개인 정보 보호 요청은 시간에 민감하며 해당 개인 정보 보호법과 관련하여 완료됩니다. 데이터 주체/소비자 액세스 또는 삭제 요청이 아닌 요청을 제출하면 모든 [!DNL Privacy Service] 고객과 [!DNL Privacy Service]이(가) 적절한 법적 타임라인을 지원할 수 있는 기능에 영향을 줍니다. 이제 서비스 남용을 방지하기 위해 엄격한 일일 업로드 제한이 적용됩니다.

PII 또는 데이터 문제를 해결하기 위한 노력을 조정하고 제공하려면 Adobe 계정 팀에 문의하십시오.

## 개인 정보 보호 요청 또는 작업 상태에 대한 정보를 얻으려면 어떻게 해야 합니까?

[!DNL Privacy Service] API 또는 사용자 인터페이스를 사용하여 특정 작업에 대한 세부 정보를 검색할 수 있습니다.

### API 사용

[!DNL Privacy Service] API를 사용하여 특정 작업의 상태를 검색하려면 요청 경로에서 작업 ID를 사용하여 루트(`GET /`) 끝점에 요청합니다. 자세한 내용은 [!DNL Privacy Service] API 안내서에서 [작업 상태 확인](api/privacy-jobs.md#check-the-status-of-a-job)의 섹션을 참조하십시오.

### UI 사용

모든 활성 작업 요청은 [!DNL Privacy Service] UI 대시보드의 **[!UICONTROL 작업 요청]** 위젯에 나열됩니다. 각 작업 요청의 상태가 **[!UICONTROL 상태]** 열 아래에 표시됩니다. UI에서 작업 요청을 보는 방법에 대한 자세한 내용은 [Privacy Service 사용 안내서](ui/user-guide.md)를 참조하십시오.

## 완료된 개인 정보 작업의 결과를 다운로드하려면 어떻게 해야 합니까?

[!DNL Privacy Service] API 및 사용자 인터페이스는 모두 완료된 작업의 결과를 ZIP 형식으로 다운로드하는 방법을 제공합니다.

### API 사용

요청 경로에서 결과를 다운로드하려는 작업의 ID를 사용하여 [!DNL Privacy Service] API의 루트(`GET /`) 끝점에 요청합니다. 작업 상태가 완료되면 API는 응답 본문에 `downloadURL` 특성을 포함합니다. 이 속성에는 브라우저의 주소 표시줄에 붙여넣어 ZIP 파일을 다운로드할 수 있는 URL이 포함되어 있습니다.

자세한 내용은 [!DNL Privacy Service] API 안내서의 [ID로 작업 조회](api/privacy-jobs.md#check-the-status-of-a-job)에 대한 섹션을 참조하십시오.

### UI 사용

[!DNL Privacy Service] UI 대시보드의 **작업 요청** 위젯에서 다운로드할 작업을 찾습니다. 작업 ID를 선택하여 [작업 세부 정보] 페이지를 엽니다. 여기에서 오른쪽 상단의 **다운로드**&#x200B;를 선택하여 ZIP 파일을 다운로드합니다. 자세한 단계는 [Privacy Service 사용 안내서](ui/user-guide.md)를 참조하세요.

## 일반적인 오류 메시지 {#common-error-messages}

다음 표에는 각 문제를 해결하는 데 도움이 되는 설명과 함께 [!DNL Privacy Service]의 몇 가지 일반적인 오류가 간략하게 나와 있습니다.

| 오류 메시지 | 설명 |
| --- | --- |
| 사용자 ID를 찾을 수 없습니다. | 요청에 입력한 사용자 ID 중 일부를 찾을 수 없어 건너뛰었습니다. 요청 페이로드에서 올바른 네임스페이스 및 ID 값을 사용하고 있는지 확인합니다. 자세한 내용은 [ID 데이터 제공](./identity-data.md)에 대한 문서를 참조하십시오. |
| 잘못된 네임스페이스 | 사용자 ID에 대해 입력한 ID 네임스페이스가 잘못되었습니다. 허용되는 네임스페이스 목록은 [!DNL Privacy Service] API 안내서 부록의 [표준 ID 네임스페이스](./api/appendix.md#standard-namespaces)에 대한 섹션을 참조하십시오. 사용자 지정 네임스페이스를 사용하는 경우 ID의 `type` 속성을 &quot;custom&quot;으로 설정해야 합니다. |
| 부분적으로 완료됨 | 작업이 성공적으로 완료되었지만 일부 데이터가 해당 요청에 적용할 수 없어 건너뜁니다. |
| 데이터가 필수 포맷이 아닙니다. | 지정한 응용 프로그램에 대한 하나 이상의 데이터 값의 형식이 잘못되었습니다. 자세한 내용은 작업 세부 사항을 확인하십시오. |
| IMS 조직이 프로비저닝되지 않았습니다. | 이 메시지는 조직에 [!DNL Privacy Service]이(가) 제공되지 않은 경우 발생합니다. 자세한 내용은 관리자에게 문의하십시오. |
| 액세스와 권한이 필요합니다. | [!DNL Privacy Service]을(를) 사용하려면 액세스 및 권한이 필요합니다. 액세스 권한을 얻으려면 관리자에게 문의하십시오. |
| 액세스 데이터를 업로드하고 보관하는 도중 문제가 발생했습니다. | 이 오류가 발생하면 액세스 데이터를 다시 업로드하고 다시 시도하십시오. |
| 작업량이 현재 문서 속도 제한을 초과했습니다. | 이 오류가 발생하면 전송 속도를 줄이고 다시 시도하십시오. |
| 요청이 너무 많음<br>(HTTP 429 오류) | 제출 패턴이 허용된 데이터 주체 작업의 모니터링되는 제한을 초과하는 경우 조직의 지속적인 트래픽에 대한 응답으로 HTTP 429 오류가 표시됩니다. Privacy Service은 데이터 주체 개인 정보 보호 요청 처리를 위한 것입니다. 데이터 정리에 사용되지 않습니다. HTTP 429 오류가 발생하면 Adobe을 합법적인 규정 준수 작업의 위험에 빠뜨릴 수 있는 남용으로부터 보호하기 위해 제한 및 요청 제한이 구현됩니다.<br>데이터 집합 만료 일정을 설정](../hygiene/ui/dataset-expiration.md)하고 [레코드 삭제 기능](../hygiene/ui/record-delete.md)을 사용하여 데이터를 최소화하는 다른 방법을 제공합니다. [ 이러한 기능을 적용하는 방법에 대한 자세한 내용은 해당 설명서를 참조하십시오. |
