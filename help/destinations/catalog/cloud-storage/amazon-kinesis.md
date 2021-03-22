---
keywords: Amazon Kinesis;kinesis destination;kinesis
title: Amazon Kinesis 연결
description: Amazon Kinesis 스토리지에 대한 실시간 아웃바운드 연결을 생성하여 Adobe Experience Platform의 데이터를 스트리밍합니다.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 2%

---


# (베타) [!DNL Amazon Kinesis] 연결

## 개요 {#overview}

>[!IMPORTANT]
>
>플랫폼의 [!DNL Amazon Kinesis] 대상이 현재 베타 상태입니다. 설명서 및 기능은 변경될 수 있습니다.

[!DNL Amazon Web Services]의 [!DNL Kinesis Data Streams] 서비스를 사용하면 대량의 데이터 레코드를 실시간으로 수집하고 처리할 수 있습니다.

Adobe Experience Platform의 데이터를 스트리밍하기 위해 [!DNL Amazon Kinesis] 스토리지에 대한 실시간 아웃바운드 연결을 만들 수 있습니다.

* [!DNL Amazon Kinesis]에 대한 자세한 내용은 [Amazon 설명서](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)를 참조하십시오.
* 프로그램 방식으로 [!DNL Amazon Kinesis]에 연결하려면 [스트리밍 대상 API 자습서](../../api/streaming-destinations.md)를 참조하십시오.
* 플랫폼 사용자 인터페이스를 사용하여 [!DNL Amazon Kinesis]에 연결하려면 아래 섹션을 참조하십시오.

![UI의 Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 사용 사례 {#use-cases}

[!DNL Amazon Kinesis]과 같은 스트리밍 대상을 사용하여 고부가가치 세그먼테이션 이벤트와 관련 프로필 속성을 원하는 시스템에 쉽게 제공할 수 있습니다.

예를 들어 잠재 고객이 &quot;전환율이 높은&quot; 세그먼트에 자격을 주는 백서를 다운로드했습니다. 잠재 고객이 [!DNL Amazon Kinesis] 대상에 속하는 세그먼트를 매핑하면 [!DNL Amazon Kinesis]에서 이 이벤트를 받게 됩니다. 엔터프라이즈 IT 시스템에서 가장 잘 사용할 수 있을 것으로 생각되는 대로 직접 처리하고 이벤트 상단에 비즈니스 논리를 설명할 수 있습니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예:이메일 주소, 전화 번호, 성)을  [대상 활성화 워크플로의 속성 선택 화면에서 선택합니다](../../ui/activate-destinations.md#select-attributes).

## 연결 대상 {#connect-destination}

[!DNL Amazon]에서 지원하는 클라우드 스토리지 대상을 포함하여 클라우드 스토리지 대상에 연결하는 방법에 대한 지침은 [클라우드 스토리지 대상 워크플로우 ](./workflow.md)을 참조하십시오.

[!DNL Amazon Kinesis] 대상의 경우 대상 만들기 작업 과정에 다음 정보를 입력합니다.

## 인증 단계 {#authentication-step}

* **[!DNL Amazon Web Services]액세스 키 및 비밀 키**:에서  [!DNL Amazon Web Services]쌍을 생성하여  `access key - secret access key` 플랫폼에 사용자 계정에 대한 액세스 권한을  [!DNL Amazon Kinesis] 부여합니다. [Amazon 웹 서비스 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)에서 자세한 내용을 살펴보십시오.
* **지역**:데이터를  [!DNL Amazon Web Services] 스트리밍할 지역을 표시합니다.

![계정 단계의 입력 필드](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

## 설정 단계 {#setup-step}

* **이름**:연결 대상 이름 입력  [!DNL Amazon Kinesis]
* **설명**:연결에 대한 설명을 제공합니다 [!DNL Amazon Kinesis].
* **스트림**:계정에 있는 기존 데이터 스트림의 이름을  [!DNL Amazon Kinesis] 제공합니다. 플랫폼이 데이터를 이 스트림으로 내보냅니다.
* **[!UICONTROL Marketing actions]**:마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 Adobe Experience Platform](../../../data-governance/policies/overview.md) 페이지의 [데이터 거버넌스 페이지를 참조하십시오. 개별 Adobe 정의 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

![인증 단계의 입력 필드](../../assets/catalog/cloud-storage/amazon-kinesis/setup.png)

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 세그먼트 활성화 {#activate-segments}

세그먼트 활성화 작업 과정에 대한 자세한 내용은 [프로필 및 세그먼트를 대상](../../ui/activate-destinations.md)에 활성화를 참조하십시오.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터는 JSON 형식으로 [!DNL Amazon Kinesis]에 저장됩니다. 예를 들어, 아래 이벤트에는 특정 세그먼트에 자격을 갖추고 다른 세그먼트를 종료한 대상자의 이메일 주소 프로필 속성이 포함되어 있습니다. 이 잠재 고객의 ID는 ECID와 이메일입니다.

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
>* [Amazon Kinesis에 연결하고 Flow Service API를 사용하여 데이터 활성화](../../api/streaming-destinations.md)
>* [Azure 이벤트 허브 대상](./azure-event-hubs.md)
>* [대상 유형 및 카테고리](../../destination-types.md)

