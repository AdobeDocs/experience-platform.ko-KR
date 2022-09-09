---
title: 설명서 셀프 서비스 템플릿 // 대상 이름으로 바꾸기
description: 이 템플릿을 사용하여 Adobe Experience Platform 카탈로그에서 대상에 대한 공개 설명서를 만듭니다. // 개요 섹션의 단락으로 대체합니다
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 788c02622b5176b41eb6da70bed0994d4824c984
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 1%

---

# 대상 연결 {#your-destination}

*이 템플릿을 진행하면 모든 단락을 기울임꼴로 바꾸거나 삭제합니다(이 단락은 시작).*

*먼저 페이지 상단에서 메타데이터(제목 및 설명)를 업데이트합니다. 이 페이지에서 UICONTROL의 모든 인스턴스를 무시하십시오. 기계 번역 프로세스를 통해 페이지를 지원하는 여러 언어로 올바르게 변환하는 태그입니다. 문서를 제출한 후 문서에 태그를 추가합니다.*

>[!IMPORTANT]
>
>* 템플릿에 요약된 순서대로 이 템플릿의 모든 섹션을 입력합니다.
>* 이 템플릿은 파트너 피드백을 기반으로 자주 업데이트됩니다. 대상에 대한 문서 작성을 시작하기 전에 [템플릿의 최신 버전](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).


## 개요 {#overview}

*고객에게 제공하는 가치를 비롯하여 귀사에 대한 간단한 개요를 제공합니다. 자세한 내용을 보려면 제품 설명서 홈 페이지에 대한 링크를 포함하십시오.*

>[!IMPORTANT]
>
>이 설명서 페이지는 *대상* 팀 문의 사항이나 업데이트 요청에 대해서는 *예를 들어 업데이트를 위해 연결할 수 있는 링크 또는 이메일 주소를 삽입합니다 `support@YourDestination.com`.*

## 사용 사례 {#use-cases}

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 *대상* 대상, Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례는 다음과 같습니다.

### 사용 사례 #1 {#use-case-1}

*모바일 메시징 플랫폼의 경우:*

*주택 임대 및 판매 플랫폼에서는 고객의 Android 및 iOS 장치에 모바일 알림을 푸시하여 이전에 대여 요청을 했던 영역에 업데이트된 목록이 100개 있음을 알려 주려고 합니다.*

### 사용 사례 #2 {#use-case-2}

*소셜 네트워크 플랫폼의 경우:*

*스포츠 의류 브랜드는 기존 고객에게 소셜 미디어 계정을 통해 연결되기를 원한다. 의류 브랜드는 자신의 CRM에서 Adobe Experience Platform으로 이메일 주소를 수집하고, 자체 오프라인 데이터에서 세그먼트를 작성하고, 이러한 세그먼트를 YourDestination으로 전송하여 고객의 소셜 미디어 피드에 광고를 표시할 수 있습니다.*

## 전제 조건 {#prerequisites}

*Adobe Experience Platform 사용자 인터페이스에서 대상을 설정하기 전에 고객이 알아야 하는 모든 사항에 대한 정보를 이 섹션에 추가합니다. 다음 항목에 대해 지정할 수 있습니다.*

* *허용 목록에 추가되어야 함*
* *이메일 해싱 요구 사항*
* *고객 측의 모든 계정 세부 사항*
* *플랫폼에 연결하기 위해 API 키를 가져오는 방법*

*고객에게 유용한 경우 관련 설명서에 연결할 수 있습니다.*

## 지원되는 ID {#supported-identities}

*대상이 지원하는 ID에 대한 정보를 이 섹션에 추가합니다. 몇 가지 표준 값으로 테이블을 미리 입력했습니다. 대상에 적용되지 않는 값과 미리 채워지지 않은 값을 삭제합니다.*

*대상* 은 아래 표에 설명된 id의 활성화를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| ECID | Experience Cloud ID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스를 다음 별칭으로 참조할 수도 있습니다. &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. 다음 문서를 참조하십시오. [ECID](/help/identity-service/ecid.md) 추가 정보. |
| phone_sha256 | SHA256 알고리즘으로 해시된 전화 번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| extern_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스이면 이 타겟 ID를 선택합니다. |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

*테이블에서 대상에 해당하는 행만 유지합니다. 내보내기 유형에 대해 한 라인과 내보내기 빈도에 대해 한 라인이 있어야 합니다. 대상에 적용되지 않는 값을 삭제합니다.*

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 에서 사용되는 식별자(이름, 전화 번호 또는 기타 식별자)로 세그먼트의 모든 멤버(대상)를 내보내고 있습니다 *대상* 대상. |
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 전자 메일 주소, 전화 번호, 성)을 선택한 대로 [대상 활성화 워크플로우](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상에 인증 {#authenticate}

*대상에 인증할 때 고객이 입력해야 하는 필드를 추가합니다. 이러한 필드는 대상별로 다르며 Destination SDK의 구성에 따라 다릅니다. 대상 필드가 아래 나열된 필드와 같을 수 없습니다. 아래 표시된 샘플 스크린샷과 유사한 스크린샷도 포함하십시오.*

대상을 인증하려면 필요한 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**.

![대상에 인증하는 방법을 보여주는 샘플 스크린샷](/help/destinations/destination-sdk/docs-framework/assets/authenticate-destination.png)

* **[!UICONTROL 베어러 토큰]**: 대상을 인증하려면 베어러 토큰을 입력합니다.

### 대상 세부 사항 채우기 {#destination-details}

*새 대상을 구성할 때 고객이 입력해야 하는 필드를 추가합니다. 이러한 필드는 대상별로 다르며 Destination SDK의 구성에 따라 다릅니다. 대상 필드가 아래 나열된 필드와 같을 수 없습니다. 아래 표시된 샘플 스크린샷과 유사한 스크린샷도 포함하십시오.*

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상에 대한 세부 사항을 채우는 방법을 보여주는 샘플 스크린샷](/help/destinations/destination-sdk/docs-framework/assets/configure-destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자 *대상* 계정 ID.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 특성 및 ID 매핑 {#map}

*활성화 워크플로우의 매핑 단계에서 소스와 대상 필드 간의 지원되는 매핑에 대한 정보를 추가합니다. 대상은 프로필 속성, ID 네임스페이스 또는 둘 다 내보내기를 지원할 수 있습니다. 일부 필드는 필수입니다. Target 속성은 사전 정의되거나 사용자 지정일 수 있습니다. 중요한 주의 사항을 살펴보고 스크린샷과 같은 예를 사용하십시오. 참조로 사용할 수 있는 대상 페이지의 두 예는 다음과 같습니다.*

* *[페가](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[메달리아](/help/destinations/catalog/voice/medallia-connector.md#map)*

## 내보낸 데이터 / 데이터 내보내기 유효성 검사 {#exported-data}

*데이터를 대상에 내보내는 방식에 대한 단락을 추가합니다. 이렇게 하면 고객이 대상에 올바르게 통합되었는지 확인하는 데 도움이 됩니다. 예를 들어 아래 JSON과 같은 샘플 JSON을 제공할 수 있습니다. 또는 대상 인터페이스의 스크린샷 및 정보를 제공하여 고객이 대상 플랫폼에서 세그먼트를 채우는 방법을 보여 줄 수 있습니다.*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
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

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 읽기 [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

*고객이 성공적으로 작업하기 위해 중요하다고 생각하는 제품 설명서나 기타 리소스에 대한 추가 링크를 제공할 수 있습니다.*