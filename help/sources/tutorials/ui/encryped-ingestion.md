---
title: 소스 UI Workspace에서 암호화된 데이터 수집
description: 소스 UI 작업 영역에서 암호화된 데이터를 수집하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 9f827c1ba97fba237c216fce9c2966bcc91fd05b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 30%

---

# 소스 UI에서 암호화된 데이터 수집

일괄 처리 데이터에 대한 클라우드 스토리지 소스를 사용하여 Adobe Experience Platform으로 암호화된 데이터를 수집하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 전제 조건

* 데이터 암호화

## 암호화된 데이터 수집 {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="파일이 암호화되어 있습니까?"
>abstract="이미 암호화된 파일을 수집하는 경우 이 토글을 선택하십시오."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="샘플 파일 선택"
>abstract="매핑을 생성하려면 암호화된 데이터를 수집할 때 샘플 파일을 수집해야 합니다."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="암호화 키 ID"
>abstract="소스 데이터를 암호화하는 데 사용된 암호화 키에 해당하는 암호화 키 ID를 입력하십시오."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="서명 확인 키 ID"
>abstract="서명되고 암호화된 소스 데이터에 해당하는 서명 확인 키 ID를 제공합니다."

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
