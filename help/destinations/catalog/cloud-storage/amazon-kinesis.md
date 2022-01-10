---
keywords: Amazon Kinesis;kinesis 대상;kinesis
title: Amazon Kinesis 연결
description: Amazon Kinesis 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 데이터를 스트리밍합니다.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: f7f3bc229ddad046dca5ea8d2889942fc9cb2cab
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---

# (베타) [!DNL Amazon Kinesis] 연결

## 개요 {#overview}

>[!IMPORTANT]
>
>다음 [!DNL Amazon Kinesis] 플랫폼의 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

다음 [!DNL Kinesis Data Streams] 서비스 기준 [!DNL Amazon Web Services] 에서는 대용량 데이터 레코드를 실시간으로 수집 및 처리할 수 있습니다.

에 대한 실시간 아웃바운드 연결을 만들 수 있습니다 [!DNL Amazon Kinesis] Adobe Experience Platform에서 데이터를 스트리밍할 수 있는 스토리지.

* 에 대한 자세한 정보 [!DNL Amazon Kinesis]를 참조하고 [Amazon 설명서](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* 에 연결하려면 [!DNL Amazon Kinesis] 프로그래밍 방식으로 [스트리밍 대상 API 자습서](../../api/streaming-destinations.md).
* 에 연결하려면 [!DNL Amazon Kinesis] platform 사용자 인터페이스를 사용하여 아래 섹션을 참조하십시오.

![UI의 Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 사용 사례 {#use-cases}

다음과 같은 스트리밍 대상 사용 [!DNL Amazon Kinesis]를 사용하면 고부가가치 세그먼테이션 이벤트 및 관련 프로필 속성을 선택한 시스템에 쉽게 제공할 수 있습니다.

예를 들어 잠재 고객이 백서를 다운로드하여 &quot;전환율이 높은&quot; 세그먼트로 분류하는 경우 잠재 고객이 속한 세그먼트를 [!DNL Amazon Kinesis] 대상, 이 이벤트를 [!DNL Amazon Kinesis]. 이 환경에서는 엔터프라이즈 IT 시스템에 가장 적합한 방식으로 IT 방식을 사용하고 이벤트 이외에도 비즈니스 논리를 설명할 수 있습니다.

## 내보내기 유형 {#export-type}

**프로필 기반** - 원하는 스키마 필드와 함께 세그먼트의 모든 멤버를 내보냅니다(예: 전자 메일 주소, 전화 번호, 성) [대상자 활성화 워크플로우](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## 필수 여부 [!DNL Amazon Kinesis] 권한 {#required-kinesis-permission}

데이터를 성공적으로 연결하고 로 내보내려면 [!DNL Amazon Kinesis] 스트림, Experience Platform은 다음 작업에 대한 권한이 필요합니다.

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

이러한 권한은 [!DNL Kinesis] Platform 사용자 인터페이스에서 Kinesis 대상을 구성한 후 Platform에서 확인합니다.

아래 예에는 데이터를 로 성공적으로 내보내는 데 필요한 최소 액세스 권한이 표시됩니다 [!DNL Kinesis] 대상.

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

액세스 제어에 대한 자세한 정보 [!DNL Kinesis] 데이터 스트림, 다음 읽기 [[!DNL Kinesis] 문서](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!DNL Amazon Web Services]액세스 키 및 비밀 키**: in [!DNL Amazon Web Services], 생성 `access key - secret access key` 플랫폼에 대한 액세스 권한을 부여하기 위한 쌍 [!DNL Amazon Kinesis] 계정이 필요합니다. 자세한 내용은 [Amazon Web Services 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **지역**: 표시할 항목 [!DNL Amazon Web Services] 데이터를 스트리밍할 영역입니다.
* **이름**: 연결할 이름을 입력합니다 [!DNL Amazon Kinesis]
* **설명**: 연결에 대한 설명을 제공합니다 [!DNL Amazon Kinesis].
* **스트림**: 에 기존 데이터 스트림의 이름을 입력합니다 [!DNL Amazon Kinesis] 계정이 필요합니다. Platform에서 데이터를 이 스트림으로 내보냅니다.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 세그먼트를 이 대상에 활성화 {#activate}

자세한 내용은 [스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-streaming-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 프로필 내보내기 동작 {#profile-export-behavior}

Experience Platform은 세그먼트 자격 또는 기타 중요한 이벤트 후에 프로필에 대한 관련 업데이트가 발생한 경우에만 데이터를 대상에 내보내도록 Amazon Kinesis 대상으로의 프로필 내보내기 동작을 최적화합니다. 프로필은 다음과 같은 상황에서 대상에 내보내집니다.

* 대상에 매핑된 세그먼트 중 하나 이상에 대한 세그먼트 멤버십 변경으로 프로필 업데이트가 트리거되었습니다. 예를 들어 프로필이 대상에 매핑된 세그먼트 중 하나에 적격이거나 대상에 매핑된 세그먼트 중 하나를 끝냈습니다.
* 프로필 업데이트는 [id 맵](/help/xdm/field-groups/profile/identitymap.md). 예를 들어 대상에 매핑된 세그먼트 중 하나에 대해 이미 자격이 있는 프로필이 ID 맵 속성에 새 ID를 추가했습니다.
* 대상에 매핑된 특성 중 하나 이상에 대한 특성 변경으로 프로필 업데이트가 트리거되었습니다. 예를 들어 매핑 단계에서 대상에 매핑된 속성 중 하나가 프로필에 추가됩니다.

위에 설명된 모든 경우 관련 업데이트가 발생한 프로필만 대상으로 내보내집니다. 예를 들어 대상 플로우에 매핑된 세그먼트에 100개의 멤버가 있고 5개의 새 프로필이 세그먼트에 대한 자격이 있는 경우 대상에 내보내기는 증분 결과이며 5개의 새 프로필만 포함합니다.

변경 사항이 있는 위치에 상관없이 모든 매핑된 속성이 프로필에 대해 내보내집니다. 따라서 위의 예에서 이러한 5개의 새 프로필에 대해 매핑된 속성은 속성 자체가 변경되지 않았더라도 내보내집니다.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터가 랜딩됨 [!DNL Amazon Kinesis] JSON 형식으로 표시합니다. 예를 들어, 아래 이벤트는 특정 세그먼트에 대해 자격이 있고 다른 세그먼트를 종료한 대상의 이메일 주소 프로필 속성을 포함합니다. 이 잠재 고객의 ID는 ECID 및 이메일입니다.

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
>* [Azure 이벤트 허브 대상](./azure-event-hubs.md)
>* [대상 유형 및 카테고리](../../destination-types.md)

