---
title: 흐름 서비스 API를 사용하여 AWS Redshift를 Experience Platform에 연결
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 AWS Redshift에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: dd9aee1ac887637d4761188d6dbcf55ad5bde407
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 3%

---

# [!DNL Flow Service] API를 사용하여 [!DNL AWS Redshift]을(를) Experience Platform에 연결

>[!IMPORTANT]
>
>[!DNL AWS Redshift] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL AWS Redshift] 소스 계정을 Adobe Experience Platform에 연결하는 방법을 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## Azure에서 [!DNL AWS Redshift]을(를) Experience Platform에 연결 {#azure}

[!DNL AWS Redshift] 소스를 Azure의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하세요.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL AWS Redshift]과(와) 연결하려면 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| `server` | [!DNL AWS Redshift] 인스턴스의 서버 이름입니다. |
| `port` | [!DNL AWS Redshift] 서버가 클라이언트 연결을 수신 대기하는 데 사용하는 TCP 포트입니다. |
| `username` | [!DNL AWS Redshift] 계정과 연결된 사용자 이름. |
| `password` | 사용자 계정에 해당하는 암호입니다. |
| `database` | 데이터를 가져올 [!DNL AWS Redshift] 데이터베이스입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL AWS Redshift]의 연결 사양 ID는 `3416976c-a9ca-4bba-901a-1f08f66978ff`입니다. |

시작에 대한 자세한 내용은 이 [[!DNL AWS Redshift] 문서](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html)를 참조하세요.

### Azure []의 Experience Platform에서 [!DNL AWS Redshift]에 대한 기본 연결#azure-base 만듭니다.

>[!NOTE]
>
>[!DNL Redshift]의 기본 인코딩 표준은 유니코드입니다. 이는 변경할 수 없습니다.

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL AWS Redshift] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

+++예를 보려면 선택

다음 요청은 [!DNL AWS Redshift]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS-redshift base connection",
      "description": "base connection for AWS-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.server` | [!DNL AWS Redshift] 인스턴스의 서버 이름입니다. |
| `auth.params.port` | [!DNL AWS Redshift] 서버가 클라이언트 연결을 수신 대기하는 데 사용하는 TCP 포트입니다. |
| `auth.params.username` | [!DNL AWS Redshift] 계정과 연결된 사용자 이름. |
| `auth.params.password` | 사용자 계정에 해당하는 암호입니다. |
| `auth.params.database` | 데이터를 가져올 [!DNL AWS Redshift] 데이터베이스입니다. |
| `connectionSpec.id` | [!DNL AWS Redshift] 연결 사양 ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**응답**

+++예를 보려면 선택

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결이 반환됩니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

+++

## AWS 웹 서비스(AWS)의 Experience Platform에 [!DNL AWS Redshift] 연결 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 AWS 웹 서비스(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../../../landing/multi-cloud.md)를 참조하세요.

[!DNL AWS Redshift] 소스를 AWS의 Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하십시오.

### AWS의 Experience Platform에서 [!DNL AWS Redshift]에 대한 기본 연결 만들기 {#aws-base}

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 [!DNL AWS Redshift]에 대한 기본 연결을 만듭니다.

+++예를 보려면 선택

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS Redshift base connection for Experience Platform on AWS",
      "description": "AWS Redshift base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "5439",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.server` | [!DNL AWS Redshift] 인스턴스의 서버 이름입니다. |
| `auth.params.port` | [!DNL AWS Redshift] 서버가 클라이언트 연결을 수신 대기하는 데 사용하는 TCP 포트입니다. |
| `auth.params.username` | [!DNL AWS Redshift] 계정과 연결된 사용자 이름. |
| `auth.params.password` | 사용자 계정에 해당하는 암호입니다. |
| `auth.params.database` | 데이터를 가져올 [!DNL AWS Redshift] 데이터베이스입니다. |
| `auth.params.schema` | [!DNL AWS Redshift] 데이터베이스와 연결된 스키마의 이름입니다. 데이터베이스 액세스 권한을 부여할 사용자도 이 스키마에 액세스할 수 있는지 확인해야 합니다. |
| `connectionSpec.id` | [!DNL AWS Redshift] 연결 사양 ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**응답**

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보가 반환됩니다. 다음 자습서에서 저장소를 탐색하려면 이 ID가 필요합니다.

+++예를 보려면 선택

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++


## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL AWS Redshift] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 데이터베이스 데이터를 플랫폼으로 가져올 데이터 흐름을 만드십시오.](../../collect/database-nosql.md)
