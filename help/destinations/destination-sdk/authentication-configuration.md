---
description: Adobe Experience Platform Destination SDK에서 지원되는 인증 구성을 사용하여 사용자를 인증하고 대상 엔드포인트에 대한 데이터를 활성화하십시오.
title: 인증 구성
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# 인증 구성 {#credentials}

## 지원되는 인증 유형 {#supported-authentication-types}

선택하는 인증 구성은 Platform UI에서 Experience Platform이 대상에 대해 인증하는 방법을 결정합니다.

Adobe Experience Platform Destination SDK은 여러 인증 유형을 지원합니다.

* [전달자 인증](#bearer)
* [기본 인증](#basic)
* [[!DNL Amazon S3] 인증](#s3)
* [[!DNL Azure Blob] 스토리지](#blob)
* [[!DNL Azure Data Lake Storage]](#adls)
* [[!DNL Google Cloud Storage]](#gcs)
* [SSH 키가 포함된 SFTP](#sftp-ssh)
* [암호가 포함된 SFTP](#sftp-password)
* [인증 코드가 있는 OAuth 2](#oauth2)
* [암호 부여가 있는 OAUth 2](#oauth2)
* [클라이언트 자격 증명 부여가 있는 OAuth 2](#oauth2)

다음을 통해 대상에 대한 인증 정보를 구성할 수 있습니다. `customerAuthenticationConfigurations` 매개 변수 `/destinations` 엔드포인트.

각 대상 유형에 대한 인증 구성 세부 정보는 다음 섹션을 참조하십시오.

* [스트리밍 대상에 대한 인증 구성](destination-configuration.md#customer-authentication-configurations)
* [파일 기반 대상에 대한 인증 구성](file-based-destination-configuration.md#customer-authentication-configurations)

## 기본 인증 {#basic}

Experience Platform의 스트리밍 대상에 대해 기본 인증이 지원됩니다.

기본 인증 유형을 구성할 때 사용자는 대상에 연결하기 위해 사용자 이름과 암호를 입력해야 합니다.

대상에 대한 기본 인증을 설정하려면 `customerAuthenticationConfigurations` 섹션을 통해 `/destinations` 아래와 같은 엔드포인트:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## 전달자 인증 {#bearer}

Experience Platform의 스트리밍 대상에 대해 전달자 인증이 지원됩니다.

대상에 대한 전달자 유형 인증을 설정하려면 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래와 같은 엔드포인트:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## [!DNL Amazon S3] 인증 {#s3}

[!DNL Amazon S3] Experience Platform의 파일 기반 대상에 대해 인증이 지원됩니다.

설정하려면 [!DNL Amazon S3] 대상에 대한 인증, 다음을 구성하십시오. `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래와 같은 엔드포인트:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] Experience Platform의 파일 기반 대상에 대해 인증이 지원됩니다.

설정하려면 [!DNL Azure Blob] 대상에 대한 인증, 다음을 구성하십시오. `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래와 같은 엔드포인트:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] Experience Platform의 파일 기반 대상에 대해 인증이 지원됩니다.

설정하려면 [!DNL Azure Data Lake Storage] 대상에 대한 (ADLS) 인증, 다음을 구성합니다. `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래와 같은 엔드포인트:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## [!DNL Google Cloud Storage] {#gcs}

[!DNL Google Cloud Storage] Experience Platform의 파일 기반 대상에 대해 인증이 지원됩니다.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## [!DNL SFTP] 인증 [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] 인증 [!DNL SSH] Experience Platform의 파일 기반 대상에 대해서는 키가 지원됩니다.

대상에 대해 SSH 키를 사용하여 SFTP 인증을 설정하려면 다음을 구성합니다. `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래와 같은 엔드포인트:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL SFTP] 암호를 사용한 인증 {#sftp-password}

[!DNL SFTP] Experience Platform의 파일 기반 대상에 대해서는 암호가 포함된 인증이 지원됩니다.

대상에 대해 암호를 사용하여 SFTP 인증을 설정하려면 다음을 구성하십시오. `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 아래와 같은 엔드포인트:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## [!DNL OAuth 2] 인증 {#oauth2}

[!DNL OAuth 2] Experience Platform의 스트리밍 대상에 대해 인증이 지원됩니다.

지원되는 다양한 을(를) 설정하는 방법에 대한 자세한 정보 [!DNL OAuth 2] 플로우 및 사용자 정의 [!DNL OAuth 2] 지원:에서 Destination SDK 설명서 읽기 [[!DNL OAuth 2] 인증](./oauth2-authentication.md).


## 사용 시기 `/credentials` API 엔드포인트 {#when-to-use}

>[!IMPORTANT]
>
>대부분의 경우 *금지* 을(를) 사용해야 함 `/credentials` API 엔드포인트. 대신 를 통해 대상에 대한 인증 정보를 구성할 수 있습니다. `customerAuthenticationConfigurations` 매개 변수 `/destinations` 엔드포인트.

다음 `/credentials` API 끝점은 Adobe과 대상 사이에 글로벌 인증 시스템이 있는 경우 대상 개발자에게 제공됩니다. [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다.

이 경우 다음을 사용하여 자격 증명 개체를 만들어야 합니다 `/credentials` API 엔드포인트. 또한 다음을 선택해야 합니다. `PLATFORM_AUTHENTICATION` 다음에서 [대상 구성](./destination-configuration.md#destination-delivery). 읽기 [자격 증명 API 끝점 작업](./credentials-configuration-api.md) 에서 수행할 수 있는 전체 작업 목록 `/credentials` 엔드포인트.
