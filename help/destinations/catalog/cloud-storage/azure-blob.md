---
keywords: Azure Blob;Blob 대상;s3;azure Blob 대상
title: Azure Blob 연결 대상
description: Azure Blob 저장소에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 데이터 또는 CSV 데이터 파일을 주기적으로 내보냅니다.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# [!DNL Azure Blob] 연결

[!DNL Azure Blob] (이하 &quot;[!DNL Blob]&quot;라 한다)는 클라우드를 위한 Microsoft의 객체 스토리지 솔루션입니다. 이 자습서에서는 [!DNL Platform] 사용자 인터페이스를 사용하여 [!DNL Blob] 대상을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 Blob 대상이 있는 경우 이 문서의 나머지 부분을 건너뛰고 대상](../../ui/activate-destinations.md)으로 세그먼트를 활성화할 때 튜토리얼을 진행할 수 있습니다.[

### 지원되는 파일 형식

[!DNL Experience Platform] 에서 내보낼 다음 파일 형식을  [!DNL Blob]지원합니다.

- 구분 기호 구분 값(DSV):DSV 형식 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다. 일반 DSV 파일에 대한 지원은 나중에 제공될 예정입니다. 지원되는 파일에 대한 자세한 내용은 [활성화 대상](../../ui/activate-destinations.md#esp-and-cloud-storage)의 튜토리얼에서 클라우드 스토리지 섹션을 참조하십시오.

## Blob 계정 {#connect-destination} 연결

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL 대상]**&#x200B;을 선택하여 **[!UICONTROL 대상]** 작업 영역에 액세스합니다. **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 대상이 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 대상을 찾을 수 있습니다.

**[!UICONTROL 클라우드 스토리지]** 범주에서 **[!UICONTROL Azure Blob 저장소]**&#x200B;을 선택하고 **[!UICONTROL 활성화]**&#x200B;를 차례로 선택합니다.

![카탈로그](../../assets/catalog/cloud-storage/blob/catalog.png)

**[!UICONTROL Azure Blob 저장소에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정 {#new-account}

새 자격 증명을 사용 중인 경우 **[!UICONTROL 새 계정]**&#x200B;을 선택합니다. 표시되는 입력 양식에서 연결 문자열을 입력합니다. Blob 저장소의 데이터에 액세스하는 데 필요한 연결 문자열입니다. [!DNL Blob] 연결 문자열 패턴은 다음으로 시작합니다.`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.

RSA 형식 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수도 있습니다. 이 공개 키 **는 Base64 인코딩 문자열로 기록되어야 합니다.**

![새 계정](../../assets/catalog/cloud-storage/blob/new.png)

### 기존 계정

기존 계정을 연결하려면 연결할 [!DNL Blob] 계정을 선택한 다음 **다음**&#x200B;을 선택하여 계속 진행합니다.

![기존 계정](../../assets/catalog/cloud-storage/blob/existing.png)

## 인증 {#authentication}

**인증** 페이지가 나타납니다. 표시되는 입력 양식에서 이름, 선택적 설명, 폴더 경로 및 파일 컨테이너를 제공합니다. 완료되면 **[!UICONTROL 대상 만들기]**&#x200B;를 선택합니다.

![인증](../../assets/catalog/cloud-storage/blob/authentication.png)

## 다음 단계 {#activate-segments}

이 자습서를 따라 [!DNL Blob] 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행할 수 있으며 [세그먼트를 대상](../../ui/activate-destinations.md)에 활성화할 수 있습니다.
