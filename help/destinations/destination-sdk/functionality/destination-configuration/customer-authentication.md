---
description: 대상에 대한 인증 메커니즘을 설정하고 선택한 인증 방법에 따라 UI에서 사용자에게 표시될 내용을 파악할 수 있는 방법을 알아봅니다.
title: 고객 인증 구성
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 0%

---


# 고객 인증 구성

Experience Platform은 파트너 및 고객이 사용할 수 있는 인증 프로토콜을 매우 유연하게 제공합니다. 와 같은 업계 표준 인증 방법을 지원하도록 대상을 구성할 수 있습니다. [!DNL OAuth2], bearer 토큰 인증, 암호 인증 등.

이 페이지에서는 기본 인증 방법을 사용하여 대상을 설정하는 방법을 설명합니다. 대상을 만들 때 사용하는 인증 구성에 따라, Experience Platform UI에서 대상에 연결할 때 고객은 서로 다른 유형의 인증 페이지를 보게 됩니다.

이 구성 요소가 Destination SDK과 함께 작성된 통합에 어떤 영향을 주는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서나 다음 대상 구성 개요 페이지를 참조하십시오.

* [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

고객이 Platform에서 대상으로 데이터를 내보내려면 먼저 [대상 연결](../../../ui/connect-destination.md) 자습서입니다.

When [대상 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md) Destination SDK, `customerAuthenticationConfigurations` 섹션에서 고객이 보게 되는 내용을 정의합니다 [인증 화면](../../../ui/connect-destination.md#authenticate). 대상 인증 유형에 따라 고객은 다음과 같은 다양한 인증 세부 사항을 제공해야 합니다.

* 을 사용하는 대상 [기본 인증](#basic), 사용자는 Experience Platform UI 인증 페이지에서 직접 사용자 이름과 암호를 제공해야 합니다.
* 을 사용하는 대상 [bearer 인증](#bearer)에서 사용자는 베어러 토큰을 제공해야 합니다.
* 을 사용하는 대상 [OAuth2 인증](#oauth2)이면 사용자는 자격 증명으로 로그인할 수 있는 대상의 로그인 페이지로 리디렉션됩니다.
* 대상 [Amazon S3](#s3) 대상, 사용자가 [!DNL Amazon S3] 키 및 암호 키에 액세스합니다.
* 대상 [Azure Blob](#blob) 대상, 사용자가 [!DNL Azure Blob] 연결 문자열입니다.

를 통해 고객 인증 세부 사항을 구성할 수 있습니다 `/authoring/destinations` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)

이 문서에서는 대상에 사용할 수 있는 지원되는 모든 고객 인증 구성에 대해 설명하고 대상에 대해 설정한 인증 방법을 기반으로 고객이 Experience Platform UI에서 보게 되는 내용을 표시합니다.

>[!IMPORTANT]
>
>고객 인증 구성에서는 매개 변수를 구성할 필요가 없습니다. 다음 경우에 API 호출에 이 페이지에 표시된 코드 조각을 복사하여 붙여 넣을 수 있습니다 [만들기](../../authoring-api/destination-configuration/create-destination-configuration.md) 또는 [업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md) 대상 구성 및 사용자에게 Platform UI에 해당 인증 화면이 표시됩니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반(일괄 처리) 통합 | 예 |

## 인증 규칙 구성 {#authentication-rule}

이 페이지에 설명된 고객 인증 구성을 사용할 때는 항상 `authenticationRule` 매개 변수 [대상 게재](destination-delivery.md) to `"CUSTOMER_AUTHENTICATION"`아래에 표시된 대로,

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## 기본 인증 {#basic}

Experience Platform의 실시간(스트리밍) 통합에 대한 기본 인증이 지원됩니다.

기본 인증 유형을 구성할 때는 대상에 연결하려면 사용자 이름과 암호를 입력해야 합니다.

![기본 인증을 사용하여 UI 렌더링](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

대상에 대한 기본 인증을 설정하려면 다음을 구성합니다 `customerAuthenticationConfigurations` 섹션 을 통해 `/destinations` 아래에 표시된 것처럼 종단점이 있습니다.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## 베어러 인증 {#bearer}

bearer 인증 유형을 구성할 때 사용자는 대상에서 가져오는 bearer 토큰을 입력해야 합니다.

![베어러 인증을 사용하여 UI 렌더링](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

대상에 대한 베어러 유형 인증을 설정하려면 다음을 구성합니다 `customerAuthenticationConfigurations` 섹션 을 통해 `/destinations` 아래에 표시된 것처럼 종단점이 있습니다.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## OAuth 2 인증 {#oauth2}

사용자가 선택 **[!UICONTROL 대상에 연결]** twitter 사용자 지정 대상 아래 예와 같이 OAuth 2 인증 흐름을 대상으로 트리거합니다. 대상 종단점에 대한 OAuth 2 인증 구성에 대한 자세한 내용은 전용 을 참조하십시오 [Destination SDK OAuth 2 인증 페이지](oauth2-authentication.md).

![OAuth 2 인증을 사용하여 UI 렌더링](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

설정하려면 [!DNL OAuth2] 대상에 대한 인증, 구성 `customerAuthenticationConfigurations` 섹션 을 통해 `/destinations` 아래에 표시된 것처럼 종단점이 있습니다.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Amazon S3 인증 {#s3}

[!DNL Amazon S3] Experience Platform의 파일 기반 대상에 대해 인증이 지원됩니다.

Amazon S3 인증 유형을 구성할 때 사용자가 S3 자격 증명을 입력해야 합니다.

![S3 인증을 사용하여 UI 렌더링](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

설정하려면 [!DNL Amazon S3] 대상에 대한 인증, 구성 `customerAuthenticationConfigurations` 섹션 을 통해 `/destinations` 아래에 표시된 것처럼 종단점이 있습니다.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Azure Blob 인증  {#blob}

[!DNL Azure Blob Storage] Experience Platform의 파일 기반 대상에 대해 인증이 지원됩니다.

Azure Blob 인증 유형을 구성할 때 연결 문자열을 입력해야 합니다.

![Blob 인증을 사용하여 UI 렌더링](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

설정하려면 [!DNL Azure Blob] 대상에 대한 인증, 구성 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래에 표시된 것처럼 종단점이 있습니다.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] 인증 {#adls}

[!DNL Azure Data Lake Storage] Experience Platform의 파일 기반 대상에 대해 인증이 지원됩니다.

를 구성할 때 [!DNL Azure Data Lake Storage] 인증 유형에서는 사용자가 Azure 서비스 사용자 자격 증명과 해당 테넌트 정보를 입력해야 합니다.

![UI 렌더링 [!DNL Azure Data Lake Storage] 인증](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

설정하려면 [!DNL Azure Data Lake Storage] 대상에 대한 (ADLS) 인증에서 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래에 표시된 것처럼 종단점이 있습니다.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## 암호 인증이 있는 SFTP

[!DNL SFTP] Experience Platform의 파일 기반 대상에 대해 암호가 포함된 인증이 지원됩니다.

암호 인증 유형을 사용하여 SFTP를 구성할 때는 SFTP 사용자 이름 및 암호와 SFTP 도메인 및 포트(기본 포트는 22)를 입력해야 합니다.

![암호 인증을 사용하여 SFTP를 통해 UI 렌더링](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

대상에 대한 암호를 사용하여 SFTP 인증을 설정하려면 다음을 구성합니다 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래에 표시된 것처럼 종단점이 있습니다.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SSH 키 인증이 있는 SFTP

[!DNL SFTP] 인증 [!DNL SSH] Experience Platform에서 파일 기반 대상에 대해 키가 지원됩니다.

SSH 키 인증 유형을 사용하여 SFTP를 구성할 때는 SFTP 사용자 이름 및 SSH 키와 SFTP 도메인 및 포트를 입력해야 합니다(기본 포트는 22).

![SSH 키 인증을 사용하여 SFTP로 UI 렌더링](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

대상에 대해 SSH 키를 사용하여 SFTP 인증을 설정하려면 다음을 구성합니다 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래에 표시된 것처럼 종단점이 있습니다.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] 인증 {#gcs}

[!DNL Google Cloud Storage] Experience Platform의 파일 기반 대상에 대해 인증이 지원됩니다.

를 구성할 때 [!DNL Google Cloud Storage] 인증 유형, 사용자는 [!DNL Google Cloud Storage] [!UICONTROL 액세스 키 ID] 및 [!UICONTROL 암호 액세스 키].

![Google 클라우드 스토리지 인증을 사용하여 UI 렌더링](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

설정하려면 [!DNL Google Cloud Storage] 대상에 대한 인증, 구성 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래에 표시된 것처럼 종단점이 있습니다.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 대상 플랫폼에 사용자 인증을 구성하는 방법을 더 잘 이해할 수 있어야 합니다.

다른 대상 구성 요소에 대해 자세히 알려면 다음 문서를 참조하십시오.

* [OAuth2 인증](oauth2-authentication.md)
* [고객 데이터 필드](customer-data-fields.md)
* [UI 속성](ui-attributes.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 게재](destination-delivery.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [집계 정책](aggregation-policy.md)
* [배치 구성](batch-configuration.md)
* [내역 프로필 자격](historical-profile-qualifications.md)