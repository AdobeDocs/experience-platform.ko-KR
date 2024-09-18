---
title: 소스 UI Workspace에서 암호화된 데이터 수집
description: 소스 UI 작업 영역에서 암호화된 데이터를 수집하는 방법을 알아봅니다.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: b4545943abbb68d36a64935feb4466d075331504
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 15%

---

# 소스 UI에서 암호화된 데이터 수집

>[!AVAILABILITY]
>
>소스 UI에서 암호화된 데이터 수집에 대한 지원은 베타 버전이며 조직에서 사용하지 못할 수 있습니다. 기능 및 설명서는 변경될 수 있습니다.

클라우드 스토리지 배치 소스를 사용하여 Adobe Experience Platform에 암호화된 데이터 파일 및 폴더를 수집할 수 있습니다. 암호화된 데이터 수집을 통해 비대칭 암호화 메커니즘을 활용하여 배치 데이터를 안전하게 Experience Platform으로 전송할 수 있습니다. 현재 지원되는 비대칭 암호화 메커니즘은 PGP와 GPG이다.

이 기능은 다음 소스에서 사용할 수 있습니다.

* [Amazon S3]
* [Azure Blob]
* [Azure Data Lake Storage Gen2]
* [Azure 파일 저장소]
* [데이터 랜딩 영역]
* [FTP]
* [Google 클라우드 저장소]
* [HDFS]
* [Oracle 개체 저장소]
* [SFTP]

UI를 사용하여 클라우드 스토리지 일괄 처리 소스로 암호화된 데이터를 수집하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 시작하기

UI에서 암호화된 데이터 수집으로 작업하기 전에 다음 Experience Platform 기능 및 개념을 이해하는 것이 좋습니다.

* [소스](../../home.md): Experience Platform의 소스를 사용하여 Adobe 응용 프로그램 또는 타사 데이터 원본에서 데이터를 수집합니다.
* [데이터 흐름](../../../dataflows/home.md): 데이터 흐름은 Experience Platform 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 소스 작업 영역을 사용하여 주어진 소스에서 Experience Platform으로 데이터를 수집하는 데이터 흐름을 만들 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform에서 샌드박스를 사용하여 Experience Platform 인스턴스 간에 가상 파티션을 만들고 개발 또는 프로덕션 전용 환경을 만듭니다.

### 높은 수준 개요

1. Experience Platform UI의 소스 작업 영역을 사용하여 암호화 키 쌍을 만듭니다. 원할 경우 서명 확인 키 쌍을 만들어 암호화된 데이터에 추가 보안 계층을 제공할 수도 있습니다.
2. 공개 키를 사용하여 데이터를 암호화합니다.
3. 클라우드 스토리지 공급자에 암호화된 데이터를 배치합니다. 이 단계에서는 소스 데이터를 XDM(Experience Data Model) 스키마에 매핑하는 참조로 사용할 수 있는 샘플 파일도 있는지 확인해야 합니다.
4. 소스 연결을 만들어 암호화된 데이터를 Experience Platform에 수집합니다.
5. 소스 연결을 만드는 동안 데이터를 암호화하는 데 사용한 공개 키에 해당하는 키 ID를 제공하십시오. 서명 확인 키 쌍 메커니즘도 사용한 경우 암호화된 데이터에 해당하는 서명 확인 키 ID도 제공해야 합니다.
6. 데이터 흐름 생성 단계로 진행합니다.

## 암호화 키 쌍 만들기 {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="암호화 키 ID"
>abstract="소스 데이터를 암호화하는 데 사용된 암호화 키와 일치하는 암호화 키 ID를 제공합니다."

* Platform UI에서 소스 작업 영역으로 이동한 다음 상단 헤더에서 [!UICONTROL 키 쌍]을 선택합니다.
* 조직의 기존 암호화 키 쌍 목록을 표시하는 페이지로 이동합니다. 이 페이지에서는 해당 키의 제목, ID, 유형, 암호화 알고리즘, 만료 및 상태에 대한 정보를 제공합니다. 새 키 쌍을 만들려면 **[!UICONTROL 키 만들기]**&#x200B;를 선택합니다.
* 그런 다음 만들려는 키 유형을 선택합니다. 암호화 키를 만들려면 **[!UICONTROL 암호화 키]**&#x200B;를 선택한 다음 암호화 키의 제목과 암호를 입력하십시오. 암호는 암호화 키에 대한 추가 보호 계층입니다. 생성 시 Experience Platform은 암호를 공개 키와 다른 보안 저장소에 저장합니다. 비어 있지 않은 문자열을 암호로 제공해야 합니다.

### 서명 인증 키 만들기 {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="서명 인증 키 ID"
>abstract="귀하의 서명이 들어간 암호화 소스 데이터에 해당하는 서명 인증 키 ID를 제공합니다."

## 암호화된 데이터 수집 {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="파일이 암호화되어 있습니까?"
>abstract="이미 암호화된 파일을 수집하는 경우 이 토글을 선택하십시오."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="샘플 파일 선택"
>abstract="매핑을 생성하려면 암호화된 데이터를 수집할 때 샘플 파일을 수집해야 합니다."


<!-- 
## Outline

Sections:

* Create public key
* Create customer key
* Create sources flow to ingest encrypted data
  * File ingestion
  * Folder ingestion
* Updated encrypted flow

* Select [!UICONTROL Key Pairs] from the header in the sources UI workspace.
  * You are taken to the [!UICONTROL Key Pairs] page:
    * Select **[!UICONTROL Encryption key]** for list of key pairs that you have created and managed.
    * Select **[!UICONTROL Customer key]** for a list of key pairs that your customers have created and managed.
* Key Pair functions:
  * Select **[!UICONTROL Key details]** to view key details.
  * Select **[!UICONTROL Delete]** to delete.
* Select [!UICONTROL Create key] to create either an encryption key or a customer key

## Questions and clarifications

* Public key vs. customer key
* Verify E2E:
  * Create keys (encryption key or customer key)
  * Use these keys to encrypt your data
  * Place your encrypted data in your cloud storage (Amazon S3 or Google Cloud Storage)
  * Ingest that encrypted data to Experience Platform by creating a source connection
    * Select the encrypted source data
    * Enable "Is the file encrypted"
    * Select/upload sample file for mapping
    * Use the encryption key name that corresponds with the key used to encrypt the source data
      * If the data was encrypted using customer key, provide the sign verification key.
  * Proceed with source connection creation flow -->
