---
title: 고객 관리 키에 대한 AWS KMS 구성
description: Adobe Experience Platform의 고객 관리 키와 함께 사용할 Amazon Web Services KMS(키 관리 서비스)를 구성하는 방법을 알아봅니다.
exl-id: 0cf0deab-dc30-412f-b511-dee5504c3953
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 0%

---

# 고객 관리 키에 대한 AWS KMS 구성

>[!AVAILABILITY]
>
>이 문서는 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/landing/multi-cloud)를 참조하세요.
>
>AWS의 [고객 관리 키](../overview.md)(CMK)는 Privacy 및 Security Shield에서 지원되지만 Healthcare Shield에서는 사용할 수 없습니다. Azure의 CMK는 Healthcare Shield뿐만 아니라 Privacy 및 Security Shield 모두에서 지원됩니다.

이 안내서를 사용하여 Adobe Experience Platform에 대한 암호화 키를 생성, 관리 및 제어하여 Amazon Web Services(AWS) KMS(키 관리 서비스)로 데이터를 보호합니다. 이러한 통합을 통해 규정 준수를 간소화하고 자동화를 통해 운영을 간소화하며 자체 주요 관리 인프라를 유지 관리할 필요가 없어집니다.

Customer Journey Analytics 관련 지침은 [Customer Journey Analytics CMK 설명서](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-privacy/cmk)를 참조하세요.

>[!IMPORTANT]
>
>Adobe Experience Platform은 시스템 관리 키를 사용하여 기본적으로 사용하지 않는 데이터를 암호화합니다. CMK(Customer Managed Keys)를 활성화하면 데이터 보안을 완전히 제어할 수 있습니다. 그러나 CMK가 활성화되면 이 변경 사항은 되돌릴 수 없습니다. 시스템 관리 키로 되돌릴 수 없습니다. 데이터에 중단 없이 액세스하고 잠재적인 액세스 가능성을 방지하기 위해 키를 안전하게 관리할 책임이 있습니다.

AWS KMS를 사용하여 Adobe Experience Platform의 통합 암호화 키 관리를 통해 데이터 보안을 강화합니다. 이 안내서에 따라 암호화 키를 만들고 관리하여 데이터를 안전하게 보호할 수 있습니다.

## 전제 조건 {#prerequisites}

이 문서를 계속하기 전에 다음 주요 개념 및 기능을 잘 이해해야 합니다.

- **AWS KMS(키 관리 서비스)**: 암호화 키를 만들고, 관리하고, 회전하는 방법을 포함하여 AWS KMS의 기본 사항을 이해합니다. 자세한 내용은 [공식 KMS 설명서](https://docs.aws.amazon.com/kms/)를 참조하세요.
- **AWS의 IAM(Identity and Access Management) 정책**: IAM은 AWS 서비스 및 리소스에 대한 액세스를 안전하게 관리할 수 있는 서비스입니다. IAM을 사용하여 다음과 같은 작업을 수행할 수 있습니다.
   - 특정 리소스에 액세스할 수 있는 사용자, 그룹 및 역할을 정의합니다.
   - 사용자가 수행할 수 있는 작업 또는 수행할 수 없는 작업을 지정합니다.
   - IAM 정책을 사용하여 권한을 할당하여 세분화된 액세스 제어를 구현합니다.
자세한 내용은 [AWS KMS용 IAM 정책 공식 설명서](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html)를 참조하십시오.
- **Experience Platform의 데이터 보안**: Experience Platform에서 데이터 보안을 유지하고 암호화를 위해 AWS KMS와 같은 외부 서비스와 통합하는 방법을 살펴보십시오. Experience Platform은 전송, 사용 중인 클라우드 공급자 암호화, 격리된 저장소, 사용자 지정 가능한 인증 및 암호화 옵션에 대해 HTTPS TLS v1.2를 사용하여 데이터를 보호합니다. 데이터를 안전하게 유지하는 방법에 대한 자세한 내용은 [거버넌스, 개인 정보 및 보안 개요](../overview.md) 또는 [Experience Platform의 데이터 암호화](../../encryption.md)에 대한 문서를 참조하십시오.
- **AWS 관리 콘솔**: 하나의 웹 기반 응용 프로그램에서 모든 AWS 서비스에 액세스하고 관리할 수 있는 중앙 허브입니다. 검색 창을 사용하여 도구를 빠르게 찾고, 알림을 확인하고, 계정 및 결제를 관리하고, 설정을 사용자 지정할 수 있습니다. 자세한 내용은 [공식 AWS 관리 콘솔 설명서](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html)를 참조하십시오.

## 시작하기 {#get-started}

이 안내서를 사용하려면 이미 Amazon Web Services 계정에 액세스하고 관리 콘솔에 액세스할 수 있어야 합니다. 시작하려면 아래 단계를 따르십시오.

### 지원되는 영역 선택 {#select-supported-region}

AWS KMS는 특정 지역에서 사용할 수 있습니다. KMS가 지원되는 지역에서 작동하고 있는지 확인하십시오. [AWS KMS 끝점 및 할당량 목록](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)에서 지원되는 영역의 전체 목록을 볼 수 있습니다.

AWS KMS 암호화 키가 Adobe Experience Platform 인스턴스와 동일한 리전에 있는지 확인하여 데이터 상주 요구 사항을 준수하고 성능을 최적화하며 추가 지역 간 비용을 방지합니다. 영역이 잘못 정렬되면 데이터에 액세스할 수 없고 통합에 실패할 수 있습니다.

### 권한 확인 {#verify-permissions}

KMS 내에서 암호화 키를 만들고, 관리하고, 사용하는 데 필요한 AWS ID 및 액세스 관리(IAM) 권한이 있는지 확인하십시오. 사용 권한을 확인하려면:

1. [IAM 정책 시뮬레이터](https://policysim.aws.amazon.com/)에 액세스합니다.
2. 사용자 계정 또는 역할을 선택합니다.
3. `kms:CreateKey` 또는 `kms:Encrypt`과(와) 같은 KMS 작업을 시뮬레이트합니다.

시뮬레이션에서 오류가 반환되거나 사용 권한에 대해 잘 모르는 경우 AWS 관리자에게 지원을 요청하십시오.

### AWS 계정 구성 확인

AWS 계정이 AWS KMS 서비스를 사용하도록 설정되어 있는지 확인합니다. 대부분의 계정에 기본적으로 KMS 액세스가 활성화되어 있지만 [AWS 관리 콘솔](https://aws.amazon.com/console/)을 방문하여 계정 설정을 검토할 수 있습니다. 자세한 내용은 [AWS 키 관리 서비스 개발자 안내서](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)를 참조하십시오.

### AWS KMS로 이동하여 키 설정 시작

암호화 키 설정 및 관리를 시작하려면 AWS 계정에 로그인하고 AWS KMS(키 관리 서비스)로 이동합니다. AWS 관리 콘솔에서 서비스 메뉴에서 **KMS(키 관리 서비스)**&#x200B;을(를) 선택합니다.

![키 관리 서비스가 강조 표시된 AWS 관리 콘솔의 검색 드롭다운 메뉴.](../../../images/governance-privacy-security/key-management-service/navigate-to-kms.png)

## 새 키 만들기 {#create-a-key}

>[!IMPORTANT]
>
>암호화 키의 안전한 저장, 액세스 및 가용성을 보장합니다. 키를 관리하고 Experience Platform 작업 중단을 방지할 책임이 있습니다.

[!DNL Key Management Service (KMS)] 작업 영역에서 **[!DNL Create a key]**&#x200B;을(를) 선택합니다.

![키 만들기가 강조 표시된 키 관리 서비스 작업 영역입니다.](../../../images/governance-privacy-security/key-management-service/create-a-key.png)

## 키 설정 구성 {#configure-key}

[!DNL Configure Key] 워크플로가 나타납니다. 기본적으로 키 유형은 **[!DNL Symmetric]**(으)로 설정되고 키 사용은 **[!DNL Encrypt and Decrypt]**(으)로 설정됩니다. 계속 진행하기 전에 이러한 옵션이 선택되어 있는지 확인하십시오.

![대칭 및 암호화 및 암호 해독 기본 옵션이 강조 표시된 키 구성 워크플로의 첫 단계입니다.](../../../images/governance-privacy-security/key-management-service/configure-key-basic-options.png)

**[!DNL Advanced options]** 드롭다운 메뉴를 확장합니다. AWS에서 주요 자료를 만들고 관리할 수 있는 **[!DNL KMS]** 옵션을 사용하는 것이 좋습니다. 기본적으로 **[!DNL KMS]** 옵션이 선택되어 있습니다.

>[!NOTE]
>
>기존 키가 이미 있는 경우 외부 키 자료를 가져오거나 AWS [!DNL CloudHSM] 키 저장소를 사용할 수 있습니다. 이 문서의 범위에서는 이러한 옵션에 대해 다루지 않습니다.

그런 다음 키의 영역 범위를 지정하는 [!DNL Regionality] 설정을 선택합니다. **[!DNL Single-Region key]**&#x200B;을(를) 선택한 후 **[!DNL Next]**&#x200B;을(를) 선택하여 2단계로 진행합니다.

>[!IMPORTANT]
>
>AWS에서는 KMS 키에 대해 지역 제한을 적용합니다. 이 지역 제한은 키가 Adobe 계정과 동일한 지역에 있어야 함을 의미합니다. Adobe은 계정 지역 내에 있는 KMS 키에만 액세스할 수 있습니다. 선택한 지역이 Adobe 단일 테넌트 계정 지역과 일치하는지 확인합니다.

![AWS 지역, KMS 및 단일 지역 키 고급 옵션이 강조 표시된 키 구성 워크플로의 첫 단계입니다.](../../../images/governance-privacy-security/key-management-service/configure-key-advanced-options.png)

## 키에 레이블 지정 및 태그 지정 {#add-labels-and-tags-to-key}

워크플로우의 두 번째 [!DNL Add labels] 단계가 나타납니다. 여기에서 [!DNL Alias] 및 [!DNL Tags] 필드를 구성하여 AWS KMS 콘솔에서 암호화 키를 관리하고 찾을 수 있습니다.

**[!DNL Alias]** 입력 필드에 키에 대한 설명 레이블을 입력합니다. 별칭은 사용자에게 친숙한 식별자 역할을 하며 AWS KMS 콘솔의 검색 창을 사용하여 키를 빠르게 찾습니다. 혼동을 방지하려면 &quot;Adobe-Experience-Platform-Key&quot; 또는 &quot;Customer-Encryption-Key&quot;와 같이 키의 목적을 반영하는 의미 있는 이름을 선택합니다. 키 별칭이 해당 용도를 설명하기에 충분하지 않은 경우 키에 대한 설명을 포함할 수도 있습니다.

마지막으로 [!DNL Tags] 섹션에서 키-값 쌍을 추가하여 키에 메타데이터를 할당합니다. 이 단계는 선택 사항이지만, 보다 쉬운 관리를 위해 AWS 리소스를 범주화하고 필터링할 태그를 추가해야 합니다. 예를 들어 조직에서 여러 Adobe 관련 리소스를 사용하는 경우 &quot;Adobe&quot; 또는 &quot;Experience-Platform&quot;으로 태그를 지정할 수 있습니다. 이 추가 단계를 사용하면 AWS Management Console에서 연결된 모든 리소스를 쉽게 검색하고 관리할 수 있습니다. 프로세스를 시작하려면 **[!DNL Add tag]**&#x200B;을(를) 선택하십시오.

<!-- I do not have an AWS account with which to document the Add tag process as yet. -->

설정에 만족하면 **[!DNL Next]**&#x200B;을(를) 선택하여 워크플로우를 계속합니다.

![별칭, 설명, 태그 및 다음을 강조 표시한 키 구성 워크플로의 2단계입니다.](../../../images/governance-privacy-security/key-management-service/add-labels.png)

## 주요 관리 권한 정의 {#define-key-admins}

키 만들기 워크플로의 3단계가 나타납니다. 안전하고 통제된 액세스를 보장하기 위해 IAM 사용자와 역할 중 키를 관리할 수 있는 사용자를 선택할 수 있습니다. 이 단계에는 [!DNL Key administrators]과(와) [!DNL Key deletion]의 두 가지 옵션이 있습니다. **[!DNL Key administrators]** 섹션에서 이 키에 대한 관리자 권한을 부여할 사용자 또는 역할의 이름 옆에 있는 확인란을 한 개 이상 선택합니다.

>[!NOTE]
>
>워크플로의 이 단계에서는 관리자를 만들 수 없습니다.

**[!DNL Key deletion]** 섹션에서 확인란을 활성화하여 키 관리자가 이 키를 삭제할 수 있는 권한을 허용합니다. 확인란을 선택하지 않으면 관리 사용자가 해당 작업을 수행할 수 없습니다.

워크플로우를 계속하려면 **[!DNL Next]**&#x200B;을(를) 선택하십시오.

![워크플로의 주요 관리 권한 단계를 정의하고 확인란 및 그 다음으로 강조 표시합니다.](../../../images/governance-privacy-security/key-management-service/define-key-admins.png)

## 주요 사용자에게 액세스 권한 부여 {#assign-key-users}

워크플로의 4단계에서 [!DNL Define key usage permissions]할 수 있습니다. **[!DNL Key users]** 목록에서 이 키를 사용할 권한을 가질 모든 IAM 사용자 및 역할에 대한 확인란을 선택합니다.

이 보기에서 [!DNL Add another AWS account]할 수도 있습니다. 그러나 다른 AWS 계정을 추가하는 것은 권장되지 않습니다. 다른 계정을 추가하면 위험이 발생하고 암호화 및 암호 해독 작업에 대한 권한 관리가 복잡해질 수 있습니다. Adobe은 단일 AWS 계정과 연결된 키를 유지함으로써 AWS KMS와의 안전한 통합을 보장하고 위험을 최소화하며 안정적인 운영을 보장합니다.

워크플로우를 계속하려면 **[!DNL Next]**&#x200B;을(를) 선택하십시오.

![워크플로의 키 사용 권한 정의 단계(확인란 포함)를 선택하고 그 다음에 강조 표시합니다.](../../../images/governance-privacy-security/key-management-service/define-key-users.png)

## 키 구성 검토 {#review}

주요 구성의 검토 단계가 나타납니다. [!DNL Key configuration] 및 [!DNL Alias and description] 섹션에서 키 세부 정보를 확인하십시오.

>[!NOTE]
>
>키 영역이 AWS 계정과 동일한지 확인합니다.

![주요 구성 및 별칭, 설명 섹션이 강조 표시된 워크플로의 검토 단계입니다.](../../../images/governance-privacy-security/key-management-service/review-key-configuration-details.png)

**[!DNL Confirm]**&#x200B;을(를) 선택하여 프로세스를 완료합니다. 사용 가능한 모든 키가 나열된 KMS 고객 관리 키 작업 영역으로 돌아갑니다.

## 다음 단계

AWS KMS가 구성되면 [!UICONTROL 플랫폼 암호화 구성] UI 또는 Adobe Experience Platform API를 사용하여 통합을 설정하십시오. 고객 관리 키 기능을 설정하는 1회 프로세스를 계속하려면 [UI 설정 안내서](./ui-set-up.md)를 계속 사용하십시오.
