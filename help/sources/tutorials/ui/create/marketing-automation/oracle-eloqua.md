---
title: Platform UI를 사용하여 Oracle Eloqua 소스 연결 만들기
description: Platform UI를 사용하여 Adobe Experience Platform을 Oracle Eloqua에 연결하는 방법을 알아봅니다.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# 플랫폼 UI를 사용하여 [!DNL Oracle Eloqua] 소스 연결 만들기

>[!WARNING]
>
>[!DNL Oracle Eloqua] 원본은 2025년 5월 말에 사용되지 않습니다.

이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 [!DNL Oracle Eloqua] 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 안내서를 사용하려면 다음 Platform 구성 요소에 대한 작업 이해가 필요합니다.

* [소스](../../../../home.md): Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): 플랫폼은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

플랫폼에서 인증된 [!DNL Oracle Eloqua] 계정이 이미 있는 경우 이 문서의 나머지 부분을 건너뛰고 [마케팅 자동화 데이터를 플랫폼으로 가져오기 위한 데이터 흐름 만들기](../../dataflow/marketing-automation.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL Oracle Eloqua]을(를) 플랫폼에 연결하려면 다음 인증 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 엔드포인트 | [!DNL Oracle Eloqua] 서버의 끝점입니다. [!DNL Oracle Eloqua]은(는) 여러 데이터 센터를 지원합니다. 끝점을 찾으려면 자격 증명으로 [[!DNL Oracle Eloqua] 인터페이스](https://login.eloqua.com)에 로그인한 다음 리디렉션 URL에서 기본 URL 부분을 복사합니다. URL 패턴의 형식은 `xxx.xx.eloqua.com`이며 `http` 또는 `https` 없이 입력해야 합니다. |
| 사용자 이름 | [!DNL Oracle Eloqua] 서버의 사용자 이름입니다. 사용자 이름은 `siteName + \\ + username` 형식이어야 합니다. 여기서 `siteName`은(는) [!DNL Oracle Eloqua]에 로그인할 때 사용한 회사 이름이고 `username`은(는) 사용자 이름입니다. 예를 들어 로그인 사용자 이름은 `Eloqua\Andy`일 수 있습니다. **참고**: 사용자 이름을 입력할 때 Experience Platform UI에서 추가 백슬래시(`\`)를 자동으로 추가하므로 UI를 사용할 때는 단일 백슬래시(`\`)를 사용해야 합니다. |
| 암호 | [!DNL Oracle Eloqua] 사용자 이름에 해당하는 암호입니다. |

[!DNL Oracle Eloqua]의 인증 자격 증명에 대한 자세한 내용은 [[!DNL Oracle Eloqua] 인증 가이드](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html)를 참조하십시오.

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL Oracle Eloqua] 계정을 플랫폼에 연결할 수 있습니다.

## [!DNL Oracle Eloqua] 계정 연결

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 마케팅 자동화] 범주에서 **[!UICONTROL Oracle Eloqua]**&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

**[!UICONTROL Oracle Eloqua 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 [!DNL Oracle Eloqua] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속합니다.

![기존](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 이름, 선택적 설명 및 [!DNL Oracle Eloqua] 자격 증명에 대한 적절한 값을 제공합니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![새로 만들기](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 다음 단계

이 자습서에 따라 [!DNL Oracle Eloqua] 계정과 플랫폼 간의 소스 연결을 인증하고 만들었습니다. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 만들어 플랫폼 자동화 데이터를 가져올 수 있습니다](../../dataflow/marketing-automation.md).
