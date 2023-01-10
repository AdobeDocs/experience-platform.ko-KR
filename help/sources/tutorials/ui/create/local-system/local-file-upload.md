---
keywords: Experience Platform;홈;인기 항목;로컬 시스템;파일 업로드;csv 매핑;csv 파일 매핑;csv 파일을 xdm에 매핑;xdm에 csv 매핑;ui 안내서;
solution: Experience Platform
title: UI에서 로컬 파일 업로드 소스 커넥터 만들기
type: Tutorial
description: 로컬 시스템을 위한 소스 연결을 만들어 로컬 파일을 Platform으로 가져오는 방법을 알아봅니다
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# UI에서 로컬 파일 업로드 소스 커넥터 만들기

이 자습서에서는 사용자 인터페이스를 사용하여 로컬 파일을 Platform에 수집하기 위해 로컬 파일 업로드 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## Platform에 로컬 파일 업로드

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL 로컬 시스템] 카테고리, 선택 **[!UICONTROL 로컬 파일 업로드]**&#x200B;를 선택한 다음 을 선택합니다. **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/local/catalog.png)

### 기존 데이터 세트 사용

다음 [!UICONTROL 데이터 흐름 세부 정보] 페이지를 사용하여 CSV 데이터를 기존 데이터 세트에 수집할지 또는 새 데이터 세트에 수집할지를 선택할 수 있습니다.

CSV 데이터를 기존 데이터 세트에 수집하려면 을 선택합니다 **[!UICONTROL 기존 데이터 세트]**. 를 사용하여 기존 데이터 세트를 검색할 수 있습니다 [!UICONTROL 고급 검색] 옵션을 선택하거나 드롭다운 메뉴에서 기존 데이터 세트 목록을 스크롤하여 선택합니다.

데이터 세트를 선택하고 데이터 흐름의 이름과 선택적 설명을 제공합니다.

이 프로세스 중에 [!UICONTROL 오류 진단] 및 [!UICONTROL 부분 수집]. [!UICONTROL 오류 진단] 에서는 데이터 플로우에서 발생하는 모든 잘못된 레코드에 대해 자세한 오류 메시지를 생성하는 반면, [!UICONTROL 부분 수집] 수동으로 정의하는 특정 임계값까지 오류가 포함된 데이터를 수집할 수 있습니다. 자세한 내용은 [부분 배치 수집 개요](../../../../../ingestion/batch-ingestion/partial.md) 추가 정보.

![기존 데이터 세트](../../../../images/tutorials/create/local/existing-dataset.png)

### 새 데이터 세트 사용

CSV 데이터를 새 데이터 세트에 수집하려면 을 선택합니다 **[!UICONTROL 새 데이터 세트]** 그런 다음 출력 데이터 세트 이름과 선택적 설명을 제공합니다. 다음으로 를 사용하여 매핑할 스키마를 선택합니다 [!UICONTROL 고급 검색] 옵션을 선택하거나 드롭다운 메뉴에서 기존 스키마 목록을 스크롤하여 선택합니다.

스키마를 선택하고 데이터 흐름의 이름과 선택적 설명을 제공한 다음 [!UICONTROL 오류 진단] 및 [!UICONTROL 부분 수집] 데이터 플로우에 대한 설정 완료되면 을 선택합니다 **[!UICONTROL 다음]**.

![새로운 데이터 세트](../../../../images/tutorials/create/local/new-dataset.png)

### 데이터 선택

다음 [!UICONTROL 데이터 선택] 로컬 파일을 업로드하고 해당 구조 및 컨텐츠를 미리 볼 수 있는 인터페이스를 제공하는 단계가 나타납니다. 선택 **[!UICONTROL 파일 선택]** 를 눌러 로컬 시스템에서 CSV 파일을 업로드합니다. 또는 업로드할 CSV 파일을 [!UICONTROL 파일 드래그 앤 드롭] 패널.

>[!TIP]
>
>로컬 파일 업로드에서는 현재 CSV 파일만 지원합니다. 각 파일의 최대 파일 크기는 1GB입니다.

![choose-files](../../../../images/tutorials/create/local/choose-files.png)

파일을 업로드하면 미리 보기 인터페이스가 업데이트되어 파일의 컨텐츠와 구조를 표시합니다.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

파일에 따라, 소스 데이터에 대한 탭, 쉼표, 파이프 또는 사용자 지정 열 구분 기호와 같은 열 구분 기호를 선택할 수 있습니다. 을(를) 선택합니다 **[!UICONTROL 구분 기호]** 드롭다운 화살표를 클릭한 다음 메뉴에서 적절한 구분 기호를 선택합니다.

완료되면 을 선택합니다 **[!UICONTROL 다음]**.

![구분 기호](../../../../images/tutorials/create/local/delimiter.png)

## 매핑

다음 [!UICONTROL 매핑] 소스 스키마의 소스 필드를 대상 스키마의 적절한 대상 XDM 필드에 매핑하는 인터페이스를 제공하는 단계가 나타납니다.

필요에 따라 필드를 직접 매핑하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산 또는 계산된 값을 도출할 수 있습니다. 매핑 인터페이스 사용에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md).

매핑 세트가 준비되면 을 선택합니다 **[!UICONTROL 완료]** 또한 새 데이터 흐름을 만들 잠시 동안 허용합니다.

![매핑](../../../../images/tutorials/create/local/mapping.png)

## 데이터 수집 모니터링

CSV 파일이 매핑되고 생성되면 모니터링 대시보드를 사용하여 CSV 파일을 통해 수집되는 데이터를 모니터링할 수 있습니다. 자세한 내용은 [UI에서 소스 데이터 흐름 모니터링](../../../../../dataflows/ui/monitor-sources.md).

## 다음 단계

이 자습서를 따라 플랫 CSV 파일을 XDM 스키마에 매핑하고 플랫폼으로 수집했습니다. 이제 이 데이터를 다운스트림에서 사용할 수 있습니다 [!DNL Platform] 와 같은 서비스 [!DNL Real-Time Customer Profile]. 다음 기간 동안 개요를 참조하십시오. [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) 추가 정보.
