---
keywords: Azure Blob;Blob 대상;s3;azure Blob 대상
title: Azure Blob 연결
description: Azure Blob 저장 공간에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform에서 CSV 데이터 파일을 주기적으로 내보냅니다.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# [!DNL Azure Blob] 연결

## 개요 {#overview}

[!DNL Azure Blob] (이하 &quot;라 한다) [!DNL Blob])은 클라우드를 위한 Microsoft의 개체 스토리지 솔루션입니다. 이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Blob] 대상 [!DNL Platform] 사용자 인터페이스.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Blob] 대상, 이 문서의 나머지 부분을 건너뛰고 다음 의 자습서를 진행할 수 있습니다. [대상에 세그먼트 활성화](../../ui/activate-batch-profile-destinations.md).

## 지원되는 파일 형식 {#file-formats}

[!DNL Experience Platform] 에서는 내보낼 다음 파일 형식을 지원합니다 [!DNL Blob]:

* 구분 기호로 구분된 값(DSV): DSV 형식 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다. 일반적인 DSV 파일에 대한 지원은 향후에 제공됩니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 연결 문자열]**: Blob 저장소의 데이터에 액세스하려면 연결 문자열이 필요합니다. 다음 [!DNL Blob] 연결 문자열 패턴은 다음으로 시작: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * 구성에 대한 자세한 정보 [!DNL Blob] 연결 문자열을 참조하십시오. [Azure 저장소 계정에 대한 연결 문자열 구성](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) ( Microsoft 설명서)를 참조하십시오.

* 선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩된 문자열입니다.
* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 컨테이너]**: 이름 입력 [!DNL Azure Blob Storage] 이 대상에서 사용할 컨테이너입니다.

선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩된 문자열입니다.

## 세그먼트를 이 대상에 활성화 {#activate}

자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.
