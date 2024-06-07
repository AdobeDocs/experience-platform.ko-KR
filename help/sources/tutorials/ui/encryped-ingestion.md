---
title: 소스 UI 작업 영역에서 암호화된 데이터 수집
description: 소스 UI 작업 영역에서 암호화된 데이터를 수집하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: f2a0a9b84dfd3c1d32c8049148d38ef4d2ec822e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 7%

---

# 소스 UI에서 암호화된 데이터 수집

일괄 처리 데이터에 대한 클라우드 스토리지 소스를 사용하여 Adobe Experience Platform으로 암호화된 데이터를 수집하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 전제 조건

* 데이터 암호화

## 암호화된 데이터 수집 {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="파일이 암호화되어 있습니까?"
>abstract="이미 암호화된 파일을 수집하는 경우 이 토글을 선택합니다."


>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="샘플 파일 선택"
>abstract="매핑을 생성하려면 암호화된 데이터를 수집할 때 샘플 파일을 수집해야 합니다."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_createCustomKey"
>title="사용자 지정 키 만들기"
>abstract="원할 경우 서명 확인 키 쌍을 만들고 암호화된 데이터에 대한 사용자 지정 키를 만들 수 있습니다."