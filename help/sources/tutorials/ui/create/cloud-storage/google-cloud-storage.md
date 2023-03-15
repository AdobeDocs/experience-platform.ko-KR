---
title: UI에서 Google 클라우드 스토리지 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Google 클라우드 스토리지 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# 만들기 [!DNL Google Cloud Storage] UI의 소스 연결

이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL Google Cloud Storage] Adobe Experience Platform UI를 사용한 소스 연결.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 을(를) 가지고 있는 경우 [!DNL Google Cloud Storage] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 튜토리얼을 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/batch/cloud-storage.md).

### 지원되는 파일 형식

[!DNL Experience Platform] 는 외부 스토리지에서 수집할 다음 파일 형식을 지원합니다.

* 구분 기호로 구분된 값 (DSV): 모든 단일 문자 값을 DSV 형식 데이터 파일의 구분 기호로 사용할 수 있습니다.
* JavaScript 개체 표기법(JSON): JSON 형식의 데이터 파일은 XDM을 준수해야 합니다.
* Apache Parquet: Parquet 포맷의 데이터 파일은 XDM을 준수해야 합니다.

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Google Cloud Storage] data on Platform에서 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 액세스 키 ID | 인증을 위해 사용되는 61자의 영숫자 문자열 [!DNL Google Cloud Storage] 계정을 플랫폼에 추가합니다. |
| 비밀 액세스 키 | 인증을 위해 사용되는 40자의 base64로 인코딩된 문자열 [!DNL Google Cloud Storage] 계정을 플랫폼에 추가합니다. |
| 버킷 이름 | 의 이름 [!DNL Google Cloud Storage] 버킷. 클라우드 저장소의 특정 하위 폴더에 대한 액세스를 제공하려면 버킷 이름을 지정해야 합니다. |
| 폴더 경로 | 액세스 권한을 제공할 폴더의 경로입니다. |

이러한 값에 대한 자세한 내용은 [Google 클라우드 스토리지 HMAC 키](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 가이드. 자신의 액세스 키 ID 및 비밀 액세스 키를 생성하는 방법에 대한 단계는 [[!DNL Google Cloud Storage] 개요](../../../../connectors/cloud-storage/google-cloud-storage.md).

필요한 자격 증명을 수집했으면 아래 단계에 따라 를 연결할 수 있습니다. [!DNL Google Cloud Storage] 계정을 플랫폼에 추가합니다.

## 연결 [!DNL Google Cloud Storage] account

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL 클라우드 스토리지] 범주, 선택 **[!UICONTROL Google 클라우드 스토리지]** 다음을 선택합니다. **[!UICONTROL 데이터 추가]**.

![소스 카탈로그 페이지를 표시하는 Platform UI 화면입니다.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

다음 **[!UICONTROL Google 클라우드 스토리지에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 [!DNL Google Cloud Storage] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속합니다.

![Google Cloud Storage 소스에 대한 기존 계정 페이지를 표시하는 Platform UI 화면](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 설명(선택 사항) 및 [!DNL Google Cloud Storage] 자격 증명. 이 단계에서는 하위 폴더에 대한 경로 이름을 정의하여 계정이 액세스할 하위 폴더를 지정할 수도 있습니다.

완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![Google 클라우드 스토리지 소스에 대한 새 계정 페이지를 표시하는 플랫폼 UI 화면입니다.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## 다음 단계

이 자습서를 따라 [!DNL Google Cloud Storage] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [클라우드 스토리지에서 플랫폼으로 데이터를 가져오도록 데이터 흐름을 구성합니다.](../../dataflow/batch/cloud-storage.md).
