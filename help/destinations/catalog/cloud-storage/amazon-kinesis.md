---
keywords: Amazon Kinesis;kinesis 대상;kinesis
title: Amazon Kinesis 연결
description: Amazon Kinesis 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 데이터를 스트리밍합니다.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---

# (베타) [!DNL Amazon Kinesis] 연결

## 개요 {#overview}

>[!IMPORTANT]
>
>플랫폼의 [!DNL Amazon Kinesis] 대상은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

[!DNL Amazon Web Services]의 [!DNL Kinesis Data Streams] 서비스를 사용하면 대용량 데이터 레코드를 실시간으로 수집 및 처리할 수 있습니다.

[!DNL Amazon Kinesis] 저장소에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 데이터를 스트리밍할 수 있습니다.

* [!DNL Amazon Kinesis]에 대한 자세한 내용은 [Amazon 설명서](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)를 참조하십시오.
* 프로그래밍 방식으로 [!DNL Amazon Kinesis]에 연결하려면 [스트리밍 대상 API 자습서](../../api/streaming-destinations.md)를 참조하십시오.
* 플랫폼 사용자 인터페이스를 사용하여 [!DNL Amazon Kinesis]에 연결하려면 아래 섹션을 참조하십시오.

![UI의 Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 사용 사례 {#use-cases}

[!DNL Amazon Kinesis] 과 같은 스트리밍 대상을 사용하면 고부가가치 세그먼테이션 이벤트와 관련 프로필 속성을 원하는 시스템에 쉽게 제공할 수 있습니다.

예를 들어 잠재 고객이 백서를 다운로드하면 &quot;전환율이 높은&quot; 세그먼트로 분류할 수 있습니다. 잠재 고객이 속한 세그먼트를 [!DNL Amazon Kinesis] 대상에 매핑하면 [!DNL Amazon Kinesis]에서 이 이벤트를 받게 됩니다. 이 환경에서는 엔터프라이즈 IT 시스템에 가장 적합한 방식으로 IT 방식을 사용하고 이벤트 이외에도 비즈니스 논리를 설명할 수 있습니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 대상 활성화 워크플로우의 속성 선택 화면에서 선택한 대로 이메일 주소,  [전화 번호, 성)](../../ui/activate-destinations.md#select-attributes).

## 필요한 [!DNL Amazon Kinesis] 권한 {#required-kinesis-permission}

데이터를 [!DNL Amazon Kinesis] 스트림에 성공적으로 연결하고 내보내려면 Experience Platform에 다음 작업에 대한 권한이 있어야 합니다.

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

이러한 권한은 [!DNL Kinesis] 콘솔을 통해 정렬되며, Platform 사용자 인터페이스에서 Kinesis 대상을 구성한 후에는 Platform에서 확인합니다.

아래 예에는 데이터를 [!DNL Kinesis] 대상으로 성공적으로 내보내는 데 필요한 최소 액세스 권한이 표시됩니다.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `kinesis:ListStreams` | Amazon Kinesis 데이터 스트림을 나열하는 작업입니다. |
| `kinesis:PutRecord` | 단일 데이터 레코드를 Kinesis 데이터 스트림에 작성하는 작업입니다. |
| `kinesis:PutRecords` | 여러 데이터 레코드를 단일 호출로 Kinesis 데이터 스트림에 쓰는 작업입니다. |

[!DNL Kinesis] 데이터 스트림에 대한 액세스 제어에 대한 자세한 내용은 다음 [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)를 참조하십시오.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!DNL Amazon Web Services]액세스 키 및 암호 키**: 에서  [!DNL Amazon Web Services]쌍을  `access key - secret access key` 생성하여 계정에 대한 플랫폼 액세스 권한을  [!DNL Amazon Kinesis] 부여합니다. 자세한 내용은 [Amazon 웹 서비스 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)를 참조하십시오.
* **지역**: 데이터를 스트리밍할  [!DNL Amazon Web Services] 지역을 지정합니다.
* **이름**: 연결할 이름을 입력합니다  [!DNL Amazon Kinesis]
* **설명**: 연결에 대한 설명을 제공합니다  [!DNL Amazon Kinesis].
* **스트림**: 계정에 기존 데이터 스트림의 이름을  [!DNL Amazon Kinesis] 제공합니다. Platform에서 데이터를 이 스트림으로 내보냅니다.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 세그먼트를 이 대상에 활성화 {#activate}

대상으로 대상 세그먼트를 활성화하는 방법에 대한 지침은 [대상 세그먼트 활성화](../../ui/activate-destinations.md)를 참조하십시오.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터가 JSON 형식으로 [!DNL Amazon Kinesis]에 도달합니다. 예를 들어, 아래 이벤트는 특정 세그먼트에 대해 자격이 있고 다른 세그먼트를 종료한 대상의 이메일 주소 프로필 속성을 포함합니다. 이 잠재 고객의 ID는 ECID 및 이메일입니다.

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
>* [Amazon Kinesis에 연결하고 Flow Service API를 사용하여 데이터를 활성화합니다](../../api/streaming-destinations.md)
* [Azure 이벤트 허브 대상](./azure-event-hubs.md)
* [대상 유형 및 카테고리](../../destination-types.md)

