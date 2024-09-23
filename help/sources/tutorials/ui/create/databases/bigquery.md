---
title: UI에서 Google Big Query Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Google Big Query 소스 연결을 만드는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: ae322ee421edd73cd5a3fb8499267cd417491318
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# UI에서 [!DNL Google BigQuery] 소스 연결 만들기

>[!IMPORTANT]
>
>[!DNL Google BigQuery] 원본은 Real-time Customer Data Platform Ultimate를 구입한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

사용자 인터페이스를 사용하여 [!DNL Google BigQuery] 계정을 Adobe Experience Platform에 연결하는 방법에 대해 알아보려면 이 자습서를 참조하십시오.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 올바른 [!DNL Google BigQuery] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/databases.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

필요한 자격 증명을 수집하는 자세한 단계는 [[!DNL Google BigQuery] 인증 안내서](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)를 참조하십시오.

## Google BigQuery 계정 연결

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 창을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 데이터베이스] 범주에서 **[!UICONTROL Google BigQuery]**&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

>[!TIP]
>
>지정된 소스에 아직 인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL 설정]** 옵션이 표시됩니다. 인증된 계정이 있으면 이 옵션이 **[!UICONTROL 데이터 추가]**(으)로 변경됩니다.

![Google BigQuery가 있는 소스 카탈로그를 선택했습니다.](../../../../images/tutorials/create/google-big-query/catalog.png)

**[!UICONTROL Google Big Query에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정에 연결하려면 연결할 [!DNL Google BigQuery] 계정을 선택한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![기존 계정 목록이 표시되는 기존 계정 페이지입니다.](../../../../images/tutorials/create/google-big-query/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 새 [!DNL Google BigQuery] 계정에 대한 이름과 선택적 설명을 입력하십시오.

![원본 워크플로의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/google-big-query/new.png)

>[!BEGINTABS]

>[!TAB 기본 인증 사용]

기본 인증을 사용하려면 **[!UICONTROL 기본 인증]**&#x200B;을 선택하고 [프로젝트, 클라이언트 ID, 클라이언트 암호, 새로 고침 토큰 및 (선택 사항) 대용량 결과 데이터 세트 ID](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)에 대한 값을 제공하십시오. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하고 연결을 설정할 수 있도록 잠시 기다립니다.

![기본 인증을 선택하는 새 계정 인터페이스입니다.](../../../../images/tutorials/create/google-big-query/basic_auth.png)

>[!TAB 서비스 인증 사용]

서비스 인증을 사용하려면 **[!UICONTROL 서비스 인증]**&#x200B;을 선택하고 [프로젝트 ID, 키 파일 콘텐츠 및 (선택 사항) 대용량 결과 데이터 세트 ID](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)에 대한 값을 제공하십시오. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하고 연결을 설정할 수 있도록 잠시 기다립니다.

![서비스 인증을 선택하는 새 계정 인터페이스입니다.](../../../../images/tutorials/create/google-big-query/service_auth.png)

>[!ENDTABS]

### 샘플 데이터의 미리 보기 건너뛰기 {#skip-preview-of-sample-data}

데이터 선택 단계에서 큰 테이블 또는 데이터 파일을 수집할 때 시간 초과가 발생할 수 있습니다. 샘플 데이터가 없어도 데이터 미리 보기를 건너뛰어 시간 초과를 우회하고 스키마를 볼 수 있습니다. 데이터 미리 보기를 건너뛰려면 **[!UICONTROL 샘플 데이터 미리 보기 건너뛰기]** 전환을 사용하도록 설정하십시오.

워크플로우의 나머지 부분은 그대로 유지됩니다. 유일한 주의 사항은 데이터 미리보기를 건너뛰면 매핑 단계에서 계산된 필드 및 필수 필드의 자동 유효성 검사를 방지할 수 있으므로 매핑 중에 이러한 필드의 유효성을 수동으로 검사해야 한다는 것입니다.

## 다음 단계

이 자습서에 따라 [!DNL Google BigQuery] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 플랫폼으로 가져오도록 데이터 흐름을 구성](../../dataflow/databases.md)할 수 있습니다.
