---
keywords: 스트리밍, Qualtrics 대상
title: Qualtrics 자동화
description: 경험과 운영 고객 데이터를 동기화하여 규모에 맞게 개인화를 잠금 해제할 수 있습니다. Adobe Experience Platform의 여러 운영 데이터 소스의 집계를 Qualtrics Experience iD의 입력으로 사용하여 고객을 더 잘 이해하고 의도, 감정 및 경험 드라이버를 이해하는 데 있어 타깃팅된 전달을 통해 간극을 좁힐 수 있습니다.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 3%

---

# Qualtrics 자동화

## 개요 {#overview}

경험과 운영 고객 데이터를 동기화하여 규모에 맞게 개인화를 잠금 해제할 수 있습니다.

Adobe Experience Platform의 여러 운영 데이터 소스의 집계를 Qualtrics Experience iD의 입력으로 사용하여 고객을 더 잘 이해하고 의도, 감정 및 경험 드라이버를 이해하는 데 있어 타깃팅된 전달을 통해 간극을 좁힐 수 있습니다.

>[!IMPORTANT]
>
>대상 커넥터 및 설명서 페이지는 Qualtrics 팀에서 만들고 관리합니다. 문의 사항이나 업데이트 요청이 있으면 [고객 성공 허브](https://support-portal.qualtrics.com/)에 로그인하여 직접 문의하십시오.

## 사용 사례 {#use-cases}

*Qualtrics Automations* 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

### 사용 사례 #1 {#use-case-1}

**시나리오**: 회사에서 웹 사이트 및 모바일 앱과 같은 다양한 디지털 접점에서 고객 만족도를 측정하려고 합니다. Adobe Experience Platform을 사용하여 구매 완료 또는 특정 웹 페이지 방문과 같은 사용자 상호 작용에 따라 Qualtrics 설문 조사를 트리거합니다.

**결과**: 이 회사는 실시간 피드백을 수집하여 고객 경험에 대한 데이터 기반의 개선 사항을 만들어 만족도와 충성도를 높일 수 있습니다.

### 사용 사례 #2 {#use-case-2}

**시나리오**: 조직은 직원 온보딩 프로세스를 향상하는 것을 목표로 합니다. 이들은 Adobe Experience Platform을 활용하여 Qualtrics 설문 조사를 통해 신입 채용자들로부터 피드백을 수집한다. 설문 조사는 사전 정의된 온보딩 기간 후에 자동으로 트리거됩니다.

**성과**: 지속적인 피드백을 통해 조직은 온보딩 프로세스를 조정하고 개선할 수 있으므로 신입 직원 간의 참여도와 생산성이 향상됩니다.

## 전제 조건

Adobe Experience Platform에서 Qualtrics 대상을 설정하기 전에 다음 사전 요구 사항이 충족되었는지 확인하십시오.

* Qualtrics 계정이 있습니다.
* Qualtrics에서 필요한 API 토큰을 얻었습니다.

### API 토큰 가져오기

다음은 Qualtrics에서 API 토큰을 가져오는 데 필요한 단계입니다.

1. Qualtrics 계정에 로그인합니다.
2. **계정 설정**(으)로 이동합니다.
3. **Qualtrics ID**&#x200B;을(를) 선택하십시오.
4. 이 페이지에서 **API** 섹션을 찾습니다. 이 섹션에는 **Token** 필드가 있습니다. API 토큰이며 대상 설정 중에 필요합니다.

## 지원되는 ID {#supported-identities}

*Qualtrics 자동화*&#x200B;에서는 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| 이메일 | 일반 텍스트 이메일 주소 | Qualtrics에서는 일반 텍스트 이메일 주소만 지원합니다. |
| external_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스인 경우 이 대상 ID를 선택합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | *Qualtrics Automations* 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 세그먼트의 모든 구성원(대상)을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

인증의 일부로 **사용자 이름** 및 **암호**&#x200B;를 제공해야 합니다. 사용자 이름은 Qualtrics 사용자 이름이고 암호는 Qualtrics 계정의 API 토큰입니다. API 토큰을 검색하려면 위의 **필수 구성 요소** 섹션의 지침을 따르십시오.

![인증](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL URL]**: Qualtrics에서 [워크플로](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About)를 트리거하는 [JSON 이벤트](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About)에 있는 URL입니다. 예제는 아래 스크린샷 을 참조하십시오.

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 속성 및 ID 매핑 {#map}

이 대상에는 스키마가 열려 있으므로 모든 속성을 Qualtrics로 보낼 수 있습니다.

#### 속성 매핑

매핑에 특성을 추가하려면 새 매핑을 추가할 때 **사용자 지정 특성**&#x200B;을 선택하면 됩니다. 속성에 대한 이름을 입력할 수 있습니다. Qualtrics에서는 특성 이름에 대한 *camelCase* 명명 규칙을 권장합니다(예제는 아래 스크린샷 참조).

![사용자 지정 특성](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

가능한 속성 매핑의 예는 아래 스크린샷 을 참조하십시오.

![예제 매핑](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### ID 매핑

이 대상에 대한 ID 네임스페이스를 선택해야 합니다. 두 가지 가능한 소스 필드와 대상 필드 매핑은 다음과 같습니다.

| 소스 필드 | 대상 필드 |
|--------------------|-----------------------|
| IdentityMap: 이메일 | ID: 이메일 |
| IdentityMap: ECID | ID: external_id |

예제는 아래 스크린샷 을 참조하십시오.

![ID 네임스페이스](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

앞에서 언급했듯이 이 대상은 열린 스키마를 사용하므로 모든 속성을 Qualtrics로 전송할 수 있습니다. 그럼에도 불구하고 Qualtrics로 전송되는 데이터는 다음 구조를 따릅니다.

```json
{
  "person": {
    "name": {
      "firstName": "Dave"
    }
  },
  "mobilePhone": {
    "number": "0123456789"
  },
  "identityMap": {
    "Email": [
      {
        "id": "Email-2Sf6C"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "046456e3b-18e1-48a6-9bda-d68547861283": {
        "lastQualificationTime": "2023-09-05T10:43:55.602687Z",
        "status": "realized"
      },
      "007844dd1-9e5d-4531-a4ee-05470doe759dd": {
        "lastQualificationTime": "2023-09-05T10:43:55.602689Z",
        "status": "realized"
      }
    }
  }
}
```

Qualtrics에서 데이터가 수집되었는지 확인하려면 **JSON 이벤트**&#x200B;가 포함된 워크플로우로 이동하십시오. 해당 워크플로우에서 워크플로우 실행이 표시되는 **실행 내역**&#x200B;으로 이동하십시오. 각 워크플로의 상태는 **성공** 또는 **실패**&#x200B;입니다. 특정 실행을 선택하면 그에 대한 자세한 정보가 표시되며, 이로 인해 문제가 발생하는 경우 문제를 해결할 수 있습니다.

**실행 기록**&#x200B;에 표시되는 실행이 없는 경우 워크플로가 아직 트리거되지 않았음을 의미하며, 이는 문제가 있을 수 있음을 나타냅니다. 워크플로우가 활성화되어 있고 Adobe Experience Platform의 대상에 있는 **URL**&#x200B;이(가) 올바른지 확인하십시오. 워크플로우 실행은 즉시 수행되지 않으므로 완료되기 전에 잠시 기다려야 할 수 있습니다.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
