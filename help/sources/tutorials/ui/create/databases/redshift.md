---
title: Ui를 사용하여 AWS Redshift를 Experience Platform에 연결
description: 소스 UI를 사용하여 AWS Redshift 계정을 Experience Platform에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: dd9aee1ac887637d4761188d6dbcf55ad5bde407
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---

# UI를 사용하여 [!DNL AWS Redshift]을(를) Experience Platform에 연결

>[!IMPORTANT]
>
>[!DNL AWS Redshift] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

사용자 인터페이스를 사용하여 [!DNL AWS Redshift] 계정을 Adobe Experience Platform에 연결하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 올바른 [!DNL AWS Redshift] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/databases.md)에 대한 자습서로 진행할 수 있습니다.

## 소스 카탈로그 탐색

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

*[!UICONTROL 데이터베이스]* 범주에서 **[!DNL AWS Redshift]**&#x200B;을(를) 선택한 다음 **[!UICONTROL 설정]**&#x200B;을(를) 선택합니다.

>[!TIP]
>
>지정된 소스에 아직 인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL 설정]** 옵션이 표시됩니다. 인증된 계정이 있으면 이 옵션이 **[!UICONTROL 데이터 추가]**(으)로 변경됩니다.

![AWS Redshift 원본 카드가 선택된 원본 카탈로그입니다.](../../../../images/tutorials/create/redshift/catalog.png)

## 기존 계정 사용 {#existing}

그런 다음 소스 워크플로우의 인증 단계로 이동합니다. 여기에서 기존 계정을 사용하거나 새 계정을 만들 수 있습니다.

기존 계정을 사용하려면 계정 디렉터리에서 [!DNL AWS Redshift] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![기존 계정이 나열된 원본 워크플로의 계정 디렉터리입니다.](../../../../images/tutorials/create/redshift/existing.png)

## 새 계정 만들기 {#create}

기존 계정이 없는 경우 소스와 일치하는 필요한 인증 자격 증명을 제공하여 새 계정을 만들어야 합니다.

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;을 선택한 다음 이름을 입력하고 필요에 따라 계정에 대한 설명을 추가하십시오.

### Azure에서 Experience Platform에 연결 {#azure}

[!DNL AWS Redshift] 계정을 Azure의 Experience Platform에 연결하려면 입력 양식에서 인증 자격 증명을 제공한 다음 **([!UICONTROL 소스에 연결])**&#x200B;을(를) 선택하십시오.

![Azure에서 AWS Redshift를 Experience Platform에 연결하는 새 계정 인터페이스입니다.](../../../../images/tutorials/create/redshift/new.png)

| 자격 증명 | 설명 |
| --- | --- |
| 서버 | [!DNL AWS Redshift] 인스턴스의 서버 이름입니다. |
| 포트 | [!DNL AWS Redshift] 서버가 클라이언트 연결을 수신 대기하는 데 사용하는 TCP 포트입니다. |
| 사용자 이름 | 액세스 권한을 부여할 계정의 사용자 이름입니다. |
| 암호 | 사용자 계정에 해당하는 암호입니다. |
| 데이터베이스 | 데이터를 가져올 [!DNL AWS Redshift] 데이터베이스입니다. |

시작에 대한 자세한 내용은 [이 [!DNL AWS Redshift] 문서](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html)를 참조하세요.

### AWS에서 Experience Platform에 연결 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 AWS 웹 서비스(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../../../landing/multi-cloud.md)를 참조하세요.

새 [!DNL AWS Redshift] 계정을 만들고 AWS의 Experience Platform에 연결하려면 VA6 샌드박스에 있는지 확인하고 인증에 필요한 자격 증명을 제공한 다음 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하십시오.

![AWS Redshift를 AWS의 Experience Platform에 연결하는 새 계정 인터페이스입니다.](../../../../images/tutorials/create/redshift/aws-auth.png)

| 자격 증명 | 설명 |
| --- | --- |
| 서버 | [!DNL AWS Redshift] 인스턴스의 서버 이름입니다. |
| 포트 | [!DNL AWS Redshift] 서버가 클라이언트 연결을 수신 대기하는 데 사용하는 TCP 포트입니다. |
| 사용자 이름 | 액세스 권한을 부여할 계정의 사용자 이름입니다. |
| 암호 | 사용자 계정에 해당하는 암호입니다. |
| 데이터베이스 | 데이터를 가져올 [!DNL AWS Redshift] 데이터베이스입니다. |
| 스키마 | [!DNL AWS Redshift] 데이터베이스와 연결된 스키마의 이름입니다. 데이터베이스 액세스 권한을 부여할 사용자도 이 스키마에 액세스할 수 있는지 확인해야 합니다. |

시작에 대한 자세한 내용은 [이 [!DNL AWS Redshift] 문서](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html)를 참조하세요.

## 다음 단계

이 자습서에 따라 [!DNL AWS Redshift] 데이터베이스와 Experience Platform 간에 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 만들어 데이터베이스에서 Experience Platform으로 데이터를 수집할 수 있습니다](../../dataflow/databases.md).