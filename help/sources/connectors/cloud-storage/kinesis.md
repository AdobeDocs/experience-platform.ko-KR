---
title: Amazon Kinesis 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Amazon Kinesis을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# [!DNL Amazon Kinesis] 소스

>[!IMPORTANT]
>
>다음 [!DNL Amazon Kinesis] 소스는 Real-time Customer Data Platform Ultimate를 구매한 사용자에게 소스 카탈로그에서 사용할 수 있습니다.

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform], 및 [!DNL Azure]. 이러한 시스템의 데이터를 로 가져올 수 있습니다 [!DNL Platform].

클라우드 스토리지 소스는 고유한 데이터를으로 가져올 수 있습니다 [!DNL Platform] 를 다운로드하거나, 형식을 지정하거나, 업로드할 필요가 없습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. [!DNL Platform] 에서 데이터를 가져올 수 있습니다. [!DNL Amazon Kinesis] 실시간으로.

>[!NOTE]
>
>다음에 대한 척도 요소 [!DNL Kinesis] 대용량 데이터를 수집해야 하는 경우 늘려야 합니다. 현재, 에서 가져올 수 있는 최대 데이터 볼륨입니다 [!DNL Kinesis] platform에 대한 계정은 초당 4000개의 레코드입니다. 더 많은 볼륨 데이터를 확장 및 수집하려면 Adobe 담당자에게 문의하십시오.

## 전제 조건

다음 단원에서는 다음을 만들기 전에 필요한 필수 구성 요소 설정에 대해 자세히 설명합니다. [!DNL Kinesis] 소스 연결.

### 액세스 정책 설정

A [!DNL Kinesis] stream을 사용하려면 원본 연결을 만드는 데 다음 권한이 필요합니다.

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

이러한 권한은 [!DNL Kinesis] 자격 증명을 입력하고 데이터 스트림을 선택하면 콘솔에서 및 을(를) 확인합니다.

아래 예는 를 만드는 데 필요한 최소 액세스 권한을 표시합니다. [!DNL Kinesis] 소스 연결.

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
| `kinesis:GetShardIterator` | 레코드 사이를 이동하는 데 필요한 작업입니다. |
| `kinesis:GetRecords` | 특정 오프셋 또는 공유 ID에서 레코드를 가져오는 데 필요한 작업입니다. |
| `kinesis:DescribeStream` | 샤드 ID를 생성하는 데 필요한 샤드 맵을 포함하는 스트림 관련 정보를 반환하는 작업입니다. |
| `kinesis:ListStreams` | UI에서 선택할 수 있는 사용 가능한 스트림을 나열하는 데 필요한 작업입니다. |

에 대한 액세스 제어에 대한 자세한 내용 [!DNL Kinesis] 데이터 스트림, 다음 참조 [[!DNL Kinesis] 문서](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### 반복자 유형 구성

[!DNL Kinesis] 는 데이터를 읽는 순서를 지정할 수 있도록 다음 반복자 유형을 지원합니다.

| 반복자 유형 | 설명 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 데이터는 특정 시퀀스 번호에 의해 식별되는 위치로부터 시작하여 판독된다. |
| `AFTER_SEQUENCE_NUMBER` | 데이터는 특정 시퀀스 번호로 식별된 위치 이후부터 읽혀집니다. |
| `AT_TIMESTAMP` | 데이터는 특정 타임스탬프로 식별된 위치에서 시작하여 읽혀집니다. |
| `TRIM_HORIZON` | 가장 오래된 데이터 레코드부터 데이터를 읽습니다. |
| `LATEST` | 가장 최근 데이터 레코드부터 데이터를 읽습니다. |

A [!DNL Kinesis] UI 소스는 현재 `TRIM_HORIZON`, API는 두 가지를 모두 지원합니다. `TRIM_HORIZON` 및 `LATEST` 를 데이터 가져오기 위한 모드로 사용하십시오. Platform이 다음에 사용하는 기본 반복자 값 [!DNL Kinesis] 소스: `TRIM_HORIZON`.

반복자 유형에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL Kinesis] 문서](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## 연결 [!DNL Amazon Kinesis] 끝 [!DNL Platform]

아래 설명서는 연결 방법에 대한 정보를 제공합니다 [!DNL Amazon Kinesis] 끝 [!DNL Platform] api 또는 사용자 인터페이스 사용:

### API 사용

- [흐름 서비스 API를 사용하여 Amazon Kinesis 소스 연결 만들기](../../tutorials/api/create/cloud-storage/kinesis.md)
- [흐름 서비스 API를 사용하여 스트리밍 데이터 수집](../../tutorials/api/collect/streaming.md)

### UI 사용

- [UI에서 Amazon Kinesis 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 구성](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
