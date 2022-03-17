---
keywords: 모바일; brize; 메시징;
title: 연결 브레이즈
description: Braze는 고객과 고객이 좋아하는 브랜드 간 연관성 있고 기억에 남을 경험을 제공하는 포괄적인 고객 참여 플랫폼입니다.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 2%

---

# [!DNL Braze] 연결

## 개요 {#overview}

다음 [!DNL Braze] 대상은 프로필 데이터를 로 보내는 데 도움이 됩니다. [!DNL Braze].

[!DNL Braze] 는 고객과 고객이 좋아하는 브랜드 간 연관성 있고 기억에 남을 경험을 제공하는 포괄적인 고객 참여 플랫폼입니다.

프로필 데이터를 로 보내려면 [!DNL Braze]를 채울 때는 먼저 대상에 연결해야 합니다.

## 대상 세부 사항 {#specifics}

다음의 특정 세부 사항을 참고하십시오 [!DNL Braze] 대상:

* [!DNL Adobe Experience Platform] 세그먼트를에 내보냅니다. [!DNL Braze] 아래에 `AdobeExperiencePlatformSegments` 속성을 사용합니다.

>[!NOTE]
>
>추가 사용자 지정 속성을에 전송한다는 점에 유의하십시오. [!DNL Braze] 이로 인해 [!DNL Braze] 데이터 포인트 소비. 귀하의 [!DNL Braze] 추가 사용자 지정 속성을 보내기 전 계정 관리자.

## 사용 사례 {#use-cases}

마케터는 세그먼트가 내장된 모바일 참여 대상의 사용자를 타깃팅하려고 합니다 [!DNL Adobe Experience Platform]. 또한 해당 고객의 특성에 따라 개인화된 경험을 제공하려고 합니다 [!DNL Adobe Experience Platform] 세그먼트와 프로필이 업데이트되는 즉시 프로필 [!DNL Adobe Experience Platform].

## 지원되는 ID {#supported-identities}

[!DNL Braze] 은 아래 표에 설명된 id의 활성화를 지원합니다.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| external_id | 사용자 지정 [!DNL Braze] 모든 id의 매핑을 지원하는 식별자입니다. | 임의의 [id](../../../identity-service/namespaces.md) 변환 후 [!DNL Braze] 대상에 매핑하기만 하면 됩니다 [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 필드 매핑에 따라 이메일 주소, 전화번호, 성) 및/또는 id를 지정합니다.[!DNL Adobe Experience Platform] 세그먼트를에 내보냅니다. [!DNL Braze] 아래에 `AdobeExperiencePlatformSegments` 속성을 사용합니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 계정 토큰 브라우징]**: 이건 네 거야 [!DNL Braze] [!DNL API] 키. 를 얻는 방법에 대한 자세한 지침은 [!DNL API] 키: [REST API 키 개요](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 이름을 입력합니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명을 입력합니다.
* **[!UICONTROL 끝점 인스턴스]**: 질문하기 [!DNL Braze] 사용해야 하는 엔드포인트 인스턴스를 나타냅니다.

## 세그먼트를 이 대상에 활성화 {#activate}

자세한 내용은 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 매핑 고려 사항 {#mapping-considerations}

대상 데이터를 올바르게 보내는 방법 [!DNL Adobe Experience Platform] 변환 후 [!DNL Braze] 대상, 필드 매핑 단계를 거쳐야 합니다.

매핑은 사용자 간에 링크를 만드는 것으로 구성됩니다 [!DNL Experience Data Model] (XDM) 스키마 필드를 [!DNL Platform] 계정 및 타겟 대상의 해당 상당물.

XDM 필드를 [!DNL Braze] 대상 필드: 다음 단계를 수행합니다.

에서 [!UICONTROL 매핑] step, **[!UICONTROL 새 매핑 추가]**.

![대상 추가 매핑 확장](../../assets/catalog/mobile-engagement/braze/mapping.png)

에서 [!UICONTROL 소스 필드] 섹션에서 빈 필드 옆에 있는 화살표 단추를 클릭합니다.

![대상 소스 매핑 브레이징](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

에서 [!UICONTROL 소스 필드 선택] 창의 두 범주(XDM 필드) 중에서 선택할 수 있습니다.
* [!UICONTROL 속성 선택]: XDM 스키마의 특정 필드를 [!DNL Braze] 속성을 사용합니다.

![대상 매핑 소스 특성 브레이징](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL ID 네임스페이스 선택]: 이 옵션을 사용하여 [!DNL Platform] id 네임스페이스를 로 [!DNL Braze] 네임스페이스.

![대상 매핑 소스 네임스페이스 브레이징](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

소스 필드를 선택한 다음 **[!UICONTROL 선택]**.

에서 [!UICONTROL Target 필드] 섹션에서 필드 오른쪽의 매핑 아이콘을 클릭합니다.

![대상 대상 매핑 브레이징](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

에서 [!UICONTROL 대상 필드 선택] 창, 다음 두 가지 대상 필드 범주 중에서 선택할 수 있습니다.
* [!UICONTROL ID 네임스페이스 선택]: 매핑하려면 이 옵션을 사용합니다 [!DNL Platform] id 네임스페이스 [!DNL Braze] id 네임스페이스.
* [!UICONTROL 사용자 지정 속성 선택]: 이 옵션을 사용하여 XDM 속성을 사용자 지정에 매핑 [!DNL Braze] 에 정의된 특성입니다 [!DNL Braze] 계정이 필요합니다. <br> 이 옵션을 사용하여 기존 XDM 속성의 이름을 [!DNL Braze]. 예를 들어 `lastName` 사용자 지정에 대한 XDM 속성 `Last_Name` 특성 [!DNL Braze]이(가) 만들어집니다. `Last_Name` 특성 [!DNL Braze]가 없는 경우 및에 매핑합니다 `lastName` XDM 속성을 사용합니다.

![대상 대상 매핑 필드 이해](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

대상 필드를 선택한 다음 **[!UICONTROL 선택]**.

이제 목록에 필드 매핑이 표시됩니다.

![대상 매핑 확장 완료](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

매핑을 더 추가하려면 이전 단계를 반복합니다.

## 매핑 예 {#mapping-example}

XDM 프로필 스키마와 사용자 [!DNL Braze] 인스턴스에는 다음 속성 및 ID가 포함됩니다.

|  | XDM 프로필 스키마 | [!DNL Braze] 인스턴스 |
|---|---|---|
| 속성 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| ID | <ul><li>이메일</code></li><li>Google 광고 ID(GAID)</code></li><li>광고주를 위한 Apple Id(IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

올바른 매핑은 다음과 같습니다.

![브레이징 대상 매핑 예](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 내보낸 데이터 {#exported-data}

데이터를 로 성공적으로 내보냈는지 확인하려면 [!DNL Braze] 대상, [!DNL Braze] 계정이 필요합니다. [!DNL Adobe Experience Platform] 세그먼트를에 내보냅니다. [!DNL Braze] 아래에 `AdobeExperiencePlatformSegments` 속성을 사용합니다.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용 을 참조하십시오. [데이터 거버넌스 개요](../../../data-governance/home.md).
