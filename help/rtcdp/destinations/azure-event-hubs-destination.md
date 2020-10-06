---
keywords: Azure event hub destination;azure event hub;azure eventhub
title: (베타) Azure 이벤트 허브 대상
seo-title: (베타) Azure 이벤트 허브 대상
description: Azure 이벤트 허브 저장소에 대한 실시간 아웃바운드 연결을 만들어 Experience Platform의 데이터를 스트리밍합니다.
seo-description: Azure 이벤트 허브 저장소에 대한 실시간 아웃바운드 연결을 만들어 Experience Platform의 데이터를 스트리밍합니다.
translation-type: tm+mt
source-git-commit: 67a353c950bef11ccbaa52c49d213f08449baa96
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---


# (베타) [!DNL Azure Event Hubs] 대상

>[!IMPORTANT]
>
>Adobe 실시간 CDP의 [!DNL Azure Event Hubs] 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

[!DNL Azure Event Hubs] 빅데이터 스트리밍 플랫폼 및 이벤트 통합 서비스입니다. 초당 수백만 개의 이벤트를 수신하고 처리할 수 있습니다. 이벤트 허브로 전송된 데이터는 모든 실시간 분석 공급자 또는 배치/저장 어댑터를 사용하여 변형하고 저장할 수 있습니다.

스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform의 데이터를 스트림할 수 있습니다. [!DNL Azure Event Hubs]

* 자세한 내용 [!DNL Azure Event Hubs]은 [Microsoft 설명서를 참조하십시오](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* API 호출 [!DNL Azure Event Hubs] 을 사용하여 연결하려면 [스트리밍 대상 API 자습서를 참조하십시오](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md).
* Adobe 실시간 CDP 사용자 인터페이스를 [!DNL Azure Event Hubs] 사용하여 연결하려면 아래 섹션을 참조하십시오.

![UI의 AWS Kinesis](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## 사용 사례 {#use-cases}

이와 같은 스트리밍 대상을 사용하면 고부가가치 세그멘테이션 이벤트 및 관련 프로필 속성을 원하는 시스템에 손쉽게 제공할 수 [!DNL Azure Event Hubs]있습니다.

예를 들어 잠재 고객이 &quot;전환율이 높은&quot; 세그먼트에 자격을 주는 백서를 다운로드했습니다. 잠재 고객이 대상에 속하는 세그먼트를 매핑하면 이 이벤트를 [!DNL Azure Event Hubs] 수신하게 됩니다 [!DNL Azure Event Hubs]. 기업 IT 시스템에서 가장 잘 작동하는 것처럼 현장 중심의 비즈니스 로직을 도입하여 설명할 수 있습니다.

## 내보내기 유형 {#export-type}

**프로필 기반** - 원하는 스키마 필드와 함께 세그먼트의 모든 멤버를 내보냅니다(예:이메일 주소, 전화 번호, 성)을 [대상 활성화 워크플로우의 속성 선택 화면에서 선택합니다](/help/rtcdp/destinations/activate-destinations.md#select-attributes).\

## 연결 대상 {#connect-destination}

클라우드 [스토리지 대상 워크플로우 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)에서 클라우드 스토리지 대상에 연결하는 방법에 대한 지침을 참조하십시오 [!DNL Azure Event Hubs].

대상에 대해 [!DNL Azure Event Hubs] 대상 만들기 워크플로우에서 다음 정보를 입력합니다.

### 인증 단계에서 {#authentication-step}

* **[!UICONTROL SAS 키 이름]** 및 **[!UICONTROL SAS 키]**:SAS 키 이름과 키를 입력합니다. [!DNL Azure Event Hubs] Microsoft 문서에서 SAS 키 [로 인증하는 방법에 대해 알아보십시오](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL 네임스페이스]**:네임스페이스를 [!DNL Azure Event Hubs] 입력합니다. Microsoft 문서 [!DNL Azure Event Hubs] 의 네임스페이스에 대해 [알아보십시오](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

![인증 단계에 필요한 입력](/help/rtcdp/destinations/assets/event-hubs-authentication.png)

### 설정 단계에서 {#setup-step}

* **[!UICONTROL 이름]**:연결할 이름을 입력합니다 [!DNL Azure Event Hubs].
* **[!UICONTROL 설명]**:연결에 대한 설명을 제공합니다.  예:&quot;Premium Tier customers&quot;, &quot;Haps interest to kitteuring.&quot;
* **[!UICONTROL eventHubName]**:대상에 스트림의 이름을 [!DNL Azure Event Hubs] 입력합니다.

![설정 단계에 필요한 데이터](/help/rtcdp/destinations/assets/event-hubs-setup-step.png)

## 세그먼트 활성화 {#activate-segments}

세그먼트 [활성화 워크플로에 대한 자세한 내용은 대상에](/help/rtcdp/destinations/activate-destinations.md) 프로필 및 세그먼트 활성화를 참조하십시오.


## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터는 JSON 형식 [!DNL Azure Event Hubs] 으로 배치됩니다. 예를 들어, 아래 이벤트에는 특정 세그먼트에 자격을 부여하여 다른 세그먼트를 종료한 대상자의 이메일 주소 프로필 속성이 포함되어 있습니다. 이 잠재 고객의 ID는 ECID와 이메일입니다.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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


>[!MORELIKETHIS]
>
>* [Azure 이벤트 허브에 연결하고 API 호출을 사용하여 데이터 활성화](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [AWS Kinesis 대상](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [대상 유형 및 카테고리](/help/rtcdp/destinations/destination-types.md)