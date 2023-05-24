---
keywords: Experience Platform;홈;인기 항목;Oracle 서비스 클라우드;oracle 서비스 클라우드
title: UI에서 Oracle 서비스 클라우드 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Oracle 서비스 클라우드 소스 연결을 만드는 방법을 알아봅니다.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# UI에서 Oracle 서비스 클라우드 소스 연결 만들기

이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 Oracle 서비스 클라우드 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 Oracle 서비스 클라우드 소스 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/customer-success.md)

### 필요한 자격 증명 수집

의 Oracle 서비스 클라우드 계정에 액세스하려면 [!DNL Platform], 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| Host | oracle 서비스 클라우드 인스턴스의 호스트 URL. |
| 사용자 이름 | oracle 서비스 클라우드 사용자 계정의 사용자 이름입니다. |
| 암호 | oracle 서비스 클라우드 계정의 암호입니다. |

oracle 서비스 클라우드 계정 인증에 대한 자세한 내용은 [[!DNL Oracle] 인증 안내서](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## oracle 서비스 클라우드 계정 연결

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만드는 데 사용할 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 창을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL 고객 성공] 범주, 선택 **[!UICONTROL Oracle 서비스 클라우드]** 다음을 선택합니다. **[!UICONTROL 데이터 추가]**.

![oracle 서비스 클라우드 소스가 강조 표시된 소스 카탈로그.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

다음 **[!UICONTROL oracle 서비스 클라우드에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 연결하려는 Oracle 서비스 클라우드 계정을 선택한 다음 을 선택합니다 **[!UICONTROL 다음]** 계속합니다.

![기존 계정 인터페이스.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 Oracle 서비스 클라우드 자격 증명을 제공합니다. 완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![의 자리 표시자 값이 있는 새 계정 인터페이스.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## 다음 단계

이 자습서에 따라 Oracle 서비스 클라우드 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하여 [고객 성공 데이터를 Platform으로 가져오기 위한 데이터 흐름 구성](../../dataflow/crm.md).
