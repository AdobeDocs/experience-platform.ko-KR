---
keywords: Azure 이벤트 허브 대상;azure 이벤트 허브;azure 이벤트 허브
title: (베타) [!DNL Azure Event Hubs] 연결
description: 에 대한 실시간 아웃바운드 연결을 만듭니다. [!DNL Azure Event Hubs] Experience Platform에서 데이터를 스트리밍할 스토리지.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: c93a054174bc68ecedf67599ef61ad0b41a56ada
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# (베타) [!DNL Azure Event Hubs] 연결

## 개요 {#overview}

>[!IMPORTANT]
>
>다음 [!DNL Azure Event Hubs] 플랫폼의 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

[!DNL Azure Event Hubs] 는 빅데이터 스트리밍 플랫폼 및 이벤트 수집 서비스입니다. 초당 수백만 개의 이벤트를 받고 처리할 수 있습니다. 이벤트 허브로 전송된 데이터는 모든 실시간 분석 공급자나 일괄 처리/저장소 어댑터를 사용하여 변환하고 저장할 수 있습니다.

에 대한 실시간 아웃바운드 연결을 만들 수 있습니다 [!DNL Azure Event Hubs] Adobe Experience Platform에서 데이터를 스트리밍할 수 있는 스토리지.

* 에 대한 자세한 정보 [!DNL Azure Event Hubs]를 참조하고 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* 에 연결하려면 [!DNL Azure Event Hubs] 프로그래밍 방식으로 [스트리밍 대상 API 자습서](../../api/streaming-destinations.md).
* 에 연결하려면 [!DNL Azure Event Hubs] platform 사용자 인터페이스를 사용하여 아래 섹션을 참조하십시오.

![UI의 AWS Kinesis](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 사용 사례 {#use-cases}

다음과 같은 스트리밍 대상 사용 [!DNL Azure Event Hubs]를 사용하면 고부가가치 세그먼테이션 이벤트 및 관련 프로필 속성을 선택한 시스템에 쉽게 제공할 수 있습니다.

예를 들어 잠재 고객이 백서를 다운로드하여 &quot;전환율이 높은&quot; 세그먼트로 분류하는 경우 잠재 고객이 속한 세그먼트를 [!DNL Azure Event Hubs] 대상, 이 이벤트를 [!DNL Azure Event Hubs]. 이 환경에서는 엔터프라이즈 IT 시스템에 가장 적합한 방식으로 IT 방식을 사용하고 이벤트 이외에도 비즈니스 논리를 설명할 수 있습니다.

## 내보내기 유형 {#export-type}

**프로필 기반** - 원하는 스키마 필드와 함께 세그먼트의 모든 멤버를 내보냅니다(예: 전자 메일 주소, 전화 번호, 성) [대상자 활성화 워크플로우](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL SAS 키 이름]** 및 **[!UICONTROL SAS 키]**: SAS 키 이름 및 키를 입력합니다. 인증 방법에 대해 알아보기 [!DNL Azure Event Hubs] SAS 키를 사용하여 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL 네임스페이스]**: 을 입력합니다. [!DNL Azure Event Hubs] 네임스페이스. 알아보기 [!DNL Azure Event Hubs] 네임스페이스 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL 이름]**: 연결할 이름을 입력합니다 [!DNL Azure Event Hubs].
* **[!UICONTROL 설명]**: 연결에 대한 설명을 제공합니다.  예: &quot;Premium Tier 고객&quot;, &quot;Guys 관심 있는 남&quot;.
* **[!UICONTROL eventHubName]**: 스트림의 이름을 로 입력합니다 [!DNL Azure Event Hubs] 대상.

## 세그먼트를 이 대상에 활성화 {#activate}

자세한 내용은 [스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-streaming-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 프로필 내보내기 동작 {#profile-export-behavior}

Experience Platform은 세그먼트 자격 또는 기타 중요한 이벤트 후에 프로필에 대한 관련 업데이트가 발생한 경우에만 데이터를 대상으로 내보내도록 Azure 이벤트 허브 대상으로 프로필 내보내기 동작을 최적화합니다. 프로필은 다음과 같은 상황에서 대상에 내보내집니다.

* 대상에 매핑된 세그먼트 중 하나 이상에 대한 세그먼트 멤버십 변경으로 프로필 업데이트가 트리거되었습니다. 예를 들어 프로필이 대상에 매핑된 세그먼트 중 하나에 적격이거나 대상에 매핑된 세그먼트 중 하나를 끝냈습니다.
* 프로필 업데이트는 [id 맵](/help/xdm/field-groups/profile/identitymap.md). 예를 들어 대상에 매핑된 세그먼트 중 하나에 대해 이미 자격이 있는 프로필이 ID 맵 속성에 새 ID를 추가했습니다.
* 대상에 매핑된 특성 중 하나 이상에 대한 특성 변경으로 프로필 업데이트가 트리거되었습니다. 예를 들어 매핑 단계에서 대상에 매핑된 속성 중 하나가 프로필에 추가됩니다.

위에 설명된 모든 경우 관련 업데이트가 발생한 프로필만 대상으로 내보내집니다. 예를 들어 대상 플로우에 매핑된 세그먼트에 100개의 멤버가 있고 5개의 새 프로필이 세그먼트에 대한 자격이 있는 경우 대상에 내보내기는 증분 결과이며 5개의 새 프로필만 포함합니다.

변경 사항이 있는 위치에 상관없이 모든 매핑된 속성이 프로필에 대해 내보내집니다. 따라서 위의 예에서 이러한 5개의 새 프로필에 대해 매핑된 속성은 속성 자체가 변경되지 않았더라도 내보내집니다.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터가 랜딩됨 [!DNL Azure Event Hubs] JSON 형식으로 표시합니다. 예를 들어, 아래 이벤트는 특정 세그먼트에 대해 자격이 있고 다른 세그먼트를 종료한 대상의 이메일 주소 프로필 속성을 포함합니다. 이 잠재 고객의 ID는 ECID 및 이메일입니다.

```json
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


>[!MORELIKETHIS]
>
>* [Azure 이벤트 허브에 연결하고 플로우 서비스 API를 사용하여 데이터를 활성화합니다](../../api/streaming-destinations.md)
>* [AWS Kinesis 대상](./amazon-kinesis.md)
>* [대상 유형 및 카테고리](../../destination-types.md)

