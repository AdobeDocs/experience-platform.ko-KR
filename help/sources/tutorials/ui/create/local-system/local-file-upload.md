---
keywords: Experience Platform;홈;인기 항목;로컬 시스템;파일 업로드;csv 매핑;csv 파일 매핑;csv 파일을 xdm으로 매핑;csv를 xdm으로 매핑;ui 안내서;
solution: Experience Platform
title: UI에서 로컬 파일 만들기 Source 커넥터 업로드
type: Tutorial
description: 로컬 시스템에 대한 소스 연결을 만들어 로컬 파일을 플랫폼으로 가져오는 방법에 대해 알아봅니다
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# UI에서 로컬 파일 업로드 소스 커넥터 만들기

이 자습서에서는 사용자 인터페이스를 사용하여 로컬 파일을 플랫폼으로 수집할 로컬 파일 업로드 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음 플랫폼 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 플랫폼에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 로컬 파일을 Platform에 업로드

Platform UI의 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 로컬 시스템] 범주에서 **[!UICONTROL 로컬 파일 업로드]**&#x200B;를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/local/catalog.png)

### 기존 데이터 세트 사용

[!UICONTROL 데이터 흐름 세부 정보] 페이지에서 CSV 데이터를 기존 데이터 세트로 수집할지 또는 새 데이터 세트로 수집할지 여부를 선택할 수 있습니다.

CSV 데이터를 기존 데이터 세트로 수집하려면 **[!UICONTROL 기존 데이터 세트]**&#x200B;를 선택하십시오. [!UICONTROL 고급 검색] 옵션을 사용하거나 드롭다운 메뉴에서 기존 데이터 세트 목록을 스크롤하여 기존 데이터 세트를 검색할 수 있습니다.

데이터 세트를 선택한 상태에서 데이터 흐름의 이름과 설명(선택 사항)을 입력합니다.

이 프로세스 동안 [!UICONTROL 오류 진단] 및 [!UICONTROL 부분 수집]을 사용하도록 설정할 수도 있습니다. [!UICONTROL 오류 진단]을 사용하면 데이터 흐름에서 발생하는 모든 잘못된 레코드에 대해 자세한 오류 메시지를 생성할 수 있고, [!UICONTROL 부분 수집]을(를) 사용하면 수동으로 정의하는 특정 임계값까지 오류가 포함된 데이터를 수집할 수 있습니다. 자세한 내용은 [부분 일괄 처리 수집 개요](../../../../../ingestion/batch-ingestion/partial.md)를 참조하십시오.

![기존 데이터 세트](../../../../images/tutorials/create/local/existing-dataset.png)

### 새 데이터 세트 사용

CSV 데이터를 새 데이터 세트로 수집하려면 **[!UICONTROL 새 데이터 세트]**&#x200B;를 선택한 다음 출력 데이터 세트 이름과 선택적 설명을 입력하십시오. 그런 다음 [!UICONTROL 고급 검색] 옵션을 사용하거나 드롭다운 메뉴에서 기존 스키마 목록을 스크롤하여 매핑할 스키마를 선택합니다.

스키마를 선택한 상태에서 데이터 흐름의 이름과 선택적 설명을 제공한 다음 데이터 흐름에 사용할 [!UICONTROL 오류 진단] 및 [!UICONTROL 부분 수집] 설정을 적용합니다. 완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![new-dataset](../../../../images/tutorials/create/local/new-dataset.png)

### 데이터 선택

로컬 파일을 업로드하고 해당 구조와 내용을 미리 볼 수 있는 인터페이스를 제공하는 [!UICONTROL 데이터 선택] 단계가 나타납니다. 로컬 시스템에서 CSV 파일을 업로드하려면 **[!UICONTROL 파일 선택]**&#x200B;을 선택하십시오. 또는 업로드할 CSV 파일을 [!UICONTROL 파일 드래그 앤 드롭] 패널로 드래그 앤 드롭할 수 있습니다.

>[!TIP]
>
>로컬 파일 업로드는 현재 CSV 파일만 지원합니다. 각 파일의 최대 파일 크기는 1GB입니다.

![파일 선택](../../../../images/tutorials/create/local/choose-files.png)

파일이 업로드되면 미리보기 인터페이스가 업데이트되어 파일의 내용과 구조가 표시됩니다.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

파일에 따라 소스 데이터에 대한 탭, 쉼표, 파이프 또는 사용자 지정 열 구분 기호와 같은 열 구분 기호를 선택할 수 있습니다. **[!UICONTROL 구분 기호]** 드롭다운 화살표를 선택한 다음 메뉴에서 적절한 구분 기호를 선택합니다.

완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![구분 기호](../../../../images/tutorials/create/local/delimiter.png)

## 매핑

소스 스키마의 소스 필드를 대상 스키마의 해당 대상 XDM 필드에 매핑할 수 있는 인터페이스를 제공하는 [!UICONTROL 매핑] 단계가 나타납니다.

필요에 따라 필드를 직접 매핑하도록 선택하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산된 값 또는 계산된 값을 파생할 수 있습니다. 매핑 인터페이스 사용에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md)를 참조하십시오.

매핑 세트가 준비되면 **[!UICONTROL 마침]**&#x200B;을(를) 선택하여 새 데이터 흐름을 만들 수 있도록 잠시 기다립니다.

![매핑](../../../../images/tutorials/create/local/mapping.png)

## 데이터 수집 모니터링

CSV 파일이 매핑되고 생성되면 모니터링 대시보드를 사용하여 CSV 파일을 통해 수집되는 데이터를 모니터링할 수 있습니다. 자세한 내용은 [UI에서 원본 데이터 흐름 모니터링](../../../../../dataflows/ui/monitor-sources.md)에 대한 자습서를 참조하십시오.

## 다음 단계

이 자습서에 따라 플랫 CSV 파일을 XDM 스키마에 매핑하고 Platform에 수집했습니다. 이제 [!DNL Real-Time Customer Profile]과(와) 같은 다운스트림 [!DNL Platform] 서비스에서 이 데이터를 사용할 수 있습니다. 자세한 내용은 [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)에 대한 개요를 참조하십시오.
