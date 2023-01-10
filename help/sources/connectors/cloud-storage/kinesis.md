---
keywords: Experience Platform;홈;인기 항목;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Amazon Kinesis을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform], 및 [!DNL Azure]. 이러한 시스템의 데이터를 [!DNL Platform].

클라우드 스토리지 소스는 고유한 데이터를 [!DNL Platform] 를 다운로드하거나, 형식을 지정하거나, 업로드할 필요가 없습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. [!DNL Platform] 에서 데이터를 가져올 수 있습니다. [!DNL Amazon Kinesis] 실시간으로

>[!NOTE]
>
>다음에 대한 배율 인수 [!DNL Kinesis] 대용량 데이터를 수집해야 하는 경우 증가해야 합니다. 현재 사용자에서 가져올 수 있는 최대 데이터 볼륨 [!DNL Kinesis] Platform에 대한 계정은 초당 4,000개의 레코드입니다. 더 높은 볼륨 데이터를 확장 및 수집하려면 Adobe 담당자에게 문의하십시오.

## 전제 조건

다음 섹션에서는 생성 전에 필요한 전제 조건 설정에 대한 추가 정보를 제공합니다 [!DNL Kinesis] 소스 연결.

### 액세스 정책 설정

A [!DNL Kinesis] 스트림에는 소스 연결을 만들려면 다음 권한이 필요합니다.

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

이러한 권한은 [!DNL Kinesis] 자격 증명을 입력하고 데이터 스트림을 선택하면 Platform에서 콘솔 및 를 확인합니다.

아래 예에는 [!DNL Kinesis] 소스 연결.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
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
| `kinesis:GetShardIterator` | 레코드를 통과하는 데 필요한 작업입니다. |
| `kinesis:GetRecords` | 특정 오프셋 또는 공유 ID에서 레코드를 가져오는 데 필요한 작업입니다. |
| `kinesis:DescribeStream` | 샤드 ID를 생성하는 데 필요한 샤드 맵을 포함하는 스트림에 대한 정보를 반환하는 작업입니다. |
| `kinesis:ListStreams` | UI에서 선택할 수 있는 사용 가능한 스트림을 나열하는 데 필요한 작업입니다. |

액세스 제어에 대한 자세한 정보 [!DNL Kinesis] 데이터 스트림에 대해서는 다음을 참조하십시오 [[!DNL Kinesis] 문서](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### 반복자 유형 구성

[!DNL Kinesis] 에서는 데이터를 읽는 순서를 지정할 수 있도록 다음 반복기 유형을 지원합니다.

| 반복기 유형 | 설명 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 데이터는 특정 시퀀스 번호로 식별되는 위치부터 읽습니다. |
| `AFTER_SEQUENCE_NUMBER` | 데이터는 특정 시퀀스 번호로 식별된 위치 이후에 읽습니다. |
| `AT_TIMESTAMP` | 특정 타임스탬프로 식별된 위치에서 데이터를 읽습니다. |
| `TRIM_HORIZON` | 데이터는 가장 오래된 데이터 레코드부터 읽습니다. |
| `LATEST` | 데이터는 최신 데이터 레코드에서 시작하여 읽습니다. |

A [!DNL Kinesis] 현재 UI 소스는 `TRIM_HORIZON`를 지원하는 반면 API는 두 가지 모두를 지원합니다 `TRIM_HORIZON` 및 `LATEST` 데이터를 가져오기 위한 모드입니다. Platform이 [!DNL Kinesis] 소스: `TRIM_HORIZON`.

반복기 유형에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL Kinesis] 문서](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Connect [!DNL Amazon Kinesis] to [!DNL Platform]

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Amazon Kinesis] to [!DNL Platform] api 또는 사용자 인터페이스 사용:

### API 사용

- [Flow Service API를 사용하여 Amazon Kinesis 소스 연결을 만듭니다](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Flow Service API를 사용하여 스트리밍 데이터를 수집합니다](../../tutorials/api/collect/streaming.md)

### UI 사용

- [UI에서 Amazon Kinesis 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [UI에서 클라우드 스토리지 연결에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
