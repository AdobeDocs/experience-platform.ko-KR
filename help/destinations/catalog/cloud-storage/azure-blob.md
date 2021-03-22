---
keywords: Azure Blob;Blob 대상;s3;azure Blob 대상
title: Azure Blob 연결
description: Azure Blob 저장소에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 데이터 또는 CSV 데이터 파일을 주기적으로 내보냅니다.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 1%

---


# [!DNL Azure Blob] 연결

## 개요 {#overview}

[!DNL Azure Blob] (이하 &quot;[!DNL Blob]&quot;라 한다)는 클라우드를 위한 Microsoft의 객체 스토리지 솔루션입니다. 이 자습서에서는 [!DNL Platform] 사용자 인터페이스를 사용하여 [!DNL Blob] 대상을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 Blob 대상이 있는 경우 이 문서의 나머지 부분을 건너뛰고 대상](../../ui/activate-destinations.md)으로 세그먼트를 활성화할 때 튜토리얼을 진행할 수 있습니다.[

## 지원되는 파일 형식 {#file-formats}

[!DNL Experience Platform] 에서 내보낼 다음 파일 형식을  [!DNL Blob]지원합니다.

- 구분 기호 구분 값(DSV):DSV 형식 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다. 일반 DSV 파일에 대한 지원은 나중에 제공될 예정입니다. 지원되는 파일에 대한 자세한 내용은 [활성화 대상](../../ui/activate-destinations.md#esp-and-cloud-storage)의 튜토리얼에서 클라우드 스토리지 섹션을 참조하십시오.

## Blob 계정 {#connect-destination} 연결

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL Destinations]**&#x200B;를 선택하여 **[!UICONTROL Destinations]** 작업 영역에 액세스합니다. **[!UICONTROL Catalog]** 화면에는 계정을 만들 수 있는 다양한 대상이 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 대상을 찾을 수 있습니다.

**[!UICONTROL Cloud Storage]** 범주에서 **[!UICONTROL Azure Blob Storage]**, 그 뒤에 **[!UICONTROL Configure]**&#x200B;를 선택합니다.

![카탈로그](../../assets/catalog/cloud-storage/blob/catalog.png)

>[!NOTE]
>
>이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL Activate]** 단추가 표시될 수 있습니다. **[!UICONTROL Activate]**&#x200B;과 **[!UICONTROL Configure]** 사이의 차이에 대한 자세한 내용은 대상 작업 공간 설명서의 [카탈로그](../../ui/destinations-workspace.md#catalog) 섹션을 참조하십시오.

**[!UICONTROL Connect to Azure Blob Storage]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

## 새 계정 {#new-account}

새 자격 증명을 사용 중인 경우 **[!UICONTROL New account]**&#x200B;을 선택합니다. 표시되는 입력 양식에서 연결 문자열을 입력합니다. Blob 저장소의 데이터에 액세스하려면 연결 문자열이 필요합니다. [!DNL Blob] 연결 문자열 패턴은 다음으로 시작합니다.`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.

[!DNL Blob] 연결 문자열 구성에 대한 자세한 내용은 Microsoft 설명서에서 [Azure 저장소 계정](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account)에 대한 연결 문자열 구성을 참조하십시오.

RSA 형식 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수도 있습니다. 이 공개 키 **는 Base64 인코딩 문자열로 기록되어야 합니다.**

![새 계정](../../assets/catalog/cloud-storage/blob/new.png)

## 기존 계정 {#existing-account}

기존 계정을 연결하려면 연결할 [!DNL Blob] 계정을 선택한 다음 **다음**&#x200B;을 선택하여 계속 진행합니다.

![기존 계정](../../assets/catalog/cloud-storage/blob/existing.png)

## 인증 {#authentication}

**인증** 페이지가 나타납니다. 표시되는 입력 양식에서 이름, 선택적 설명, 폴더 경로 및 파일 컨테이너를 제공합니다.

이 단계에서 이 대상에 적용할 **[!UICONTROL Marketing actions]**&#x200B;을 선택할 수도 있습니다. 마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

완료되면 **[!UICONTROL Create destination]**&#x200B;을 선택합니다.

![인증](../../assets/catalog/cloud-storage/blob/authentication.png)

## 다음 단계 {#activate-segments}

이 자습서를 따라 [!DNL Blob] 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행할 수 있으며 [세그먼트를 대상](../../ui/activate-destinations.md)에 활성화할 수 있습니다.
