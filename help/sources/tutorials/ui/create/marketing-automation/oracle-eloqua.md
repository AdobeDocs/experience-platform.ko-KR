---
title: Platform UI를 사용하여 Oracle Eloqua 소스 연결 만들기
description: Platform UI를 사용하여 Adobe Experience Platform을 Oracle Eloqua에 연결하는 방법을 알아봅니다.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# 만들기 [!DNL Oracle Eloqua] 플랫폼 UI를 사용한 소스 연결

이 튜토리얼에서는 [!DNL Oracle Eloqua] Adobe Experience Platform 사용자 인터페이스를 사용한 소스 연결.

## 시작하기

이 안내서를 사용하려면 다음 Platform 구성 요소에 대한 작업 이해가 필요합니다.

* [소스](../../../../home.md): Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

이미 인증된 사용자가 있는 경우 [!DNL Oracle Eloqua] 플랫폼에서 작업하는 경우 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [마케팅 자동화 데이터를 Platform으로 가져오기 위한 데이터 흐름 만들기](../../dataflow/marketing-automation.md).

### 필요한 자격 증명 수집

연결하려면 [!DNL Oracle Eloqua] 플랫폼에 다음 인증 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 엔드포인트 | 의 엔드포인트 [!DNL Oracle Eloqua] 서버입니다. [!DNL Oracle Eloqua] 는 여러 데이터 센터를 지원합니다. 엔드포인트를 찾으려면 [[!DNL Oracle Eloqua] 인터페이스](https://login.eloqua.com) 자격 증명을 사용한 다음 리디렉션 URL에서 기본 URL 부분을 복사합니다. URL 패턴의 형식은 다음과 같습니다. `xxx.xx.eloqua.com` 및 를 입력하지 않고 입력해야 합니다. `http` 또는 `https`. |
| 사용자 이름 | 의 사용자 이름 [!DNL Oracle Eloqua] 서버입니다. 사용자 이름은 다음 형식으로 지정해야 합니다. `siteName + \\ + username`, 여기서 `siteName` 은(는) 로그인할 때 사용한 회사 이름입니다 [!DNL Oracle Eloqua] 및 `username` 은 사용자 이름입니다. 예를 들어 로그인 사용자 이름은 다음과 같을 수 있습니다. `Eloqua\Andy`. **참고**: 단일 백슬래시()를 사용해야 합니다`\`를 사용하십시오. Experience Platform UI에서 추가 백슬래시( )를 자동으로 추가하기 때문입니다`\`)을 클릭하여 사용자 이름을 입력합니다. |
| 암호 | 다음에 해당하는 암호 [!DNL Oracle Eloqua] 사용자 이름. |

의 인증 자격 증명에 대한 자세한 정보 [!DNL Oracle Eloqua], 다음을 참조하십시오. [[!DNL Oracle Eloqua] 인증 안내서](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

필요한 자격 증명을 수집했으면 아래 단계에 따라 를 연결할 수 있습니다. [!DNL Oracle Eloqua] 계정을 플랫폼에 추가합니다.

## 연결 [!DNL Oracle Eloqua] account

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL 마케팅 자동화] 범주, 선택 **[!UICONTROL Oracle Eloqua]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

다음 **[!UICONTROL oracle Eloqua 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL Oracle Eloqua] 새 데이터 흐름을 만들 계정 을 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![기존](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### 새 계정

새 계정을 만드는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**&#x200B;을 누르고 이름, 설명(선택 사항) 및 의 적절한 값을 제공합니다. [!DNL Oracle Eloqua] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![신규](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 다음 단계

이 자습서에 따라 간의 소스 연결을 인증하고 만들었습니다. [!DNL Oracle Eloqua] 계정과 플랫폼. 이제 다음 튜토리얼을 계속 진행하여 [데이터 흐름을 만들어 Platform으로 마케팅 자동화 데이터 가져오기](../../dataflow/marketing-automation.md).
