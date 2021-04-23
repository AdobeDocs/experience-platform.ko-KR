---
keywords: Experience Platform;홈;인기 항목;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis 소스 커넥터 개요
topic-legacy: overview
description: API 또는 유저 인터페이스를 사용하여 Amazon Kinesis을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
translation-type: tm+mt
source-git-commit: af11bc966889be54fc27e02f3eee321519cef88f
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform] 및 [!DNL Azure] 같은 클라우드 공급자에 대한 기본 연결을 제공합니다. 이러한 시스템의 데이터를 [!DNL Platform]으로 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 없이 자신의 데이터를 [!DNL Platform]에 가져올 수 있습니다. 인제스트된 데이터는 XDM JSON, XDM 쪽모이 세공 마루 또는 구분된 형태로 포맷될 수 있습니다. 프로세스의 모든 단계가 소스 워크플로우에 통합됩니다. [!DNL Platform] 데이터를 실시간으로 가져올 수  [!DNL Amazon Kinesis] 있습니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역 특정 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류 또는 비성능이 발생할 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 전제 조건

다음 섹션에서는 [!DNL Kinesis] 소스 연결을 만들기 전에 필요한 사전 요구 사항 설정에 대한 추가 정보를 제공합니다.

### 액세스 정책 설정

소스 연결을 만들려면 [!DNL Kinesis] 스트림에 다음 권한이 필요합니다.

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

이러한 권한은 [!DNL Kinesis] 콘솔을 통해 정렬되며 자격 증명을 입력하고 데이터 스트림을 선택하면 플랫폼별로 검사됩니다.

아래 예에는 [!DNL Kinesis] 소스 연결을 만드는 데 필요한 최소 액세스 권한이 표시됩니다.

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
| `kinesis:GetShardIterator` | 레코드를 트래버스하는 데 필요한 작업입니다. |
| `kinesis:GetRecords` | 특정 오프셋 또는 공유 ID에서 레코드를 가져오는 데 필요한 작업입니다. |
| `kinesis:DescribeStream` | 공유 ID를 생성하는 데 필요한 공유 맵을 포함한 스트림에 대한 정보를 반환하는 작업입니다. |
| `kinesis:ListStreams` | UI에서 선택할 수 있는 사용 가능한 스트림을 나열하는 데 필요한 작업입니다. |

[!DNL Kinesis] 데이터 스트림에 대한 액세스 제어에 대한 자세한 내용은 다음 [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)를 참조하십시오.

### 반복기 유형 구성

[!DNL Kinesis] 데이터를 읽는 순서를 지정할 수 있도록 다음과 같은 반복기 유형을 지원합니다.

| 반복기 유형 | 설명 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 데이터는 특정 시퀀스 번호로 식별된 위치에서 읽습니다. |
| `AFTER_SEQUENCE_NUMBER` | 데이터는 특정 시퀀스 번호로 식별된 위치 후 시작됩니다. |
| `AT_TIMESTAMP` | 특정 타임스탬프로 식별된 위치에서 데이터를 읽습니다. |
| `TRIM_HORIZON` | 데이터는 가장 오래된 데이터 레코드에서 시작됩니다. |
| `LATEST` | 최신 데이터 레코드에서 데이터를 읽습니다. |

[!DNL Kinesis] UI 소스는 현재 `TRIM_HORIZON`만 지원하며, API는 데이터를 가져오기 위한 모드로 `TRIM_HORIZON` 및 `LATEST`을 모두 지원합니다. Platform에서 [!DNL Kinesis] 소스에 사용하는 기본 반복기 값은 `TRIM_HORIZON`입니다.

반복기 유형에 대한 자세한 내용은 다음 [[!DNL Kinesis] document](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax)을 참조하십시오.

## [!DNL Amazon Kinesis]을(를) [!DNL Platform]에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Amazon Kinesis]을 [!DNL Platform]에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

- [Flow Service API를 사용하여 Amazon Kinesis 소스 연결 만들기](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Flow Service API를 사용하여 스트리밍 데이터 수집](../../tutorials/api/collect/streaming.md)

### UI 사용

- [UI에서 Amazon Kinesis 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [UI에서 클라우드 스토리지 연결에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
