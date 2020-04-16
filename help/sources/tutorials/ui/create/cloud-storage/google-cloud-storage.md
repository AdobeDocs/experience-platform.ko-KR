---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 Google 클라우드 스토리지 소스 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# UI에서 Google 클라우드 스토리지 소스 커넥터 만들기

Adobe Experience Platform의 소스 커넥터는 외부 소스 데이터를 일정 기준에 따라 인제스트할 수 있는 기능을 제공합니다. 이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 Google 클라우드 스토리지(이하 &quot;GCS&quot;) 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의](../../../../../xdm/schema/composition.md)기본 사항:스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [실시간 고객 프로필](../../../../../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.

이미 GCS 기반 연결을 사용하고 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성에 대한 자습서로 진행할 수 있습니다](../../dataflow/cloud-storage.md).

### 지원되는 파일 형식

Experience Platform은 외부 스토리지에서 인제스트할 다음 파일 형식을 지원합니다.

* 구분 기호 구분 값(DSV):DSV 형식 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다. DSV 형식 파일 내의 필드 헤더 값은 영숫자 문자와 밑줄로만 구성되어야 합니다. 일반 DSV 파일에 대한 지원이 나중에 제공될 예정입니다.
* JavaScript 개체 표기법(JSON):JSON 형식 데이터 파일은 XDM과 호환되어야 합니다.
* Apache Partiquet:쪽모이 세공 마루 형식 데이터 파일은 XDM과 호환되어야 합니다.

### 필요한 자격 증명 수집

플랫폼에서 GCS 데이터에 액세스하려면 유효한 GCS 액세스 키 ID 및 **암호를** 제공해야 **합니다**. Google Cloud에 대한 <a href="https://cloud.google.com/docs/authentication/production" target="_blank">서버 간 인증 안내서를</a> 읽어 이러한 값을 얻는 방법에 대한 자세한 내용을 살펴볼 수 있습니다.

## GCS 계정 연결

필요한 자격 증명을 수집했으면 아래 절차에 따라 GCS 계정을 플랫폼에 연결하는 새 인바운드 기본 연결을 만들 수 있습니다.

Adobe Experience <a href="https://platform.adobe.com" target="_blank">Platform에</a> 로그인한 다음 **왼쪽 탐색** 표시줄에서 Sources를 선택하여 *Sources* 작업 영역에 액세스할 수있습니다. [ *카탈로그* ] 화면에는 인바운드 기본 연결을 만들 수 있는 다양한 소스가 표시되며, 각 소스에는 연결된 기존 기본 연결의 수가 표시됩니다.

클라우드 *스토리지* 카테고리 아래에서 **Google 클라우드** 스토리지를 선택하여 화면 오른쪽에 정보 막대를 표시합니다. 정보 표시줄에서는 선택한 소스에 대한 간단한 설명과 소스 뷰와 연결하거나 소스와 연결할 수 있는 옵션을 제공합니다. 새 인바운드 기본 연결을 만들려면 Connect **소스를**&#x200B;클릭합니다.

![](../../../../images/tutorials/create/google-cloud-storage/sources-catalog.png)

Google _Cloud 스토리지에 연결_ 대화 상자가 나타납니다. 입력 양식에서 이름, 선택적 설명 및 GCS 자격 증명으로 기본 연결을 제공합니다. 완료되면 Connect **를** 클릭한 다음 새 기본 연결을 설정하는 데 약간의 시간이 소요됩니다.

![](../../../../images/tutorials/create/google-cloud-storage/gcs-credentials.png)

기본 연결이 설정되면 다음 섹션으로 계속 이동하여 데이터를 Platform으로 가져오도록 데이터 흐름을 구성할 수 있습니다.

## 다음 단계

이 튜토리얼을 따라 GCS 계정에 대한 기본 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하고 데이터를 Platform으로 가져오도록 데이터 흐름을 [구성할 수 있습니다](../../dataflow/cloud-storage.md).