---
title: 암호화된 데이터 수집
description: Adobe Experience Platform을 사용하면 클라우드 스토리지 배치 소스를 통해 암호화된 파일을 수집할 수 있습니다.
hide: true
hidefromtoc: true
source-git-commit: 0457784b8aa97d55882b794077aecdbd2a9a612a
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---

# 암호화된 데이터 섭취

Adobe Experience Platform을 사용하면 클라우드 스토리지 배치 소스를 통해 암호화된 파일을 수집할 수 있습니다. 암호화된 데이터 섭취를 사용하면 비대칭 암호화 메커니즘을 활용하여 배치 데이터를 Experience Platform으로 안전하게 전송할 수 있습니다. 현재 지원되는 비대칭 암호화 메커니즘은 PGP 및 GPG입니다.

암호화된 데이터 수집 프로세스는 다음과 같습니다.

1. [Experience Platform API를 사용하여 암호화 키 쌍 만들기](#create-encryption-key-pair). 암호화 키 쌍은 개인 키와 공개 키로 구성됩니다. 만든 후에는 해당 공개 키 ID 및 만료 시간과 함께 공개 키를 복사하거나 다운로드할 수 있습니다. 이 프로세스 중에 개인 키는 보안 저장소에서 Experience Platform이 저장합니다.
2. 공개 키를 사용하여 수집할 데이터 파일을 암호화합니다.
3. 암호화된 파일을 클라우드 저장소에 배치합니다.
4. 암호화된 파일이 준비되면 [클라우드 스토리지 소스에 대한 소스 연결 및 데이터 흐름 만들기](#create-a-dataflow-for-encrypted-data). 흐름 생성 단계에서 다음을 제공해야 합니다 `encryption` 매개 변수와 공개 키 ID를 포함합니다.
5. Experience Platform은 수집 시 데이터를 해독하기 위해 보안 저장소에서 개인 키를 검색합니다.

이 문서에서는 데이터를 암호화하고 해당 암호화된 데이터를 클라우드 스토리지 소스를 사용하여 Experience Platform으로 수집하는 암호화 키 쌍을 생성하는 방법에 대해 설명합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
   * [클라우드 스토리지 소스](../api/collect/cloud-storage.md): 데이터 흐름을 만들어 클라우드 스토리지 소스에서 Experience Platform으로 배치 데이터를 가져옵니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../landing/api-guide.md).

## 암호화 키 쌍 만들기 {#create-encryption-key-pair}

암호화된 데이터를 Experience Platform에 수집하는 첫 번째 단계는 암호화 키 쌍을 만들기 위해 `/encryption/keys` 의 끝점 [!DNL Connectors] API.

**API 형식**

```http
POST /data/foundation/connectors/encryption/keys
```

**요청**

다음 요청은 PGP 암호화 알고리즘을 사용하여 암호화 키 쌍을 생성합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{PASSPHRASE}"
      }
  }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `encryptionAlgorithm` | 사용 중인 암호화 알고리즘의 유형입니다. 지원되는 암호화 유형은 다음과 같습니다 `PGP` 및 `GPG`. |
| `params.passPhrase` | 암호는 암호화 키에 대한 추가 보호 계층을 제공합니다. 생성 시 Experience Platform은 공개 키의 다른 보안 저장소에 암호를 저장합니다. 비어 있지 않은 문자열을 암호로 제공해야 합니다. |

**응답**

성공적인 응답은 공개 키, 공개 키 ID 및 키의 만료 시간을 반환합니다. 만료 시간은 키 생성 날짜로부터 180일로 자동 설정됩니다. 만료 시간은 현재 구성할 수 없습니다.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## 을 사용하여 클라우드 스토리지 소스를 Experience Platform에 연결 [!DNL Flow Service] API

암호화 키 쌍을 검색한 후에는 클라우드 스토리지 소스에 대한 소스 연결을 만들고 암호화된 데이터를 Platform으로 가져올 수 있습니다.

먼저 Platform에 대해 소스를 인증하려면 기본 연결을 만들어야 합니다. 기본 연결을 만들고 소스를 인증하려면 아래 목록에서 사용할 소스를 선택합니다.

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure 파일 저장소](../api/create/cloud-storage/azure-file-storage.md)
* [데이터 랜딩 영역](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google 클라우드 스토리지](../api/create/cloud-storage/google.md)
* [Oracle 개체 저장소](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

기본 연결을 만든 후 다음에 대한 자습서에 설명된 단계를 따라야 합니다 [클라우드 스토리지 소스에 대한 소스 연결 만들기](../api/collect/cloud-storage.md) 소스 연결, 대상 연결 및 매핑을 생성하기 위해

## 암호화된 데이터에 대한 데이터 흐름 만들기 {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>암호화된 데이터 수집을 위한 데이터 스트림을 만들려면 다음을 수행해야 합니다.
>* [공개 키 ID](#create-encryption-key-pair)
>* [소스 연결 ID](../api/collect/cloud-storage.md#source)
>* [Target 연결 ID](../api/collect/cloud-storage.md#target)
>* [매핑 ID](../api/collect/cloud-storage.md#mapping)


데이터 흐름을 만들려면 `/flows` 의 끝점 [!DNL Flow Service] API. 암호화된 데이터를 수집하려면 `encryption` 섹션에 `transformations` 속성 및 `publicKeyId` 이는 이전 단계에서 생성된 것입니다.

**API 형식**

```http
POST /flows
```

**요청**

다음 요청은 데이터 흐름을 만들어 클라우드 스토리지 소스에 대해 암호화된 데이터를 수집합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Customer Data",
      "description: "ACME encrypted data ingestion",
      "flowSpec": {
          "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "26b53912-1005-49f0-b539-12100559f0e2"
      ],
      "targetConnectionIds": [
        "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                  "mappingVersion": 0
              }
          },
          {
              "name": "Encryption",
              "params": {
                  "publicKeyId": 512e686e-543e-4354-bcba-e1403ddcc532
          }
  }
      ],
      "scheduleParams": {
          "startTime": "1597784298",
          "frequency": "once"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `flowSpec.id` | 클라우드 스토리지 소스에 해당하는 흐름 사양 ID입니다. |
| `sourceConnectionIds` | 소스 연결 ID입니다. 이 ID는 소스에서 플랫폼으로 데이터의 전송을 나타냅니다. |
| `targetConnectionIds` | 대상 연결 ID입니다. 이 ID는 데이터가 Platform으로 전송되면 도착하는 위치를 나타냅니다. |
| `transformations[x].params.mappingId` | 매핑 ID입니다. |
| `transformations.name` | 암호화된 파일을 수집할 때 다음을 제공해야 합니다 `Encryption` 를 데이터 흐름의 추가 변형 매개 변수로 사용하십시오. |
| `transformations[x].params.publicKeyId` | 만든 공개 키 ID입니다. 이 ID는 클라우드 스토리지 데이터를 암호화하는 데 사용되는 암호화 키 쌍의 절반입니다. |
| `scheduleParams.startTime` | epoch 시간의 데이터 흐름의 시작 시간입니다. |
| `scheduleParams.frequency` | 데이터 흐름에서 데이터를 수집하는 빈도입니다. 허용되는 값은 다음과 같습니다. `once`, `minute`, `hour`, `day`, 또는 `week`. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 빈도가 로 설정된 경우 간격이 필요하지 않습니다 `once` 및 보다 크거나 같아야 합니다. `15` 다른 주파수 값에 사용할 수 있습니다. |

**응답**

성공적인 응답은 ID(`id`)를 만들 수 있습니다.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 다음 단계

이 자습서에 따라 클라우드 저장소 데이터에 대한 암호화 키 쌍 및 데이터 흐름을 만들어 을 사용하여 암호화된 데이터를 수집했습니다 [!DNL Flow Service API]. 데이터 흐름의 완결성, 오류 및 지표에 대한 상태 업데이트를 보려면 다음 안내서를 참조하십시오 [다음을 사용하여 데이터 흐름 모니터링 [!DNL Flow Service] API](./monitor.md).