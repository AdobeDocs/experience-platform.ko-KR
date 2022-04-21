---
title: (베타) HTTP API 연결
keywords: 스트리밍;
description: Adobe Experience Platform의 HTTP API 대상을 사용하면 프로필 데이터를 타사 HTTP 엔드포인트로 보낼 수 있습니다.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: c62117de27b150f072731c910bb0593ce1fca082
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 1%

---

# (베타) HTTP API 연결

>[!IMPORTANT]
>
>Platform의 HTTP API 대상은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

HTTP API 대상은 [!DNL Adobe Experience Platform] 프로필 데이터를 타사 HTTP 종단점으로 보내는 데 도움이 되는 스트리밍 대상입니다.

프로필 데이터를 HTTP 끝점으로 보내려면 먼저 해야 합니다 [대상에 연결](#connect-destination) in [!DNL Adobe Experience Platform].

## 사용 사례 {#use-cases}

HTTP 대상은 XDM 프로필 데이터 및 대상 세그먼트를 일반 HTTP 종단점으로 내보내야 하는 고객을 대상으로 합니다.

HTTP 엔드포인트는 고객의 시스템 또는 타사 솔루션일 수 있습니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 전자 메일 주소, 전화 번호, 성)을 선택한 대로 [대상 활성화 워크플로우](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 전제 조건 {#prerequisites}

>[!IMPORTANT]
>
>회사에 대해 HTTP API 대상 베타 기능을 활성화하려면 Adobe 담당자 또는 Adobe 고객 지원 팀에 문의하십시오.

HTTP API 대상을 사용하여 Experience Platform에서 데이터를 내보내려면 다음 사전 요구 사항을 충족해야 합니다.

* REST API를 지원하는 HTTP 엔드포인트가 있어야 합니다.
* HTTP 종단점은 Experience Platform 프로필 스키마를 지원해야 합니다. HTTP API 대상에서 타사 페이로드 스키마에 대한 변환이 지원되지 않습니다. 자세한 내용은 [내보낸 데이터](#exported-data) Experience Platform 출력 스키마의 예를 보려면 섹션을 참조하십시오.
* HTTP 끝점은 헤더를 지원해야 합니다.
* HTTP 종단점은 을 지원해야 합니다 [OAuth 2.0 클라이언트 자격 증명](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 인증. HTTP API 대상이 베타 단계에 있는 동안 이 요구 사항이 유효합니다.
* 아래 예와 같이 클라이언트 자격 증명은 엔드포인트에 대한 POST 요청 본문에 포함해야 합니다.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

를 사용할 수도 있습니다 [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) 통합을 설정하고 Experience Platform 프로필 데이터를 HTTP 엔드포인트로 보냅니다.

## IP 주소 허용 목록에 추가하다 {#ip-address-allowlist}

고객의 보안 및 규정 준수 요구 사항을 충족하기 위해 Experience Platform은 HTTP API 대상에 대해 검색할 수 허용 목록에 추가하다 있는 정적 IP 목록을 제공합니다. 을(를) 참조하십시오. [스트리밍 대상을 위한 IP 주소 허용 목록](/help/destinations/catalog/streaming/ip-address-allow-list.md) 을 클릭하여 검색할 IP의 전체 목록을 허용 목록에 추가하다 확인합니다.

## 대상에 연결 {#connect-destination}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="클라이언트 자격 증명 유형"
>abstract="선택 **본문 양식 인코딩됨** 클라이언트 ID 및 클라이언트 암호를 요청 본문에 포함하려면 **기본 인증** 인증 헤더에 클라이언트 ID 및 클라이언트 암호를 포함하기 위해 설명서에서 예를 봅니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="헤더"
>abstract="다음 형식을 사용하여 대상 호출에 포함할 사용자 지정 헤더를 입력합니다. `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP 끝점"
>abstract="프로필 데이터를 보낼 HTTP 끝점의 URL입니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="세그먼트 이름 포함"
>abstract="데이터 내보내기에 내보낼 세그먼트의 이름이 포함되도록 하려면 전환합니다. 이 옵션을 선택한 상태로 데이터 내보내기 예제에 대한 설명서를 봅니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="세그먼트 타임스탬프 포함"
>abstract="세그먼트가 생성 및 업데이트될 때 데이터 내보내기에 UNIX 타임스탬프와 세그먼트가 활성화 대상에 매핑될 때 UNIX 타임스탬프를 포함하려면 을 전환합니다. 이 옵션을 선택한 상태로 데이터 내보내기 예제에 대한 설명서를 봅니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="쿼리 매개 변수"
>abstract="선택적으로 HTTP 엔드포인트 URL에 쿼리 매개 변수를 추가할 수 있습니다. 다음과 같이 사용하는 쿼리 매개 변수의 형식을 지정합니다. `parameter1=value&parameter2=value`."

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL httpEndpoint]**: a [!DNL URL] 프로필 데이터를 보낼 HTTP 끝점입니다.
   * 선택적으로 쿼리 매개 변수를 [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: a [!DNL URL] 에 사용되는 HTTP 끝점의 [!DNL OAuth2] 인증.
* **[!UICONTROL 클라이언트 ID]**: a [!DNL clientID] 에 사용된 매개 변수 [!DNL OAuth2] 클라이언트 자격 증명입니다.
* **[!UICONTROL 클라이언트 암호]**: a [!DNL clientSecret] 에 사용된 매개 변수 [!DNL OAuth2] 클라이언트 자격 증명입니다.

   >[!NOTE]
   >
   >전용 [!DNL OAuth2] 클라이언트 자격 증명은 현재 지원됩니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 이름을 입력합니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명을 입력합니다.
* **[!UICONTROL 사용자 지정 헤더]**: 다음 형식을 사용하여 대상 호출에 포함할 사용자 지정 헤더를 입력합니다. `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >현재 구현에는 하나 이상의 사용자 지정 헤더가 필요합니다. 이 제한은 향후 업데이트에서 해결됩니다.

## 세그먼트를 이 대상에 활성화 {#activate}

자세한 내용은 [스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-streaming-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 대상 속성 {#attributes}

에서 [[!UICONTROL 속성 선택]](../../ui/activate-streaming-profile-destinations.md#select-attributes) Adobe은 사용자 지정 페이지에서 고유 식별자를 선택할 것을 권장합니다 [조합 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 모든 XDM 필드를 선택합니다.

## 프로필 내보내기 동작 {#profile-export-behavior}

Experience Platform은 세그먼트 자격 또는 기타 중요한 이벤트 후에 프로필에 대한 관련 업데이트가 발생한 경우에만 데이터를 API 종단점으로 내보내도록 프로필 내보내기 동작을 HTTP API 대상에 최적화합니다. 프로필은 다음과 같은 상황에서 대상에 내보내집니다.

* 프로필 업데이트는 대상에 매핑된 세그먼트 중 하나 이상에 대한 세그먼트 멤버십 변경에 의해 결정됩니다. 예를 들어 프로필이 대상에 매핑된 세그먼트 중 하나에 적격이거나 대상에 매핑된 세그먼트 중 하나를 끝냈습니다.
* 프로필 업데이트는 [id 맵](/help/xdm/field-groups/profile/identitymap.md). 예를 들어 대상에 매핑된 세그먼트 중 하나에 대해 이미 자격이 있는 프로필이 ID 맵 속성에 새 ID를 추가했습니다.
* 프로필 업데이트는 대상에 매핑된 특성 중 하나 이상에 대한 특성 변경에 의해 결정됩니다. 예를 들어 매핑 단계에서 대상에 매핑된 속성 중 하나가 프로필에 추가됩니다.

위에 설명된 모든 경우 관련 업데이트가 발생한 프로필만 대상으로 내보내집니다. 예를 들어 대상 플로우에 매핑된 세그먼트에 100개의 멤버가 있고 5개의 새 프로필이 세그먼트에 대한 자격이 있는 경우 대상에 내보내기는 증분 결과이며 5개의 새 프로필만 포함합니다.

변경 사항이 있는 위치에 상관없이 모든 매핑된 속성이 프로필에 대해 내보내집니다. 따라서 위의 예에서 이러한 5개의 새 프로필에 대해 매핑된 속성은 속성 자체가 변경되지 않았더라도 내보내집니다.

### 데이터 내보내기와 내보내기에 포함된 내용을 결정하는 것은 무엇입니까? {#what-determines-export-what-is-included}

주어진 프로필에 대해 내보낸 데이터에 대해서는 의 두 가지 개념을 이해하는 것이 중요합니다 *http API 대상에 대한 데이터 내보내기를 결정하는 것은 무엇입니까?* 및 *내보내기에 포함된 데이터*.

| 대상 내보내기를 결정하는 것은 무엇입니까? | 대상 내보내기에 포함된 항목 |
|---------|----------|
| <ul><li>매핑된 속성 및 세그먼트는 대상 내보내기의 단서로 사용됩니다. 즉, 매핑된 세그먼트가 상태(null에서 실현됨 또는 실현됨/존재에서 종료로)를 변경하거나 매핑된 속성을 업데이트하면 대상 내보내기가 해제됩니다.</li><li>현재 ID를 HTTP API 대상에 매핑할 수 없으므로 주어진 프로필의 ID를 변경하면 대상 내보내기도 결정됩니다.</li><li>속성 변경은 속성이 동일한 값이든 간에 속성에 대한 업데이트로 정의됩니다. 즉, 값 자체가 변경되지 않았더라도 속성에 대한 덮어쓰기는 변경 사항으로 간주됩니다.</li></ul> | <ul><li>데이터 플로우에 매핑되었는지 여부에 상관없이 모든 세그먼트(최신 멤버십 상태 포함)는 `segmentMembership` 개체.</li><li>의 모든 ID `identityMap` 개체도 포함됩니다(Experience Platform은 현재 HTTP API 대상에서 ID 매핑을 지원하지 않습니다).</li><li>매핑된 속성만 대상 내보내기에 포함됩니다.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

예를 들어 이 데이터 흐름을 데이터 플로우에서 세 개의 세그먼트를 선택하고 네 개의 속성이 대상에 매핑되는 HTTP 대상으로 간주합니다.

![HTTP API 대상 데이터 흐름](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

대상에 대한 프로필 내보내기는 하나 또는 둘 중 하나에 대해 자격이 있는 프로필로 결정할 수 있습니다 *3개의 매핑된 세그먼트*. 그러나 데이터 내보내기에서 `segmentMembership` 개체(참조 [내보낸 데이터](#exported-data) 아래 섹션)을 사용하면, 특정 프로필이 해당 세그먼트의 구성원일 경우 매핑되지 않은 다른 세그먼트가 나타날 수 있습니다. 프로가 DeLorinan Cars 세그먼트를 통해 고객 자격을 얻지만 또한 Viewed &quot;Back to the Future&quot; 영화 및 SF 팬의 멤버인 경우 다른 두 세그먼트도 함께 제공됩니다 `segmentMembership` 데이터가 데이터 플로우에 매핑되지 않더라도 데이터 내보내기의 객체입니다.

프로필 속성 POV에서 위에 매핑된 4개의 속성에 대한 변경 사항이 대상 내보내기를 결정하며 프로필에 있는 4개의 매핑된 속성이 데이터 내보내기에 표시됩니다.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터가 [!DNL HTTP] JSON 형식으로 대상을 타깃팅합니다. 예를 들어 아래 내보내기에는 특정 세그먼트에 대해 자격이 있고 다른 두 세그먼트의 구성원이며 다른 세그먼트를 종료한 프로필이 포함되어 있습니다. 내보내기에는 프로필 속성 이름, 성, 생년월일 및 개인 이메일 주소도 포함됩니다. 이 프로필의 ID는 ECID 및 이메일입니다.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
