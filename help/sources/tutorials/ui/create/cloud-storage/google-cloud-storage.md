---
title: UI에서 Google 클라우드 스토리지 Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Google 클라우드 스토리지 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---

# UI에서 [!DNL Google Cloud Storage] 소스 연결 만들기

이 자습서에서는 Adobe Experience Platform UI를 사용하여 [!DNL Google Cloud Storage] 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 올바른 [!DNL Google Cloud Storage] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/batch/cloud-storage.md)에 대한 자습서로 진행할 수 있습니다.

### 지원되는 파일 형식

[!DNL Experience Platform]은(는) 외부 저장소에서 수집할 다음 파일 형식을 지원합니다.

* 구분 기호로 구분된 값 (DSV): 모든 단일 문자 값을 DSV 형식 데이터 파일의 구분 기호로 사용할 수 있습니다.
* JavaScript 개체 표기법(JSON): JSON 형식의 데이터 파일은 XDM을 준수해야 합니다.
* Apache Parquet: Parquet 포맷의 데이터 파일은 XDM을 준수해야 합니다.

### 필요한 자격 증명 수집

Experience Platform에서 [!DNL Google Cloud Storage] 데이터에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 액세스 키 ID | Experience Platform에 [!DNL Google Cloud Storage] 계정을 인증하는 데 사용되는 61자 영숫자 문자열입니다. |
| 비밀 액세스 키 | Experience Platform에 [!DNL Google Cloud Storage] 계정을 인증하는 데 사용되는 40자의 Base64로 인코딩된 문자열입니다. |
| 버킷 이름 | [!DNL Google Cloud Storage] 버킷의 이름입니다. 클라우드 저장소의 특정 하위 폴더에 대한 액세스를 제공하려면 버킷 이름을 지정해야 합니다. |
| 폴더 경로 | 액세스 권한을 제공할 폴더의 경로입니다. |

이러한 값에 대한 자세한 내용은 [Google Cloud Storage HMAC 키](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 안내서를 참조하십시오. 자신의 액세스 키 ID와 비밀 액세스 키를 생성하는 방법에 대한 단계는 [[!DNL Google Cloud Storage] 개요](../../../../connectors/cloud-storage/google-cloud-storage.md)를 참조하세요.

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL Google Cloud Storage] 계정을 Experience Platform에 연결할 수 있습니다.

## [!DNL Google Cloud Storage] 계정 연결

Experience Platform UI의 왼쪽 탐색 모음에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 클라우드 저장소] 범주에서 **[!UICONTROL Google 클라우드 저장소]**&#x200B;를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![소스 카탈로그 페이지를 표시하는 Experience Platform UI 화면입니다.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

**[!UICONTROL Google 클라우드 저장소에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정에 연결하려면 연결할 [!DNL Google Cloud Storage] 계정을 선택한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![Experience Platform 클라우드 저장소 원본의 기존 계정 페이지를 표시하는 Google UI 화면](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택하십시오. 표시되는 입력 양식에서 이름, 선택적 설명 및 [!DNL Google Cloud Storage] 자격 증명을 제공합니다. 이 단계에서는 하위 폴더에 대한 경로 이름을 정의하여 계정이 액세스할 하위 폴더를 지정할 수도 있습니다.

완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![Google 클라우드 저장소 원본에 대한 새 계정 페이지를 표시하는 Experience Platform UI 화면입니다.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## 다음 단계

이 자습서에 따라 [!DNL Google Cloud Storage] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [클라우드 저장소에서 Experience Platform으로 데이터를 가져오도록 데이터 흐름을 구성](../../dataflow/batch/cloud-storage.md)할 수 있습니다.
