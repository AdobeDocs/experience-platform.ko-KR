---
title: 암호화된 데이터 수집
description: API를 사용하여 클라우드 스토리지 일괄 처리 소스를 통해 암호화된 파일을 수집하는 방법에 대해 알아봅니다.
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: a92a3d4ce16e50d9eec97448e677ca603931fa44
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 2%

---

# 암호화된 데이터 수집

Adobe Experience Platform을 사용하면 클라우드 스토리지 배치 소스를 통해 암호화된 파일을 수집할 수 있습니다. 암호화된 데이터 수집을 통해 비대칭 암호화 메커니즘을 활용하여 배치 데이터를 안전하게 Experience Platform으로 전송할 수 있습니다. 현재 지원되는 비대칭 암호화 메커니즘은 PGP와 GPG이다.

암호화된 데이터 수집 프로세스는 다음과 같습니다.

1. [Experience Platform API를 사용하여 암호화 키 쌍 만들기](#create-encryption-key-pair). 암호화 키 쌍은 개인 키(private key)와 공개 키(public key)로 구성된다. 만든 후에는 해당 공개 키 ID 및 만료 시간과 함께 공개 키를 복사하거나 다운로드할 수 있습니다. 이 프로세스 중에 개인 키는 Experience Platform이 보안 저장소에 저장합니다. **참고:** 응답의 공개 키는 Base64로 인코딩되며 사용하기 전에 해독해야 합니다.
2. 공개 키를 사용하여 수집할 데이터 파일을 암호화합니다.
3. 암호화된 파일을 클라우드 저장소에 저장합니다.
4. 암호화된 파일이 준비되면 [클라우드 스토리지 소스에 대한 소스 연결 및 데이터 흐름 만들기](#create-a-dataflow-for-encrypted-data). 플로우 생성 단계에서 다음을 제공해야 합니다 `encryption` 매개 변수를 추가하고 공개 키 ID를 포함하십시오.
5. Experience Platform은 수집 시 데이터를 해독하기 위해 보안 저장소에서 개인 키를 검색합니다.

>[!IMPORTANT]
>
>암호화된 단일 파일의 최대 크기는 1GB입니다. 예를 들어 단일 데이터 흐름 실행에서 2GB의 데이터를 수집할 수 있지만 해당 데이터의 개별 파일은 1GB를 초과할 수 없습니다.

이 문서에서는 데이터를 암호화하고 클라우드 스토리지 소스를 사용하여 암호화된 데이터를 Experience Platform에 수집하는 암호화 키 쌍을 생성하는 방법에 대한 단계를 제공합니다.

## 시작하기

이 자습서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 잘 알고 있어야 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
   * [클라우드 스토리지 소스](../api/collect/cloud-storage.md): 데이터 흐름을 만들어 클라우드 스토리지 소스의 배치 데이터를 Experience Platform으로 가져옵니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../landing/api-guide.md).

### 암호화된 파일에 대해 지원되는 파일 확장명

암호화된 파일에 대해 지원되는 파일 확장자 목록은 다음과 같습니다.

* .csv
* .tsv
* .json
* .parquet
* .csv.gpg
* .tsv.gpg
* .json.gpg
* .parquet.gpg
* .csv.pgp
* .tsv.pgp
* .json.pgp
* .parquet.pgp
* .gpg
* .pgp

>[!NOTE]
>
>Adobe Experience Platform Sources의 암호화된 파일 수집은 openPGP를 지원하며 PGP의 특정 독점 버전이 아닙니다.

## 암호화 키 쌍 만들기 {#create-encryption-key-pair}

Experience PlatformPOST 에 암호화된 데이터를 수집하는 첫 번째 단계는 `/encryption/keys` 의 엔드포인트 [!DNL Connectors] API.

**API 형식**

```http
POST /data/foundation/connectors/encryption/keys
```

**요청**

다음 요청은 PGP 암호화 알고리즘을 사용하여 암호화 키 쌍을 생성합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| 매개변수 | 설명 |
| --- | --- |
| `encryptionAlgorithm` | 사용 중인 암호화 알고리즘의 유형입니다. 지원되는 암호화 유형은 다음과 같습니다 `PGP` 및 `GPG`. |
| `params.passPhrase` | 암호는 암호화 키에 대한 추가 보호 계층을 제공합니다. 생성 시 Experience Platform은 암호를 공개 키와 다른 보안 저장소에 저장합니다. 비어 있지 않은 문자열을 암호로 제공해야 합니다. |

**응답**

성공적인 응답은 Base64로 인코딩된 공개 키, 공개 키 ID 및 키의 만료 시간을 반환합니다. 만료 시간은 키 생성일로부터 180일로 자동 설정됩니다. 만료 시간은 현재 구성할 수 없습니다.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

| 속성 | 설명 |
| --- | --- |
| `publicKey` | 공개 키는 클라우드 스토리지의 데이터를 암호화하는 데 사용됩니다. 이 키는 이 단계 중에 생성된 개인 키와 일치합니다. 하지만 개인 키는 즉시 Experience Platform으로 이동합니다. |
| `publicKeyId` | 공개 키 ID는 데이터 흐름을 만들고 암호화된 Experience Platform 스토리지 데이터를 수집하여 수집하는 데 사용됩니다. |
| `expiryTime` | 만료 시간은 암호화 키 쌍의 만료 날짜를 정의합니다. 이 날짜는 키 생성 날짜 후 180일로 자동 설정되며 unix 타임스탬프 형식으로 표시됩니다. |

+++(선택 사항) 서명된 데이터에 대한 서명 확인 키 쌍 만들기

### 고객 관리 키 쌍 만들기

선택적으로 서명 확인 키 쌍을 만들어 암호화된 데이터에 서명하고 수집할 수 있습니다.

이 단계에서는 개인 키와 공개 키 조합을 생성한 다음 개인 키를 사용하여 암호화된 데이터에 서명해야 합니다. 다음으로, Platform에서 서명을 확인하려면 Base64에서 공개 키를 인코딩한 다음 Experience Platform에 공유해야 합니다.

### 공개 키를 공유하여 Experience Platform

POST 공개 키를 공유하려면 `/customer-keys` 암호화 알고리즘과 Base64로 인코딩된 공개 키를 제공하는 동안 끝점이 발생했습니다.

**API 형식**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}}
    }'
```

| 매개변수 | 설명 |
| --- | --- |
| `encryptionAlgorithm` | 사용 중인 암호화 알고리즘의 유형입니다. 지원되는 암호화 유형은 다음과 같습니다 `PGP` 및 `GPG`. |
| `publicKey` | 암호화된 서명에 사용되는 고객 관리 키에 해당하는 공개 키입니다. 이 키는 Base64로 인코딩해야 합니다. |

**응답**

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| 속성 | 설명 |
| --- | --- |
| `publicKeyId` | 이 공개 키 ID는 고객이 관리하는 키를 Experience Platform과 공유하는 것에 대한 응답으로 반환됩니다. 서명 및 암호화된 데이터에 대한 데이터 흐름을 만들 때 이 공개 키 ID를 서명 확인 키 ID로 제공할 수 있습니다. |

+++

## 다음을 사용하여 클라우드 스토리지 소스를 Experience Platform에 연결 [!DNL Flow Service] API

암호화 키 쌍을 검색했으면 이제 계속하여 클라우드 스토리지 소스에 대한 소스 연결을 만들고 암호화된 데이터를 플랫폼으로 가져올 수 있습니다.

먼저 Platform에 대해 소스를 인증하려면 기본 연결을 만들어야 합니다. 기본 연결을 만들고 소스를 인증하려면 아래 목록에서 사용할 소스를 선택하십시오.

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure 파일 스토리지](../api/create/cloud-storage/azure-file-storage.md)
* [데이터 랜딩 영역](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google 클라우드 스토리지](../api/create/cloud-storage/google.md)
* [Oracle 개체 스토리지](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

기본 연결을 만든 후에는 자습서에 설명된 단계를 따라야 합니다 [클라우드 스토리지 소스에 대한 소스 연결 생성](../api/collect/cloud-storage.md) 소스 연결, 대상 연결 및 매핑을 생성합니다.

## 암호화된 데이터에 대한 데이터 흐름 만들기 {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>암호화된 데이터 수집을 위한 데이터 흐름을 만들려면 다음이 있어야 합니다.
>
>* [공개 키 ID](#create-encryption-key-pair)
>* [소스 연결 ID](../api/collect/cloud-storage.md#source)
>* [대상 연결 ID](../api/collect/cloud-storage.md#target)
>* [ID 매핑](../api/collect/cloud-storage.md#mapping)

데이터 흐름을 만들려면 다음에 대한 POST 요청을 만듭니다. `/flows` 의 엔드포인트 [!DNL Flow Service] API. 암호화된 데이터를 수집하려면 `encryption` 섹션에 대한 섹션 `transformations` 속성 및 포함 `publicKeyId` 이전 단계에서 만들어졌습니다.

**API 형식**

```http
POST /flows
```

**요청**

>[!BEGINTABS]

>[!TAB 암호화된 데이터 수집을 위한 데이터 흐름 만들기]

다음 요청은 클라우드 스토리지 소스에 대해 암호화된 데이터를 수집하기 위한 데이터 흐름을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| 속성 | 설명 |
| --- | --- |
| `flowSpec.id` | 클라우드 저장소 소스에 해당하는 흐름 사양 ID입니다. |
| `sourceConnectionIds` | 소스 연결 ID. 이 ID는 소스에서 플랫폼으로 데이터를 전송하는 것을 나타냅니다. |
| `targetConnectionIds` | 대상 연결 ID입니다. 이 ID는 데이터가 플랫폼으로 가져오면 들어오는 위치를 나타냅니다. |
| `transformations[x].params.mappingId` | 매핑 ID입니다. |
| `transformations.name` | 암호화된 파일을 수집할 때 다음을 제공해야 합니다. `Encryption` 를 데이터 흐름의 추가 변형 매개 변수로 사용하십시오. |
| `transformations[x].params.publicKeyId` | 만든 공개 키 ID입니다. 이 ID는 클라우드 스토리지 데이터를 암호화하는 데 사용되는 암호화 키 쌍의 절반입니다. |
| `scheduleParams.startTime` | epoch 시간 내 데이터 흐름의 시작 시간입니다. |
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. 허용되는 값은 다음과 같습니다. `once`, `minute`, `hour`, `day`, 또는 `week`. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 빈도를 로 설정하면 간격이 필요하지 않습니다. `once` 다음보다 크거나 같아야 합니다. `15` 다른 빈도 값의 경우. |


>[!TAB 데이터 흐름을 만들어 암호화 및 서명된 데이터 수집]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data (with Sign Verification)",
    "description": "ACME Customer Data (with Sign Verification)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17",
                "signVerificationKeyId":"e31ae895-7896-469a-8e06-eb9207ddf1c2"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| 속성 | 설명 |
| --- | --- |
| `params.signVerificationKeyId` | 서명 확인 키 ID는 Base64로 인코딩된 공개 키를 Experience Platform과 공유한 후 검색된 공개 키 ID와 동일합니다. |

>[!ENDTABS]

**응답**

성공적인 응답은 ID( )를 반환합니다.`id`)에 포함되어 있습니다.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```


>[!BEGINSHADEBOX]

**반복 수집 제한 사항**

암호화된 데이터 수집은 소스에서 반복 또는 다중 수준 폴더의 수집을 지원하지 않습니다. 암호화된 모든 파일은 단일 폴더에 포함되어야 합니다. 단일 소스 경로에 여러 폴더가 있는 와일드카드도 지원되지 않습니다.

다음은 지원되는 폴더 구조의 예입니다. 여기서 소스 경로는 `/ACME-customers/*.csv.gpg`.

이 시나리오에서는 굵게 표시된 파일이 Experience Platform으로 수집됩니다.

* ACME-customer
   * **File1.csv.gpg**
   * File2.json.gpg
   * **File3.csv.gpg**
   * File4.json
   * **File5.csv.gpg**

다음은 소스 경로가 인 지원되지 않는 폴더 구조의 예입니다. `/ACME-customers/*`.

이 시나리오에서는 흐름 실행이 실패하고 소스에서 데이터를 복사할 수 없다는 오류 메시지가 반환됩니다.

* ACME-customer
   * File1.csv.gpg
   * File2.json.gpg
   * Subfolder1
      * File3.csv.gpg
      * File4.json.gpg
      * File5.csv.gpg
* ACME-충성도
   * File6.csv.gpg

>[!ENDSHADEBOX]

## 다음 단계

이 자습서를 따라 클라우드 스토리지 데이터에 대한 암호화 키 쌍과 를 사용하여 암호화된 데이터를 수집하기 위한 데이터 흐름을 만들었습니다. [!DNL Flow Service API]. 데이터 흐름의 완결성, 오류 및 지표에 대한 상태 업데이트는 의 안내서를 참조하십시오. [를 사용하여 데이터 흐름 모니터링 [!DNL Flow Service] API](./monitor.md).