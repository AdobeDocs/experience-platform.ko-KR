---
keywords: Azure Blob;Blob 대상;s3;azure Blob 대상
title: Azure Blob 연결
description: Azure Blob 저장 공간에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform에서 CSV 데이터 파일을 주기적으로 내보냅니다.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: a07557ec398631ece0c8af6ec7b32e0e8593e24b
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 1%

---

# [!DNL Azure Blob] 연결

## 대상 변경 로그 {#changelog}

>[!IMPORTANT]
>
>데이터 세트 내보내기 기능의 베타 릴리스와 향상된 파일 내보내기 기능을 사용하면 이제 두 가지 기능이 표시될 수 있습니다 [!DNL Azure Blob] 대상 카탈로그에 있는 카드.
>* 이미 파일을 로 내보내는 경우 **[!UICONTROL Azure Blob]** 대상: 새 데이터 흐름을 새로 만드세요 **[!UICONTROL Azure Blob 베타]** 대상.
>* 데이터 흐름을 아직 만들지 않았다면 **[!UICONTROL Azure Blob]** 대상, 새 **[!UICONTROL Azure Blob 베타]** 파일로 내보내기 **[!UICONTROL Azure Blob]**.


![나란히 보기에서 두 Azure Blob 대상 카드의 이미지입니다.](../../assets/catalog/cloud-storage/blob/two-azure-blob-destination-cards.png)

새로운 기능 개선 사항 [!DNL Azure Blob] 대상 카드는 다음과 같습니다.

* [데이터 집합 내보내기 지원](/help/destinations/ui/export-datasets.md).
* 추가 [파일 이름 지정 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 를 통해 내보낸 파일에서 사용자 지정 파일 헤더를 설정할 수 있습니다. [매핑 단계 개선](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [내보낸 CSV 데이터 파일의 형식을 사용자 지정하는 기능](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 개요 {#overview}

[!DNL Azure Blob] (이하 &quot;라 한다) [!DNL Blob])은 클라우드를 위한 Microsoft의 개체 스토리지 솔루션입니다. 이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Blob] 대상 [!DNL Platform] 사용자 인터페이스.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Blob] 대상, 이 문서의 나머지 부분을 건너뛰고 다음 의 자습서를 진행할 수 있습니다. [대상에 세그먼트 활성화](../../ui/activate-batch-profile-destinations.md).

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 전자 메일 주소, 전화 번호, 성)을 선택한 대로 [대상 활성화 워크플로우](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 지원되는 파일 형식 {#file-formats}

[!DNL Experience Platform] 에서는 내보낼 다음 파일 형식을 지원합니다 [!DNL Azure Blob]:

* 쉼표로 구분된 값(CSV): 내보낸 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 입력합니다.

### 대상에 인증 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="RSA 공개 키"
>abstract="선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 설명서 링크에서 올바른 형식의 키의 예를 봅니다."

대상을 인증하려면 필요한 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**.

* **[!UICONTROL 연결 문자열]**: Blob 저장소의 데이터에 액세스하려면 연결 문자열이 필요합니다. 다음 [!DNL Blob] 연결 문자열 패턴은 다음으로 시작: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * 구성에 대한 자세한 정보 [!DNL Blob] 연결 문자열을 참조하십시오. [Azure 저장소 계정에 대한 연결 문자열 구성](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) ( Microsoft 설명서)를 참조하십시오.
* **[!UICONTROL 암호화 키]**: 선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

   ![UI에서 올바른 형식의 PGP 키의 예를 보여주는 이미지](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 컨테이너]**: 이름 입력 [!DNL Azure Blob Storage] 이 대상에서 사용할 컨테이너입니다.
* **[!UICONTROL 파일 유형]**: 내보낸 파일에 사용할 형식 Experience Platform을 선택합니다. 이 옵션은 **[!UICONTROL Azure Blob 베타]** 대상. 을(를) 선택할 때 [!UICONTROL CSV] 선택 사항 [파일 서식 옵션 구성](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 압축 포맷]**: 내보낸 파일에 사용할 압축 유형을 Experience Platform에서 선택합니다. 이 옵션은 **[!UICONTROL Azure Blob 베타]** 대상.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## (베타) 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 집합 내보내기를 지원합니다. 데이터 집합 내보내기를 설정하는 방법에 대한 자세한 내용은 [데이터 세트 내보내기 자습서](/help/destinations/ui/export-datasets.md).

## 내보낸 데이터 {#exported-data}

대상 [!DNL Azure Blob Storage] 대상, [!DNL Platform] 만들기 `.csv` 파일을 입력한 저장 위치에 저장합니다. 파일에 대한 자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 세그먼트 활성화 자습서에서 를 참조하십시오.