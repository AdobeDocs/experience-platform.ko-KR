---
keywords: Azure 이벤트 허브 대상;azure 이벤트 허브;azure 이벤트 허브
title: (베타)!DNL Azure 이벤트 허브] 연결
description: Experience Platform에서 데이터를 스트리밍하려면 사용자의!DNL Azure 이벤트 허브] 스토리지에 대한 실시간 아웃바운드 연결을 만듭니다.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---

# (베타) [!DNL Azure Event Hubs] 연결

## 개요 {#overview}

>[!IMPORTANT]
>
>플랫폼의 [!DNL Azure Event Hubs] 대상은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

[!DNL Azure Event Hubs] 는 빅데이터 스트리밍 플랫폼 및 이벤트 수집 서비스입니다. 초당 수백만 개의 이벤트를 받고 처리할 수 있습니다. 이벤트 허브로 전송된 데이터는 모든 실시간 분석 공급자나 일괄 처리/저장소 어댑터를 사용하여 변환하고 저장할 수 있습니다.

[!DNL Azure Event Hubs] 저장소에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 데이터를 스트리밍할 수 있습니다.

* [!DNL Azure Event Hubs]에 대한 자세한 내용은 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)를 참조하십시오.
* 프로그래밍 방식으로 [!DNL Azure Event Hubs]에 연결하려면 [스트리밍 대상 API 자습서](../../api/streaming-destinations.md)를 참조하십시오.
* 플랫폼 사용자 인터페이스를 사용하여 [!DNL Azure Event Hubs]에 연결하려면 아래 섹션을 참조하십시오.

![UI의 AWS Kinesis](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 사용 사례 {#use-cases}

[!DNL Azure Event Hubs] 과 같은 스트리밍 대상을 사용하면 고부가가치 세그먼테이션 이벤트와 관련 프로필 속성을 원하는 시스템에 쉽게 제공할 수 있습니다.

예를 들어 잠재 고객이 백서를 다운로드하면 &quot;전환율이 높은&quot; 세그먼트로 분류할 수 있습니다. 잠재 고객이 속한 세그먼트를 [!DNL Azure Event Hubs] 대상에 매핑하면 [!DNL Azure Event Hubs]에서 이 이벤트를 받게 됩니다. 이 환경에서는 엔터프라이즈 IT 시스템에 가장 적합한 방식으로 IT 방식을 사용하고 이벤트 이외에도 비즈니스 논리를 설명할 수 있습니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 대상 활성화 워크플로우의 속성 선택 화면에서 선택한 대로 이메일 주소,  [전화 번호, 성)](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL SAS 키]** 이름 및  **[!UICONTROL SAS 키]**: SAS 키 이름 및 키를 입력합니다. [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)에서 SAS 키를 사용하여 [!DNL Azure Event Hubs]에 인증하는 방법에 대해 알아봅니다.
* **[!UICONTROL 네임스페이스]**: 네임스페이스를  [!DNL Azure Event Hubs] 입력합니다. [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)의 [!DNL Azure Event Hubs] 네임스페이스에 대해 알아봅니다.
* **[!UICONTROL 이름]**: 연결 이름을  [!DNL Azure Event Hubs]입력합니다.
* **[!UICONTROL 설명]**: 연결에 대한 설명을 제공합니다.  예: &quot;Premium Tier 고객&quot;, &quot;Guys 관심 있는 남&quot;.
* **[!UICONTROL eventHubName]**: 대상에 스트림의 이름을  [!DNL Azure Event Hubs] 입력합니다.

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [스트리밍 프로필 내보내기 대상으로 대상 활성화](../../ui/activate-streaming-profile-destinations.md)를 참조하십시오.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터가 JSON 형식으로 [!DNL Azure Event Hubs]에 도달합니다. 예를 들어, 아래 이벤트는 특정 세그먼트에 대해 자격이 있고 다른 세그먼트를 종료한 대상의 이메일 주소 프로필 속성을 포함합니다. 이 잠재 고객의 ID는 ECID 및 이메일입니다.

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
>* [Azure 이벤트 허브에 연결하고 플로우 서비스 API를 사용하여 데이터를 활성화합니다](../../api/streaming-destinations.md)
* [AWS Kinesis 대상](./amazon-kinesis.md)
* [대상 유형 및 카테고리](../../destination-types.md)

