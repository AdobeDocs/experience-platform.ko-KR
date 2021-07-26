---
keywords: Experience Platform;홈;인기 항목;Azure 테이블 저장소;azure 테이블 저장소;ats;ATS
solution: Experience Platform
title: UI에서 Azure 테이블 저장소 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Azure 테이블 저장소 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: 7af79b9e0d6ed29b796ac7c98b4df1dda09f3513
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# UI에서 [!DNL Azure Table Storage] 소스 연결 만들기

Adobe Experience Platform의 소스 커넥터는 예약된 방식으로 외부 소스 데이터를 수집할 수 있습니다. 이 자습서에서는 [!DNL Platform] 사용자 인터페이스를 사용하여 [!DNL Azure Table Storage](이하 &quot;ATS&quot;라 함) 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 ATS 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/databases.md)에서 자습서를 진행할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL Platform]에서 ATS 계정에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | [!DNL Azure Table Storage] 인스턴스에 연결하는 연결 문자열입니다. ATS 인스턴스에 연결할 연결 문자열입니다. ATS에 대한 연결 문자열 패턴은 `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`입니다. |

시작하는 방법에 대한 자세한 내용은 [이 [!DNL Azure Table Storage] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)를 참조하십시오.

## [!DNL Azure Table Storage] 계정을 연결합니다

필요한 자격 증명을 수집하면 아래 단계에 따라 ATS 계정을 [!DNL Platform]에 연결할 수 있습니다.

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음, 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 **[!UICONTROL 소스]** 작업 영역에 액세스합니다. **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

**[!UICONTROL 데이터베이스]** 범주에서 **[!UICONTROL Azure 테이블 저장소]**&#x200B;를 선택합니다. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**&#x200B;을 선택합니다. 그렇지 않으면 **[!UICONTROL 데이터 추가]**&#x200B;를 선택하여 새 ATS 커넥터를 만듭니다.

![카탈로그](../../../../images/tutorials/create/ats/catalog.png)

**[!UICONTROL Azure 테이블 저장소에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**&#x200B;을 선택합니다. 표시되는 입력 양식에서 이름, 선택적 설명 및 ATS 자격 증명을 제공합니다. 완료되면 **[!UICONTROL Connect]**&#x200B;를 선택한 다음 새 연결이 설정될 시간을 허용합니다.

![connect](../../../../images/tutorials/create/ats/new.png)

### 기존 계정

기존 계정을 연결하려면 연결할 ATS 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속 진행합니다.

![기존](../../../../images/tutorials/create/ats/existing.png)

## 다음 단계

이 자습서에 따라 ATS 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 구성하여 데이터를 [!DNL Platform]](../../dataflow/databases.md)로 가져올 수 있습니다.
