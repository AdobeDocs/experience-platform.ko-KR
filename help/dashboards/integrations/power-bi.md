---
title: Platform 대시보드용 Power BI 보고서 템플릿
description: 보고서 템플릿을 사용함으로써 Power BI를 사용하여 Experience Platform 데이터를 탐색합니다.
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: 729d218f72a8caecc90a98810b973d0754f7757b
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 92%

---

# 대시보드용 Power BI 보고서 템플릿

Power BI 보고서 템플릿 기능을 사용하면 Adobe Experience Platform의 데이터로 채워진 강력한 보고서를 작성할 수 있습니다. 간소화된 설치 프로세스는 실시간 고객 프로필, 세분화 및 대상에 대한 표준 위젯을 자동으로 설치합니다. 이러한 설치를 통해 Power BI가 데이터 모델에 연결되므로 보고서 템플릿을 손쉽게 맞춤화하고 확장할 수도 있습니다. 이러한 보고서는 수신자가 Platform에서 조직에 대한 자격 증명을 필요로 하지 않아도 조직 전체에 공유할 수 있습니다.

이 문서에서는 Adobe Experience Platform을 Power BI 애플리케이션과 연결하고 보고서 템플릿을 사용하여 주요 Platform 데이터 인사이트를 외부 사용자와 공유하는 방법에 대한 지침을 제공합니다.

## 시작하기

이 자습서를 계속하기 전에 다음을 잘 이해하는 것이 좋습니다. [스키마 구성](../../xdm/schema/composition.md) Experience Platform 및 을 통해 실시간 고객 프로필에 특성이 포함되는 방법 [유니온 스키마](../../xdm/schema/composition.md#union).

Power BI 애플리케이션 통합을 설치하려면 먼저 사용자가 다음과 같은 Platform 권한을 획득해야 합니다.

- 쿼리 관리
- 샌드박스 관리

이러한 권한을 할당하는 방법에 대해 알아보려면 [액세스 제어](../../access-control/home.md) 설명서를 참조하십시오.

또한 이 튜토리얼을 수행하려면 Power BI 계정이 있어야 합니다. 계정을 만들려면 [Power BI 홈 페이지](https://powerbi.microsoft.com/ko-kr/)로 이동하여 등록 프로세스를 따르십시오. 이 Power BI 계정의 사용자는 Power BI 설정 내에서 **작업 영역 만들기** 설정도 활성화해야 합니다. 이 설정은 Power BI 관리 포털의 테넌트 설정에서 찾을 수 있습니다. 테넌트 또는 고용주가 계정을 제공하는 경우 해당 관리자에게 문의하여 이 설정을 활성화하십시오.

![Power BI 관리 포털에서 작업 영역 설정을 만듭니다.](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>Platform UI의 왼쪽 탐색 영역에 대시보드 탭이 표시되고 대시보드 인벤토리 보기가 표시되도록 하려면 Platform 라이선스의 일부로 프로필, 세그먼트 또는 대상 대시보드 중 하나에 대한 액세스 권한이 있어야 합니다.

## Power BI 애플리케이션 통합 설치

Platform UI 내의 왼쪽 탐색 영역에서 **[!UICONTROL 대시보드]**&#x200B;를 선택하여 [!UICONTROL 대시보드] 작업 영역을 엽니다. [!UICONTROL 찾아보기] 탭에는 현재 사용 가능한 대시보드 보기 목록이 표시됩니다. 사용 가능한 대시보드를 확인하는 방법에 대한 자세한 내용은 [인벤토리 설명서](../inventory.md)를 참조하십시오.

그런 다음 **[!UICONTROL 통합]** 탭을 선택합니다. Power BI 애플리케이션 통합 페이지가 표시됩니다. 여기에서 **[!UICONTROL 설치]**&#x200B;를 선택하여 설치를 시작합니다.

>[!NOTE]
>
>[!UICONTROL 설치] 버튼은 쿼리 서비스 관리 및 샌드박스 관리 권한이 모두 있어야 사용할 수 있습니다.

![[설치] 버튼이 강조 표시된 Power BI 세부 정보 화면입니다.](../images/power-bi/details-screen.png)

### 자격 증명 제공

설치 프로세스의 첫 번째 단계는 Power BI 애플리케이션 통합에 만료되지 않는 자격 증명을 제공하는 것입니다. 이를 제공하는 데 사용할 수 있는 두 가지 옵션은 [[!UICONTROL 새 자격 증명을 만들거나]](#create-new-credentials) [[!UICONTROL 기존 자격 증명을 사용]](#use-existing-credentials)하는 것입니다. 적절한 토글을 선택하여 계속합니다.

#### 새 자격 증명 만들기 {#create-new-credentials}

새 자격 증명을 생성할 때 필요한 필드에는 [!UICONTROL 이름]과 [!UICONTROL 할당 대상]이 있습니다. [!UICONTROL 할당 대상] 필드는 Power BI 계정과 연결된 이메일 주소와 관련이 있습니다.

![Power BI가 새 자격 증명 화면을 생성합니다.](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>만료되지 않는 자격 증명을 만들려면 특정 권한과 역할이 할당되어야 합니다. 필요한 권한은 샌드박스 관리 및 쿼리 서비스 통합 관리 권한입니다. 필요한 역할은 Adobe Experience Platform 관리자 및 개발자 역할입니다. 이러한 권한을 할당하는 방법에 대해 알아보려면 [액세스 제어](../../access-control/home.md) 설명서를 참조하십시오.

만료되지 않는 쿼리 서비스 자격 증명을 생성하는 방법에 대한 자세한 내용은 [만료되지 않는 자격 증명 안내서](../../query-service/ui/credentials.md#non-expiring-credentials)를 참조하십시오.

만료되지 않는 자격 증명을 처음으로 생성한 다음에는 JSON 파일이 해당 컴퓨터에 다운로드됩니다. 그런 다음 이 JSON 파일을 다른 사용자와 자격 증명으로 공유하여 설치 프로세스를 완료할 수 있습니다.

#### 기존 자격 증명 사용 {#use-existing-credentials}

JSON 자격 증명 파일을 업로드하여 유효성 검사를 통과할 수도 있습니다. 만료되지 않는 자격 증명 값을 포함하는 이러한 JSON 파일은 만료되지 않는 자격 증명이 생성될 때 사용 중인 로컬 컴퓨터에 다운로드됩니다.

>[!IMPORTANT]
>
>만료되지 않는 기존 자격 증명을 사용하려면 사용자에게 자격 증명이 이미 할당되어 있어야 합니다. 사용자에게 할당된 자격 증명이 없고 Adobe Admin Console을 사용하여 새 자격 증명을 만들 수 없는 경우 사용자는 설치 프로세스를 진행할 수 없습니다.

**[!UICONTROL 자격 증명 파일 업로드]**&#x200B;를 선택한 다음 표시되는 대화 상자에서 업로드할 적절한 JSON 파일을 선택합니다.

![[자격 증명 파일 업로드] 버튼이 강조 표시된 Power BI 자격 증명 화면입니다.](../images/power-bi/upload-credential-file.png)

만료되지 않는 자격 증명을 제공하면 Platform에서 자동으로 유효성을 검사합니다. 유효성 검사가 성공하면 확인 메시지가 표시됩니다. **[!UICONTROL 다음]**&#x200B;을 선택하여 Power BI 애플리케이션에 대한 동의 계약을 검토합니다.

![[다음] 버튼이 강조 표시된 만료되지 않는 자격 증명 유효성 검사 성공 화면입니다.](../images/power-bi/successfully-uploaded-credential-file.png)

### 동의 제공

동의 화면이 나타납니다. **[!UICONTROL 동의 검토]**&#x200B;를 선택하여 Power BI가 서비스 약관 및 개인정보 처리방침에 따라 데이터에 액세스하고 사용하는 데 필요한 권한이 자세히 설명되어 있는 새 창을 엽니다.

![[동의 검토] 버튼이 강조 표시된 동의 제공 화면입니다.](../images/power-bi/provide-consent-display.png)

**[!UICONTROL 동의]**&#x200B;를 선택하여 Power BI에 Platform 데이터에 액세스하고 사용할 수 있는 권한을 부여합니다.

![Power BI 애플리케이션에 대한 권한 요청입니다.](../images/power-bi/permissions.png)

>[!NOTE]
>
>동의를 제공하기 전에 언제든지 설치 프로세스를 종료하면 Power BI 애플리케이션 통합이 대시보드 인벤토리에 설치되지 않습니다.

동의를 제공하면 보고서 템플릿이 설치 프로세스의 일부로 Power BI 환경에 자동으로 설치됩니다. 그런 다음 Power BI는 만료되지 않는 자격 증명을 사용하여 Platform에 액세스하고, 모든 SQL 쿼리를 순차적으로 실행하고, 보고서 템플릿을 반환된 데이터로 채웁니다.

**[!UICONTROL 완료]**&#x200B;를 선택하여 대시보드 인벤토리로 돌아갑니다.

![[완료] 버튼이 강조 표시된 동의 제공 화면입니다.](../images/power-bi/finish-consent-review.png)

Power BI 보고서 템플릿이 설치되었으므로 [!UICONTROL 찾아보기] 탭 아래의 사용 가능한 대시보드 목록에 표시됩니다. 목록에서 **[!UICONTROL Power BI]**&#x200B;를 선택하여 Power BI 환경으로 이동합니다.

![대시보드 인벤토리에 나열된 Power BI입니다.](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Power BI 관리자는 사용자에게 Power BI 환경에서 이러한 대시보드를 볼 수 있는 적절한 액세스 권한이 있는지 확인해야 합니다.

## Power BI 작업 영역

[Power BI 작업 영역](https://dxt.powerbi.com)에 로그인하면 액세스 권한이 있는 각 서비스에 보고서 템플릿을 사용할 수 있습니다. 보고서 템플릿에는 프로필, 세그먼트 및 대상 대시보드가 해당 보기 권한이 있는 경우&#x200B;**에만** 포함됩니다.

프로필, 세그먼트 및 대상의 표준 위젯은 기본적으로 Power BI 템플릿 보고서 내에서 사용할 수 있습니다.

>[!NOTE]
>
>지정된 대시보드에 대해 편집 권한을 활성화해야 해당 대시보드를 Power BI 환경에 설치할 수 있습니다.

![표준 Platform 프로필 위젯을 사용하는 Power BI 프로필 템플릿 보고서입니다.](../images/power-bi/profile-report-template.png)

Power BI에 대시보드를 설치하면 기본적으로 모든 사용자에게 보고서 템플릿이 표시됩니다. 보고서 템플릿에 대한 액세스를 제한하려면 Power BI 환경 내에서 해당 사용자에 대한 액세스를 비활성화해야 합니다.

## Power BI 보고서 템플릿 맞춤화

사용자 정의 위젯을 사용하여 데이터 모델에 사용자 정의 특성을 추가하고 Power BI에서 제공하는 보고서 템플릿을 보완할 수 있습니다.

>[!NOTE]
>
>사용자 정의 위젯에 사용할 수 있는 속성은 공용 구조체 스키마에서 사용할 수 있는 항목에 따라 다릅니다. 공용 구조체 스키마를 보고 탐색하여 사용자 정의 위젯의 이점을 활용하는 방법을 알아보려면 [공용 구조체 스키마 UI 안내서](../../profile/ui/union-schema.md)를 참조하십시오.

### 사용자 정의 위젯 만들기

사용자 정의 위젯은 위젯 라이브러리를 통해 생성됩니다. 기능에 대한 소개는 [위젯 라이브러리 개요](../customize/widget-library.md)를, 특정 지침은 [사용자 정의 위젯 만들기 튜토리얼](../customize/custom-widgets.md)을 참조하십시오.

>[!IMPORTANT]
>
>새로 생성된 사용자 정의 위젯은 Adobe Experience Platform 대시보드와 Power BI 보고서 템플릿 간에 자동으로 동기화되지 **않습니다**. Platform UI에서 생성된 모든 사용자 정의 위젯은 Power BI 환경 내에서 수동으로 다시 만들어야 합니다.

### Power BI 환경에서 사용자 정의 위젯 다시 만들기

대시보드에 사용자 정의 위젯 내에 적절한 지표 및 특성이 포함되어 있다면 Power BI 환경 내에서 표시되는 보고서 템플릿을 수정할 준비가 된 것입니다. 사용자 인터페이스를 통해 보고서를 편집하는 방법에 대한 자세한 내용은 [Power BI 설명서](https://docs.microsoft.com/ko-kr/power-bi/)를 참조하십시오.

## Power BI 애플리케이션 통합 삭제

대시보드를 삭제하려면 대시보드 인벤토리로 이동한 다음 대시보드 이름 옆에 있는 삭제 아이콘(![](../images/power-bi/delete-icon.png))을 선택합니다.

>[!NOTE]
>
>Power BI 대시보드를 설치한 사용자만 Platform UI에서 통합 기능을 삭제할 수 있습니다.

![[찾아보기] 버튼과 [삭제] 아이콘이 강조 표시된 대시보드 인벤토리 화면 찾아보기 탭입니다.](../images/power-bi/delete-power-bi-dashboard.png)

확인 팝오버가 표시됩니다. **[!UICONTROL 삭제]**&#x200B;를 선택하여 프로세스를 확인합니다.

>[!IMPORTANT]
>
>Platform UI에서 Power BI 대시보드를 삭제해도 Power BI 환경에서 사용할 수 있는 보고서 템플릿은 삭제되지 **않습니다**. Power BI 보고서 템플릿에 보관된 정보를 완전히 삭제하려면 Power BI 계정에 로그인한 다음 해당 환경에서 보고서 템플릿을 삭제해야 합니다. 삭제한 다음에도 위에서 설명한 것과 동일한 설치 지침에 따라 Power BI 대시보드를 다시 설치할 수 있습니다.

## 다음 단계

이 문서를 읽으면 Power BI 보고서 템플릿을 Platform에 통합하여 프로필, 세그먼트 또는 대상 대시보드에서 강력한 데이터 인사이트를 공유하는 방법을 더 잘 이해할 수 있습니다. [대시보드 맞춤화 개요](../customize/overview.md)를 참조하여 대시보드 맞춤화에 대해 자세히 알아보십시오.
