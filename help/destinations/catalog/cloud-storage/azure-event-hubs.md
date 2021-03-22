---
keywords: Azure 이벤트 허브 대상;azure 이벤트 허브;azure 이벤트 하위 그룹
title: (베타) Azure 이벤트 허브 연결
description: Experience Platform의 데이터를 스트리밍하기 위해 Azure 이벤트 허브 저장소에 대한 실시간 아웃바운드 연결을 만듭니다.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---


# (베타) [!DNL Azure Event Hubs] 연결

## 개요 {#overview}

>[!IMPORTANT]
>
>플랫폼의 [!DNL Azure Event Hubs] 대상이 현재 베타 상태입니다. 설명서 및 기능은 변경될 수 있습니다.

[!DNL Azure Event Hubs] 빅데이터 스트리밍 플랫폼 및 이벤트 통합 서비스입니다. 초당 수백만 개의 이벤트를 받고 처리할 수 있습니다. 이벤트 허브로 전송된 데이터는 실시간 분석 공급자 또는 배치/저장 어댑터를 사용하여 변환하여 저장할 수 있습니다.

Adobe Experience Platform의 데이터를 스트리밍하기 위해 [!DNL Azure Event Hubs] 스토리지에 대한 실시간 아웃바운드 연결을 만들 수 있습니다.

* [!DNL Azure Event Hubs]에 대한 자세한 내용은 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)를 참조하십시오.
* 프로그램 방식으로 [!DNL Azure Event Hubs]에 연결하려면 [스트리밍 대상 API 자습서](../../api/streaming-destinations.md)를 참조하십시오.
* 플랫폼 사용자 인터페이스를 사용하여 [!DNL Azure Event Hubs]에 연결하려면 아래 섹션을 참조하십시오.

![UI의 AWS Kinesis](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 사용 사례 {#use-cases}

[!DNL Azure Event Hubs]과 같은 스트리밍 대상을 사용하여 고부가가치 세그먼테이션 이벤트와 관련 프로필 속성을 원하는 시스템에 쉽게 제공할 수 있습니다.

예를 들어 잠재 고객이 &quot;전환율이 높은&quot; 세그먼트에 자격을 주는 백서를 다운로드했습니다. 잠재 고객이 [!DNL Azure Event Hubs] 대상에 속하는 세그먼트를 매핑하면 [!DNL Azure Event Hubs]에서 이 이벤트를 받게 됩니다. 엔터프라이즈 IT 시스템에서 가장 잘 사용할 수 있을 것으로 생각되는 대로 직접 처리하고 이벤트 상단에 비즈니스 논리를 설명할 수 있습니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예:이메일 주소, 전화 번호, 성)을  [대상 활성화 워크플로의 속성 선택 화면에서 선택합니다](../../ui/activate-destinations.md#select-attributes).

## 연결 대상 {#connect-destination}

[!DNL Azure Event Hubs]를 포함하여 클라우드 스토리지 대상에 연결하는 방법에 대한 지침은 [클라우드 스토리지 대상 워크플로우 ](./workflow.md)을 참조하십시오.

[!DNL Azure Event Hubs] 대상의 경우 대상 만들기 작업 과정에 다음 정보를 입력합니다.

## 인증 단계 {#authentication-step}

* **[!UICONTROL SAS Key Name]** 및:  **[!UICONTROL SAS Key]** SAS 키 이름과 키를 입력합니다. [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)에서 SAS 키를 사용하여 [!DNL Azure Event Hubs]에 인증하는 방법에 대해 학습합니다.
* **[!UICONTROL Namespace]**:네임스페이스를  [!DNL Azure Event Hubs] 입력합니다. [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)의 [!DNL Azure Event Hubs] 네임스페이스에 대해 알아봅니다.

![인증 단계에서 입력 필요](../../assets/catalog/cloud-storage/event-hubs/authentication.png)

## 설정 단계 {#setup-step}

* **[!UICONTROL Name]**:연결 이름을 입력합니다 [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**:연결에 대한 설명을 제공합니다.  예:&quot;프리미엄 계층 고객&quot;, &quot;고양이에 관심 있는 남성&quot;
* **[!UICONTROL eventHubName]**:대상에 스트림의 이름을  [!DNL Azure Event Hubs] 지정합니다.
* **[!UICONTROL Marketing actions]**:마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 Adobe Experience Platform](../../../data-governance/policies/overview.md) 페이지의 [데이터 거버넌스 페이지를 참조하십시오. 개별 Adobe 정의 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

![설정 단계에 필요한 데이터](../../assets/catalog/cloud-storage/event-hubs/setup.png)

## 세그먼트 활성화 {#activate-segments}

세그먼트 활성화 작업 과정에 대한 자세한 내용은 [프로필 및 세그먼트를 대상](../../ui/activate-destinations.md)에 활성화를 참조하십시오.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터는 JSON 형식으로 [!DNL Azure Event Hubs]에 저장됩니다. 예를 들어, 아래 이벤트에는 특정 세그먼트에 자격을 갖추고 다른 세그먼트를 종료한 대상자의 이메일 주소 프로필 속성이 포함되어 있습니다. 이 잠재 고객의 ID는 ECID와 이메일입니다.

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
>* [Azure 이벤트 허브에 연결하고 흐름 서비스 API를 사용하여 데이터를 활성화합니다.](../../api/streaming-destinations.md)
>* [AWS Kinesis 대상](./amazon-kinesis.md)
>* [대상 유형 및 카테고리](../../destination-types.md)